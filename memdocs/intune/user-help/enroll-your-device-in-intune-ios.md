---
title: Konfigurera iOS-enhetsåtkomst till företagsresurser | Microsoft Docs
description: Beskriver hur du hämtar en iOS-enhet som hanteras av Intune
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 12/18/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 6eeec7aa-1b07-4ce3-894c-13e09b89bdd4
searchScope:
- User help
ROBOTS: ''
ms.reviewer: tisilv
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: aeb2e22348e7197f0abb62ee540c37079f8645f4
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/21/2020
ms.locfileid: "80084689"
---
# <a name="set-up-ios-device-access-to-your-company-resources"></a>Konfigurera iOS-enhetsåtkomst till företagsresurser  

Registrera din iOS-enhet i Intune-företagsportalappen för att få säker åtkomst till organisationens e-post, filer och appar.

När enheten har registrerats blir den *hanterad*. Din organisation kan tilldela principer och appar till enheten via en MDM-provider för hantering av mobilenheter, t.ex. Intune.  

> [!NOTE]
> Vi säljer inte några data som samlas in av vår tjänst till någon tredje part av någon anledning.  

För att kunna komma åt arbets- eller skolinformation från din enhet måste du konfigurera enheten så att den matchar organisationens önskade inställningar. Den här artikeln beskriver hur du använder Företagsportalen för att registrera enheten och underhålla organisationens inställningskrav.  
</br>
> [!VIDEO https://www.youtube.com/embed/mJyv6YcHi7c?rel=0]

> [!NOTE]
> Om du försökte komma åt företagets e-post i e-postprogrammet och du fick ett meddelande om att enheten måste vara hanterad, är du på rätt plats. Följ anvisningarna nedan för att få åtkomst till din e-post och andra företagsresurser på iOS-enheten.  


## <a name="what-to-expect-from-the-company-portal-app"></a>Vad du kan förvänta dig av företagsportalappen  

### <a name="security"></a>Säkerhet  
Under installationen kräver appen att du autentiserar dig själv hos organisationen. Du informeras sedan om eventuella enhetsinställningar som du behöver uppdatera. Organisationer anger exempelvis ofta krav på lägsta eller högsta antal tecken i lösenordet som du måste uppfylla.

### <a name="protection"></a>Skydd  
När enheten har registrerats fortsätter företagsportalappen att se till att enheten är skyddad. Om du till exempel installerar en app från en ej betrodd källa kommer appen meddela dig och återkallar ibland åtkomst till företagets data. Den här typen av princip är vanlig i organisationer och kräver ofta att du avinstallerar den icke betrodda appen innan du kan få åtkomst igen.  

### <a name="setting-notifications"></a>Konfigurera meddelanden  
Om organisationen inför ett nytt säkerhetskrav efter registreringen, t.ex. multifaktorautentisering, meddelar företagsportalappen dig. Du får möjlighet att justera dina inställningar så att du kan fortsätta arbeta från enheten.  

Mer information om registrering finns i [Vad händer när jag installerar företagsportalappen och registrerar min enhet?](https://docs.microsoft.com//mem/intune/user-help/what-happens-if-you-install-the-company-portal-app-and-enroll-your-device-in-intune-ios).  

## <a name="enroll-your-ios-device"></a>Registrera din iOS-enhet  

Gå till appbutiken för att ladda ned och installera [Intune-företagsportalappen ](install-and-sign-in-to-the-intune-company-portal-app-ios.md) på din enhet. Du måste även ha en Wi-Fi-anslutning och åtkomst till Safari under registreringen. 

En paus på mer än några minuter under registreringen göra att appen stängs eller att installationen avslutas. Om detta inträffar öppnar du företagsportalappen och försöker igen.  

1. Öppna företagsportalen och logga in med ditt arbets- eller skolkonto.  

2. När du uppmanas att ta emot meddelanden från företagsportalappen trycker du på **Tillåt**. Företagsportalen använder meddelanden för att avisera dig, t.ex. om dina enhetsinställningar behöver uppdateras.  

3. Välj **Börja** på skärmen **Konfigurera åtkomst**.   

    ![Exempel på skärmbild av Företagsportal, skärmen ”Konfigurera åtkomst”.](./media/ios-enrollment-checklist-1909.PNG)  

4. Skärmen **Välj enhet och typ av registrering** visas och du får ange din enhetstyp.  
    * Tryck på **(organisation) äger den här enheten** om du har fått enheten från din organisation. Gå sedan vidare till [Skydda hela enheten](#secure-entire-device) i den här artikeln och slutför konfigurationen.  
    * Tryck på **Jag äger enheten** om du använder en personlig enhet som du har tagit med hemifrån. Fortsätt sedan till nästa steg.  

    Om du inte ser den här skärmen kan du gå vidare till [Skydda hela enheten](#secure-entire-device) och slutföra konfigurationen.  
    
    ![Exempelbild på skärmen ”Välj enhet och typ av registrering” i företagsportalen med olika enhetstypsalternativ.](./media/ios-device-type-1909.PNG)  


5. Välj hur du vill skydda data på enheten när den är registrerad.  
    * Tryck på **Skydda hela enheten** om du vill skydda alla appar och data på enheten. Gå sedan till [Skydda hela enheten](enroll-your-device-in-intune-ios.md#secure-entire-device) för att slutföra konfigurationen.
    * Tryck på **Skydda endast arbetsrelaterade appar och data** om du bara vill skydda de appar och data som används via arbetskontot. Gå sedan till [Skydda arbetsrelaterade appar och data](enroll-your-device-in-intune-ios.md#secure-work-related-apps-and-data).  

    ![Exempelbild på skärmen ”Välj enhet och typ av registrering” i företagsportalen med olika registreringsalternativ.](./media/ios-enrollment-type-1909.PNG)  


### <a name="secure-entire-device"></a>Skydda hela enheten  

1. Gå igenom listan med enhetsinformation som din organisation kan och inte kan se på skärmen **Enhetshantering och sekretess**. Tryck sedan på **Fortsätt**.  


 > [!IMPORTANT]
> Nästa steg och vilka skärmar som visas varierar beroende på din iOS-version. Följ anvisningarna för din iOS-version. 

2. Safari öppnar webbplatsen för Företagsportal på enheten. När du uppmanas att ladda ned konfigurationsprofilen trycker du på **Tillåt**. Om du använder en enhet som kör:  
    * iOS 12.2 och senare: När nedladdningen har slutförts trycker du på **Stäng**. Fortsätt därefter till steg 3.  
    * iOS 12.1 och tidigare: När nedladdningen är färdig omdirigeras du automatiskt till appen Inställningar. Gå vidare till steg 4.  
 
    Om du trycker på **Ignorera** av misstag, uppdaterar du sidan. Du uppmanas att öppna appen Företagsportal. Väl där trycker du på **Ladda ned igen**.

  > [!NOTE]
  > Du måste installera hanteringsprofilen enligt beskrivningen i nästa steg inom 8 minuter efter nedladdningen. Annars tas profilen bort och du måste börja om registreringen.  

3. När du uppmanas att öppna företagsportalen trycker du på **Öppna**. Läs igenom informationen på skärmen **Så här installerar du hanteringsprofilen**.  

4. Öppna appen Inställningar och tryck på **Registrera i <organisationsnamn>** eller **Profilen har laddats ned**.  

    ![Exempelbild av appen Inställningar, alternativet Registrera i organisation.](./media/enroll-in-organization-ios-1909.PNG)  

   Om du inte ser några alternativ går du till **Allmänt** > **Profiler och enhetshantering**> **Hanteringsprofil**. Om du fortfarande inte ser någon hanteringsprofil kan du behöva ladda ned den igen.  

5. Tryck på **Installera**.  
    
6. Ange ditt enhetslösenord. Tryck sedan på **Installera**.    

7. Nästa skärm är en standardsystemvarning för enhetshantering. Fortsätt med installationen genom att trycka på **Installera**. Om du uppmanas att lita på fjärrhantering trycker du på **Förtroende**.  

8. När installationen är klar trycker du på **Klar**. Kontrollera att profilen har installerats, gå till inställningarna för **Profiler och enhetshantering**. Du bör se profilen under **Hantering av mobilenheter**.   

    ![Exempel på skärmbild av appen Inställningar, inställningar för Profiler och enhetshantering, som visar hanteringsprofilen.](./media/ios-12-cp-enroll-1904.PNG)  

9. Gå tillbaka till appen Företagsportal. Företagsportalen börjar synkronisera och konfigurera din enhet. Du kan uppmanas att uppdatera ytterligare enhetsinställningar. I så fall trycker du på **Fortsätt**.  

10. Du vet att installationen är klar när alla objekt i listan visas med en grön bockmarkering. Tap **Klar**.   

> [!Note]
> Om din organisation övervakar röst- och databegränsningar, eller ger dig en företagsägd enhet, kan du behöva utföra några ytterligare steg. Om du uppmanas att installera appen **Datalert** läser du avsnittet om hur du [registrerar din enhet i kostnadshanteringen för telekommunikation](enroll-your-device-with-telecom-expense-management-ios.md). Om din organisation är en del av Apples program för enhetsregistrering (DEP) tar du reda på [hur du registrerar din företagsägda enhet](enroll-your-device-dep-ios.md).  

### <a name="secure-work-related-apps-and-data"></a>Skydda arbetsrelaterade appar och data  
1. Skärmen **Ladda ned Microsoft Authenticator** visas (om du redan har Authenticator ser du inte den här skärmen, så gå vidare till steg 2).  
    1. Tryck på **Ladda ned från App Store**.
    2. När App Store öppnas installerar du appen. 
    3. Gå tillbaka till företagsportalen och tryck på **Fortsätt**.    
    
   När du har installerat Microsoft Authenticator behöver du inte göra något mer i appen. Den behöver bara finnas på enheten. 

   ![Exempelbild av företagsportalen, skärmen ”Ladda ned Microsoft Authenticator”.](./media/download-ms-authenticator-1909.PNG)  

2. Gå igenom listan med enhetsinformation som din organisation kan och inte kan se på skärmen **Enhetshantering och sekretess**. Tryck sedan på **Fortsätt**.  


 > [!IMPORTANT]
> Nästa steg och vilka skärmar som visas varierar beroende på din iOS-version. Följ anvisningarna för din iOS-version. 

3. Safari öppnar webbplatsen för Företagsportal på enheten. När du uppmanas att ladda ned konfigurationsprofilen trycker du på **Tillåt**. Om du använder en enhet som kör:  
    * iOS 12.2 och senare: När nedladdningen har slutförts trycker du på **Stäng**. Fortsätt därefter till steg 4.  
    * iOS 12.1 och tidigare: När nedladdningen är färdig omdirigeras du automatiskt till appen Inställningar. Gå vidare till steg 5.  
 
    Om du trycker på **Ignorera** av misstag, uppdaterar du sidan. Du uppmanas att öppna appen Företagsportal. Från appen kan du trycka på **Ladda ned igen**.

  > [!NOTE]
  > Du måste installera hanteringsprofilen enligt beskrivningen i nästa steg inom 8 minuter efter nedladdningen. Annars tas profilen bort och du måste börja om registreringen.  

4. När du uppmanas att öppna företagsportalen trycker du på **Öppna**. Läs igenom informationen på skärmen **Så här installerar du hanteringsprofilen**. 

5. Öppna appen Inställningar och tryck på **Registrera i <organisationsnamn>** eller **Profilen har laddats ned**.  

    ![Exempelbild av appen Inställningar, alternativet Registrera i organisation.](./media/enroll-in-organization-ios-1909.PNG)  

   Om du inte ser några alternativ går du till **Allmänt** > **Profiler och enhetshantering**> **Hanteringsprofil**. Om du fortfarande inte ser någon hanteringsprofil kan du behöva ladda ned den igen.   


6. På skärmen **Användarregistrering** trycker du på **Registrera min iPhone**.  

    ![Exempelbild av appen Inställningar, skärmen Användarregistrering, knappen Registrera framhävd.](./media/user-enrollment-information-1909.PNG)  

7. Ange enhetslösenordet. Tryck sedan på **Installera**.  

8. På skärmen **Logga in** anger du lösenordet för ditt hanterade Apple-ID. I de flesta fall är de här autentiseringsuppgifterna samma som de du använder till att logga in på ditt arbets- eller skolkonto, om inte organisationen har försett dig med andra autentiseringsuppgifter. 
9. Tryck på **Logga in**.  
10. Du ser ett meddelande på skärmen när profilen har installerats. Kontrollera att profilen har installerats genom att gå till inställningarna för  **Profiler och enhetshantering** . Du bör se profilen under  **Hantering av mobilenheter.**  

    ![Exempel på skärmbild av appen Inställningar, inställningar för Profiler och enhetshantering, som visar hanteringsprofilen.](./media/ios-12-cp-enroll-1904.PNG)  

11. Gå tillbaka till appen Företagsportal. Företagsportalen börjar synkronisera och konfigurera din enhet. Du kan uppmanas att uppdatera ytterligare enhetsinställningar. I så fall trycker du på **Fortsätt**.    

12. Du vet att installationen är klar när alla objekt i listan visas med en grön bockmarkering. Tryck på  **Klar**.  

## <a name="it-administrator-support"></a>IT-administratörssupport  
Om du är IT-administratör och stöter på problem när du registrerar enheter kan du läsa [Felsöka problem med registrering av iOS-enhet i Microsoft Intune](https://support.microsoft.com/en-us/help/4039809). Den här artikeln innehåller vanliga fel, deras orsaker och stegen för att lösa dem.  

## <a name="next-steps"></a>Nästa steg  
Hitta appar som hjälper dig i arbetet eller skolan. Lär dig [hur appar blir tillgängliga](use-managed-apps-on-your-device-ios.md) för dig via Företagsportalen.  

Behöver du fortfarande hjälp? Kontakta företagets support. Du hittar kontaktinformationen på [Företagsportalens webbplats](https://go.microsoft.com/fwlink/?linkid=2010980).  
