---
title: Funktioner i Technical Preview 1611
titleSuffix: Configuration Manager
description: Lär dig mer om funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1611.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d2ad00e8-9f10-41b6-816a-d8542c23a22e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: e1e1348e9d230a5525a91e7e7dceea4da6d1311b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721551"
---
# <a name="capabilities-in-technical-preview-1611-for-configuration-manager"></a>Funktioner i Technical Preview 1611 för Configuration Manager

*Gäller för: Configuration Manager (Technical Preview Branch)*



Den här artikeln beskriver de funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1611. Du kan installera den här versionen för att uppdatera och lägga till nya funktioner till din Configuration Manager Technical Preview-webbplats. Innan du installerar den här versionen av Technical Preview kan du läsa introduktions avsnittet, [teknisk för hands version för Configuration Manager](../../core/get-started/technical-preview.md), för att bekanta dig med allmänna krav och begränsningar för att använda en teknisk för hands version, hur du uppdaterar mellan versioner och hur du ger feedback om funktionerna i en teknisk för hands version.    

**Kända problem i den här tekniska för hands versionen:**   
- ***Krav status***: när du installerar version 1611 kan den övergripande statusen för nödvändiga komponenter visas som godkänd med varningar, men listar inte vilka krav som orsakade varningarna. Detta kan orsakas av följande två krav:
  - Minnes alternativ för att skapa SQL-index
  - Söker efter SQL Server version som stöds  

  Eftersom dessa endast är varningar kan de ignoreras.

- ***PowerShell***: när du ansluter till Windows PowerShell från Configuration Manager-konsolen kan du få följande fel meddelande: **Microsoft. ConfigurationManagement. PowerShell. types. ps1xml är inte digitalt signerat**.  

   Du kan lösa det här problemet genom att ersätta vissa filer med signerade versioner från version 1610. Kopiera alla filer med följande fil namns tillägg från ** &lt;installations katalogen>\\ \adminconsole\bin** -mappen i version 1610-installationen: **. psd1**, **. ps1xml**och **. psm1**. Klistra in filerna i mappen ** &lt;installations katalog> \adminconsole\bin\\ ** i den tekniska för hands versionen 1611-installationen och skriv över 1611-versionen av filerna.


**Följande är nya funktioner som du kan prova med den här versionen.**  

## <a name="pre-cache-content-for-available-deployments-and-task-sequences"></a>Innehåll i förinställt cacheminne för tillgängliga distributioner och aktivitetssekvenser
I den här tekniska för hands versionen, för tillgängliga distributioner och aktivitetssekvenser, kan du välja att använda funktionen för cache för att låta klienterna Ladda ned relevant innehåll innan en användare installerar innehållet.

Anta till exempel att du vill distribuera en aktivitetssekvens för uppgradering av Windows 10 på plats, bara vill ha en enda aktivitetssekvens för alla användare och har flera arkitekturer och/eller språk. Om du skapar en tillgänglig distribution i Current Branch och sedan klickar på **Installera** i Software Center, hämtas innehållet vid den tidpunkten. Detta lägger till ytterligare tid innan installationen kan starta. Alternativt, i Current Branch om du skapar en tillgänglig aktivitetssekvensdistribution, hämtas allt innehåll som refereras i aktivitetssekvensen. Detta inkluderar uppgraderings paketet för operativ system för alla språk och arkitekturer. Om var och en är ungefär 3 GB i storlek kan hämtnings paketet vara ganska stort.

Med funktionen för cachelagring av innehåll kan du välja att låta klienten Ladda ned tillämpligt innehåll så fort det tar emot distributionen. När användaren klickar på **Installera** i Software Center är innehållet därför klart och installationen startar snabbt eftersom innehållet finns på den lokala hård disken.

### <a name="to-configure-the-pre-cache-feature"></a>Konfigurera för-cache-funktionen

1. Skapa uppgraderings paket för operativ system för vissa arkitekturer och språk. Ange arkitekturen och språket på fliken **data källa** för paketet. För språket använder du decimal konverteringen (till exempel 1033 är decimalen för engelska och 0x0409 är den hexadecimala motsvarigheten). Mer information finns i [skapa en aktivitetssekvens för att uppgradera ett operativ system](../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md).

    Arkitekturen och språk värdena används för att matcha stegen i aktivitetssekvensen som du skapar i nästa steg för att avgöra om uppgraderings paketet för operativ systemet ska förcachelagras.
2. Skapa en aktivitetssekvens med villkorliga steg för de olika språken och arkitekturerna. För den engelska versionen kan du till exempel skapa ett steg som följande:

    ![egenskaper för cachelagring](media/precacheproperties2.png)

    ![alternativ för cachelagring](media/precacheoptions2.png)  

3. Distribuera aktivitetssekvensen. Konfigurera följande för för-cache-funktionen:
    - På fliken **Allmänt** väljer du **Hämta innehåll i förväg för den här aktivitetssekvensen**.
    - På fliken **distributions inställningar** konfigurerar du aktivitetssekvensen med **tillgänglig** för **användning**. Om du skapar en **nödvändig** distribution fungerar inte för-cache-funktionen.
    - På fliken **Schemaläggning** för **schemat när den här distributionen ska vara tillgänglig** väljer du en tid i framtiden som ger klienter tillräckligt med tid att förinstallera innehållet innan distributionen görs tillgänglig för användarna. Du kan till exempel ange att den tillgängliga tiden ska vara tre timmar i framtiden för att tillåta tillräckligt med tid för att innehållet ska lagras i förväg.  
    - På fliken **distributions platser** konfigurerar du inställningarna för **distributions alternativ** . Om innehållet inte cachelagras på en klient innan användaren startar installationen, används dessa inställningar.


### <a name="user-experience"></a>Användarupplevelse
- När klienten tar emot distributions principen börjar den förcachelagra innehållet i förväg. Detta inkluderar allt refererat innehåll (alla andra paket typer) och endast uppgraderings paketet för operativ system som matchar klienten baserat på de villkor som du anger i aktivitetssekvensen.
- När distributionen görs tillgänglig för användare (inställningen på fliken **Schemaläggning** i distributionen) visas ett meddelande som informerar användarna om den nya distributionen och distributionen blir synlig i Software Center. Användaren kan gå till Software Center och klicka på **Installera** för att starta installationen.
- Om innehållet inte är fullständigt cachelagrat används inställningarna som anges på fliken **distributions alternativ** i distributionen. Vi rekommenderar att det finns tillräckligt med tid mellan när distributionen skapas och tiden då distributionen blir tillgänglig för användare för att tillåta klienter tillräckligt med tid för att cachelagra innehållet.


## <a name="see-also"></a>Se även
[Teknisk för hands version för Configuration Manager](../../core/get-started/technical-preview.md)
