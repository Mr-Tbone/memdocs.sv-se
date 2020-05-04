---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 10/04/2019
ms.openlocfilehash: 5d65b2c250890c10c16214bcee385c39a4f58204
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81716175"
---
### <a name="hardware-inventory-reports"></a><a name="ki_hinv"></a>Rapporter för maskin varu inventering

<!--5468413-->
Om du försöker köra en rapport som förlitar sig på maskin varu inventeringen returneras ett fel. Till exempel returnerar en BitLocker-rapport ett fel som liknar följande meddelande:

```
Microsoft.Reporting.WinForms.ReportServerException
An error has occurred during report processing. (rsProcessingAborted)
```

Du kan också se följande fel i filen **Dataldr. log** :

`[42S22][207][Microsoft][SQL Server Native Client 11.0][SQL Server]Invalid column name 'FileTimeStamp00'. : pOFFICE_ADDIN_DATA`

Instrument paneler för konsolen som är beroende av maskin varu inventeringen kan också påverkas.

Det här problemet beror på en databas schema ändring på vissa maskin varu inventerings tabeller.

#### <a name="workaround"></a>Lösning

Lösningen är att ta bort det befintliga attributet från databasen. Dataloader-plats komponenten kan sedan skapa ett nytt attribut. Kör följande SQL-skript på plats databas servern för att åtgärda tabell schemat:

``` SQL
IF NOT EXISTS (SELECT * FROM SYS.columns WHERE name = 'FileTimestamp00' AND object_id = OBJECT_ID('OFFICE_ADDIN_DATA'))
BEGIN
       DELETE am
       FROM AttributeMap am
       INNER JOIN GroupMap gm ON am.GroupKey=gm.GroupKey
       WHERE gm.GroupClass='MICROSOFT|OFFICE_ADDIN|1.0'
       AND am.AttributeName='FileTimeStamp'

       PRINT 'Fix OFFICE_ADDIN_DATA schema'
END
```
