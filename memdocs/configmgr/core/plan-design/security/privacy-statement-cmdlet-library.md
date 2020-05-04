---
title: Sekretess policy för cmdlets
titleSuffix: Configuration Manager
description: Lär dig mer om hur Microsoft samlar in och använder data som är relaterade till Configuration Manager-cmdlets
ms.date: 01/3/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bec00fb4-1ac0-4e49-b330-0871b3722459
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 551a8086894f877d07c57fbe2848c2befacfc5b5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714649"
---
# <a name="configuration-manager-cmdlet-library-privacy-statement"></a>Sekretess policy för Configuration Manager cmdlet-bibliotek

*Gäller för: Configuration Manager (aktuell gren)*

Den här sekretess policyn täcker funktionerna för Configuration Manager cmdlet-biblioteket.  

## <a name="usage-data"></a>Användningsdata  

#### <a name="what-this-feature-does"></a>Vad den här funktionen gör

Med Configuration Manager cmdlet-biblioteket kan du hantera en Configuration Manager-hierarki med hjälp av Windows PowerShell-cmdletar och-skript. Cmdlet-biblioteket samlar in information om hur du använder cmdletarna i biblioteket för att identifiera trender och användnings mönster. Cmdlet-biblioteket samlar även in typer och antal fel som du får när du använder cmdlet: arna.  

#### <a name="information-collected-processed-or-transmitted"></a>Information som samlas in, bearbetas eller överförs
   
De insamlade användnings data innefattar att starta, stoppa och avsluta cmdlets, köra inaktuella cmdletar och aktivitets mått för SMS-provider-åtgärder som är relaterade till cmdletarna. Den här informationen är inte personligt identifierbar. Insamlad fel information innehåller fel som visar information om fel i cmdlets och fel information för undantags fel. Vissa fel rapporter kan oavsiktligt inkludera enskilda identifierare, t. ex. ett serie nummer för en enhet som är ansluten till din dator. Cmdlet-biblioteket filtrerar och anonymiseras uppgifterna information som finns i fel rapporterna för att ta bort enskilda identifierare före överföring till Microsoft.  

#### <a name="use-of-information"></a>Användning av information
   
Microsoft använder den här informationen för att förbättra kvalitet, säkerhet och integritet för de produkter och tjänster som de erbjuder.  

#### <a name="choicecontrol"></a>Valmöjligheter/kontroll   

Den här funktionen för användnings data är aktive rad som standard. Configuration Manager cmdlet-biblioteket har två register nycklar som styr den här funktionen.  

 Ange dessa två register nyckel värden för att helt avanmäla. De är för var och en av de ETW (Event Tracing for Windows)-providers (ETW):  

- HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Provider: CeipLevel = 0 (väljer du bort användnings data för enhets leverantören)  

- HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Cmdlets: CeipLevel = 0 (väljer bort användnings data för cmdletarna)  

  Ändringar av inställningarna för användnings data är bara för den dator där de görs.  


## <a name="next-steps"></a>Nästa steg

[Dokumentation om Configuration Manager cmdlet-bibliotek](https://docs.microsoft.com/powershell/sccm/configurationmanager/).   
