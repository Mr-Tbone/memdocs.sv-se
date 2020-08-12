---
title: Configuration Manager konsol meddelanden
titleSuffix: Configuration Manager
description: Lär dig mer om meddelanden från Configuration Manager-konsolen.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a0d709fa-c4f8-46e1-b432-582cc293be35
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 12ec788fdf19ec72e954f5a9f229a5a3f95a4610
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129686"
---
# <a name="configuration-manager-console-notifications"></a>Configuration Manager konsol meddelanden

*Gäller för: Configuration Manager (aktuell gren)*

<!--3556016, fka 1318035-->
Från och med Configuration Manager version 1902 meddelar Configuration Manager-konsolen om vissa händelser som inträffar. Du kan konfigurera vissa händelse aviseringar för dina Configuration Manager-platser.

- Händelse aviseringar som inte kan konfigureras:
   - När en uppdatering är tillgänglig för Configuration Manager
   - När livs cykel-och underhålls händelser inträffar i miljön
- Konfigurerbara händelse meddelanden:
   - [Hälso ändringar för icke-kritiska platser](#bkmk_noncrit)
   - [Meddelanden från Microsoft](#bkmk_msft) (från och med version 2006)

Det här meddelandet är ett fält överst i konsol fönstret under menyfliksområdet. Den tidigare upplevelsen ersätts när Configuration Manager uppdateringar är tillgängliga. Dessa meddelanden i konsolen visar fortfarande viktig information, men stör inte ditt arbete i-konsolen. Du kan inte ignorera viktiga meddelanden. I-konsolen visas alla meddelanden i ett nytt meddelande fält i namn listen.

![Meddelande fältet och flaggan i-konsolen](./media/1318035-notify-eval-version-expired.png)

## <a name="configure-a-site-to-show-non-critical-notifications"></a><a name="bkmk_noncrit"></a>Konfigurera en plats för att visa meddelanden som inte är kritiska

Du kan konfigurera varje plats så att den visar icke-kritiska meddelanden i egenskaperna för platsen.

1. I arbets ytan **Administration** expanderar du **plats konfiguration**och väljer noden **platser** .
1. Välj den plats som du vill konfigurera för icke-kritiska meddelanden.
1. I menyfliksområdet väljer du **Egenskaper**.
1. På fliken **aviseringar** väljer du alternativet för att **Aktivera konsol meddelanden för icke-kritiska plats hälso ändringar**.
   - Om du aktiverar den här inställningen ser alla konsol användare viktiga, varnings-och informations meddelanden. Den här inställningen är aktiverad som standard.  
   - Om du inaktiverar den här inställningen visas endast viktiga meddelanden i konsol användare.  

De flesta konsol meddelanden är per session. -Konsolen utvärderar frågor när en användare startar den. Starta om-konsolen om du vill se ändringar i meddelandena. Om en användare avstår från ett icke-kritiskt meddelande, meddelas du igen när konsolen startas om, om det fortfarande är tillämpligt.

Följande meddelanden utvärderas var femte minut:

- Platsen är i underhålls läge  
- Platsen är i återställnings läge  
- Platsen är i uppgraderings läge  

Meddelanden följer behörigheterna för rollbaserad administration. Om en användare till exempel inte har behörighet att se Configuration Manager uppdateringar visas inte dessa meddelanden.

Vissa aviseringar har en relaterad åtgärd. Om konsol versionen till exempel inte matchar plats versionen väljer **du installera den nya konsol versionen**. Den här åtgärden startar konsol installations programmet.

Från och med version 2006 visas meddelanden med en åtgärd för att [förnya den hemliga nyckeln](../deploy/configure/azure-services-wizard.md#bkmk_renew)om du konfigurerar Azure-tjänster för moln anslutning till din plats.<!--6386392--> Platsen utvärderar statusen för följande aviseringar en gång per timme:

- En eller flera Azure AD-appens hemliga nycklar upphör snart att gälla
- En eller flera Azure AD-appens hemliga nycklar har upphört att gälla

Följande meddelanden är mest tillämpliga för den Technical Preview-grenen:  

- Utvärderings versionen är inom 30 dagar efter förfallo datum (varning): det aktuella datumet infaller inom 30 dagar från utvärderings versionens förfallo datum  
- Utvärderings versionen har upphört att gälla (kritiskt): det aktuella datumet infaller efter utvärderings versionens förfallo datum  
- Felaktig matchning av konsol version (kritisk): konsol versionen matchar inte plats versionen  
- Plats uppgradering är tillgänglig (varning): det finns ett nytt uppdaterings paket tillgängligt  

Mer information och fel söknings hjälp finns i filen **SmsAdminUI. log** på-konsol datorn. Som standard har logg filen följande sökväg: `C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\AdminUILog\SmsAdminUI.log` .

## <a name="configure-a-site-to-receive-messages-from-microsoft"></a><a name="bkmk_msft"></a>Konfigurera en plats för att ta emot meddelanden från Microsoft
 <!--3953121-->

Från och med version 2006 kan du välja att ta emot meddelanden från Microsoft i Configuration Manager-konsolen. De här aviseringarna hjälper dig att hålla dig informerad om nya eller uppdaterade funktioner, ändringar av Configuration Manager och anslutna tjänster och problem som kräver åtgärder för att åtgärda problemet.

### <a name="configure-notification-settings-for-microsoft-messages"></a>Konfigurera meddelande inställningar för Microsoft-meddelanden

1. Gå till **Administration**  >  **plats konfiguration**  >  **platser**.
1. Högerklicka på en plats och välj **Egenskaper**.
1. På fliken **aviseringar** aktiverar du meddelanden genom att välja **ta emot meddelanden från Microsoft**. Du kan avmarkera något av följande meddelanden om du föredrar att inte ta emot dem:  
   - **Förhindra/åtgärda**: kända problem som påverkar din organisation som kan kräva att du vidtar åtgärder.
   - **Planera för ändring**: ändringar av Configuration Manager som kan kräva att du vidtar åtgärder.
   - **Håll dig informerad**: informerar dig om nya eller uppdaterade funktioner som är tillgängliga.

     [![Meddelande från Microsoft-alternativ i plats egenskaper](./media/3953121-microsoft-notifications.png)](./media/3953121-microsoft-notifications.png#lightbox)



## <a name="next-steps"></a>Nästa steg

- [Använda konsolen](admin-console.md)
- [Konsol tips](admin-console-tips.md)
- [Hjälpmedelsfunktioner](../../understand/accessibility-features.md)
