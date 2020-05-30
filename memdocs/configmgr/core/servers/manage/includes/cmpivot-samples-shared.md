---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 05/26/2020
ms.openlocfilehash: c450cff20df5dd45daa8097b8132f00d51bf713d
ms.sourcegitcommit: 0d2f6132428b5fa994e5b770ab1d2bf7d78ac179
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/30/2020
ms.locfileid: "84226694"
---
<!--This file is shared by the CMPivot script samples articles for both Microsoft Endpoint Manager tenant attach and Configuration Manager-->


## <a name="operating-system"></a>Operativsystem

Hämtar information om operativ system.

```kusto
// Sample query for OS information
OperatingSystem
```

## <a name="recently-used-applications"></a>Nyligen använda program

Följande fråga hämtar nyligen använda program (senaste 2 timmarna):

```kusto
CCMRecentlyUsedApplications
| where (LastUsedTime > ago(2h))
| project CompanyName, ProductName, ProductVersion, LastUsedTime
```

## <a name="device-start-times"></a>Enhetens start tider

Följande fråga visar när enheter har startats under de senaste sju dagarna:

```kusto
OperatingSystem
| where LastBootUpTime <= ago(7d)
| summarize count() by bin(LastBootUpTime,1d)
```

## <a name="free-disk-space"></a>Ledigt diskutrymme

Följande fråga visar ledigt disk utrymme:

```kusto
LogicalDisk
| project Device, DeviceID, Name, Description, FileSystem, Size, FreeSpace
| order by DeviceID asc
```

## <a name="device-information"></a>Enhets information

Visa enhet, tillverkare, modell och OSVersion:

```kusto 
ComputerSystem
| project Device, Manufacturer, Model
| join (OperatingSystem | project Device, OSVersion=Caption)
```

## <a name="boot-times-for-a-device"></a>Start tider för en enhet

Visa start tider för enheter:

```kusto
SystemBootData
| project Device, SystemStartTime, BootDuration, OSStart=EventLogStart, GPDuration, UpdateDuration
| order by SystemStartTime desc
```

## <a name="authentication-failures"></a>Autentiseringsfel

Sök i händelse loggarna efter autentiseringsfel.

```kusto
EventLog('Security')
| where  EventID == 4673
```

## <a name="processmoduleprocessname"></a>ProcessModule ( \<processname> )  

Räknar upp alla moduler (dll) som lästs in av en specifik process. ProcessModule är användbart när det gäller skadlig kod som döljer i legitima processer.  

```kusto
ProcessModule('powershell')
| summarize count() by ModuleName
| order by count_ desc
```

## <a name="antimalware-software-status"></a>Program status för program mot skadlig kod

Hämtar status för program vara för program mot skadlig kod som är installerad på datorn.

```kusto
EPStatus
| project Device, QuickScanAge=datetime_diff('day',now(),QuickScanEndTime)
| summarize DeviceCount=count() by QuickScanAge
```

## <a name="find-bios-manufacturer-that-contains-any-word-like-micro"></a>Hitta BIOS-tillverkare som innehåller valfritt ord som Micro

```kusto
Bios
// Find BIOS Manufacturer that contains any word like Micro, such as Microsoft
| where Manufacturer like '%Micro%'
```

## <a name="find-file-by-its-hash"></a>Hitta filen efter dess hash

Sök efter en fil med hash.

```kusto
Device
| join kind=leftouter ( File('%windir%\\system32\\*.exe')
| where SHA256Hash == 'A92056D772260B39A876D01552496B2F8B4610A0B1E084952FE1176784E2CE77')
| project Device, MalwareFound = iif( isnull(FileName), 'No', 'Yes')
```

## <a name="find-scripts-in-the-ccm-logs-in-the-last-hour"></a>Hitta "skript" i CCM-loggarna under den senaste timmen

Följande fråga kommer att titta på händelser under de senaste 1 timmarna:

```kusto
CcmLog('Scripts',1h)
```

