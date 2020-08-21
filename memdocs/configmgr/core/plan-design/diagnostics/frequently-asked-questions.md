---
title: Vanliga frågor och svar om diagnostik och användnings data
titleSuffix: Configuration Manager
description: Vanliga frågor om diagnostik-och användnings data för Configuration Manager
ms.date: 01/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3fe32aa2-d594-4ad0-a291-b8f5395ac50b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: eb14f909238e86a7aa4a87493b17a218a21f0909
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700205"
---
# <a name="frequently-asked-questions-about-diagnostics-and-usage-data"></a>Vanliga frågor om diagnostik och användningsdata

*Gäller för: Configuration Manager (aktuell gren)*

Den här artikeln innehåller svar på vanliga frågor om diagnostik-och användnings data i Configuration Manager.

## <a name="can-i-turn-off-diagnostic-and-usage-data"></a><a name="bkmk_off"></a> Kan jag stänga av diagnostik-och användnings data?

Använd tjänst anslutnings punkten i offline-läge för att hjälpa till att hantera när platsen skickar data. Använd sedan tjänst anslutnings verktyget för att skicka data manuellt. Mer information finns i följande artiklar:

- [Om tjänstanslutningspunkten](../../servers/deploy/configure/about-the-service-connection-point.md)
- [Använd tjänstanslutningsverktyget](../../servers/manage/use-the-service-connection-tool.md)

För att stödja nya versioner av Windows 10 och moln tjänster som Microsoft Intune måste du uppdatera den aktuella grenen av Configuration Manager regelbundet. Microsoft kräver minst den grundläggande nivån av diagnostik-och användnings data. Dessa data används för att hålla produkten uppdaterad, förbättra uppdaterings upplevelsen och förbättra produktens kvalitet och säkerhet.

Inga data skickas till tjänsten när tjänst anslutnings punkten är i offline-läge. När du växlar till onlineläge eller använder tjänst anslutnings verktyget, skickar den data till tjänsten för att söka efter uppdateringar.

Du kan också välja den data nivå som Configuration Manager samlar in. Mer information finns i [nivåer av diagnostikens användnings data](levels-overview.md).

## <a name="what-is-the-data-retention-period"></a><a name="bkmk_retention"></a> Hur länge sparas data?

Microsoft lagrar Configuration Manager diagnostik-och användnings data i ett år.

## <a name="is-diagnostics-and-usage-data-sent-when-setup-runs"></a><a name="bkmk_update"></a> Skickas diagnostik-och användnings data när installations programmet körs?

Nej. Diagnostik och användningsdata skickas endast efter att platsen har installerats och är i drift.

## <a name="how-frequently-is-the-data-sent"></a><a name="bkmk_frequency"></a> Hur ofta skickas data?

SQL-lagrade procedurer körs var sjunde dag från det datum då du installerade platsen.

- I onlineläge överför tjänst anslutnings punkten data efter att frågorna har körts.

- I offline-läge använder du tjänst anslutnings verktyget för att ladda upp data. (Data är inte tillgängliga för offlineanvändning förrän sju dagar efter att du har installerat platsen.)  

## <a name="can-the-data-be-used-to-form-a-network-map"></a><a name="bkmk_network"></a> Kan data användas för att bilda en nätverkskarta?

Nej. Dessa data omfattar inga nätverks uppgifter, till exempel IP-adresser eller detaljerad geografisk information. Mer information finns i [nivåer av diagnostikens användnings data](levels-overview.md#bkmk_versions)och hitta mer information om den version som du använder.

Data innehåller tids zons information från varje plats. Den här informationen kan ge insikter om bred plats och global spridning av platser i en hierarki.

## <a name="can-you-see-data-in-custom-sql-tables"></a><a name="bkmk_tables"></a> Kan du se data i anpassade SQL-tabeller?

Nej. Configuration Manager samlar in diagnostik-och användnings data via lagrade SQL-procedurer. Dessa lagrade procedurer körs mot standard produkt tabeller i databasen. Alla dessa SQL-tabeller har prefixet **TEL_**. Som en del av SQL-schemaidentifieringsfrågan hashas alla tabellnamn för jämförelse med kända standardvärden. Det här beteendet avgör att anpassade tabeller finns i databasen. Förekomsten av anpassade tabeller informerar Microsoft att du utökade databasschemat från standardvärdet. Den innehåller inte några av de data som lagras i dessa tabeller.

## <a name="can-you-see-other-databases"></a><a name="bkmk_databases"></a> Kan du se andra databaser?

Nej. De lagrade procedurerna för att samla in data är begränsade till Configuration Manager plats databasen. Microsoft kan inte se namnen på andra databaser eller data i andra databaser.

## <a name="is-any-data-sent-to-other-integrated-cloud-services"></a><a name="bkmk_cloud"></a> Skickas alla data till andra integrerade moln tjänster?

Ja, när du integrerar dessa tjänster med Configuration Manager. Som en del av interaktionen med valfri moln tjänst skickar Configuration Manager vissa data till den tjänsten. Dessa data är bara aktuella för moln tjänsten och skiljer sig från Configuration Manager diagnostik-och användnings data. Mer information om de data som används i interaktionen med en annan moln tjänst finns i dokumentationen för den tjänsten.

Följande moln tjänster är till exempel en del av Microsoft Endpoint Manager:

- [Data sekretess för Skriv bords analys](../../../desktop-analytics/privacy.md)
- [Sekretess och personliga data i Intune](/intune/protect/privacy-personal-data)
- [Windows autopilot-krav](/windows/deployment/windows-autopilot/windows-autopilot-requirements)

## <a name="does-configuration-manager-collect-any-personal-data"></a><a name="bkmk_personal"></a> Samlar Configuration Manager in personliga data?

Nej. Konfigurationen samlar inte in eller överför inga personliga data eller kund uppgifter. Det är en lokal produkt som du direkt distribuerar, hanterar och använder. Diagnostik-och användnings data som Microsoft samlar in förbättrar installations upplevelsen, kvaliteten och säkerheten i framtida versioner.

Mer information om Configuration Manager data finns i [nivåer av diagnostikdata](levels-overview.md).