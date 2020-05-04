---
title: Skapa PFX-certifikatprofiler
titleSuffix: Configuration Manager
description: Lär dig hur du använder PFX-filer i Configuration Manager för att generera användarspecifika certifikat som stöder krypterat data utbyte.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: d240a836-c49b-49ab-a920-784c062d6748
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b45474484629b437f2548fb375075cfe55275ee2
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711177"
---
# <a name="create-pfx-certificate-profiles-using-a-certificate-authority"></a>Skapa PFX-certifikat profiler med en certifikat utfärdare

*Gäller för: Configuration Manager (aktuell gren)*

Lär dig hur du skapar en certifikat profil som använder en certifikat utfärdare för autentiseringsuppgifter. I den här artikeln beskrivs detaljerad information om PFX-certifikat (personal information Exchange). Mer information om hur du skapar och konfigurerar de här profilerna finns i [certifikat profiler](../../protect/deploy-use/introduction-to-certificate-profiles.md).

Med Configuration Manager kan du skapa en PFX-certifikat profil med autentiseringsuppgifter som utfärdats av en certifikat utfärdare. Du kan välja Microsoft eller Entrust som certifikat utfärdare. När de distribueras till användar enheter genererar PFX-filer användarspecifika certifikat för att stödja krypterade data utbyte.

Information om hur du importerar autentiseringsuppgifter för certifikatet från befintliga certifikatfiler finns i [Importera PFX-certifikat profiler](import-pfx-certificate-profiles.md).

## <a name="prerequisites"></a>Krav

Innan du börjar skapa en certifikat profil kontrollerar du att nödvändiga komponenter är klara. Mer information finns i [krav för certifikat profiler](../../protect/plan-design/prerequisites-for-certificate-profiles.md). För PFX-certifikat profiler behöver du till exempel en plats system roll för [certifikat registrering](../../protect/deploy-use/certificate-infrastructure.md#step-2---install-and-configure-the-certificate-registration-point) .

## <a name="create-a-profile"></a>Skapa en profil  

1. Gå till arbets ytan **till gångar och efterlevnad** i Configuration Manager-konsolen **, expandera kompatibilitetsinställningar, expandera** **åtkomst till företags resurser**och välj sedan **certifikat profiler**.

1. På fliken **Start** i menyfliksområdet väljer du **Skapa certifikat profil**i gruppen **skapa** .

1. På sidan **Allmänt** i **guiden Skapa certifikat profil**anger du följande information:  

    - **Namn**: Ange ett unikt namn för certifikatprofilen. Använd högst 256 tecken.  

    - **Beskrivning**: Ange en beskrivning som ger en översikt över certifikat profilen som hjälper dig att identifiera den i Configuration Manager-konsolen. Använd högst 256 tecken.  

1. Välj **personal information Exchange – inställningar för PKCS #12 (pfx) – skapa**. Det här alternativet begär ett certifikat för en användares räkning från en ansluten lokal certifikat utfärdare (CA). Välj certifikat utfärdare: **Microsoft** eller **Entrust DataCard**.

    > [!NOTE]
    > **Import** alternativet hämtar information från ett befintligt certifikat för att skapa en certifikat profil. Mer information finns i [Importera PFX-certifikat profiler](import-pfx-certificate-profiles.md).

1. På sidan **plattformar som stöds** väljer du de OS-versioner som certifikat profilen stöder. Mer information om operativ system versioner som stöds för din version av Configuration Manager finns i [OS-versioner som stöds för klienter och enheter](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md).

1. På sidan **certifikat utfärdare** väljer du certifikat registrerings plats (CRP) för att bearbeta PFX-certifikaten:

    1. **Primär plats**: Välj den server som innehåller CRP-rollen för certifikat utfärdaren.
    1. **Certifikat utfärdare**: Välj relevant certifikat utfärdare.

    Mer information finns i [certifikat infrastruktur](../../protect/deploy-use/certificate-infrastructure.md).

Inställningarna på sidan **PFX-certifikat** varierar beroende på vald ca på sidan **Allmänt** :

- [Microsoft CA](#bkmk_microsoft)
- [Entrust Datacard CA](#bkmk_entrust)

### <a name="configure-pfx-certificate-settings-for-microsoft-ca"></a><a name="bkmk_microsoft"></a>Konfigurera inställningar för **PFX-certifikat** för Microsoft ca

1. Välj certifikat mal len för **certifikatmallens namn**.

1. Aktivera **certifikat användning**om du vill använda certifikat profilen för S/MIME-signering eller kryptering.

    När du aktiverar det här alternativet levererar det alla PFX-certifikat som är kopplade till mål användaren till alla deras enheter. Om du inte aktiverar det här alternativet får varje enhet ett unikt certifikat.  

1. Ange **format för ämnes namn** till antingen ett **eget** namn eller ett **fullständigt unikt namn**. Kontakta CA-administratören om du är osäker på vilken du ska använda.

1. För **Alternativt namn**på certifikat mottagare aktiverar du **e-postadress** och **användar namn (UPN)** som passar din certifikat utfärdare.

1. **Tröskelvärde för förnyelse**: fastställer när certifikat förnyas automatiskt, baserat på den procent andel av tiden som återstår innan den upphör att gälla.

1. Ange **certifikatets giltighets period** som certifikatets livs längd.

1. När certifikat registrerings platsen anger Active Directory autentiseringsuppgifter aktiverar **Active Directory publicering**.

1. Om du har valt en eller flera plattformar som stöds av Windows 10:

    1. Ange **Windows certifikat Arkiv** till **användare**. (Alternativet **lokal dator** distribuerar inte certifikat, Välj det inte.)

    1. Välj en av följande **nyckel lagrings leverantör (KSP)**:

        - **Installera till TPM (Trusted Platform Module) om den är tillgänglig**  
        - **Installera till Trusted Platform Module (TPM), rapportera annars ett problem**
        - **Installera på Windows Hello för företag, rapportera annars ett problem**
        - **Installera till programvaruprovidern för nyckellagring**

1. Slutför guiden.

### <a name="configure-pfx-certificate-settings-for-entrust-datacard-ca"></a><a name="bkmk_entrust"></a>Konfigurera inställningar för **PFX-certifikat** för Entrust DataCard ca

1. För **konfiguration av digitalt ID**väljer du konfigurations profilen. Hanteraren för administratör skapar konfigurations alternativen för digitalt ID.

1. Aktivera **certifikat användning**om du vill använda certifikat profilen för S/MIME-signering eller kryptering.

    När du aktiverar det här alternativet levererar det alla PFX-certifikat som är kopplade till mål användaren till alla deras enheter. Om du inte aktiverar det här alternativet får varje enhet ett unikt certifikat.  

1. Om du vill mappa Entrust **subject Name format** -token till Configuration Manager fält väljer du **format**.

    I dialog rutan **certifikat namns formatering** visas variablerna för att konfigurera digitala ID-konfigurationer. För varje Entrust-variabel väljer du lämpliga Configuration Manager fält.

1. Om du vill mappa **ett alternativt namn** -token för certifikat mottagare till LDAP-variabler som stöds väljer du **format**.

    I dialog rutan **certifikat namns formatering** visas variablerna för att konfigurera digitala ID-konfigurationer. Välj lämplig LDAP-variabel för varje Entrust-variabel.

1. **Tröskelvärde för förnyelse**: fastställer när certifikat förnyas automatiskt, baserat på den procent andel av tiden som återstår innan den upphör att gälla.

1. Ange **certifikatets giltighets period** som certifikatets livs längd.

1. När certifikat registrerings platsen anger Active Directory autentiseringsuppgifter aktiverar **Active Directory publicering**.

1. Om du har valt en eller flera plattformar som stöds av Windows 10:

    1. Ange **Windows certifikat Arkiv** till **användare**. (Alternativet **lokal dator** distribuerar inte certifikat, Välj det inte.)

    1. Välj en av följande **nyckel lagrings leverantör (KSP)**:

        - **Installera till TPM (Trusted Platform Module) om den är tillgänglig**  
        - **Installera till Trusted Platform Module (TPM), rapportera annars ett problem**
        - **Installera på Windows Hello för företag, rapportera annars ett problem**
        - **Installera till programvaruprovidern för nyckellagring**

1. Slutför guiden.

## <a name="deploy-the-profile"></a>Distribuera profilen

När du har skapat en certifikat profil är den nu tillgänglig i noden **certifikat profiler** . Mer information om hur du distribuerar det finns i [distribuera resurs åtkomst profiler](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md).

## <a name="see-also"></a>Se även

[Skapa en ny certifikat profil](../../protect/deploy-use/create-certificate-profiles.md)

[Importera PFX-certifikatprofiler](import-pfx-certificate-profiles.md)

[Distribuera Wi-Fi-, VPN-, e-post- och certifikatprofiler](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)
