---
title: Använd molntjänster
titleSuffix: Configuration Manager
description: Etablera moln resurser för Configuration Manager att komplettera din lokala infrastruktur.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 24fca61e-9cdb-447a-ad7a-f4d2e4fd6704
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 84cb878de3eea56dc68180a83fd4b6a32b2d1073
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906429"
---
# <a name="use-cloud-services-with-configuration-manager"></a>Använda molntjänster med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Manager stöder flera molnbaserade alternativ. Dessa kan komplettera din lokala infrastruktur och kan hjälpa till att lösa affärs problem som:  

-   Hantera BYOD (med Intune för hantering av mobila enheter).  

-   Hur du tillhandahåller innehålls resurser till isolerade klienter eller resurser i intranätet utanför företagets brand vägg (med hjälp av molnbaserade distributions platser).  

-   Skala ut infrastruktur när fysisk maskin vara inte är tillgänglig eller inte är logiskt placerad för att stödja dina behov (genom att använda Microsoft Azure virtuella datorer).  

Även om etablering av moln resurser inte är något som du måste göra innan du distribuerar Configuration Manager, kan det vara bra att förstå dessa alternativ innan du fortsätter för långt i en hierarkis design plan. Användningen av moln resurser kan spara pengar och tid och lösa affärs problem som inte kan uppstå i den lokala infrastrukturen.  

## <a name="cloud-based-resources-you-can-use-with-configuration-manager"></a>Molnbaserade resurser som du kan använda med Configuration Manager  
 Eftersom varje alternativ har olika krav kan du undersöka var och en mer på djupet för att förstå de unika kraven, begränsningarna och potentiella ytterligare kostnaderna baserat på användning.  

-   Information om molnbaserade distributions platser finns i [Installera molnbaserade distributions platser](../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md).

-   Mer information om Azure finns i [Vad är Azure?](https://azure.microsoft.com/overview/what-is-azure/)

### <a name="azure-virtual-machines-for-cloud-based-infrastructure"></a>Virtuella Azure-datorer (för molnbaserad infrastruktur)  
 Configuration Manager stöder användning av datorer som körs på virtuella datorer i Azure, precis som när det körs lokalt i det fysiska företags nätverket. Du kan använda virtuella Azure-datorer i följande scenarier:  

-   **Scenario 1:** Du kan köra Configuration Manager på en virtuell dator och använda den för att hantera klienter som är installerade på andra virtuella datorer.  

-   **Scenario 2:** Du kan köra Configuration Manager på en virtuell dator och använda den för att hantera klienter som inte körs i Azure.  

-   **Scenario 3:** Du kan köra olika Configuration Manager plats system roller på virtuella datorer, samtidigt som du kör andra roller i det fysiska företags nätverket (med lämpliga nätverks anslutningar för kommunikation).  

Samma krav för nätverk, operativ system och maskin varu krav som gäller för att installera Configuration Manager i det fysiska företags nätverket gäller även för installationen av Configuration Manager i Azure.  

En Azure-prenumeration krävs för att använda virtuella Azure-datorer. Du debiteras utifrån antalet virtuella datorer som du använder, deras konfiguration och användning av molnbaserade resurser.  

Dessutom omfattas Configuration Manager-platser och klienter som körs på virtuella Azure-datorer av samma licens krav som lokala installationer.  

### <a name="azure-services-for-cloud-based-distribution-points"></a>Azure-tjänster (för molnbaserade distributions platser)  
 Du kan använda en Azure-tjänst som värd för en Configuration Manager distributions plats, som kallas en molnbaserad distributions plats. Du kan [använda en molnbaserad distributions plats med Configuration Manager tillsammans med](../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md) lokala distributions platser och distributions platser som distribueras på virtuella Azure-datorer.  

 Detta skiljer sig från att använda en virtuell Azure-dator, där du distribuerar en platssystemroll. Molnbaserade distributions platser:  

-   Kör som en tjänst i Azure, inte på en virtuell dator.  

-   Skala automatiskt för att möta ökade innehålls begär Anden från klienter.  

-   Stöd för klienter på Internet och intranätet.  

En Azure-prenumeration krävs för att använda Azure som värd för distributions platser. Du debiteras utifrån mängden data som överförs till och från tjänsten.  

### <a name="additional-configuration-manager-capabilities"></a>Ytterligare funktioner i Configuration Manager  
 Vissa Configuration Manager-funktioner kan ansluta till molnbaserade tjänster, t. ex.:  

-   Windows Server Update Services (WSUS).  

-   Configuration Manager tjänst molnet för att hämta uppdateringar för Configuration Manager.  

Dessa ytterligare funktioner kräver inte att du har en Azure-prenumeration. Du behöver inte konfigurera vissa anslutningar, certifikat eller tjänster i molnet. De hanteras i stället automatiskt av Configuration Manager åt dig. Allt du behöver göra är att säkerställa att lämpliga plats system och enheter har åtkomst till Internetbaserade URL: er.  

##  <a name="security-for-cloud-based-services"></a><a name="BKMK_CloudSec"></a>Säkerhet för molnbaserade tjänster  
 Configuration Manager använder certifikat för att etablera och få åtkomst till ditt innehåll i Azure och för att hantera de tjänster som du använder. Configuration Manager krypterar de data som du lagrar i Azure, men ger inga ytterligare säkerhets-eller data kontroller utöver de som Azure tillhandahåller.  

 Mer information finns i informationen om de olika molnbaserade resurs scenarierna. Se även en [Introduktion till Azure-säkerhet](https://docs.microsoft.com/azure/security/fundamentals/overview).
