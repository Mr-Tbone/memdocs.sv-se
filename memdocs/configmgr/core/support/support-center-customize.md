---
title: Anpassa Support Center
titleSuffix: Configuration Manager
description: Anpassa konfigurations filen för Support Center.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a6f7f6b7-9ef3-4ffa-a3cf-d877ac55983b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: fc17437e508ea69a19043c29bf9ad4501cbac3e4
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078523"
---
# <a name="customize-support-center"></a>Anpassa Support Center

*Gäller för: Configuration Manager (aktuell gren)*

[Support Center](support-center.md) -verktyget innehåller en konfigurations fil som du kan anpassa. Som standard är filen i följande sökväg när du installerar Support Center: `C:\Program Files (x86)\Configuration Manager Support Center\ConfigMgrSupportCenter.exe.config`. Konfigurations filen ändrar programmets beteende:

- [Anpassa data insamling](#bkmk_datacoll): redigera uppsättningar med register nycklar och WMI-namnområden som ingår under data insamlingen  

- [Anpassa logg grupper](#bkmk_loggroups): definiera nya grupper med loggfiler med hjälp av reguljära uttryck. Lägg också till andra loggfiler i logg grupper.  

- [Samla in ytterligare loggfiler med jokertecken](#bkmk_wildcards): Använd jokertecken sökning för att samla in ytterligare loggfiler  

Om du vill göra dessa ändringar måste du ha lokal administratörs behörighet på klienten där du har installerat Support Center. Gör dessa anpassningar med hjälp av en text-eller XML-redigerare, till exempel anteckningar eller Visual Studio.

> [!Important]  
> Konfigurations filen för Support Center är en XML-formaterad fil. Det är viktigt för att Support Center ska fungera. Att ändra den här filen rekommenderas endast för användare som är bekanta med XML och reguljära uttryck.  

Innan du anpassar konfigurations filen för Support Center sparar du en säkerhets kopia av originalet. Med den här säkerhets kopian kan du återställa de ursprungliga Support Center-funktionerna om du gör fel när du redigerar filen. Om du inte skapar någon säkerhets kopia och Support Center inte fungerar korrekt när du har ändrat konfigurations filen, installerar du om Support Center. Du kan också kopiera en konfigurations fil från en annan installation av Support Center.



## <a name="customize-data-collection"></a><a name="bkmk_datacoll"></a>Anpassa data insamling

Om du vill anpassa data insamlingen på klienten ändrar du konfigurations filen för Support Center med hjälp av XML `<dataCollectorSettings>` -element som finns i elementet.


### <a name="wmi-data-collection"></a>Insamling av WMI-data

`<CcmWmiDataCollector>` Elementet innehåller ett `<collectionScopes>` -element. Använd det här elementet för att ändra WMI-namnrymder från vilka Support Center samlar in data. Det innehåller också ett `<ignoreScopes>` -element. Använd det här elementet för att filtrera bort data mängden från delar av de namn områden som definierats `<collectionScopes>` i elementet.  
    
#### <a name="example"></a>Exempel
Standard konfigurations filen samlar in data från `root\ccm` namn området. Den innehåller den här sökvägen i `<add/>` ett- `<collectionScopes>`element i. 

Dessutom ignoreras allting `\cimodels`under, `\invagt` `\events`, och `\policy` för det här namn området. Den innehåller dessa sökvägar `<add/>` i element som `<ignoreScopes>`finns i.

```XML
<CcmWmiDataCollector>
  <collectionScopes>
    <!-- Collect these namespaces (ignoring the sub-scopes in the ignoreScopes block) -->
    <add key="root\ccm"/>
    <add key="root\cimv2\sms"/>
  </collectionScopes>
  <ignoreScopes>
    <!-- Collecting these namespaces is known to be problematic/unnecessary -->
    <add key="root\ccm\cimodels"/>
    <add key="root\ccm\invagt"/>
    <add key="root\ccm\events"/>
    <!-- Do not collect policy, there's already a separate policy collector.-->
    <add key="root\ccm\policy"/>
  </ignoreScopes>
</CcmWmiDataCollector>
```


### <a name="registry-data-collection"></a>Insamling av register data

`<RegistryDataCollector>` Elementet innehåller ett `<registryKeys>` -element. Använd det här elementet för att ändra register nycklar och under nycklar som stöder Center samlar in under `HKEY_LOCAL_MACHINE` sökvägen. Support Center stöder inte insamling av register data från andra rot register Sök vägar.

#### <a name="example"></a>Exempel
Om du vill samla in register nycklar för de klassiska program som är installerade på enheten `<add/>` lägger du till `<registryKeys>` följande-element i-elementet:`<add key="software\\microsoft\\windows\\currentversion\\uninstall"/>`

```XML
<RegistryDataCollector>
  <registryKeys>
    <!-- Registry keys (and all subkeys) to collect -->
    <add key="software\\microsoft\\ccm"/>
    <add key="software\\microsoft\\sms"/>
    <add key="software\\microsoft\\ccmsetup"/>
    <add key="software\\microsoft\\windows\\currentversion\\uninstall"/>
  </registryKeys>
</RegistryDataCollector>
```



## <a name="customize-log-file-groups"></a><a name="bkmk_loggroups"></a>Anpassa logg fils grupper

Om du vill anpassa vilka loggfiler som Support Center samlar in och hur de presenteras i listan **logg grupper** , använder du element i `<logGroups>` elementet. När du startar Support Center genomsöks det här avsnittet i konfigurations filen. Sedan skapas en grupp i listan över **logg grupper** för varje unikt nyckel värde som finns i `<add/>` elementen i `<logGroups>` elementet.

- **Komponent logg grupp**: `<componentLogGroup>` elementet använder ett nyckelattribut för att definiera namnet på den logg grupp som visas i listan. Det använder också ett Value-attribut som innehåller ett vanligt uttryck (regex). Detta regex används för att samla in en uppsättning relaterade loggfiler.  

- **Statisk logg grupp:** `<staticLogGroup>` Elementet använder ett nyckelattribut för att definiera namnet på den logg grupp som visas i listan. Det använder också ett Value-attribut som definierar ett logg fil namn.  

Om samma nyckel-attributvärde används i ett `<add/>` -element i både `<componentLogGroup>` elementet och- `<staticLogGroup>` elementet skapar Support Center en enda grupp. Den här gruppen innehåller de loggfiler som definieras av båda elementen som använder samma nyckel.

#### <a name="example"></a>Exempel
```XML
<logGroups>
  <componentLogGroup>
    <add key="Application Management" value="^(app.*|ci.*|contentaccess|contenttransfermanager|datatransferservice|dcm.*|execmgr.*|UserAffinity.*|.*Handler$|.*Provider$)"/>
    <add key="Client Registration" value="^(clientregistration|locationservices|ccmmessaging|ccmexec)"/>
    <add key="Inventory" value="^(ccmmessaging|inventoryagent|mtrmgr|swmtrreportgen|virtualapp|mtr.*|filesystemfile)"/>
    <add key="Policy" value="^(ccmmessaging|policyagent_.*|policyevaluator_.*)"/>
    <add key="Software Updates" value="^(ci.*|contentaccess|contenttransfermanager|datatransferservice|dcm.*|update.*|wuahandler|xmlstore|scanagent)"/>
    <add key="Software Distribution" value="^(datatransferservice|execmgr.*|contenttransfermanager|locationservices|contentaccess|filebits)"/>
    <add key="Desired Configuration Management" value="^(ci.*|dcm.*)"/>
    <add key="Operating System Deployment" value="^(ts.*)"/>
  </componentLogGroup>
  <staticLogGroup>
    <add key="Application Management" value="ccmsdkprovider.log"/>
    <add key="Desired Configuration Management" value="ccmsdkprovider.log"/>
    <add key="Software Updates" value="ccmsdkprovider.log"/>
  </staticLogGroup>
</logGroups>
```



## <a name="collecting-additional-log-files-using-wildcards"></a><a name="bkmk_wildcards"></a>Samla in ytterligare loggfiler med jokertecken

Om du vill samla in ytterligare loggfiler använder du jokertecken i fil Sök vägen eller fil namnet. Dessa jokertecken innehåller systemomfattande miljövariabler som `%WINDIR%`, men undantar miljövariabler från användare och till exempel. `%USERPROFILE%` Om du vill samla in ytterligare loggfiler med hjälp av denna sökning efter rekursiv logg fils `<add/>` ökning använder du `<additionalLogFiles>` ett-element i-elementet. 

Följande exempel visar hur Support Center använder den här funktionen i standard konfigurations filen.

#### <a name="example-1-collect-all-windows-update-log-files-in-the-windows-directory"></a>Exempel 1: samla in alla Windows Update loggfiler i Windows-katalogen
Följande element samlar in en fil med namnet `WindowsUpdate.log` som finns i Windows-katalogen: 

`<add key="%WINDIR%\WindowsUpdate.log" />`

#### <a name="example-2-collect-all-log-files-in-the-windows-logs-directory"></a>Exempel 2: samla in alla loggfiler i katalogen Windows-loggar
Följande element samlar in alla filer som slutar i `.log` som finns i Windows logs-katalogen: 

`<add key="%WINDIR%\logs\*.log" />`

#### <a name="full-example-xml"></a>Fullständigt exempel-XML
```XML
<CcmLogDataCollector>
  <additionalLogFiles>
    <!-- Collect these additional log files. Can pass in a wildcard for the filename. System variables are also supported. -->
    <!--
    <add key="%WINDIR%\WindowsUpdate.log" />
    <add key="%WINDIR%\logs\*.log" />
    -->
  </additionalLogFiles>
</CcmLogDataCollector>
```
