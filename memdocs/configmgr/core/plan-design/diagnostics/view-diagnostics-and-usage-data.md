---
title: Visa diagnostikdata
titleSuffix: Configuration Manager
description: Visa diagnostik-och användnings data för att bekräfta att din Configuration Manager-hierarki inte innehåller känslig information.
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 594eb284-0d93-4c5d-9ae6-f0f71203682a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 993a3549ddca4c2b5ae1dbbfc0346f28b9c3083e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712542"
---
# <a name="how-to-view-diagnostics-and-usage-data-for-configuration-manager"></a>Så här visar du diagnostik-och användnings data för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Du kan visa diagnostik-och användnings data från din Configuration Manager-hierarki för att bekräfta att den inte innehåller känslig eller identifierbar information. Platsen sammanfattar och lagrar sina diagnostikdata i **TEL_TelemetryResultss** tabellen i plats databasen. Den formaterar data så att de kan användas program mässigt och effektivt.

Informationen i den här artikeln ger dig en översikt över de exakta data som skickas till Microsoft. Den är inte avsedd att användas för andra ändamål, t. ex. data analys.  

## <a name="view-data-in-database"></a>Visa data i databasen

Använd följande SQL-kommando för att visa innehållet i den här tabellen och visa exakt vilka data som skickas:  

``` SQL
SELECT * FROM TEL_TelemetryResults
```

## <a name="export-the-data"></a>Exportera data

När tjänst anslutnings punkten är i offlineläge använder du tjänst anslutnings verktyget för att exportera aktuella data till en fil med kommaavgränsade värden (CSV). Kör tjänst anslutnings verktyget på tjänst anslutnings punkten med parametern **-export** .

Mer information finns i [använda tjänst anslutnings verktyget](../../servers/manage/use-the-service-connection-tool.md).

## <a name="one-way-hashes"></a><a name="bkmk_hashes"></a>Enkelriktade hash-värden

Vissa data består av strängar med slumpmässiga alfanumeriska tecken. Configuration Manager använder SHA-256-algoritmen för att skapa enkelriktade hash-värden. Den här processen ser till att Microsoft inte samlar in potentiellt känsliga data. De hashade data kan fortfarande användas för korrelation och jämförelse.

I stället för att till exempel samla in namnen på tabeller i plats databasen, samlar den in enkelriktad hash för varje tabell namn. Det här beteendet ser till att alla anpassade tabell namn inte visas. Microsoft gör sedan samma enkelriktade hash-process som standard namnen på SQL-tabell. Om du jämför resultaten av de två frågorna bestäms avvikelsen för databas schemat från produktens standard. Den här informationen används sedan för att förbättra uppdateringar som kräver ändringar i SQL-schemat.  

När du visar rå data visas ett gemensamt hashat värde på varje datarad. Denna hash är hierarki-ID: t. Den används för att korrelera data med samma hierarki utan att identifiera kunden eller källan.

### <a name="how-the-one-way-hash-works"></a>Hur enkelriktad hash fungerar

1. Hämta ditt hierarki-ID genom att köra följande SQL-fråga i SQL Management Studio mot Configuration Manager-databasen:

    ``` SQL
    select [dbo].[fnGetHierarchyID]()
    ```

2. Använd följande Windows PowerShell-skript för att utföra det enkelriktade hashvärdet för ditt hierarki-ID.  

    ``` PowerShell
    Param( [Parameter(Mandatory=$True)] [string]$value )  
      $guid = [System.Guid]::NewGuid()  
      if( [System.Guid]::TryParse($value,[ref] $guid) -eq $true ) {  
      #many of the values we hash are Guids  
      $bytesToHash = $guid.ToByteArray()  
    } else {  
      #otherwise hash as string (unicode)  
      $ue = New-Object System.Text.UnicodeEncoding  
      $bytesToHash = $ue.GetBytes($value)
    }  
      # Load Hash Provider (https://en.wikipedia.org/wiki/SHA-2)
    $hashAlgorithm = [System.Security.Cryptography.SHA256Cng]::Create()
    # Hash the input
    $hashedBytes = $hashAlgorithm.ComputeHash($bytesToHash)
    # Base64 encode the result for transport
    $result = [Convert]::ToBase64String($hashedBytes)
    return $result
    ```

3. Jämför skriptets utdata mot GUID i rå data. Den här processen visar hur data döljs.

## <a name="next-steps"></a>Nästa steg

> [!div class="nextstepaction"]
> [Nivåer av diagnostikens användnings data](levels-overview.md)
