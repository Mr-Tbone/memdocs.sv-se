---
title: Hantera uppdateringar
titleSuffix: Configuration Manager
description: Hantera uppdateringar som du distribuerar och skapar med System Center Updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: cd64994c-b426-4465-96cd-54b0edc2778d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d2cb1d1547c23357adbaa26e649e4e22a78e0f39
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717813"
---
# <a name="manage-software-updates-in-updates-publisher"></a>Hantera program uppdateringar i Updates Publisher

*Gäller för: System Center Updates Publisher*     

I System Center Updates Publisher använder du **arbets ytan uppdateringar** för att hantera program uppdateringar och paket som du har importerat till lagrings platsen.  

Hanterings uppgifter omfattar duplicering, redigering och förfaller eller återaktivering av uppdateringar och paket samt tilldelning av uppdateringar och paket till publikationer. Du kan också exportera anpassade kataloger för användning med andra Updates Publisher-installationer.

Så här hämtar du uppdateringar som du kan hantera:
-  [Lägg till en uppdaterings katalog](updates-publisher-catalogs.md#add-software-update-catalogs) i installationen av Updates Publisher
-  [Importera](updates-publisher-catalogs.md#import-updates) uppdateringarna från katalogen till din lagrings plats.

Du kan också [skapa egna uppdateringar](create-updates-with-updates-publisher.md).



## <a name="create-a-duplicate-of-an-update"></a>Skapa en dubblett av en uppdatering
Du kan skapa dubbletter eller kopior av uppdateringar i din lagrings plats. Sedan kan du ändra kopian i stället för att ändra den ursprungliga uppdateringen. Du kan inte skapa kopior av uppdaterings paket.

Om du vill skapa en kopia väljer du en uppdatering i **arbets ytan uppdateringar**och väljer sedan **duplicera**. Kopian av uppdateringen visas på samma plats i arbets ytan uppdateringar med en *kopia av* till dess namn.

En ny kopia som du skapar har statusen inte **längre**, men behåller annars inställningarna för originalet.

## <a name="edit-updates-and-bundles"></a>Redigera uppdateringar och paket
Du kan välja uppdateringar och paket som finns i lagrings platsen för att ändra dem.

I **arbets ytan uppdateringar** väljer du en uppdatering eller paket och väljer sedan **Redigera** på fliken **Start** för att öppna redigerings guiden. Uppdateringarna och buntarna har separata men nära relaterade guider som visar samma alternativ som guiden [skapa uppdatering](create-updates-with-updates-publisher.md#use-the-create-update-wizard) eller [skapa paket](create-updates-with-updates-publisher.md#use-the-create-bundle-wizard) .

När du redigerar kan du ändra tillgänglig information om uppdateringen eller paketet så att den kan användas i din miljö. Du kan till exempel redigera tillämplighets reglerna eller prioritets reglerna eller ändra språket. Du kan också ändra produkten och leverantören för att flytta uppdateringen eller paketet till en anpassad mapp för att gruppera uppdateringar för eget bruk.

## <a name="assign-updates-and-bundles-to-a-publication"></a>Tilldela uppdateringar och paket till en publikation
Du kan välja uppdateringar och paket på **arbets ytan uppdateringar** och sedan välja **tilldela** från fliken **Start** i menyfliksområdet för att lägga till dem i en publikation. Då startas guiden **tilldela program uppdateringar** .
-  Se [publicera uppdateringar och paket](#publish-updates-and-bundles-from-the-updates-workspace) för information om hur du väljer och publicerar uppdateringar och paket som en enskild uppgift.
-  Se [Hantera publikationer](updates-publisher-publications.md) för information om hur du hanterar grupper med uppdateringar och paket som ett enda objekt. När du har tilldelat uppdateringar av en publikation kan du hantera den publikationen, som i sin tur innehåller alla tilldelade uppdateringar.

När du tilldelar uppdateringar till en publikation:

-   Du kan ta med inaktuella och icke-utgångna uppdateringar och paket i samma publikation.

-   Ange typ av publikation:

    -   **Fullständigt innehåll** – detta publicerar hela innehållet i uppdateringen till WSUS-servern. Detta inkluderar metadata och binärfilerna för uppdateringen.

    -   **Endast metadata** – detta publicerar endast metadata. uppdaterings-binärfiler publiceras inte. Du kan välja det här alternativet om du vill samla in efterlevnadsprinciper.

    -   **Automatiskt** – det här läget är bara tillgängligt när du har anslutit Updates Publisher till Configuration Manager (se [Server](updates-publisher-options.md#configmgr-server) alternativet för ConfigMgr.)

    Med den här typen uppdaterar Publisher frågor Configuration Manager för att avgöra om uppdateringarna eller paketen ska publiceras med fullständigt innehåll eller endast metadata. Fullständig innehåll för en uppdatering publiceras bara när uppdateringen uppfyller de **begärda tröskelvärdena för antal klienter** och **paketets käll storlek,** som anges på sidan **ConfigMgr-Server** i alternativ för Updates Publisher.

-   Välj en publikation:

    -   Använd **tilldela program uppdatering till befintliga publikationer** när du redan har skapat en publikation som du vill använda. Det här alternativet är inte tillgängligt förrän det finns minst en publikation.

    -   Använd **tilldela program uppdatering till en ny publikation** när du inte har en lämplig publikation. Då skapas en ny publikation med det namn som du anger.

När du har tilldelat uppdateringar av en publikation kan du använda **arbets ytan** publicera för att [publicera](updates-publisher-publications.md#publish-publications) eller [Exportera](updates-publisher-publications.md#export-a-publication) publikationen som en grupp.

## <a name="publish-updates-and-bundles-from-the-updates-workspace"></a>Publicera uppdateringar och paket från arbets ytan uppdateringar
När du publicerar uppdateringar och paket lägger uppdaterings utgivare till information om dessa uppdateringar och paket (metadata) och eventuellt binärfiler för uppdateringarna (fullständigt innehåll) till en uppdaterings Server för distribution till enheter.

Innan du kan publicera måste du konfigurera alternativet [uppdaterings Server](updates-publisher-options.md#update-server) för Updates Publisher. För att öppna det här konfigurations alternativet går du till **Översikt över** **uppdateringar arbets yta** &gt; och väljer **Konfigurera WSUS och signerings certifikat.** Du kan också gå till sidan uppdaterings server i Updates Publisher-alternativ.

Det finns två sätt att publicera uppdateringar och paket:
-   Direkt från arbets ytan uppdateringar. (Se följande procedur *för att publicera uppdateringar och paket*.)
-   Som en [publikation](updates-publisher-publications.md#publish-publications) från arbets ytan publikationer.  

> [!NOTE]   
> Updates Publisher kan bara publicera uppdateringar som är 375 megabyte (MB) eller mindre i storlek.

### <a name="to-publish-updates-and-bundles"></a>Publicera uppdateringar och paket
1.  Gå till **arbets ytan uppdateringar** och välj en eller flera uppdateringar och paket som du vill publicera. Välj sedan **publicera** från fliken **Start** i menyfliksområdet.

2.  På sidan **Välj** i **publicerings** guiden väljer du hur du vill publicera uppdateringarna. Alternativen är desamma som för att [tilldela uppdateringar](#assign-updates-and-bundles-to-a-publication): **fullständigt innehåll**, **endast metadata**eller **automatiskt**.

    Du kan också välja att signera alla uppdateringar med ett nytt publicerings certifikat.

3.  Slutför guiden.

Om publiceringen Miss lyckas visas en länk till filen UpdatesPublisher. log som kan innehålla mer information.

## <a name="export-updates"></a>Exportera uppdateringar
Du kan exportera uppdateringar och paket från din Updates Publisher-lagringsplats för att skapa en anpassad uppdaterings katalog. Sedan kan du [lägga till](updates-publisher-catalogs.md#add-software-update-catalogs) och [Importera](updates-publisher-catalogs.md#import-updates) katalogen till en annan instans av Updates Publisher. (Du kan också [Exportera uppdateringar som en publikation](updates-publisher-publications.md#export-a-publication).)

Om du vill exportera direkt går du till **arbets ytan** > uppdateringar**alla program uppdateringar** och väljer en eller flera uppdateringar och paket. Du kan inte exportera en leverantör eller en produkt-mapp, men du kan välja en mapp och sedan välja uppdateringarna i den mappen för export.

När du har valt en eller flera uppdateringar väljer du **Exportera** på fliken **Start** i menyfliksområdet och anger sedan en sökväg och ett fil namn för katalog exporten.

Du kan välja att exportera (inkludera) beroende program uppdateringar.

## <a name="delete-updates-and-bundles"></a>Ta bort uppdateringar och paket
Du kan ta bort uppdateringar och paket med uppdateringar och ta bort dem från Updates Publisher-lagringsplatsen.

Gå till **arbets ytan** > uppdateringar**alla program uppdateringar** och välj en eller flera enskilda uppdateringar. Välj sedan **ta bort** på fliken **Start** i menyfliksområdet.

-   Om ditt val bara innehåller uppdateringar eller paket som inte har publicerats eller som har upphört att gälla, uppmanas du att bekräfta borttagningen innan de tas bort.

-   Om ditt val innehåller en uppdatering eller paket som har publicerats och ännu inte har gått ut, får du en varning. Du bör [upphöra](updates-publisher-publications.md#expire-or-reactivate-updates-and-bundles) med uppdateringarna och sedan publicera den ändringen innan du tar bort dem från lagrings platsen.  

Om du tar bort en uppdatering eller paket från en leverantör och sedan importerar katalogen igen, återställs den uppdateringen till din lagrings plats.

## <a name="manage-vendor-and-product-folders"></a>Hantera leverantörs-och produkt mappar
Om du vill visa en lista över leverantörer och produkter för varje leverantör för vilken du har importerat eller skapat uppdateringar går du till **arbets ytan** > uppdateringar**Översikt över** > **alla program uppdateringar**.

Mappar för leverantörer och produkter skapas automatiskt av Updates Publisher när du använder en guide för att importera eller skapa en program uppdatering eller paket. Du kan också skapa de här mapparna manuellt.

-   Om du vill skapa en leverantörs katalog högerklickar du på **alla program uppdateringar**i navigerings fönstret i **arbets ytan uppdateringar**och väljer sedan **skapa leverantör**.

-   Om du vill skapa en produkt-mapp under en leverantörs-mapp högerklickar du på mappen leverantör och väljer **skapa produkt**.

Förutom att skapa mappar kan du byta namn på eller ta bort en leverantör eller en produkt-mapp i din lagrings plats. Det gör du genom att högerklicka på mappen och välja det alternativ som du vill använda, **byta namn på** eller **ta bort**. Om du tar bort en mapp tas alla uppdateringar och paket i mappen och dess produktattribut bort från utgivarens uppdaterings plats.

Du kan flytta uppdateringar mellan leverantörs-och produkt kataloger, inklusive mappar som du skapar. Om du vill flytta en uppdatering eller paket till en ny mapp måste du markera och **Redigera** uppdateringen eller paketet. På sidan **information** i guiden Redigera uppdatering kan du sedan omtilldela leverantören och produkten. När guiden **Redigera uppdatering** slutförs, gäller ändringen och uppdateringen flyttas till den nya mappen.

## <a name="view-the-xml-of-an-update-or-bundle"></a>Visa XML för en uppdatering eller paket
Du kan välja en enskild uppdatering eller paket på **arbets ytan uppdateringar** och sedan välja **Visa** XML för att visa XML-strukturen för uppdateringen. Det finns inga alternativ för att redigera XML-strukturen direkt.
