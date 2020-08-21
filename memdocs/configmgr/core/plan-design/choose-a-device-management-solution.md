---
title: Välja en lösning för enhetshantering
titleSuffix: Configuration Manager
description: Lär dig mer om de lösningar som Microsoft erbjuder för att hantera datorer, servrar och enheter.
ms.date: 01/24/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 24633725-791a-4df7-8dce-2c24c1a19a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 877345e64045530193a4cdd735cdd399235b90c7
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700273"
---
# <a name="choose-a-device-management-solution"></a>Välja en lösning för enhetshantering

Microsoft erbjuder olika lösningar för att hantera datorer, servrar och enheter. Dessa lösningar är tillgängliga lokalt, molnbaserad eller en kombination av båda. Välj den lösning som passar organisationens affärs krav. Basera ditt beslut på de enhets plattformar du behöver för att hantera och de hanterings funktioner du behöver.

## <a name="overview"></a>Översikt

Det finns flera Microsoft-lösningar som kan fungera bäst i olika scenarier. Du behöver inte välja bara en.

- För en liten organisation kan ett verktyg som t. ex. Windows administrations Center vara en bra anpassning.
- Cirka 75% av IT-organisationer använder Configuration Manager för att hantera sina enheter.
- Microsoft Azure tillhandahåller olika lösningar från molnet eller lokalt med Azure Stack som främst riktar sig mot Server hantering.
- Microsoft Intune tillhandahåller moln hantering av klienter.
- Du kan kombinera Configuration Manager och Intune med samhantering.

Använd följande tabell som hjälp för att jämföra dessa hanterings tekniker:

|  | Enbart molnet | Molnbaserad | Lokal | Frånkopplad |
|---------|---------|---------|---------|---------|
| **Hyper-V-värd** | Inte tillämpligt | -Azure Stack<br/> – Windows administrations Center<br/> -Virtual Machine Manager | -Azure Stack<br/> – Windows administrations Center<br/> -Virtual Machine Manager | -Azure Stack<br/> – Windows administrations Center<br/> -Virtual Machine Manager |
| **Windows Server** | – Azure-hantering<br/> -Configuration Manager | – Azure-hantering<br/> -Configuration Manager | – Azure-hantering<br/> -Configuration Manager | Configuration Manager |
| **Linux-Server** | Azure-hantering | Azure-hantering | Azure-hantering |  |
| **Windows 10** | – Intune<br/> -Configuration Manager | – Intune<br/> -Configuration Manager | – Intune<br/> -Configuration Manager | Configuration Manager |
| **Windows 7 eller 8,1** | Configuration Manager | Configuration Manager | Configuration Manager | Configuration Manager |
| **Windows Virtual Desktop** | Configuration Manager | Inte tillämpligt | Inte tillämpligt | Inte tillämpligt |

Mer information finns i följande artiklar:

- [Vad är Azure Stack?](/azure-stack/operator/azure-stack-overview)
- [Vad är Windows administrations Center?](/windows-server/manage/windows-admin-center/understand/what-is)
- [Vad är Virtual Machine Manager?](/system-center/vmm/overview)
- [Azure-hanterings produkter](/azure/)
- [Vad är Windows Virtual Desktop?](/azure/virtual-desktop/overview)

Om du vill ha mer information om Configuration Manager-och Intune-lösningar kan du fortsätta till nästa avsnitt.

## <a name="client-management"></a>Klienthantering

I det här avsnittet jämförs följande fyra klient hanterings lösningar:

- [Configuration Manager-klient](#bkmk_sccm)
- [Lokal hantering av mobila enheter (MDM) med Configuration Manager](#bkmk_opmdm)
- [Samhantering med Microsoft Intune](#bkmk_comanage)
- [Microsoft Exchange](#bkmk_opmdm)

Du kan använda dessa lösningar själva eller i kombination med varandra. Du kan till exempel använda den klientbaserade hanterings metoden för att hantera datorer och servrar i organisationen och även använda samhantering för att hantera Internetbaserade bärbara datorer. Genom att kombinera metoder på det här sättet kan du hantera alla behov av enhets hantering.  

Det finns också två tabeller som jämför hanterings lösningarna med följande faktorer:

- [Jämför med plattformar som stöds](#bkmk_comp1)
- [Jämför med hanterings funktioner](#bkmk_comp2)

### <a name="configuration-manager-client"></a><a name="bkmk_sccm"></a> Configuration Manager-klient  

Det här alternativet kräver installation av Configuration Manager-klienten på enheter. Den innehåller de flesta funktioner för att hantera datorer, servrar och andra enheter i din miljö.

Mer information finns i [klient installations metoder](../clients/deploy/plan/client-installation-methods.md).  

### <a name="on-premises-mdm"></a><a name="bkmk_opmdm"></a> Lokal MDM  

Det här alternativet använder de enhets hanterings funktioner som är inbyggda i Windows 10. Även om det inte är en fullständig hantering av klientbaserade hanterings funktioner ger lokala MDM en lättare touch-metod för hantering. Den använder lokala Configuration Manager resurser för att hantera enheter.  

Mer information finns i [Hantera mobila enheter med lokal infrastruktur](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

### <a name="co-management-with-microsoft-intune"></a><a name="bkmk_comanage"></a> Samhantering med Microsoft Intune

Samhantering är ett av de främsta sätten att koppla din befintliga Configuration Manager-distribution till Microsoft 365 molnet. Det gör att du kan hantera Windows 10-enheter samtidigt genom att använda både Configuration Manager och Microsoft Intune. Med samhantering kan du Cloud-ansluta din befintliga investering i Configuration Manager genom att lägga till nya funktioner.

Mer information finns i [Vad är samhantering?](../../comanage/overview.md).  

### <a name="microsoft-exchange"></a><a name="bkmk_exchange"></a> Microsoft Exchange  

Det här alternativet använder Exchange Server-anslutningen för att ansluta flera Exchange-servrar till Configuration Manager. Den centraliserar hanteringen av enheter som kan ansluta till Exchange ActiveSync. Du kan konfigurera hanterings funktioner för mobila enheter i Exchange från Configuration Manager-konsolen. Exempel på funktioner är fjär rensning av enheter och inställnings kontroll för flera Exchange-servrar.

Mer information finns i [Hantera mobila enheter med Configuration Manager och Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

### <a name="compare-solutions-by-supported-platforms"></a><a name="bkmk_comp1"></a> Jämför lösningar med plattformar som stöds  

|Plattform|Configuration Manager-klient|Lokal MDM|Configuration Manager med Exchange| Intune |
|--------|----------------------------|---------------|-----------------------------------|--------|
|Android| | |Ja| Ja |
|iOS| | |Ja| Ja |
|Mac OS X|Ja| |Ja| Ja |
|Windows 10|Ja|Ja|Ja| Ja |
|Windows 10 Mobil| |Ja|Ja| Ja |
|Windows (tidigare versioner)|Ja| |Ja|  |
|Windows Server|Ja| |Ja|  |
|Windows Embedded|Ja| | |  |

En fullständig lista över plattformar som stöds finns i följande artiklar:

- [Operativ system som stöds för klienter och enheter för Configuration Manager](configs/supported-operating-systems-for-clients-and-devices.md)
- [Konfigurationer som stöds av Intune](/intune/supported-devices-browsers)

Microsoft rekommenderar att du använder Intune för att hantera Android-, iOS-och Windows 10 Mobile-enheter. Mer information finns i [Vad är Microsoft Intune?](/intune/what-is-intune).

### <a name="compare-solutions-by-management-functionality"></a><a name="bkmk_comp2"></a> Jämför lösningar efter hanterings funktioner  

|Hanterings funktioner|Configuration Manager-klient|Lokal MDM|Configuration Manager med Exchange|  
|--------|----------------------------|---------------|-----------------------------------|  
|Certifikatbaserad ömsesidig autentisering|Ja|Ja| |
|Klientinstallation|Ja| | |
|Support via Internet|Ja| | |
|Identifiering|Ja| |Ja|
|Maskinvaruinventering|Ja|Ja|Ja|
|Programvaruinventering|Ja| |Ja|
|Inställningar|Ja|Ja|Ja|
|Programvarudistribution|Ja|Ja| |
|Programuppdateringshanteraren|Ja| | |
|Distribution av operativsystem|Ja| | |
|Blockera från Configuration Manager|Ja|Ja| |
|Karantän och blockera från Exchange Server (och Configuration Manager)| | |Ja|
|Fjärrensning| |Ja|Ja|