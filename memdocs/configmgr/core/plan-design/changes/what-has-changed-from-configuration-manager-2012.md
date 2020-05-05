---
title: Ändringar från version 2012
titleSuffix: Configuration Manager
description: Identifiera ändringarna och nya funktioner i Configuration Manager jämfört med System Center 2012 Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3ae68fa6-8b30-45dd-9d12-50bb67cb4a9d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0cd49eac95d9789fd11ba2bf1ca01b68b236628d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720830"
---
# <a name="whats-changed-from-system-center-2012-configuration-manager"></a>Vad har ändrats från System Center 2012 Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Den aktuella grenen av Configuration Manager introducerar viktiga ändringar från System Center 2012 Configuration Manager. I den här artikeln beskrivs viktiga ändringar och nya funktioner som finns i den ursprungliga bas linje versionen 1511 av Configuration Manager aktuella grenen. Information om vilka ändringar som gjorts i de senaste uppdateringarna för Configuration Manager finns i [Nyheter i Configuration Manager stegvisa versioner](whats-new-incremental-versions.md).

> [!NOTE]
> Från Configuration Manager och med version 1910 är nu en del av Microsoft Endpoint Manager. Mer information finns i [Microsoft Endpoint Configuration Manager](whats-new-in-version-1910.md#bkmk_mem).

Versionen från december 2015 (version 1511) av Configuration Manager var den första versionen av den aktuella Configuration Manager produkten från Microsoft. Det kallas vanligt vis Configuration Manager aktuella grenen. *Aktuell gren* anger att den här versionen stöder stegvisa uppdateringar av produkten. Det ger också ett sätt att skilja mellan den här versionen och tidigare versioner av Configuration Manager.  

Configuration Manager aktuella grenen:  

- Använder inte ett år eller en produkt identifierare i produkt namnet, till skillnad från tidigare versioner som Configuration Manager 2007 eller System Center 2012 Configuration Manager.  

- Har stöd för stegvisa uppdateringar i produkten, även kallade uppdaterings versioner. Den första versionen var version 1511. Senare versioner släpps flera gånger per år som uppdateringar i konsolen, t. ex. version 1910.  

- Installeras med en bas linje version. Även om 1511 var den ursprungliga bas linje versionen, kommer nya bas linje versioner också att frisläppas från tiden till exempel 2002. Bas linje versioner kan användas för att installera en ny Configuration Manager webbplats och hierarki, eller för att uppgradera från en version av System Center 2012 Configuration Manager som stöds.  

## <a name="in-console-updates"></a><a name="bkmk_updates"></a>Uppdateringar i konsolen

Configuration Manager använder en tjänst metod i konsolen som kallas **uppdateringar och underhåll** som gör det enkelt att hitta och installera rekommenderade uppdateringar.  

Vissa versioner är bara tillgängliga som uppdateringar för befintliga platser inifrån Configuration Manager-konsolen. Du kan inte använda de här uppdateringarna för att installera en ny Configuration Manager-webbplats. Till exempel är 1910-uppdateringen bara tillgänglig i Configuration Manager-konsolen. Den används för att uppdatera en plats som redan kör en version av Configuration Manager som stöds.

Med jämna mellanrum släpps även en uppdaterings version som en ny *bas linje* version. Till exempel är uppdatering av version 2002 också en bas linje. Använd en bas linje version för att installera en ny plats eller hierarki. Starta inte med en äldre bas linje version som 1802 och uppgradera ditt sätt till den senaste versionen. Använd alltid den senaste bas linjen.

Mer information finns i följande artiklar:

- [Uppdateringar för Configuration Manager](../../servers/manage/updates.md)
- [Bas linje-och uppdaterings versioner](../../servers/manage/updates.md#bkmk_Baselines)

## <a name="service-connection-point"></a><a name="bkmk_servicepoint"></a>Tjänst anslutnings punkt  

Configuration Manager aktuella grenen innehåller en ny plats system roll, **tjänst anslutnings punkten**:  

- En kontakt punkt för många moln aktiverade funktioner

- Hämtar uppdateringar för webbplatsen

- Överför diagnostik-och användnings data om din webbplats till Microsoft Cloud

Den här plats system rollen stöder både online-och offline-läge. Mer information finns i [om tjänst anslutnings punkten](../../servers/deploy/configure/about-the-service-connection-point.md).  

## <a name="diagnostics-and-usage-data"></a><a name="bkmk_usage"></a>Diagnostik-och användnings data

Configuration Manager samlar in diagnostik-och användnings data om dina platser och din infrastruktur. Den här informationen kompileras och skickas till Microsofts moln tjänst av tjänst anslutnings punkten. Configuration Manager kräver dessa data för att hämta uppdateringar som gäller för din miljö. När du konfigurerar tjänst anslutnings punkten kan du ange både nivån på de data som samlas in och om du vill att data ska skickas automatiskt (online) eller manuellt (offline).

Mer information finns i [diagnostik-och användnings data](../diagnostics/diagnostics-and-usage-data.md).  

## <a name="deprecated-functionality"></a><a name="bkmk_out"></a>Föråldrade funktioner  

Vissa funktioner, till exempel inbyggt [stöd för Intel Active Management Technology (AMT)](#bkmk_AMT) baserade datorer, tas bort från Configuration Manager-konsolen. Andra funktioner, t. ex. Network Access Protection, tas bort helt. Dessutom stöds inte längre några äldre Microsoft-produkter som Windows Vista, Windows Server 2008 och SQL Server 2008.  

En lista över inaktuella funktioner finns i [borttagna och föråldrade objekt](deprecated/removed-and-deprecated.md).  

Mer information om produkter, operativ system och konfigurationer som stöds finns i [konfigurationer som stöds](../configs/supported-configurations.md).  

### <a name="support-for-intel-active-management-technology-amt"></a><a name="bkmk_AMT"></a> Stöd för Intel AMT (Active Management Technology)  

Configuration Manager aktuella grenen tar bort inbyggt stöd för AMT-baserade datorer i Configuration Manager-konsolen. AMT-baserade datorer förblir fullständigt hanterade när du använder [Intel SCS-tillägget för Microsoft Configuration Manager](https://www.intel.com/content/www/us/en/software/setup-configuration-software.html). Tillägget ger dig till gång till de senaste funktionerna för att hantera AMT och ta bort begränsningar som introduceras tills Configuration Manager kan inkludera ändringarna.  

Borttagning av integrerad AMT för Configuration Manager innehåller out-of-band-hantering. Plats system rollen för out-of-band-hantering är inte tillgänglig längre.  

> [!Note]
> Den här ändringen påverkar inte out-of-band-hantering i System Center 2012 Configuration Manager.

## <a name="changes-in-functionality"></a>Funktions ändringar

I följande avsnitt sammanfattas några av de betydande ändringarna i funktions områdena mellan System Center 2012 R2 Configuration Manager och version 1511-versionen av Configuration Manager aktuella grenen. Mer information om de senaste ändringarna i funktionerna finns i [Nyheter i stegvisa versioner](whats-new-incremental-versions.md).

### <a name="client-deployment"></a>Klientdistribution  

Configuration Manager introducerar en ny funktion för att testa nya versioner av Configuration Manager-klienten innan du uppgraderar resten av platsen med den nya program varan. Du kan ställa in en för produktions samling där du kan pilota en ny klient. När du är nöjd med den nya klient program varan i för produktion kan du befordra klienten för att automatiskt uppgradera resten av platsen med den nya versionen.  

Mer information om hur du testar klienter finns i [så här testar du klient uppgraderingar i en för produktions samling](../../clients/manage/upgrade/test-client-upgrades.md).  

### <a name="os-deployment"></a>Distribution av operativsystem  

Tänk på följande ändringar av OS-distributionen:

- I guiden skapa aktivitetssekvens är en ny typ av aktivitetssekvens tillgänglig: **uppgradera ett operativ system från uppgraderings paket**. Det skapar stegen för att uppgradera datorer från Windows 7 eller Windows 8,1 till Windows 10. Mer information finns i [uppgradera Windows till den senaste versionen](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md).  

- Peer-cache i Windows PE är nu tillgängligt när du distribuerar operativ system. Datorer som kör en aktivitetssekvens för att distribuera ett operativ system kan använda peer-cache i Windows PE för att hämta innehåll från en peer-cache-källa i stället för att hämta innehåll från en distributions plats. Den här funktionen bidrar till att minimera WAN-trafik i scenarier där det inte finns någon lokal distributions plats. Mer information finns i [förbereda peer-cache i Windows PE för att minska WAN-trafiken](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md).  

- Nu kan du Visa status för Windows som en tjänst i din miljö. Du kan också skapa Service planer för att skapa distributions ringar och se till att de aktuella avdelnings datorerna i Windows 10 hålls uppdaterade när nya versioner släpps. Dessutom kan du Visa aviseringar när Windows 10-klienter närmar sig slutet av stödet för deras version. Mer information finns i [hantera Windows som en tjänst](../../../osd/deploy-use/manage-windows-as-a-service.md).  

### <a name="application-management"></a>Programhantering  

Tänk på följande ändringar i program hanteringen:

- Med Configuration Manager kan du distribuera Universell Windows-plattform-appar (UWP) för enheter som kör Windows 10 och senare. Mer information finns i [skapa Windows-program](../../../apps/get-started/creating-windows-applications.md).  

- Software Center har ett nytt, modernt utseende. Användar tillgängliga appar som tidigare endast fanns i program katalogen visas nu i Software Center på fliken program. Detta gör att de här distributionerna blir mer synliga och gör dem onödigt att referera till den separata program katalogen. Dessutom krävs inte längre en Silverlight-aktiverad webbläsare. Mer information finns i [Planera för och konfigurera program hantering](../../../apps/plan-design/plan-for-and-configure-application-management.md).  

- Med det nya Windows Installer via MDM-programtypen kan du skapa och distribuera Windows Installer-baserade appar till registrerade datorer som kör Windows 10. Mer information finns i [skapa Windows-program](../../../apps/get-started/creating-windows-applications.md).  

- I Configuration Manager 2012, för att ange en länk till en app i Windows Store, kan du antingen ange länken direkt eller bläddra till en fjärrdator som hade appen installerad. I Configuration Manager aktuella grenen kan du fortfarande ange länken direkt, men nu kan du i stället för att bläddra till en referens dator söka i butiken efter appen direkt från Configuration Manager-konsolen.  

### <a name="software-updates"></a>Programuppdateringar  

Tänk på följande ändringar av program uppdateringar:

- Configuration Manager kan nu identifiera skillnaden mellan program uppdaterings hanterings metoder för datorer. Mer specifikt kan det skilja mellan en Windows 10-dator som ansluter till Windows Update for Business (WUfB) och en dator som är ansluten till WSUS. Attributet **UseWUServer** är nytt och anger om datorn hanteras med WUfB. Du kan använda den här inställningen i en samling för att ta bort de här datorerna från programuppdateringshanteringen. Mer information finns i [Integrering med Windows Update för företag i Windows 10](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md).  

- Nu kan du schemalägga och köra rensnings uppgiften i WSUS från Configuration Manager-konsolen. När du väljer att köra rensnings uppgiften för **program uppdaterings plats i komponent egenskaper för program uppdatering** körs den vid nästa synkronisering av program uppdateringar. Program uppdateringar som har upphört att gälla har statusen nekad på WSUS-servern och Windows Update-agenten på datorer inte längre genomsöker dessa program uppdateringar. Mer information finns i [Schemalägga och köra rensningsuppgiften i WSUS](../../../sum/deploy-use/software-updates-maintenance.md).  

### <a name="compliance-settings"></a>Kompatibilitetsinställningar  

Tänk på följande ändringar av kompatibilitetsinställningar:

- Configuration Manager förbättrar arbets flödet för att skapa konfigurations objekt. Nu när du skapar ett konfigurationsobjekt och väljer plattformar som stöds är endast inställningarna som är relevanta för plattformen tillgängliga. Se [Kom igång med](../../../compliance/get-started/get-started-with-compliance-settings.md)kompatibilitetsinställningar.  

- Med guiden **skapa konfigurations objekt** blir det nu enklare att välja den typ av konfigurations objekt som du vill skapa. Dessutom finns nya och uppdaterade konfigurationsobjekt för:  

    - Windows 10-enheter som hanteras med Configuration Manager-klienten  

    - Mac OS X-enheter som hanteras med Configuration Manager-klienten  

    - Windows-datorer och serverdatorer som hanteras med Configuration Manager-klienten  

    - Windows 8,1-och Windows 10-enheter som hanteras utan Configuration Manager-klienten  

    Mer information finns i [så här skapar du konfigurations objekt](../../../compliance/deploy-use/create-configuration-items.md).  

- Stöd för hantering av inställningar på Mac OS X-datorer som hanteras utan Configuration Manager-klienten.

### <a name="on-premises-mobile-device-management"></a>Lokal hantering av mobila enheter  

Nu kan du hantera mobila enheter med hjälp av lokal Configuration Manager infrastruktur. Alla enhets-och hanterings data hanteras lokalt och är inte en del av Microsoft Intune eller andra moln tjänster. Den här typen av enhets hantering kräver inte klient program vara. Configuration Manager hanterar enheter med funktioner som är inbyggda i enhetens operativ system.  

Mer information finns i [Hantera mobila enheter med lokal infrastruktur](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).

## <a name="next-steps"></a>Nästa steg

[Nyheter i senare versioner](whats-new-incremental-versions.md)
