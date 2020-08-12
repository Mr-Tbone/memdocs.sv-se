---
title: Inkompatibel kod
titleSuffix: Configuration Manager
description: En teknisk referens för möjliga koder från en Configuration Manager-klient som inte är kompatibel med BitLocker-principen
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: reference
ms.assetid: 6c28fa29-fc97-49ef-9fc3-cb062bdba908
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2cb6c17802319b0d559474fa8ff208346c2811e0
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127941"
---
# <a name="non-compliance-codes"></a>Inkompatibel kod

*Gäller för: Configuration Manager (aktuell gren)*

<!--3601034-->

WMI på klienten innehåller följande koder för inkompatibilitet. Det beskriver också orsakerna till att en viss enhet rapporterar som icke-kompatibel.

Det finns olika metoder för att Visa WMI. Använd till exempel följande PowerShell-kommando:

``` PowerShell
(Get-WmiObject -Class mbam_Volume -Namespace root\microsoft\mbam).ReasonsForNoncompliance
```

> [!TIP]
> Om enheten är kompatibel returnerar inte det här kommandot något.
>
> Du kan också kontrol lera `Compliant` attributet för den här klassen, som är `1` om enheten är kompatibel.

|Kod som inte uppfyller kraven|Orsak till inkompatibilitet|
|--- |--- |
|0|Krypterings styrkan är inte AES 256.|
|1|BitLocker-principen kräver att den här volymen krypteras, men den är inte det.|
|2|BitLocker-principen kräver att volymen *inte* är krypterad, men den är.|
|3|BitLocker-principen kräver att den här volymen använder ett TPM-skydd, men det är inte det.|
|4|BitLocker-principen kräver att den här volymen använder ett TPM + PIN-skydd, men det är inte det.|
|5|BitLocker-principen tillåter inte att icke-TPM-datorer rapporterar som kompatibla.|
|6|Volymen har ett TPM-skydd, men TPM: en är inte synlig.|
|7|BitLocker-principen kräver att den här volymen använder ett lösen ords skydd, men det finns ingen.|
|8|BitLocker-principen kräver att den här volymen *inte* använder ett lösen ords skydd, men har en.|
|9|BitLocker-principen kräver att den här volymen använder ett automatiskt lås skydd, men det finns ingen.|
|10|BitLocker-principen kräver att den här volymen *inte* använder ett skydd för automatisk upplåsning, men det har ett.|
|11|BitLocker identifierar en princip konflikt, vilket förhindrar att den rapporterar volymen som kompatibel.|
|12|En system volym krävs för att kryptera operativ system volymen, men den finns inte.|
|13|Skyddet har pausats för volymen.|
|14|Automatisk upplåsning av skydd är osäker om inte operativ system volymen är krypterad.|
|15|Principen kräver lägsta chiffer-styrka är XTS-AES-128-bit, verklig chiffer-styrka är svagare.|
|16|Principen kräver lägsta chiffer-styrka är XTS-AES-256-bit, verklig chiffer-styrka är svagare.|
