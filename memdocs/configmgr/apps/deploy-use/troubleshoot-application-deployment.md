---
title: Fel söknings tips för distribution av appar
titleSuffix: Configuration Manager
description: Tips för fel sökning av problem med program distribution i Configuration Manager
ms.date: 05/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 4e8b46a3-3e11-475f-a4d7-6bf9ddf14145
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4723a85c55a2a5f7a4fbd0a99a14fbf31e7511c6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710589"
---
# <a name="troubleshooting-tips-for-application-deployments"></a>Fel söknings tips för program distributioner

*Gäller för: Configuration Manager (aktuell gren)*

Vanliga problem med program distributioner omfattas av någon av följande kategorier:

- Program nedladdnings problem

- Kompatibilitet för program distribution har fastnat vid 0%

Om något av dessa problem uppstår innehåller den här artikeln några steg som du kan använda för att felsöka. Mer djupgående fel sökning finns i [Felsöka teknisk referens för program distribution](../understand/app-deployment-technical-reference.md).


## <a name="download-failures"></a>Hämtnings problem

Fel vid hämtning av program innehåller följande problem:

- Klienten har fastnat i nedladdningen av ett program

- Klienten kan inte ladda ned program innehållet

- Klienten har fastnat på 0% när programmet laddas ned

Det första du bör kontrol lera när du får problem med program hämtningen är för saknade eller felkonfigurerade gränser och gräns grupper. Om klienten till exempel är på intranätet och inte har kon figurer ATS för klient hantering enbart för Internet måste dess nätverks plats finnas i en konfigurerad gränser. Det måste också finnas en avgränsnings grupp som har tilldelats den här gränser för att klienten ska kunna hämta innehåll. Mer information finns i [definiera plats gränser och gräns grupper](../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md).

Om du inte kan konfigurera en gränser för en klient, eller om en angiven avgränsnings grupp inte kan vara medlem i en annan avgränsnings grupp:

1. Öppna egenskaperna för **distributions typen**i Configuration Manager-konsolen.  

1. Växla till fliken **innehåll** .

1. I avsnittet för att använda en distributions plats från en intilliggande gränser grupp eller standard platsens gränser grupp, ändrar du **distributions alternativen** för att **Ladda ned innehåll från distributions platsen och kör lokalt**. (Som standard är den här inställningen **inte ladda ned innehåll**.)

Om klienten inte kan ladda ned program innehållet ser du till att det distribueras till en distributions plats. För att verifiera den här konfigurationen kan du använda konsol funktionerna i konsolen för att övervaka innehålls distribution till distributions platserna. Mer information finns i [Övervaka innehåll som du har distribuerat](../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  


## <a name="compliance-stuck-at-0"></a>Kompatibilitet har fastnat vid 0%

När programmets distributions-kompatibilitet är 0%, kontrol lera distributions statusen för programmet i arbets ytan **övervakning** under noden **distributioner** .

- **Pågår**: klienten kan fastna från [nedladdning av innehåll](#download-failures)

- **Fel**: Mer information om hur du felsöker det här problemet finns i följande blogg inlägg: [tips och trick: hur du utför åtgärder på till gångar som rapporterar en misslyckad distribution](https://techcommunity.microsoft.com/t5/Configuration-Manager-Archive/Tips-and-Tricks-How-to-Take-Action-on-Assets-That-Report-a/ba-p/273019)

- **Okänd**: denna status innebär vanligt vis att klienten inte har tagit emot någon princip. Uppdatera klient principen manuellt för att se om klienten tar emot den. Mer information finns i [Starta princip hämtning för en Configuration Manager-klient](../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval).
  
Om dessa åtgärder inte löser problemet kontrollerar du klientens status. Det kan finnas ett djupare underliggande problem med klienten. Mer information finns i [övervaka klienter](../../core/clients/manage/monitor-clients.md).


## <a name="next-steps"></a>Nästa steg

- [Övervakning av program](monitor-applications-from-the-console.md)
- [Distribuera program](deploy-applications.md)
- [Hanterings uppgifter för program](management-tasks-applications.md)
- [Felsöka teknisk referens för program distribution](../understand/app-deployment-technical-reference.md)
