---
title: Registrera en iOS- eller iPadOS-enhet med Intune-företagsportalen och Entrust Datacard
description: Registrera en iOS- eller iPadOS-enhet och konfigurera härledd autentisering med Entrust Datacard.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/31/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: tisilver
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 763d67c393eede1920f356e54d6ab422bc75a480
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79348503"
---
# <a name="set-up-ios-or-ipados-device-with-company-portal-and-entrust-datacard"></a>Konfigurera en iOS- eller iPadOS-enhet med företagsportalen och Entrust Datacard

Registrera din enhet med appen för Intune-företagsportal om du vill få säker mobil åtkomst till din organisations e-post, filer och appar. När enheten har registrerats blir den *hanterad*. Din organisation kan tilldela principer och appar till enheten via en MDM-provider för hantering av mobilenheter, t.ex. Intune.  

Under registreringen ska du även installera härledda autentiseringsuppgifter på enheten. Din organization kan kräva att du använder härledda autentiseringsuppgifter som en autentiseringsmetod när du får åtkomst till resurser, eller för att signera och kryptera e-post. 

Det är sannolikt att du behöver konfigurera en härledd autentiseringsuppgift om du använder ett smartkort för att:  

* Logga in på skol- eller arbetsappar, Wi-Fi och virtuella privata nätverk (VPN)
* Signera och kryptera e-post för skola eller arbete med S/MIME-certifikat  

I den här artikeln kommer du att:  

   * Registrera en mobil iOS- eller iPadOS-enhet med Intune-företagsportalen.  
   * Hämta en härledd autentiseringsuppgift från organisationens provider för den härledda autentiseringsuppgiften [Entrust Datacard](https://www.entrustdatacard.com/).  

### <a name="what-are-derived-credentials"></a>Vad är härledda autentiseringsuppgifter?  
En härledd autentiseringsuppgift är ett certifikat som härleds från autentiseringsuppgifter för smartkort och som är installerat på din enhet. Det ger dig fjärråtkomst till arbetsresureser samtidigt som det förhindrar obehöriga användare att komma åt känslig information.  

Härledda autentiseringsuppgifter används för att: 
* Autentisera studenter och medarbetare som loggar in på skol- eller arbetsappar, Wi-Fi och VPN
* Signera och kryptera e-post för skola eller arbete med S/MIME-certifikat

Härledda autentiseringsuppgifter är en implementering av riktlinjerna från National Institute of Standards and Technology (NIST) för härledda PIV-autentiseringsuppgifter (Personal Identity Verification) som en del av en Special Publication (SP) 800-157.  

## <a name="prerequisites"></a>Krav

 För att slutföra registreringen måste du ha:

* Ditt smartkort som tillhandahålls av skola eller arbete
* Åtkomst till en dator eller kiosk där du kan logga in med ditt smartkort
* Din mobila enhet
* Intunes-företagsportalsappen för iOS och iPadOS installerad på din enhet  


## <a name="enroll-device"></a>Registrera enhet  
1. Öppna företagsportalappen för iOS/iPadOS på din mobila enhet och logga in med ditt arbetskonto.  

2. Skriv ned koden på skärmen.  

    ![Exempelavbildning på företagsportalappen med meddelandet och koden på skärmen.](./media/copy-code-intercede.png)   

3. Växla till din smartkortaktiverade enhet och gå till https://microsoft.com/devicelogin. 
4. Ange koden du tidigare skrev ned.  

    ![Exempel på skärmbild på företagsportalswebbplatsens uppmaning ”Ange kod”.](./media/enter-code-intercede.png)   

5. Infoga smartkortet för att logga in.   
6. Gå tillbaka till företagsportalen på din mobila enhet och följ anvisningarna på skärmen för att registrera enheten.  
7. När registreringen är klar meddelar företagsportalen dig att du ska konfigurera smartkortet. Tryck på meddelandet. Om du inte får ett meddelande bör du kontrollera din e-post.   

    ![Exempel på skärmbild av företagsportalen push-meddelande på enhetens startsida.](./media/action-required-in-app-intercede.png)  

8. På skärmen **Ställ in åtkomst till mobilens smartkort**:   
    a. Tryck på länken till organisationens konfigurationsinstruktioner. Om din organisation inte tillhandahåller ytterligare instruktioner kommer du att skickas till den här artikeln.  
    b. Tryck på **Börja**.  

    ![Exempel på skärmbild av företagsportalen skärm till mobil smartkortåtkomst.](./media/smart-card-info-intercede.png)

9. Växla till din smartkortaktiverade enhet och öppna IdentityGuard. 
10. Hitta inloggningsområdet för smarta autentiseringsuppgifter och välj inloggningsknappen.  
11. När du uppmanas att välja ett certifikat väljer du autentiseringsuppgifterna för smartkortet. Välj sedan **OK**. 
12. Ange PIN-koden för smartkortet.  
13. Du uppmanas att välja från en lista med åtgärder. Välj en som låter dig registrera dig för en härledd mobil smart autentiseringsuppgift. På länken eller knappen kan det stå **I'd like to enroll for a derived mobile smart card credential** (Jag vill registrera mig för en härledd mobil autentiseringsuppgift för smartkort).  
14. Välj att du har laddat ned och installerat programmet är som är aktiverat för smarta autentiseringsuppgifter. Fortsätt sedan till nästa skärm.   
15. Ange information om dina härledda autentiseringsuppgifter för smartkort.  
    a. För identitetsnamnet anger du ett namn, till exempel *Entrust-härledda aut*.  
    b. På listmenyn väljer du **Entrust IdentityGudard Mobile Smart Credential** (Mobil smart autentiseringsuppgift för Entrust IdentityGudard).  
    c. Fortsätt till nästa skärm. Du ser en QR-kod med ett numeriskt lösenord under.  

16. Återgå till din mobila enhet. I Företagsportal > skärmen **Hämta QR-kod** trycker du på **Fortsätt**. 

    ![Exempel på skärmbild av skärmen Företagsportal Hämta QR-kod.](./media/get-qr-code-intercede.png)  
17. Tryck på **Använd kamera** > **OK**.  

    ![Exempel på skärmbild av en Företagsportalsfråga som ber om behörighet att tillåta åtkomst till kameran.](./media/allow-cp-camera-access-intercede.png)  
18. Skanna avbildningen av QR-koden som finns på din Smart Cards-aktiverade enhet.  
19. Ange det numeriska lösenordet som visas under QR-koden.  

    ![Exempel på skärmbild av skärmen Company Portal Password (Lösenord för företagsportal) anger du lösenordsfältet.](./media/enter-password-derived-credentials.png)   

20. Vänta tills företagsportalen har slutfört konfigurationen av enheten.  


## <a name="next-steps"></a>Nästa steg  
När registreringen är klar har du åtkomst till arbetsresurser, till exempel e-post, Wi-Fi och alla appar som din organisation gör tillgängliga. Mer information om hur du hämtar, söker efter, installerar och avinstallerar appar i företagsportalen finns i:

* [Hantera appar från Företagsportal-webbplatsen](manage-apps-cpweb.md)  
* [Använda hanterade appar på enheten](use-managed-apps-on-your-device-ios.md)  

Behöver du fortfarande hjälp? Kontakta företagssupporten. Titta efter IT-administratörens kontaktuppgifter på [företagsportalens webbplats](https://go.microsoft.com/fwlink/?linkid=2010980).  
