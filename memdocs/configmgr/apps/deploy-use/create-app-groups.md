---
title: Skapa programgrupper
titleSuffix: Configuration Manager
description: Skapa en grupp av program som du kan skicka till en användar-eller enhets samling som en enskild distribution i Configuration Manager.
ms.date: 04/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: e67c691e-62ef-4f43-9cfb-0e957d1e7a5f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f63c52fcd2aaccbfbe04160581318126bc53db12
ms.sourcegitcommit: 2aa97d1b6409575d731c706faa2bc093c2b298c4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82643118"
---
# <a name="create-application-groups"></a>Skapa programgrupper

*Gäller för: Configuration Manager (aktuell gren)*

<!--3555907-->

Från och med version 1906 skapar du en grupp av program som du kan skicka till en användar-eller enhets samling som en enskild distribution. Metadata som du anger om app-gruppen visas i Software Center som en enda enhet. Du kan beställa apparna i gruppen så att klienten installerar dem i en speciell ordning.

> [!Note]  
> I den här versionen av Configuration Manager är app-grupper en för hands versions funktion. För att aktivera den, se [för hands versions funktioner](../../core/servers/manage/pre-release-features.md).  

1. I Configuration Manager-konsolen går du till arbets ytan **program varu bibliotek** . Expandera **program hantering** och välj noden **program grupp** .  

1. I gruppen Skapa i menyfliksområdet väljer du **skapa program grupp**.

1. På sidan **allmän information** anger du information om app-gruppen.  

1. På sidan **Software Center** inkluderar du information som visas i Software Center.  

1. På sidan **program grupp** väljer du **Lägg till**. Välj en eller flera appar för den här gruppen. Ändra ordning på dem med åtgärderna **Flytta upp** och **Flytta ned** .  

1. Slutför guiden.  

Distribuera App-gruppen med samma process som för ett program. Mer information finns i [distribuera program](deploy-applications.md). Från och med version 1910 kan du distribuera en app-grupp till enhets-eller användar samlingar.

När du har distribuerat gruppen:

- Om du lägger till en ny app i gruppen måste du separat distribuera den nya appens innehåll till distributions platser.

- Om du ändrar en app i app-gruppen distribuerar du om innehållet.

Om du vill felsöka en app Group-distribution använder du följande loggfiler på klienten:

- **AppGroupHandler. log**
- **AppEnforce.log**
- **SettingsAgent. log**

> [!Important]  
> Skapa eller distribuera inte en app-grupp förrän du har uppdaterat hela hierarkin och riktade klienter till minst version 1906.

### <a name="known-issues"></a>Kända problem

- *Version 1906*: appar i gruppen får bara innehålla **Windows Installer** -eller **skript** distributions typer.
  - *Version 1906*: Ange installations beteende för distributions typ **för att installera för system**.
- Följande distributions alternativ fungerar kanske inte: aviseringar, godkännande, stegvis distribution, reparation.
- Du kan inte exportera eller importera app-grupper.
- Ta inte med i gruppen alla appar som kräver omstart, eller så kan grupp distributionen Miss lyckas.
- *Version 1906*: det går inte att distribuera app-gruppen till en användar samling.
- *Version 1906*: användare kan inte **Avinstallera** app-gruppen i Software Center.
- Om du tar bort en app som är en del av en app-grupp visas följande varning när du visar egenskaperna för app-gruppen: "det går inte att läsa in information om alla program i gruppen." Gör en enkel ändring i app-gruppen och spara den. Du kan till exempel lägga till ett utrymme i **Administratörs kommentarerna**. När du sparar ändringen tas den borttagna appen bort från gruppen.<!-- 7099542 -->
