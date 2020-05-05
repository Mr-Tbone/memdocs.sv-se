---
title: Funktioner i Technical Preview 1601
titleSuffix: Configuration Manager
description: Lär dig mer om funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1601.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: aae1cf2f-2c04-4f68-a03a-f4a925433c09
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 2ae184400a3de0d7ab27fffc1ce1e6287593b1ae
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82076313"
---
# <a name="capabilities-in-technical-preview-1601-for-configuration-manager"></a>Funktioner i Technical Preview 1601 för Configuration Manager

*Gäller för: Configuration Manager (Technical Preview Branch)*

Den här artikeln beskriver de funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1601. Du kan installera den här versionen för att uppdatera och lägga till nya funktioner till din Configuration Manager Technical Preview-webbplats.      Innan du installerar den här versionen av Technical Preview kan du läsa introduktions avsnittet, [teknisk för hands version för Configuration Manager](../../core/get-started/technical-preview.md), för att bekanta dig med allmänna krav och begränsningar för att använda en teknisk för hands version, hur du uppdaterar mellan versioner och hur du ger feedback om funktionerna i en teknisk för hands version.  

 **Kända problem för den här tekniska för hands versionen:**  

-   När du hanterar **alternativ för klient uppdatering** för att flytta upp en för produktions klient till produktion, visar texten för kryss rutan en klient version av noll (0) i stället för det faktiska klient versions numret. Rätt för produktions klient version visas på ytan ovanför det här alternativet och är den klient version som befordras till produktion när du väljer det här alternativet.  

-   När du uppdaterar till Technical Preview 1601 och väljer att testa Configuration Manager klienten i en för produktions samling, uppgraderas inte klient paketet för samlingen. Det här problemet gäller endast för teknisk för hands version 1601.  

     Gör något av följande för att lösa problemen:  

    -   Kör följande SQL-skript på den primära platsens databas:  

        ``` SQL
        DECLARE @PilotingPkgID NVARCHAR(8)  

        SELECT @PilotingPkgID = PilotingPackageID FROM ClientDeploymentSettings  

        MERGE INTO PkgServers_G AS T  
        USING (  
            SELECT @PilotingPkgID AS PkgID, NALPath, SiteCode, SiteName, SourceSite, RefreshTrigger, UpdateMask, [Action]  
            FROM PkgServers_G WHERE PkgID IN (SELECT UpgradePackageID FROM ClientDeploymentSettings)  
            ) AS S  
        ON T.PkgID = S.PkgID and T.NALPath = S.NALPath  

        WHEN NOT MATCHED THEN  
            INSERT (PkgID, NALPATH, SiteCode, SiteName, SourceSite, LastRefresh, RefreshTrigger, UpdateMask, [Action])  
            VALUES (S.PkgID, S.NALPath, S.SiteCode, S.SiteName, S.SourceSite, GetUTCDate(), S.RefreshTrigger, S.UpdateMask, S.[Action])  
        ;  

        ```  

    -   Lägg till en ny plats system roll för distributions plats på din labb webbplats. Den nya distributions platsen uppgraderar för produktions samlingen med det nya klient paketet.  

**Följande är nya funktioner som du kan prova med den här versionen.**  

##  <a name="improvements-to-microsoft-intune-integration"></a><a name="bkmk_hybrid1"></a>Förbättringar av Microsoft Intune-integrering  
I 1601 Technical Preview har vi lagt till stöd för följande funktioner:  

### <a name="improvements-to-conditional-access"></a>Förbättringar av villkorlig åtkomst  

-   **Stöd för villkorlig åtkomst för datorer som hanteras av Configuration Manager**  

     Nu kan du ange principer för villkorlig åtkomst för datorer som hanteras av Configuration Manager, vilket kräver att datorerna är kompatibla med policyn för efterlevnad för att få åtkomst till Exchange Online-och SharePoint Online-tjänster.  Med den här nya funktionen kan du också registrera datorer med Azure AD via policyn för efterlevnad och övervaka och rapportera om Azure AD-registrering.  

    > [!NOTE]  
    >  Villkorlig åtkomst stöds inte ännu i Windows 10.  

    Följande är förutsättningarna för att använda den här funktionen:  

    -   Azure Active Directory Premium prenumeration och ADFS-synkronisering.  

    -   En Microsoft Intune-prenumeration. Microsoft Intune prenumerationen ska konfigureras i Configuration Manager-konsolen.  

    -   [Krav för automatisk registrering av Azure AD](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1).  

    Om du vill använda alternativet måste du skapa en efterlevnadsprincip i Configuration Manager med vissa regler som beskrivs nedan och ange en princip för villkorlig åtkomst i Intune-konsolen.  För att se till att endast kompatibla datorer är tillåtna, måste du också ställa in krav för Windows-dator på alternativet **enheter måste vara kompatibelt** . Nedan följer de regler för kompatibla principer som gäller för datorer som hanteras av Configuration Manager.  

    -   **Kräv registrering i Azure ActiveDirectory:** Den här regeln kontrollerar om användarens enhet är arbets plats ansluten till Azure AD, och om den inte är det registreras enheten automatiskt i Azure AD. Automatisk registrering stöds bara på Windows 8.1. Distribuera en MSI för att utföra automatisk registrering för Windows 7-datorer. Mer information finns [här](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1).  

    -   **Alla begärda uppdateringar har installerats med en tids gräns som är äldre än ett visst antal dagar:** Den här regeln kontrollerar om användarens enhet har alla uppdateringar som krävs (anges i regeln för **obligatoriska automatiska uppdateringar** ) inom en tids gräns och respittid som du anger och installerar automatiskt eventuella väntande uppdateringar som krävs.  

    -   **Kräv BitLocker-enhets kryptering:** Detta är en kontroll för att se om den primära enheten (t. ex\\. C:) på enheten är BitLocker-krypterad. Om Bitlocker-kryptering inte är aktiverat på den primära enheten blockeras åtkomsten till e-post och SharePoint-tjänster.  

    -   **Kräv program mot skadlig kod:** Detta är en kontroll för att se om program mot skadlig kod (endast System Center Endpoint Protection eller Windows Defender) är aktiverat och körs.  
         Om det inte är aktiverat blockeras åtkomsten till e-post och SharePoint-tjänster.  

    Slutanvändare som blockeras på grund av inkompatibilitet kommer att Visa kompatibilitetsinformation i Software Center och starta en ny princip utvärdering när kompatibilitetsproblemen har åtgärd ATS.  

-   **Villkorlig åtkomst med tjänsten Hälsoattestering** Du kan nu begränsa åtkomsten till e-post och 0365-tjänster baserat på hälso tillståndet för de enheter som rapporteras av tjänsten hälsoattestering.  Enheter som hanteras av Intune ingår dessutom i enhetens hälso rapporter.  

    En ny efterlevnadsprincip har lagts till i Configuration Manager-konsolen som gör att du kan ange om enheterna ska tillåtas eller blockeras åtkomst baserat på deras hälso status.  Om du vill skapa den här regeln öppnar du **guiden skapa efterlevnadsprincip**och lägger till en ny regel.  Välj det **rapporterade hälso tillståndet per Hälsoattesterings tjänst** för villkoret och ange värdet till **Sant**.  Detta ser till att endast enheter som rapporteras som felfria får åtkomst till företagets resurser. Information om tjänsten hälsoattestering och hur hälso tillståndet för enheterna rapporteras i Intune finns [Hälsoattestering för enhet](capabilities-in-technical-preview-1512.md#bkmk_devicehealth).  

-   **Nya inställningar för efterlevnadsprinciper:** De nya inställningarna för efterlevnadsprinciper hjälper till att förbättra säkerheten och skyddet på enheter som används för att komma åt företagets e-post och SharePoint-tjänster:  

    -   **Kräv automatiska uppdateringar:** Du kan kräva enheter med Windows 8,1 eller senare för att tillåta automatisk installation av uppdateringar och även ange klassen för uppdateringar som är installerade.  Du kan antingen välja att: Installera endast uppdateringar som marker ATS som viktiga eller installera alla rekommenderade uppdateringar.  

         Om du vill skapa en regel för automatiska uppdateringar öppnar du **guiden skapa efterlevnadsprincip**och lägger till en ny regel.  Välj **minsta klassificering för nödvändiga uppdateringar** som villkor och ange värdet till något av de tillgängliga värdena: **ingen**, **rekommenderas**och **viktigt**.  

        -   **Ingen:** Uppdateringar installeras inte automatiskt.  

        -   **Rekommenderas:** Alla rekommenderade uppdateringar är installerade  

        -   **Viktigt:** Endast uppdateringar som klassificeras som viktiga är installerade.  

    -   **Kräv lösen ord för att låsa upp mobila enheter:** När den här inställningen är inställd på **Ja**måste slutanvändarna ange ett lösen ord innan de kan komma åt sin enhet.  

         Om du vill skapa en regel för lösen ord för att låsa upp mobila enheter öppnar du **guiden skapa efterlevnadsprincip**och lägger till en ny regel. Välj **Kräv lösen ord för att låsa upp en inaktiv enhet** som villkor och ange värdet **Sant**.  

    -   **Minuter av inaktivitet innan lösen ord måste anges:**  Anger vänte tiden innan användaren måste ange sitt lösen ord på nytt.  

         Om du vill skapa den här regeln öppnar du **guiden skapa efterlevnadsprincip**och lägger till en ny regel. **Välj minuter av inaktivitet innan lösen ord krävs** som villkor och ange värdet till något av de tillgängliga alternativen: 1 minut, 5 minuter, 15 minuter, 30 minuter, I timmen.  

-   **Åsidosätt standard regel – Tillåt alltid att Intune-registrerade och kompatibla enheter får åtkomst till Exchange lokalt:**  

     När du markerar det här alternativet får enheter som är registrerade i Intune och kompatibla med efterlevnadsprinciper åtkomst till Exchange lokalt. Den här regeln åsidosätter standard regeln, vilket innebär att även om du ställer in standard regeln för karantän eller blockera åtkomst, kommer registrerade och kompatibla enheter fortfarande att kunna komma åt Exchange lokalt.  
     Använd den här inställningen när du vill att registrerade och kompatibla enheter alltid ska ha åtkomst till e-post via Exchange lokalt.  

     Detta stöds på följande plattformar: Windows Phone 8 och senare, iOS 6 och senare. Android 4,0 och senare, Samsung KNOX Standard 4,0 och senare.  

     Om du vill använda det här alternativet går du till sidan **Allmänt** i **guiden Konfigurera princip för villkorlig åtkomst** för Exchange lokalt.  

##  <a name="client-online-status"></a><a name="bkmk_clientStatus"></a>Status för klient online  
Från och med Technical Preview 1601 kan du snabbt identifiera om en klient är online eller offline i Configuration Manager-konsolen. Med uppdaterade ikoner och kolumner i konsolens enhets listor kan du utvärdera status för klienter i din miljö för att identifiera problemområden och andra problem som kan behöva åtgärdas.  

En klient är online om den är ansluten till en plats system roll för en Configuration Manager hanterings plats. Så länge hanterings platsen tar emot ping-liknande meddelanden från klienten, är dess status online. Om hanteringen inte tar emot ett meddelande i 5 minuter, ändras klientens status till offline.  

### <a name="icons-for-client-status"></a>Ikoner för klient status  

|||  
|-|-|  
|![ikon för onlinestatus för klienter](media/online-status-icon.png)|Klienten är online.|  
|![ikon för offlinestatus för klienter](media/offline-status-icon.png)|Klienten är offline.|  
|![ikon för okänd status för klienter](media/unknown-status-icon.png)|Klientens status är okänd.|  

### <a name="prerequisites"></a>Krav  
 Klientens onlinestatus saknar krav. Du kan börja använda det så snart Configuration Manager Technical Preview 1601 har installerats.  

### <a name="limitations"></a>Begränsningar  
 Klientens onlinestatus är bara tillgänglig för Windows-datorer med den Configuration Manager-klienten installerad. Klientens onlinestatus stöds inte för Mac-datorer, Linux-eller UNIX-datorer eller enheter som hanteras\-med lokal hantering av mobila enheter.  

### <a name="to-view-client-online-status"></a>Visa klientens onlinestatus  

1. I Configuration Manager-konsolen går du till **till gångar och efterlevnad > översikt > enheter**.  

2. Högerklicka på kolumn rubriken och klicka sedan på ett av fälten för klientens online-status för att lägga till det i vyn enhet. Fälten är  

   -   **Onlinestatus för enhet** anger om klienten är online eller offline.  

   -   **Senaste online-tid** anger när klientens onlinestatus ändrades från offline till online.  

   -   **Senast offline** anger när statusen ändrades från online till offline.  

   Uppdatera-konsolen om du vill visa de senaste ändringarna i klient status.  

##  <a name="improvements-to-application-management"></a><a name="bkmk_appmgmt1601"></a>Förbättringar av program hantering  
 I 1601 Technical Preview har vi lagt till stöd för följande funktioner:  

### <a name="manage-volume-purchased-apps-for-ios-devices"></a>Hantera appar som köpts genom volyminköpsprogrammet för iOS-enheter  
 En del appbutiker erbjuder möjligheten att köpa flera licenser till en app som du vill köra i företaget. Det hjälper dig att minska det administrativa arbetet med att spåra flera köpta kopior av appar.  

 Configuration Manager nu kan du hantera appar som du har köpt via ett sådant program genom att importera licens informationen från App Store och spåra hur många av de licenser som du har använt.  

 Mer information finns i [Hantera appar som du har köpt via ett volym inköps program med Configuration Manager](https://technet.microsoft.com/library/mt627954.aspx).  

### <a name="ios---app-configuration-for-applicationsbr-hybrid"></a>iOS-app-konfiguration för program<br />Hybrid  
 Vissa iOS-program har stöd för förkonfiguration av inställningar, till exempel en server eller databas som programmet ska ansluta till. Configuration Manager stöder nu distribution av konfigurations principer för appar till enheten som gör att användaren kan använda appen direkt utan att behöva känna till den här informationen. Utvecklare måste aktivera den här funktionen i sina appar.  

 Ett begränsat antal offentligt lanserade appar har för närvarande stöd för att konfigurera inställningar. Du kan också ha interna utvecklade branschspecifika appar som stöder dessa.  

#### <a name="prerequisites-for-this-scenario"></a>Krav för det här scenariot  

-   Du måste ha lagt till en Microsoft Intune-prenumeration i Configuration Manager.  

-   Du måste ha lagt till ett giltigt Apple APNs-certifikat i Intune-prenumerationen.  

-   Du måste ha distribuerat ett iOS-program som har stöd för program konfiguration.  

#### <a name="try-it-out"></a>prova!  
 När kraven ovan är uppfyllda måste du skapa ett Configuration Manager-program som använder en distributions typ för iOS. Appen du använder måste ha stöd för program konfigurationen. Läs programmets leverantörs dokumentation för att lära dig vilka specifika objekt (namn/värde-par) som du kan konfigurera.  

 Sedan associerar du appens konfigurations princip med distributions typen iOS vid app-distributionen. Du kan också distribuera principen från noden **konfigurations principer för appar** som är riktad mot en befintlig app och samling.  

 Försök att utföra följande uppgifter och Använd sedan feedback-informationen nära överst i det här avsnittet för att berätta för oss hur de fungerade:  

-   Om du har en iOS-app som stöder konfiguration av appar kan du läsa appens leverantörs dokumentation för att ta reda på vilka namn och värde-par du måste ange för att konfigurera programmet.  

-   Starta guiden **skapa konfigurations princip för appar** . På sidan **iOS-princip** i guiden kan du försöka lägga till namn-och värdepar som du hittar i dokumentationen för program leverantören eller så kan du importera en XML-fil som innehåller de värden som krävs.  

-   I guiden **distribuera program vara** , på sidan **konfigurations princip för appar** , associerar du den konfigurations princip för appar som du skapade med en kompatibel distributions typ från programmet.  

##  <a name="improvements-to-compliance-settings"></a><a name="bkmk_compliance1601"></a>Förbättringar av kompatibilitetsinställningar  
 I 1601 Technical Preview har vi lagt till stöd för följande funktioner:  

### <a name="microsoft-edge-browser-settings"></a>Inställningar för Microsoft Edge-webbläsare  
 Nya inställningar för Microsoft Edge-webbläsaren har lagts till i konfigurations objekt för **windows 8,1 och Windows 10** (inställningarna gäller endast Windows 10-enheter).  

 Om du vill se de nya inställningarna väljer du **Microsoft Edge** på sidan **enhets inställningar** för konfigurations objekt i guiden **skapa konfigurations objekt** .  

 Mer information finns i [så här skapar du konfigurations objekt för windows 8,1-och Windows 10-enheter som hanteras utan Configuration Manager-klienten](../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  

### <a name="compliance-settings-for-windows-10-team-devices"></a>Kompatibilitetsinställningar för Windows 10 team-enheter  
 Använd de här nya kompatibilitetsinställningarna för att konfigurera enheter som kör Windows 10 team, till exempel Surface Hub enheter.  

 Om du vill se de nya inställningarna väljer du **Windows 10 team** på sidan **enhets inställningar** för konfigurations objekt i guiden **skapa konfigurations objekt** .  

 Mer information finns i [så här skapar du konfigurations objekt för windows 8,1-och Windows 10-enheter som hanteras utan Configuration Manager-klienten](../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  

### <a name="android---kiosk-mode-for-samsung-knox-standardbr-hybrid"></a>Android – hel skärms läge för Samsung KNOX Standard<br />Hybrid  
 Med hel skärms läget kan du låsa en enhet så att bara vissa funktioner fungerar. Du kan t.ex. tillåta att enheten endast ska kunna köra en hanterad app som du anger, eller så kan du inaktivera volymknapparna på en enhet. De här inställningarna kan användas på en demonstrationsmodell av en enhet, eller en enhet som bara används för att utföra en enda funktion, till exempel i en butikskassa. De här inställningarna är inte tillgängliga för Samsung KNOX Standard-enheter i konfigurations objekt för **windows 8,1 och Windows 10** (inställningarna gäller endast Windows 10-enheter).  

 Om du vill se de nya inställningarna väljer du **hel skärms läge – Samsung KNOX** på sidan **enhets inställningar** för konfigurations objekt i guiden **skapa konfigurations objekt** .  

 Mer information finns i [så här skapar du konfigurations objekt för windows 8,1-och Windows 10-enheter som hanteras utan Configuration Manager-klienten](../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  
