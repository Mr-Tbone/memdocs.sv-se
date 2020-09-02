---
title: Felsök användning av PKCS-certifikatprofiler för att etablera certifikat till Microsoft Intune | Microsoft Docs
description: Felsök användning av privata och offentliga nyckelpar (PKCS) profiler av enheter för att begära certifikat för användning med Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/11/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: acc61df344cb4134a863d75fff517047e78d067d
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914794"
---
# <a name="troubleshoot-pkcs-certificate-deployment-in-microsoft-intune"></a>Felsök PKCS-certifikatdistribution i Microsoft Intune

Informationen i den här artikeln kan hjälpa dig att lösa flera vanliga problem när du distribuerar privata och PKCS-certifikat i Microsoft Intune. Innan felsökning bör du se till att du har slutfört följande uppgifter som finns i [Konfigurera och använd PKCS-certifikat med Intune](../protect/certficates-pfx-configure.md#export-the-root-certificate-from-the-enterprise-ca):

- Granska [kraven för att använda PKCS-certifikatprofiler](../protect/certficates-pfx-configure.md#requirements)
- Exportera rotcertifikatet från Enterprise-certifikatutfärdaren (CA)
- Konfigurera certifikatmallar på certifikatutfärdaren
- Installera och konfigurera Intunes certifikatkoppling
- Skapa och distribuera en betrodd certifikatprofil om du vill distribuera rotcertifikatet
- Skapa och distribuera en PKCS-certifikatprofil

Den vanligaste problemkällan med PKCS-certifikatprofiler har varit konfigurationen av PKCS-certifikatprofilen. Granska profilkonfigurationen och leta efter stavfel i servernamn eller fullständigt kvalificerade domännamn (FQDN) och bekräfta att **certifikatutfärdare** och **certifikatutfärdarens namn** stämmer.

- **Certifikatutfärdare**: Det interna FQDN för certifikatutfärdarens dator. Till exempel server1.domain.local.
- **Namn på certifikatutfärdare**: Certifikatutfärdarens namn som det visas i certifikatutfärdarens MMC. Leta under **Certifikatutfärdare (Lokal)**

Du kan använda [kommandoradsprogrammet certutil](/windows-server/administration/windows-commands/certutil) på CA:n för att bekräfta rätt namn för certifikatutfärdaren och certifikatutfärdarnamn.

## <a name="pkcs-communication-overview"></a>PKCS-kommunikationsöversikt

Följande bild innehåller en grundläggande översikt över distributionsprocessen för PKCS-certifikatet i Intune.

> [!div class="mx-imgBorder"]
> ![PKCS-certifikatprofilflöde](./media/troubleshoot-pkcs-certificate-profiles/pkcs-overview-graphic.png)

1. En administratör skapar en PKCS-certifikatprofil i Intune.
2. Intune-tjänsten begär att den lokala Intune-certifikatanslutningen skapar ett nytt certifikat för användaren.
3. Intune-certifikatkopplingen skickar en PFX-blob och en begäran till din Microsoft-certifikatutfärdare.
4. Certifikatutfärdaren utfärdar och skickar PFX-certifikatet tillbaka till Intune-certifikatkopplingen.
5. Intune-certifikatkopplingen laddar upp det krypterade PFX-användarcertifikatet till Intune.
6. Intune dekrypterar PFX-användarcertifikatet och omkrypterar det för enheten med enhetshanteringscertifikatet.  Intune skickar sedan PFX-användarcertifikatet till enheten.
7. Enheten rapporterar certifikatstatusen till Intune.

## <a name="data-and-log-files"></a>Data och loggfiler

Om du vill identifiera problem med arbetsflödet för kommunikation och certifikatsetablering granskar du loggfilerna från både serverinfrastrukturen och från enheter. Senare avsnitt för felsökning av PKCS-certifikatprofiler avser de loggfiler som refereras till i det här avsnittet.

- [Infrastruktur- och serverloggar](#logs-for-on-premises-infrastructure)

Enhetsloggar är beroende av enhetsplattformen:

- [iOS- och iPadOS](#logs-for-ios-and-ipados-devices)
- [Android](#logs-for-android-devices)
- [Windows](#logs-for-windows-devices)

### <a name="logs-for-on-premises-infrastructure"></a>Loggar för den lokala infrastrukturen
  
Den lokala infrastrukturen som stöder användning av PKCS-certifikatprofiler för certifikatdistributioner innehåller Microsoft Intune Certificate Connector, NDES som körs på en Windows-Server och certifikatutfärdaren.

Loggfilerna för dessa roller omfattar Windows-loggboken, certifikatkonsoler och olika loggfiler som är speciella för Intune Certificate Connector, NDES eller andra roller och åtgärder som ingår i den lokala infrastrukturen.

- **NDESConnector_date_time.svclog**:

  Den här loggen visar kommunikation från Microsoft Intune Certificate Connector till Intune-molnet. Du kan använda [visningsverktyget för tjänstspårning](/dotnet/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe) för att visa den här loggfilen.

  Relaterad registernyckel: *HKLM\SW\Microsoft\MicrosoftIntune\NDESConnector\ConnectionStatus*

  Plats: På servern som är värd för NDES på *%program_files%\Microsoft intune\ndesconnectorsvc\logs\logs*

- **CertificateRegistrationPoint_date_time.svclog**:

  I den här loggen visas NDES-principmodulen som tar emot och verifierar certifikatbegäranden. Du kan använda [visningsverktyget för tjänstspårning](/dotnet/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe) för att visa den här loggfilen.

  Plats: På servern som är värd för NDES på *%program_files%\Microsoft intune\ndesconnectorsvc\logs\logs*

- **NDESPlugin.log**:

  I den här loggen visas överföring av certifikatbegäranden till certifikatregistreringsplatsen och den resulterande verifieringen av dessa begäranden.

  Plats: På den server som är värd för NDES på *%program_files%\Microsoft Intune\NDESPolicyModule\logs*

- **Windows-programlogg**:

  Plats: På den server som är värd för NDES: Öppna Loggboken i Windows genom att köra **eventvwr.msc**

### <a name="logs-for-android-devices"></a>Loggar för Android-enheter

För enheter som kör Android använder du programloggfilen **OMADM.log** i **Företagsportalen för Android**. Innan du samlar in och granskar loggar måste [utförlig loggning](../user-help/use-verbose-logging-to-help-your-it-administrator-fix-device-issues-android.md) vara aktiverad. Återskapa sedan problemet.

Om du vill samla in OMADM.logs från en enhet, se [Ladda upp och skicka e-postloggar med en USB-kabel](../user-help/send-logs-to-your-it-admin-using-cable-android.md).

Du kan också [Ladda upp och skicka loggarna med e-post](../user-help/send-logs-to-your-it-admin-by-email-android.md#upload-and-email-logs-from-microsoft-intune-app) som stöd.

### <a name="logs-for-ios-and-ipados-devices"></a>Loggar för iOS- och iPadOS-enheter

För enheter som kör iOS/iPadOS använder du felsökningsloggar och **Xcode** som körs på en Mac-dator:

1. Anslut iOS/iPadOS-enheten till Mac och gå sedan till **Program** > **Verktyg** för att öppna konsolprogrammet.

2. Under **Åtgärd** väljer du **Inkludera informationsmeddelanden** och **Inkludera felsökningsmeddelanden**.

   ![Välj loggalternativ](../protect/media/troubleshoot-pkcs-certificate-profiles/message-options.png)

3. Återskapa problemet och spara loggarna i en textfil:
   1. Välj **Redigera** > **Välj alla** för att markera alla meddelanden på den aktuella skärmen. Välj sedan **Redigera** > **Kopiera** för att kopiera meddelandena till urklipp.
   2. Öppna TextEdit-programmet, klistra in de kopierade loggarna i en ny textfil och spara sedan filen.

Företagsportalloggen för iOS- och iPadOS-enheter innehåller inte information om PKCS-certifikatprofiler.

### <a name="logs-for-windows-devices"></a>Loggar för Windows-enheter

För enheter som kör Windows använder du händelseloggarna i Windows för att diagnosticera problem med registrering eller enhetshantering för enheter som du hanterar med Intune.

Öppna **Loggboken** > på enheten och gå sedan till **Program- och tjänstloggar** > **Microsoft** > **Windows** > **DeviceManagement-Enterprise-Diagnostic-Provider**

![Windows-händelseloggar](../protect/media/troubleshoot-pkcs-certificate-profiles/windows-event-log.png)

## <a name="antivirus-exclusions"></a>Undantag för antivirus

Överväg att lägga till undantag för antivirus på servrar som är värdar för NDES eller certifikatanslutningsprogrammet när:

- Certifikatbegäranden når servern eller Intune-certifikatanslutningsprogrammet men inte bearbetas korrekt 
- Certifikat utfärdas långsamt

Följande är exempel på platser som du kan undanta:

- *%program_files%* \Microsoft Intune\PfxRequest
- *%program_files%* \Microsoft Intune\CertificateRequestStatus
- *%program_files%* \Microsoft Intune\CertificateRevocationStatus

## <a name="common-errors"></a>Vanliga fel

Följande vanliga fel åtgärdas vart och ett i följande avsnitt:

- [RPC-servern är inte tillgänglig 0x800706ba](#the-rpc-server-is-unavailable-0x800706ba)
- [Det går inte att hitta en registreringsprincipserver 0x80094015](#an-enrollment-policy-server-cannot-be-located-0x80094015)
- [Sändningen väntar](#the-submission-is-pending)
- [Parametern är felaktig 0x80070057](#the-parameter-is-incorrect-0x80070057)
- [Nekad av principmodulen](#denied-by-policy-module)
- [Certifikatprofilen har fastnat som väntande](#certificate-profile-stuck-as-pending)
- [Fel – 2146875374 CERTSRV_E_SUBJECT_EMAIL_REQUIRED](#error--2146875374-certsrv_e_subject_email_required)

### <a name="the-rpc-server-is-unavailable-0x800706ba"></a>RPC-servern är inte tillgänglig 0x800706ba

Under PFX-distributionen visas det betrodda rotcertifikatet på enheten, men PFX-certifikatet visas inte på enheten. NDESConnector-loggfilen innehåller strängen **RPC-servern är inte tillgänglig. 0x800706ba**, som visas på den första raden i följande exempel:

```
IssuePfx - COMException: System.Runtime.InteropServices.COMException (0x800706BA): CCertRequest::Submit: The RPC server is unavailable. 0x800706ba (WIN32: 1722 RPC_S_SERVER_UNAVAILABLE)
IssuePfx -Generic Exception: System.ArgumentException: CCertRequest::Submit: The parameter is incorrect. 0x80070057 (WIN32: 87 ERROR_INVALID_PARAMETER)
IssuePfx - COMException: System.Runtime.InteropServices.COMException (0x80094800): The requested certificate template is not supported by this CA. (Exception from HRESULT: 0x80094800)
```

#### <a name="cause-1---incorrect-configuration-of-the-ca-in-intune"></a>Orsak 1 – felaktig konfiguration av CA:n i Intune

Det här problemet kan inträffa när en PKCS-certifikatprofil anger fel server eller innehåller stavfel för namnet eller FQDN för certifikatutfärdaren. Certifikatutfärdare anges i följande egenskaper för profilen:

- Certification authellerity
- Namn på certifikatutfärdare:

**Lösning**:

Granska följande inställningar och korrigera om de är felaktiga:

- Egenskapen **Certifikatutfärdare** visar den interna FQDN för din CA-server.
- Egenskapen **Namn på certifikatutfärdare** visar namnet på din certifikatutfärdare.

#### <a name="cause-2---ca-doesnt-support-certificate-renewal-for-requests-signed-by-previous-ca-certificates"></a>Orsak 2 – Certifikatutfärdaren stöder inte certifikatförnyelse för begäranden som signerats av tidigare CA-certifikat

Om CA FQDN och namn är korrekta i PKCS-certifikatprofilen, granskar du Windows-programloggen som finns på certifikatutfärdarens server. Sök efter en **Händelse-ID 128** som liknar följande exempel:

```
Log Name: Application:
Source: Microsoft-Windows-CertificationAuthority
Event ID: 128
Level: Warning
Details:
An Authority Key Identifier was passed as part of the certificate request 2268. This feature has not been enabled. To enable specifying a CA key for certificate signing, run: "certutil -setreg ca\UseDefinedCACertInRequest 1" and then restart the service.
```

När CA-certifikatet förnyas, måste det signera onlinecertifikatstatusprotokoll (OCSP) certifikatet för svarssignering. Signering gör att OCSP-certifikatet för svarssignering kan verifiera andra certifikat genom att kontrollera deras återkallningsstatus. Den här signeringen är inte aktiverad som standard.

**Lösning**:

Framtvinga signering av certifikatet manuellt:

1. På CA-servern öppnar du en förhöjd kommandotolk och kör följande kommando: **certutil-setreg ca\UseDefinedCACertInRequest 1**
2. Starta om Certificate Services-tjänsten.

När Certificate Services-tjänsten har startats om kan enheter ta emot certifikat.

### <a name="an-enrollment-policy-server-cannot-be-located-0x80094015"></a>Det går inte att hitta en registreringsprincipserver 0x80094015

**Det går inte att hitta en registreringsprincipserver** och **0x80094015**, som visas i följande exempel:

```
IssuePfx - COMException: System.Runtime.InteropServices.COMException (0x80094015): An enrollment policy server cannot be located. (Exception from HRESULT: 0x80094015)
```

#### <a name="cause---certificate-enrollment-policy-server-name"></a>Orsak – Namn på principserver för registrering av certifikat

Det här problemet uppstår om den dator som är värd för Intune NDES-kopplingen inte kan hitta en principserver för registrering av certifikat.

**Lösning**:

Konfigurera namnet på principservern för registrering av certifikat manuellt på den dator som är värd för NDES-kopplingen. Om du vill konfigurera namnet använder du PowerShell-cmdleten [Add-CertificateEnrollmentPolicyServer](/powershell/module/pkiclient/add-certificateenrollmentpolicyserver?view=win10-ps).

### <a name="the-submission-is-pending"></a>Sändningen väntar

När du har distribuerat en PKCS-certifikatfil till mobila enheter har certifikaten inte hämtats och NDESConnector-loggen innehåller strängen **Sändningen väntar**, som visas i följande exempel:

```
IssuePfx - The submission is pending: Taken Under Submission
IssuePfx -Generic Exception: System.InvalidOperationException: IssuePfx - The submission is pending
```

På certifikatutfärdarens server kan du dessutom se PFX-begäran i mappen **Väntande begäranden**:

> [!div class="mx-imgBorder"]
> ![Skärmbild av mappen Väntande begäranden för certifikatutfärdaren](./media/troubleshoot-pkcs-certificate-profiles/pending-requests.png)

#### <a name="cause---incorrect-configuration-for-request-handling"></a>Orsak – felaktig konfiguration för begärandehantering

Det här problemet uppstår om alternativet **Ange status för begäran till väntande. Administratören måste uttryckligen utfärda certifikatet** har markerats i certifikatutfärdarens dialogruta **Egenskaper** > **Principmodul** > **Egenskaper**.

> [!div class="mx-imgBorder"]
> ![Skärmbild av egenskaperna för principmodulen](./media/troubleshoot-pkcs-certificate-profiles/policy-module-properties.png)

**Lösning**:

Redigera egenskaperna för principmodulen för att ange: **Följ inställningarna i certifikatmallen, om tillämpligt. Annars utfärdas certifikatet automatiskt.**

### <a name="the-parameter-is-incorrect-0x80070057"></a>Parametern är felaktig 0x80070057

När Intune certifikatkopplingen har installerats och konfigurerats får enheterna inte några PKCS-certifikat och NDESConnector-loggen innehåller strängen **Parametern är felaktig. 0x80070057**, som visas i följande exempel:

```
CCertRequest::Submit: The parameter is incorrect. 0x80070057 (WIN32: 87 ERROR_INVALID_PARAMETER)
```

#### <a name="cause---configuration-of-the-pkcs-profile"></a>Orsak – konfiguration av PKCS-profilen

Det här problemet uppstår om PKCS-profilen i Intune är felkonfigurerad. Följande är vanliga felkonfigurationer:

- Profilen innehåller ett felaktigt namn för certifikatutfärdaren.
- Det alternativa namnet för subjektet (SAN) har konfigurerats för e-postadress, men målanvändaren har inte någon giltig e-postadress ännu. Den här kombinationen resulterar i ett null-värde för SAN, vilket är ogiltigt.

**Lösning**:

Verifiera följande konfigurationer för PKCS-profilen och vänta sedan på att principen ska uppdateras på enheten:

- Konfigurerat med namnet på certifikatutfärdaren
- Tilldelad till rätt användargrupp
- Användare i gruppen har giltiga e-postadresser

Mer information finns i [Konfigurera och använda PKCS-certifikat med Intune](../protect/certficates-pfx-configure.md).

### <a name="denied-by-policy-module"></a>Nekad av principmodulen

När enheter får det betrodda rotcertifikatet men inte tar emot PFX-certifikatet och NDESConnector-loggen innehåller strängen **Det inte gick att skicka in: Nekad av principmodulen**, som visas i följande exempel:

```
IssuePfx - The submission failed: Denied by Policy Module
IssuePfx -Generic Exception: System.InvalidOperationException: IssuePfx - The submission failed
   at Microsoft.Management.Services.NdesConnector.MicrosoftCA.GetCertificate(PfxRequestDataStorage pfxRequestData, String containerName, String& certificate, String& password)
Issuing Pfx certificate for Device ID <Device ID> failed  
```

#### <a name="cause--computer-account-permissions-to-the-certificate-template"></a>Orsak – datorkontobehörigheter till certifikatmallen

Det här problemet uppstår när datorkontot på den server som är värd för Intune certifikatkopplingen inte har behörighet till certifikatmallen.

**Lösning**:

1. Logga in på din Enterprise CA med ett konto som har administratörsbehörighet.
2. Öppna konsolen **Certifikatutfärdare**, högerklicka på **Certifikatmallar och välj Hantera**.
3. Leta upp certifikatmallen och öppna dialogrutan **Egenskaper** i mallen.
4. På fliken **Säkerhet**, lägger du till datorkontot för den server där du installerade Microsoft Intune certifikatkopplingen. Bevilja det här kontot **Läs-** och **Registrera**-behörigheter.
5. Välj **Tillämpa** > **OK** för att spara certifikatmallen och stäng sedan **Certifikatmallar**-konsolen.
6. I konsolen **Certifikatutfärdare** högerklickar du på **Certifikatmallar** > **Ny** > **Certifikatmall som ska utfärdas**.
7. Välj den mall som du ändrade och klicka sedan på **OK**.

Mer information finns i [Konfigurera certifikatmallar på certifikatutfärdaren](../protect/certficates-pfx-configure.md#configure-certificate-templates-on-the-ca).

### <a name="certificate-profile-stuck-as-pending"></a>Certifikatprofilen har fastnat som väntande

I administrationscenter för Microsoft Endpoint Manager kan inte PKCS-certifikatprofilerna distribueras med tillståndet **Väntar**. Det finns inga uppenbara fel i loggfilen för NDESConnector.
Eftersom orsaken till det här problemet inte har identifierats tydligt i loggarna, kan du gå igenom följande orsaker.

#### <a name="cause-1---unprocessed-request-files"></a>Orsak 1 – obearbetade begärandefiler

Granska begärandefilerna för fel som anger varför de inte kunde bearbetas.

1. På den dator som är värd för NDES-anslutningen använder du Utforskaren för att navigera till **%programfiles%\Microsoft Intune\PfxRequest**.
2. Granska filerna i mapparna **Misslyckade** och **Bearbetas** med hjälp av din textredigerare.

   > [!div class="mx-imgBorder"]
   > ![Granska mappen PfxRequest](./media/troubleshoot-pkcs-certificate-profiles/pfxrequest-folder.png)

3. Leta efter poster som indikerar fel eller antyder problem i de här filerna. Använd en webbaserad sökning och leta upp felmeddelandena för att få ledtrådar till varför begäran inte kunde bearbetas och för lösningar på problemen.

#### <a name="cause-2---misconfiguration-for-the-pkcs-certificate-profile"></a>Orsak 2 – felaktig konfiguration för PKCS-certifikatprofilen

Om du inte hittar begärandefilerna i mapparna **Misslyckade**, **Bearbetas** eller **Lyckade** så kan orsaken vara att fel certifikat är associerat med PKCS-certifikatprofilen. Till exempel kanske en underordnad certifikatutfärdare är kopplad till profilen, eller så används fel rotcertifikat.

**Lösning**:

1. Granska din betrodda certifikatprofil för att se till att du har distribuerat rotcertifikatet från din företagscertifikatutfärdare till enheter.
2. Granska din PKCS-certifikatprofil för att se till att den refererar till rätt CA, certifikattyp och den betrodda certifikatprofil som distribuerar rotcertifikatet till enheter.

Mer information om certifikat finns i [Använda certifikat för autentisering](../protect/certificates-configure.md) i Microsoft Intune.

### <a name="error--2146875374-certsrv_e_subject_email_required"></a>Fel – 2146875374 CERTSRV_E_SUBJECT_EMAIL_REQUIRED

PKCS-certifikat kan inte distribueras och certifikatkonsolen på den utfärdande certifikatutfärdaren visar ett meddelande med strängen **-2146875374 CERTSRV_E_SUBJECT_EMAIL_REQUIRED** som visas i följande exempel:

```
Active Directory Certificate Services denied request abc123 because The Email name is unavailable and cannot be added to the Subject or Subject Alternate name. 0x80094812 (-2146875374 CERTSRV_E_SUBJECT_EMAIL_REQUIRED). The request was for CN=” Common Name”.  Additional information: Denied by Policy Module”.
```

#### <a name="cause---supply-in-the-request-is-miscongifured"></a>Orsak – Anges i begäran är felkonfigurerat

Det här problemet uppstår om **Anges i begäran** inte har aktiverats på fliken **Ämnesnamn** i dialogrutan **Egenskaper** för certifikatmallen.

> [!div class="mx-imgBorder"]
> ![Konfigurera NDES-egenskaperna](./media/troubleshoot-pkcs-certificate-profiles/supply-in-the-request.png)

**Lösning**:

Redigera mallen för att lösa konfigurationsproblemet:

1. Logga in på din Enterprise CA med ett konto som har administratörsbehörighet.
2. Öppna konsolen **Certifikatutfärdare**, högerklicka på **Certifikatmallar** och välj **Hantera**.
3. Öppna dialogrutan Egenskaper för certifikatmallen.
4. På fliken **Ämnesnamn** väljer du **Anges i begäran**.
5. Välj **Ok** för att spara certifikatmallen och stäng sedan **Certifikatmallar**-konsolen.
6. I **Certifikatutfärdare**-konsolen högerklickar du på **Certifikatmallar** > **Ny** > **Certifikatmall som ska utfärdas**.
7. Välj den mall som du ändrade och klicka sedan på **OK**.

## <a name="next-steps"></a>Nästa steg

Om du fortfarande letar efter en lösning eller letar efter mer information om Intune, lägg upp en fråga i vårt [Microsoft Intune-forum](https://social.technet.microsoft.com/Forums/home?category=microsoftintune&filter=alltypes&sort=lastpostdesc). Många supporttekniker, MVP:er och medlemmar i vårt utvecklingsteam använder forumen ofta, så det finns en god chans att någon kan hjälpa dig.

Öppna ett supportärende med Microsoft Intune-produktsupportteamet genom att se [Så kan du få support för Microsoft Intune](../fundamentals/get-support.md).
Mer information om PKCS-certifikatdistribution finns i följande artiklar:

- [Konfigurera och använda PKCS-certifikat med Intune](../protect/certficates-pfx-configure.md)
- [Konfigurera en certifikatprofil för enheterna i Microsoft Intune](../protect/certificates-configure.md)
- [Ta bort SCEP- och PKCS-certifikat i Microsoft Intune](../protect/remove-certificates.md)