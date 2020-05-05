---
title: Aktivitetssekvenssteg för att hantera konvertering av BIOS till UEFI
titleSuffix: Configuration Manager
description: Lär dig hur du anpassar en aktivitetssekvens för operativ Systems distribution för att förbereda en FAT32-partition för över gång till UEFI.
ms.date: 03/24/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: bd3df04a-902f-4e91-89eb-5584b47d9efa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9183efd622cb425027500d3fe51ed7b86d3a94e4
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82079373"
---
# <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>Aktivitetssekvenssteg för att hantera konvertering av BIOS till UEFI
Windows 10 innehåller många nya säkerhetsfunktioner som kräver UEFI-aktiverade enheter. Du kanske har moderna Windows-datorer som har stöd för UEFI, men använder äldre BIOS. Om du konverterar en enhet till UEFI måste du gå till varje dator, partitionera om hård disken och konfigurera om den inbyggda program varan. Genom att använda aktivitetssekvenser i Configuration Manager kan du förbereda en hård disk för BIOS till UEFI-konvertering, konvertera från BIOS till UEFI som en del av uppgraderings processen på plats och samla in UEFI-information som en del av maskin varu inventeringen.

## <a name="hardware-inventory-collects-uefi-information"></a>Maskin varu inventering samlar in UEFI-information
Från och med version 1702 är en ny maskin varu inventerings klass (**SMS_Firmware**) och egenskap (**UEFI**) tillgängliga för att hjälpa dig att avgöra om en dator startar i UEFI-läge. När en dator startas i UEFI-läge anges egenskapen **UEFI** till **True**. Detta är aktiverat i maskin varu inventeringen som standard. Mer information om maskin varu inventering finns i [så här konfigurerar du maskin varu inventering](../../core/clients/manage/inventory/configure-hardware-inventory.md).

## <a name="create-a-custom-task-sequence-to-prepare-the-hard-drive-for-bios-to-uefi-conversion"></a>Skapa en anpassad aktivitetssekvens för att förbereda hård disken för BIOS till UEFI-konvertering
Från och med Configuration Manager version 1610 kan du nu anpassa en aktivitetssekvens för operativ Systems distribution med en ny variabel, TSUEFIDrive, så att steget **starta om datorn** ska förbereda en FAT32-partition på hård disken för över gång till UEFI. Följande procedur visar ett exempel på hur du kan skapa steg i aktivitetssekvensen för att förbereda hård disken för BIOS till UEFI-konvertering.

### <a name="to-prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>Förbereda FAT32-partitionen för konvertering till UEFI:
I en befintlig aktivitetssekvens för att installera ett operativ system lägger du till en ny grupp med steg för att göra BIOS till UEFI-konvertering.

1. Skapa en ny aktivitetssekvens efter stegen för att avbilda filer och inställningar, och före stegen för att installera operativ systemet. Du kan till exempel skapa en grupp efter mappen **avbilda filer och inställningar som** heter **BIOS-till-UEFI**.
2. På fliken **alternativ** i den nya gruppen lägger du till en ny variabel för aktivitetssekvens som ett villkor där **_SMSTSBootUEFI** **inte är lika** med **Sant**. Detta förhindrar att stegen i gruppen körs när en dator redan är i UEFI-läge.

   ![BIOS till UEFI-grupp](../../core/get-started/media/BIOS-to-UEFI-group.png)
3. Under den nya gruppen lägger du till steget **starta om datorn** . I **Ange vad som ska köras efter omstart**väljer **du den Start avbildning som är tilldelad den här aktivitetssekvensen är markerad** för att starta datorn i Windows PE.  
4. På fliken **alternativ** lägger du till en aktivitetssekvens-variabel som ett villkor där **_SMSTSInWinPE är lika med falskt**. Detta förhindrar att det här steget körs om datorn redan finns i Windows PE.

   ![Steg för omstart av dator](../../core/get-started/media/restart-in-windows-pe.png)
5. Lägg till ett steg för att starta OEM-verktyget som kommer att konvertera den inbyggda program varan från BIOS till UEFI. Detta är vanligt vis en åtgärd för att **köra kommando rads** steg med en kommando rad för att starta OEM-verktyget.
6. Lägg till steget för att formatera och partitionera disk som kommer att partitionera och formatera hård disken. I steget gör du följande:
   1. Skapa FAT32-partitionen som ska konverteras till UEFI innan operativ systemet installeras. Välj **GPT** som **disk typ**.
    ![Disk steget formatera och partitionera](../media/format-and-partition-disk.png)
   2. Gå till egenskaperna för FAT32-partitionen. Ange **TSUEFIDrive** i fältet **variabel** . När den här variabeln identifieras av aktivitetssekvensen förbereds den för UEFI-över gången innan datorn startas om.
    ![Egenskaper för partition](../../core/get-started/media/partition-properties.png)
   3. Skapa en NTFS-partition som motorn använder för att spara sitt tillstånd och lagra loggfiler.
7. Lägg till steget **starta om dator** i aktivitetssekvensen. I **Ange vad som ska köras efter omstart**väljer **du den Start avbildning som är tilldelad den här aktivitetssekvensen är markerad** för att starta datorn i Windows PE.  

## <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Konvertera från BIOS till UEFI under en uppgradering på plats
Windows 10 Creators Update introducerar ett enkelt konverterings verktyg som automatiserar processen för att partitionera om hård disken för UEFI-aktiverad maskin vara och integrera konverterings verktyget i Windows 7 till Windows 10 uppgraderings process på plats. När du kombinerar det här verktyget med aktivitetssekvensen för uppgradering av operativ system och OEM-verktyget som konverterar den inbyggda program varan från BIOS till UEFI, kan du konvertera datorerna från BIOS till UEFI under en uppgradering på plats till Windows 10 Creators Update.

**Krav**:
- Windows 10 Creators Update
- Datorer som stöder UEFI
- OEM-verktyg som konverterar datorns inbyggda program vara från BIOS till UEFI

### <a name="to-convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Så här konverterar du från BIOS till UEFI under en uppgradering på plats
1. Skapa en aktivitetssekvens för uppgradering av operativ system som utför en uppgradering på plats till Windows 10 Creators Update.
2. Redigera aktivitetssekvensen. I **gruppen efter bearbetning**lägger du till följande steg i aktivitetssekvensen:
   1. Lägg till steget **Kör kommando rad** från allmänt. Du lägger till kommando raden för MBR2GPT-verktyget som tar bort en disk från MBR till GPT utan att ändra eller ta bort data från disken. Skriv följande i kommando rad: **MBR2GPT/Convert/disk: 0/AllowFullOS**. Du kan också välja att köra MBR2GPT. EXE-verktyget i Windows PE i stället för i det fullständiga operativ systemet. Du kan göra detta genom att lägga till ett steg för att starta om datorn till WinPE innan steget för att köra MBR2GPT. EXE-verktyget och borttagning av alternativet/AllowFullOS från kommando raden. Mer information om verktyget och tillgängliga alternativ finns i [MBR2GPT. EXE](https://technet.microsoft.com/itpro/windows/deploy/mbr-to-gpt).
   2. Lägg till ett steg för att starta OEM-verktyget som kommer att konvertera den inbyggda program varan från BIOS till UEFI. Detta är vanligt vis en åtgärd för att köra kommando rads steg med en kommando rad för att starta OEM-verktyget.
   3. Lägg till steget **starta om datorn** från allmänt. För ange vad som ska köras efter omstart väljer **du det aktuella installerade standard operativ systemet**.
3. Distribuera aktivitetssekvensen.
