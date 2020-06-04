---
title: Registrera en Android-enhet med Microsoft Intune-appen och DISA Purebred
description: Lär dig hur du registrerar en Android-enhet och konfigurerar autentisering av härledd autentisering med DISA Purebred.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 05/15/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: jeyang
ms.suite: ems
ms.custom: intune-enduser
ms.collection: M365-identity-device-management
ms.openlocfilehash: 584392891320f96eed16863225ffb323dc240594
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83880621"
---
# <a name="set-up-android-device-with-the-microsoft-intune-app-and-disa-purebred"></a>Konfigurera Android-enhet med Microsoft Intune-appen och DISA Purebred

Registrera din enhet med Microsoft Intune-appen om du vill få säker mobil åtkomst till din organisations e-post, filer och appar. När enheten har registrerats blir den *hanterad*. Din organisation kan tilldela principer och appar till enheten via en MDM-provider för hantering av mobilenheter, t.ex. Intune.  

Under registreringen ska du även installera härledda autentiseringsuppgifter på enheten. Din organisation kan kräva att du använder härledda autentiseringsuppgifter som en autentiseringsmetod när du får åtkomst till resurser, eller för att signera och kryptera e-post.

Det är sannolikt att du behöver konfigurera en härledd autentiseringsuppgift om du använder ett smartkort för att:

* Logga in på skol- eller arbetsappar, Wi-Fi och virtuella privata nätverk (VPN)
* Signera och kryptera e-post för skola eller arbete med S/MIME-certifikat

I den här artikeln kommer du att:

* Registrera en mobil Android-enhet med Intune-appen
* Konfigurera smartkortet genom att installera en härledd autentiseringsuppgift från organisationens leverantör av den härledda autentiseringsuppgiften, [DISA Purebred](https://public.cyber.mil/pki-pke/purebred/)

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
* Purebred-appen som är installerad på enheten (appen bör installeras automatiskt strax efter installationen av enheten. Om inte kontaktar du IT-supporten).

Du måste också kontakta en Purebred-agent eller representant under installationen.

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

16. Fortsätt till avsnittet [Konfigurera smartkort](enroll-android-device-disa-purebred.md#set-up-smart-card) i den här artikeln för att slutföra konfigurationen av enheten.  

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

1. På skärmen för Google-inloggning går du till rutan **E-post eller telefon** och skriver **afw#setup**. Tryck på **nästa**. 

   ![Exempelbild på Google-inloggningsskärmen som visar att ”afw#setup” skrivs in i fältet.](./media/token-intune-app-01.png)   

2. Välj **Installera** för appen **Android Device Policy**. Fortsätt att gå igenom installationen. Beroende på din enhet kan du behöva granska och godkänna ytterligare villkor.    

3. På skärmen **Registrera den här enheten** väljer du **Nästa**.  

4. Välj **Ange kod**.  

5. På skärmen **Skanna eller ange kod** skriver du in den kod som du har fått av din organisation.  Klicka sedan på **Nästa**.  

   ![Exempelbild på skärmen Skanna eller ange kod med knappen Nästa markerad.](./media/token-intune-app-04.png)  

6. Gå tillbaka till steg 4 i [Registrera enhet](#enroll-device) för att fortsätta med installationen.


## <a name="set-up-smart-card"></a>Konfigurera smartkort  

> [!NOTE]
> Purebred-appen krävs för att slutföra de här stegen och installeras automatiskt på enheten efter registreringen. Kontakta din IT-support om du fortfarande inte har appen när du har väntat en kort stund.  

1. När registreringen är klar meddelar Intune-appen dig att du ska konfigurera smartkortet. Tryck på meddelandet. Om du inte får något meddelande bör du kontrollera din e-post.

   > [!div class="mx-imgBorder"]
   > ![Skärmbild av Intune-appens push-meddelande på enhetens startsida.](./media/action-required-in-app-android.png)

2. På skärmen **Konfigurera smartkort**:

   1. Tryck på länken till organisationens konfigurationsanvisningar och se över dem. Om din organisation inte tillhandahåller ytterligare instruktioner kommer du att skickas till den här artikeln.

   2. Tryck på **BÖRJA**.   

   > [!div class="mx-imgBorder"]
   > ![Skärmbild av appen Intune, skärmen Konfigurera smartkort.](./media/smart-card-open-disa-purebred-android.png)

3. På skärmen för att **hämta certifikat** trycker du på **STARTA PUREBRED** för att öppna Purebred-appen. (Appen bör ha installerats automatiskt på enheten. Kontakta support om du inte har den.)  

   > [!div class="mx-imgBorder"]
   > ![Skärmbild av uppmaningen i appen Intune för att öppna DISA Purebred-appen.](./media/open-app-prompt-disa-purbred-android.png)  

4. Purebred-appen kan behöva ytterligare behörigheter för att kunna köras korrekt. Tryck på **Tillåt** eller **Tillåt alla** när du uppmanas till det. Mer information om varför dessa behörigheter krävs får du genom att prata med supporten eller Purebred-agenten.  

5. När du är i Purebred-appen arbetar du med din organisations Purebred-agent för att ladda ned och installera de certifikat du behöver för att få åtkomst till arbets- eller skolresurser.

    > [!IMPORTANT]
    > Under den här processen trycker du på **OK** eller **Installera** när du uppmanas till det. Ändra inte namnen på alla certifikatutfärdare eller certifikat som du uppmanas att installera.    

6. När installationen är klar får du ett meddelande om att dina certifikat är klara. Tryck på meddelandet för att återgå till Intune-appen.

    > [!div class="mx-imgBorder"]
    > ![Skärmbild av skärmen Allow access to certificates (Tillåt åtkomst till certifikat)](./media/certificates-ready-prompt-disa-purbred-android.png)

7. På skärmen **Allow access to certificates** (Tillåt åtkomst till certifikat) ger du Intune-appen behörighet att komma åt de härledda autentiseringsuppgifter som du fick från DISA Purebred. Det här steget ser till att din organisation kan verifiera din identitet när du har åtkomst till skyddade arbets- eller skolresurser.  

    1. Tryck på **NÄSTA**.

       > [!div class="mx-imgBorder"]
       > ![Skärmbild av uppmaningen om att dina certifikat är klara](./media/certificates-access-disa-purbred-android.png)

    2. Ändra inte valet när du uppmanas att **välja certifikat**. Rätt certifikat har redan markerats, så tryck bara på **Välj** eller **OK**.  

       > [!div class="mx-imgBorder"]
       > ![Skärmbild av uppmaningen Välj certifikat](./media/choose-certificates-prompt-disa-purbred-android.png)

    3. Dina härledda autentiseringsuppgifter består av flera certifikat, så du kan se uppmaningen **Välj certifikat** flera gånger. Upprepa föregående steg tills inga fler uppmaningar visas.  

8. När alla certifikat har bearbetats väntar du tills Intune-appen har slutfört konfigurationen av enheten. Du vet att installationen är klar när du ser texten **Nu är du klar!** .  

    > [!div class="mx-imgBorder"]
    > ![Skärmbild av skärmen Nu är du klar!](./media/all-set-android.png)

## <a name="next-steps"></a>Nästa steg

När registreringen är klar har du åtkomst till arbetsresurser, till exempel e-post, Wi-Fi och alla appar som din organisation har gjort tillgängliga. Mer information om hur du hämtar, söker efter, installerar och avinstallerar appar i Intune-appen finns i:

* [Använda hanterade appar på enheten](use-managed-apps-on-your-device-android.md)  
* [Hantera appar från Företagsportal-webbplatsen](manage-apps-cpweb.md)  


Behöver du fortfarande hjälp? Kontakta företagssupporten. Titta efter IT-administratörens kontaktuppgifter på [företagsportalens webbplats](https://go.microsoft.com/fwlink/?linkid=2010980).
