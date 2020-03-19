---
title: Inställningar för begränsningar för Windows 8.1-enheter i Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Läs vilka Intune-inställningar du kan använda för att kontrollera enhetsinställningar och funktioner på enheter som kör Windows 8.1.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 12/19/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 921d0562211d7cd91b28cbafe2edd71fe37af994
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79361646"
---
# <a name="microsoft-intune-windows-81-device-restriction-settings"></a>Inställningar för begränsningar för Windows 8.1-enheter i Microsoft Intune

I den här artikeln visas inställningarna av enhetsbegränsningar som du kan konfigurera för enheter som kör Windows 8.1.

## <a name="general"></a>Allmänt

- **Sändning av diagnostikdata** – Gör att enheten skickar diagnostikinformation till Microsoft.
- **Brandvägg** – Kräver att Windows-brandväggen är aktiverad.
- **User Account Control** – Kräver användning av UAC (User Account Control) på enheter.

## <a name="password"></a>lösenordsinställning
- **Krav på lösenordstyp** – Kräver att slutanvändaren måste ange ett lösenord för att få åtkomst till enheten.
- **Minsta längd på lösenord** – Konfigurerar den minsta tillåtna längden (i antal tecken) för lösenordet.
- **Antal felaktiga inloggningar innan enheten rensas** – Rensar enheten om inloggningsförsök misslyckas detta antal gånger.
- **Maximalt antal minuter av inaktivitet innan skärmen låses** – Anger antalet minuter en enhet måste vara inaktiv innan det krävs ett lösenord för att låsa upp den.
- **Lösenordets giltighetstid (dagar)** – Anger antal dagar innan lösenordet för enheten måste ändras.
- **Förhindra återanvändning av tidigare lösenord** – Anger om användaren kan konfigurera tidigare använda lösenord.
- **Bildlösenord och PIN-kod** – Gör att det går att använda ett bildlösenord och en PIN-kod. Med ett bildlösenord kan användaren logga in med gester på en bild. Med en PIN-kod kan användaren snabbt logga in med en fyrsiffrig kod.
- **Kryptering** – Kräver att filer på enheten krypteras.<br>Om du vill framtvinga kryptering på enheter som kör Windows 8.1 måste du installera [December 2014 MDM-klientuppdateringen för Windows](https://support.microsoft.com/kb/3013816) på varje enhet.
Om du aktiverar den här inställningen för Windows 8.1-enheter måste alla användare av sådana enheter ha ett Microsoft-konto.
För att krypteringen ska fungera måste enheten uppfylla kraven för [Microsoft InstantGo](https://blogs.windows.com/windowsexperience/2014/06/19/instantgo-a-better-way-to-sleep/#IBHULcTfI4PokO8X.97)-maskinvarucertifiering.
När du framtvingar kryptering på en enhet är återställningsnyckeln enbart tillgänglig från användarens Microsoft-konto, som nås från användarens OneDrive-konto. Du kan inte återställa denna nyckel för en användares räkning. 

## <a name="browser"></a>Webbläsare
- **Autofyll** – Gör att användarna kan ändra inställningarna för att komplettera automatiskt i webbläsaren.
- **Bedrägerivarningar** – Aktiverar eller inaktiverar varningar för webbplatser som kan vara bedrägliga.
- **SmartScreen** – Aktiverar eller inaktiverar varningar för webbplatser som kan vara bedrägliga.
- **JavaScript** – Gör att webbläsaren kan köra skript, till exempel Java-skript.
- **Popup-fönster** – Aktiverar eller inaktiverar webbläsarens blockering av popup-fönster.
- **Skicka Do Not Track-huvuden** – Skickar ett Do Not Track-huvud till besökta webbplatser i Internet Explorer.
- **Plugin-program** – Gör att användarna kan lägga till plugin-program i Internet Explorer.
- **Enstaka ord på intranätsplats** – Gör att det går att använda ett enstaka ord för att dirigera Internet Explorer till en webbplats, t.ex. Bing.
- **Automatisk identifiering av intranätsplats** – Hjälper till att konfigurera säkerheten för intranätsplatser i Internet Explorer.
- **Säkerhetsnivå för Internet** – Anger säkerhetsnivån i Internet Explorer för webbplatser på Internet.
- **Säkerhetsnivå för intranät** – Anger säkerhetsnivån i Internet Explorer för intranätplatser.
- **Säkerhetsnivå för betrodda platser** – Konfigurerar säkerhetsnivån för zonen Betrodda platser.
- **Hög säkerhet för ej tillförlitliga platser** – Konfigurerar säkerhetsnivån för zonen Ej tillförlitliga platser.
- **Menyåtkomst till företagsläge** – Låter användaren komma åt menyalternativen för företagsläget från Internet Explorer.
Om du väljer den här inställningen kan du även ange en **plats för loggningsrapport** som innehåller en URL till en rapport som visar webbplatser som användarna har aktiverat åtkomst till företagsläge för.
- **Plats för webbplatslista för företagsläge** – Anger platsen där listan med webbplatser finns, som ska använda företagsläget när den är aktiv.

## <a name="cellular"></a>Mobilnät
- **Datanätverksväxling** – Gör att det går att använda datanätverksväxling när enheten är i ett mobilnät.

## <a name="cloud-and-storage"></a>Moln och lagring
- **URL till arbetsmappar** – Anger arbetsmappens URL så att dokument kan synkroniseras mellan enheter.
- **Åtkomst till Windows Mail-app utan Microsoft-konto** – Ger åtkomst till Windows Mail utan ett Microsoft-konto.

## <a name="next-steps"></a>Nästa steg

Skapa en profil för enhetsbegränsningar på [Windows 10 och senare](device-restrictions-windows-10.md).
