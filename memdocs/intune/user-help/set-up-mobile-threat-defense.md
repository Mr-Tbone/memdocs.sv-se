---
title: Installera Skydd mot mobilhot på din mobila enhet
description: Ta reda på vad appar för skydd mot mobilhot är och hur du konfigurerar en sådan app.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/20/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.custom: intune-enduser, contperfq1
ms.collection: ''
ms.openlocfilehash: 23d449b6b5edf43ea709f8fce194ac5a8afe8eb4
ms.sourcegitcommit: 19ef60175cbfd5c5d1e213a6d64eded34ee42041
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/21/2020
ms.locfileid: "88725357"
---
# <a name="install-mobile-threat-defense-app"></a>Installera app med skydd mot mobilhot  

> [!TIP]
> Det finns många olika MTD-appar på marknaden. Din organisation bör berätta vilken du vill använda. Om du uppmanas att installera en MTD-app och du inte omedelbart omdirigeras till att konfigurera eller installera appen kan du kontakta IT-supporten för att få hjälp.  

Som en del av din organisations säkerhetskrav kan du behöva installera en MTD-leverantörsapp (Mobile Threat Defense). Den här typen av app identifierar och varnar dig för hot på enheten, till exempel misstänkta appar, nätverk eller OS-sårbarheter.  

Om du inte har den nödvändiga MTD-appen blockeras du från att logga in på skyddade eller hanterade appar (till exempel Microsoft Excel eller OneDrive) med ditt arbets- eller skolkonto. I den här artikeln får du lära dig [hur du installerar en MTD-app](set-up-mobile-threat-defense.md#set-up-mtd-app) och återfår åtkomst.    

## <a name="mtd-apps-for-ios"></a>MTD-appar för iOS
Följande MTD-appar används ofta på iOS-enheter. Välj en app för att öppna dess produktpost i App Store.   

* [Lookout for Work](https://go.microsoft.com/fwlink/?linkid=2139367)
* [Symantec Endpoint Protection (SEP) Mobile](https://go.microsoft.com/fwlink/?linkid=2139141)
* [Sandblast Mobile Protect](https://go.microsoft.com/fwlink/?linkid=2139231)
* [Zimperium zIPS](https://go.microsoft.com/fwlink/?linkid=2139232)


## <a name="mtd-apps-for-android"></a>MTD-appar för Android-enheter 
Följande MTD-appar används ofta på Android-enheter. Välj en app för att öppna dess produktpost i Google Play.  

* [Lookout for Work](https://go.microsoft.com/fwlink/?linkid=2139453)
* [Symantec Endpoint Protection (SEP) Mobile](https://go.microsoft.com/fwlink/?linkid=2139454)
* [SandBlast Mobile Protect](https://go.microsoft.com/fwlink/?linkid=2139455)
* [Zimperium Mobile IPS (zIPS)](https://go.microsoft.com/fwlink/?linkid=2139142)  


## <a name="information-your-organization-can-see"></a>Information din organisation kan se   

Din organisation kan inte se några data, till exempel texter, e-post och bilder, i dina personliga appar. MTD-appen rapporterar information om dina appar, till exempel namn och version, till din organisation. Den faktiska informationen som rapporteras beror på vilken MTD-leverantör företaget använder. Din organisation kanske ser:   

* Appnamn  
* App-ID: Det unika namn som identifierar appen i Google Play.  
* Appversion och kort versionsnummer: De specifika versionsnumren för en app.  
* Appsamling (bundle) och dynamisk storlek: Mängden utrymme en app använder på din enhet. 


## <a name="set-up-mtd-app"></a>Konfigurera MTD-app 
När du loggar in på en skyddad app uppmanas du att installera en MTD-app. Slutför installationen och få tillgång till den skyddade appen genom att följa stegen på skärmen. 

Mer information finns i anvisningarna för [iOS](set-up-mobile-threat-defense.md#ios-setup) eller [Android](set-up-mobile-threat-defense.md#android-setup) i det här avsnittet. De här stegen är kompletterande och är inte avsedda att ersätta de instruktioner som visas på skärmen. 

Om du uppmanas att installera en MTD-app men inte är säker på vilken av dem som ska installeras kontaktar du IT-supporten för att få hjälp.  

### <a name="device-registration"></a>Enhetsregistrering  
Registreringen är nödvändig för att bekräfta din identitet och ansluta ditt skol- eller arbetskonto till enheten. Om enheten inte är registrerad guidas du automatiskt genom de stegen innan du installerar MTD-appen.   

Mer information om enhetsregistrering finns i [Registrera din personliga enhet i organisationens nätverk](https://docs.microsoft.com/azure/active-directory/user-help/user-help-register-device-on-network).  

### <a name="ios-setup"></a>iOS-installation  
De här stegen börjar på skärmen **Få åtkomst** som visas när du har loggat in på en skyddad app.  

1. På skärmen **Få åtkomst** följer du anvisningarna för att installera MTD-appen som krävs av din organisation.   
2. Gå tillbaka till skärmen **Få åtkomst** och välj **Öppna**.  
3. MTD-appen ber om behörighet att öppna Microsoft Authenticator. Välj **Öppna**. 
4. Välj ditt arbetskonto för att logga in. 
5. Vänta medan MTD-appen söker igenom din enhet efter säkerhetshot. 
6. Gå tillbaka till skol- eller arbetsappen som du ursprungligen försökte komma åt. I det här läget kan din organisation uppmana dig att konfigurera andra appsäkerhetskrav, till exempel skapa en PIN-kod.   
7. Du bör nu ha åtkomst till appen. Om du fortfarande är blockerad:  
    * På skärmen **Få åtkomst** väljer du **Kontrollera igen**.  
    * Gå till MTD-appen och sök efter befintliga hot. Slutför de rekommenderade stegen för att lösa hotet och återfå åtkomsten.    

### <a name="android-setup"></a>Android-konfigurering 
De här stegen börjar på skärmen **Få åtkomst** som visas när du har loggat in på en skyddad app.  

1. På skärmen **Få åtkomst** följer du anvisningarna för att installera MTD-appen som krävs av din organisation.  
2. Gå tillbaka till skärmen **Få åtkomst** och välj **Öppna**.  
3. MTD-appen ber om tillåtelse att komma åt vissa delar av enheten, om det behövs. För att den här appen ska fungera korrekt måste du **tillåta** åtkomst till kontakter. De begärda behörigheterna varierar mellan MTD-leverantörerna.  
4. Välj ditt arbetskonto för att logga in.  
5. Vänta medan MTD-appen söker igenom din enhet efter säkerhetshot.  
6. Gå tillbaka till skol- eller arbetsappen som du ursprungligen försökte komma åt. I det här läget kan din organisation uppmana dig att konfigurera andra appsäkerhetskrav, till exempel skapa en PIN-kod.  
7. Du bör nu ha åtkomst till appen. Om du fortfarande är blockerad:  
    * På skärmen **Få åtkomst** väljer du **Kontrollera igen**.  
    * Gå till MTD-appen och sök efter befintliga hot. Slutför de rekommenderade stegen för att lösa hotet och återfå åtkomsten.  


## <a name="resolving-a-threat"></a>Lösa ett hot
Om ett hot påträffas och överskrider organisationens definierade hotnivå kommer din organisation antingen att:  
   
* Blockera åtkomst: Hindrar dig från att använda organisationens skyddade appar när du är inloggad på ditt arbets- eller skolkonto.  
* Rensa data: Tar bort dina arbets- eller skoldata från en eller flera av organisationens skyddade appar.  

Så här löser du ett hot och får åtkomst till skyddade appar:  

1. Öppna MTD-appen på enheten.     
2. Läs igenom hotinformationen i appen som förklarar hur hotet kan påverka din enhet om det kvarstår samt hur du kan åtgärda det. 
3. När du har genomfört de nödvändiga ändringarna på enheten går du tillbaka till MTD-appen och startar en ny genomsökning. Upprepa dessa steg tills alla hot har lösts. Det kan ta några minuter innan ändringarna synkroniseras med din organisation. När dessa ändringar har synkroniserats får du åtkomst till den skyddade appen. 

## <a name="get-support"></a>Få support
Gå till [Företagsportal-webbplatsen](https://go.microsoft.com/fwlink/?linkid=2010980) och leta upp din organisations kontaktuppgifter. Kontakta dem för att få hjälp med:

* Identifiera vilken MTD-app som ska användas  
* Installation  
* Installationen misslyckades  
* Upptäcka/lösa ett hot  
* Avinstallera en MTD-app   
 

### <a name="share-app-logs-with-it-support"></a>Dela apploggar med IT-supporten  
Du kan också skicka dina apploggar till IT-supporten för att ge dem mer sammanhang om en misslyckad installation.  
* Android-användare: [Ladda upp och skicka dina loggar via e-post](https://docs.microsoft.com/mem/intune/user-help/send-logs-to-your-it-admin-by-email-android) från företagsportalen.   

* iOS-enhetsanvändare: [Hämta och skicka dina loggar](https://docs.microsoft.com/intune/apps/manage-microsoft-edge#use-microsoft-edge-to-access-managed-app-logs) från Microsoft Edge för iOS.  


## <a name="next-steps"></a>Nästa steg  

Se följande artiklar för att lära dig mer om hur hanterade appar fungerar, hur du hämtar dem och hur du kan identifiera om du använder en sådan.  

* [Använda hanterade appar på Android-enheten](use-managed-apps-on-your-device-android.md)
* [Använda hanterade appar på iOS-enheten](use-managed-apps-on-your-device-ios.md)  

Behöver du fortfarande hjälp? Kontakta företagssupporten. Titta efter IT-administratörens kontaktuppgifter på [företagsportalens webbplats](https://go.microsoft.com/fwlink/?linkid=2010980).

