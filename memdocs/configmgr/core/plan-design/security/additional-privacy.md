---
title: Ytterligare sekretessinformation
titleSuffix: Configuration Manager
description: Lär dig mer om hur Microsoft samlar in och använder data från Configuration Manager.
ms.date: 09/04/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1fcc921f-085f-4b0b-9c53-1e0707211076
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f877de32c9915f91d1e2d7f2d90b9b40ab69df11
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906579"
---
# <a name="additional-information-about-privacy-for-configuration-manager"></a>Ytterligare information om sekretess för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*


## <a name="updates-and-servicing"></a>Uppdateringar och service

Configuration Manager använder en uppdaterings modell som hjälper dig att hålla din miljö uppdaterad med de senaste uppdateringarna och funktionerna. Den här funktionen använder en plats system roll som kallas tjänst anslutnings punkt. Du väljer den server där du vill installera den här rollen. 

Mer information om insamlad information och hur de används finns i [användnings data](#usage-data).



## <a name="usage-data"></a>Användningsdata

Configuration Manager samlar in diagnostik-och användnings data om sig själv, som används av Microsoft för att förbättra installations upplevelsen, kvaliteten och säkerheten i framtida versioner.
Diagnostik-och användnings data är aktiverat för varje Configuration Manager hierarki. Det består av SQL Server frågor som körs veckovis på varje primär plats och på den centrala administrations webbplatsen. När hierarkin använder en central administrationswebbplats replikeras sedan data från primära platser till den platsen. På platsen på den översta nivån i hierarkin skickar tjänst anslutnings punkten den här informationen när den söker efter uppdateringar. Om tjänstanslutningspunkten är i offlineläge överförs informationen med hjälp av tjänstanslutningsverktyget.

Configuration Manager samlar endast in data från platsens SQL Server-databas och samlar inte in data direkt från klienter eller plats servrar.

Administratörer kan ändra data nivån som samlas in genom att gå till avsnittet **användnings data** i Configuration Manager-konsolen.

Mer information om nivåer och inställningar för användnings data finns i [diagnostik-och användnings data](../diagnostics/diagnostics-and-usage-data.md).



## <a name="log-analytics-connector"></a>Log Analytics koppling

Log Analytics Connector synkroniserar data, till exempel samlingar, från Configuration Manager till Azures moln tjänst. ID för Azure-prenumerationen och den hemliga nyckeln lagras i Configuration Manager-databasen när en administratör konfigurerar funktionen. Både den Azure Active Directory klient hemligheten och Azure-arbetsytans delade nyckel lagras i den lokala Configuration Managers databasen. All kommunikation mellan Configuration Manager och Azure använder HTTPS. Ingen ytterligare information om samlingarna tillhandahålls till Microsoft utanför slumpmässig diagnostik och användnings data. 

Mer information om den information som Log Analytics samlar in finns i [logg analys data säkerhet](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-security).



## <a name="asset-intelligence"></a>Tillgångsinformation

Tillgångsinformation låter administratörer definiera, spåra och proaktivt hantera överensstämmelse med konfigurations standarder. Mätning av och rapportering om distribution och användning av både fysiska och virtuella program hjälper organisationer att fatta bättre affärsbeslut om programlicenser och upprätthålla överensstämmelse med licensavtal. När du har samlat in användnings data från Configuration Manager-klienter kan du använda olika funktioner för att visa data, inklusive samlingar, frågor och rapporter.

Under varje synkronisering hämtas en katalog med känd program vara från Microsoft. Du kan välja att skicka Microsoft information om Okategoriserade program varu titlar som identifieras i din organisation för att genomsökas och läggas till i katalogen. Innan den här informationen överförs visas en dialog ruta med data som ska överföras. Överförda data kan inte återkallas. Tillgångsinformation skickar inte information om användare och datorer eller licens användning till Microsoft.

När en program varu titel har överförts identifierar Microsoft-forskare, kategoriserar och gör sedan kunskapen tillgänglig för alla andra kunder som använder den här funktionen och andra användare av katalogen. Överförda program varu titlar blir offentliga. Programmet och dess kategorisering blir en del av katalogen och kan sedan laddas ned till andra användare av katalogen. Innan du konfigurerar insamling av tillgångsinformationsdata och bestämmer huruvida du ska skicka information till Microsoft bör du tänka på vilka sekretesskrav som finns i din organisation.

Tillgångsinformation är inte aktiverat som standard i Configuration Manager. Överföring av Okategoriserade-titlar sker aldrig automatiskt och systemet är inte avsett att automatisera den här uppgiften. Du måste manuellt välja och godkänna överföring av varje programvarutitel.



## <a name="endpoint-protection"></a>Slutpunktsskydd

Microsoft Cloud Protection-tjänsten kallades tidigare Microsoft Active Protection Service eller MAPS.

Tillämpliga produkter är System Center-Endpoint Protection och Endpoint Protection funktionen i Configuration Manager (för att hantera System Center-Endpoint Protection och Windows Defender för Windows 10). Den här funktionen har inte implementerats för System Center-Endpoint Protection för Linux-eller System Center Endpoint Protection för Mac.

Communityn för skydd mot skadlig kod för Microsoft Cloud skydd är en frivillig världs omspännande värld med Endpoint Protection användare i System Center. När du ansluter Microsoft Cloud Protection Service skickar System Center Endpoint Protection automatiskt information till Microsoft. Microsoft använder informationen för att avgöra vilken program vara som ska undersökas efter potentiella hot och förbättra System Center-Endpoint Protectionens effektivitet. Den här gruppen hjälper till att stoppa spridningen av nya skadliga program varu infektioner. Om en Microsoft Cloud skydds tjänst rapport innehåller information om skadlig kod eller potentiellt oönskad program vara som Endpoint Protection klienten kan ta bort, kan Microsoft Cloud skydds tjänst hämta den senaste signaturen för att åtgärda den. Microsoft Cloud skydds tjänsten kan också hitta "falska positiva identifieringar" och åtgärda dem. (Falska positiva identifieringar är där något som ursprungligen identifierats som skadlig kod inte blir det.) 

Microsoft Cloud Protection Service-rapporter innehåller information om potentiella filer för skadlig kod, t. ex. fil namn, kryptografisk hash, åter försäljare, storlek och datumstämpel. Dessutom kan Microsoft Cloud skydds tjänst samla in fullständiga URL: er för att ange filens ursprung. Dessa URL: er kan ibland innehålla personlig information som Sök termer eller data som har angetts i formulär. Rapporter kan också innehålla åtgärder som du vidtog när du Endpoint Protection meddelat dig om oönskad program vara. Microsoft Cloud Protection Service-rapporter innehåller den här informationen för att hjälpa Microsoft att mäta hur effektivt Endpoint Protection kan identifiera och ta bort skadlig kod och potentiellt oönskad program vara och försöka identifiera ny skadlig kod.

Du kan gå med i Microsoft Cloud Protection Service om du har ett grundläggande eller avancerat medlemskap. De grundläggande medlems rapporterna innehåller den information som beskrivs ovan. Avancerade medlems rapporter är mer omfattande och kan innehålla ytterligare information om den program vara som Endpoint Protection identifierar, t. ex. program varans plats, fil namn, hur program varan fungerar och hur den påverkar din dator. Dessa rapporter och rapporter från andra Endpoint Protection användare som deltar i Microsoft Cloud Protection Service hjälper Microsoft-forskare att upptäcka nya hot snabbare. Definitioner av skadlig kod skapas sedan för program som uppfyller analys villkoren och de uppdaterade definitionerna görs tillgängliga för alla användare via Microsoft Update.

För att hjälpa till att identifiera och åtgärda vissa typer av skadlig kod skickar produkten regelbundet Microsoft Cloud skydds tjänst information om DATORns säkerhets tillstånd. Den här informationen innehåller information om DATORns säkerhets inställningar och loggfiler som beskriver de driv rutiner och annan program vara som läses in när datorn startas.

Ett tal som unikt identifierar din dator skickas också. Microsoft Cloud skydds tjänsten kan också samla in IP-adresser som de potentiella filerna för skadlig kod ansluter till.

Microsoft Cloud Protection Service-rapporter används för att förbättra Microsofts program vara och tjänster. Rapporterna kan också användas för statistiska eller andra testnings-eller analys ändamål och för att generera definitioner. Endast Microsofts anställda, leverantörer, partners och leverantörer som har ett företag som behöver använda rapporterna har till gång till dem.

Microsoft Cloud skydds tjänsten samlar inte avsiktligt in personlig information. I den utsträckning som Microsoft Cloud skydds tjänsten samlar in personlig information använder Microsoft inte informationen för att identifiera eller kontakta dig.

Mer information finns i [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md).



## <a name="site-hierarchy--geographical-view-with-bing-maps"></a>Webbplatshierarki – geografisk vy med Bing Maps

I Configuration Manager-konsolen går du till arbets ytan **övervakning** , väljer noden **platshierarki** och växlar till den **geografiska vyn**. I den här vyn kan du använda kartor som Microsoft Bing Maps tillhandahåller för att visa din Configuration Manager fysiska servertopologi. Den plats information som du anger skickas från servern till Bing Maps-webbtjänsten för att aktivera den här funktionen.

Microsoft använder den här informationen för att driva och förbättra Microsoft Bing Maps och andra webbplatser och tjänster från Microsoft. Mer information finns i [Microsofts sekretess policy](https://privacy.microsoft.com/privacystatement).

Du kan välja att inte använda den geografiska vyn för webbplatshierarkin. I vyn standardhierarki-diagram kan du se hierarkin och inte använda Bing Maps-tjänsten.
