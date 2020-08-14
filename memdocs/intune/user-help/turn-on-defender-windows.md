---
title: Starta Windows Defender | Microsoft Docs
description: Lär dig hur du aktiverar Windows Defender för att komma åt företagets resurser.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/07/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: d16dd2de-3ed5-474f-a04b-36dcd350162c
searchScope:
- User help
ROBOTS: ''
ms.reviewer: shburbid
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: a57010a5c8089b0ac979cf43c3706467d83faea2
ms.sourcegitcommit: 532a06163f462527254d23e7dc505b18c0c4f938
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/11/2020
ms.locfileid: "88110706"
---
# <a name="turn-on-windows-defender-to-access-company-resources"></a>Aktivera Windows Defender för att komma åt företagets resurser

Organisationer vill se till att enheter som kommer åt deras resurser är säkra. Därför kan de kräva att du använder [Windows Defender](https://www.microsoft.com/safety/pc-security/windows-defender.aspx). Windows Defender är ett antivirusprogram som ingår i Windows och hjälper till att skydda din enhet från virus samt annan skadlig kod och hot. 

Den här artikeln beskriver hur du uppdaterar enhetsinställningarna för att uppfylla din organisations antiviruskrav och lösa åtkomstproblem. 

## <a name="turn-on-windows-defender"></a>Starta Windows Defender
Utför följande steg för att aktivera Windows Defender på din enhet. 

1. Välj **Start**-menyn.
2. I sökfältet skriver du **grupprincip**. Välj sedan **Redigera grupprincip** bland de visade resultaten. Redigeraren för lokala grupprinciper öppnas.
4. Välj **Datorkonfiguration** > **Administrativa mallar** > **Windows-komponenter** > **Windows Defender Antivirus**. 
5. Rulla längst ned i listan och välj **Inaktivera Windows Defender Antivirus**.  
6. Välj **Inaktiverat** eller **Inte konfigurerat**. Det kan verka ologiskt att välja de här alternativen eftersom namnen antyder att du stänger av Windows Defender. Men i själva verket säkerställer de här alternativen att det är aktiverat. 
7. Välj **Tillämpa** > **OK**.  


## <a name="turn-on-real-time-and-cloud-delivered-protection"></a>Aktivera molnlevererat skydd i realtid

Utför följande steg för att aktivera molnlevererat skydd i realtid. Tillsammans skyddar dessa antivirusfunktioner mot spionprogram och kan leverera korrigeringar för problem med skadlig kod via molnet. 

1. Välj **Start**-menyn.
2. I sökfältet skriver du **Windows Security**. Välj det matchande resultatet. 
3. Välj **Virus & threat protection** (Skydd mot virus och hot).
4. Under **Virus & threat protection settings** (Inställningar för skydd mot virus och hot) väljer du **Hantera inställningar**.
5. Växla varje växel under **Realtidsskydd** och **Molnlevererat skydd** för att aktivera dem. 

Om du inte ser de här alternativen på skärmen kan de vara dolda. Utför följande steg för att göra dem synliga.  

1. Välj **Start**-menyn.  
2. I sökfältet skriver du **grupprincip**. Välj sedan **Redigera grupprincip** bland de visade resultaten. Redigeraren för lokala grupprinciper öppnas.
3. Välj **Datorkonfiguration** > **Administrativa mallar** > **Windows-komponenter** > **Windows-säkerhet** > **Skydd mot virus och hot**.
4. Välj **Dölj avsnittet Skydd mot virus och hot**.
5. Välj **Inaktiverat** > **Tillämpa** > **OK**.  

## <a name="update-your-antivirus-definitions"></a>Uppdatera antivirusdefinitionerna
Utför följande steg för att uppdatera antivirusdefinitionerna.  
1. Välj **Start**-menyn.
2. I sökfältet skriver du **Windows Security**. Välj det matchande resultatet. 
3. Välj **Virus & threat protection** (Skydd mot virus och hot).
4. Under **Virus & threat protection updates** (Uppdateringar av skydd mot virus och hot) väljer du **Sök efter uppdateringar**. Om du inte ser det här alternativet på skärmen slutför du den första uppsättningen med steg i [Aktivera realtidsskydd](turn-on-defender-windows.md#turn-on-real-time-and-cloud-delivered-protection). Försök sedan att söka efter uppdateringar igen. 

## <a name="next-steps"></a>Nästa steg  

Behöver du fortfarande hjälp? Kontakta företagssupporten. Titta efter kontaktuppgifter på [företagsportalens webbplats](https://go.microsoft.com/fwlink/?linkid=2010980).
