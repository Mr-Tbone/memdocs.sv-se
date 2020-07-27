---
title: Använda importerade PFX-certifikat i Microsoft Intune – Azure | Microsoft Docs
description: Använda importerade PKCS-certifikat (Public Key Cryptography Standards) med Microsoft Intune. Importera certifikat, konfigurera certifikatmallar, installera det Intune-importerade PFX-certifikatanslutningsprogrammet och skapa en importerad profil för PKCS-certifikatet.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/29/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: lacranda; rimarram
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: d09f3a2e734709f769aebcd4e8aab4fec774d4fc
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/18/2020
ms.locfileid: "86461835"
---
# <a name="configure-and-use-imported-pkcs-certificates-with-intune"></a>Konfigurera och använda importerade PKCS-certifikat med Intune

Microsoft Intune stöder användningen av importerade PKCS-certifikat (certifikat med offentlig nyckel-par), som vanligtvis används för S/MIME-kryptering med e-postprofiler. Vissa e-postprofiler i Intune stöder ett alternativ för att aktivera S/MIME där du kan definiera ett S/MIME-signeringscertifikat och S/MIME-krypteringscertifikat.

S/MIME-kryptering är en utmaning eftersom e-post krypteras med ett specifikt certifikat:

- Du måste ha den privata nyckeln för certifikatet som krypterade e-postmeddelandet på enheten där du läser e-postmeddelandet så att den kan dekrypteras.
- Innan ett certifikat på en enhet upphör, bör du importera ett nytt certifikat så att enheterna kan fortsätta att dekryptera nya e-postmeddelanden. Det finns inte stöd för att förnya dessa certifikat.
- Krypteringscertifikat förnyas regelbundet, vilket innebär att du kan behålla gamla certifikat på dina enheter så att äldre e-postmeddelanden fortsätter att dekrypteras.  

Eftersom samma certifikat måste användas på olika enheter kan du inte använda [SCEP](certificates-scep-configure.md)- eller [PKCS](certficates-pfx-configure.md)-certifikatprofiler för detta ändamål, eftersom dessa certifikatleveransmetoder levererar unika certifikat per enhet.

Mer information om användning av S/MIME med Intune finns i [Använda S/MIME för att kryptera e-post](certificates-s-mime-encryption-sign.md).

## <a name="supported-platforms"></a>Plattformar som stöds

Intune stöder import av PFX-certifikat för följande plattformar:

- Android – enhetsadministratör
- Android Enterprise – fullständigt hanterad
- Android Enterprise – arbetsprofil
- Android Enterprise – företagsägd arbetsprofil
- iOS/iPadOS
- macOS
- Windows 10

## <a name="requirements"></a>Krav

Om du vill använda importerade PKCS-certifikat med Intune behöver du följande infrastruktur:

- **PFX-certifikatanslutningsprogram för Microsoft Intune**:

  Varje Intune-klient har stöd för en enda instans av den här anslutningen. Du kan installera den här anslutningen på samma server som en instans av Microsoft Intune Certificate Connector.

  Anslutningsappen hanterar begäranden för PFX-filer som importeras till Intune för S/MIME-kryptering av e-post för en specifik användare.

  Den här anslutningsappen kan uppdatera sig automatiskt när nya versioner blir tillgängliga. Om du vill använda uppdateringsfunktionen måste du se till att brandväggarna är öppna så att anslutningsappen tillåts kontakta **autoupdate.msappproxy.net** på port **443**.

  Mer information finns i [Nätverksslutpunkter för Microsoft Intune](../fundamentals/intune-endpoints.md) och [Krav för Intune-nätverkskonfiguration och bandbredd](../fundamentals/network-bandwidth-use.md).

- **Windows Server**:

  Du använder Windows Server som värd för PFX-certifikatanslutningsappen för Microsoft Intune.  Anslutningsappen används för att bearbeta begäranden för certifikat som importerats till Intune.
  
  Anslutningsappen måste ha åtkomst till samma portar som för hanterade enheter. Dessa beskrivs i vår [information om slutpunkter för enheter](https://docs.microsoft.com/intune/fundamentals/intune-endpoints#access-for-managed-devices).

  Intune stöder installation av *Microsoft Intune Certificate Connector* på samma server som *PFX-certifikatanslutningsappen för Microsoft Intune*.

  För att stödja anslutningsappen måste servern köra .NET 4.6 Framework eller senare. Om .NET 4.6 Framework inte är installerad när du startar installationen av installeras det av anslutningsappens installation automatiskt.

- **Visual Studio 2015 eller senare** (valfritt):

  Du använder Visual Studio för att bygga PowerShell-hjälpmodulen med cmdletar för import av PFX-certifikat till Microsoft Intune. Information om hur du hämtar PowerShell-hjälp-cmdletar finns i [PFXImport PowerShell Project på GitHub](https://github.com/microsoft/Intune-Resource-Access/tree/develop/src/PFXImportPowershell).

## <a name="how-it-works"></a>Så här fungerar det

När du använder Intune för att distribuera ett **importerat PFX-certifikat** till en användare finns det två komponenter i spel utöver enheten:

- **Intune-tjänsten**: Lagrar PFX-certifikaten i ett krypterat tillstånd och hanterar distributionen av certifikatet till användarenheten.  Lösenorden som skyddar de privata nycklarna för certifikaten krypteras innan de laddas upp med hjälp av antingen en modul för maskinvarusäkerhet (HSM) eller Windows-kryptografi, vilket säkerställer att Intune inte kan komma åt den privata nyckeln när som helst.

- **PFX-certifikatanslutningsprogram för Microsoft Intune**: När en enhet begär ett PFX-certifikat som har importerats till Intune skickas det krypterade lösenordet, certifikatet och enhetens offentliga nyckel till anslutningsappen.  Anslutningsappen dekrypterar lösenordet med hjälp av den lokala privata nyckeln och krypterar sedan lösenordet på nytt (och eventuella plist-profiler om du använder iOS) med enhetsnyckeln innan certifikatet skickas tillbaka till Intune.  Intune levererar sedan certifikatet till enheten och enheten kan dekryptera det med enhetens privata nyckel och installera certifikatet.

## <a name="download-install-and-configure-the-pfx-certificate-connector-for-microsoft-intune"></a>Ladda ned, installera och konfigurera PFX-certifikatanslutningsappen för Microsoft Intune

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Välj **Administration av klientorganisation** > **Anslutning och token** > **Certifikatanslutningsprogram** > **Lägg till**.

   ![Ladda ned PFX-certifikatanslutningsappen för Microsoft Intune](./media/certificates-imported-pfx-configure/download-imported-pfxconnector.png)

3. Följ anvisningarna för att ladda ned *PFX-certifikatanslutningsappen för Microsoft Intune* till en plats som är åtkomlig från servern där du kommer att installera anslutningsappen.

4. När nedladdningen har slutförts loggar du in på servern och kör installationsprogrammet (PfxCertificateConnectorBootstrapper.exe).  
   - När du accepterar standardinstallationsplatsen installeras anslutningsappen i `Program Files\Microsoft Intune\PFXCertificateConnector`.
   - Anslutningsapptjänsten körs under det lokala systemkontot. Om en proxy krävs för Internetåtkomst kontrollerar du att det lokala tjänstkontot kan komma åt proxyinställningarna på servern.

5. PFX-certifikatanslutningsappen för Microsoft Intune öppnar fliken **Registrering** efter installationen. Om du vill aktivera anslutningen till Intune **loggar du in** och anger ett konto med behörigheter för global Azure-administratör eller Intune-administratör.

   > [!WARNING]
   > Som standard är **Förbättrad säkerhetskonfiguration i IE** i Windows Server inställt på **På** som kan orsaka problem med inloggningen till Office 365.

6. Stäng fönstret.

7. I administrationscentret för Microsoft Endpoint Manager går du tillbaka till **Administration av klientorganisation** > **Anslutning och token** > **Certifikatanslutningsprogram**. Efter en stund visas en grön bockmarkering och anslutningsstatusen uppdateras. Anslutningsservern kan nu kommunicera med Intune.

## <a name="import-pfx-certificates-to-intune"></a>Importera PFX-certifikat till Intune

Du använder [Microsoft Graph](https://docs.microsoft.com/graph) för att importera dina användares PFX-certifikat till Intune. Hjälpkomponenten [PFXImport PowerShell Project på GitHub](https://github.com/microsoft/Intune-Resource-Access/tree/develop/src/PFXImportPowershell) ger dig cmdletar för att utföra åtgärderna enkelt.

Om du föredrar att använda en egen anpassad lösning med hjälp av Graph använder du [resurstypen userPFXCertificate](https://docs.microsoft.com/graph/api/resources/intune-raimportcerts-userpfxcertificate?view=graph-rest-beta).

### <a name="build-pfximport-powershell-project-cmdlets"></a>Bygg PFXImport PowerShell Project-cmdletar

Om du vill använda PowerShell-cmdletarna bygger du projektet själv med hjälp av Visual Studio. Processen är enkel och kan köras på servern, men vi rekommenderar att du kör den på din arbetsstation.  

1. Gå till roten på lagringsplatsen [Intune-Resource-Access](https://github.com/microsoft/Intune-Resource-Access) på GitHub och ladda sedan ned eller klona lagringsplatsen med Git på din dator.

   ![GitHub-nedladdningsknappen](./media/certificates-imported-pfx-configure/github-download.png)

2. Gå till `.\Intune-Resource-Access-develop\src\PFXImportPowershell\` och öppna projektet med Visual Studio med hjälp av filen **PFXImportPS.sln**.

3. Ändra **Debug** till **Release**.

4. Gå till **Build** och välj **Build PFXImportPS**. Efter en stund ser du bekräftelsen **Build succeeded** längst ned till vänster i Visual Studio.

   ![Build-alternativet i Visual Studio](./media/certificates-imported-pfx-configure/vs-build-release.png)

5. Byggprocessen skapar en ny mapp med PowerShell-modulen i `.\Intune-Resource-Access-develop\src\PFXImportPowershell\PFXImportPS\bin\Release`.

   Du använder den här **Release**-mappen för nästa steg.

### <a name="create-the-encryption-public-key"></a>Skapa den offentliga nyckeln för kryptering

Du importerar PFX-certifikat och deras privata nycklar till Intune. Lösenordet som skyddar den privata nyckeln krypteras med en offentlig nyckel som lagras lokalt. Du kan använda Windows-kryptografi, en modul för maskinvarusäkerhet eller en annan typ av kryptografi för att generera och lagra offentlig/privat nyckel-paren.  Beroende på vilken typ av kryptografi som används kan offentlig/privat nyckel-paret exporteras i ett filformat för säkerhetskopiering.

PowerShell-modulen tillhandahåller metoder för att skapa en nyckel med Windows-kryptografi. Du kan också använda andra verktyg för att skapa en nyckel.  

#### <a name="to-create-the-encryption-key-using-windows-cryptography"></a>Så här skapar du krypteringsnyckeln med Windows-kryptografi

1. Kopiera *Release*-mappen som har skapats av Visual Studio till servern där du har installerat **PFX-certifikatanslutningsappen för Microsoft Intune**. Den här mappen innehåller PowerShell-modulen.

2. Öppna *PowerShell* på servern som administratör och gå sedan till *Release*-mappen som innehåller PowerShell-modulen.

3. Kör `Import-Module .\IntunePfxImport.psd1` för att importera modulen.

4. Kör sedan `Add-IntuneKspKey -ProviderName "Microsoft Software Key Storage Provider" -KeyName "PFXEncryptionKey"`

   > [!TIP]
   > Providern du använder måste väljas igen när du importerar PFX-certifikat. Du kan använda **Microsoft-programvaruprovidern för nyckellagring** men den stöds för att använda en annan provider. Nyckelnamnet anges också som ett exempel och du kan välja ett annat nyckelnamn.

   Om du planerar att importera certifikatet kan du exportera den här nyckeln till en fil med följande kommando: `Export-IntunePublicKey -ProviderName "<ProviderName>" -KeyName "<KeyName>" -FilePath "<File path\Filename.PFX>"`

   Den privata nyckeln måste importeras på servern som är värd för PFX-certifikatanslutningsappen för Microsoft Intune så att importerade PFX-certifikat kan bearbetas korrekt.

#### <a name="to-use-a-hardware-security-module-hsm"></a>Använda en modul för maskinvarusäkerhet (HSM)

Du kan använda en modul för maskinvarusäkerhet (HSM) för att generera och lagra offentlig/privat nyckel-paret. Mer information finns i HSM-providerns dokumentation.

### <a name="import-pfx-certificates"></a>Importera PFX-certifikat

I följande process används PowerShell-cmdletarna som ett exempel på hur du importerar PFX-certifikaten. Du kan välja olika alternativ beroende på dina krav.

Alternativen är:

- Avsett syfte (grupperar certifikat baserat på en tagg):
  - unassigned
  - smimeEncryption
  - smimeSigning

- Utfyllnadsschema:
  - oaepSha256
  - oaepSha384
  - oaepSha512

Välj den nyckellagrinsprovider som matchar providern du använde för att skapa nyckeln.

#### <a name="to-import-the-pfx-certificate"></a>Så här importerar du PFX-certifikatet  

1. Exportera certifikaten från en certifikatutfärdare (CA) genom att följa dokumentationen från providern.  För Microsoft Active Directory-certifikattjänster kan du använda [det här exempelskriptet](https://gallery.technet.microsoft.com/Export-CMPfxCertificatesFro-d55f687b).

2. Öppna *PowerShell* på servern som administratör och gå sedan till *Release*-mappen som innehåller PowerShell-modulen.

3. Kör `Import-Module .\IntunePfxImport.psd1` för att importera modulen

4. Kör `Set-IntuneAuthenticationToken  -AdminUserName "<Admin-UPN>"` för autentisera till Intune Graph

   > [!NOTE]
   > Då autentiseringen körs mot Graph måste du ange behörigheter för AppID. Om det är först gången du använder det här verktyget krävs en *global administratör*. PowerShell-cmdletarna använder samma AppID som den som används med [PowerShell Intune-exempel](https://github.com/microsoftgraph/powershell-intune-samples).

5. Konvertera lösenordet för varje PFX-fil du importerar till en säker sträng genom att köra `$SecureFilePassword = ConvertTo-SecureString -String "<PFXPassword>" -AsPlainText -Force`.

6. Om du vill skapa ett **UserPFXCertificate**-objekt kör du `$userPFXObject = New-IntuneUserPfxCertificate -PathToPfxFile "<FullPathPFXToCert>" $SecureFilePassword "<UserUPN>" "<ProviderName>" "<KeyName>" "<IntendedPurpose>"`

   Exempelvis: `$userPFXObject = New-IntuneUserPfxCertificate -PathToPfxFile "C:\temp\userA.pfx" $SecureFilePassword "userA@contoso.com" "Microsoft Software Key Storage Provider" "PFXEncryptionKey" "smimeEncryption"`

   > [!NOTE]
   > När du importerar certifikatet från ett annat system än servern där anslutningsappen är installerad måste du använda följande kommando som innehåller nyckelfilsökvägen: `$userPFXObject = New-IntuneUserPfxCertificate -PathToPfxFile "<FullPathPFXToCert>" $SecureFilePassword "<UserUPN>" "<ProviderName>" "<KeyName>" "<IntendedPurpose>" "<PaddingScheme>" "<File path to public key file>"`
   >
   > *VPN* kan inte användas som IntendedPurpose. 


7. Importera **UserPFXCertificate**-objektet till Intune genom att köra `Import-IntuneUserPfxCertificate -CertificateList $userPFXObject`

8. Validera certifikatet som har importerats genom att köra `Get-IntuneUserPfxCertificate -UserList "<UserUPN>"`

9.  Vi rekommenderar att du rensar AAD-tokencachen utan att vänta på att den ska upphöra av sig själv, genom att köra `Remove-IntuneAuthenticationToken`

Mer information om andra tillgängliga kommandon finns i readme-filen i [PFXImport PowerShell Project på GitHub](https://github.com/microsoft/Intune-Resource-Access/tree/develop/src/PFXImportPowershell).

## <a name="create-a-pkcs-imported-certificate-profile"></a>Skapa en PKCS-importerad certifikatprofil

När du har importerat certifikaten till Intune skapar du en profil för **PKCS-importerat certifikat** och tilldelar den till Azure Active Directory-grupper.

> [!NOTE]
> När du har skapat en PKCS-importerad certifikatprofil är värdena för **Avsett syfte** och **Key Storage Provider** (KSP) i profilen skrivskyddade och kan inte redigeras. Om du behöver ett annat värde för någon av dessa inställningar skapar och distribuerar du en ny profil. 

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Välj och gå till **Enheter** > **Konfigurationsprofiler** > **Skapa profil**.

3. Ange följande egenskaper:
   - **Plattform**: Välj plattform för dina enheter.
   - **Profil**: Välj **PKCS-importerat certifikat**

4. Välj **Skapa**.

5. Ange följande egenskaper i **Grundinställningar**:
   - **Namn**: Ange ett beskrivande namn på profilen. Namnge dina profiler så att du enkelt kan identifiera dem senare. Ett exempel på ett bra profilnamn är *PKCS imported certificate profile for entire company* (PKCS-importerad certifikatprofil för hela företaget).
   - **Beskrivning**: Ange en beskrivning av profilen. Denna inställning är valfri, men rekommenderas.

6. Välj **Nästa**.

7. Välj **Konfigurationsinställningar** och ange följande egenskaper:

   - **Avsett syfte**: Ange syftet med de certifikat som har importerats för den här profilen. Administratörer kan importera certifikat med olika syften (till exempel S/MIME-signering eller S/MIME-kryptering). Avsett syfte som valts i certifikatprofilen matchar certifikatprofilen med rätt importerade certifikat. Avsett syfte är en tagg för att gruppera importerade certifikat och garanterar inte att certifikat som importerats med den taggen uppfyller det avsedda syftet.  

   <!-- Not in new UI:
   - **Certificate validity period**: Unless the validity period was changed in the certificate template, this option defaults to one year.
   -->
   - **Nyckellagringsprovider (KSP)** : För Windows väljer du var du vill lagra nycklarna på enheten.

8. Välj **Nästa**.

9. Under **Omfångstaggar** (valfritt), tilldelar du en tagg för att filtrera profilen till specifika IT-grupper, till exempel `US-NC IT Team` eller `JohnGlenn_ITDepartment`. Mer information om omfångstaggar finns i [Använda RBAC och omfångstaggar för distribuerad IT](../fundamentals/scope-tags.md).

   Välj **Nästa**.

10. Under **Tilldelningar** väljer du de användare eller grupper som ska ta emot din profil. Mer information om hur du tilldelar profiler finns i [Tilldela användar- och enhetsprofiler](../configuration/device-profile-assign.md).

    Välj **Nästa**.

11. (*Gäller endast Windows 10*) I **Tillämplighetsregler** anger du tillämplighetsregler för att förfina tilldelningen av profilen. Du kan välja att tilldela eller inte tilldela profilen baserat på operativsystemversionen eller enhetsversionen.

    Mer information finns i [Tillämplighetsregler](../configuration/device-profile-create.md#applicability-rules) i *Skapa en enhetsprofil i Microsoft Intune*.

    Välj **Nästa**.

12. Granska inställningarna under **Granska + skapa**. När du väljer Skapa sparas dina ändringar och profilen tilldelas. Principen visas också i profillistan.

## <a name="support-for-third-party-partners"></a>Support för partner från tredje part

Följande partners erbjuder metoder och verktyg som du kan använda för att importera PFX-certifikat till Intune.

### <a name="digicert"></a>DigiCert

Om du använder DigiCert PKI-plattformen kan du använda DigiCerts **importverktyg för Intune S/MIME-certifikat** när du importerar PFX-certifikat till Intune. Om du använder detta verktyg behöver du inte följa anvisningarna i avsnittet [Importera PFX-certifikat till Intune](#import-pfx-certificates-to-intune) tidigare i denna artikel.

Mer information om DigiCert-importverktyget, inklusive hur du hämtar verktyget, finns på https://knowledge.digicert.com/tutorials/microsoft-intune.html i kunskapsbasen för DigiCert.

### <a name="keytalk"></a>KeyTalk

Om du använder KeyTalk-tjänsten så kan du konfigurera deras tjänst att importera PFX-certifikat till Intune. När du slutfört integreringen så behöver du inte följa anvisningarna i avsnittet [Importera PFX-certifikat till Intune](#import-pfx-certificates-to-intune) som det står tidigare i denna artikel.

Mer information om KeyTalks integrering med Intune finns i https://keytalk.com/support i KeyTalk-kunskapsbasen.

## <a name="next-steps"></a>Nästa steg

Profilen har skapats, men den gör inte något än. [Tilldela](../configuration/device-profile-assign.md) den nya enhetsprofilen.
