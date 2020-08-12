---
title: Etableringsläge
titleSuffix: Configuration Manager
description: Lär dig mer om klient etablerings läget under Configuration Manager aktivitetssekvens.
ms.date: 05/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: troubleshooting
ms.assetid: 3e3ff3a4-7a75-41bb-bdf9-33ede9c0e3a3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b0039648c6f444efdbbaeb16f55d29b630ee7f16
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124278"
---
# <a name="provisioning-mode"></a>Etableringsläge

*Gäller för: Configuration Manager (aktuell gren)*

Under en aktivitetssekvens för operativ system distribution placerar Configuration Manager klienten i etablerings läge. (En aktivitetssekvens för operativ Systems distribution omfattar uppgradering på plats till Windows 10.) I det här läget bearbetar klienten inte principen från platsen. Med det här beteendet kan aktivitetssekvensen köras utan risk för ytterligare distributioner som körs på klienten. När aktivitetssekvensen slutförs, antingen slutförs eller hanteras, avslutas klient etablerings läget.

Om aktivitetssekvensen Miss lyckas kan klienten lämna i etablerings läge. Om enheten till exempel startas om i mitten av bearbetningen av aktivitetssekvensen och det inte går att återställa. En administratör måste identifiera och åtgärda klienter manuellt i det här läget.


## <a name="manually-remove-provisioning-mode"></a>Ta bort etablerings läget manuellt

Om en klient lämnas i etablerings läge använder du den här manuella processen för att returnera klienten till normal drift.

```PowerShell
Invoke-WmiMethod -Namespace root\CCM -Class SMS_Client -Name SetClientProvisioningMode -ArgumentList $false
```

> [!Important]  
> En av de ändringar som gjorts av den här WMI-metoden är att ange ett register värde, men det gör även andra ändringar. Att bara ändra registervärdet tar inte helt bort klienten från etablerings läget. Om du redigerar registret manuellt kan klienten uppvisa oväntade beteenden.  


## <a name="client-provisioning-mode-timeout"></a>Timeout för klient etablerings läge

Från och med version 1902 anger aktivitetssekvensen en tidsstämpel när klienten placeras i etablerings läge. Var 60: e minut kontrollerar en klient i etablerings läget varaktigheten för tiden sedan tidsstämpeln. Om den är i etablerings läge i mer än 48 timmar, avslutar klienten automatiskt etablerings läget och startar om processen.

48 timmar är standard tids gräns värdet för etablerings läge. Du kan justera den här timern på en enhet genom att ange värdet **ProvisioningMaxMinutes** i följande register nyckel: `HKLM\Software\Microsoft\CCM\CcmExec` . Om det här värdet inte finns eller är `0` , använder klienten standardvärdena 48 timmar.

Tidsstämpelns **ProvisioningEnabledTime** finns i följande register nyckel: `HKLM\Software\Microsoft\CCM\CcmExec` . Tidsstämpeln har värdet senaste gången datorn angav etablerings läge. Formatet är epok (Unix-tidsstämpel) och är i UTC.

Den här tidsstämpeln återställs också till den aktuella tiden när du placerar datorn i etablerings läge manuellt med hjälp av följande kommando:

```powershell
Invoke-WmiMethod -Namespace root\CCM -Class SMS_Client -Name SetClientProvisioningMode -ArgumentList $true
```

## <a name="process-flow-diagrams"></a>Process flödes diagram

Diagrammen visar process flödet för aktivitetssekvensen och klienten.

### <a name="task-sequence"></a>Aktivitetssekvens

Följande diagram visar hur aktivitetssekvensen ställer in etablerings läge:

![Flödes diagram för etablerings läge för aktivitetssekvens](media/3197824-ts-flow.png)

### <a name="client-remediation"></a>Klient reparation

Följande diagram visar hur klienten avslutar etablerings läget:

![Flödes diagram för klienten som avslutar etablerings läget](media/3197824-client-flow.png)


## <a name="see-also"></a>Se även

[Installera Windows och ConfigMgr](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr)

[Uppgradera operativsystem](task-sequence-steps.md#BKMK_UpgradeOS)
