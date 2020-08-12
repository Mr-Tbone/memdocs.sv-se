---
title: Introduktion till samlingar
titleSuffix: Configuration Manager
description: Få en introduktion till att använda samlingar i Configuration Manager.
ms.date: 05/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d17e1188-d277-438f-9236-db9cd213b421
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4e43f5a36f2a1bf44959b9645c2fb48a22cc71f1
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126781"
---
# <a name="introduction-to-collections-in-configuration-manager"></a>Introduktion till samlingar i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Samlingarna hjälper dig att ordna resurser i hanterbara enheter. Du kan skapa samlingar som matchar dina klient hanterings behov och utföra åtgärder på flera resurser på en gång. 

De flesta hanterings uppgifter förlitar sig på eller kräver att du använder en eller flera samlingar. Även om du kan använda den inbyggda samlingen av alla system är det inte bästa praxis att använda den för hanterings uppgifter. Skapa anpassade samlingar för att mer specifikt identifiera enheter eller användare för en aktivitet.  

 Inbyggda och anpassade samlingar visas i noderna **användar samlingar** och **enhets samlingar** i arbets ytan **till gångar och efterlevnad** i Configuration Manager-konsolen.  

 Samlingar som du nyligen har visat visas i noden **användare** och i noden **enheter** i arbets ytan **till gångar och efterlevnad** .  

Här följer några exempel på samlings användning:  

|Åtgärd|Exempel|  
|---------|-------|  
|Gruppera resurser|Du kan skapa samlingar som grupperar resurser baserat på organisationens hierarki.<br /><br /> Du kan till exempel skapa en samling med alla datorer i "London Headquarters" Active Directory organisationsenhet (OU). Mer information om hur du skapar den här typen av samling finns i [så här skapar du samlingar](../../../../core/clients/manage/collections/create-collections.md).<br /><br /> Du kan använda den här samlingen för åtgärder som att konfigurera Endpoint Protection inställningar, konfigurera inställningar för enhets energispar funktioner eller installera Configuration Manager-klienten.|  
|Appdistribution|Du kan skapa en samling med alla datorer som inte har Microsoft Microsoft 365-appar installerade och sedan distribuera dem till alla datorer i samlingen.<br /><br /> Du kan också använda programkrav för att utföra den här uppgiften. Mer information finns i [så här skapar du program med Configuration Manager](../../../../apps/deploy-use/create-applications.md).|  
|[Hantera klientinställningar](../../../../core/clients/deploy/about-client-settings.md)|Även om standardinställningarna för klienten i Configuration Manager gäller alla enheter och alla användare kan du skapa anpassade klientinställningar som gäller för en samling med enheter eller en samling med användare.<br /><br /> Om du till exempel vill att fjärr styrning ska vara tillgängligt på alla utom ett fåtal enheter konfigurerar du standard klient inställningarna så att de tillåter fjärr styrning och konfigurerar sedan anpassade klient inställningar som inte tillåter fjärr styrning och distribuerar dem till samlingen med exceptionella klienter. |  
|[Energisparfunktioner](../power/introduction-to-power-management.md)|Du kan konfigurera specifika energi inställningar per samling.|  
|[Rollbaserad administration](../../../../core/servers/deploy/configure/configure-role-based-administration.md)|Använd samlingar för att kontrol lera vilka grupper av användare som har åtkomst till olika funktioner i Configuration Manager-konsolen.|  
|[Underhålls fönster](../../../../core/clients/manage/collections/use-maintenance-windows.md)|Med underhålls perioder kan du definiera en tids period när olika Configuration Manager-åtgärder kan utföras på medlemmar i en enhets samling. |  


## <a name="collection-types-in-configuration-manager"></a>Samlingstyper i Configuration Manager  
 Configuration Manager har inbyggda samlingar för vanliga åtgärder och du kan också skapa anpassade samlingar.   

### <a name="built-in-collections"></a>Inbyggda samlingar  
 Configuration Manager innehåller som standard följande samlingar som inte kan ändras.  

|**Samlingsnamn**|Beskrivning|  
|-------------------------|-----------------|  
|**Alla användargrupper**|Innehåller de användargrupper som identifieras med hjälp av Gruppidentifiering för Active Directory-säkerhet.|  
|**Alla användare**|Innehåller de användare som identifieras med hjälp av Identifiering av Active Directory-användare.|  
|**Alla användare och användargrupper**|Innehåller samlingarna Alla användare och Alla användargrupper. Den här samlingen innehåller det största omfånget för användar-och användar grupp resurser.|  
|**Alla skrivbords- och serverklienter**|Innehåller de server-och skriv bords enheter som har Configuration Manager-klienten installerad. Medlemskap erhålls av Identifiering av pulsslag.|  
|**Alla mobila enheter**|Innehåller de mobila enheter som hanteras av Configuration Manager. Medlemskapet är begränsat till de mobila enheter som har tilldelats en plats eller har identifierats av Exchange Server-anslutningen.|  
|**Alla system**|Innehåller alla Skriv bords-och Server klienter, alla mobila enheter och de okända dator samlingarna och alla mobila enheter som har registrerats med Microsoft Intune. Den här samlingen innehåller det största omfånget för enhets resurser.|  
|**Alla okända datorer**|Innehåller allmänna datorposter för flera datorplattformar. Du kan använda den här samlingen för att distribuera ett operativsystem med hjälp av en aktivitetssekvens och PXE-start, startbara medier eller förberedda medier.|  

### <a name="custom-collections"></a>Anpassade samlingar  
 När du skapar en anpassad samling i Configuration Manager bestäms medlemskapet i samlingen av en eller flera samlings regler, enligt beskrivningen i [skapa samlingar](../../../../core/clients/manage/collections/create-collections.md). 

