---
title: Stöd för Unicode och ASCII
titleSuffix: Configuration Manager
description: Läs om stöd för Unicode-och ASCII-tecken i Configuration Manager objekt.
ms.date: 08/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2bdec799-905f-48bc-aed5-2d92134739e8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7bd3dad5f0ef24074ac8c8e6d2edf01d5641b541
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717554"
---
# <a name="unicode-and-ascii-support-in-configuration-manager"></a>Stöd för Unicode och ASCII i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Manager skapar de flesta objekt genom att använda Unicode-tecken. Flera objekt har dock bara stöd för ASCII-tecken eller andra begränsningar.  

## <a name="objects-that-use-ascii-characters"></a><a name="BKMK_ASCIIchar"></a>Objekt som använder ASCII-tecken

När du skapar följande objekt stöder Configuration Manager endast ASCII-teckenuppsättningen:  

- Platskod  

- Alla dator namn för plats system servrar  

- Följande Configuration Manager-konton:  

    > [!NOTE]  
    > Dessa konton har stöd för ASCII-tecken och ru: er-tecken på en plats som körs på ryska.  

    - Konto för push-installation av klient  

    - Anslutnings konto för hanterings plats databas  

    - Nätverksåtkomstkonto  

    - Paket åtkomst konto  

    - Standard avsändar konto  

    - Konto för installation av plats system  

    - Anslutnings konto för program uppdaterings plats  

    - Konto för program uppdaterings platsens proxyserver  

    > [!NOTE]  
    > De konton som du anger för rollbaserad administration stöder Unicode.  
    >
    > Repor ting Services-platsens konto stöder Unicode, med undantag av ru: er tecken.  

- Fullständigt kvalificerat domän namn (FQDN) för plats servrar och plats system  

- Installations Sök väg för Configuration Manager  

- SQL Server instans namn  

- Sökvägen för följande plats system roller:  

    - Registreringsplats  

    - Registreringsproxyplats  

    - Rapporteringstjänstpunkt  

    - Plats för tillståndsmigrering  

- Sökvägen för följande mappar:  

    - Mappen som lagrar överförings data för klient tillstånd  

    - Mappen som innehåller Configuration Manager rapporter  

    - Mappen som lagrar Configuration Manager säkerhets kopian  

    - Mappen som lagrar installationskällfilerna för plats konfiguration  

    - Mappen som lagrar nödvändiga hämtningar för användning av installations programmet  

- Sökvägen för följande objekt:  

    - IIS-webbplats  

    - Installations Sök väg för virtuellt program  

    - Namn på virtuellt program  

- ISO-filnamn för start medier  


## <a name="additional-limitations"></a><a name="BKMK_OtherCharLimitations"></a>Ytterligare begränsningar

Följande är ytterligare begränsningar för teckenuppsättningar och språk versioner som stöds:  

- Configuration Manager har inte stöd för att ändra språk för plats serverdatorn.  

- En företags certifikat utfärdare (CA) stöder inte klient dator namn som använder DBCS-teckenuppsättningar (double-byte character set). De klient dator namn som du kan använda begränsas av PKI-begränsningen för den inställda IA5-teckenuppsättningen. Configuration Manager stöder inte CA-namn eller ämnes namns värden som använder DBCS.  


## <a name="objects-that-arent-localized"></a><a name="BKMK_LangNonLocalize"></a>Objekt som inte är lokaliserade

Configuration Manager-databasen stöder Unicode för de flesta objekt som lagras. När det är möjligt visas den här informationen i OS-språket som matchar datorns nationella inställningar. För att klient gränssnittet eller Configuration Manager-konsolen ska visa information på datorns operativ system språk måste datorns språk inställning matcha ett klient-eller Server språk som du installerar på en plats.  

Flera Configuration Manager objekt stöder inte Unicode. De lagras i-databasen med hjälp av ASCII, eller så har de ytterligare språk begränsningar. Den här informationen visas alltid med ASCII-teckenuppsättningen eller på det språk som användes när du skapade objektet.  
