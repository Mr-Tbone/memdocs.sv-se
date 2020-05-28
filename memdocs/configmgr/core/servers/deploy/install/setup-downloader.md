---
title: Verktyget för konfigurations hämtare
titleSuffix: Configuration Manager
description: Använd det fristående verktyget för att ladda ned aktuella versioner av nyckel installationsfilerna för installationen.
ms.date: 05/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bda87fc5-2e4c-4992-98a4-01770365038c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2da8aed5cfe4a478010165445094f1fce4627d9a
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428840"
---
# <a name="setup-downloader-for-configuration-manager"></a>Installations hämtaren för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Innan du kör Configuration Manager installations programmet för att installera eller uppgradera en plats kan du använda det fristående verktyget för installations hämtaren för att hämta uppdaterade installationsfiler. Kör verktyget från den version av Configuration Manager som du vill installera. Använd uppdaterade installationsfiler för att kontrol lera att plats installationen använder aktuella versioner av nyckel installations filer.

När du använder installations hämtaren anger du en mapp som innehåller filerna. Det konto som du använder för att köra verktyget måste ha **fullständig** behörighet till download-mappen. När du kör installations programmet för att installera eller uppgradera en plats kan du ange den här lokala kopian av filer som du tidigare har laddat ned. Det här beteendet förhindrar att installations programmet ansluter till Microsoft när du startar plats installationen eller uppgraderingen. Du kan använda samma lokala kopia av installationsfilerna för andra plats installationer eller uppgraderingar av samma version.

Installations hämtaren hämtar följande typer av filer:

- Nödvändiga omdistribuerbara filer som krävs
- Språkpaket
- De senaste produkt uppdateringarna för installation

Det finns två alternativ för att köra installations hämtaren:

- Kör programmet med användar gränssnittet
- Kör programmet i en kommando tolk för ytterligare kommando rads alternativ

Om din organisation begränsar nätverkskommunikation med Internet med hjälp av en brand vägg eller proxyserver, måste du tillåta att verktyget får åtkomst till Internet-slutpunkter. Enheten där du ska köra verktyget kräver Internet åtkomst på samma sätt som tjänst anslutnings punkten. Mer information finns i [krav för Internet åtkomst](../../../plan-design/network/internet-endpoints.md#bkmk_scp).<!-- SCCMDocs#677 -->

## <a name="run-setup-downloader-with-the-user-interface"></a><a name="bkmk_ui"></a>Kör installations hämtaren med användar gränssnittet

1. På en dator som har Internet åtkomst bläddrar du till installations mediet för den version av Configuration Manager som du vill installera.

1. I undermappen **SMSSETUP\BIN\X64** kör du **setupdl. exe**.

1. Ange sökvägen till mappen där du vill lagra de uppdaterade installationsfilerna och välj sedan **Hämta**. Installations hämtaren verifierar de filer som för närvarande finns i download-mappen. Den hämtar bara filer som saknas eller som är nyare än befintliga filer. Den skapar undermappar för nedladdade språk och andra nödvändiga komponenter.

1. Information om hämtnings resultaten finns i **C:\ConfigMgrSetup.log**.

## <a name="run-setup-downloader-from-a-command-prompt"></a><a name="bkmk_cmd"></a>Kör installations hämtaren från en kommando tolk

1. Öppna en kommando tolk och ändra katalogen till installations mediet för den version av Configuration Manager som du vill installera.

1. Ändra katalogen till undermappen **SMSSETUP\BIN\X64** och kör **setupdl. exe** med de nödvändiga alternativen.

1. Information om hämtnings resultaten finns i **C:\ConfigMgrSetup.log**.

### <a name="command-line-options"></a>Kommandoradsalternativ

Du kan använda följande kommando rads alternativ med **setupdl. exe**:

- **/Verify**: verifiera filerna i download-mappen, som innehåller språkfiler. För en lista över inaktuella filer, granska **C:\ConfigMgrSetup.log**. När du använder det här alternativet hämtas inga filer.

- **/VERIFYLANG**: kontrol lera bara språkfilerna i download-mappen. För en lista över inaktuella språkfiler, granska **C:\ConfigMgrSetup.log**.

- **/Lang**: Hämta bara språkfilerna till download-mappen.

- **/NOUI**: starta installations hämtaren utan användar gränssnittet. När du använder det här alternativet krävs **hämtnings Sök vägen** .

- **Hämtnings Sök väg**: om du vill starta verifierings-eller hämtnings processen automatiskt anger du sökvägen till download-mappen. När du använder alternativet **/NOUI** , krävs hämtnings Sök vägen. Om du inte anger en hämtnings Sök väg uppmanas du att ange sökvägen med installations hämtaren. Om mappen inte finns skapas den av installations hämtaren.

### <a name="example-commands"></a>Exempelkommandon

#### <a name="example-1"></a>Exempel 1

Installations hämtaren verifierar filerna i den angivna download-mappen och laddar ned filer.

`setupdl.exe C:\Download`

#### <a name="example-2"></a>Exempel 2

Installations hämtaren verifierar bara filerna i den angivna download-mappen.

`setupdl.exe /VERIFY C:\Download`

#### <a name="example-3"></a>Exempel 3

Installations hämtaren verifierar filerna i den angivna download-mappen och laddar ned filer. Verktyget visar inte något användar gränssnitt.

`setupdl.exe /NOUI C:\Download`

#### <a name="example-4"></a>Exempel 4

Installations hämtaren verifierar språkfilerna i den angivna download-mappen och hämtar sedan bara språkfilerna.

`setupdl.exe /LANG C:\Download`

## <a name="copy-setup-downloader-files-to-another-computer"></a><a name="bkmk_cp-files"></a>Kopiera installations hämta filer till en annan dator

1. I Utforskaren går du till någon av följande platser:

    - **&lt;Configuration Manager installationsmedia> \SMSSETUP\BIN\X64**

    - **&lt;Configuration Manager installations Sök väg> \BIN\X64**

1. Kopiera följande filer till samma målmapp på den andra datorn:

    - **setupdl. exe**

    - **.\\&lt; språk > \\ setupdlres. dll**

        > [!NOTE]
        > Den här filen finns i undermappen för installations språket. Till exempel är engelska i `00000409` undermappen.

    Målmapparna på enheten bör se ut som i följande exempel:

    - `C:\ConfigManInstall\setupdl.exe`

    - `C:\ConfigManInstall\00000409\setupdlres.dll`

1. Kör installations hämtaren från mål datorn. Använd antingen [användar gränssnittet](#bkmk_ui) eller [kommando tolken](#bkmk_cmd).
