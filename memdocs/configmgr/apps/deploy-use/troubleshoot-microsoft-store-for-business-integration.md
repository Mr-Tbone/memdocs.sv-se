---
title: Felsök MSfB-integrering
titleSuffix: Configuration Manager
description: Innehåller förslag och lösningar för att felsöka några av de vanligaste problemen med Microsoft Store för affärs-och utbildnings integrering.
ms.date: 04/24/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 09929057-ecf2-4d49-aee0-709916932b14
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 694083bbce34b9e1b62f77a1d18cf79663704b2a
ms.sourcegitcommit: af8a3efd361a7f3fa6e98e5126dfb1391966ff76
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/24/2020
ms.locfileid: "82149092"
---
# <a name="troubleshoot-the-microsoft-store-for-business-and-education-integration-with-configuration-manager"></a>Felsök Microsoft Store för affärs-och utbildnings integrering med Configuration Manager

Den här artikeln innehåller tips för viktiga fel sökning och korrigeringar för några av de vanligaste problemen som du kan ha med Microsoft Store for Business and Education (MSfB)-integration med Configuration Manager.

Mer information om hur du använder Microsoft Store för företag och utbildning med Configuration Manager finns i [Hantera appar från Microsoft Store för företag och utbildning med Configuration Manager](manage-apps-from-the-windows-store-for-business.md).

## <a name="monitor"></a>Övervaka

### <a name="component-status"></a>Komponent status

I Configuration Manager-konsolen går du till arbets ytan **övervakning** , expanderar **system status**och väljer noden **komponent status** . Övervaka status för följande komponenter:

- SMS_BUSINESS_APP_PROCESS_MANAGER
- SMS_CLOUDCONNECTION

### <a name="sync-status"></a>Synkroniseringsstatus

I Configuration Manager-konsolen går du till arbets ytan **Administration** , expanderar **Cloud Services**och väljer noden **Microsoft Store för företag** . Kontrol lera den **Senaste synkroniseringsstatus** -kolumnen.

### <a name="view-synchronized-apps"></a>Visa synkroniserade appar

Gå till arbets ytan **program bibliotek** i Configuration Manager-konsolen, expandera **program hantering**och välj **licens information för Store Apps** -noden.


## <a name="log-files"></a>Loggfiler

### <a name="wsfbsyncworkerlog"></a>WSfBSyncWorker. log

Logg filen finns på tjänst anslutnings punkten under `\Logs` i Configuration Manager installations katalog. Den registrerar information om kommunikationen med moln tjänsten. Den här informationen omfattar metadata, ikoner, paket och hämtning av licens fil.

Om du vill ändra loggnings nivån ändrar `LoggingLevel` du värdet `0` till i `HKLM\SOFTWARE\Microsoft\SMS\Tracing\SMS_CLOUDCONNECTION` register nyckeln. Mer information finns i [Konfigurera loggnings alternativ](../../core/plan-design/hierarchy/about-log-files.md#bkmk_reg-site).

### <a name="sms_cloudconnectionlog"></a>SMS_CLOUDCONNECTION. log

Logg filen finns på tjänst anslutnings punkten under `\Logs` i Configuration Manager installations katalog. Om WSfBSyncWorker-tjänsten inte har startats eller upprepade gånger startar och stoppar, granskar du posterna i den här logg filen.

> [!NOTE]
> Den här logg filen delas med andra funktioner.

### <a name="businessappprocessworkerlog"></a>BusinessAppProcessWorker. log

Logg filen finns på plats servern för platsen på den översta nivån i hierarkin. Den finns under `\Logs` i Configuration Manager installations katalog. Den registrerar information om följande processer:

- Infoga metadatainformation som synkroniserats av BusinessAppProcessWorker-komponenten i databasen
- Bearbeta filer i`\InstallDir\inboxes\businessappprocess.box`

### <a name="sms_business_app_process_managerlog"></a>SMS_BUSINESS_APP_PROCESS_MANAGER. log

Logg filen finns på plats servern för platsen på den översta nivån i hierarkin. Den finns under `\Logs` i Configuration Manager installations katalog. Om BusinessAppProcessWorker-tjänsten inte har startats eller upprepade gånger startar och stoppar, granskar du posterna i den här logg filen.



## <a name="last-sync-failed"></a>Senaste synkronisering misslyckades

När den senaste synkroniseringsstatus-statusen har *misslyckats*börjar du med att granska följande [loggfiler](#log-files) för att identifiera problemet:

- WSfbSyncWorker. log
- SMS_CLOUDCONNECTION. log

Titta sedan på något av följande avsnitt för vanliga problem:

- [Auktoriseringsfel](#bkmk_fail-symptom1)
- [Den hemliga nyckeln är ogiltig](#bkmk_fail-symptom2)
- [Fel vid hämtning av programtoken](#bkmk_fail-symptom3)
- [Innehålls platsen finns inte eller har felaktig behörighet](#bkmk_fail-symptom4)
- [Ett fel uppstod när http-begäran anropade GET-metoden](#bkmk_fail-symptom5)
- [Det går inte att skriva fler byte till bufferten](#bkmk_fail-symptom6)

### <a name="authorization-error"></a><a name="bkmk_fail-symptom1"></a>Auktoriseringsfel

#### <a name="cause"></a>Orsak

Det här problemet kan uppstå om det konfigurerade Azure Active Directory-programmet (Azure AD) inte har behörighet att hantera Microsoft Store för företag och utbildning för den här klienten.

#### <a name="workaround"></a>Lösning

1. Logga in som administratör på Microsoft Store för affärs-eller utbildnings portalen.
1. Gå till **Inställningar**och välj **hanterings verktyg**.
1. Om programmet inte visas väljer du **Lägg till ett hanterings verktyg**. Sök sedan efter namn och välj det Azure AD-program som är associerat med samma ClientID som Configuration Manager.
1. Om statusen inte visas som **aktiv**väljer du **Aktivera** i avsnittet **åtgärd** .
1. I Configuration Manager-konsolen går du till arbets ytan **Administration** , expanderar **Cloud Services**och väljer noden **Microsoft Store för företag** . Synkronisera med Store eller vänta tills nästa synkroniseringstillstånd inträffar.

> [!Tip]
> Så här hittar du ClientID i Configuration Manager:
>
> 1. I Configuration Manager-konsolen går du till arbets ytan **Administration** , expanderar **Cloud Services**och väljer noden **Azure Active Directory Tennts** .
> 1. Välj den klient som du använder för Microsoft Store för affärs-och utbildnings integrering.
> 1. Leta upp det matchande programmet i resultat fönstret och titta i kolumnen **klient-ID** .

### <a name="the-secret-key-is-invalid"></a><a name="bkmk_fail-symptom2"></a>Den hemliga nyckeln är ogiltig

#### <a name="cause"></a>Orsak

Det här problemet kan uppstå om den hemliga nyckeln har upphört att gälla i Azure AD-appen för konfiguration av Microsoft Store för företag och utbildning.

#### <a name="resolution"></a>Lösning

Förnya den hemliga nyckeln för Azure AD-programmet. Mer information finns i [förnya hemlig nyckel](../../core/servers/deploy/configure/azure-services-wizard.md#bkmk_renew).

### <a name="error-getting-application-token"></a><a name="bkmk_fail-symptom3"></a>Fel vid hämtning av programtoken

#### <a name="cause"></a>Orsak

Det här problemet kan uppstå om den anslutna appen inte längre finns i Azure AD.

#### <a name="resolution"></a>Lösning

Ta bort och återskapa anslutningen till Microsoft Store för företag och utbildning.

1. I Configuration Manager-konsolen går du till arbets ytan **Administration** , expanderar **Cloud Services**och väljer noden **Microsoft Store för företag** .
1. Välj den befintliga anslutningen.
1. Välj **ta bort** i menyfliksområdet.

Återskapa sedan anslutningen. Mer information finns i följande artiklar:

- [Konfigurera Azure-tjänster](../../core/servers/deploy/configure/azure-services-wizard.md)
- [Konfigurera Microsoft Store för synkronisering av affärs-och utbildning](manage-apps-from-the-windows-store-for-business.md#bkmk_setup)

### <a name="content-location-doesnt-exist-or-incorrect-permissions"></a><a name="bkmk_fail-symptom4"></a>Innehålls platsen finns inte eller har felaktig behörighet

#### <a name="cause"></a>Orsak

När du konfigurerar Microsoft Store för affärs-och utbildnings anslutning kan du ange en nätverks resurs för att lagra synkroniserat innehåll. Det här problemet kan uppstå om resursen inte finns eller har fel behörighet. Dator kontot för tjänst anslutnings punkten ska vara ägare till den här katalogen och eventuella under kataloger.<!-- memdocs#146 --> Om den inte är det ser du ett fel som liknar följande fel:

```
Failed to download package d788cc1b-ab00-bb5f-1548-f2dfe717583b-X86-Arm for product 9WZDNCRFJ3PS\0015.
System.IO.IOException: This security ID may not be assigned as the owner of this object.
```

Så här visar du den plats som du har konfigurerat:

1. I Configuration Manager-konsolen går du till arbets ytan **Administration** , expanderar **Cloud Services**och väljer noden **Microsoft Store för företag** .

1. Välj kontot och öppna dess **Egenskaper**.

1. Växla till fliken **konfiguration** . Inställningen **plats** visar nätverks Sök vägen för att lagra program innehåll som laddats ned från Microsoft Store för företag och utbildning.

#### <a name="workaround"></a>Lösning

1. Om den inte redan finns skapar du resursen.

1. Kontrol lera NTFS-behörigheter för mappen och behörigheterna på nätverks resursen. Ge dator kontot för tjänst anslutnings punktens **Läs** -och **Skriv** behörighet.

Om du vill konfigurera om platsen tar du bort och återskapar anslutningen med den nya innehålls platsen.

### <a name="error-occurred-making-http-request-calling-get-method"></a><a name="bkmk_fail-symptom5"></a>Ett fel uppstod när http-begäran anropade GET-metoden

#### <a name="cause"></a>Orsak

Det här problemet kan uppstå om synkroniseringen av program från arkivet tog så lång tid att innehålls-URL: en har upphört att gälla.

#### <a name="workaround"></a>Lösning

Försök att synkronisera igen

1. I Configuration Manager-konsolen går du till arbets ytan **Administration** , expanderar **Cloud Services**och väljer noden **Microsoft Store för företag** .
1. Välj anslutningen. I menyfliksområdet väljer du **Synkronisera från Microsoft Store för företag**.

Varje gång bör det fortsätta. Det kan ta flera återförsök beroende på följande faktorer:

- Antalet offline-program
- Paketets storlek
- Nätverks hastigheten

Vid varje försök bör du se felet färre gånger. Om antalet fel inte minskar finns det ett problem.

### <a name="cannot-write-more-bytes-to-the-buffer"></a><a name="bkmk_fail-symptom6"></a>Det går inte att skriva fler byte till bufferten

#### <a name="cause"></a>Orsak

Det här problemet kan uppstå om programmets paket är större än 500 MB. Configuration Manager stöder bara automatisk synkronisering av offline-program med paket som är mindre än 500 MB.

#### <a name="workaround"></a>Lösning

Du kan inte synkronisera dessa appar automatiskt, men du kan ladda ned innehållet och manuellt skapa programmet:

1. Hämta det misslyckade program-ID: t från följande rad i **WSfbSynWorker. log**:

    `Error(s) syncing or downloading application <ApplicationID> from the Microsoft Store for Business.`

1. Logga in som administratör på Microsoft Store för affärs-eller utbildnings portalen. Hitta sidan för det här programmet.

    > [!Tip]
    > Sidans URL liknar:`https://businessstore.microsoft.com/en-us/store/p/app/ApplicationID`

    1. Välj **offline**, om det inte redan är markerat. Välj sedan **Hantera**.

    1. Skapa en separat mapp på din program innehålls resurs för alla plattformar som stöds.

    1. Ladda ned paketet till Package-mappen.

    1. Ladda ned den kodade licens filen `.bin` som en fil till Package-mappen.

    1. Ladda ned alla nödvändiga ramverk till Package-mappen.

1. Gå till arbets ytan **program bibliotek** i Configuration Manager-konsolen, expandera **program hantering**och välj noden **program** .

1. [Skapa ett program](create-applications.md), ange programinformationen manuellt.

    1. Skapa en distributions typ för varje plattform som stöds och som du tidigare har laddat ned.

    1. Typ: **Windows app-paket\*(. appx \*,. appxbundle)**

    1. Ange appx/appxbundle för det faktiska Appaketet, inte ett nödvändigt beroende paket.

Bekräfta följande information på sidan slutgiltig **import information** :

- **Licens fil:** Anger `.bin` filen. Den här licens filen krävs för offline-appar.
- **Windows-program beroenden:** Kontrol lera att alla nödvändiga beroenden har hämtats för det här paketet.


## <a name="sync-doesnt-run"></a>Synkroniseringen körs inte

I det här avsnittet beskrivs följande synkroniseringsproblem:

- Du startar Sync-processen manuellt, men den körs inte
- Platsen synkroniseras inte automatiskt varje dag

Börja med att granska följande [loggfiler](#log-files) för att identifiera problemet:

- BusinessAppProcessWorker. log
- SMS_BUSINESS_APP_PROCESS_MANAGER. log
- WsfbSyncWorker. log
- SMS_CLOUDCONNECTION. log

Titta sedan på något av följande avsnitt för vanliga problem:

- [Manuell synkronisering startar inte](#bkmk_sync-symptom1)
- [Automatisk Daglig synkronisering körs inte och "stänga av # Worker"-fel i SMS_BUSINESS_APP_PROCESS_MANAGER. log](#bkmk_sync-symptom2)

### <a name="manual-sync-doesnt-start"></a><a name="bkmk_sync-symptom1"></a>Manuell synkronisering startar inte

#### <a name="cause"></a>Orsak

Det här problemet kan uppstå om du startar en synkronisering som är mindre än 10 minuter efter den tidigare synkroniseringen. Du kan inte synkronisera oftare än var tionde minut.

#### <a name="resolution"></a>Lösning

Vänta i minst 10 minuter innan du startar en annan synkronisering.

### <a name="automatic-daily-sync-doesnt-run-and-shutting-down--workers-error-in-sms_business_app_process_managerlog"></a><a name="bkmk_sync-symptom2"></a>Automatisk Daglig synkronisering körs inte och "stänga av # Worker"-fel i SMS_BUSINESS_APP_PROCESS_MANAGER. log

#### <a name="cause"></a>Orsak

Det här problemet kan uppstå om SMS_BUSINESS_APP_PROCESS_MANAGER-komponenten stoppar WsfbSyncWorker-tråden. Felet kan ange antingen `2` eller `4` Worker.

#### <a name="workaround"></a>Lösning

Starta om tjänsten **SMS_EXECUTIVE** .

Om du inte kan starta om den huvudsakliga tjänsten stoppar du båda komponenterna med MSfB-arbetare och startar sedan båda:

1. Öppna Windows-registret på den server som kör tjänst anslutnings punkten

1. Gå till `HKLM\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_EXECUTIVE\Threads\SMS_CLOUDCONNECTION`

    1. Ange den begärda åtgärden som ska **stoppas**.

    1. Uppdatera för att verifiera aktuell status = **stoppad**.

1. Gå till `HKLM\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_EXECUTIVE\Threads\SMS_BUSINESS_APP_PROCESS_MANAGER`

    1. Ange den begärda åtgärden som ska **stoppas**.

    1. Uppdatera för att verifiera aktuell status = **stoppad**.

1. I **SMS_CLOUDCONNECTION**anger du att den begärda åtgärden ska **Starta**.

1. I **SMS_BUSINESS_APP_PROCESS_MANAGER**anger du att den begärda åtgärden ska **Starta**.


## <a name="language-related-issues"></a>Språkrelaterade problem

Det här avsnittet innehåller följande vanliga problem:

- [Ändringar av val av språk tillämpas inte](#bkmk_lang-symptom1)
- [Alla valda språk är inte tillgängliga för all licens information](#bkmk_lang-symptom2)

### <a name="language-selection-changes-arent-applied"></a><a name="bkmk_lang-symptom1"></a>Ändringar av val av språk tillämpas inte

#### <a name="cause"></a>Orsak

Det här problemet kan uppstå om det valda språket är cachelagrat och inte rensas efter att egenskapsvärdena har ändrats.

#### <a name="workaround"></a>Lösning

Lös problemet genom att starta om tjänsten **SMS_EXECUTIVE** .

### <a name="not-all-selected-languages-are-present-for-all-license-information"></a><a name="bkmk_lang-symptom2"></a>Alla valda språk är inte tillgängliga för all licens information

#### <a name="cause"></a>Orsak

Det här problemet kan inträffa om programmets licens information för Microsoft Store för företag och utbildning inte innehåller lokaliserade data för det angivna språket.

#### <a name="workaround"></a>Lösning

Lägg till eventuella språk som saknas för de skapade programmen manuellt.


## <a name="offline-applications"></a>Offline-program

Det här avsnittet innehåller följande vanliga problem:

- [Det gick inte att skapa ett offline-program eftersom det inte går att verifiera innehållet](#bkmk_off-symptom1)
- [Det gick inte att installera programmet som skapades från licens informationen för offline](#bkmk_off-symptom2)

### <a name="fail-to-create-offline-application-because-content-cant-be-verified"></a><a name="bkmk_off-symptom1"></a>Det gick inte att skapa ett offline-program eftersom det inte går att verifiera innehållet

#### <a name="cause"></a>Orsak

Det här problemet kan uppstå om det synkroniserade innehållet för programmet offline är skadat eller ändrat.

#### <a name="workaround"></a>Lösning

Starta en ny synkronisering. När synkroniseringen är klar bör du kontrol lera och ladda ned eventuella felaktiga innehållsfiler.

### <a name="fail-to-install-application-created-from-offline-license-information"></a><a name="bkmk_off-symptom2"></a>Det gick inte att installera programmet som skapades från licens informationen för offline

#### <a name="cause"></a>Orsak

Det här problemet kan uppstå om du distribuerar programmet till en klient som kör en tidigare version av Windows 10 än version 1511. Offline-licensierade appar från Microsoft Store for Business och Education stöds endast på Windows 10 version 1511 och senare.

#### <a name="resolution"></a>Lösning

Installera den senaste versionen av Windows 10.


## <a name="next-steps"></a>Nästa steg

Mer hjälp finns i [hitta hjälp för att använda Configuration Manager](../../core/understand/find-help.md).
