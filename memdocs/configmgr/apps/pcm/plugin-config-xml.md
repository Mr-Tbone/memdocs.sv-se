---
title: Konfigurations-XML för plugin
titleSuffix: Configuration Manager
description: Teknisk referens för XML-elementen i Package Conversion Manager-plugin-programmet.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 940cc075-4066-44d5-972a-927c0b0a1143
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: ced1cc1347167451d4efb789b40746ff849710ee
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709966"
---
# <a name="technical-reference-for-the-package-conversion-manager-plug-in-configuration-xml"></a>Teknisk referens för konfigurations-XML för Package Conversion Manager-plugin

*Gäller för: Configuration Manager (aktuell gren)*

<!--1357861-->

I den här artikeln beskrivs XML-elementen i Configuration Manager konfigurations filen (Microsoft. ConfigurationManagement. exe. config) som styr åtgärden för Package Conversion Manager-plugin-programmet. Mer information om hur du använder det här plugin-programmet finns i [så här använder du Package Conversion Manager-plugin-programmet](how-to-use-plug-in.md).



## <a name="xml-configuration-elements"></a>XML-konfigurations element

I följande tabell beskrivs XML-elementen i Configuration Manager konfigurations filen som relaterar till plugin-programmet Package Conversion Manager.

|Element  |Typ  |Beskrivning  |
|---------|---------|---------|
|**PcmPlugIn**|Sträng|Namnet på det skript eller den körbara fil som ska användas som Package Conversion Manager-plugin.|
|**PcmPlugInTimeoutMilliseconds**|Integer|Den maximala tiden, i millisekunder, för att vänta på plugin-skriptet eller den körbara filen för Package Conversion Manager för att slutföra bearbetningen av ett paket.|
|**PcmPluginExitCode**|Integer|Den förväntade slut koden från plugin-processen. Det här värdet anger lyckad. Alla andra koder betraktas som ett fel.|
|**ForceRequirementsExtraction**|Boolesk|Tillåt automatisk konvertering att använda samlings krav som är associerade med ett paket. Detta bör endast anges till sant när du arbetar med ett Package Conversion Manager-pluginprogram som har utformats för att fatta beslut om vilka krav som ska användas.|



## <a name="sample-configuration-xml"></a>Exempel på konfigurations-XML

Det här avsnittet innehåller ett exempel på XML-element för Package Conversion Manager-konfiguration i Configuration Manager konfigurations filen **Microsoft. ConfigurationManagement. exe. config**. Som standard är filen i följande sökväg:  
`C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.exe.config`

I exemplet finns elementen som är relaterade till paket konverterings hanteraren i följande element:`Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings`

``` XML
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
...
    </Microsoft.ConfigurationManagement.AdminConsole.Properties.Settings>
    <Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings>
      <setting name="DecisionVerbosity" serializeAs="String">
        <value>2</value>
      </setting>
      <setting name="PcmPlugIn" serializeAs="String">
        <value>pcmplugin.vbs</value>
      </setting>
      <setting name="PcmPlugInTimeoutMilliseconds" serializeAs="String">
        <value>10000</value>
      </setting>
      <setting name="PcmPluginExitCode" serializeAs="String">
        <value>0</value>
      </setting>
      <setting name="ForceRequirementsExtraction" serializeAs="String">
        <value>True</value >
      </setting>
    </Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings>
  </applicationSettings>
...
```

