---
title: Installera konsol
titleSuffix: Configuration Manager
description: Installera Configuration Manager-konsolen för att ansluta till en central administrations plats eller en primär plats.
ms.date: 04/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d39c201f-d364-4e7b-bde4-faa76d747f33
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f5fda03090f7ec69eb78b20385dfc009bac88f40
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718240"
---
# <a name="install-the-configuration-manager-console"></a>Installera Configuration Manager-konsolen

*Gäller för: Configuration Manager (aktuell gren)*

Administratörer använder Configuration Manager-konsolen för att hantera Configuration Managers miljön. Varje Configuration Manager-konsol kan ansluta till en central administrations plats (ca) eller till en primär plats. Du kan inte ansluta en Configuration Manager-konsol till en sekundär plats.

Configuration Manager-konsolen installeras alltid på plats servern för certifikat utfärdarna eller en primär plats. Installera-konsolen separat från plats Server installationen genom att köra det fristående installations programmet.  



## <a name="prerequisites"></a>Krav

- Du har lokal **Administratörs** behörighet på mål datorn för-konsolen.  

- Du har **Läs** behörighet till platsen för Configuration Manager-konsolens installationsfiler.  



## <a name="source-paths"></a>Käll Sök vägar

Bestäm vilken käll Sök väg som ska användas:  

- ConsoleSetup-mapp på plats servern:`<Configuration Manager site server installation path>\Tools\ConsoleSetup`  

    När du installerar en plats Server kopieras-konsolens installationsfiler och språk paket som stöds för platsen till undermappen **Tools\ConsoleSetup** . Du kan också kopiera mappen **ConsoleSetup** till en annan plats för att starta installationen. När du uppdaterar platsen behåller den alltid den lokala versionen som är uppdaterad.  

- Configuration Manager installations medium:`<Configuration Manager installation media>\SMSSETUP\BIN\I386`  

    Om du installerar Configuration Manager-konsolen från installations mediet installeras alltid den engelska versionen. Det här beteendet inträffar även om plats servern har stöd för olika språk, eller om mål datorns operativ system är inställt på ett annat språk.  

När det är möjligt kan du starta-konsol installations programmet från **ConsoleSetup** -mappen i stället för från käll mediet.

> [!Important]  
> Installera inte-konsolen med **CD: n. Senaste** källfilerna. Det är ett scenario som inte stöds och kan orsaka problem med konsol installationen. Mer information finns [på CD-skivan. Senaste mappen](../../manage/the-cd.latest-folder.md#unsupported-scenarios).<!-- SCCMDocs issue 1359 -->  

Om du skapar ett paket för att installera-konsolen på andra datorer måste du kontrol lera att paketet innehåller följande filer:<!--3612513-->

- ConsoleSetup. exe
- AdminConsole. msi
- ConfigMgr. AC_Extension. i386. cab (från och med version 1902)
- ConfigMgr. AC_Extension. amd64. cab (från och med version 1902)



## <a name="use-the-setup-wizard"></a>Använd installationsguiden  

1. Bläddra till käll Sök vägen och öppna **ConsoleSetup. exe**.  

    > [!IMPORTANT]  
    > Installera alltid-konsolen genom att använda **ConsoleSetup. exe**. Även om du kan installera Configuration Manager-konsolen genom att köra AdminConsole. msi, kör inte den här metoden nödvändiga komponenter eller beroende kontroller. Installationen kanske inte kan installeras på rätt sätt.  

2. I guiden väljer du **Nästa**.  

3. På sidan **plats Server** anger du det fullständigt kvalificerade domän namnet (FQDN) för den plats server som Configuration Manager-konsolen ansluter till.  

4. På sidan **installationsmapp** anger du installationsmappen för Configuration Manager-konsolen. Mappsökvägen får inte innehålla avslutande blank steg eller Unicode-tecken.  

5. På sidan **Customer Experience Improvement Program** väljer du om du vill ansluta till Customer Experience IMPROVEMENT program (CEIP).  

    > [!Note]  
    > Med början i Configuration Manager version 1802 tas CEIP-funktionen bort från produkten.

6. På sidan **klar att installera** väljer du **Installera**.  



## <a name="install-from-a-command-prompt"></a>Installera från en kommando tolk  

> [!TIP]  
> Om du installerar Configuration Manager-konsolen från en kommando tolk installeras alltid den engelska versionen. Det här beteendet inträffar även om mål datorns operativ system är inställt på ett annat språk. Om du vill installera Configuration Manager-konsolen på ett annat språk än engelska [använder du installations guiden](#use-the-setup-wizard).  


### <a name="consolesetupexe-command-line-options"></a>Kommando rads alternativ för ConsoleSetup. exe

#### <a name="q"></a>/q

Installerar Configuration Managers konsolen obevakad. Alternativen **EnableSQM**, **TargetDir**och **DefaultSiteServerName** krävs när du använder det här alternativet.

#### <a name="uninstall"></a>/uninstall

Avinstallerar Configuration Manager-konsolen. Ange det här alternativet först när du använder det med alternativet **/q** .

#### <a name="langpackdir"></a>LangPackDir

Anger sökvägen till den mapp som innehåller språkfilerna. Du kan hämta språkfilerna med **installations hämtaren** . Om du inte använder det här alternativet söker installations programmet efter mappen språk i den aktuella mappen. Om språkmappen inte hittas, fortsätter installations programmet att installera enbart engelska. Mer information finns i [installations hämtaren](setup-downloader.md).

#### <a name="targetdir"></a>TargetDir

Anger installationsmappen för att installera Configuration Manager-konsolen. Det här alternativet krävs när du använder alternativet **/q** .

#### <a name="enablesqm"></a>EnableSQM

Anger om Customer Experience Improvement Program (CEIP) ska anslutas. Använd värdet **1** om du vill delta i CEIP och värdet **0** om du inte vill delta i programmet. Det här alternativet krävs när du använder alternativet **/q** .

> [!Important]  
> Med början i Configuration Manager version 1802 tas CEIP-funktionen bort från produkten. Om du använder parametern kommer installationen att Miss förorsakas.

#### <a name="defaultsiteservername"></a>DefaultSiteServerName

Anger det fullständiga domän namnet för den plats server som konsolen ansluter till när den öppnas. Det här alternativet krävs när du använder alternativet **/q** .


### <a name="examples"></a>Exempel

> [!Important]  
> För version 1802 och senare ska du inte inkludera parametern **EnableSQM**

#### <a name="silent-install"></a>Tyst installation

`ConsoleSetup.exe /q TargetDir="%ProgramFiles%\ConfigMgr Console" DefaultSiteServerName=MyServer.Contoso.com`

#### <a name="silent-install-with-language-packs"></a>Tyst installation med språk paket

`ConsoleSetup.exe /q TargetDir="C:\Program Files\ConfigMgr Console" DefaultSiteServerName=MyServer.Contoso.com LangPackDir=C:\Downloads\ConfigMgr`  

#### <a name="silent-uninstall"></a>Tyst avinstallation

`ConsoleSetup.exe /uninstall /q`  



## <a name="see-also"></a>Se även

En administratör ser objekt i-konsolen baserat på de behörigheter som tilldelats användar kontot. Mer information finns i [grunderna i rollbaserad administration](../../../understand/fundamentals-of-role-based-administration.md).

Mer information om grunderna i hur du navigerar i Configuration Manager-konsolen finns i [använda-konsolen](../../manage/admin-console.md).
