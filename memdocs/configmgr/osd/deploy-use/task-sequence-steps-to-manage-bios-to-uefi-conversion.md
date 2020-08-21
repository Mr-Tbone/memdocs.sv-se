---
title: Konvertera BIOS till UEFI
titleSuffix: Configuration Manager
description: Lär dig hur du anpassar en aktivitetssekvens för distribution av operativ system för att förbereda en FAT32-partition för över gång till UEFI.
ms.date: 05/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: bd3df04a-902f-4e91-89eb-5584b47d9efa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bf108cec074129f9b70e7cd2658cf2b1c8c10bc2
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697916"
---
# <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>Aktivitetssekvenssteg för att hantera konvertering av BIOS till UEFI

Windows 10 innehåller många nya säkerhetsfunktioner som kräver UEFI-aktiverade enheter. Du kan ha nyare Windows-enheter som stöder UEFI, men som använder äldre BIOS. Tidigare var du tvungen att konvertera en enhet till UEFI för att gå till varje enhet, partitionera om hård disken och konfigurera om den inbyggda program varan.

Med Configuration Manager kan du automatisera följande åtgärder:

- Förbereda en hård disk för BIOS till UEFI-konvertering
- Konvertera från BIOS till UEFI som en del av uppgraderings processen på plats
- Samla in UEFI-information som en del av maskin varu inventeringen

## <a name="hardware-inventory-collects-uefi-information"></a>Maskin varu inventering samlar in UEFI-information

Maskin varu inventerings klassen (**SMS_Firmware**) och Property (**UEFI**) är tillgängliga för att hjälpa dig att avgöra om en dator startar i UEFI-läge. När en dator startas i UEFI-läge anges egenskapen **UEFI** till **True**. Med maskin varu inventering aktive ras den här klassen som standard. Mer information om maskin varu inventering finns i [så här konfigurerar du maskin varu inventering](../../core/clients/manage/inventory/configure-hardware-inventory.md).

## <a name="create-a-custom-task-sequence-to-prepare-the-hard-drive"></a>Skapa en anpassad aktivitetssekvens för att förbereda hård disken

Du kan anpassa en aktivitetssekvens för operativ system distribution med variabeln **TSUEFIDrive** . Steget **starta om datorn** förbereder en FAT32-partition på hård disken för över gång till UEFI. Följande procedur visar ett exempel på hur du kan skapa steg i aktivitetssekvensen för att utföra den här åtgärden.

### <a name="prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>Förbereda FAT32-partitionen för konvertering till UEFI

I en befintlig aktivitetssekvens för att installera ett operativ system lägger du till en ny grupp med steg för att göra BIOS till UEFI-konvertering.

1. Skapa en ny aktivitetssekvens efter stegen för att avbilda filer och inställningar, och före stegen för att installera operativ systemet. Du kan till exempel skapa en grupp efter mappen **avbilda filer och inställningar som** heter **BIOS-till-UEFI**.

1. På fliken **alternativ** i den nya gruppen lägger du till en ny aktivitetssekvens som ett villkor. Ange **_SMSTSBootUEFI inte lika med sant**. Med det här villkoret körs bara dessa steg på BIOS-enheter i aktivitetssekvensen.

    :::image type="content" source="media/bios-to-uefi-group.png" alt-text="Villkor för BIOS till UEFI-grupp":::

1. Under den nya gruppen lägger du till steget **starta om datorn** . I **Ange vad som ska köras efter omstart**väljer **du den Start avbildning som är tilldelad den här aktivitetssekvensen är markerad**. Den här åtgärden startar om datorn i Windows PE.

1. På fliken **alternativ** lägger du till en aktivitetssekvens-variabel som ett villkor. Ange **_SMSTSInWinPE är lika med falskt**. Med det här villkoret körs inte aktivitetssekvensen detta steg om datorn redan finns i Windows PE.

    :::image type="content" source="media/restart-in-windows-pe.png" alt-text="Villkor vid omstart av dator steg":::

1. Lägg till ett steg för att starta ett OEM-verktyg för att konvertera den inbyggda program varan från BIOS till UEFI. Det här steget Kör vanligt vis **kommando raden**med kommandot för att köra OEM-verktyget.

1. Lägg till steget **Formatera och partitionera disk** i aktivitetssekvensen. I det här steget konfigurerar du följande alternativ:

    1. Skapa FAT32-partitionen för att konvertera till UEFI innan du installerar operativ systemet. Välj **GPT**för **disk typ**.

        :::image type="content" source="media/format-and-partition-disk.png" alt-text="Konfiguration av steg för att formatera och partitionera disk":::

    1. Gå till egenskaperna för FAT32-partitionen. I fältet **variabel** anger du `TSUEFIDrive` . När den här variabeln identifieras i aktivitetssekvensen förbereds partitionen för UEFI-över gången innan datorn startas om.

        :::image type="content" source="media/partition-properties.png" alt-text="Konfiguration av egenskaper för FAT32-partition":::

    1. Skapa en NTFS-partition som aktivitetssekvensen använder för att spara sitt tillstånd och lagra loggfiler.

1. Lägg till en annan åtgärd för att **starta om datorn** . I **Ange vad som ska köras efter omstart**väljer **du den Start avbildning som är tilldelad den här aktivitetssekvensen är markerad** för att starta datorn i Windows PE.

    > [!TIP]
    > Som standard är storleken på EFI-partitionen 500 MB. I vissa miljöer är start avbildningen för stor för att lagra på den här partitionen. Undvik det här problemet genom att öka storleken på EFI-partitionen. Ange till exempel 1 GB.<!-- SCCMDocs#1024 -->

## <a name="convert-from-bios-to-uefi-during-in-place-upgrade"></a><a name="bkmk_ipu"></a> Konvertera från BIOS till UEFI vid uppgradering på plats

Windows 10 innehåller ett enkelt konverterings verktyg, **MBR2GPT**. Den automatiserar processen för att partitionera om hård disken för UEFI-aktiverad maskin vara. Du kan integrera konverterings verktyget i uppgraderings processen på plats till Windows 10. Kombinera det här verktyget med din uppgraderings aktivitetssekvens och OEM-verktyget som konverterar den inbyggda program varan från BIOS till UEFI.

### <a name="requirements"></a>Krav

- En version av Windows 10 som stöds
- Datorer som stöder UEFI
- OEM-verktyg som konverterar datorns inbyggda program vara från BIOS till UEFI

### <a name="process-to-convert-from-bios-to-uefi-during-an-in-place-upgrade-task-sequence"></a>Process för att konvertera från BIOS till UEFI under en aktivitets serie för uppgradering på plats

1. [Skapa en aktivitetssekvens för att uppgradera ett operativsystem](create-a-task-sequence-to-upgrade-an-operating-system.md)

1. Redigera aktivitetssekvensen. I gruppen **efter bearbetning** gör du följande ändringar:

    1. Lägg till steget **Kör kommando rad** . Ange kommando raden för MBR2GPT-verktyget. När du kör i det fullständiga operativ systemet konfigurerar du det för att konvertera disken från MBR till GPT utan att ändra eller ta bort data. I **kommando rad**anger du följande kommando: `MBR2GPT.exe /convert /disk:0 /AllowFullOS`

    > [!TIP]
    > Du kan också välja att köra verktyget MBR2GPT.EXE när du är i Windows PE i stället för i det fullständiga operativ systemet. Lägg till ett steg för att starta om datorn till Windows PE innan du kör MBR2GPT.EXE-verktyget. Ta sedan bort alternativet **/AllowFullOS** från kommando raden.

    Mer information om verktyget och tillgängliga alternativ finns i [MBR2GPT.EXE](/windows/deployment/mbr-to-gpt).

    1. Lägg till ett steg för att köra OEM-verktyget som konverterar den inbyggda program varan från BIOS till UEFI. Det här steget Kör vanligt vis **kommando raden**, med en kommando rad för att köra OEM-verktyget.

    1. Lägg till steget **starta om datorn** och välj **det aktuella installerade standard operativ systemet**.

1. Distribuera aktivitetssekvensen.