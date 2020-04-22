---
title: Installera Skydd mot mobilhot på din mobila enhet
description: Lär dig installera Skydd mot mobilhot på din mobila enhet.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/25/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: b5df63a14f27b657c585eb43e09b02368d969939
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "80084404"
---
# <a name="install-mobile-threat-defense"></a>Installera Skydd mot mobilhot   

Som en del av din organisations säkerhetskrav kan du behöva installera en MTD-leverantörsapp (Mobile Threat Defense). Den här typen av app identifierar och varnar dig för hot på enheten, till exempel misstänkta appar, nätverk eller OS-sårbarheter.  

Om du inte har den nödvändiga MTD-appen blockeras du från att logga in på skyddade appar med ditt arbets- eller skolkonto. I den här artikeln får du lära dig [hur du installerar en MTD-app](set-up-mobile-threat-defense.md#install-app) för att bli avblockerad.  

Det finns flera MTD-leverantörsappar som kan installeras. Din organisation meddelar dig vilken som ska användas. 


## <a name="information-your-organization-can-see"></a>Information din organisation kan se   

Din organisation kan inte se några data, till exempel texter, e-post och bilder, i dina personliga appar. MTD-appen rapporterar information om dina appar, till exempel namn och version, till din organisation. Den faktiska informationen som rapporteras beror på vilken MTD-leverantör företaget använder. Din organisation kanske ser:   

* Appnamn  
* App-ID: Det unika namn som identifierar appen i Google Play.  
* Appversion och kort versionsnummer: De specifika versionsnumren för en app.  
* Appsamling (bundle) och dynamisk storlek: Mängden utrymme en app använder på din enhet. 


## <a name="install-app"></a>Installera appen    
När du loggar in på en skyddad app uppmanas du automatiskt att installera en MTD-app. Slutför installationen genom att följa stegen på skärmen. Använd stegen i det här avsnittet för ytterligare hjälp.  
 
Du kan också uppmanas att registrera din enhet. Registreringen är nödvändig för att bekräfta din identitet och ansluta ditt skol- eller arbetskonto till enheten. Om du inte är registrerad guidas du automatiskt genom den konfigurationen innan du installerar MTD-appen. När du kommer till skärmen **Få åtkomst** kan du påbörja installationsstegen.  

Mer information om enhetsregistrering finns i [Registrera din personliga enhet i organisationens nätverk](https://docs.microsoft.com/azure/active-directory/user-help/user-help-register-device-on-network).  

### <a name="ios-setup"></a>iOS-installation  

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

1. På skärmen **Få åtkomst** följer du anvisningarna för att installera MTD-appen som krävs av din organisation.  
2. Gå tillbaka till skärmen **Få åtkomst** och välj **Öppna**.  
3. MTD-appen ber om tillåtelse att komma åt vissa delar av enheten, om det behövs. För att den här appen ska fungera korrekt måste du **tillåta** åtkomst till kontakter. De begärda behörigheterna varierar mellan MTD-leverantörerna.  
4. Välj ditt arbetskonto för att logga in.  
5. Vänta medan MTD-appen söker igenom din enhet efter säkerhetshot.  
6. Gå tillbaka till skol- eller arbetsappen som du ursprungligen försökte komma åt. I det här läget kan din organisation uppmana dig att konfigurera andra appsäkerhetskrav, till exempel skapa en PIN-kod.  
7. Du bör nu ha åtkomst till appen. Om du fortfarande är blockerad:  
    * På skärmen **Få åtkomst** väljer du **Kontrollera igen**.  
    * Gå till MTD-appen och sök efter befintliga hot. Slutför de rekommenderade stegen för att lösa hotet och återfå åtkomsten.  

### <a name="installation-failed"></a>Installationen misslyckades  

Kontakta din IT-support om installationen misslyckas. Gå till [Företagsportal-webbplatsen](https://go.microsoft.com/fwlink/?linkid=2010980) och leta upp din organisations kontaktuppgifter.  

Du kan också skicka dina apploggar till IT-supporten för att ge dem mer sammanhang om installationen.  
* Android-användare: [Ladda upp och skicka dina loggar via e-post](https://docs.microsoft.com/mem/intune/user-help/send-logs-to-your-it-admin-by-email-android) från företagsportalen.   

* iOS-enhetsanvändare: [Hämta och skicka dina loggar](https://docs.microsoft.com/intune/apps/manage-microsoft-edge#use-microsoft-edge-to-access-managed-app-logs) från Microsoft Edge för iOS.  

## <a name="resolve-a-threat"></a>Lösa ett hot  
Om ett hot överskrider organisationens definierade hotnivå kommer din organisation antingen att:  
   
* Blockera åtkomst: Hindrar dig från att använda organisationens skyddade appar när du är inloggad på ditt arbets- eller skolkonto.  
* Rensa data: Tar bort dina arbets- eller skoldata från en eller flera av organisationens skyddade appar.  

Öppna MTD-appen enheten för att lösa ett hot och återfå åtkomsten. Läs igenom den tillhandahållna informationen för att lära dig hur hotet kan påverka din enhet och hur du kan lösa det. När du har följt stegen för att lösa hotet går du tillbaka till MTD-appen och startar en ny genomsökning. Det kan ta några minuter att få åtkomst till din organisation igen.  

## <a name="next-steps"></a>Nästa steg  

Behöver du fortfarande hjälp? Kontakta företagssupporten. Titta efter IT-administratörens kontaktuppgifter på [företagsportalens webbplats](https://go.microsoft.com/fwlink/?linkid=2010980).

