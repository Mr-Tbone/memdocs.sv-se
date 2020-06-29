---
title: Registrera din Mac med Intune-företagsportalen | Microsoft Docs
description: Lär dig att registrera din Mac i Intune med företagsportalappen.
keywords: Mac OS X, macOS, OS X
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 06/18/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 3bb659cc-9b57-4d19-8631-2c26749fa71c
searchScope:
- User help
ROBOTS: ''
ms.reviewer: kakyker
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: fe405b66892ec7777d8d1572b2fb6ab6ce1aaa91
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/19/2020
ms.locfileid: "85094225"
---
# <a name="enroll-your-macos-device-using-the-company-portal-app"></a>Registrera din macOS-enhet med företagsportalappen  

Registrera din macOS-enhet i Intune-företagsportalappen för att få säker åtkomst till arbetets eller skolans e-post, filer och appar.

Organisationer kräver vanligtvis att din enhet registreras innan du får åtkomst till upphovsrättsskyddade data. När enheten har registrerats blir den *hanterad*. Din organisation kan tilldela principer och appar till enheten via en MDM-provider för hantering av mobilenheter, t.ex. Intune. För att få kontinuerlig tillgång till arbets- eller skolinformation på enheten måste du konfigurera den så att policyinställningarna matchar organisationens.  

Den här artikeln beskriver hur du använder appen Företagsportal för macOS till att konfigurera och underhålla enheten så att du uppfyller organisationens krav.  


## <a name="what-to-expect-from-the-company-portal-app"></a>Vad du kan förvänta dig av företagsportalappen

Under installationen kräver företagsportalappen att du loggar in och autentiserar dig hos organisationen. Företagsportalen informerar dig sedan om eventuella enhetsinställningar som du behöver konfigurera för att uppfylla organisationens krav. Organisationer anger exempelvis ofta krav på lägsta eller högsta antal tecken i lösenordet som du måste uppfylla.    

När du har registrerat din enhet ser företagsportalen alltid till att enheten är skyddad enligt organisationens krav. Om du till exempel installerar en app från en obetrodd källa varnar företagsportalen dig och kan även begränsa åtkomsten till organisationens resurser. Appskyddsprinciper som den här är vanligt förekommande. För att få tillbaka åtkomsten måste du troligen avinstallera appen. 

Om organisationen inför ett nytt säkerhetskrav efter registreringen, t.ex. multifaktorautentisering, meddelar företagsportalen dig. Du får möjlighet att justera dina inställningar så att du kan fortsätta arbeta från enheten.  

Mer information om registrering finns i [Vad händer när jag installerar företagsportalappen och registrerar min enhet?](what-happens-if-you-install-the-Company-Portal-app-and-enroll-your-device-in-intune-macos.md).  

## <a name="get-your-macos-device-managed"></a>Hantera din macOS-enhet  
Utför följande steg när du ska registrera din macOS-enhet i organisationen. Enheten måste köra macOS 10.12 eller senare.   

> [!NOTE]
> I den här processen kan du uppmanas att tillåta att företagsportalen använder konfidentiell information som finns lagrad i din nyckelring. Dessa meddelanden ingår i Apples säkerhet. När du får frågan skriver du in lösenordet för inloggningsnyckeln och väljer **Tillåt alltid**. Om du trycker på **Enter** eller **Retur** på tangentbordet väljs i stället **Tillåt**, vilket kan resultera i ytterligare frågor.  

### <a name="install-company-portal-app"></a>Installera företagsportalappen  
1. Gå till [Registrera min Mac](https://go.microsoft.com/fwlink/?linkid=853070).  
2. Företagsportalens .pkg-fil för installationsprogrammet laddas ned. Öppna installationsprogrammet och fortsätt med anvisningarna. 
3. Godkänn licensavtalet för programvaran. 
4. Ange enhetens lösenord eller det registrerade fingeravtrycket för att installera programvaran.  
5. Öppna appen Företagsportal. 

> [!IMPORTANT]
> Microsoft AutoUpdate kan öppnas för att uppdatera din Microsoft-programvara. När alla uppdateringar har installerats öppnar du företagsportalappen. För bästa installationsupplevelse installerar du de senaste versionerna av Microsoft AutoUpdate och företagsportalen.  


### <a name="enroll-your-mac"></a>Registrera din Mac  


1. Logga in på företagsportalen med ditt arbets- eller skolkonto.  
2. När appen öppnas väljer du **Börja**.  
3. Granska [vad din organisation kan se och inte kan se](what-info-can-your-company-see-when-you-enroll-your-device-in-intune.md) på din registrerade enhet. Välj sedan **Fortsätt**.
4. På skärmen **Installera hanteringsprofil** väljer du **Ladda ned profil**.  

    ![Exempel på skärmbild av företagsportalen och profilskärmen för installationshantering med lösenordsfrågan markerad.](./media/install-management-profile-macos-2006.png)   

5. Enhetens systeminställningar öppnas.  
    a. Välj **Installera** och sedan **Installera** igen.  
    b. Om du uppmanas till det anger du enhetens lösenord.   
6. När profilen har installerats visas den i listan med profiler under **Hanteringsprofil**.
    ![Exempel på skärmbild av skärmen Systeminställningar och skärmen Hanteringsprofil, med knappen ”Godkänn” markerad.](./media/management-profile-approve-macos-2006.png)   
7. Logga in i Företagsportal.    
8. Din organisation kan kräva att du uppdaterar enhetsinställningarna. När du har uppdaterat inställningarna väljer du **Försök igen**.  

    ![Skärmbild av företagsportalen och skärmen Uppdatera enhetsinställningar, med knappen Försök igen markerad.](./media/update-settings-mac-2006.png)  
9. När installationen är klar trycker du på **Klar**.  


 ## <a name="troubleshooting-and-feedback"></a>Felsökning och feedback   

Om du stöter på problem under registreringen går du till **Hjälp** > **Skicka diagnostikrapport** för att rapportera problemet till Microsofts apputvecklare. Informationen används för att förbättra appen. Den används också för att hjälpa till att lösa problemet om din IT-support kontaktar dem för att få hjälp.  

När du har rapporterat problemet till Microsoft kan du skicka information om det till din IT-support. Välj **Skicka information via e-post**. Beskriv problemet i e-postmeddelandets brödtext. Om du söker efter din supportkontakts e-postadress går du till företagsportalappen > **Kontakt**. Mer information finns på [webbplatsen Företagsportal](https://go.microsoft.com/fwlink/?linkid=2010980).  
 

Dessutom vill Microsoft Intunes företagsportalteam gärna få din feedback. Gå till **Hjälp** > **Skicka feedback** för att dela med dig av dina tankar och idéer.  

## <a name="unverified-profiles"></a>Overifierade profiler  
När du visar de installerade MDM-profilerna för hantering av mobilenheter i **Systeminställningar** > **Profiler**, kan vissa profiler visas med statusen Inte verifierad. Så länge som hanteringsprofilen visar statusen Verifierad behöver du inte bry dig om detta.  

Hanteringsprofilen är vad som definierar MDM-kanalanslutningen. Så länge hanteringsprofilen är verifierad ärver alla andra profiler som levereras till datorn, via kanalen, hanteringsprofilens säkerhetsegenskaper.  

## <a name="updating-the-company-portal-app"></a>Uppdatera företagsportalappen

Företagsportalappen uppdateras på samma sätt som andra Office-appar, genom Microsoft AutoUpdate för macOS. Läs mer om [uppdatering av Microsoft-appar för macOS](https://support.office.com/article/Check-for-Office-for-Mac-updates-automatically-bfd1e497-c24d-4754-92ab-910a4074d7c1).  

## <a name="next-steps"></a>Nästa steg  
Behöver du fortfarande hjälp? Kontakta företagssupporten. Titta efter IT-administratörens kontaktuppgifter på [företagsportalens webbplats](https://go.microsoft.com/fwlink/?linkid=2010980).  


