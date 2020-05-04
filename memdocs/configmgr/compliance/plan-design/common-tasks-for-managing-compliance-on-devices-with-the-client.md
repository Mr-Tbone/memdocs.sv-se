---
title: Vanliga uppgifter för hantering av efterlevnad
titleSuffix: Configuration Manager
description: Lär dig mer om att Configuration Manager kompatibilitetsinställningar genom att gå igenom några vanliga scenarier.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 4e345791-74db-41ad-b472-024ce6521daf
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 1ccb0f0a042a0dd82817e030f96bbbc729e752f0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712178"
---
# <a name="common-tasks-for-managing-compliance-on-devices-with-the-configuration-manager-client"></a>Vanliga aktiviteter för att hantera efterlevnad på enheter med Configuration Manager-klienten

*Gäller för: Configuration Manager (aktuell gren)*

Den här artikeln ger dig en introduktion till hur du använder Configuration Manager kompatibilitetsinställningar genom att du kan använda några vanliga scenarier som du kan stöta på.  

 Om du redan är bekant med kompatibilitetsinställningar kan du hitta detaljerad information om alla funktioner som du använder i [konfigurations objekt för enheter som hanteras med Configuration Manager-klienten](../../compliance/deploy-use/create-configuration-items.md).  

 Innan du börjar läser du [komma igång med](../../compliance/get-started/get-started-with-compliance-settings.md) kompatibilitetsinställningar för att lära dig grunderna om kompatibilitetsinställningar. Läs [plan för och konfigurera kompatibilitetsinställningar](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) för information om nödvändiga förutsättningar.  

## <a name="general-information-for-each-scenario"></a>Allmän information för varje scenario  
 I varje scenario skapar du ett konfigurationsobjekt som utför en viss uppgift. Gör så här för att öppna guiden skapa konfigurations objekt och komma igång:  

1.  I Configuration Manager-konsolen väljer du **till gångar och kompatibilitet** > **kompatibilitetsinställningar** > **konfigurations objekt**.  

1.  På fliken **Start** går du till gruppen **skapa** och väljer **skapa konfigurations objekt**.  

1.  På sidan **Allmänt** i guiden skapa konfigurations objekt, som visas på följande skärm bild, anger du ett namn och en beskrivning för konfigurationsobjektet. Välj sedan lämplig konfigurations objekt typ för varje scenario i den här artikeln.  

     ![Sidan allmänt i guiden skapa konfigurations objekt](../../mdm/deploy-use/media/Compliance-Settings-Wizard---1.png)  

## <a name="scenario-disable-bluetooth-on-windows-10-devices"></a>Scenario: inaktivera Bluetooth på Windows 10-enheter

 I det här scenariot har din säkerhets avdelning fastställt att Bluetooth-funktionen på enheter skulle kunna användas för att skicka känslig företags information utanför företaget. Du har nyligen uppgraderat alla dina datorer till Windows 10. Du bestämmer dig för att inaktivera Bluetooth på dessa enheter.  

1. På sidan **Allmänt** i guiden skapa konfigurations objekt väljer du konfigurations objekt typen **Windows 10** och väljer sedan **Nästa**.  

2. På sidan **Plattformar som stöds** i guiden väljer du alla Windows 10-plattformar.  

3. På sidan **enhets inställningar** väljer du **enhet**och väljer sedan **Nästa**.  

4. På sidan **Enhet** väljer du **Förhindras** som värde för **Bluetooth**.  

5. Välj **Reparera inställningar som inte är kompatibla** för att säkerställa att ändringen gäller för alla Windows 10-enheter.  

6. Skapa konfigurationsobjektet genom att slutföra guiden.  

 Nu kan du använda informationen i [vanliga uppgifter för att skapa och distribuera konfigurations bas linjer med Configuration Manager](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) artikel som hjälper dig att distribuera konfigurationen som du har skapat till enheter.  

## <a name="scenario-remediate-an-incorrect-registry-value-on-windows-desktop-computers"></a>Scenario: Åtgärda ett felaktigt registervärde på stationära Windows-datorer

> [!NOTE] 
> På Mac-datorer som kör Configuration Manager-klienten har du två alternativ för att utvärdera kompatibilitet:  
> - Utvärdera en fil med Mac OS X-inställningar (plist).
> - Använda ett anpassat skript och utvärdera resultaten av skriptet.  
>
>Mer information finns i [så här skapar du konfigurations objekt för Mac OS X-enheter som hanteras med Configuration Manager-klienten](../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md).  

 I det här scenariot upptäcker du att en viktig affärsappen inte körs på rätt sätt på vissa Windows 8,1-datorer som du hanterar. Du fastställer att detta beror på att en register nyckel med namnet **HKEY_LOCAL_MACHINE \Software\woodgrove\lob App\Configuration\Configuration1** har angetts till värdet **0** på vissa datorer. För att affärsappen ska kunna köras måste värdet vara **1**.  

 I den här proceduren ska du skapa ett konfigurations objekt som övervakar och automatiskt reparerar eventuella felaktiga register nyckel värden som hittas.  

1. På sidan **Allmänt** i guiden skapa konfigurations objekt väljer du konfigurations objekt typen **Windows-datorer och servrar (anpassad)** och väljer sedan **Nästa**.  

2. På sidan **plattformar som stöds** i guiden väljer du **Windows 8,1** (för att se till att konfigurationsobjektet endast gäller för datorer som påverkas).  

3. På sidan **Inställningar** väljer du **nytt** för att skapa en ny inställning.  

4. Konfigurera följande inställningar på fliken **Allmänt** i dialog rutan **Skapa inställning** :  

   -   **Namn** > **exempel inställning**  

   -   **Anger**register**värde**  >   

   -   **Data typen** > **Integer** (eftersom värdet endast innehåller ett tal)  

   -   **Hive** > -**HKEY_LOCAL_MACHINE**  

   -   **Key** > **SOFTWARE\Woodgrove\LOB App\Configuration\Configuration1**  

   -   **Värde** > **1** (det obligatoriska värdet)  

5. På fliken **efterlevnadsprinciper** i dialog rutan **Skapa inställning** väljer du **ny**. Konfigurera de här inställningarna i dialog rutan **Skapa regel** :  

   -   **Namn** > **exempel regel**  

   -   **Vald inställning** > verifiera att den valda inställningen är **exempel inställning**.

   -   **Regel typ** > **värde**  

   -   **Inställningen måste vara kompatibel med följande regel** > kontrol lera att Inställningens namn är korrekt och konfigurera alternativet för att ange att inställning svärdet måste vara lika med **1**.  

   -   **Reparera inkompatibla regler när stöd** > Markera den här kryss rutan för att se till att Configuration Manager återställer värdet för registervärdet till rätt värde om det är felaktigt.  

6. Skapa konfigurationsobjektet genom att slutföra guiden.  

 Nu kan du använda informationen i artikeln [vanliga aktiviteter för att skapa och distribuera konfigurations bas linjer](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) som hjälper dig att distribuera den konfiguration som du har skapat till enheter.  

## <a name="next-steps"></a>Nästa steg

[Skapa och distribuera konfigurationsbaslinjer](common-tasks-for-creating-and-deploying-configuration-baselines.md)
