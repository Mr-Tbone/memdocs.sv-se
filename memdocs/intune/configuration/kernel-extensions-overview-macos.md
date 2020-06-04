---
title: Skapa systemtillägg och kerneltillägg i macOS med Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Lägg till eller skapa en macOS-enhetsprofil och konfigurerar systemtillägg eller kerneltillägg för att tillåta användaråsidosättning, lägga till teamidentifierare och lägga till en paket- och teamidentifierare i Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/07/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: fce8218c9f8fb8757f0aef892f0854f1c386a8bd
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990300"
---
# <a name="add-macos-system-and-kernel-extensions-in-intune"></a>Lägga till systemtillägg och kerneltillägg i macOS i Intune

> [!NOTE]
> macOS kernel-tillägg håller på att ersättas med systemtillägg. Mer information finns i [Supporttips: Användning av systemtillägg i stället för kernel-tillägg för macOS Catalina 10.15 i Intune](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-using-system-extensions-instead-of-kernel-extensions/ba-p/1191413).

På macOS-enheter kan du lägga till kerneltillägg och systemtillägg. Med både kerneltillägg och systemtillägg kan användare installera apptillägg som utökar de inbyggda funktionerna i operativsystemet. Kerneltillägg kör sin kod på kernelnivå. Systemtillägg körs i ett noga kontrollerat användarutrymme.

Använd Microsoft Intune när du vill lägga till tillägg som alltid får läsas in på dina enheter. Intune använder ”konfigurationsprofiler” till att skapa och anpassa inställningarna efter din organisations behov. När du har lagt till de här funktionerna i en profil kan du push-överföra eller distribuera profilen till macOS-enheter i din organisation.

I den här artikeln beskrivs systemtillägg och kerneltillägg. Dessutom beskrivs hur du skapar en enhetskonfigurationsprofil med hjälp av tillägg i Intune.

## <a name="system-extensions"></a>Systemtillägg

Systemtillägg körs i användarmiljön och har inte tillgång till kerneln. Målet är att öka säkerheten, ge användaren mer kontroll och begränsa attacker på kernelnivå. Här är några exempel på sådana tillägg:

- Drivrutinstillägg som drivrutiner för USB, nätverkskort (NIC), seriestyrenheter och gränssnittsenheter (HID)
- Nätverkstillägg som innehållsfilter, DNS-proxyservrar och VPN-klienter
- Endpoint Security-tillägg som slutpunktsidentifiering, slutpunktssvar och antivirus

Systemtilläggen ingår paketet för en app och installeras från appen.

Mer information om systemtillägg finns i [Systemtillägg](https://developer.apple.com/documentation/systemextensions) (öppnar Apples webbplats).

## <a name="kernel-extensions"></a>Kerneltillägg

Kerneltillägg lägger till funktioner på kernelnivå. Dessa funktioner kommer åt delar av operativsystemet som vanliga program inte har åtkomst till. Din organisation kan ha särskilda behov eller krav som inte är tillgängliga i en app, en enhetsfunktion och så vidare.

Till exempel har du ett antivirusprogram som söker igenom enheten efter skadligt innehåll. Du kan lägga till det här antivirusprogrammets kerneltillägg som ett tillåtet kerneltillägg i Intune. Sedan "assign" (tilldelar) du tillägget till dina macOS-enheter.

Med den här funktionen kan administratörer tillåta att användare åsidosätter kerneltillägg, lägger till teamidentifierare och lägger till specifika kerneltillägg i Intune.

Mer information om kerneltillägg finns i [Kerneltillägg](https://developer.apple.com/library/archive/documentation/Darwin/Conceptual/KernelProgramming/Extend/Extend.html) (öppnar Apple-webbplatsen).

## <a name="prerequisites"></a>Krav

- Den här funktionen gäller för:

  - macOS 10.13.2 eller senare (kerneltillägg)
  - macOS 10.15 eller senare (systemtillägg)

  Från macOS 10.15 till macOS 10.15.4 kan du köra kerneltillägg och systemtillägg tillsammans.

- För användning av den här funktionen måste enheterna vara:

  - Registrerade i Intune med hjälp av Apple-programmet för enhetsregistrering (DEP). Mer information finns i [Registrera macOS-enheter automatiskt](../enrollment/device-enrollment-program-enroll-macos.md).

    ELLER

  - Registrerade i Intune med "user approved enrollment" (användargodkänd registrering, term från Apple). Mer information finns i [Förbered för ändringar av kerneltillägg i macOS High Sierra](https://support.apple.com/en-us/HT208019) (öppnar Apple-webbplatsen).

## <a name="what-you-need-to-know"></a>Vad du behöver veta

- Du kan lägga till osignerade äldre kerneltillägg och systemtillägg.
- Se till att ange rätt teamidentifierare och paket-ID för tillägget. Intune validerar inte de värden som du anger. Om du anger fel information fungerar inte tillägget på enheten. En teamidentifierare består av exakt 10 alfanumeriska tecken.

> [!NOTE]
> Apple har publicerat information om signering och notarisering för all programvara. I macOS 10.14.5 och senare behöver kerneltillägg som distribueras via Intune inte uppfylla Apples notariseringsprincip.
>
> Information om den här notariseringsprincipen och eventuella uppdateringar eller ändringar finns i följande resurser:
>
> - [Notarisera din app före distribution](https://developer.apple.com/documentation/security/notarizing_your_app_before_distribution) (öppnar Apple-webbplatsen) 
> - [Förbered för ändringar av kerneltillägg i macOS High Sierra](https://support.apple.com/en-us/HT208019) (öppnar Apple-webbplatsen)

## <a name="create-the-profile"></a>Skapa profilen

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj **Enheter** > **Konfigurationsprofiler** > **Skapa profil**.
3. Ange följande egenskaper:

    - **Plattform**: Välj **macOS**
    - **Profil**: Välj **Tillägg**.

4. Välj **Skapa**.
5. Ange följande egenskaper i **Grundinställningar**:

    - **Namn**: Ange ett beskrivande namn på principen. Namnge dina principer så att du enkelt kan identifiera dem senare. Till exempel är ett användbart principnamn **macOS: Lägg till antivirusgenomsökning i kerneltillägg på enheter**.
    - **Beskrivning**: Ange en beskrivning av principen. Denna inställning är valfri, men rekommenderas.

6. Välj **Nästa**.

7. I **Konfigurationsinställningar** konfigurerar du inställningarna:

    - [macOS](kernel-extensions-settings-macos.md)

8. Välj **Nästa**.
9. Under **Omfångstaggar** (valfritt), tilldelar du en tagg för att filtrera profilen till specifika IT-grupper, till exempel `US-NC IT Team` eller `JohnGlenn_ITDepartment`. Mer information om omfångstaggar finns i [Använda RBAC och omfångstaggar för distribuerad IT](../fundamentals/scope-tags.md).

    Välj **Nästa**.

10. Under **Tilldelningar**väljer du de användare eller grupper som ska ta emot din profil. Mer information om hur du tilldelar profiler finns i [Tilldela användar- och enhetsprofiler](device-profile-assign.md).

    Välj **Nästa**.

11. Granska inställningarna under **Granska + skapa**. När du väljer **Skapa** sparas dina ändringar och profilen tilldelas. Principen visas också i profillistan.

## <a name="next-steps"></a>Nästa steg

När profilen har skapats är den klar att tilldelas. [Tilldela profilen](device-profile-assign.md) och [övervaka dess status](device-profile-monitor.md).
