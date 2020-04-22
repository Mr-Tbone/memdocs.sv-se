---
title: Så här loggar du in i företagsportalappen | Microsoft Docs
description: Lär dig hur du loggar in på företagsportalappen på flera plattformar.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 12/31/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: cfd214bc-f072-4808-af2e-a3cbf7af9bca
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 4088185da2c01cfa7fd343203f7452d2796c4466
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "79335828"
---
# <a name="sign-in-to-company-portal"></a>Logga in på Företagsportal  

Det finns tre sätt att logga in i appen Företagsportal:

* Logga in med din e-postadress för arbetet och ditt lösenord.  
* Logga in med certifikatbaserad autentisering.  
* Logga in från en annan enhet.    


## <a name="sign-in-with-your-email-address-and-password"></a>Logga in med din e-postadress och ditt lösenord
Följande steg visar skärmbilder från Företagsportal för iOS.  

1. Öppna appen på enheten och tryck på **Logga in**.  

   ![Exempel på skärmbild av inloggningssidan för Företagsportal.](./media/intune-ios-cp-signin-1908.png)


2. Ange ditt **Arbets- eller skolkonto** och tryck på **Nästa**.

   ![Användaren ombeds endast att ange sin e-postadress, i stället för sin e-post och lösenord på samma skärm.](./media/cp_ios_aad_signin_after_1804_002.png)

3. Ange ditt lösenord och tryck på **Logga in**.

   ![Användaren uppmanas att ange lösenordet när e-postadressen har accepterats.](./media/cp_ios_aad_signin_after_1804_003.png)

4. Appen verifierar dina autentiseringsuppgifter. När du är klar har du tillgång till organisationens resurser och kan installera tillgängliga appar.  

   ![När autentiseringsprocessen är klar loggar företagsportalsappen in och en förloppsindikator visas.](./media/cp_ios_aad_signin_after_1804_004.png)

## <a name="sign-in-with-certificate-based-authentication"></a>Logga in med certifikatbaserad autentisering
Det här inloggningsalternativet visas bara om din organisation tillåter certifikatbaserad autentisering och du har ett certifikat som är tillgängligt för användning.  

1. Öppna företagsportalappen på din enhet.  

2. Ange ditt **arbets- eller skolkonto**.  

3. Tryck på länken **Logga in med ett certifikat**.  

4. Tryck på **Fortsätt** för att använda certifikatet.  

## <a name="sign-in-from-another-device"></a>Logga in från en annan enhet

Om företaget använder smartkort för att få åtkomst till datorerna behöver du troligen logga in med en annan enhet.  

1. Öppna företagsportalappen på din enhet. Se till att det är den enhet som du kommer att använda för att få åtkomst till dina arbetsresurser.       

1. Välj **Logga in från en annan enhet**.  

   ![På företagsportalens inloggningssida uppmanas användaren att ange en e-postadress.  Visar knappen ”Nästa” och en länk till ”Logga in från en annan enhet”. Det finns också en länk till ”Kan du inte öppna ditt konto?” En länk längst ner leder till Microsofts information om sekretess och cookies.](./media/cp_ios_aad_signin_after_1804_005.png)

2. Du får en unik engångskod som du kan använda för att logga in på företagsportalen. Kopiera koden.

   ![Instruktioner för att gå till sidan https://microsoft.com/devicelogin visas, med ett unikt lösenord från din arbetsdator. Därefter använder du koden för att logga in.](./media/cp_ios_aad_signin_after_1804_006.png)

3. Öppna webbläsaren på din andra enhet (den som du använder för att autentisera) och gå till [https://microsoft.com/devicelogin](https://microsoft.com/devicelogin). Ange eller klistra in koden.  

   ![En bild av användarens webbläsare på arbetsdatorn, i stället för företagsportalappen. Sidan ”Inloggning på enhet” visas och uppmanar användarna ange koden de fick i företagsportalsappen.](../fundamentals/media/whats-new-app-ui/cp_ios_aad_signin_from_another_device_after_1704_004.png)

4. Välj __Fortsätt__ för att tillåta Företagsportal att logga in på din arbetsenhet.   

   ![Användaren har matat in sin unika kod i fältet och webbplatsen ”Inloggning på enhet” har begärt en bekräftelse på att Intunes företagsportal är rätt app för att få behörighet att logga in.](../fundamentals/media/whats-new-app-ui/cp_ios_aad_signin_from_another_device_after_1704_005.png) 

5. Du kan stänga fönstret när koden har verifierats.  

   ![En bekräftelsesida som anger att användaren har loggat in i företagsportalsappen på sin enhet visas nu, och den här sidan kan stängas.](../fundamentals/media/whats-new-app-ui/cp_ios_aad_signin_from_another_device_after_1704_006.png)

6. Företagsportal-appen loggar in dig på din arbetsenhet.  

   ![Efter att ha genomgått autentiseringsprocessen loggas företagsportalappen in, vilket visas med en förloppsindikator.](./media/cp_ios_aad_signin_after_1804_007.png)

Behöver du fortfarande hjälp? Kontakta företagssupporten. Titta efter IT-administratörens kontaktuppgifter på [företagsportalens webbplats](https://go.microsoft.com/fwlink/?linkid=2010980).  
