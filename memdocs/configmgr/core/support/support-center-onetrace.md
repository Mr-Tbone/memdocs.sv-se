---
title: Support Center OneTrace (förhandsversion)
titleSuffix: Configuration Manager
description: OneTrace är ett nytt logg visnings program med Support Center som har förbättringar över CMTrace.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4cde43d1-9b09-4601-b389-0776de451b4e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 150090556d63b1bdf0b35dc9b53b450137d7f9d3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723112"
---
# <a name="support-center-onetrace-preview"></a>Support Center OneTrace (förhandsversion)

<!--3555962-->

Från och med version 1906 är OneTrace ett nytt logg visnings program med Support Center. Det fungerar ungefär som CMTrace, med följande förbättringar:

- En flikad vy
- Docknings bara Windows
- Förbättrade Sök funktioner
- Möjlighet att aktivera filter utan att lämna vyn logg
- Rullnings tips för att snabbt identifiera kluster av fel
- Snabb logg öppning för stora filer

[![Skärm bild av OneTrace logg visare](media/3555962-onetrace.png)](media/3555962-onetrace.png#lightbox)

OneTrace fungerar med många typer av loggfiler, till exempel:

- Configuration Manager klient loggar
- Configuration Manager Server loggar
- Statusmeddelanden
- Windows Update ETW-loggfil i Windows 10
- Windows Update logg filen på Windows 7 & Windows 8,1

## <a name="prerequisites"></a>Krav

- .NET Framework version 4,6 eller senare

## <a name="install"></a>Installera

OneTrace installeras med Support Center. Hitta installations programmet för Support Center på plats servern på följande sökväg: `cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi`.

Som standard installeras OneTrace-programmet på `C:\Program Files (x86)\Configuration Manager Support Center\CMPowerLogViewer.exe`.

> [!Note]  
> Support Center och OneTrace använder Windows Presentation Foundation (WPF). Den här komponenten är inte tillgänglig i Windows PE. Fortsätt att använda CMTrace i Start avbildningar med aktivitetssekvensdistribution.  

## <a name="log-groups"></a>Logg grupper

<!--5559993-->

Från och med version 2002 stöder OneTrace anpassningsbara logg grupper som liknar funktionen i Support Center. Med logg grupper kan du öppna alla loggfiler för ett enda scenario. OneTrace innehåller för närvarande grupper för följande scenarier:

- Programhantering
- Kompatibilitetsinställningar (kallas även för önskad konfigurations hantering)
- Programuppdateringar

Om du vill visa logg grupper går du till menyn **Visa** och väljer **logg grupper**.

![Skärm bild av OneTrace logg grupp för program hantering](media/5559993-onetrace-log-groups.png)

### <a name="customize-log-groups"></a>Anpassa logg grupper

Du kan anpassa dessa grupper genom att ändra konfigurations-XML, som som standard finns i följande sökväg `C:\Program Files (x86)\Configuration Manager Support Center\LogGroups.xml`:.

Följande exempel är en del av standard konfigurations filen:

``` XML
<LogGroups>
  <LogGroup Name="Desired Configuration Management" GroupType="1" GroupFilePath="">
    <LogFile>CIAgent.log</LogFile>
    <LogFile>CIDownloader.log</LogFile>
    <LogFile>CIStateStore.log</LogFile>
    <LogFile>CIStore.log</LogFile>
    <LogFile>CITaskMgr.log</LogFile>
    <LogFile>ccmsdkprovider.log</LogFile>
    <LogFile>DCMAgent.log</LogFile>
    <LogFile>DCMReporting.log</LogFile>
    <LogFile>DcmWmiProvider.log</LogFile>
  </LogGroup>
</LogGroups>
```

`GroupType` Egenskapen accepterar följande värden:

- `0`: Okänd eller annan
- `1`: Configuration Manager klient loggar
- `2`: Configuration Manager Server loggar

`GroupFilePath` Egenskapen kan innehålla en explicit sökväg för loggfilerna. Om det är tomt är OneTrace beroende av register konfigurationen för grupp typen. Om du t. ex. `GroupType=1`anger så kommer OneTrace automatiskt att söka `C:\Windows\CCM\Logs` efter loggarna i gruppen. I det här exemplet behöver du inte ange `GroupFilePath`.

## <a name="see-also"></a>Se även

- [Logg visaren för Support Center](support-center-ui-reference.md#bkmk_log-viewer)

- [CMTrace](cmtrace.md)
