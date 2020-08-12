---
title: Uppdateringar och service
titleSuffix: Configuration Manager
description: Lär dig mer om tjänst metoden i konsolen kallas uppdateringar och underhåll som gör det enkelt att hitta och installera rekommenderade uppdateringar.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3a832943-580a-4a40-b454-961d0854ac2b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3d8d9097b95a5daf06dc0260173e616fa2f88eb4
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126145"
---
# <a name="updates-and-servicing-for-configuration-manager"></a>Uppdateringar och underhåll för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Manager använder en tjänst metod i konsolen som kallas **uppdateringar och underhåll**. Den här metoden i konsolen gör det enkelt att hitta och installera rekommenderade uppdateringar för din Configuration Manager-infrastruktur. Underhåll i konsolen kompletteras med out-of-band-uppdateringar, till exempel snabb korrigeringar. Out-of-band-uppdateringar är avsedda för kunder som behöver lösa problem som kan vara specifika för deras miljö.  

> [!TIP]  
> Villkoren *Uppgradera*, *Uppdatera*och *Installera* används för att beskriva tre olika koncept i Configuration Manager. Mer information om hur varje term används finns i [om uppgradering, uppdatering och installation](../../understand/upgrade-update-install.md).  

## <a name="baseline-and-update-versions"></a><a name="bkmk_Baselines"></a> Baslinje- och uppdateringsversioner  

Använd den senaste baslinjeversionen när du installerar en ny plats i en ny hierarki.

- Du kan också använda en bas linje version för att uppgradera från System Center 2012 Configuration Manager.  

- När du har uppgraderat till Configuration Manager aktuella grenen ska du inte använda bas linje versioner för att hålla dig uppdaterad. Använd i stället bara [uppdateringar i konsolen](install-in-console-updates.md) för att uppdatera till den senaste versionen.  

- Med jämna mellanrum släpps ytterligare bas linje versioner. När du använder den senaste bas linje versionen för att installera en ny hierarki behöver du inte installera en inaktuell eller ej stödd version av Configuration Manager, följt av en ytterligare uppgradering av infrastrukturen för att få den uppdaterad.  

När du har installerat en baslinjeversion blir ytterligare versioner av Configuration Manager tillgängliga som uppdateringar i konsolen. Uppdateringar i konsolen uppdaterar infrastrukturen till den senaste versionen av Configuration Manager.  

- Installera uppdateringar i konsolen för att uppdatera versionen av platsen på högsta nivån.  

- Uppdateringar som du installerar på den centrala administrations platsen installeras automatiskt på underordnade primära platser. Styr den här tids inställningen genom att använda ett service fönster på den primära platsen. Mer information finns i [Service Windows](service-windows.md).  

- Uppdatera sekundära platser manuellt till en ny uppdaterings version från-konsolen.  

När du installerar en uppdatering lagrar uppdateringen installationsfiler för den versionen på plats servern i en mapp med namnet **CD. Senaste**. Mer information om dessa filer finns [på CD-skivan. Senaste mappen](the-cd.latest-folder.md).  

- Använd filerna i CD-skivan. Senaste mappen under webbplats återställning. När din hierarki inte längre kör en bas linje version kan du också använda dessa filer för att installera ytterligare platser.  

- Det går inte att använda installationsfiler från CD. Senaste för att installera den första platsen i en ny hierarki eller för att uppgradera en plats från System Center 2012 Configuration Manager.  

### <a name="version-details"></a>Versions information

Vissa uppdateringar för Configuration Manager finns både som en uppdateringsversion i konsolen för en befintlig infrastruktur, samt som en ny baslinjeversion.  

#### <a name="supported-versions"></a>Versioner som stöds

Följande versioner av Configuration Manager som stöds är för närvarande tillgängliga som en bas linje, en uppdatering eller båda:  

| Version | Tillgänglighetsdatum | [Slutdatum för support](current-branch-versions-supported.md) | Baslinje | Uppdatering i konsolen |  
|-------------|-----------|------------|--------------|------------------------|  
| [**2006**](../../plan-design/changes/whats-new-in-version-2006.md)<br /> (5.00.9012) | 11 augusti 2020 | 11 februari 2022 | Inga | Ja |
| [**2002**](../../plan-design/changes/whats-new-in-version-2002.md)<br /> (5.00.8968) | Den 1 april 2020 | 1 oktober 2021 | Ja,<sup>[Anmärkning 1](#bkmk_note1)</sup> | Ja |
| [**1910**](../../plan-design/changes/whats-new-in-version-1910.md)<br /> (5.00.8913) | 29 november 2019 | Den 29 maj, 2021 | Inga | Ja |
| [**1906**](../../plan-design/changes/whats-new-in-version-1906.md)<br /> (5.00.8853) | 26 juli 2019 | 26 januari 2021 | Inga | Ja |
| [**1902**](../../plan-design/changes/whats-new-in-version-1902.md)<br /> (5.00.8790) | 27 mars 2019 | 27 september 2020 | Ja | Ja |
| [**1810**](../../plan-design/changes/whats-new-in-version-1810.md)<br /> (5.00.8740) | 27 november 2018 | Den 1 december 2020 | Inga | Ja |

**Tillgänglighets datumet** är när [tidig uppdaterings ringen](checklist-for-installing-update-2006.md#early-update-ring) släpps. Du kommer att få ett bas linje medium tillgängligt i Volume licens Service Center när uppdateringen är globalt tillgänglig.

<a name="bkmk_note1"></a>

> [!Note]  
> <sup>**Anmärkning 1:**</sup> Bas linje mediet är tillgängligt som en del av följande versioner av [Volume Licensing Service Center](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) (VLSC):
>
> - Microsoft Endpoint ConfigMgr (aktuell gren)
> - System Center Data Center
> - System Center standard  
>
> Du kan till exempel söka i VLSC efter `Microsoft Endpoint Configmgr (current branch)` . Hitta bas linje mediet i listan med filer och ladda ned för den versionen.  

#### <a name="historical-versions"></a>Historiska versioner

I följande tabell visas tidigare versioner av Configuration Manager aktuella grenen som inte stöds:

| Version | Tillgänglighetsdatum | Stöds till och med | Baslinje | Uppdatering i konsolen |  
|-------------|-----------|------------|--------------|------------------------|  
| **1806** <br /> (5.00.8692) | 31 juli 2018 | 31 januari 2020 | Inga | Ja |
| **1802** <br /> (5.00.8634) | Den 22 mars 2018 | Den 22 september 2019 | Ja | Ja |
| **1710** <br /> (5.00.8577) | 20 november 2017 | 20 maj, 2019 | Inga | Ja |
| **1706** <br /> (5.00.8540) | 31 juli 2017 | 31 juli 2018 | Inga | Ja |
| **1702** <br /> (5.00.8498) | 27 mars 2017 | 27 mars 2018 | Ja | Ja |
| **1610** <br /> (5.00.8458) | 18 november 2016 | 18 november 2017 | Inga | Ja |
| **1606** <br /> (5.00.8412.1000) | Den 22 juli 2016 | Den 22 juli 2017 | Inga | Ja |
| **1606 med KB3186654** <br />5.00.8412.1307) | 12 oktober 2016 | 12 oktober 2017 | Ja | Inga |
| **1602** <br /> (5.00.8355) | 11 mars 2016 | 11 mars 2017 | Inga | Ja |
| **1511** <br /> (5.00.8325) | 8 december 2015 | 8 december 2016 | Ja | Inga |  

#### <a name="how-to-check-the-version"></a>Kontrol lera versionen

Om du vill kontrol lera versionen av din Configuration Manager plats går du till **om Configuration Manager** i konsolens övre vänstra hörn. I den här dialog rutan visas plats-och konsol versioner.  

> [!Note]  
> Konsol versionen skiljer sig något från plats versionen. Den lägre versionen av konsolen motsvarar Configuration Manager version. I Configuration Manager version 1802 är till exempel den första plats versionen 5.0.8634.1000 och den inledande konsol versionen är 5. **1802**. 1082,1700. Versions numren för build (1082) och revision (1700) kan ändras med framtida snabb korrigeringar.

## <a name="in-console-updates-and-servicing"></a><a name="bkmk_inconsole"></a> Uppdateringar och service i konsolen  

När du använder en produktions klar installation av Configuration Manager aktuella grenen är de flesta uppdateringar tillgängliga via kanalen för **uppdateringar och underhåll** . Den här metoden identifierar, hämtar och gör tillgängliga uppdateringar som gäller för den aktuella infrastruktur versionen och konfigurationen. Den innehåller bara uppdateringar som Microsoft rekommenderar för alla kunder.

Dessa uppdateringar omfattar:  

- Nya versioner, som version 1910, 2002 eller 2006.

- Uppdateringar som innehåller nya funktioner för den aktuella versionen.

- Snabb korrigeringar för din version av Configuration Manager och som alla kunder ska installera.

    > [!Note]  
    > Från och med version 1902 har snabb korrigeringar i konsolen nu ersättnings relationer. Mer information finns i [ersättning för snabb korrigeringar i konsolen](#bkmk_supersede).

Uppdateringarna i konsolen ger ökad stabilitet och löser vanliga problem. De ersätter de uppdaterings typer som visas för tidigare produkt versioner, till exempel Service Pack, kumulativa uppdateringar, snabb korrigeringar som är tillämpliga för alla kunder och tillägget för Microsoft Intune.

Uppdateringar i konsolen kan tillämpas på ett eller flera av följande system:  

- Primära och centrala administrationsplatsservrar  

- Platssystemroller och platssystemservrar  

- Instanser av SMS-providern  

- Configuration Manager-konsoler  

- Configuration Manager klienter  

Configuration Manager identifierar nya uppdateringar åt dig. Synkronisera din Configuration Manager tjänst anslutnings punkt med Microsoft Cloud service och Observera följande beteenden:  

- När tjänst anslutnings punkten är i onlineläge synkroniseras platsen med Microsoft varje dag. Den identifierar automatiskt nya uppdateringar som gäller för din infrastruktur. För att hämta uppdateringar och omdistribuerbara filer använder datorn som är värd för tjänst anslutnings punktens plats system roll **system** kontexten för att få åtkomst till följande Internet platser: go.microsoft.com och Download.Microsoft.com. Mer information om ytterligare platser som används av tjänst anslutnings punkten finns i [krav för Internet åtkomst](../deploy/configure/about-the-service-connection-point.md#bkmk_urls).  

- När tjänst anslutnings punkten är i offlineläge använder du tjänst anslutnings verktyget för att synkronisera manuellt med Microsoft-molnet. Mer information finns i [använda tjänst anslutnings verktyget](use-the-service-connection-tool.md).  

- Uppdateringar i konsolen ersätter behovet av att oberoende hitta och installera enskilda uppdateringar, service pack och nya funktioner.  

- Installera endast de uppdateringar i konsolen som du väljer. När du installerar vissa uppdateringar kan du välja enskilda funktioner för att aktivera och använda. Mer information finns i avsnittet [Enable optional features from updates](install-in-console-updates.md#bkmk_options).  

När du installerar en uppdatering i konsolen utförs följande process:  

- En kravkontroll körs automatiskt. Du kan även köra den här kontrollen manuellt innan du startar installationen.  

- Den installeras på platsen på den översta nivån i din miljö. Den här platsen är den centrala administrations platsen om du har en. I en-hierarki installeras uppdateringen automatiskt på primära platser. Styr när varje primär plats server tillåts uppdatera med hjälp av [Service Windows för plats servrar](service-windows.md).  

- När en plats server uppdateras uppdateras alla berörda plats system roller automatiskt. Dessa roller innehåller instanser av SMS-providern. När platsen har installerat uppdateringen kommer Configuration Manager-konsoler också att meddela konsol användaren att uppdatera konsolen.  

- Om en uppdatering innehåller Configuration Manager klienten, erbjuds du möjligheten att testa uppdateringen i för produktion eller att tillämpa uppdateringen på alla klienter direkt.  

- Sekundära platser uppdateras inte automatiskt när en primär plats har uppdaterats. I stället måste du starta uppdateringen av den sekundära platsen manuellt.  

> [!NOTE]  
> Den Configuration Manager aktuella grenen, den långsiktiga service grenen och den tekniska för hands versionen är olika versioner. Uppdateringar som gäller för en gren är inte tillgängliga som uppdateringar i konsolen för de andra grenarna. Mer information om tillgängliga grenar finns i [vilken gren av Configuration Manager ska jag använda?](../../understand/which-branch-should-i-use.md).

### <a name="supersedence-for-in-console-hotfixes"></a><a name="bkmk_supersede"></a>Ersättning för snabb korrigeringar i konsolen

<!-- 3229613 -->
Från och med version 1902 har snabb korrigeringar i konsolen nu ersättnings relationer. När Microsoft publicerar en ny Configuration Manager snabb korrigering, visar konsolen inte några snabb korrigeringar som ersätts av den här nya snabb korrigeringen. Med det här nya beteendet kan du bättre bestämma vilka snabb korrigeringar som ska installeras.

### <a name="supersedence-example"></a>Ersättnings exempel

Det finns tre snabb korrigeringar: hotfix – A, Hotfix-B och Hotfix-C. Hotfix – A ersätts av Hotfix-B och Hotfix-B ersätts av Hotfix-C.

|Snabb korrigering – A|Snabb korrigering – B|Snabb korrigering – C|I konsol läge|
|--------|--------|--------|---------------|
|Inte installerad|Inte installerad|Inte installerad|Visa alla tre snabb korrigeringar|
|Installerad|Installerad|Inte installerad|Hotfix-B visas som installerat<br/>Snabb korrigering – C visar som redo att installeras|
|Inte installerad|Inte installerad|Installerad|Hotfix-C visas som installerat|

## <a name="out-of-band-hotfixes"></a><a name="bkmk_outofband"></a> Out-of-band-snabbkorrigeringar  

Vissa snabb korrigeringar har begränsad tillgänglighet för att åtgärda specifika problem. Andra snabb korrigeringar är tillämpliga för alla kunder men kan inte installeras med hjälp av en i-konsol-metod. Dessa korrigeringar levereras out-of-band och identifieras inte från Microsoft-molntjänsten.  

När du vill åtgärda eller åtgärda ett problem med din distribution av Configuration Manager kan du vanligt vis lära dig om out-of-band-snabbkorrigeringar från Microsofts kund support, en Microsoft Support Knowledge Base-artikel eller [Configuration Manager teamets blogg](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/bg-p/ConfigurationManagerBlog).

Installera de här korrigeringarna manuellt med någon av följande två metoder:  

### <a name="update-registration-tool"></a>Verktyget uppdatera registrering

Det här verktyget importerar snabb korrigeringen manuellt till Configuration Manager-konsolen. Installera sedan uppdateringen på samma sätt som i konsol uppdateringar som identifieras automatiskt.  

Den här metoden används för snabb korrigeringar som använder följande fil namns struktur:  
    `<Product>-<product version>-<KB article ID>-ConfigMgr.Update.exe`

Mer information finns i [använda verktyget uppdatera registrering för att importera snabb korrigeringar](use-the-update-registration-tool-to-import-hotfixes.md).  

### <a name="hotfix-installer"></a>Installations program för snabb korrigeringar

Använd det här verktyget för att manuellt installera en snabb korrigering som inte kan installeras med hjälp av konsol metoden i konsolen.  

Den här metoden används för korrigeringar som använder följande fil namns struktur:  
    `<Product>-<product version>-<KB article ID>-<platform>-<language>.exe`  

Mer information finns i [Använd installations programmet för snabb korrigeringar för att installera uppdateringar](use-the-hotfix-installer-to-install-updates.md).  

## <a name="next-steps"></a>Nästa steg

Följande artiklar kan hjälpa dig att förstå hur du hittar och installerar de olika uppdaterings typerna för Configuration Manager:  

- [Installera uppdatering i konsolen](install-in-console-updates.md)  

- [Använd tjänstanslutningsverktyget](use-the-service-connection-tool.md)  

- [Använd verktyget uppdatera registrering för att importera snabb korrigeringar](use-the-update-registration-tool-to-import-hotfixes.md)  

- [Använd installations programmet för snabb korrigeringar för att installera uppdateringar](use-the-hotfix-installer-to-install-updates.md)  

Mer information om den tekniska för hands versionen finns i [Technical Preview](../../get-started/technical-preview.md).
