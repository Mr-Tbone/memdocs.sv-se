---
title: Koppla användare till en dator
titleSuffix: Configuration Manager
description: Konfigurera Configuration Manager för att associera användare med mål datorer vid distribution av operativ system.
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 07c3c6d9-f056-4c4d-bc70-ede5ca933807
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f3a77e06dd2502b9007244ff9a3c9c9922fea592
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724204"
---
# <a name="associate-users-with-a-destination-computer-in-configuration-manager"></a>Koppla användare till mål datorn i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

När du använder Configuration Manager för att distribuera operativ system kan du koppla användare till mål datorn. Det här alternativet fungerar oavsett om en enskild användare eller flera användare är de primära användarna av mål datorn.  

Mappning mellan användare och enhet stöder användarorienterad hantering när du distribuerar program. När du kopplar en användare till mål datorn där du ska installera ett operativ system kan du senare distribuera program till den användaren och programmen installeras automatiskt på mål datorn. Även om du kan konfigurera stöd för mappning mellan användare och enhet under distribution av operativ system kan du inte använda mappning mellan användare och enhet för att distribuera operativ systemet.  

Mer information om mappning mellan användare och enhet finns i [Länka användare och enheter med mappning mellan användare och enhet](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

Det finns flera metoder som du kan använda för att integrera mappning mellan användare och enhet i dina operativ system distributioner. Du kan integrera mappning mellan användare och enhet i PXE-distributioner, startbara medier och distributioner med förberett medium.  


### <a name="create-a-task-sequence-that-includes-the-smstsassignusersmode-variable"></a>Skapa en aktivitetssekvens som innefattar variabeln **SMSTSAssignUsersMode**

Lägg till variabeln **SMSTSAssignUsersMode** i början av aktivitetssekvensen med hjälp av variabel steget [Ange aktivitetssekvens](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) . Den här variabeln specificerar hur aktivitetssekvensen hanterar användarinformationen.

Mer information finns i [variabler för aktivitetssekvens](../understand/task-sequence-variables.md#SMSTSAssignUsersMode).


### <a name="create-a-prestart-command-that-gathers-the-user-information"></a>Skapa ett förinläsningskommando som samlar in användarinformationen

För inläsnings kommandot kan vara ett VBScript med en inmatad ruta. Det kan också vara ett HTML-program (HTA) som validerar de användar data som de anger. 

Det här för inläsnings kommandot måste ange variabeln **SMSTSUDAUsers** som används när aktivitetssekvensen körs. Den här variabeln kan ställas in på en dator, en samling eller en aktivitetssekvensvariabel.

Mer information finns i [variabler för aktivitetssekvens](../understand/task-sequence-variables.md#SMSTSUDAUsers).


### <a name="configure-how-distribution-points-and-media-associate-the-user-with-the-destination-computer"></a>Konfigurera hur distributionsplatser och media kopplar användaren till måldatorn

Distributions platsen eller mediet har stöd för att associera användare med mål datorn där operativ systemet distribueras. Använd någon av följande metoder: 

- [Konfigurera en distributions plats att ta emot PXE-startbegäranden](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)  
- [Skapa startbara media](../deploy-use/create-bootable-media.md)  
- [Skapa för beredda medier](../deploy-use/create-prestaged-media.md)  


Att konfigurera stöd för mappning mellan användare och enhet har inte en inbyggd metod för att validera användar identiteten. Det här beteendet är viktigt när en tekniker konfigurerar datorn och anger information för användarens räkning. Förutom att ange hur aktivitetssekvensen hanterar användar informationen, ger konfigurering av dessa alternativ på distributions platsen och media möjligheten att begränsa de distributioner som startas från en PXE-start eller från en viss typ av medium.
