---
title: Installationshämtare
titleSuffix: Configuration Manager
description: Läs mer om det här fristående programmet som är utformat för att se till att plats installationen använder aktuella versioner av nyckel installations filer.
ms.date: 01/22/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bda87fc5-2e4c-4992-98a4-01770365038c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2fa1899f8e7dc14812f9f9ecf889350a153b2d25
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718079"
---
# <a name="setup-downloader-for-configuration-manager"></a>Installations hämtaren för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Innan du kör installations programmet för att installera eller uppgradera en Configuration Manager plats kan du använda det fristående installations hämtande programmet från den version av Configuration Manager som du vill installera för att hämta uppdaterade installationsfiler.  

Om du använder uppdaterade installationsfiler ser du till att plats installationen använder aktuella versioner av nyckel installations filer. I Oveview:   
-   När du använder installations hämtaren för att ladda ned filer innan du startar installationen anger du en mapp som innehåller filerna.  
-   Det konto som du använder för att köra installations hämtaren måste ha **fullständig** behörighet till download-mappen.  
-   När du kör installations programmet för att installera eller uppgradera en plats kan du dirigera den till att använda den här lokala kopian av filer som du tidigare har laddat ned. Detta förhindrar att installations formuläret ansluter till Microsoft när du startar plats installationen eller uppgraderingen.  
-   Du kan använda samma lokala kopia av installationsfilerna för efterföljande plats installationer eller uppgraderingar.  

Följande typer av filer hämtas av installations hämtaren:  
-   Nödvändiga omdistribuerbara filer som krävs  
-   Språkpaket  
-   De senaste produkt uppdateringarna för installation  

Det finns två alternativ för att köra installations hämtaren:
- Kör programmet med användar gränssnittet
- För kommando rads alternativ kör du programmet i en kommando tolk


## <a name="run-setup-downloader-with-the-user-interface"></a><a name="bkmk_ui"></a>Kör installations hämtaren med användar gränssnittet  

1.  Öppna Utforskaren och gå till ** &lt;ConfigMgrInstallationMedia\>\SMSSETUP\BIN\X64**på en dator som har Internet åtkomst.  

2.  Öppna installations hämtaren genom att dubbelklicka på **setupdl. exe**.   

3. Ange sökvägen till den mapp som ska vara värd för de uppdaterade installationsfilerna och klicka sedan på **Hämta**. Installations hämtaren verifierar de filer som för närvarande finns i download-mappen. Den hämtar bara filer som saknas eller som är nyare än befintliga filer. Installations hämtaren skapar undermappar för nedladdade språk och andra nödvändiga undermappar.  

4.  Om du vill granska nedladdnings resultatet öppnar du filen **ConfigMgrSetup. log** i rot katalogen på enhet C.  .  

## <a name="run-setup-downloader-from-a-command-prompt"></a><a name="bkmk_cmd"></a>Kör installations hämtaren från en kommando tolk  

1.  I ett kommando tolks fönster går du till ** &lt; *Configuration Manager installations medie*\>\SMSSETUP\BIN\X64**.   

2.  Öppna installations hämtaren genom att köra **setupdl. exe**.

    Du kan använda följande kommando rads alternativ med **setupdl. exe**:   

    -   **/Verify**: Använd det här alternativet för att verifiera filerna i download-mappen, som innehåller språkfiler. Granska filen ConfigMgrSetup. log i rot katalogen på enhet C för en lista över filer som är inaktuella. Inga filer laddas ned när du använder det här alternativet.  

    -   **/VERIFYLANG**: Använd det här alternativet för att verifiera språkfilerna i download-mappen. Granska filen ConfigMgrSetup. log i rot katalogen på enhet C för en lista över språkfiler som är inaktuella.

    -   **/Lang**: Använd det här alternativet om du bara vill hämta språkfilerna till download-mappen.  

    -   **/NOUI**: Använd det här alternativet för att starta installations hämtaren utan att Visa användar gränssnittet. När du använder det här alternativet måste du ange **hämtnings Sök vägen** som en del av kommandot i kommando tolken.  

    -   DownloadPath: du kan ange sökvägen till download-mappen för att automatiskt starta verifierings-eller hämtnings processen. ** &lt;\>** Du måste ange hämtnings Sök vägen när du använder alternativet **/NOUI** . Om du inte anger en sökväg för hämtning måste du ange sökvägen när installations hämtaren öppnas. Installations hämtaren skapar mappen om den inte finns.  

    Exempel på kommandon:

    -   **setupdl &lt;DownloadPath\>**  

        -   Installations hämtaren startar, verifierar filerna i den angivna download-mappen och hämtar sedan bara de filer som saknas eller som har nyare versioner än befintliga filer.     

    -   **setupdl/VERIFY &lt;-DownloadPath\>**  

        -   Installations hämtaren startar och verifierar filerna i den angivna download-mappen.  

    -   **setupdl/NOUI &lt;-DownloadPath\>**  

        -   Installations hämtaren startar, verifierar filerna i den angivna download-mappen och hämtar sedan bara de filer som saknas eller som är nyare än de befintliga filerna.  

    -   **setupdl/LANG &lt;-DownloadPath\>**  

        -   Installations hämtaren startar, verifierar språkfilerna i den angivna download-mappen och hämtar sedan bara de språkfiler som saknas eller som är nyare än de befintliga filerna.  

    -   **setupdl/VERIFY**  

        -   Installations hämtaren startar och du måste ange sökvägen till download-mappen. Därefter verifierar installations hämtaren filerna i download-mappen när du har klickat på **Verifiera**.  

3.  Om du vill granska nedladdnings resultatet öppnar du filen **ConfigMgrSetup. log** i rot katalogen på enhet C.

## <a name="copy-setup-downloader-files-to-another-computer"></a><a name="bkmk_cp-files"></a>Kopiera installations hämta filer till en annan dator

1. I Utforskaren går du till någon av följande platser:

    - **&lt;Configuration Manager installationsmedia> \SMSSETUP\BIN\X64**
    - **&lt;Configuration Manager installations Sök väg> \BIN\X64**
    
1. Kopiera följande filer till samma målmapp på den andra datorn:
    
    - **setupdl. exe**
    - **. \\språk>\\setupdlres &lt;. dll**
      - Den här filen finns i undermappen för installations språket. Till exempel är engelska i `00000409` undermappen.

    Som exempel bör målmapparna på enheten se ut så här:
    - C:\ConfigManInstall\setupdl.exe
    - C:\ConfigManInstall\00000409\setupdlres.dll

1. Starta installations hämtaren från datorn med antingen [användar gränssnittet](#bkmk_ui) eller [kommando tolken](#bkmk_cmd), som beskrivs i avsnitten ovan.
