---
title: Importera PFX-certifikatprofiler
titleSuffix: Configuration Manager
description: Lär dig hur du använder PFX-filer i Configuration Manager för att generera användarspecifika certifikat som stöder krypterat data utbyte.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e3bb3e13-3037-4122-93bc-504bfd080a4d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: df5dfdeab010012a258fe59612a348c269081c45
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700505"
---
# <a name="import-pfx-certificate-profiles"></a>Importera PFX-certifikatprofiler

*Gäller för: Configuration Manager (aktuell gren)*

Lär dig hur du skapar en certifikat profil genom att importera autentiseringsuppgifter från externa certifikat. I den här artikeln beskrivs detaljerad information om PFX-certifikat (personal information Exchange). Mer information om hur du skapar och konfigurerar de här profilerna finns i [certifikat profiler](../../protect/deploy-use/introduction-to-certificate-profiles.md).

Configuration Manager stöder olika typer av certifikat Arkiv för olika enheter och OS-versioner. Till exempel Windows 10 och Windows 10 Mobile. Mer information finns i [krav för certifikat profiler](../../protect/plan-design/prerequisites-for-certificate-profiles.md).

Använd Configuration Manager för att importera autentiseringsuppgifter för certifikatet och etablera sedan PFX-filer till enheter. Du kan använda dessa filer för att generera användarspecifika certifikat som stöd för krypterad data utbyte.

> [!TIP]  
> En stegvis genom gång av den här processen finns i blogg inlägget [så här skapar och distribuerar du PFX-certifikat profiler i Configuration Manager](/archive/blogs/karanrustagi/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager).  

## <a name="create-a-profile"></a>Skapa en profil

1. Gå till arbets ytan **till gångar och efterlevnad** i Configuration Manager-konsolen **, expandera kompatibilitetsinställningar, expandera** **åtkomst till företags resurser**och välj sedan **certifikat profiler**.

1. På fliken **Start** i menyfliksområdet väljer du **Skapa certifikat profil**i gruppen **skapa** .

1. På sidan **Allmänt** i **guiden Skapa certifikat profil**anger du följande information:  

    - **Namn**: Ange ett unikt namn för certifikatprofilen. Använd högst 256 tecken.  

    - **Beskrivning**: Ange en beskrivning som ger en översikt över certifikat profilen som hjälper dig att identifiera den i Configuration Manager-konsolen. Använd högst 256 tecken.  

1. Välj **personal information Exchange – inställningar för PKCS #12 (pfx) – importera**. Det här alternativet importerar information från ett befintligt certifikat för att skapa en certifikat profil.

    > [!NOTE]
    > Alternativet **skapa** begär ett certifikat för en användares räkning från en ansluten lokal certifikat utfärdare (ca). Den här processen levererar sedan certifikatet till klienter som PFX-filer på ett säkert sätt. Mer information finns i [Skapa PFX-certifikat profiler med en certifikat utfärdare](create-pfx-certificate-profiles.md).

1. På sidan **PFX-certifikat** i **guiden Skapa certifikat profil**anger du enhets nyckel lagrings leverantör (KSP):

    - **Installera till TPM (Trusted Platform Module) om den är tillgänglig**  
    - **Installera till Trusted Platform Module (TPM), rapportera annars ett problem**
    - **Installera på Windows Hello för företag, rapportera annars ett problem**
    - **Installera till programvaruprovidern för nyckellagring**

1. På sidan **plattformar som stöds** väljer du de plattformar som stöds.

1. Slutför guiden.

## <a name="deploy-the-profile"></a>Distribuera profilen

När du har skapat och förkonfigurerat en certifikat profil är den nu tillgänglig i noden **certifikat profiler** . Mer information om hur du distribuerar det finns i [distribuera resurs åtkomst profiler](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md).

## <a name="assign-primary-users"></a>Tilldela primära användare

Tilldela mål användarna som primära användare på Windows 10-enheter där du behöver installera PFX-certifikaten. Mer information finns i [mappning mellan användare och enhet](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

## <a name="provision-a-create-pfx-script"></a>Etablera ett Create PFX-skript

Om du vill importera ett PFX-certifikat använder du följande Configuration Manager PowerShell-cmdletar för att etablera ett Create PFX-skript:

- [Get-CMClientCertificatePfx](/powershell/module/configurationmanager/get-cmclientcertificatepfx?view=sccm-ps)
- [Importera – CMClientCertificatePfx](/powershell/module/configurationmanager/import-cmclientcertificatepfx?view=sccm-ps)
- [Remove-CMClientCertificatePfx](/powershell/module/configurationmanager/remove-cmclientcertificatepfx?view=sccm-ps)

### <a name="example-script"></a>Exempelskript

Om du vill etablera en PFX-fil till en certifikat profil för en användare öppnar du PowerShell på en dator med Configuration Manager-konsolen. Ändra variablerna med värden från din miljö.

``` PowerShell
# The display name of your PFX Import certificate profile
$PfxProfileDisplayName = "ImportPFX"

# The password you used to protect/encrypt the external PFX file that was created/exported from your certificate storage provider
# If you omit this password, PowerShell will securely prompt you for it. You can specify it as a parameter for process automation.
$password = ""

# The username of the user who will receive this PFX certificate on their device
$user = "Melissa"

# The full path to the PFX file you exported from the certificate store
$pfxfile = "c:\p1.pfx"

# If the target user isn't in the same domain as the user running this script, specify a different domain
Import-CMClientCertificatePfx -UserName "$env:USERDOMAIN\$user" -Password (ConvertTo-SecureString -String $password -AsPlainText -Force) -CertificateProfilePfx (Get-CMCertificateProfilePfx -Fast -Name $PfxProfileDisplayName) -Path $pfxfile
```

## <a name="see-also"></a>Se även

[Skapa en ny certifikat profil](../../protect/deploy-use/create-certificate-profiles.md)

[Skapa PFX-certifikat profiler med en certifikat utfärdare](create-pfx-certificate-profiles.md)

[Distribuera Wi-Fi-, VPN-, e-post- och certifikatprofiler](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)