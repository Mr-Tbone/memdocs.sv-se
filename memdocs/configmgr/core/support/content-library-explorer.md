---
title: Innehållsbiblioteksutforskaren
titleSuffix: Configuration Manager
description: Använd innehålls biblioteks Utforskaren för att visa och felsöka innehålls biblioteket på en Configuration Manager distributions plats.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 691896d9-ec0f-461f-a3f2-40378ebd3121
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: aa92fb143815faf693f6c2629c3f6436546c5080
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078540"
---
# <a name="content-library-explorer"></a>Innehållsbiblioteksutforskaren

*Gäller för: Configuration Manager (aktuell gren)*

Innehålls biblioteks Utforskaren är ett av de [Configuration Manager verktygen](tools.md). Använd verktyget för följande aktiviteter:  

- Utforska innehålls biblioteket på en viss distributions plats  

- Felsök problem med innehålls biblioteket  

- Kopiera paket, innehåll, mappar och filer från innehålls biblioteket  

- Distribuera om paket till distributions platsen  

- Verifiera paket på fjärranslutna distributions platser  



## <a name="requirements"></a>Krav

- Kör verktyget med ett konto som har administrativ åtkomst till:  

    - Mål distributions platsen  

    - WMI-providern på plats servern  

    - Configuration Manager-providern  

- Endast rollen **Fullständig administratör** och **skrivskyddad analytiker** har behörighet att visa all information från det här verktyget.  

    - Andra roller, till exempel **program administratör**, kan visa ofullständig information. Mer information finns i [inaktiverade paket](#bkmk_disabled-packages).  

    - Den **skrivskyddade analytikern** kan inte distribuera om paket från det här verktyget.  

- Kör verktyget från vilken dator som helst, så länge det kan anslutas till:  

    - Mål distributions platsen  

    - Den primära plats servern  

    - Configuration Manager-providern  

- Om distributions platsen befinner sig på plats servern är det fortfarande nödvändigt att ha administrativ åtkomst till plats servern.  



## <a name="usage"></a>Användning 

När du startar **ContentLibraryExplorer. exe**anger du det fullständigt kvalificerade domän namnet (FQDN) för mål distributions platsen. Den ansluter sedan till distributions platsen. Om distributions platsen är en del av en sekundär plats uppmanas du att ange FQDN för den primära plats servern och den primära plats koden.

I det vänstra fönstret visar du de paket som distribueras till den här distributions platsen. Expandera paketen och utforska deras mappstruktur. Den här strukturen matchar mappstrukturen som du skapade paketet från.

När du väljer en mapp visas den i den högra rutan alla filer i mappen. Den här vyn innehåller följande information: 
- Filnamn
- Filstorlek
- Vilken enhet den finns på
- Andra paket som använder samma fil på enheten
- När filen senast ändrades på distributions platsen

Verktyget ansluter också till Configuration Manager-providern. Den här anslutningen är att avgöra vilka paket som distribueras till distributions platsen och om de faktiskt finns i distributions platsens innehålls bibliotek. Till exempel kanske ett paket som väntar på distribution ännu inte finns i innehålls biblioteket. Ett sådant paket visas som "väntar" i verktyget och inga åtgärder har Aktiver ATS för det här paketet.


### <a name="disabled-packages"></a><a name="bkmk_disabled-packages"></a>Inaktiverade paket

Vissa paket finns på distributions platsen, men visas inte i Configuration Manager-konsolen. Dessa paket är markerade med en asterisk (\*). Inga åtgärder kan utföras för dessa paket. Andra paket kan också markeras med en asterisk och ha åtgärder inaktiverade. 

Det finns tre huvudsakliga orsaker till inaktiverade paket:  

- Paketet är Configuration Manager klient uppgradering. Det här paketet innehåller "CCMSetup. exe".  

- Ditt användar konto har inte åtkomst till paketet, troligen på grund av rollbaserad administration. Rollen **program författare** kan till exempel inte se driv rutins paket i-konsolen, så alla driv rutins paket på distributions platsen markeras som inaktiverade.  

- Paketet har överblivnas på distributions platsen.  


### <a name="validate-packages"></a>Validera paket

Verifiera paket med hjälp av **paket** > **verifiering** i verktygsfältet. Välj först en Package-nod i den vänstra rutan Välj inte ett innehåll eller en mapp. Verktyget ansluter till WMI-providern på distributions platsen för den här åtgärden. När verktyget startar markeras paket som saknar ett eller flera innehåll som ogiltiga. Verifierar att paketet visar vilket innehåll som saknas. Om allt innehåll finns men data skadas, identifierar verifieringen felet.


### <a name="redistribute-packages"></a>Distribuera om paket

Distribuera om paket med **Package** > **omdistribution** av paket i verktygsfältet. Välj först en Package-nod i det vänstra fönstret. Den här åtgärden kräver att du distribuerar om paket.


### <a name="other-actions"></a>Andra åtgärder

Använd **Redigera** > **kopia** för att kopiera paket, innehåll, mappar och filer från innehålls biblioteket till en angiven mapp. Du kan inte kopiera själva innehålls biblioteket. Välj fler än en fil, men du kan inte välja flera mappar.

Sök efter paket med hjälp av **Redigera** > **Sök-paket**. Den här åtgärden söker efter din fråga i paket namnet och paket-ID: t.



## <a name="limitations"></a>Begränsningar

- Verktyget kan inte ändra innehålls biblioteket direkt på något sätt. Ändringar i innehålls biblioteket kan leda till fel.  

- Verktyget kan omdistribuera paket, men endast till mål distributions platsen.  

- När du samplacerar distributions platsen med plats servern kan du inte validera paket data. Använd Configuration Manager-konsolen i stället. Verktyget söker fortfarande igenom paketet för att se till att allt innehåll finns, men inte nödvändigt vis intakt.  

- Du kan inte ta bort innehåll med det här verktyget.



## <a name="see-also"></a>Se även

- [Grundläggande begrepp för innehållshantering](../plan-design/hierarchy/fundamental-concepts-for-content-management.md)
- [Innehållsbibliotek](../plan-design/hierarchy/the-content-library.md)
