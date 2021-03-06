---
title: Hantera uppdateringar för Surface-drivrutiner
titleSuffix: Configuration Manager
description: Configuration Manager synkroniserar uppdateringar för Surface-drivrutiner för distribution till Surface-enheter.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 06/18/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: e9f9f4e6-5b4f-4b8f-94d6-db9b2b239113
ms.openlocfilehash: c0b4942e8a6e81477814e24281e0d9e3752c5f90
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88696879"
---
# <a name="manage-surface-drivers-with-configuration-manager"></a>Hantera Surface-drivrutiner med Configuration Manager

*Gäller för: System Center Configuration Manager (Current Branch)*

Med System Center Configuration Manager kan du synkronisera driv rutiner för Surface-enheter och distribuera dem som en program uppdatering. Med den här funktionen kan du se till att dina Surface-enheter kör de senaste tillgängliga driv rutinerna. Den här synkroniseringen introducerades först i version 1706 som en för hands versions funktion och den blev en funktion i 1710. <!--3684621, 3608197, 1098490-->

## <a name="prerequisites-for-synchronizing-surface-drivers"></a>Krav för synkronisering av Surface-drivrutiner

- En Internet ansluten program uppdaterings plats på översta nivån.
- Alla program uppdaterings platser måste köra Windows Server 2016 med Cumulative Update KB4025339 eller senare installerat.
- Configuration Manager aktiverar inte den här valfria funktionen som standard. Aktivera den här funktionen innan du använder den. Mer information finns i avsnittet [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

## <a name="enable-sync-for-surface-drivers"></a>Aktivera synkronisering för Surface-drivrutiner

Gör så här för att aktivera synkronisering av Surface-drivrutiner:

1. Anslut Configuration Manager-konsolen till plats servern på den översta nivån.
1. Gå till **Administration**  >  **plats konfiguration**  >  **platser**och klicka sedan på platsen på den högsta nivån.
1. I menyfliksområdet väljer du **Inställningar**  >  **Konfigurera plats komponenter**  >  **program uppdaterings plats**.
1. Klicka på fliken **klassificeringar** och klicka sedan på kryss rutan för att **Inkludera uppdateringar för Microsoft-Surface-drivrutiner och inbyggd program vara** och klicka på **tillämpa**.

     ![Aktivera Surface-drivrutiner från egenskaperna för program uppdaterings platsen](media/enable-surface-driver-sync.png)

1. Klicka på fliken **produkter** i egenskaperna för komponenten för program uppdaterings plats. Mer information finns i avsnittet [produkter för Surface-drivrutiner](#bkmk_prod) och [Surface-modeller](#bkmk_models) .
1. Välj produkter för varje version av Windows 10 som du vill stödja Surface-drivrutiner för. Du ser att det finns två olika versioner av varje produkt för driv rutiner:

   - Windows 10- *version* **uppdatering och senare underhålls driv rutiner**
   - Windows 10- *versions* **uppdatering och senare uppgradering & underhålls driv rutiner**.

     ![Produkt lista för driv rutiner för Windows 10-versioner](media/surface-driver-products-sup.png)

1. När du är färdig med att välja produkterna klickar du på **OK**.
1. [Synkronisera program uppdaterings platsen](../get-started/synchronize-software-updates.md) för att ta med Surface-drivrutinerna i Configuration Manager.
1. När du har synkroniserat Surface-drivrutinerna distribuerar du dem på samma sätt som du distribuerar andra uppdateringar.

## <a name="products-for-surface-drivers"></a><a name="bkmk_prod"></a> Produkter för Surface-drivrutiner

De flesta driv rutiner tillhör följande produkt grupper:

- Driv rutiner för Windows 10 och senare versioner
- & underhålls driv rutiner för Windows 10 och senare uppgradering
- Uppdatering av Windows 10-årsdagar och senare underhålls driv rutiner
- Uppdatering av Windows 10-jubileum och senare uppgradering & underhålls driv rutiner
- Windows 10 Creators Update och senare underhålls driv rutiner
- Windows 10 Creators Update och senare uppgraderar & underhålls driv rutiner
- Windows 10 är Creators Update och senare underhålls driv rutiner
- Windows 10 är Creators Update och senare uppgraderar & underhålls driv rutiner
- Windows 10 S och senare underhålls driv rutiner
- Windows 10 S version 1709 och senare underhålls driv rutiner för testning
- Windows 10 S version 1709 och senare uppgradera & underhålls driv rutiner för testning
- Windows 10 S version 1803 och senare underhålls driv rutiner
- Windows 10 S version 1803 och senare uppgradera & underhålls driv rutiner
- Windows 10 S version 1809 och senare underhålls driv rutiner
- Windows 10 S version 1809 och senare, uppgradera & underhålls driv rutiner
- Windows 10 S version 1903 och senare underhålls driv rutiner
- Windows 10 S version 1903 och senare, uppgradera & underhålls driv rutiner
- Underhålls driv rutiner för Windows 10 version 1803 och senare
- Windows 10 version 1803 och senare uppgradering & underhålls driv rutiner
- Windows 10 version 1809 och senare underhåll driv rutiner
- Windows 10 version 1809 och senare, uppgradera & underhålls driv rutiner
- Windows 10 version 1903 och senare underhåll driv rutiner
- Windows 10 version 1903 och senare, uppgradera & underhålls driv rutiner

> [!NOTE]
> De flesta Surface-drivrutinerna tillhör flera Windows 10-produktsortiment. Du kanske inte behöver välja alla produkter som anges här. För att minska antalet produkter som fyller din uppdaterings katalog rekommenderar vi att du bara väljer de produkter som krävs av din miljö för synkronisering.

## <a name="surface-models"></a><a name="bkmk_models"></a> Surface-modeller

Följande tabell innehåller de funktions modeller och versioner av Windows 10 där Configuration Manager kan installera driv rutiner. Uppdateringar av Surface-drivrutiner är inte tillgängliga i Configuration Manager samma dag som de publiceras i Microsoft Updates katalogen. Configuration Manager upprätthåller en egen lista över vilka Surface-drivrutiner som ska importeras. Enheter som behöver Windows 10 S-produkter noteras. Microsoft syftar till att hämta de Surface-drivrutiner som lagts till i listan över tillåtna den andra tisdagen varje månad för att göra dem tillgängliga för synkronisering till Configuration Manager. Mer information finns i [vanliga frågor och svar](#bkmk_faq).

</br>

|Surface-modell|Windows 10 1709| Windows 10 1803|Windows 10 1809|Windows 10 1903|Windows 10 1909|
|----|----|----|----|----|----|
|Surface Pro 3|Ja| Ja| Ja |Ja|Ja|
|Surface Pro 4|Ja| Ja| Ja |Ja|Ja|
|Surface Pro 6|Ej tillämpligt| Ja| Ja |Ja|Ja|
|Surface Pro 7|Saknas| Saknas| Saknas |Ja|Ja|
|Yta Pro X|Saknas| Saknas| Saknas |Ja|Ja|
|Surface Book|Ja| Ja| Ja |Ja|Ja|
|Surface Book 2|Ja| Ja| Ja |Ja|Ja|
|Surface Book 3|Saknas| Saknas| Saknas |Ja|Ja|
|Surface-dator|Ja, med produkten "Windows 10 S version 1709 och senare service driv rutiner" valt| Ja, med produkten "Windows 10 S version 1803 och senare service driv rutiner" valt|Ja, med produkten "Windows 10 S version 1809 och senare uppgradera & Servicing-drivrutiner" valt|Ja, med produkten "Windows 10 S version 1903 och senare uppgradera & Servicing-drivrutiner" valt|Ja, med produkten "Windows 10 S version 1903 och senare uppgradera & Servicing-drivrutiner" valt|
|Surface laptop 2|Ej tillämpligt| Ja |Ja|Ja|Ja|
|Surface laptop 3|Saknas| Saknas|Saknas|Ja |Ja|
|Surface go|Ej tillämpligt| Ja, med produkten "Windows 10 S version 1803 och senare service driv rutiner" valt|Ja, med produkten "Windows 10 S version 1809 och senare uppgradera & Servicing-drivrutiner" valt|Ja, med produkten "Windows 10 S version 1903 och senare uppgradera & Servicing-drivrutiner" valt|Ja, med produkten "Windows 10 S version 1903 och senare uppgradera & Servicing-drivrutiner" valt|
|Surface Go 2|Saknas| Saknas| Ja |Ja|Ja, med produkten "Windows 10 S version 1903 och senare uppgradera & Servicing-drivrutiner" valt|
|Surface Studio|Ja| Ja| Ja |Ja|Ja|
|Surface Studio 2|Ej tillämpligt| Ja| Ja |Ja|Ja|

## <a name="verify-the-configuration"></a>Verifiera konfigurationen

Kontrol lera att program uppdaterings platsen är korrekt konfigurerad genom att använda **WsyncMgr. log** och **WCM. log**.

1. Öppna WsyncMgr. log och Sök efter följande loggpost:

    ```text
    Surface Drivers can be supported in this hierarchy since all software update points are on Windows Server 2016, WCM SCF property Sync Catalog Drivers is set. 
    …
    Sync Catalog Drivers SCF value is set to : 1
    ```

1. Om någon av följande poster är inloggad i **WsyncMgr. log**, markera kryss rutan **Inkludera uppdateringar för Microsoft-Surface-drivrutiner och inbyggd program vara** i egenskaperna för program uppdaterings platsen:
   - `Sync Surface Drivers option is not set`
   - `Sync Catalog Drivers SCF value is set to : 0`

1. Öppna **WCM. log** och leta efter objekt som liknar följande poster:
   ```text
   <Categories>
   <Category Id="Product:05eebf61-148b-43cf-80da-1c99ab0b8699"><![CDATA[Windows 10 and later drivers]]></Category>
   <Category Id="Product:06da2f0c-7937-4e28-b46c-a37317eade73"><![CDATA[Windows 10 Creators Update and Later Upgrade & Servicing Drivers]]></Category>
   <Category Id="Product:c1006636-eab4-4b0b-b1b0-d50282c0377e"><![CDATA[Windows 10 S and Later Servicing Drivers]]></Category>
   … …
   </Categories>
   ```

   Den här posten är ett XML-element som visar varje produkt grupp och klassificering som är synkroniserad av program uppdaterings plats servern. Om du inte hittar de produkter som du har valt, så sparas dubbla kontroller av produkterna för program uppdaterings platsen.
1. Du kan också vänta tills nästa synkronisering har slutförts. Kontrol lera sedan om uppdateringar för Surface-drivrutinen och inbyggd program vara visas i program uppdateringar i Configuration Manager-konsolen. Konsolen kan till exempel visa följande information: ![ synkroniserade Surface-drivrutiner i Configuration Manager-konsolen](media/synchronized-surface-drivers.png)

##  <a name="frequently-asked-questions-faq"></a><a name="bkmk_faq"></a> Vanliga frågor och svar

### <a name="after-i-follow-the-steps-in-this-article-my-surface-drivers-are-still-not-synchronized-why"></a>När jag har följt stegen i den här artikeln synkroniseras inte mina Surface-drivrutiner. Varför?

Om du synkroniserar från en överordnad Windows Server Update Services (WSUS)-Server, i stället för Microsoft Update, kontrollerar du att den överordnade WSUS-servern är konfigurerad för att stödja och synkronisera uppdateringar av Surface-drivrutiner. Alla underordnade servrar är begränsade till uppdateringar som finns i den överordnade WSUS-serverdatabasen.

Det finns fler än 68 000 uppdateringar som klassificeras som driv rutiner i WSUS. För att förhindra att icke-Surface-relaterade driv rutiner synkroniseras till Configuration Manager, filtrerar Microsoft filter driv rutins synkronisering mot en lista över tillåtna. När den nya listan över tillåtna har publicerats och integrerats i Configuration Manager läggs de nya driv rutinerna till i-konsolen efter nästa synkronisering. Microsoft syftar till att hämta de Surface-drivrutiner som lagts till i listan över tillåtna den andra tisdagen varje månad för att göra dem tillgängliga för synkronisering till Configuration Manager.

Om din Configuration Managers miljö är offline, importeras en ny lista över tillåtna varje gång du importerar [service uppdateringar](../../core/servers/manage/use-the-service-connection-tool.md) till Configuration Manager. Du måste också importera en [ny WSUS-katalog](../get-started/synchronize-software-updates-disconnected.md) som innehåller driv rutinerna innan uppdateringarna visas i Configuration Manager-konsolen. Eftersom en fristående WSUS-miljö innehåller fler driv rutiner än en Configuration Manager-SUP rekommenderar vi att du upprättar en Configuration Manager miljö som har online-funktioner och att du konfigurerar den för att synkronisera Surface-drivrutiner. Detta ger en mindre WSUS-export som liknar offline-miljön.

Om din Configuration Managers miljö är online och kan identifiera nya uppdateringar kommer du att få uppdateringar av listan automatiskt. Om du inte ser de förväntade driv rutinerna granskar du WCM. log och WsyncMgr. log efter synkroniseringsfel.

### <a name="my-configuration-manager-environment-is-offline-can-i-manually-import-surface-drivers-into-wsus"></a>Min Configuration Managers miljö är offline, kan jag importera Surface-drivrutiner manuellt till WSUS?

Nej. Även om uppdateringen importeras till WSUS importeras inte uppdateringen till Configuration Manager-konsolen för distribution om den inte visas i listan över tillåtna. Du måste använda [tjänst anslutnings verktyget](../../core/servers/manage/use-the-service-connection-tool.md) för att importera service uppdateringar till Configuration Manager för att uppdatera listan över tillåtna.

### <a name="what-alternative-methods-do-i-have-to-deploy-surface-driver-and-firmware-updates"></a>Vilka alternativa metoder behöver jag för att distribuera uppdateringar för Surface-drivrutiner och inbyggd program vara?

Information om hur du distribuerar uppdateringar för Surface-drivrutiner och inbyggd program vara via alternativa kanaler finns i [Hantera uppdateringar av Surface-drivrutiner och inbyggd program vara](/surface/manage-surface-driver-and-firmware-updates). Om du vill ladda ned MSI-eller. exe-filen och sedan distribuera via traditionella program varu distributions kanaler, se [behålla den inbyggda program varan för den aktuella arbets ytan med Configuration Manager](/archive/blogs/thejoncallahan/keeping-surface-firmware-updated-with-configuration-manager).

## <a name="next-steps"></a>Nästa steg

Mer information om Surface-drivrutiner finns i följande artiklar:

- [Överväganden för Surface och System Center Configuration Manager](/surface/considerations-for-surface-and-system-center-configuration-manager#deploy-surface-app-with-configuration-manager)
- [Uppdaterings historik för yta](https://support.microsoft.com/help/4036283/surface-surface-update-history)
- [Ladda ned den senaste inbyggda program varan och driv rutinerna för Surface-enheter](/surface/manage-surface-driver-and-firmware-updates)