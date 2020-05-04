---
title: 'Skapa konfigurations objekt för klient-hanterade Mac-enheter '
titleSuffix: Configuration Manager
description: Använd konfigurations objekt Configuration Manager Mac OS X för att hantera inställningar för Mac OS X-enheter.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 722d5bf5-bedc-4dfc-b324-6eeb773874e9
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 219ddd4c828cdabd022deb9fe372718184a4c024
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713025"
---
# <a name="create-configuration-items-for-mac-os-x-devices"></a>Skapa konfigurations objekt för Mac OS X-enheter
Använd det anpassade konfigurationsobjektet Configuration Manager **Mac OS X (anpassat)** för att hantera inställningar för Mac OS X-enheter som hanteras av Configuration Manager klienten.  
  
Operativ systemet Mac OS X använder egenskaps List (. plist)-filer för att lagra program inställningar. Använd kompatibilitetsinställningarna när du ska utvärdera och reparera inställningar i en fil med en egenskapslista. Du kan också hantera Mac OS X-inställningar genom att skriva ett kommando skript som returnerar ett värde som du kan utvärdera och åtgärda för efterlevnad.  
  
## <a name="create-a-custom-mac-os-x-configuration-item"></a>Skapa ett anpassat konfigurations objekt för Mac OS X  
  
1. I Configuration Manager-konsolen väljer du **till gångar och efterlevnad**.  
  
2. I arbets ytan **till gångar och efterlevnad** expanderar du **kompatibilitetsinställningar**och väljer sedan **konfigurations objekt**.  
  
3. På fliken **Start** går du till gruppen **skapa** och väljer **skapa konfigurations objekt**.  
  
4. På sidan **Allmänt** i guiden **skapa konfigurations objekt** anger du ett namn och en valfri beskrivning för konfigurationsobjektet.  
  
5. Välj **Mac OS X (anpassat)** under **Ange typen av konfigurationsobjekt som du vill skapa**.  
  
6. Om du skapar och tilldelar kategorier som hjälper dig att söka efter och filtrera konfigurations objekt i Configuration Manager-konsolen väljer du **Kategorier**.  
  
7. På sidan **Plattformar som stöds** i guiden väljer du de specifika Mac OS X-versioner som ska utvärdera konfigurationsobjektet.  
  
8. På sidan **Inställningar** i guiden lägger du till nya inställningar som utvärderas för kompatibilitet på Mac-datorer. Välj **ny** för att öppna dialog rutan **Skapa inställning** .  
  
9. Ange ett unikt namn och en beskrivning av inställningen i dialogrutan **Skapa inställning**.  
  
10. Välj den **inställnings typ** som du vill använda och ange den information som krävs:  
  
    -   **Inställningar för Mac OS X**  
  
        -   **Program-ID**: Ange program-ID: t för den egenskaps lista fil från vilken du vill utvärdera en nyckel för efterlevnad.  
  
             Om du till exempel vill redigera inställningarna för webbläsaren Safari kan du använda **com.apple.Safari.plist**.  
  
        -   **Nyckel**: Ange namnet på den nyckel som du vill utvärdera för kompatibilitet på Mac-datorer. Använd följande syntax: */<ordlista\>/<nyckelnamn\>*.  
  
            > [!IMPORTANT]  
            >  Nyckel namnet är Skift läges känsligt och utvärderas inte om det skiljer sig från nyckel namnet på Mac-datorn. Dessutom kan du inte redigera nyckel namnet när du har angett det. Om du behöver redigera nyckel namnet tar du bort och återskapar sedan inställningen.  
  
    -   **Över**  
  
        -   **Identifierings skript**: Välj **Lägg till skript**och ange sedan ett gränssnitts skript för att utvärdera inställningarna på Mac-datorn för kompatibilitet. Använd **ECHO** -kommandot i Shell-skriptet för att returnera värden till Configuration Manager för efterlevnad. Configuration Manager använder de resultat som returneras i **STDOUT** för att utvärdera kompatibiliteten.  
  
            > [!IMPORTANT]  
            >  Ta inte med kommandot **reboot** i identifierings skriptet. Eftersom identifierings skriptet körs varje gång klienten startas om, gör detta att Mac-datorn startar om kontinuerligt.  
  
        -   **Reparations skript (valfritt)**: du kan också välja **Lägg till skript**och sedan ange ett gränssnitts skript som används för att reparera inkompatibla inställningar som hittas på Mac-klientdatorer.  
  
            > [!IMPORTANT]  
            >  Använd inte kopiera och klistra in för att se till att du inte använder formateringstecken som Mac-datorn inte kan tolka. Skriv i stället i skriptet.  
  
11. Välj **datatyp**, vilket är det format som villkoret returnerar data i innan det används för att utvärdera inställningen.  
  
    > [!NOTE]  
    >  Datatypen **Flyttal** stöder endast tre siffror efter decimaltecknet.  
    >   
    >  Configuration Manager stöder inte användning av skript inställningarna **Boolean** data Type för Mac-konfigurationsobjekt. Ange i stället data typen **Integer**och kontrol lera att skriptet returnerar ett heltals värde.  
  
12. Välj **OK** för att spara inställningen och stänga dialog rutan **Skapa inställning** . Fortsätt sedan att lägga till så många inställningar som du behöver.  
  
13. På sidan **efterlevnadsprinciper** i guiden anger du villkoren som definierar kompatibiliteten för ett konfigurations objekt. Innan kompatibiliteten för en inställning kan utvärderas måste den ha minst en kompatibilitetsregel. Välj **ny** för att lägga till en ny regel.  
  
14. Ange följande information i dialogrutan **Skapa regel**:  
  
    -   **Namn**: Ange ett namn för regeln för efterlevnad.  
  
    -   **Beskrivning**: Ange en beskrivning av regeln för efterlevnad.  
  
    -   **Vald inställning**: Välj **Bläddra** för att öppna dialog rutan **Välj inställning** . Välj den inställning som du vill definiera en regel för eller Välj **ny inställning**. När du är färdig väljer du **Välj**.  
  
        > [!TIP]  
        >  Du kan också välja **Egenskaper** om du vill visa information om den valda inställningen.  
  
    -   **Regeltyp**: Välj den typ av efterlevnadsprincip som du vill använda:  
  
        -   **Värde**: skapa en regel som jämför värdet som returneras av konfigurationsobjektet med ett värde som du anger.  
  
        -   **Existentiell**: skapa en regel som utvärderar inställningen beroende på om den finns på en enhet.  
  
    -   Ange följande information för regeltypen **Värde**:  
  
        -   **Inställningen måste vara kompatibel med följande regel**: Välj en operator och ett värde som utvärderas för kompatibilitet med den valda inställningen. Du kan använda följande operatorer:  
  
            -   **Är lika med**  
  
            -   **Inte lika med**  
  
            -   **Större än**  
  
            -   **Mindre än**  
  
            -   **Mellan**  
  
            -   **Större än eller lika med**  
  
            -   **Mindre än eller lika med**  
  
            -   **En av**: Ange en post på varje rad i text rutan.  
  
            -   **Ingen av**: Ange en post på varje rad i text rutan.  
  
        -   **Reparera inkompatibla regler när stöd**: Välj det här alternativet om du vill att Configuration Manager ska reparera inkompatibla regler automatiskt.  
  
            > [!IMPORTANT]  
            >  Du kan bara reparera inkompatibla regler när regeloperatorn har värdet **Lika med**.  
  
        -   **Rapportera inkompatibilitet om den här inställnings instansen inte hittas**: konfigurationsobjektet rapporterar inkompatibilitet om den här inställningen inte hittas på Mac-datorn.  
  
        -   **Allvarlighets grad för inkompatibilitet för rapporter**: Ange allvarlighets graden som rapporteras om denna efterlevnadsprincip Miss lyckas. Följande allvarlighetsgrader finns:  
  
            -   **Ingen**: datorer som inte uppfyller den här regeln rapporterar inte allvarlighets grad för Configuration Manager rapporter.  
  
            -   **Information**: datorer som inte uppfyller den här regeln rapporterar allvarlighets graden **information** för Configuration Manager rapporter.  
  
            -   **Varning**! datorer som inte uppfyller den här regeln rapporterar allvarlighets graden **Varning** för Configuration Manager rapporter.  
  
            -   **Kritiskt**: datorer som inte uppfyller den här regeln rapporterar allvarlighets graden **kritisk** för Configuration Manager rapporter.  
  
            -   **Kritisk med händelse**: datorer som inte uppfyller den här regeln rapporterar allvarlighets graden **kritisk** för Configuration Manager rapporter. Den här allvarlighets graden loggas också av Mac-klientdatorn.  
  
    -   Ange följande information för regeltypen **Existentiell**:  
  
        -   Välj något av följande:  
  
            -   **Inställningen måste finnas på klientenheter**  
  
            -   **Inställningen får inte finnas på klientenheterna**  
  
        -   **Allvarlighets grad för inkompatibilitet för rapporter**: Ange allvarlighets graden som rapporteras om den här regeln för efterlevnad Miss lyckas. Följande allvarlighetsgrader finns:  
  
            -   **Ingen**: datorer som inte uppfyller den här regeln rapporterar inte allvarlighets grad för Configuration Manager rapporter.  
  
            -   **Information**: datorer som inte uppfyller den här regeln rapporterar allvarlighets graden **information** för Configuration Manager rapporter.  
  
            -   **Varning**! datorer som inte uppfyller den här regeln rapporterar allvarlighets graden **Varning** för Configuration Manager rapporter.  
  
            -   **Kritiskt**: datorer som inte uppfyller den här regeln rapporterar allvarlighets graden **kritisk** för Configuration Manager rapporter.  
  
            -   **Kritisk med händelse**: datorer som inte uppfyller den här regeln rapporterar allvarlighets graden **kritisk** för Configuration Manager rapporter. Den här allvarlighets graden loggas också av Mac-klientdatorn.  
  
        > [!NOTE]  
        >  Vilka alternativ som visas varierar beroende på vilken inställnings typ du konfigurerar en regel för.  
  
15. Stäng dialog rutan **Skapa regel** genom att klicka på **OK** .  
  
16. På sidan **Sammanfattning** bekräftar du inställningarna för det nya konfigurationsobjektet. Slutför sedan guiden.  
  
Se det nya konfigurationsobjektet i noden **konfigurations objekt** på arbets ytan **till gångar och efterlevnad** .  
  
Om du nu vill lägga till det här konfigurationsobjektet i en konfigurations bas linje, se [så här skapar du konfigurations bas linjer](../../compliance/deploy-use/create-configuration-baselines.md).  
  
## <a name="next-steps"></a>Nästa steg

 [Konfigurations objekt för enheter som hanteras med Configuration Manager-klienten](../../compliance/deploy-use/create-configuration-items.md)
