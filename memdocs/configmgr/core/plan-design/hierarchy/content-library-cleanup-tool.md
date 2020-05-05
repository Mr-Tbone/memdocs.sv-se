---
title: Rensningsverktyg för innehållsbibliotek
titleSuffix: Configuration Manager
description: Använd rensnings verktyget för innehålls bibliotek för att ta bort överblivna innehåll som inte längre är kopplat till en Configuration Manager-distribution.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 226cbbb2-9afa-4e2e-a472-be989c0f0e11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8b1b415d5c24800f003f730426216ac7cf190a4f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720221"
---
# <a name="content-library-cleanup-tool"></a>Rensningsverktyg för innehållsbibliotek

*Gäller för: Configuration Manager (aktuell gren)*

Använd kommando rads verktyget Rensa innehålls bibliotek för att ta bort innehåll som inte längre är kopplat till något paket eller program på en distributions plats. Den här typen av innehåll kallas *överblivna innehåll*. Det här verktyget ersätter äldre versioner av liknande verktyg som har släppts för tidigare Configuration Manager produkter.  

Verktyget påverkar bara innehållet på den distributions plats som du anger när du kör verktyget. Verktyget kan inte ta bort innehåll från innehålls biblioteket på plats servern.

Sök efter **ContentLibraryCleanup. exe** på `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` plats servern.



## <a name="requirements"></a>Krav  

- Kör bara verktyget mot en enskild distributions plats i taget.  

- Kör den direkt på den dator som är värd för distributions platsen för att rensa eller fjärrans luta från en annan dator.  

- Det användar konto som kör verktyget måste ha behörigheterna samma som säkerhets rollen **Fullständig administratör** i Configuration Manager.  



## <a name="modes-of-operation"></a>Lägen för åtgärden

Kör verktyget i följande två lägen: [What-If](#what-if-mode) och [Delete](#delete-mode).

> [!Tip]  
> Börja med *konsekvens* läget. När du är nöjd med resultaten kör du verktyget i *borttagnings* läge.  


### <a name="what-if-mode"></a>Konsekvens läge   

Om du inte anger `/delete` parametern körs verktyget i vad-om-läge. I det här läget identifieras det innehåll som skulle tas bort från distributions platsen.

- När det körs i det här läget tar verktyget inte bort några data.  

- Verktyget skriver till logg fils informationen om det innehåll som det skulle ta bort. Du uppmanas inte att bekräfta varje möjlig borttagning.  


### <a name="delete-mode"></a>Ta bort läge   

När du kör verktyget med- `/delete` parametern körs verktyget i borttagnings läge.

- Vid körning i det här läget kan överblivna innehåll som hittas på den angivna distributions platsen tas bort från distributions platsens innehålls bibliotek.  

- Innan du tar bort varje fil bör du kontrol lera att verktyget bör ta bort det. Välj **Y** för Ja, **N** för nej eller **Ja till alla** för att hoppa över ytterligare prompter och ta bort allt överblivna innehåll.  


### <a name="log-file"></a>Loggfil

När verktyget körs i båda lägena skapas automatiskt en logg. Den namnger logg filen med följande information: 
- Läget som verktyget körs i  
- Namnet på distributions platsen  
- Datum och tid för åtgärden  

När verktyget har slutförts öppnas logg filen automatiskt i Windows. 

Som standard skriver verktyget logg filen till Temp-mappen för det användar konto som kör verktyget. Den här platsen finns på den dator där du kör verktyget, som inte alltid är mål för verktyget. Använd `/log` parametern för att omdirigera logg filen till en annan plats, inklusive en nätverks resurs.



## <a name="run-the-tool"></a>Kör verktyget

Så här kör du verktyget: 

1. Öppna en kommandotolk som administratör. Ändra katalogen till den mapp som innehåller **ContentLibraryCleanup. exe**.  

2. Ange en kommando rad som innehåller de nödvändiga [kommando rads parametrarna](#bkmk_params)och eventuella valfria parametrar som du vill använda.



## <a name="command-line-parameters"></a><a name="bkmk_params"></a>Kommando rads parametrar  

Använd de här kommando rads parametrarna i vilken ordning som helst.   

### <a name="required-parameters"></a>Obligatoriska parametrar

|Parameter|Information|
|---------|-------|
| `/dp <distribution point FQDN>`  | Ange det fullständigt kvalificerade domän namnet (FQDN) för distributions platsen som ska rensas. |
| `/ps <primary site FQDN>` | *Krävs* endast när innehåll rensas från en distributions plats på en sekundär plats. Verktyget ansluter till den överordnade primära platsen för att köra frågor mot SMS-providern. Med dessa frågor kan verktyget avgöra vilket innehåll som ska finnas på distributions platsen. Den kan sedan identifiera det överblivna innehållet som ska tas bort. Den här anslutningen till den överordnade primära platsen måste göras för distributions platser på en sekundär plats eftersom den information som krävs inte är tillgänglig direkt från den sekundära platsen.|
| `/sc <primary site code>`  | *Krävs* endast när innehåll rensas från en distributions plats på en sekundär plats. Ange plats koden för den överordnade primära platsen. |

#### <a name="example-scan-and-log-what-content-it-would-delete-what-if"></a>Exempel: Genomsök och logga det innehåll som det skulle ta bort (vad-om)
`ContentLibraryCleanup.exe /dp server1.contoso.com`

#### <a name="example-scan-and-log-content-for-a-dp-at-a-secondary-site"></a>Exempel: Skanna och logga innehåll för en DP på en sekundär plats
`ContentLibraryCleanup.exe /dp server1.contoso.com /ps siteserver1.contoso.com /sc ABC` 


### <a name="optional-parameters"></a>Valfria parametrar

|Parameter|Information|
|---------|-------|
|`/delete`| Använd den här parametern när du är redo att ta bort innehåll från distributions platsen. Du blir ombedd att ta bort innehållet. </br></br> När du inte använder den här parametern loggar verktyget resultatet av vilket innehåll som tas bort. Utan den här parametern tar den inte bort något innehåll från distributions platsen. |
| `/q` | Den här parametern kör verktyget i tyst läge som förhindrar alla uppmaningar. Dessa meddelanden inkluderar när innehåll tas bort. Den öppnar inte heller logg filen automatiskt. |
| `/ps <primary site FQDN>` | Valfritt endast när innehåll rensas från en distributions plats på en primär plats. Ange det fullständiga domän namnet för den primära plats som distributions platsen tillhör. |
| `/sc <primary site code>` | Valfritt endast när innehåll rensas från en distributions plats på en primär plats. Ange plats koden för den primära plats som distributions platsen tillhör. |
| `/log <log file directory>` | Ange den plats där verktyget skriver logg filen. Den här platsen kan vara en lokal enhet eller en nätverks resurs.</br></br> När du inte använder den här parametern placerar verktyget logg filen i användarens Temp-katalog på den dator där verktyget körs.|

#### <a name="example-delete-content"></a>Exempel: ta bort innehåll 
`ContentLibraryCleanup.exe /dp server1.contoso.com /delete`

#### <a name="example-delete-content-without-prompts"></a>Exempel: ta bort innehåll utan prompter
`ContentLibraryCleanup.exe /q /dp server1.contoso.com /delete` 

#### <a name="example-log-to-local-drive"></a>Exempel: logga till lokal enhet
`ContentLibraryCleanup.exe /dp server1.contoso.com /log C:\Users\Administrator\Desktop` 

#### <a name="example-log-to-network-share"></a>Exempel: logga till nätverks resurs
`ContentLibraryCleanup.exe /dp server1.contoso.com /log \\server\share`


### <a name="known-issue"></a>Kända problem

När ett paket eller en distribution har misslyckats eller pågår kan verktyget returnera följande fel:`System.InvalidOperationException: This content library cannot be cleaned up right now because package <packageID> is not fully installed.`

Det finns ingen lösning för det här problemet. Verktyget kan inte på ett tillförlitligt sätt identifiera överblivna filer när innehåll pågår eller inte har kunnat distribueras. Verktyget tillåter inte att du rensar innehåll förrän du har löst problemet.
