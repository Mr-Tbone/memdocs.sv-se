---
title: Funktioner i Technical Preview 1604
titleSuffix: Configuration Manager
description: Lär dig mer om funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1604.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 684a5559-9e6e-469b-86ae-e768e9f0c9ac
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 1785880af8c7d0d106abfe3eea8ecd390f6ce6b1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074460"
---
# <a name="capabilities-in-technical-preview-1604-for-configuration-manager"></a>Funktioner i Technical Preview 1604 för Configuration Manager

*Gäller för: Configuration Manager (Technical Preview Branch)*

Den här artikeln beskriver de funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1604. Du kan installera den här versionen för att uppdatera och lägga till nya funktioner till din Configuration Manager Technical Preview-webbplats.      Innan du installerar den här versionen av Technical Preview kan du läsa introduktions avsnittet, [teknisk för hands version för Configuration Manager](../../core/get-started/technical-preview.md), för att bekanta dig med allmänna krav och begränsningar för att använda en teknisk för hands version, hur du uppdaterar mellan versioner och hur du ger feedback om funktionerna i en teknisk för hands version.  

 Följande är nya funktioner som du kan prova med den här versionen.  

##  <a name="manage-volume-purchased-apps-from-the-windows-store-for-business"></a><a name="BKMK_WindowsVPP"></a>Hantera volym köpta appar från Windows Store för företag  
 [Windows Store för företag](https://www.microsoft.com/business-store) är där du kan hitta och köpa appar för din organisation, enskilt eller i volym. Genom att ansluta butiken till Configuration Manager kan du hantera volym köpta appar från Configuration Manager-konsolen, till exempel:  

-   Du kan synkronisera listan med köpta appar med Configuration Manager  

-   Appar som är synkroniserade visas i Configuration Manager-konsolen och du kan distribuera dem precis som andra appar  

-   Du kan spåra hur många licenser som är tillgängliga och hur många som används i Configuration Manager-konsolen  

### <a name="try-it-out"></a>prova!  

##### <a name="scenario-1-set-up-windows-store-for-business-synchronization"></a>Scenario 1: Konfigurera Windows Store för företag-synkronisering  

1.  I Azure Active Directory registrerar du Configuration Manager som hanterings verktyg för webb program och/eller webb-API. Då får du ett klient-ID som du kommer att behöva senare.  

    1.  I noden **Active Directory** i [https://manage.windowsazure.com](https://manage.windowsazure.com)väljer du din Azure Active Directory och klickar sedan på **program** > **Lägg till**.  

    2.  Klicka på **Lägg till ett program som min organisation utvecklar**.  

    3.  Ange ett namn för programmet, Välj **webb program** och/eller **webb-API**och klicka sedan på pilen nästa.  

    4.  Ange samma URL för både **inloggnings-URL: en** och **app-ID-URI: n**.  URL: en kan vara vad som helst och behöver inte matcha en riktig adress. Du kan till exempel ange **&lt;https://dindomän\>/SCCM**.  

    5.  Slutför guiden.  

2.  I Azure Active Directory skapar du en klient nyckel för det registrerade hanterings verktyget.  

    1.  Markera det program som du nyss skapat och klicka på **Konfigurera**.  

    2.  Under **nycklar**väljer du en varaktighet i listan och klickar på **Spara**.  Då skapas en ny klient nyckel.  Navigera inte från den här sidan förrän du har registrerat Windows Store för företag till Configuration Manager.  

3.  Konfigurera Configuration Manager som lagrings hanterings verktyg i Windows Store för företag.  

    1.  Öppna [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/en-us/managementtools) och logga in om du uppmanas att göra det.  

    2.  Godkänn användnings villkoren om det behövs.  

    3.  Under **hanterings verktyg**klickar du på **Lägg till ett hanterings verktyg**.  

    4.  I **Sök efter verktyget efter namn**, anger du namnet på det program som du skapade i AAD tidigare och klickar sedan på **Lägg till**.  

    5.  Klicka på **Aktivera** bredvid det program som du nyss importerade.  

    6.  I guiden **Visa offline-licensierade appar** klickar du på **Ja** om du vill tillåta att offline-licensierade program kan köpas.  

4.  Köp minst en app från Windows Store för företag.  

5.  I arbets ytan **Administration** i Configuration Manager-konsolen expanderar du **Cloud Services**och klickar sedan på **Windows Store för företag**.  

6.  På fliken **Start** går du till gruppen **skapa** och klickar på **Lägg till Windows Store för företag-konto**.  

7.  Lägg till klient-ID, klient-ID och klient nyckel från Azure Active Directory och slutför sedan guiden.  

8.  När du är färdig visas det konto som du konfigurerade i listan **Windows Store för företag-konton** i Configuration Manager-konsolen.  

##### <a name="scenario-2-create-and-deploy-a-configuration-manager-application-from-a-windows-store-for-business-offline-licensed-app"></a>Scenario 2: skapa och distribuera ett Configuration Manager program från en Windows Store för företag-licensierad program vara  

1.  I arbets ytan **program varu bibliotek** i Configuration Manager-konsolen expanderar du **program hantering**och klickar sedan på **licens information för Store-appar**.  

2.  I listan **köpta Windows Store för företag-appar** visas en lista över appar som synkroniserats från Store. Välj den app som du vill distribuera och klicka sedan på **skapa program**i gruppen **skapa** på fliken **Start** .  

3.  Ett Configuration Manager program skapas som innehåller appen Windows Store för företag. Sedan kan du distribuera och övervaka programmet på samma sätt som andra Configuration Manager program.  

##  <a name="improvements-to-microsoft-passport-for-work-management"></a><a name="BKMK_PFW"></a>Förbättringar av Microsoft Passport for Work hantering  
 Nu kan du distribuera Passport for Work-principer till domänanslutna Windows 10-enheter som hanteras av Configuration Manager-klienten.  

##  <a name="option-for-clients-to-switch-to-a-new-software-update-point"></a><a name="bkmk_switchsup"></a>Alternativ för klienter att växla till en ny program uppdaterings plats  
 I 1604 Technical Preview kan du aktivera alternativet för Configuration Manager klienter ska växla till en ny program uppdaterings plats när det finns problem med den aktiva program uppdaterings platsen. För det här alternativet måste du ha flera program uppdaterings platser tillgängliga på en primär plats. Du aktiverar det här alternativet på en enhets samling och när den är aktive rad kommer klienterna i samlingen att söka efter en annan program uppdaterings plats vid nästa genomsökning när klienten Miss lyckas med att ansluta till den aktiva program uppdaterings platsen. Beroende på dina konfigurations inställningar för WSUS (uppdaterings klassificeringar, produkter osv.), genererar växeln till en ny program uppdaterings plats ytterligare nätverks trafik. Använd därför bara det här alternativet när det är ett måste.  

#### <a name="to-enable-the-option-to-switch-software-update-points"></a>Så här aktiverar du alternativet för att byta programuppdateringsplats  

1.  Klicka på **Tillgångar och efterlevnad > Översikt > Enhetssamlingar** i Configuration Manager-konsolen.  

2.  På fliken **Start** ,i gruppen **Samling** klickar du på **Klientmeddelande** och sedan på **Byt till nästa programuppdateringspunkt**.  

> [!NOTE]  
>  Det här alternativet är bara tillgängligt på platser som har flera program uppdaterings platser.  

##  <a name="client-settings-to-manage-client-cache-settings-and-client-peer-cache"></a><a name="bkmk_peercache"></a>Klient inställningar för att hantera inställningar för klient-cache och klient-peer-cache  
 Technical Preview version 1604 introducerar två nya enhets klient inställningar som påverkar användningen av en klients cacheminne. Båda kan användas individuellt men konfigureras på samma egenskaps sida för klient inställningar och kombineras för att hjälpa dig att hantera distribution av innehåll till klienter på fjärrplatser.  

-   Det första är **klient-peer-cache**, en inbyggd Configuration Manager-lösning som klienter kan använda för att dela innehåll med andra klienter direkt från deras lokala cacheminne. För att peer-cache-klienter ska kunna dela innehåll måste de vara medlemmar i samma avgränsnings grupp. Peer-cache ersätter inte användningen av andra lösningar som BracnchCache utan fungerar i stället sida vid sida för att ge dig fler alternativ för att utöka traditionella innehålls distributions lösningar som distributions platser.  

     När du har distribuerat klient inställningar som aktiverar peer-cache till en samling kan medlemmar i samlingen fungera som peer-innehålls källa för andra klienter i dess gränser grupp.  Klienten som fungerar som en peer-innehålls källa skickar en lista över tillgängligt innehåll som den har cachelagrat till hanterings platsen. När nästa klient i den begränsande gruppen begär innehåll, erbjuds peer cache-källan som en potentiell innehålls källa tillsammans med alla distributions platser som är konfigurerade att vara snabba. Klienten väljer en slumpmässig innehålls källa från den här kombinerade poolen med innehålls källor. Klienterna söker bara efter innehåll från en distributions plats som är konfigurerad att vara långsam när det inte finns några snabba distributions platser eller peer-cache-källor i gränser gruppen.  

-   Med den andra nya inställningen kan du **hantera storleken på cachen** på klienter. Du kan ange att cachen ska ha en maximal storlek i megabyte och en maximal storlek som procent andel av klienternas enhets utrymme.  Klienten tillämpar den inställning som nåtts först.  

För att hjälpa dig att förstå användningen av klient-peer-cache kan du Visa instrument panelen för **klient data källor** . I-konsolen går du till **övervakning > klient Status > klient data källor**. Här kan du välja en tids period som ska gälla för instrument panelen. Sedan kan du välja den gränser grupp eller det paket som du vill visa information för i visningen. När du visar information kan du Hovra musen över ytan för att se mer information om de olika innehålls-eller princip källorna.  

 Du kan också använda en ny rapport, **klient data källor – Sammanfattning**för att visa en sammanfattning av klientens data källor för varje avgränsnings grupp.   
**Krav för att använda peer-cache:**  

-   Du måste konfigurera platsen med ett **konto för nätverks åtkomst** som har **fullständig kontroll** över cache-mappen på varje klient. Som standard är detta **%windir%\ccmcache**  

-   Klienter kan bara överföra innehåll med peer-cache när de är medlemmar i samma avgränsnings grupp.  

#### <a name="to-configure-client-peer-cache-client-settings"></a>Konfigurera klient inställningar för peer-cachelagring  

1.  Båda inställningarna konfigureras på samma sida med klient inställningar. I Configuration Manager-konsolen går du till **Administration > klient inställningar**och öppnar sedan enhets klient inställnings objekt som du vill använda. Du kan också ändra standard klient inställnings objekt.  

2.  I listan över tillgängliga inställningar väljer du **Inställningar för klient-cache**.  

3.  Om du vill hantera storleken på cachen anger du **Konfigurera klientens cachestorlek** lika med **Ja**. Sedan kan du konfigurera den maximala cachestorleken för både megabyte och som en procent andel av klienternas enhets utrymme.  

4.  Om du vill att klienter ska delta i klientens peer-cache anger du **aktivera Configuration Manager-klienten i fullständigt operativ system för att dela innehåll** som är lika med **Ja**. Sedan kan du konfigurera de portar som klienter använder, inklusive om de ska vara HTTP eller HTTPS.  

### <a name="try-it-out"></a>prova!  
 Försök att utföra följande uppgifter och Använd sedan feedback-informationen nära överst i det här avsnittet för att berätta för oss hur det fungerade:  

1.  Ändra klient inställningarna för att ange en ny storlek för klientens cacheminne och bekräfta sedan inställningen på en klient.  

2.  Använd klient inställningar för att konfigurera flera klienter att använda peer-cache  

3.  Distribuera innehåll till klienter så att vissa eller de flesta klienter får det innehållet från en annan klient med hjälp av peer-cache.  Du kan bekräfta innehålls källan som används genom att visa den nya instrument panelen.  

    > [!NOTE]  
    >  För att slutföra den här uppgiften med den tekniska för hands versionen och en enda distributions plats konfigurerar du distributions platsen så att den blir långsam för nätverks platsen för alla klienter. Distribuera sedan innehållet till en enda klient.  När klienten hämtar innehållet kan du distribuera innehållet till ytterligare klienter som ska hitta lokala peer-datorer som ska användas som en innehålls källa innan du använder distributions platsen som anses vara långsam från klientens plats.  

##  <a name="support-for-passport-for-work-as-a-ksp"></a><a name="bkmk_passport"></a>Stöd för Passport for Work som en KSP  
 Med Configuration Manager kan du integrera med Microsoft Passport for Work som är en alternativ inloggnings metod som använder Active Directory eller ett Azure Active Directory konto för att ersätta ett lösen ord, smartkort eller virtuellt smartkort.  
Passport gör det möjligt att använda en användargest för att logga in i stället för ett lösenord. En användargest kan vara en enkel PIN-kod, biometrisk autentisering, t.ex. Windows Hello, eller en extern enhet, t.ex. en fingeravtrycksläsare.  

-   Du kan använda Configuration Manager för att kontrol lera vilka gester användare kan och inte kan använda för att logga in och för att konfigurera komplexitets krav för PIN.  

-   Du kan lagra certifikat för autentisering i nyckellagringsprovidern (KSP) för Passport for Work.  

När en användare skapar en PIN-kod för Passport skickar Windows ett meddelande som Configuration Manager lyssnar efter.  På så sätt kan Configuration Manager snabbt bli medveten om vilka användare som har skapat en PIN-kod för Passport. Configuration Manager kan sedan även utfärda nya certifikat till användarna om Passport används som nyckel lagrings leverantör i en certifikat profil.  

##  <a name="on-premises-device-health-attestation"></a><a name="bkmk_onpremdha"></a>Lokala Hälsoattestering för enhet  
 Hälsoattestering för Windows 10-enheter kan nu konfigureras för att kommunicera med den lokala infrastrukturen.  Administratörer kan ange om rapportering görs via molnet eller lokala resurser.  Om **lokalt** har valts för rapportering av hälso deklarationen kan en URI anges för tjänsten. Detta gör att klient datorer utan Internet åtkomst kan använda för att aktivera och hantera enheter som använder hälsoattestering.  

#### <a name="enable-health-attestation-for-on-premises-devices"></a>Aktivera hälsoattestering för lokala enheter  

1.  I Configuration Manager-konsolen navigerar du till **Administration** > **Översikt** > **klient inställningar**och anger sedan **Använd tjänsten för den lokala tjänsten för hälso** tillstånd till **Ja**.  

2.  Ange **URL till lokal hälsoattesteringstjänst**och klicka sedan på **OK**.  

Konfigurera tjänsten för lokal hälsoattestering med hjälp av inställningarna för klient agenten för att testa den.  

##  <a name="smartlock-setting-for-android-devices"></a><a name="BKMK_Smart"></a>Smart Lock-inställning för Android-enheter  
 En ny inställning, **Tillåt Smart Lock och andra betrodda agenter** har lagts till i konfigurationsobjektet **Android och Samsung KNOX** som låter dig styra Smart Lock-funktionen på kompatibla Android-enheter. Med den här telefonfunktionen, som ibland kallas förtroendeagenter, kan du inaktivera eller kringgå lösenordet för enhetens låsskärm om enheten är på en betrodd plats, till exempel när det är anslutet till en specifik bluetoothenhet eller när den är nära en NFC-tagg. Du kan använda den här inställningen för att förhindra att slutanvändare konfigurerar Smart Lock.  
