---
title: Åtgärda problem med åtkomstpunktsbegränsningar i Intune
description: Här beskriver vi tre vanliga felmeddelanden relaterade till principer för åtkomstpunktsbegränsning i Intune och hur du åtgärdar dem.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 05/28/2018
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: b58ce9956a96779d1e16226567d170ce2bfea1b5
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83877376"
---
# <a name="resolve-access-point-restrictions"></a>Åtgärda problem med åtkomstpunktsbegränsningar

Organisationer kan begränsa vilka platser enheter kan komma åt företagsdata från.
De konfigurerar dessa *åtkomstpunktsbegränsningar* genom att konfigurera och definiera godkända nätverksplatser.  

Om du försöker ansluta till en okänt eller icke godkänt nätverk kan något av följande meddelanden visas:

* Begränsningar för åtkomstpunkt har inte ställts in.
* Du är inte ansluten till ett godkänt nätverk.
* Det uppstod ett fel och det gick inte att tillämpa åtkomstpunktsbegränsningarna.

 I tabellerna nedan visas respektive meddelande, vad det innebär och hur du kommer åt dina arbetsresurser igen.

## <a name="access-point-restrictions-not-set-up"></a>Begränsningar för åtkomstpunkt har inte ställts in  
| Meddelande på företagsportalen | Vad meddelandet betyder | Det här bör du göra                                                               
|------------------------|--------------------------|--------------------------|
| **Begränsningar för åtkomstpunkt har inte ställts in – Åtkomstpunktsbegränsningar har aktiverats och måste konfigureras.** | Ditt företag har konfigurerat åtkomstpunktsbegränsningar som tillämpas på din enhet. Den här inställningen kräver att företagsportalappen verifierar några nätverksinställningar på din enhet. | Tryck på **Lös**. Företagsportalappen kontrollerar att du är ansluten till ett nätverk som har godkänts av företaget. |

## <a name="not-connected-to-an-approved-network"></a>Du är inte ansluten till ett godkänt nätverk  

| Meddelande på företagsportalen | Vad meddelandet betyder | Det här bör du göra                                                                   
|------------------------|-----------------------------------|--------------------------|
| **Enheten är inte ansluten till en godkänt nätverk – Anslut till ett godkänt trådlöst nätverk.** | Du är ansluten till ett nätverk som inte är godkänt för arbetsplatsåtkomst. När du är ansluten till det här nätverket kan du inte komma åt din e-post för arbetet, appar och andra skyddade företagsresurser. | Anslut till ett nätverk som godkänts av företaget. Försök sedan igen genom att trycka på **Lös**. |

## <a name="restrictions-couldnt-be-enforced"></a>Det gick inte att tillämpa begränsningar  

| Meddelande på företagsportalen | Vad meddelandet betyder | Det här bör du göra                                                                      
|------------------------|-----------------------------------|--------------------------|
| **Det gick inte att tillämpa åtkomstpunktsbegränsningar – Företagsportalen påträffade ett fel.** | Intune kan inte avgöra om du är ansluten till ett godkänt nätverk. Det här felet kan bero på en dålig nätverksanslutning, låg batterinivå, batterisparfunktionsläge eller ett fel på företagsportalen. | Kontrollera att du har bra nätverksmottagning. Inaktivera batterisparfunktionsläge och kontrollera att det återstår minst 30 % batteritid. Försök sedan igen genom att trycka på **Lös**. 

Behöver du fortfarande hjälp? Vi rekommenderar att du kontaktar din företagssupport. Specifika kontaktuppgifter finns på [webbplatsen för företagsportalen](https://portal.manage.microsoft.com/#HelpDeskDialog).
