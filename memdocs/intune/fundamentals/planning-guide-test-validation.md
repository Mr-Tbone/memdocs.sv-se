---
title: Testning och validering av Intune
titleSuffix: Microsoft Intune
description: Så här testar och verifierar du den molnbaserade Intune-lösningen i din miljö.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 3/22/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 4f82ee0c-4bd6-4623-9b10-9249d316ccf5
ms.reviewer: jeffbu, cgerth
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: aeca72af3eadf55174f1ad97c1e294f48f131801
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "79357239"
---
# <a name="intune-testing-and-validation"></a>Testning och validering av Intune

När du testar implementeringen av Microsoft Intune, bör du fundera över funktionell verifiering och användningsbaserad verifiering. Funktionell validering består av testa varje komponent och konfiguration för att se om de fungerar korrekt. Den användningsbaserade verifieringen inbegriper tester för att verifiera att de scenarier som omfattar en serie aktiviteter fungerar som förväntat. 

Vi rekommenderar att du involverar IT-supporten och annan supportpersonal i testningsfasen så att supportdokumentation kan tas fram, och så att de känner sig trygga med att ge support för produkten. Om en komponent eller ett scenario inte fungerar baserat på användningsfallen, dokumenterar du de ändringar som krävs och beskriver orsaken till ändringen.

## <a name="before-you-begin"></a>Innan du börjar

Vi rekommenderar att du dokumenterar följande:

- **Testkriterier:** Identifiera de referensvärden som testningen ska mätas mot.

- **Designkomponenter:** Måste finnas i minst ett testningskriterium.

Om en designkomponent inte finns i minst ett testningskriterium som är knutet till ett krav eller scenario bör du överväga om designkomponenten är nödvändig eller inte. Se även till att ha följande poster:

- **Konton:** Testkonton som licensierats för EMS och Office 365 för att kunna testa alla användningsfallsscenarier.

- **Enheter:** Testenheter som kan rensas eller återställas till fabriksinställningarna.

- **Integrationskomponenter:** Alla integrationskomponenter (certifikatanslutningsappar och den lokala Intune Exchange-anslutningsappen) ska installeras och konfigureras om det behövs.

Designändringar kan krävas i händelse av oförutsedda problem. Dessutom bör alla ändringar dokumenteras fullständigt med orsaken för varje ändring. Här visas ett exempel som illustrerar vad en ändring kan vara:

<blockquote>Du kanske upptäcker att du inte uppfyller kraven för Network Device Enrollment Service (NDES), och du inser också att VPN- och Wi-Fi-profiler kan konfigureras med en rotcertifikatutfärdare som uppfyller samma krav utan en NDES-implementering.</blockquote>

Du kanske ställs inför utmaningar eller problem som kräver teknisk hjälp eller särskild felsökning under testnings- och valideringsprocessen. Vi rekommenderar att du ber om hjälp via Microsofts supportkanaler.

- [Så här får du support för Intune](get-support.md)

- [Kontakta telefonsupporten för Microsoft Intune](get-support.md)

## <a name="functional-validation-testing"></a>Funktionell valideringstestning

Funktionell validering består av testa varje komponent och konfiguration för att se om de fungerar korrekt. Ett exempel på valideringstestning visas i tabellen nedan.

![Avsnitt 9 tabell 1](./media/planning-guide-test-validation/section-9-image-1-table.PNG)

## <a name="use-case-validation-testing"></a>Valideringstestning för användningsfall

Kör valideringstestning för användningsfall för att bekräfta att scenarierna är fullständiga och funktionella. Det finns två typer av användningsfall: IT-administratör och slutanvändare.

### <a name="it-admin"></a>IT-administratör

Kör valideringstestning för IT-administratörer för att bekräfta att administrativa åtgärder som utförs på en enhet eller användare fungerar korrekt. Nedan är ett exempel på ett valideringsscenario från slutpunkt till slutpunkt för IT-administratörer.

![Avsnitt 9 tabell 2](./media/planning-guide-test-validation/section-9-image-2-table.PNG)

### <a name="end-user"></a>Slutanvändare

Kör valideringstestning för slutanvändare för att kontrollera att slutanvändarupplevelsen är som förväntat och att den presenteras korrekt i all användarkommunikation. Det är viktigt att verifiera att slutanvändarupplevelsen är korrekt. Om du inte verifierar slutanvändarupplevelsen kan det leda till lägre integreringsfrekvens av användarna och fler supportsamtal.

![Avsnitt 9 tabell 3](./media/planning-guide-test-validation/section-9-image-3-table.PNG)

## <a name="next-steps"></a>Nästa steg

Nu när du har testat och validerat Intunes funktionella scenarier och användningsfall är du redo att [distribuera Intune i produktionsmiljön](planning-guide-rollout-plan.md).

Fler planeringsmallar och mer information finns i [Fler resurser](planning-guide-resources.md).
