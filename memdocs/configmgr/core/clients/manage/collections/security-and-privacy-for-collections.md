---
title: Säkerhet och sekretess för samlingar
titleSuffix: Configuration Manager
description: Få metod tips för säkerhet och sekretess i samlingar i Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 30bf2451-5415-4be2-ba8d-21759370cd83
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 42345ee91baaad7dcc82eab537fbeb697d6cd7ab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714495"
---
# <a name="security-and-privacy-for-collections-in-configuration-manager"></a>Säkerhet och sekretess för samlingar i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Det här avsnittet innehåller rekommenderade säkerhets metoder och sekretess information för samlingar i Configuration Manager.  

 Det finns ingen sekretess information som är specifik för samlingar i Configuration Manager. Samlingar är containrar för resurser, t.ex. användare och enheter. Samlings medlemskap beror ofta på vilken information som Configuration Manager samlas in under standard åtgärden. Exempelvis kan en samling med hjälp av resursinformation som har samlats in vid identifiering eller inventering konfigureras så att den innehåller de enheter som uppfyller angivna villkor. Samlingar kan även baseras på information om den aktuella statusen för klienthanteringsåtgärder, t.ex. distribution av program och kompatibilitetskontroll. Förutom dessa frågebaserade samlingar kan administrativa användare även lägga till resurser till samlingar.  

 Mer information om samlingar finns i [Introduktion till samlingar](../../../../core/clients/manage/collections/introduction-to-collections.md). Mer information om rekommenderade säkerhets metoder och sekretess information för Configuration Manager åtgärder som kan användas för att konfigurera samlings medlemskap, finns i [metod tips för säkerhet och sekretess information för Configuration Manager](../../../../core/plan-design/security/security-best-practices-and-privacy-information.md).  

## <a name="security-best-practices-for-collections"></a>Rekommenderade säkerhetsmetoder för samlingar  
 Använd följande rekommenderade säkerhetsmetoder för samlingar.  

|Regelverk för säkerhet|Mer information|  
|----------------------------|----------------------|  
|När du exporterar eller importerar en samling med en MOF-fil (Managed Object Format) som sparas på en nätverksplats måste du skydda platsen och nätverkskanalen.|Begränsar vem som kan komma åt nätverksmappen.<br /><br /> Använd SMB-signering (Server Message Block) eller IPsec (Internet Protocol Security) mellan nätverksplatsen och platsservern för att hindra en angripare från att manipulera exporterade samlingsdata. Kryptera alla data i nätverket med IPsec för att förhindra att information röjs.|  

### <a name="security-issues-for-collections"></a>Säkerhetsproblem för samlingar  
 Samlingar medför följande säkerhetsproblem:  

-   Om du använder samlingsvariabler kan lokala administratörer läsa information som kan vara känslig.  

     Samlingsvariabler kan användas när du distribuerar ett operativsystem.  
