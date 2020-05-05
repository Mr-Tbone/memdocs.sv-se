---
title: Säkerhet och sekretess för Wi-Fi-och VPN-profil
titleSuffix: Configuration Manager
description: Lär dig mer om säkerhets rekommendationer för att hantera Wi-Fi-och VPN-profiler för enheter i Configuration Manager.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ef3ab519-9cf7-47fc-8831-d400e0e96df8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a6f444e35e16a3b42414fdc6fbee50687cf76f2f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722069"
---
# <a name="security-and-privacy-for-wi-fi-and-vpn-profiles-in-configuration-manager"></a>Säkerhet och sekretess för Wi-Fi-och VPN-profiler i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

## <a name="security-recommendations"></a>Säkerhetsrekommendationer

Använd följande rekommenderade säkerhets metoder när du hanterar Wi-Fi-och VPN-profiler för enheter.

### <a name="choose-the-most-secure-options-that-your-wi-fi-and-vpn-infrastructure-and-client-operating-systems-can-support"></a>Välj de säkraste alternativ som din Wi-Fi-och VPN-infrastruktur och klient operativ system har stöd för

Wi-Fi-och VPN-profiler är ett bekvämt sätt att centralt distribuera och hantera Wi-Fi-och VPN-inställningar som dina enheter redan stöder. Configuration Manager lägger inte till Wi-Fi-eller VPN-funktioner. Identifiera, implementera och följ eventuella säkerhets rekommendationer för dina enheter och din infrastruktur.

## <a name="privacy-information"></a>Sekretess information

Du kan använda Wi-Fi-och VPN-profiler för att konfigurera klient enheter för att ansluta till Wi-Fi-och VPN-servrar. Använd sedan Configuration Manager för att utvärdera om enheterna blir kompatibla när profilerna har tillämpats. Hanteringsplatsen skickar uppfyllelseinformation till platsservern, och informationen lagras i platsdatabasen. Informationen är krypterad när enheterna skickar den till hanterings platsen, men den lagras inte i krypterat format i plats databasen. Informationen sparas i databasen tills platsunderhållsuppgiften **Ta bort föråldrade data för Configuration Manager** tar bort den. Standardintervallet för borttagning är 90 dagar, men du kan ändra det. Kompatibilitetsinformation skickas inte till Microsoft.

Som standard utvärderar enheterna inte Wi-Fi-och VPN-profiler. Dessutom måste du konfigurera profilerna och sedan distribuera dem till användarna.  

Innan du konfigurerar Wi-Fi-eller VPN-profiler bör du tänka igenom dina sekretess krav.  
