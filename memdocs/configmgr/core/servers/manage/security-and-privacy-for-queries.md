---
title: Säkerhet och sekretess för frågor
titleSuffix: Configuration Manager
description: Lär dig metod tips för säkerhet och sekretess när du frågar efter information från plats databasen.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 30080620-20d3-4c38-b8dd-db5516e1acae
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 882eedd1be029d5824fbd5d26a3f08d8f8f0021d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714614"
---
# <a name="security-and-privacy-for-queries-in-configuration-manager"></a>Säkerhet och sekretess för frågor i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Med frågor i Configuration Manager kan du hämta information från plats databasen enligt de kriterier som du anger. Configuration Manager samlar in plats databas information under standard åtgärden. Genom att t. ex. använda information som har samlats in under identifiering eller inventering kan du konfigurera en fråga för att identifiera enheter som uppfyller angivna villkor.  

 Mer information om frågor finns i [Introduktion till frågor](../../../core/servers/manage/introduction-to-queries.md). Rekommenderade säkerhets metoder och sekretess information om Configuration Manager åtgärder som samlar in data som du kan hämta med hjälp av frågor finns i [säkerhet och sekretess för Configuration Manager](../../../core/plan-design/security/security-and-privacy.md).  

## <a name="security-best-practices-for-queries"></a>Rekommenderade säkerhets metoder för frågor

 Använd den här rekommenderade säkerhets metoden för frågor.  

|Regelverk för säkerhet|Mer information|  
|----------------------------|----------------------|  
|När du exporterar eller importerar en fråga som har sparats på en nätverks plats måste du skydda platsen och nätverks kanalen.|Begränsa vilka som har tillgång till nätverksmappen.<br /><br /> Använd SMB-signering (Server Message Block) eller Internet Protocol security (IPsec) mellan nätverks platsen och plats servern för att hindra en angripare från att manipulera frågedata innan den importeras.|  

## <a name="next-steps"></a>Nästa steg
  
[Säkerhet och sekretess för Configuration Manager](../../../core/plan-design/security/security-and-privacy.md)
