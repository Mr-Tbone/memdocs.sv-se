---
title: Tilldela enhetsprofiler i Microsoft Intune – Azure | Microsoft Docs
description: Använd administrationscentret för Microsoft Endpoint Manager för att tilldela enhetsprofiler och principer till användare och enheter. Lär dig att undanta grupper från en profiltilldelning i Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: f6f5414d-0e41-42fc-b6cf-e7ad76e1e06d
ms.reviewer: altsou
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 08d53bd7ffedc2679fca675b88e021301d15fb62
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989017"
---
# <a name="assign-user-and-device-profiles-in-microsoft-intune"></a>Tilldela användar- och enhetsprofiler i Microsoft Intune

Du skapar en profil som innehåller alla inställningar som du har angett. Nästa steg är att distribuera eller ”tilldela” profilen till din användare eller dina enhetsgrupper i Azure Active Directory (Azure AD). När den är tilldelad får användarna och enheterna din profil och de inställningar som du har angett tillämpas.

Den här artikeln visar hur du tilldelar en profil, samt innehåller information om hur du använder omfångstaggar på dina profiler.

> [!NOTE]  
> När en profil tas bort eller inte längre är tilldelad till en enhet kan olika saker hända, beroende på inställningarna i profilen. Inställningarna baseras på konfigurationstjänstprovider och varje konfigurationstjänstprovider kan hantera borttagningen av profilen på olika sätt. En inställning kan till exempel behålla det befintliga värdet och inte återgå till ett standardvärde. Beteendet styrs av varje konfigurationstjänstprovider i operativsystemet. En lista över Windows-konfigurationstjänstprovider finns i [referensen för konfigurationstjänstprovider](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference).
>
> Om du vill ändra en inställning till ett annat värde skapar du en ny profil, konfigurerar inställningen som **Inte konfigurerad** och tilldelar profilen. När inställningen har tillämpats bör användarna ha kontroll över att ändra den till deras önskade värde.
>
> När du konfigurerar de här inställningarna rekommenderar vi att du distribuerar till en pilotgrupp. Mer information om Intune-distribution finns i [Skapa en distributionsplan](../fundamentals/planning-guide-rollout-plan.md).

## <a name="before-you-begin"></a>Innan du börjar

Se till att du har rätt roll för att tilldela principer. Mer information finns i [Rollbaserad åtkomstkontroll (RBAC) med Microsoft Intune](../fundamentals/role-based-access-control.md).

## <a name="assign-a-device-profile"></a>Tilldela en enhetsprofil

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj **Enheter** > **Konfigurationsprofiler**. Alla profilerna visas i listan.
3. Välj den profil som du vill tilldela > **Tilldelningar**.
4. Välj om du vill **inkludera** eller **exkludera** grupper och välj sedan grupperna. När du väljer dina grupper väljer du en Azure AD-grupp. Håll ned **Ctrl**-tangenten om du vill markera flera grupper.

    :::image type="content" source="./media/device-profile-assign/group-include-exclude.png" alt-text="Skärmbild med alternativ för att inkludera eller exkludera grupper från en profiltilldelning i Microsoft Intune":::

5. **Spara** ändringarna.

### <a name="evaluate-how-many-users-are-targeted"></a>Utvärdera hur många användare som omfattas

När du tilldelar profilen kan du också **utvärdera** hur många användare som påverkas. Den här funktionen beräknar användare, den beräknar inte enheter.

1. I administrationscentret väljer du **Enheter** > **Konfigurationsprofiler**.
2. Välj en profil > **Tilldelningar** > **Utvärdera**. Ett meddelande visas med hur många användare som omfattas av profilen.

Om knappen **Utvärdera** är nedtonad, kontrollerar du att profilen har tilldelats till en eller flera grupper.

## <a name="use-scope-tags-or-applicability-rules"></a>Använd omfångstaggar eller tillämpbarhetsregler

När du skapar eller uppdaterar en profil, kan du också lägga till omfångstaggar och tillämpbarhetsregler i profilen.

**Omfångstaggar** kan användas till att filtrera profiler till vissa IT-grupper, till exempel `US-NC IT Team` eller `JohnGlenn_ITDepartment`. Mer information finns i [Använda RBAC och omfångstaggar för distribuerad IT](../fundamentals/scope-tags.md).

På Windows 10-enheter kan du lägga till **tillämpbarhetsregler** så att profilen endast gäller för en speciell OS-version eller en speciell Windows-version. [Tillämpbarhetsregler](device-profile-create.md#applicability-rules) innehåller mer information.

## <a name="user-groups-vs-device-groups"></a>Användargrupper jämfört med enhetsgrupper

Många användare undrar när de ska använda användargrupper och när de ska använda enhetsgrupper. Svaret är att det beror på ditt mål. Här är några riktlinjer som hjälper dig att komma igång.

### <a name="device-groups"></a>Enhetsgrupper

Om du vill tillämpa inställningar på en enhet, oavsett vem som är inloggad, tilldelar du dina profiler till en enhetsgrupp. Inställningar som tillämpas på enhetsgrupper följer alltid med enheten, inte användaren.

Exempel:

- Enhetsgrupper är användbara för att hantera enheter som inte har en dedikerad användare. Om du till exempel har enheter som skriver ut biljetter, skannar lager, delas av skiftarbetare, tilldelas ett särskilt lager och så vidare. Placera dessa enheter i en enhetsgrupp och tilldela dina profiler till den här enhetsgruppen.

- Du skapar en [Intune-profil för enhetskonfigurationsgränssnitt (DFCI)](device-firmware-configuration-interface-windows.md) som uppdaterar inställningarna i BIOS. Du kan till exempel konfigurera den här profilen så att den låser enhetskameran eller startalternativen för att hindra användare från att starta ett annat operativsystem. Den här profilen är ett utmärkt scenario för att tilldela till en enhetsgrupp.

- På vissa Windows-enheter vill du alltid kunna kontrollera vissa inställningar för Microsoft Edge, oavsett vem som använder enheten. Du vill till exempel blockera alla hämtningar, begränsa alla cookies till den aktuella webbläsarsessionen och ta bort webbhistoriken. I det här scenariot sätter du in dessa Windows-enheter i en enhetsgrupp. Skapa sedan en [Administrativ mall i Intune](administrative-templates-windows.md), lägg till dessa enhetsinställningar och tilldela sedan profilen till enhetsgruppen.

För att sammanfatta använder du enhetsgrupper när du inte bryr dig om vem som är inloggad på enheten eller om någon är inloggad alls. Du vill att inställningarna alltid ska finnas på enheten.

### <a name="user-groups"></a>Användargrupper

Profilinställningar som tillämpas på användargrupper följer alltid med användaren och går sedan till användaren när de loggar in på olika enheter. Det är vanligt att användare har många enheter, till exempel en Surface Pro för arbete och en personlig iOS/iPadOS-enhet. Och det är vanligt att en person får åtkomst till e-post och andra organisationsresurser från dessa enheter.

Exempel:

- Du vill placera en supportikon för alla användare på alla enheter. I det här scenariot ska du placera dessa användare i en användargrupp och tilldela din supportikonprofil till den här användargruppen.
- En användare får en ny enhet som tillhör organisationen. Användaren loggar in på enheten med sitt domän konto. Enheten registreras automatiskt i Azure AD och hanteras automatiskt av Intune. Den här profilen är ett utmärkt scenario för att tilldela till en användargrupp.
- När en användare loggar in på en enhet vill du kontrollera funktioner i apparna, till exempel OneDrive eller Office. I det här scenariot tilldelar du inställningarna för OneDrive- eller Office-profilen till en användargrupp.

  Du vill kanske blockera obetrodda ActiveX-kontroller i dina Office-appar. Du kan sedan skapa en [Administrativ mall i Intune](administrative-templates-windows.md), konfigurera den här inställningen och tilldela sedan profilen till enhetsgruppen.

Sammanfattningsvis använder du användargrupper när du vill att dina inställningar och regler ska följa med användaren, oavsett vilken enhet de använder.

## <a name="exclude-groups-from-a-profile-assignment"></a>Exkludera grupper från en profiltilldelning

Med hjälp av Intunes profiler för enhetskonfiguration kan du inkludera och exkludera grupper från profiltilldelningen.

Vi rekommenderar att du skapar och tilldelar profiler som är specifika för dina användargrupper. Du kan även skapa och tilldela olika profiler specifikt för dina enhetsgrupper. Mer information om grupper finns i [Lägga till grupper för att organisera användare och enheter](../fundamentals/groups-add.md).

När du tilldelar profilerna använder du följande tabell till att inkludera och exkludera grupper. En bockmarkering innebär att tilldelningen stöds:

:::image type="content" source="./media/device-profile-assign/include-exclude-user-device-groups.png" alt-text="Alternativ som stöds för att inkludera eller exkludera grupper från en profiltilldelning":::

### <a name="what-you-should-know"></a>Det här bör du veta

- Undantag har företräde framför inkludering i följande scenarier för grupptyper:

  - Inkludera och exkludera användargrupper
  - Inkludera och exkludera enhetsgrupper

  Du kan t.ex. tilldela en enhetsprofil till användargruppen **Alla företagsanvändare** men välja att exkludera medlemmar i användargruppen **Ledningsgrupp**. Eftersom båda grupperna är användargrupper får **Alla företagsanvändare** förutom **Ledningsgrupp** profilen.

- Intune utvärderar inte grupprelationer från användare till enhet. Om du tilldelar profiler till blandade grupper, kanske resultatet inte blir det du vill ha eller förväntar dig.

  Du kan till exempel tilldela en enhetsprofil till användargruppen **Alla användare**, men undanta enhetsgruppen **Alla personliga enheter**. I den här blandade grupprofiltilldelningen får **Alla användare** profilen. Undantaget tillämpas inte.

  Därför rekommenderar vi inte att du tilldelar profiler till blandade grupper.

## <a name="next-steps"></a>Nästa steg

Se avsnittet om att [övervaka enhetsprofiler](device-profile-monitor.md) för anvisningar om hur du övervakar dina profiler och de enheter som kör dina profiler.
