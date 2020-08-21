---
title: Hitta hjälp
titleSuffix: Configuration Manager
description: Hitta resurser för ytterligare information om Configuration Manager.
ms.date: 05/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 86810629-cf2a-43e8-86a2-847444119fc1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4ae2d837179e3b661bfbfa68d1db429674e20de5
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699406"
---
# <a name="find-help-for-using-configuration-manager"></a>Få hjälp med att använda Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Den här artikeln innehåller följande avsnitt med flera resurser för att få hjälp med att använda Configuration Manager:  

- [Produktdokumentation](#bkmk_Info)  

- [Dela produkt feedback](#product-feedback)  

- [Följ Configuration Manager teamets blogg](#BKMK_ProductGroupBlog)  

- [Supportalternativ och gruppresurser](#BKMK_SupportOptions)  

Hjälp med produkt tillgänglighet finns i [hjälpmedels funktioner](accessibility-features.md).  



##  <a name="product-documentation"></a><a name="bkmk_Info"></a> Produkt dokumentation  

Börja med [biblioteks indexet](/sccm/)för att få åtkomst till den mest aktuella produkt dokumentationen.  

<a name="BKMK_SearchTips"></a>  

Tips om att söka, lämna feedback och mer information om hur du använder produkt dokumentationen finns i [så här använder du dokumenten](use-docs.md).  



<a name="product-feedback"></a>

## <a name="product-feedback-starting-with-version-1806"></a><a name="BKMK_1806Feedback"></a> Produkt feedback från och med version 1806

Från och med Configuration Manager version 1806 kan du skicka produkt feedback direkt från-konsolen. Använd [feedback Hub](#BKMK_FeedbackHub)om du behöver bifoga loggar. Du kan göra följande saker: <!--1357542-->

- **Skicka ett leende**: skicka feedback om vad du gillade.
- **Skicka en bister min**: skicka feedback om vad du inte gillade.
- **Skicka ett förslag**: går till UserVoice- [webbplatsen](https://configurationmanager.uservoice.com/) för att dela din idé.

  ![Skicka feedback i Configuration Manager 1806](media/1806-send-a-smile.png)


### <a name="send-a-smile-or-send-a-frown"></a>Skicka ett leende eller skicka en bister min

Skicka feedback om något som du gillade genom att följa anvisningarna nedan:

1. I det övre högra hörnet i konsolen klickar du på glad min.
2. I den nedrullningsbara menyn väljer du **Skicka ett leende** eller **skicka en bister min**.
3. Använd text rutan för att förklara vad du gillade eller vad du inte gillade. 
4. Välj om du vill dela din e-postadress och en skärm bild.
5. Klicka på **Skicka feedback**
     - Om du inte har någon Internet anslutning klickar du på **Spara** längst ned. Följ anvisningarna i avsnittet [Skicka feedback som du sparade för senare sändning](#BKMK_NoInternet) för att skicka det till Microsoft. 

![Skicka feedback-formulär i Configuration Manager 1806](media/1806-feedback-form.png)

#### <a name="status-messages-for-send-a-smile"></a>Status meddelanden för att skicka ett leende
<!--5891852-->
Från och med Configuration Manager 2002 skapas ett status meddelande när din feedback skickas när du **skickar ett leende** eller **skickar en bister min**. Den här förbättringen innehåller en post med:
- När din feedback skickades
- Som skickade feedbacken
- Feedback-ID
- Om feedback-överföringen lyckades eller inte
   - Meddelande-ID 53900 för lyckad överföring.
   - Meddelande-ID 53901 för misslyckad överföring.

Visa status meddelanden från **övervaka**  >  **system status**  >  **status meddelande frågor**. Börja med frågan **alla status meddelanden** och välj tidsram. När meddelande inläsningen visas klickar du på knappen **filtrera meddelanden** och filtrerar efter meddelande-ID 53900 eller 53901.

Status meddelanden skapas inte om du [skickar feedback som du har sparat för senare sändning](find-help.md#BKMK_NoInternet).

[![Status meddelande för att skicka feedback](./media/5891852-send-smile-status-message.png)](./media/5891852-send-smile-status-message.png#lightbox)

### <a name="send-a-suggestion"></a>Skicka ett förslag

När du **skickar ett förslag**dirigeras du till [UserVoice](https://configurationmanager.uservoice.com/), en webbplats från tredje part, för att dela din idé. I Configuration Manager produkt teamet används följande UserVoice-status värden:

- Vi har **antecknat** – vi förstår begäran och det är bäst. Vi har lagt till den i vår efter släpning.
- **Planerat** – vi har börjat koda för den här funktionen och förväntar dig att den ska visas i en teknisk för hands version inom de kommande månaderna.
- **Startade** – funktionen finns nu i en teknisk för hands version. Gå igenom den och ge oss feedback. Berätta för oss om funktionen är i rätt spår eller inte. Lägg till ytterligare feedback i avsnittet kommentarer i den ursprungliga begäran som andra kan se och kommentera. Vi läser det och använder feedbacken för att försöka förbättra funktionen.
- **Slutförd** – den första versionen av funktionen finns i en produktions version. Den här statusen innebär inte att vi är 100% klara med funktionen och kommer inte längre att förbättra den. Men det innebär att v1 av funktionerna finns i en produktions version och du kan börja använda det i Real. Vi markerar det klart eftersom:
  - Vi vill att du vet att funktionen är produktions klar.
  - Vi vill ge tillbaka dina UserVoice-röster så att du kan använda dem på andra objekt.
  - Du kan skicka in nya begär Anden om design ändringar till den här funktionen för att hjälpa oss att känna till nästa viktiga förbättring av den här funktionen.

### <a name="information-sent-with-feedback"></a>Information som skickas med feedback

När du **skickar ett leende** eller **skickar en bister min**skickas följande information med feedback:

- Build-information för operativ system
- Configuration Manager hierarki-ID
- Produkt versions information
- Språk information
- Enhets identifierare 
    - HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\SQMClient: MachineId



### <a name="send-feedback-that-you-saved-for-later-submission"></a><a name="BKMK_NoInternet"></a> Skicka feedback som du sparade för senare överföring

1. Klicka på **Spara** längst ned i fönstret **ge feedback** . 
2. Spara zip-filen. Om den lokala datorn inte har till gång till Internet kopierar du filen till en dator som är ansluten till Internet. 
3. Om det behövs kopierar du UploadOfflineFeedback-mappen som finns på `cd.latest\SMSSETUP\Tools\UploadOfflineFeedback\`
    - Mer information om CD. senaste-mappen finns [på CD-skivan. Senaste mappen](../servers/manage/the-cd.latest-folder.md)

4. Öppna en kommando tolk på en dator som är ansluten till Internet. 
5. Kör följande kommando: `UploadOfflineFeedback.exe -f c:\folder\location_of.zip`
    
    - Du kan också ange följande parametrar:
        -  `-t, --timeout` Tids gräns i sekunder för att skicka data. 0 är obegränsad. Standardvärdet är 30.
        - `-s --silent`  Ingen loggning till konsolen (det går inte att kombinera med--verbose)
        - `-v, --verbose` Utförlig loggning av utdata till konsolen (kan inte kombineras med--Silent)
        - `--help` Visar hjälp skärmen
    
    - Från och med version 1910 stöder UploadOfflineFeedback-verktyget användningen av en proxyserver. Du kan ange följande parametrar:
        - `-x, --proxy` Anger en proxyserver för att ansluta Internet.
        - `-o, --port` Anger porten för proxyservern för att ansluta Internet.
        - `-u, --user` Anger användar namnet för proxyservern för anslutning av Internet.
        - `-w, --password` Anger lösen ordet för proxyservern för att ansluta Internet. Ange en asterisk (&#42;) för att skapa en prompt för lösen ordet. Lösen ordet visas inte när du skriver det vid lösen ords prompten. Vi rekommenderar starkt att du använder en asterisk (&#42;) för att skapa en uppräkning för lösen ords indatatypen eftersom oformaterad text på kommando raden är mindre säker.
        - `-i` Hoppa över anslutnings kontroll: hoppar över kontrollen av nätverks anslutningen och överför bara feedback med angivna inställningar.

## <a name="confirmation-of-console-feedback"></a><a name="bkmk_feedbackid"></a> Bekräftelse av konsol kommentarer

<!--3556010-->
Från och med version 1902 visas ett bekräftelse meddelande när du skickar feedback via Configuration Manager-konsolen eller UploadOfflineFeedback.exe. Det här meddelandet innehåller ett **feedback-ID**, som du kan ge till Microsoft som ett spårnings-ID.

- Om du vill kopiera **feedback-ID: t**väljer du kopierings ikonen bredvid ID: t eller använder kortkommandot **CTRL**  +  **C** .
  - Detta ID lagras inte på din dator, så se till att kopiera det innan du stänger fönstret.
- Om du klickar på **Visa inte det här meddelandet igen** utelämnas dialog rutan och det kan inte visas i framtiden.

   ![Bekräfta feedback från-konsolen i Configuration Manager 1902](media/1902-feedback-id-example.png)
- Kommando verktyget **UploadOfflineFeedback** skriver **FeedbackID** till konsolen om inte-s eller--Silent används.

  ![Bekräftelse av feedback från UploadOfflineFeedback.exe i Configuration Manager 1902](media/1902-offline-feedback-id-example.png)

##  <a name="product-feedback-for-versions-1802-and-earlier"></a><a name="BKMK_FeedbackHub"></a> Produkt feedback för version 1802 och tidigare

Rapportera potentiella produkt fel via [appen för feedback Hub](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app) som är inbyggd i Windows 10. När du **lägger till nya kommentarer**, se till att välja kategorin **företags hantering** och välj sedan någon av följande under Kategorier:
- Configuration Manager-klient
- Configuration Manager-konsolen
- Configuration Manager OS-distribution
- Configuration Manager Server

Fortsätt att använda [sidan UserVoice](https://configurationmanager.uservoice.com/) för att rösta på nya funktions idéer i Configuration Manager. I Configuration Manager produkt teamet används följande UserVoice-status värden:

- Vi har **antecknat** – vi förstår begäran och det är bäst. Vi har lagt till den i vår efter släpning.
- **Planerat** – vi har börjat koda för den här funktionen och förväntar dig att den ska visas i en teknisk för hands version inom de kommande månaderna.
- **Startade** – funktionen finns nu i en teknisk för hands version. Gå igenom den och ge oss feedback. Berätta för oss om funktionen är i rätt spår eller inte. Lägg till ytterligare feedback i avsnittet kommentarer i den ursprungliga begäran som andra kan se och kommentera. Vi läser det och använder feedbacken för att försöka förbättra funktionen.
- **Slutförd** – den första versionen av funktionen finns i en produktions version. Den här statusen innebär inte att vi är 100% klara med funktionen och kommer inte längre att förbättra den. Men det innebär att v1 av funktionerna finns i en produktions version och du kan börja använda det i Real. Vi markerar det klart eftersom:
  - Vi vill att du vet att funktionen är produktions klar.
  - Vi vill ge tillbaka dina UserVoice-röster så att du kan använda dem på andra objekt.
  - Du kan skicka in nya begär Anden om design ändringar till den här funktionen för att hjälpa oss att känna till nästa viktiga förbättring av den här funktionen.

##  <a name="configuration-manager-team-blog"></a><a name="BKMK_ProductGroupBlog"></a> Configuration Manager teamets blogg  

Configuration Manager tekniker och partner team använder [Enterprise Mobility + Security Blogg](https://cloudblogs.microsoft.com/enterprisemobility/?product=system-center-configuration-manager) för att ge dig teknisk information och andra nyheter om Configuration Manager och relaterade tekniker. Våra bloggposter kompletterar produktdokumentationen och supportinformationen.  


##  <a name="support-options-and-community-resources"></a><a name="BKMK_SupportOptions"></a> Support alternativ och grupp resurser  

Följande länkar ger information om supportalternativ och gruppresurser:  

-   [Microsoft-Support](https://aka.ms/cmcbsupport)  

-   [Configuration Manager community: Configuration Manager (Current Branch) överlevnads guide](https://social.technet.microsoft.com/wiki/contents/articles/33035.system-center-configuration-manager-current-branch-survival-guide.aspx )  

-   [Sidan Configuration Manager forum](https://social.technet.microsoft.com/Forums/en-US/home?category=ConfigMgrCB)  
    <!-- NOTE: the above URL requires "en-US" for the category to work -->