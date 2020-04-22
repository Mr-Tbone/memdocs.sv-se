---
title: Hämta en återställningsnyckel för en macOS-enhet från webbplatsen för Intune-företagsportalen
description: Visa återställningsnyckeln för en registrerad, hanterad macOS-enhet.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 12/04/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: ''
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 5a15f3a05f96333eba19cf69c5778e6c8bd04f59
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "79336764"
---
# <a name="get-a-recovery-key-for-a-macos-device"></a>Hämta en återställningsnyckel för en macOS-enhet

Använd webbplatsen för företagsportalen till att hämta en återställningsnyckel för din låsta macOS-enhet. Om du glömmer enhetslösenordet kan du logga in på Företagsportal från en annan enhet och hämta nyckeln.  

## <a name="get-recovery-key-from-company-portal-website"></a>Hämta återställningsnyckel från webbplatsen för företagsportalen

Det här alternativet är tillgängligt för enheter som krypterades av din organisation med hjälp av FileVault. Det är inte tillgängligt för enheter som du har krypterat personligen.

1. På valfri enhet loggar du in på [webbplatsen för företagsportalen](https://portal.manage.microsoft.com) och väljer knappen **Meny** > **Enheter**.  
2. Välj den krypterade macOS-enheten.  
3. Välj **Hämta återställningsnyckel**.  

    ![Skärmbild av webbplatsen för företagsportalen, med avsnittet Hämta återställningsnyckel markerat.](./media/1907-recovery2-cpweb-intune.PNG)  

4. Din återställningsnyckel kommer att visas.

    ![Skärmbild av webbplatsen för företagsportalen, där återställningsnyckeln visas.](./media/1907-recovery-cpweb-intune.PNG)  

    Av säkerhetsskäl försvinner nyckeln efter fem minuter. Om du vill se nyckeln igen väljer du **Hämta återställningsnyckel**.

Om en nyckel inte hittas men enheten är korrekt krypterad kontaktar du din organisations tekniska support. Titta efter IT-administratörens kontaktuppgifter på [företagsportalens webbplats](https://go.microsoft.com/fwlink/?linkid=2010980).  

## <a name="get-recovery-key-from-company-portal-app-for-ios"></a>Hämta återställningsnyckel från företagsportalappen för iOS

Du kan hämta din personliga återställningsnyckel (FileVault-key) med hjälp av företagsportalappen för iOS. Din enhet som har den personliga återställningsnyckeln måste registreras med Intune och krypteras med FileVault via Intune. Det här alternativet är inte tillgängligt för enheter som du har krypterat personligen. 

Med hjälp av företagsportalappen kan du öppna Safari-webbvyn och hämta din personliga återställningsnyckel. 

1. Öppna appen Företagsportal.
2. Klicka på **Hämta återställningsnyckel**.

    ![Skärmbild av företagsportalappen för iOS, där återställningsnyckeln visas](./media/get-recovery-key-cpweb-02.png)  

Webbplatsen för företagsportalen öppnas i Safari-webbvyn och visar nyckeln. 

## <a name="it-pro-support"></a>IT-supportpersonal

Om du är IT-supporttekniker och vill konfigurera och hantera FileVault-kryptering för macOS-enheter läser du [Använda enhetskryptering med Intune](/intune/protect/encrypt-devices).

## <a name="next-steps"></a>Nästa steg

Få reda på vad du mer kan göra på webbplatsen för företagsportalen. Listan över åtgärder finns i [Använda Intune-företagsportalens webbplats](using-the-intune-company-portal-website.md).  

Behöver du fortfarande hjälp? Kontakta IT-supporten. Titta efter IT-administratörens kontaktuppgifter på [företagsportalens webbplats](https://go.microsoft.com/fwlink/?linkid=2010980).  
