---
title: Registrera Android-enhet med Microsoft Intune-appen och Entrust Datacard
description: Registrera en Android-enhet och konfigurera härledd autentisering med Entrust Datacard.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/17/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: jeyang
ms.suite: ems
ms.custom: intune-enduser
ms.collection: M365-identity-device-management
ms.openlocfilehash: 16d14a802c82918656741c137da672e501ddd41a
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83879370"
---
# <a name="set-up-android-device-with-company-portal-and-entrust-datacard"></a>Konfigurera en Android-enhet med företagsportalen och Entrust Datacard

Registrera din enhet med Microsoft Intune-appen om du vill få säker mobil åtkomst till din organisations e-post, filer och appar. När enheten har registrerats blir den *hanterad*. Din organisation kan tilldela principer och appar till enheten via en MDM-provider för hantering av mobilenheter, t.ex. Intune.

Under registreringen ska du även installera härledda autentiseringsuppgifter på enheten. Din organisation kan kräva att du använder härledda autentiseringsuppgifter som en autentiseringsmetod när du får åtkomst till resurser, eller för att signera och kryptera e-post.

Det är sannolikt att du behöver konfigurera en härledd autentiseringsuppgift om du använder ett smartkort för att:

* Logga in på skol- eller arbetsappar, Wi-Fi och virtuella privata nätverk (VPN)
* Signera och kryptera e-post för skola eller arbete med S/MIME-certifikat

I den här artikeln kommer du att:

* Registrera en mobil Android-enhet med Intune-appen
* Konfigurera smartkortet genom att installera en härledd autentiseringsuppgift från organisationens leverantör av den härledda autentiseringsuppgiften, [Entrust Datacard](https://www.entrustdatacard.com/)

## <a name="what-are-derived-credentials"></a>Vad är härledda autentiseringsuppgifter?

En härledd autentiseringsuppgift är ett certifikat som härleds från smartkortets autentiseringsuppgifter och som är installerat på din enhet. Det ger dig fjärråtkomst till arbetsresurser samtidigt som det förhindrar att obehöriga användare får åtkomst till känslig information.

Härledda autentiseringsuppgifter används för att:

* Autentisera elever och medarbetare som loggar in på skol- eller arbetsappar, Wi-Fi och VPN
* Signera och kryptera e-post för skola eller arbete med S/MIME-certifikat

Härledda autentiseringsuppgifter är en implementering av riktlinjerna från National Institute of Standards and Technology (NIST) för härledda PIV-autentiseringsuppgifter (Personal Identity Verification) som en del av en Special Publication (SP) 800-157.

## <a name="prerequisites"></a>Krav

 För att slutföra registreringen måste du ha:

* Ditt smartkort som tillhandahålls av skola eller arbete
* Åtkomst till en dator eller kiosk där du kan logga in med ditt smartkort
* En ny eller fabriksåterställd enhet som kör Android 7.0 eller senare
* Microsoft Intune-appen installerad på din enhet

## <a name="enroll-device"></a>Registrera enhet  

1. Aktivera din nya eller fabriksåterställda enhet.  
2. Välj språk på **välkomstskärmen**. Om du har fått instruktioner om att registrera med en QR-kod eller NFC följer du de nedanstående steg som matchar metoden.  
     * NFC: Vidrör en programmeringsenhet med din NFC-stödda enhet för att ansluta till organisationens nätverk. Följ uppmaningarna på skärmen. När du når skärmen för användningsvillkoren för Chrome fortsätter du till steg 5.  

     * QR-kod: Slutför stegen i [QR-kodsregistrering](#qr-code-enrollment).  

     Om du har fått instruktioner om att använda en annan metod fortsätter du till steg 3.    

3. Anslut till Wi-Fi och tryck på **NÄSTA**. Följ de steg som matchar din registreringsmetod. 

    * Token: När du kommer till inloggningssidan för Google slutför du stegen i [Tokenregistrering](#token-enrollment).  
    * Google Zero Touch: När du har anslutit till Wi-Fi identifieras enheten av din organisation. Fortsätt till steg 4 och följ anvisningarna på skärmen tills installationen är klar.    
 
       ![Exempelbild på skärmen med villkor för Google som visas om du använder Google Zero Touch, med knappen Godkänn och fortsätt markerad.](./media/google-zero-touch-intune-app-01.png)   
   
4. Granska villkoren för Google. Tryck sedan på **GODKÄNN OCH FORTSÄTT**.  

      ![Exempelbild på skärmen för Google-villkor med knappen Godkänn och fortsätt markerad.](./media/fully-managed-intune-app-04.png)   

5. Granska användningsvillkoren för Chrome. Tryck sedan på **GODKÄNN OCH FORTSÄTT**.  

   ![Exempelbild på skärmen för Chrome-användningsvillkor med knappen Godkänn och fortsätt markerad.](./media/fully-managed-intune-app-06.png)   

6. På inloggningsskärmen trycker du på **inloggningsalternativ** och sedan **Logga in från en annan enhet**. 

7. Skriv ned koden på skärmen.  

8. Växla till den smartkort-aktiverade enheten och gå till webbadressen som visas på skärmen. 

9. Ange koden som du skrev ned förut.

   > [!div class="mx-imgBorder"]
   > ![Skärmbild av uppmaningen ”Ange kod” på företagsportalens webbplats.](./media/enter-code-intercede.png)

10. Sätt i smartkortet för att logga in.  

11. På inloggningsskärmen väljer du ditt arbets- eller skolkonto. Växla sedan tillbaka till din mobila enhet. 

12. Beroende på din organisations krav kan du uppmanas att uppdatera inställningar såsom skärmlås eller kryptering. Om du ser de här uppmaningarna trycker du på **KONFIGURERA** och följer instruktionerna på skärmen.  

       ![Exempelbild på Konfigurera på arbetstelefonskärmen med knappen Konfigurera markerad.](./media/fully-managed-intune-app-10.png)   

13. För att installera arbetsappar på enheten trycker du på **INSTALLERA**. När installationen är klar trycker du på **NÄSTA**.  

       ![Exempelbild på Konfigurera på arbetstelefonskärmen med knappen Installera markerad.](./media/fully-managed-intune-app-11.png)    

14. Tryck på **START** för att öppna Microsoft Intune-appen. 

    ![Exempelbild på Konfigurera på arbetstelefonskärmen med knappen Start markerad.](./media/fully-managed-intune-app-17.png)   
 
15. Gå tillbaka till Intune-appen på din mobila enhet och följ anvisningarna på skärmen tills registreringen är klar. 

    ![Exempelbild på lyckad konfiguration, skärmen Registrera din enhet, med knappen Klar markerad.](./media/fully-managed-intune-app-19.png)   

16. Fortsätt till avsnittet [Konfigurera smartkort](enroll-android-device-entrust-datacard.md#set-up-smart-card) i den här artikeln för att slutföra konfigurationen av enheten.  

### <a name="qr-code-enrollment"></a>QR-kodsregistrering  
I det här avsnittet skannar du den QR-kod som du fått av företaget.  När du är klar omdirigeras du tillbaka till stegen för enhetsregistrering.     
  
1. På sidan **Välkommen** trycker du på skärmen fem gånger för att starta QR-kodskonfiguration.  

   ![Exempelbild på välkomstskärmen för enhetskonfiguration med instruktioner att trycka på skärmen markerade.](./media/qr-code-intune-app-01.png)  

2. Följ alla anvisningar på skärmen för att ansluta till Wi-Fi.  
3. Om enheten inte har en QR-kodsläsare visar installationsskärmarna förloppet när en skanner installeras. Vänta tills installationen är klar.  
4. När du uppmanas skannar du registreringsprofilens QR-kod som du fått av din organisation.  
5. Gå tillbaka till steg 4 i [Registrera enhet](#enroll-device) för att fortsätta med installationen.  

### <a name="token-enrollment"></a>Tokenregistrering  
I det här avsnittet anger du den token som du fått av företaget. När du är klar omdirigeras du tillbaka till stegen för enhetsregistrering.  

1. På skärmen för Google-inloggning går du till rutan **E-post eller telefon** och skriver **afw#setup**. Tryck sedan på **Nästa**. 

   ![Exempelbild på Google-inloggningsskärmen som visar att ”afw#setup” skrivs in i fältet.](./media/token-intune-app-01.png)   

2. Välj **Installera** för appen **Android Device Policy**. Fortsätt att gå igenom installationen. Beroende på din enhet kan du behöva granska och godkänna ytterligare villkor.    

3. På skärmen **Registrera den här enheten** väljer du **Nästa**.  

4. Välj **Ange kod**.  

5. På skärmen **Skanna eller ange kod** skriver du in den kod som du har fått av din organisation.  Klicka sedan på **Nästa**.  

   ![Exempelbild på skärmen Skanna eller ange kod med knappen Nästa markerad.](./media/token-intune-app-04.png)  

6. Gå tillbaka till steg 4 i [Registrera enhet](#enroll-device) för att fortsätta med installationen.

## <a name="set-up-smart-card"></a>Konfigurera smartkort  

1. När registreringen är klar meddelar Intune-appen dig att du ska konfigurera smartkortet. Tryck på meddelandet. Om du inte får något meddelande bör du kontrollera din e-post.

   > [!div class="mx-imgBorder"]
   > ![Exempel på skärmbild av företagsportalens push-meddelande på enhetens startsida.](./media/action-required-in-app-android.png)

2. På skärmen **Konfigurera smartkort**:

   1. Tryck på länken till organisationens konfigurationsanvisningar. Om din organisation inte tillhandahåller ytterligare instruktioner kommer du att skickas till den här artikeln.

   2. Tryck på **BÖRJA**. 

   > [!div class="mx-imgBorder"]
   > ![Exempel på skärmbild av företagsportalens skärm för mobil smartkortåtkomst.](./media/smart-card-open-entrust-android.png)

3. Växla till din smartkortaktiverade enhet och öppna IdentityGuard.

4. Hitta inloggningsområdet för smarta autentiseringsuppgifter och välj inloggningsknappen.

5. När du uppmanas att välja ett certifikat väljer du autentiseringsuppgifterna för smartkortet. Välj sedan **OK**.

6. Ange PIN-koden för smartkortet.

7. Du uppmanas att välja från en lista med åtgärder. Välj en som låter dig registrera dig för en härledd mobil smart autentiseringsuppgift. På länken eller knappen kan det stå **I'd like to enroll for a derived mobile smart card credential** (Jag vill registrera mig för en härledd mobil autentiseringsuppgift för smartkort).

8. Välj att du har laddat ned och installerat programmet är som är aktiverat för smarta autentiseringsuppgifter. Fortsätt sedan till nästa skärm.

9. Ange information om dina härledda autentiseringsuppgifter för smartkort:

    1. För identitetsnamnet anger du ett namn, till exempel *Entrust-härledda aut*.  
    2. På listmenyn väljer du **Entrust IdentityGuard Mobile Smart Credential** (Mobil smart autentiseringsuppgift för Entrust IdentityGuard).

    3. Fortsätt till nästa skärm. Du ser en QR-kod med ett numeriskt lösenord under.

10. Återgå till Android-enheten. I Intune-appen > på skärmen **Hämta QR-kod** trycker du på **NÄSTA**.

    > [!div class="mx-imgBorder"]
    > ![Exempel på skärmbild av skärmen Företagsportal > Hämta QR-kod.](./media/get-qr-code-entrust-android.png)

11. Om du uppmanas att tillåta att Intune-appen använder kameran trycker du på **Tillåt**.

12. Skanna bilden av QR-koden som finns på din smartkortaktiverade enhet.

13. På skärmen **Lösenord krävs** anger du lösenordet som visas under QR-koden.

    > [!div class="mx-imgBorder"]
    > ![Exempel på skärmbild av skärmen Company Portal Password (Lösenord för företagsportal).](./media/password-required-entrust-android.png)  

14. Intune-appen börjar hämta och installera de certifikat som krävs för att få åtkomst till arbets- eller skolresurser. Den här processen kan ta lite tid, beroende på din Internet-anslutning. Stäng inte appen medan den pågår.

    > [!div class="mx-imgBorder"]
    > ![Exempel på skärmbild av företagsportalens skärm för att ladda ner och installera certifikat](./media/install-certificates-entrust-android.png)

15. När alla certifikat har bearbetats väntar du tills Intune-appen har slutfört konfigurationen av enheten. Du vet att installationen är klar när du ser texten **Nu är du klar!** .

    > [!div class="mx-imgBorder"]
    > ![Exempel på skärmbild av skärmen ”Nu är du klar!”](./media/all-set-android.png)

## <a name="next-steps"></a>Nästa steg

När registreringen är klar har du åtkomst till arbetsresurser, till exempel e-post, Wi-Fi och alla appar som din organisation har gjort tillgängliga. Mer information om hur du hämtar, söker efter, installerar och avinstallerar appar i Intune-appen finns i:

* [Använda hanterade appar på enheten](use-managed-apps-on-your-device-android.md)  
* [Hantera appar från Företagsportal-webbplatsen](manage-apps-cpweb.md)  

Behöver du fortfarande hjälp? Kontakta företagssupporten. Titta efter IT-administratörens kontaktuppgifter på [företagsportalens webbplats](https://go.microsoft.com/fwlink/?linkid=2010980).