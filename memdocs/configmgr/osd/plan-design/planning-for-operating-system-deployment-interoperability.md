---
title: Interoperabilitet för OS-distribution
titleSuffix: Configuration Manager
description: Förstå kompatibilitetsfrågor när olika Configuration Manager-platser i en enskild hierarki använder olika versioner.
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: e327ce38-6c07-4a27-b6eb-7e5bf74ed04b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5931c43f0f8513ea1819e00f4eac7ecfd35dc717
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723553"
---
# <a name="plan-for-os-deployment-interoperability"></a>Planera för distribution av operativ system

*Gäller för: Configuration Manager (aktuell gren)*

Om olika Configuration Manager-platser i en enskild hierarki använder olika versioner är vissa Configuration Manager-funktionerna inte tillgängliga. Normalt är funktioner från den nya versionen av Configuration Manager inte tillgängliga på platser eller av klienter som kör en lägre version. Mer information finns i [samverkan mellan olika versioner av Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  


## <a name="objects"></a>Objekt

Överväg följande objekt när du uppgraderar platsen på den översta nivån i hierarkin och andra platser i hierarkin kör Configuration Manager med en lägre version:  

### <a name="client-installation-package"></a>Klient installations paket  

- Källan för standard klient installations paketet uppgraderas automatiskt. Alla distributions platser i hierarkin uppdateras med det nya klient installations paketet. Det här beteendet sker även på distributions platser på platser i hierarkin som har en lägre version.  

- Du kan inte tilldela nya versions klienter till webbplatser som du ännu inte har uppgraderat till den nya versionen. Tilldelningen blockeras på hanterings platsen.  

### <a name="boot-images"></a>Startavbildningar  

- När platsen på den översta nivån uppgraderas till den senaste versionen av Configuration Manager, uppdaterar den automatiskt standard start avbildningarna (x86 och x64). Uppdateringen använder Windows ADK för Windows 10, som innehåller Windows PE 10. De filer som är associerade med standard start avbildningarna uppdateras med den senaste Configuration Manager versionen av filerna. Platsen uppdaterar inte automatiskt anpassade Start avbildningar. Du måste uppdatera anpassade Start avbildningar manuellt, inklusive äldre versioner av Windows PE.  

- Om din platshierarki innehåller platser med olika versioner av Configuration Manager bör du undvika att använda dynamiska medier. Använd i stället platsbaserade medier för att kontakta en viss hanterings plats. När du har uppdaterat alla platser till samma version av Configuration Manager kan du använda dynamiskt medium igen.

- Kontrol lera att de senaste Configuration Manager start avbildningarna innehåller dina anpassningar. Uppdatera sedan alla distributions platser på den nya versions platsen med den senaste versionen av de nya start avbildningarna.  

### <a name="user-state-migration-tool-usmt"></a>USMT (User State Migration Tool)  

När platsen på den översta nivån uppgraderas till den senaste versionen av Configuration Manager uppdateras standard USMT-paketet automatiskt till den senaste versionen. Alla anpassade USMT-paket uppdateras inte automatiskt. Du måste uppdatera dessa paket manuellt.  

### <a name="new-task-sequence-steps"></a>Nya uppgiftssekvenssteg  

Med jämna mellanrum introduceras nya steg i en aktivitetssekvens med nya versioner av Configuration Manager. När du distribuerar en aktivitetssekvens med ett nytt steg till äldre klienter, Miss lyckas steget i aktivitetssekvensen. Innan du distribuerar en aktivitetssekvens med ett nytt steg, kontrollera att klienterna i målsamlingen har uppdaterats till den nya versionen.  

### <a name="os-deployment-media"></a>Mediet för operativ Systems distribution  

När platsen uppdateras till en ny version uppdaterar du alla media med det nya Configuration Manager klient paketet. Dessa medie typer är startbar, avbildning, förinstallerad och fristående.

### <a name="third-party-extensions-to-os-deployment"></a>Tillägg från tredje part till OS-distribution  

När du har tillägg från tredje part för operativ Systems distribution och du har olika versioner av Configuration Manager-platser eller Configuration Manager klienter kan det uppstå problem med tilläggen.  


## <a name="latest-version-of-configuration-manager-sites-in-a-mixed-hierarchy"></a>Senaste versionen av Configuration Manager-platser i en blandad hierarki  

När du uppgraderar en plats till den senaste versionen av Configuration Manager, börjar aktivitetssekvenser som refererar till standard klient installations paketet automatiskt att distribuera den senaste Configuration Manager-klient versionen.

Aktivitetssekvenser som refererar till ett anpassat klient installations paket fortsätter att distribuera den version av klienten som finns i det anpassade paketet. Anpassade paket innehåller troligen en tidigare version av Configuration Manager-klienten. Uppdatera eventuella anpassade klient installations paket till den senaste versionen om du vill undvika distributions problem vid aktivitetssekvensdistribution.

Gör något av följande när du konfigurerar en aktivitetssekvens för att använda ett anpassat klient installations paket:

- Uppdatera steget i aktivitetssekvensen om du vill använda den senaste Configuration Manager versionen av klient installations paketet
- Uppdatera det anpassade paketet för att använda den senaste Configuration Manager klient installations källan

> [!IMPORTANT]  
> Distribuera inte en aktivitetssekvens som refererar till det senaste Configuration Manager klient installations paketet till klienter på en äldre Configuration Manager plats. När klienter som är tilldelade till en äldre Configuration Manager plats uppgraderas till den senaste Configuration Manager-klient versionen, blockerar Configuration Manager tilldelningen till den äldre Configuration Managers platsen. De här klienterna är inte längre tilldelade till någon plats. Innan du tilldelar klienten till den senaste Configuration Manager-platsen manuellt, eller installerar om den äldre Configuration Manager versionen av klienten på datorn, är dessa klienter ohanterade.


## <a name="older-versions-of-configuration-manager-in-a-mixed-hierarchy"></a>Äldre versioner av Configuration Manager i en blandad hierarki  

När du uppgraderar den centrala administrations platsen till den senaste versionen av Configuration Manager, se till att de aktivitetssekvenser som du distribuerar inte lämnar dessa klienter i ohanterat tillstånd. Om du till exempel distribuerar till klienter som tilldelats en äldre Configuration Manager plats som du ännu inte har uppgraderat till den senaste versionen av Configuration Manager.

Gör en kopia av en aktivitetssekvens som du använder för att distribuera till klienter i den senaste versionen av Configuration Manager-platsen. Ändra sedan aktivitetssekvensen så att du kan distribuera den till klienter på en äldre Configuration Manager plats. Konfigurera aktivitetssekvensen så att den refererar till ett anpassat klient installations paket som använder den äldre Configuration Manager klient installations källan. Om du inte redan har ett anpassat klient installations paket som refererar till den äldre Configuration Manager klient installations källan, skapar du manuellt ett.  

> [!Important]  
> Från och med version 1902 kan du inte distribuera ett paket eller en aktivitetssekvens till en klient version 5,7730 eller tidigare. Undvik den här begränsningen genom att uppgradera klienten till en senare version.<!-- SCCMDocs-pr issue #3493 -->
