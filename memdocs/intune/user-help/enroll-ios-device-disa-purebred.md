---
title: Registrera en iOS- eller iPadOS-enhet med Intune-företagsportalen och DISA Purebred
description: Lär dig hur du registrerar en iOS-eller iPad-enhet och konfigurerar autentisering av härledd autentisering med DISA Purebred.
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
ms.openlocfilehash: 38d1b40ecdeee5bfd872297a5fd4f0229cb48dcf
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79337596"
---
# <a name="set-up-ios-or-ipados-device-with-company-portal-and-disa-purebred"></a>Konfigurera en iOS- eller iPadOS-enhet med Intune-företagsportalen och DISA Purebred  

Registrera din enhet med appen för Intune-företagsportal om du vill få säker mobil åtkomst till din organisations e-post, filer och appar. När enheten har registrerats blir den *hanterad*. Din organisation kan tilldela principer och appar till enheten via en MDM-provider för hantering av mobilenheter, t.ex. Intune.  

Under registreringen ska du även installera härledda autentiseringsuppgifter på enheten. Din organization kan kräva att du använder härledda autentiseringsuppgifter som en autentiseringsmetod när du får åtkomst till resurser, eller för att signera och kryptera e-post. 

Det är sannolikt att du behöver konfigurera en härledd autentiseringsuppgift om du använder ett smartkort för att:

* Logga in på skol- eller arbetsappar, Wi-Fi och virtuella privata nätverk (VPN)
* Signera och kryptera e-post för skola eller arbete med S/MIME-certifikat  

I den här artikeln kommer du att:  

   * Registrera en mobil iOS- eller iPadOS-enhet med Intune-företagsportalen.  
   * Hämta en härledd autentiseringsuppgift från organisationens leverantör av den härledda autentiseringsuppgiften, [DISA Purebred](https://cyber.mil/pki-pke/purebred/).  

## <a name="what-are-derived-credentials"></a>Vad är härledda autentiseringsuppgifter?  
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

Du måste också kontakta en Purebred-agent eller representant under installationen.      

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
    b. Öppna Purebred-appen genom att klicka på **Öppna**.  

    ![Exempel på skärmbild av företagsportalen skärm till mobil smartkortåtkomst.](./media/smart-card-open-disa-purebred.png)  
9. När du uppmanas att tillåta företagsportalen att öppna Purebreds registreringsapp väljer du **Öppna**.   

    ![Exempel på skärmbild av företagsportalsfrågan för att öppna DISA Purebred-appen.](./media/open-app-prompt-disa-purbred.png)  
10. När appen fungerar arbetar du med organisationens Purebred-agent för att konfigurera och ladda ned konfigurationsprofilen för Purebred-förregistrering.   
11. Gå till appen Inställningar > **Allmänt** > **Profiler och enhetshantering** > **Installera profil** och tryck på **Installera**.  
12. Ange ditt enhetslösenord.  
13. Installera profilen. Du kan behöva trycka på **Installera** mer än en gång för att starta installationen. 
14. Gå tillbaka till Purebreds registreringsapp. Följ Purebred-agentens instruktioner för att fortsätta.  
 
15. När du har laddat ned konfigurationsprofilen går du till appen Inställningar > **Allmänt** > **Profiler och enhetshantering** > **Installera profil** och trycker på **Installera**.   
16.  Ange ditt enhetslösenord.
17. Installera profilen. Du kan behöva trycka på **Installera** mer än en gång för att starta installationen. 
18. När installationen är klar återgår du till företagsportalappen.  
19.  På skärmen **Ställ in åtkomst till mobilens smartkort** trycker du på **Fortsätt**.  

20. På skärmen **Importera certifikat** hämtar och importerar du de härledda autentiseringsuppgifter som du fick från DISA Purebred.  

    a. Tryck på **Fortsätt**.   

    ![Exempel på skärmbild av företagsportalens skärm för att ställa in Importera certifikat.](./media/import-certificate-disa-purebred.png)  
    b. Gå till iCloud-enheten **Bläddra** > **Platser** och tryck på **More Locations** (Fler platser).  

    ![Exempel på skärmbild av iCloud-enhet, Bläddra-menyn för att markera alternativet More Locations (Fler platser).](./media/icloud-drive-more-locations.png)  
    c. Aktivera **Purebred Key Chain** genom att trycka på växeln.  

    ![Exempel på skärmbild av iCloud-enhet, Bläddra-vyn, markera att Purebred Key Chain är aktiverat.](./media/icloud-drive-enable-purebred-keychain.png)   

    d. Tryck på **Purebred Credential Package**.  

    ![Exempel på skärmbild av en iOS-skärm med ett valbart alternativ för Purebred Credential Package.](./media/purebred-credential-package.png)  
    f. En lista över certifikat visas. Välj en och tryck sedan på **Importnyckel**.  

    ![Exempel på en skärmbild av en lista över certifikat som kan väljas, med ett redan valt.](./media/import-purebred-keychain.png) 
21. Återgå till företagsportalappen och vänta medan företagsportalen har slutfört konfigurationen av enheten.   

## <a name="next-steps"></a>Nästa steg  
När registreringen är klar har du åtkomst till arbetsresurser, till exempel e-post, Wi-Fi och alla appar som din organisation gör tillgängliga. Mer information om hur du hämtar, söker efter, installerar och avinstallerar appar i företagsportalen finns i:

* [Hantera appar från Företagsportal-webbplatsen](manage-apps-cpweb.md)  
* [Använda hanterade appar på enheten](use-managed-apps-on-your-device-ios.md)  

Behöver du fortfarande hjälp? Kontakta företagssupporten. Titta efter IT-administratörens kontaktuppgifter på [företagsportalens webbplats](https://go.microsoft.com/fwlink/?linkid=2010980).
