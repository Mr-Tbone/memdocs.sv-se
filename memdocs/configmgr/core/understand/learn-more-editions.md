---
title: Licensiering och förgreningar
titleSuffix: Configuration Manager
description: Läs om licens kraven för de installations alternativ som är tillgängliga med Configuration Manager
ms.date: 06/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 495b87ae-41a4-49ba-abe2-d4f7d22ac0d4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 04ed335c65369840085fe44ba2f1b81d7806a0e3
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906052"
---
# <a name="licensing-and-branches-for-configuration-manager"></a>Licensiering och filialer för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren) & System Center Configuration Manager (långsiktig service gren)*

Använd den här artikeln om du vill veta mer om licens kraven för de installations alternativ som är tillgängliga med Configuration Manager. De här installations alternativen omfattar följande grenar:

- Aktuell gren
- Långsiktig service gren (LTSB)
- Utvärderings installation av den aktuella grenen
- Technical Preview-gren

## <a name="licensing-overview"></a>Licensöversikt

Kunder med aktiv Software Assurance (SA) på Configuration Manager licenser eller med motsvarande prenumerations rättigheter från och med den 1 oktober 2016 har rätt att använda version 1606 från oktober 2016 för Configuration Manager. Kunder med rättigheter att Configuration Manager den 1 oktober 2016 hittar två licensierade alternativ vid installation: aktuell gren och långsiktig service gren (LTSB).

De fullständiga villkoren för de produkter som du köper via Microsofts volym licensierings program finns i [licens villkoren och dokumentationen](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?mode=1).


## <a name="licensed-branches"></a>Licensierade grenar

Den här artikeln hänvisar till Software Assurance-avtalet eller motsvarande prenumerations rättigheter. Detta Microsoft licens avtal ger rättigheter att installera och använda Configuration Manager.

### <a name="current-branch"></a>Aktuell gren

Den aktuella grenen kräver ett aktivt Software Assurance-avtal eller motsvarande rättigheter att Configuration Manager. Mer information finns i [Software Assurance och Current Branch](#software-assurance-and-the-current-branch).

Den här grenen stöds för användning i produktions miljöer som vill få regelbundna kvalitets-och funktions uppdateringar från Microsoft. Den ger åtkomst till att använda alla funktioner och förbättringar.

Från och med 1710-versionen är varje uppdaterings version fortfarande i stöd i 18 månader från dess allmänna utgivnings datum. Mer information finns i [stöd för Configuration Manager aktuella gren versioner](../servers/manage/current-branch-versions-supported.md).

### <a name="long-term-servicing-branch-ltsb"></a>Långsiktig service gren (LTSB)

LTSB kräver ett aktuellt Software Assurance-avtal med Microsoft från och med den 1 oktober 2016. Mer information finns i [Software Assurance och LTSB](#software-assurance-and-the-ltsb).

Den här grenen stöds för användning i produktions miljöer. Den är avsedd att användas av kunder som har till gång till sina Software Assurance (SA) eller motsvarande prenumerations rättigheter att Configuration Manager upphör att gälla efter den 1 oktober 2016. Den här grenen är begränsad jämfört med Current Branch.

Kritiska säkerhets uppdateringar för Configuration Manager görs tillgängliga för den här grenen men inga nya funktioner blir tillgängliga.

### <a name="evaluation-installation-of-the-current-branch"></a>Utvärderings installation av den aktuella grenen

Utvärderings versionen kräver inte ett Software Assurance-avtal med Microsoft. [Utvärderings installationer](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection) är alltid den aktuella grenen och du kan använda dem i 180 dagar.

Du kan uppgradera utvärderings installationen till en fullständig installation av den aktuella grenen. Du kan inte uppgradera en utvärderings installation till den långsiktiga service grenen.

### <a name="technical-preview-branch"></a>Technical Preview-gren

Den [tekniska förhands gransknings grenen](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview) är också tillgänglig. Den här grenen är en begränsad version av Configuration Manager som gör att du kan testa nya funktioner. Du installerar den tekniska för hands versionen med ett annat medium än licensierade versioner. Mer information finns i [teknisk för hands version](../get-started/technical-preview.md).


## <a name="software-assurance-agreements"></a>Software Assurance-avtal

Status för Software Assurance på Configuration Manager licenser, eller motsvarande prenumerations rättigheter, den 1 oktober 2016, bestämmer grenen du kan installera och använda.

### <a name="software-assurance-and-the-current-branch"></a>Software Assurance och den aktuella grenen

Rättigheter att använda Configuration Manager aktuella grenen kan tillhandahållas av:

- **System Center:** Kunder med aktiva SA i System Center standard-eller data Center-licenser kan installera och använda den aktuella gren inställningen för Configuration Manager.

- **System Center Configuration Manager:** Kunder med aktiva SA på Configuration Manager licenser, eller med motsvarande prenumerations rättigheter, kan installera och använda den aktuella gren inställningen för Configuration Manager.

Om du har aktiva SA på Configuration Manager licenser eller motsvarande prenumerations rättigheter den 1 oktober 2016:

- Du kan installera och använda den aktuella grenen.
- Om du tillåter att SA eller prenumerationen upphör måste du avinstallera den aktuella grenen.

### <a name="software-assurance-and-the-ltsb"></a>Software Assurance och LTSB

Om du har en aktiv SA på Configuration Manager licenser eller motsvarande prenumerations rättigheter den 1 oktober 2016:

- Du kan installera och använda LTSB. Kunder som har permanent behörighet att Configuration Manager eller som tillåter deras SA eller prenumeration att upphöra att använda, kan installera den version av Configuration Manager LTSB som är aktuell vid tidpunkten för förfallet.

LTSB baseras på den aktuella gren versionen 1606 och har följande begränsningar:

- Det finns inget stöd för att konvertera en aktuell gren till LTSB. Om du för närvarande har en aktuell gren plats måste du installera LTSB som en ny plats.  

- LTSB stöder inte alla funktioner i den aktuella grenen. Mer information finns i [Introduktion till långsiktig service gren](introduction-to-the-ltsb.md). Dessa begränsningar omfattar en begränsad funktions uppsättning, begränsade uppgraderings alternativ och en separat produkt support livs cykel.  

### <a name="software-assurance-expiration-date"></a>Utgångs datum för Software Assurance

Från och med versionen från oktober 2016 av version 1606 bas linje medium för Configuration Manager kan du ange förfallo datumet för Software Assurance-avtalet. **Utgångs datumet för Software Assurance** är ett valfritt värde som en bekväm påminnelse. Lägg till den när du kör Configuration Manager installationen eller senare i Configuration Manager-konsolen.

> [!NOTE]
> Microsoft validerar inte det förfallo datum som du anger och använder inte det här datumet för licens validering. Använd den som en påminnelse om ditt förfallo datum. Det här värdet är användbart när Configuration Manager regelbundet söker efter nya program uppdateringar som erbjuds online. Licens statusen för Software Assurance bör vara aktuell för att vara kvalificerad att använda dessa ytterligare uppdateringar.

#### <a name="to-specify-the-software-assurance-expiration-date"></a>Ange utgångs datum för Software Assurance

- När du kör installations programmet från Configuration Manager Media anger du värdet på sidan **produkt nyckel** i installations guiden.

- I Configuration Manager-konsolen i **Inställningar för hierarki**anger du värdet på fliken **licensiering** .


## <a name="licensing-resources"></a>Licensierings resurser

Om du vill veta mer om produkt licens information använder du följande resurser.

### <a name="microsoft-volume-licensing-service-center-vlsc"></a>Microsoft Volume Licensing Service Center (VLSC)

- [Översikt över VLSC](https://www.microsoft.com/Licensing/existing-customer/vlsc-training-and-resources.aspx)

- [Produkt villkor för Microsoft Volume Licensing](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?mode=1)

- Volym licens kunder kan få en översikt över sina licenser från [volym licens Service Center](https://www.microsoft.com/Licensing/servicecenter/default.aspx). Gå till menyn **licenser** och välj **licens översikt**.

### <a name="vlsc-videos"></a>VLSC-videor

- Om du vill lära dig mer om hur VLSC fungerar går du till [Microsoft Volume Licensing Service Center utbildning och resurser](https://www.microsoft.com/licensing/existing-customer/vlsc-training-and-resources) och väljer **instruktions video**.

- [Var du kan leta upp ditt aktiva Software Assurance-avtal](https://www.microsoft.com/showcase/video.aspx?uuid=fe1846cb-1d26-49fc-b064-57b25dcc31a0) (från 43 sekunder)  

- [Så här hämtar du behörigheter för VLSC](https://www.microsoft.com/showcase/video.aspx?uuid=ac4ed1ca-d0a9-43cd-89fa-74ccb555dec4). Du kan delegera VLSC Läs-och Skriv behörighet till andra personer i din organisation.
