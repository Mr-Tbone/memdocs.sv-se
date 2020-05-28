---
title: Vilken gren ska jag använda
titleSuffix: Configuration Manager
description: Lär dig skillnaderna mellan tillgängliga grenar av Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a3be4f8f-3d44-4e3c-9fa1-e85f30a36e72
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 542069b82ea4c68a48ccc47b79007fd2fa25322a
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906016"
---
# <a name="which-branch-of-configuration-manager-should-i-use"></a>Vilken gren av Configuration Manager bör jag använda?

*Gäller för: Configuration Manager (aktuell gren & Technical Preview-gren) & System Center Configuration Manager (långsiktig service gren)*

Det finns tre grenar av tillgängliga Configuration Manager:

- Aktuell gren
- Långsiktig underhållsgren (LTSB)
- Technical Preview-gren

Använd den här artikeln för att hjälpa dig att välja rätt gren.

> [!TIP]  
> Alla platser i en hierarki måste köra samma gren. Det finns inte stöd för att ha en hierarki med olika grenar på olika platser.

## <a name="current-branch"></a>Aktuell gren

Den här grenen är licensierad för användning i en produktions miljö. Använd den här grenen för att få de senaste funktionerna. Om du har någon av följande licenser kan du använda den här grenen:  

- System Center Data Center
- System Center standard
- System Center Configuration Manager
- Motsvarande prenumerations rättigheter  

Mer information om Software Assurance och licensierings alternativ finns i [licensiering och filialer för Configuration Manager](learn-more-editions.md) och [vanliga frågor och svar om Configuration Manager grenar och licensiering](product-and-licensing-faq.md).

Microsoft planerar att lansera uppdateringar för Configuration Manager aktuella grenen några gånger per år. Varje uppdaterings version är fortfarande i stöd i 18 månader från dess allmänna utgivnings datum (GA). Teknisk support tillhandahålls för hela support perioden. Vår support struktur är dock dynamisk och utvecklas i två olika service faser som är beroende av tillgängligheten för den senaste aktuella gren versionen. (Mer information finns i [stöd för Configuration Manager aktuella gren versioner](../servers/manage/current-branch-versions-supported.md). Uppdateringar av nyare versioner är tillgängliga som uppdateringar i konsolen.

Om du vill installera den aktuella grenen som en ny plats använder du [bas linje medier](../servers/manage/updates.md#bkmk_Baselines). Använd också bas linje medier för att uppgradera från System Center 2012 Configuration Manager med Service Pack 2 eller System Center 2012 R2 Configuration Manager med Service Pack 1. Åtkomst till det här mediet beror på hur din organisations licenser Configuration Manager.

Du kan också använda bas linje mediet för att installera en ny plats som är en utvärderings version av den aktuella grenen. Utvärderings versionen kräver ingen licens. Du kan använda utvärderings versionen i 180 dagar. Den stöder uppgradering till en licensierad version av den aktuella grenen. Om du bara vill installera en utvärderings version hämtar du den från [utvärderings centret](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection).

> [!NOTE]
> Använd bas linje medium för att installera platser för en ny Configuration Manager hierarki. Om du tidigare har installerat en bas linje version använder du uppdateringar i konsolen för att uppdatera dina platser till en ny version.  
>
> Webbplatser som uppdateras med uppdateringar i konsolen resulterar i platser som är samma som den nya plats som installeras med hjälp av bas linje mediet.
>
> Mer information finns i [uppdateringar för Configuration Manager](../servers/manage/updates.md).  

### <a name="features-of-the-current-branch"></a>Funktioner i aktuell gren

- Tar emot [uppdateringar i konsolen](../servers/manage/install-in-console-updates.md) som gör nya funktioner tillgängliga för användning.
- Tar emot uppdateringar i konsolen som levererar säkerhets-och kvalitets korrigeringar till befintliga funktioner.
- Stöder out-of-band-uppdateringar vid behov. Mer information finns i [använda verktyget uppdatera registrering](../servers/manage/use-the-update-registration-tool-to-import-hotfixes.md) eller [Använd installations programmet för snabb korrigeringar](../servers/manage/use-the-hotfix-installer-to-install-updates.md).
- Integreras med molnbaserade tjänster.
- Stöder [migrering av data](../migration/migrate-data-between-hierarchies.md) till och från andra Configuration Manager-installationer.
- Stöder uppgradering från tidigare versioner av Configuration Manager.
- Stöder installation som en utvärderings version, från vilken du senare kan uppgradera till en fullt licensierad installation.

Microsoft rekommenderar att du uppdaterar till den senaste versionen strax efter dess version. Du kan vänta upp till 18 månader innan du uppdaterar till en nyare version. Du kan även hoppa över en uppdatering för att installera den senaste versionen som är tillgänglig. Eftersom varje version är kumulativ, om du hoppar över en uppdatering och installerar den senaste versionen, får du fortfarande åtkomst till alla funktioner och förbättringar från tidigare versioner.

Mer information finns i [stöd för aktuella gren versioner](../servers/manage/current-branch-versions-supported.md).

### <a name="current-branch-update-options"></a>Aktuella uppdaterings alternativ för gren

- Med aktiv Software Assurance kan du installera uppdateringar i konsolen för aktuella gren versioner.  
- Det finns inget alternativ för att konvertera den aktuella grenen till en Technical Preview-gren. Tekniska för hands grenar är separata installationer som inte kräver en licens.
- Det finns inget alternativ för att konvertera din aktuella gren till LTSB (Long term Servicing Branch). Du måste avinstallera den aktuella grenen och sedan installera LTSB som en ny installation.

## <a name="long-term-servicing-branch"></a>Långsiktig underhållsgren (LTSB)

Den här grenen är licensierad för användning i produktion för Configuration Manager kunder som använder den aktuella grenen och har tillåtit sina Configuration Manager Software Assurance (SA) eller motsvarande prenumerations rättigheter att upphöra att gälla efter den 1 oktober 2016. Mer information om Software Assurance och licensierings alternativ finns i [licensiering och filialer för Configuration Manager](learn-more-editions.md) och [vanliga frågor och svar om Configuration Manager grenar och licensiering](product-and-licensing-faq.md).

LTSB baseras på version 1606. Den här grenen tar inte emot uppdateringar i konsolen som tillhandahåller nya funktioner eller uppdaterar befintliga funktioner. Viktiga säkerhets korrigeringar tillhandahålls dock. Om du vill installera LTSB måste du använda det version 1606- [bas linje medium](../servers/manage/updates.md#bkmk_Baselines) som du får med System Center 2016. Senare bas linje versioner stöder inte installation av LTSB.

Om du vill installera LTSB som en ny plats eller som en uppgradering från en System Center 2012 Configuration Manager-plats som stöds, använder du det 1606 versions-och [bas linje medium](../servers/manage/updates.md#bkmk_Baselines) som du får med system Center 2016. Du kan använda bas linje medier för att installera en ny plats som kör version 1606 av den aktuella grenen, eller en ny plats som kör den långsiktiga service grenen.

> [!TIP]  
> Läs mer om System Center 2016 i [dokumentationen för system center 2016](https://docs.microsoft.com/system-center/index). Den här dokumentationen identifierar också hur du hämtar System Center 2016, som kräver ett licens avtal för Microsoft eller liknande rättigheter.  
>  
> Om du vill hitta Configuration Manager version 1606 i Volume Licensing Service Center (VLSC) går du till fliken **nedladdningar och nycklar** i [VLSC](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx), söker efter `System Center 2016` och väljer sedan antingen **System Center 2016 Data Center** eller **System Center 2016 standard**.  
>  
> Du kan också få en utvärderings version av System Center 2016 från [utvärderings centret](https://www.microsoft.com/evalcenter/evaluate-system-center-technical-preview).  

### <a name="features-of-the-ltsb"></a>Funktioner i LTSB

- Tar emot uppdateringar i konsolen som levererar viktiga säkerhets korrigeringar.
- Tillhandahåller ett installations alternativ när ditt SA-avtal eller motsvarande rättigheter för Configuration Manager har upphört att gälla.
- Stöder uppgradering (konvertering) till den aktuella grenen när du har ett aktuellt SA-avtal eller motsvarande rättigheter att Configuration Manager.

### <a name="ltsb-limitations"></a>LTSB-begränsningar

LTSB baseras på den aktuella gren versionen 1606 och har följande begränsningar:

- LTSB stöds för 10 års kritiska säkerhets uppdateringar efter dess allmänna tillgänglighet (oktober 2016), efter vilken support för den här grenen upphör att gälla. Mer information om support livs cykeln finns i [Microsofts livs cykel princip](https://support.microsoft.com/lifecycle).
- Har stöd för en begränsad uppsättnings lista med Server-och klient operativ system och relaterade tekniker, till exempel SQL Server-versioner. Mer information finns i [konfigurationer som stöds för långsiktig service gren](supported-configurations-for-ltsb.md).
- Tar inte emot uppdateringar för nya funktioner
- Har inte stöd för följande funktioner:
  - Molnbaserade funktioner som samtidig hantering eller Skriv bords analys
  - Lokal MDM
  - Service instrument panelen för Windows 10, Service planer eller Windows 10-halvårs kanal
  - Framtida versioner av Windows 10 LTSB och Windows Server
  - Till gångs information
  - Alla för hands funktioner

### <a name="ltsb-update-options"></a>LTSB uppdaterings alternativ

- Du kan konvertera din LTSB-installation till en aktuell Branch-installation. Det finns stöd för omvandling till den aktuella grenen före eller efter stöd för LTSB förfaller.

  För att konvertera måste du ha ett aktivt Software Assurance-avtal med Microsoft. Mer information finns i följande artiklar:

  - [Uppgradera den långsiktiga service grenen till den aktuella grenen](convert-to-current-branch.md)
  - [Licensiering och filialer för Configuration Manager](learn-more-editions.md)
  - [Bas linje-och uppdaterings versioner](../servers/manage/updates.md#bkmk_Baselines)

- Det finns inget alternativ för att konvertera LTSB till en Technical Preview-gren. Tekniska för hands grenar är separata installationer som inte kräver en licens.

- Du kan inte uppgradera en utvärderings version av den aktuella grenen till en LTSB-installation.

## <a name="technical-preview-branch"></a>Technical Preview-gren

Den tekniska förhands gransknings grenen används i en labb miljö. Lär dig mer om och prova de senaste funktionerna som utvecklas för Configuration Manager. Det stöds inte i en produktions miljö och kräver inte att du har ett licens avtal för Software Assurance.

Om du vill installera en ny plats som kör den tekniska för hands versionen använder du det senaste [bas linje mediet för den tekniska för hands versionen](../get-started/technical-preview.md#bkmk_install). När du har installerat den tekniska förhands gransknings grenen är nya versioner tillgängliga som uppdateringar i konsolen varje månad.

### <a name="features-of-the-technical-preview-branch"></a>Funktioner i den tekniska förhands gransknings grenen

- Baserat på de senaste bas linje versionerna av den aktuella grenen
- Tar emot uppdateringar i konsolen som uppdaterar installationen till den senaste tekniska för hands versions grenen
- Innehåller nya funktioner som utvecklas och för vilka Microsoft vill ha din feedback
- Tar emot uppdateringar som endast gäller för den Technical Preview-grenen

### <a name="technical-preview-limitations"></a>Tekniska för hands versions begränsningar

- [Stödet är begränsat](../get-started/technical-preview.md#bkmk_reqs), inklusive endast en primär plats och upp till 10 klienter.  
- Du kan inte uppgradera eller migrera den till en aktuell gren eller LTSB-installation.
- Har inte stöd för följande beteenden:
  - Använd migrering för att importera eller exportera data till en annan Configuration Manager-installation
  - Uppgradera från en tidigare version av Configuration Manager
  - Installera som utvärderings version

Funktioner som först introduceras i en Technical Preview-gren läggs ofta till i den aktuella grenen i en senare uppdatering. Varje ny teknisk för hands versions gren innehåller funktioner från tidigare tekniska för hands grenar, även efter att dessa funktioner har lagts till i den aktuella grenen.

Mer information finns i [teknisk för hands version för Configuration Manager](../get-started/technical-preview.md).

### <a name="technical-preview-update-options"></a>Uppdaterings alternativ för teknisk för hands version

- Du kan installera eventuella uppdateringar i konsolen för en ny version av Technical Preview-grenen.

- Det finns inget alternativ för att konvertera en Technical Preview-gren till den aktuella grenen eller LTSB.

## <a name="identify-your-version-and-branch"></a>Identifiera din version och gren

### <a name="version"></a>Version

Om du vill kontrol lera versionen av din webbplats går du till **om Configuration Manager** i det övre vänstra hörnet i-konsolen. I den här dialog rutan visas **plats versionen**. En lista över plats versioner finns i [bas linje-och uppdaterings versioner](../servers/manage/updates.md#bkmk_Baselines).

### <a name="branch"></a>Gren

Om du vill bekräfta grenen för platsen går du till **Administration**  >  **plats konfiguration**  >  **platser**och öppnar **Inställningar för hierarkin**i-konsolen. Om det finns ett aktivt alternativ för att konvertera till den aktuella grenen kör platsen LTSB-versionen. När platsen kör den aktuella grenen inaktiverar konsolen det här alternativet.

Mer information om olika versioner av Configuration Manager finns i [bas linje-och uppdaterings versioner](../servers/manage/updates.md#bkmk_Baselines).
