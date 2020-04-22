---
title: Registrera en iOS- eller iPadOS-enhet med Intune-företagsportalen och Intercede
description: Lär dig att registrera en iOS- eller iPad-enhet och konfigurera härledd autentisering med Intercede.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/31/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: tisilver
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 8caf05a2869088fd4f8206d1306d82c696f527a2
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81638214"
---
# <a name="set-up-ios-or-ipados-device-with-company-portal-and-intercede"></a>Konfigurera en iOS- eller iPadOS-enhet med företagsportalen och Intercede

Registrera din enhet med appen för Intune-företagsportal om du vill få säker mobil åtkomst till din organisations e-post, filer och appar.  När enheten har registrerats blir den *hanterad*. Din organisation kan tilldela principer och appar till enheten via en MDM-provider för hantering av mobilenheter, t.ex. Intune.  

Under registreringen ska du även installera härledda autentiseringsuppgifter på enheten. Din organisation kan kräva att du använder härledda autentiseringsuppgifter som en autentiseringsmetod när du får åtkomst till resurser, eller för att signera och kryptera e-post. 

Det är sannolikt att du behöver konfigurera en härledd autentiseringsuppgift om du använder ett smartkort för att:

* Logga in på skol- eller arbetsappar, Wi-Fi och virtuella privata nätverk (VPN)
* Signera och kryptera e-post för skola eller arbete med S/MIME-certifikat  

I den här artikeln kommer du att:  

* Registrera en mobil iOS- eller iPadOS-enhet med Intune-företagsportalen.  
* Hämta en härledd autentiseringsuppgift från organisationens leverantör av den härledda autentiseringsuppgiften, [Intercede](https://www.intercede.com/).   


## <a name="what-are-derived-credentials"></a>Vad är härledda autentiseringsuppgifter?  
En härledd autentiseringsuppgift är ett certifikat som härleds från smartkortets autentiseringsuppgifter och som är installerat på din enhet. Det ger dig fjärråtkomst till arbetsresurser samtidigt som det förhindrar att obehöriga användare får åtkomst till känslig information.  

Härledda autentiseringsuppgifter används för att: 
* Autentisera elever och medarbetare som loggar in på skol- eller arbetsappar, Wi-Fi och VPN
* Signera och kryptera e-post för skola eller arbete med S/MIME-certifikat  

Härledda autentiseringsuppgifter är en implementering av riktlinjerna från National Institute of Standards and Technology (NIST) för härledda PIV-autentiseringsuppgifter (Personal Identity Verification) som en del av en Special Publication (SP) 800-157.  

## <a name="prerequisites"></a>Förutsättningar

 För att slutföra registreringen måste du ha:

* Ditt smartkort för skola eller arbete
* Åtkomst till en dator eller självbetjäningskiosk där du kan logga in med ditt smartkort
* Din mobila enhet
* Intunes-företagsportalappen för iOS och iPadOS installerad på din enhet


## <a name="enroll-device"></a>Registrera enhet  
1. Öppna företagsportalappen för iOS/iPadOS på din mobila enhet och logga in med ditt arbetskonto.  
2. Skriv ner koden som visas på skärmen.  

    ![Exempelbild på företagsportalappen med meddelandet och koden på skärmen.](./media/copy-code-intercede.png)  
1. Växla till din smartkortaktiverade enhet och gå till https://microsoft.com/devicelogin. 

1. Ange koden som du skrev ned förut.
 
2. Sätt i smartkortet för att logga in.   

3. Gå tillbaka till företagsportalappen på din mobila enhet och följ anvisningarna på skärmen för att registrera enheten.  
4. När registreringen är klar meddelar företagsportalen dig att du ska konfigurera smartkortet. Tryck på meddelandet. Om du inte får något meddelande bör du kontrollera din e-post.   

    ![Exempel på skärmbild av företagsportalens push-meddelande på enhetens startsida.](./media/action-required-in-app-intercede.png)  

5. På skärmen **Ställ in åtkomst till mobilens smartkort**:  
    a. Tryck på länken till organisationens konfigurationsanvisningar. Om din organisation inte har några ytterligare anvisningar, kommer du att skickas till den här artikeln.  
    b. Tryck på **Börja**.  

    ![Exempel på skärmbild av företagsportalens skärm för mobil smartkortåtkomst.](./media/smart-card-info-intercede.png)  

6. Växla till din smartkortaktiverade enhet eller självbetjäningskiosk och öppna MyID-appen. Logga in med dina autentiseringsuppgifter för arbetet.  
7. Välj alternativet för att begära ditt ID. 
8. När du tillfrågas om vilken profil du vill använda, väljer du alternativet att aktivera med en mobilautentiseringsuppgift. En QR-kod visas.  
9. Gå tillbaka till din mobila enhet. I Företagsportal > skärmen **Hämta QR-kod** trycker du på **Fortsätt**.  

    ![Exempel på skärmbild av skärmen Företagsportal > Hämta QR-kod.](./media/get-qr-code-intercede.png) 
 
10. Tryck på **Använd kamera** > **OK**.  

    ![Exempel på skärmbild av en fråga i företagsportalen om att få åtkomst till kameran.](./media/allow-cp-camera-access-intercede.png)  

11. Skanna bilden av QR-koden som finns på din smartkortaktiverade enhet. 
12. Vänta tills företagsportalen har slutfört konfigurationen av enheten.  

## <a name="next-steps"></a>Nästa steg  
När registreringen är klar har du åtkomst till arbetsresurser, till exempel e-post, Wi-Fi och alla appar som din organisation har gjort tillgängliga. Mer information om hur du hämtar, söker efter, installerar och avinstallerar appar i företagsportalen finns i:

* [Hantera appar från Företagsportal-webbplatsen](manage-apps-cpweb.md)  
* [Använda hanterade appar på enheten](use-managed-apps-on-your-device-ios.md)  

Behöver du fortfarande hjälp? Kontakta företagssupporten. Titta efter IT-administratörens kontaktuppgifter på [företagsportalens webbplats](https://go.microsoft.com/fwlink/?linkid=2010980).
