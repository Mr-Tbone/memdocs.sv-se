---
title: Förbereda distributioner till okända datorer
titleSuffix: Configuration Manager
description: Lär dig hur du distribuerar operativ system till datorer som inte hanteras av Configuration Manager i din Configuration Manager-miljö.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 9e447e34-0943-49ed-b6ba-3efebf3566c1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6e79e2ec1d42c7ed0e520b5e117fbac73817511a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724071"
---
# <a name="prepare-for-unknown-computer-deployments-in-configuration-manager"></a>Förbered för okända distributioner av datorer i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Använd informationen i det här avsnittet för att distribuera operativ system till okända datorer i din Configuration Managers miljö. En okänd dator är en dator som inte hanteras av Configuration Manager. Det innebär att det inte finns någon post för de här datorerna i Configuration Managers databasen. Okända datorer är:  

- En dator där Configuration Manager-klienten inte är installerad  

- En dator som inte har importer ATS till Configuration Manager  

- En dator som inte har identifierats av Configuration Manager  

  Du kan distribuera operativsystem till okända datorer med följande distributionsmetoder:  

- [Använda PXE för att distribuera Windows via nätverket](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)  

- [Använda startbara medier för att distribuera ett operativsystem](../deploy-use/create-bootable-media.md)  

- [Använda förinstallerade medier för att distribuera ett operativsystem](../deploy-use/create-prestaged-media.md)  

## <a name="unknown-computer-deployment-workflow"></a>Arbetsflöde för distribution till okänd dator  
 Följande är det grundläggande arbetsflödet för att distribuera ett operativsystem till en okänd dator:  

-   Välj ett okänt datorobjekt som ska användas i distributionen. Du kan distribuera operativsystemet till något av de okända datorobjekten i samlingen **Alla okända datorer** eller så kan du lägga till objekten i samlingen **Alla okända datorer** i en annan samling. Configuration Manager innehåller två okända dator objekt i samlingen **alla okända datorer** . Det ena objektet är avsett för x86-datorer och det andra för x64-datorer.  

    > [!NOTE]  
    >  Objektet **x86 okänd dator** används för datorer som är endast x86-kompatibla. Objektet **x64 okänd dator** är för datorer som är x86- och x64-kompatibla. Med andra ord beskriver de här objekten måldatorns arkitektur. De definierar däremot inte det operativsystem som du vill distribuera till måldatorn.  

-   Konfigurera en PXE-aktiverad distributionsplats eller skapa ett medium som ger stöd för distribution till okända datorer.  

-   Distribuera aktivitetssekvensen för att installera operativsystemet.  

## <a name="unknown-computer-installation-process"></a>Installationsprocess för okänd dator  
 När en dator först startas från PXE eller från ett medium kontrollerar Configuration Manager om det finns en post för datorn i Configuration Manager databasen. Om det finns en post, kontrollerar Configuration Manager om det finns några aktivitetssekvenser som distribueras till posten. Om det inte finns någon post kontrollerar Configuration Manager om det finns några aktivitetssekvenser som distribueras till ett okänt dator objekt. I båda fallen utför Configuration Manager sedan någon av följande åtgärder:  

- Om det finns en tillgänglig aktivitetssekvens, kommer Configuration Manager att begära att användaren kör aktivitetssekvensen.  

- Om det finns en obligatorisk aktivitetssekvens kör Configuration Manager automatiskt aktivitetssekvensen.  

- Om en aktivitetssekvens inte har distribuerats för posten genererar Configuration Manager ett fel som det inte finns någon distribuerad aktivitetssekvens för mål datorn.  

  När en okänd dator startas identifierar Configuration Manager datorn som en avetablerad dator i stället för en okänd dator. Det innebär att datorn kan ta emot aktivitetssekvenser som har distribuerats till det okända datorobjektet. Den distribuerade aktivitetssekvensen installerar sedan en operativ system avbildning som måste innehålla Configuration Manager-klienten.  

  När Configuration Manager-klienten har installerats skapas en post för datorn och datorn anges i lämplig Configuration Manager-samling. Om datorn inte kan installera operativ system avbildningen eller Configuration Manager klienten, skapas en "okänd" post för datorn och datorn visas i samlingen **alla system** .  

> [!NOTE]  
>  När operativsystemavbildningen installeras kan aktivitetssekvensen hämta samlingsvariabler men inte datorvariabler från datorn.  

##  <a name="enabling-unknown-computer-support"></a><a name="BKMK_EnablingUnknown"></a>Aktivera stöd för okända datorer  
 Använd följande för att aktivera stöd för okända datorer när du distribuerar ett operativsystem med PXE, startbara medier och förinstallerade medier.  

-   **PXE**  

     Markera kryssrutan **Aktivera stöd för okända datorer** på fliken **PXE** för en distributionsplats som är aktiverad för PXE. Mer information finns i [Konfigurera distributionsplatser att godta PXE-begäranden](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint).  

-   **Startbart medium**  

     Markera kryssrutan **Aktivera stöd för okända datorer** på sidan **Säkerhet** i guiden Skapa aktivitetssekvensmedia. Mer information finns i [Konfigurera distributions platser för att godkänna PXE-begäranden](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint) och [använda PXE för att distribuera Windows via nätverket med Configuration Manager](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

-   **Förberett medium**  

     Markera kryssrutan **Aktivera stöd för okända datorer** på sidan **Säkerhet** i guiden Skapa aktivitetssekvensmedia. Mer information finns i [Skapa förinstallerade media med Configuration Manager](../deploy-use/create-prestaged-media.md).  
