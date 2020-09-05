---
title: Registrera en Android-enhet med Intune-företagsportalen | Microsoft Docs
description: Beskriver hur du registrerar en Android-enhet med Intune-företagsportalen
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/27/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 0ed3a002-7533-4001-ae24-e10b64b66620
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: ef1b6c82cae82763dc327f16e35d0e3bc522c3c7
ms.sourcegitcommit: 41e6e6b7f5c2a87aaf7f23d90d0f175dd63c0579
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/28/2020
ms.locfileid: "89057478"
---
# <a name="enroll-your-device-with-company-portal"></a>Registrera din enhet med företagsportalen  
Registrera din personliga eller företagsägda Android-enhet för att få säker åtkomst till företagets e-post, appar och data. Företagsportalen har stöd för Android-enheter, däribland Samsung Knox, som kör Android 4.4 och senare.  
</br>
> [!VIDEO https://www.youtube.com/embed/k0Q_sGLSx6o?rel=0]

> [!NOTE]
> Samsung Knox är en typ av säkerhet som vissa Samsung-enheter använder för ytterligare skydd utöver vad den interna säkerheten i Android ger. Du kan kontrollera om du har en Samsung Knox-enhet genom att gå till **Inställningar** > **Om enheten**. Om du inte ser **Knox version** där har du en ursprunglig Android-enhet.  

## <a name="install-company-portal-app"></a>Installera företagsportalappen  
Installera Intune-företagsportalsappen [från Google Play](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal). Se [Installera företagsportalsappen i Folkrepubliken Kina](install-company-portal-android-china.md) för en lista över butiker som erbjuder appen i Folkrepubliken Kina.

1. Tryck på **Start** > **Play Store**.

2. Sök efter **Intune-företagsportal**. Tryck sedan på appen för att öppna den. 

    ![android-search-company-portal](./media/and-cpinstall-1-search-cp.png)

4. Tryck på **INSTALLERA**.

5. När du tillfrågas om appbehörigheter trycker du på **GODKÄNN**.  

    ![android-accept-company-portal-terms](./media/and-cpinstall-3-cp-accept.png)

## <a name="enroll-device"></a>Registrera enhet  
Under registreringen kan du bli ombedd att välja en kategori som bäst beskriver hur du använder enheten. Företagets support använder ditt svar för att se vilka appar du har åtkomst till.  

1. Öppna företagsportalappen och logga in med ditt arbets- eller skolkonto.  

2. Om du uppmanas att godkänna din organisations villkor trycker du på **GODKÄNN ALLT**.  

   ![Exempelbild på Företagsportal, skärmen Villkor, med knappen "Godkänn alla" markerad.](./media/accept-terms-1911.png)  


3. Granska vad din organisation kan och inte kan se. Tryck sedan på **FORTSÄTT**.


    ![Exempelbild av Företagsportalen, vi värnar om din integritet-skärm som visar knappen Fortsätt.](./media/android-privacy-screen-1911.png)  
4. Gå igenom vad du kan förvänta dig i de kommande stegen. Tryck sedan på **NÄSTA**.  

    ![Exempelbild på Företagsportal, skärmen Vad händer nu, med knappen "Nästa" markerad.](./media/android-whats-next-1911.png)  


5. Beroende på din Android-version kan du bli uppmanad att tillåta åtkomst till vissa delar av enheten. Dessa meddelanden krävs av Google och styrs inte av Microsoft.  

    Tryck på **Tillåt** för följande behörigheter:  
    * **Tillåt att företagsportalen kan ringa och hantera telefonsamtal**: Den här behörigheten gör att din enhet kan dela sitt IMEI-nummer (International Mobile Station Equipment Identity) med Intune, din organisations enhetshanteringsprovider. Det är säkert att tillåta den här behörigheten. Microsoft varken ringer eller hanterar telefonsamtal.  
    * **Tillåt att företagsportalappen får åtkomst till dina kontakter**: Den här behörigheten gör att företagsportalappen kan skapa, använda och hantera ditt arbetskonto.  Det är säkert att tillåta den här behörigheten. Microsoft bereder sig aldrig åtkomst till dina kontakter. 

    Om du nekar behörighet får du frågan igen nästa gång du loggar in på Företagsportal. Om du vill stänga av de här meddelandena väljer du **Fråga inte igen**. Du hanterar appbehörigheter genom att gå till Inställningar-appen > **Appar** > **Företagsportal** > **Behörigheter** > **Telefon**.  

6. Aktivera enhetens administratörsapp. 

    Företagsportal behöver enhetens administratörsbehörigheter för att på ett säkert sätt hantera din enhet. När du aktiverar appen kan din organisation identifiera potentiella säkerhetsproblem, till exempel upprepade misslyckade försök att låsa upp din enhet, och vidta åtgärder.  

    ![Exempelbild på skärmen Aktivera enhetsadministratör, med knappen "Aktivera" markerad.](./media/activate-device-administrator-1911.png)  

> [!NOTE]
> Microsoft kontrollerar inte meddelanden på den här skärmen. Vi förstår att formuleringen på den kan verka dramatisk. Företagsportal kan inte ange vilka begränsningar och vilken åtkomst som är relevant för din organisation. Om du har frågor om hur din organisation använder appen bör du kontakta IT-personalen. Gå till [Företagsportal-webbplatsen](https://go.microsoft.com/fwlink/?linkid=2010980) och leta upp din organisations kontaktuppgifter.  


7. Din enhet börjar registreras. Om du använder en Samsung Knox-enhet uppmanas du att läsa och godkänna sekretesspolicyn för ELM-agenten först.   

    ![Exempelbild på Samsung Knox-skärmen för sekretesspolicy, som visas under registreringen.](./media/and-enroll-7-knox-privacy-policy.png)  

8. På skärmen **Konfiguration av företagsåtkomst** kontrollerar du att enheten har registrerats. Tryck sedan på **FORTSÄTT**.  

    ![Exempelbild av Företagsportal, skärmen Konfiguration av företagsåtkomst, där Få din enhet hanterad visas som slutfört.](./media/update-settings-1911.png)  

9. Din organisation kan kräva att du uppdaterar enhetsinställningarna. Tryck på **LÖS** för att justera en inställning. När du är klar med att uppdatera inställningarna trycker du på **FORTSÄTT**.  

   ![Exempelbild på skärmen Företagsportal, Uppdatera enhetsinställningar, där knapparna Lös och Fortsätt markerade.](./media/resolve-settings-1911.png)  

10. När installationen är klar trycker du på **KLAR**.    

    ![Exempelbild av Företagsportal, Konfiguration av företagsåtkomst-skärmen som visar slutförd installation och Klar-knappen.](./media/android-enrollment-done-1911.png) 

## <a name="next-steps"></a>Nästa steg  

Innan du försöker installera en skol- eller arbetsapp går du till **Inställningar** > **Säkerhet** och aktiverar **Okända källor**. Om du inte aktiverar det här alternativet visas följande meddelande när du försöker att installera en app: ”Installationen blockerades. Av säkerhetsskäl är enheten inställd på att blockera installationer av appar från okända källor. Du kan trycka på **Inställningar** i meddelandet för att gå direkt till **Okända källor**.  

> [!Note]
> Om din organisation använder kostnad hanteringsprogramvara för telekomtjänster måste ytterligare ett part steg utföras innan enheten har registrerats fullständigt. Läs mer [här](enroll-your-device-with-telecom-expense-management-android.md).

Om du får ett felmeddelande när du försöker registrera enheten i Intune kan du [skicka ett e-postmeddelande till företagets support](send-logs-to-your-it-admin-by-email-android.md).  

Behöver du fortfarande hjälp? Kontakta företagssupporten. Titta efter IT-administratörens kontaktuppgifter på [företagsportalens webbplats](https://go.microsoft.com/fwlink/?linkid=2010980).  