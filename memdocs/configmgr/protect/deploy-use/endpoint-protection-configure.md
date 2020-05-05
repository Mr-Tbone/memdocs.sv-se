---
title: Konfigurera Endpoint Protection
titleSuffix: Configuration Manager
description: Lär dig hur du konfigurerar Configuration Manager att uppdatera och distribuera definitioner för skadlig kod för Windows Defender.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e48f20dd56f445a10faa485b8bb7e86dbb05f75a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720886"
---
# <a name="configure-endpoint-protection"></a>Konfigurera Endpoint Protection

*Gäller för: Configuration Manager (aktuell gren)*

Innan du kan använda Endpoint Protection för att hantera säkerhet och skadlig kod på Configuration Manager klient datorer måste du utföra de konfigurations steg som beskrivs i den här artikeln.  

## <a name="how-to-configure-endpoint-protection-in-configuration-manager"></a>Konfigurera Endpoint Protection i Configuration Manager  
 Endpoint Protection i Configuration Manager har externa beroenden och beroenden i produkten.  

### <a name="steps-to-configure-endpoint-protection-in-configuration-manager"></a>Steg för att konfigurera Endpoint Protection i Configuration Manager  
 I följande tabell finns anvisningar, detaljerad information och mer information om hur du konfigurerar Endpoint Protection.  

> [!IMPORTANT]  
>  Om du hanterar Endpoint Protection för Windows 10-datorer måste du konfigurera Configuration Manager för att uppdatera och distribuera definitioner av skadlig kod för Windows Defender. Windows Defender ingår i Windows 10 men SCEPInstall måste fortfarande installeras och anpassade klient inställningar för Endpoint Protection (**steg 5** nedan) krävs fortfarande. </br> </br>
> Från och med Configuration Manager 1802 behöver inte Windows 10-enheter ha installerat Endpoint Protection-agenten (SCEPInstall). Om den redan är installerad på Windows 10-enheter kommer Configuration Manager inte att ta bort den. Administratörer kan ta bort Endpoint Protection-agenten på Windows 10-enheter som kör minst 1802-klient versionen. SCEPInstall. exe kanske fortfarande finns i C:\Windows\ccmsetup på vissa datorer men bör inte laddas ned vid nya klient installationer. Anpassade klient inställningar för Endpoint Protection (**steg 5** nedan) krävs fortfarande. <!--503654-->

|Steg|Information|  
|-----------|-------------|  
|**Steg 1:** [skapa en plats system roll för Endpoint Protection Point](endpoint-protection-site-role.md)|Platssystemrollen för Endpoint Protection-platser måste installeras innan du kan använda Endpoint Protection. Den får endast installeras på en platssystemserver och den måste installeras längst upp i hierarkin på en central administrationsplats eller en fristående primär plats. |  
|**Steg 2:** [Konfigurera aviseringar för Endpoint Protection](endpoint-configure-alerts.md)|Aviseringar informerar administratören om specifika händelser har inträffat, till exempel en smitta med skadlig kod. Aviseringar visas i noden **Aviseringar** på arbetsytan **Övervakning** . De kan även skickas till angivna användare. |  
|**Steg 3:** [Konfigurera definitions uppdaterings källor för Endpoint Protection klienter](endpoint-definition-updates.md)|Endpoint Protection kan konfigureras för att använda olika källor för att hämta definitions uppdateringar. |  
|**Steg 4:** [Konfigurera standard principen för program mot skadlig kod och skapa anpassade principer för program mot skadlig kod](endpoint-antimalware-policies.md)|Standard principen för program mot skadlig kod tillämpas när Endpoint Protection-klienten är installerad. Eventuella anpassade principer som du har distribuerat tillämpas som standard inom 60 minuter efter att klienten har distribuerats. Se till att du har konfigurerat principer för program mot skadlig kod innan du distribuerar Endpoint Protection-klienten. |  
|**Steg 5:** [Konfigurera anpassade klient inställningar för Endpoint Protection](endpoint-protection-configure-client.md)|Använd anpassade klient inställningar för att konfigurera Endpoint Protection inställningar för samlingar med datorer i hierarkin.<br /><br /> Obs! Konfigurera inte standard Endpoint Protection klient inställningar om du inte är säker på att du vill att dessa inställningar ska tillämpas på alla datorer i hierarkin. |  
