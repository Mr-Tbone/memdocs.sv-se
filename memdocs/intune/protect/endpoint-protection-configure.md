---
title: Konfigurera inställningar för slutpunktsskydd i Microsoft Intune – Azure | Microsoft Docs
description: Skapa inställningar för slutpunktsskydd när du skapar en profil för macOS- eller Windows 10-enheter i Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/24/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
mr.reviewer: karthib
ms.openlocfilehash: 6b5d0f88222c8d48da4f91ff3cf8d4628ccb179d
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "80551582"
---
# <a name="add-endpoint-protection-settings-in-intune"></a>Lägga till inställningar för slutpunktsskydd i Intune

Med Intune kan du använda profiler för enhetskonfiguration för att hantera vanliga säkerhetsfunktioner för slutpunkter på enheter, inklusive:

- Brandvägg
- BitLocker
- Tillåta och blockera appar
- Microsoft Defender och kryptering

Du kan till exempel skapa en profil för slutpunktsskydd som endast tillåter att macOS-användare installerar appar från Mac App Store. Du kan också aktivera Windows SmartScreen när appar körs på Windows 10-enheter.

Innan du skapar en profil ska du läsa följande artiklar om de inställningar för skydd av slutpunkter som Intune kan hantera för varje plattform som stöds:

- [Inställningar för macOS](endpoint-protection-macos.md)
- [Inställningar för Windows 10](endpoint-protection-windows-10.md)

> [!NOTE]
> Användargränssnittet i Intune uppdateras till en helskärmsupplevelse och kan ta flera veckor. Innan klienten får den här uppdateringen får du ett något annorlunda arbetsflöde när du skapar eller redigerar de inställningar som beskrivs i den här artikeln.

## <a name="create-a-device-profile-containing-endpoint-protection-settings"></a>Skapa en enhetsprofil med inställningar för slutpunktsskydd

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Välj **Enheter** > **Konfigurationsprofiler** > **Skapa profil**.

3. Ange följande egenskaper:

    - **Plattform**: Välj plattform för dina enheter. Alternativen är:

        - **macOS**
        - **Windows 10 och senare**

    - **Profil**: Välj **Endpoint Protection**.

4. Välj **Skapa**.
5. Ange följande egenskaper i **Grundinställningar**:

    - **Namn**: Ange ett beskrivande namn på principen. Namnge dina principer så att du enkelt kan identifiera dem senare. Till exempel är ett användbart principnamn **macOS: Endpoint Protection-profil som konfigurerar brandväggen för alla macOS-enheter**.
    - **Beskrivning**: Ange en beskrivning av principen. Denna inställning är valfri, men rekommenderas.

6. Välj **Nästa**.

7. Under **Konfigurationsinställningar**  visas olika inställningar som du kan konfigurera beroende på vilken plattform du väljer. Välj din plattform för detaljerade inställningar:

   - [Inställningar för macOS](endpoint-protection-macos.md)
   - [Inställningar för Windows 10](endpoint-protection-windows-10.md)

8. Välj **Nästa**.
9. Under **Omfångstaggar** (valfritt), tilldelar du en tagg för att filtrera profilen till specifika IT-grupper, till exempel `US-NC IT Team` eller `JohnGlenn_ITDepartment`. Mer information om omfångstaggar finns i [Använda RBAC och omfångstaggar för distribuerad IT](../fundamentals/scope-tags.md).

    Välj **Nästa**.

10. Under **Tilldelningar**väljer du de användare eller grupper som ska ta emot din profil. Mer information om hur du tilldelar profiler finns i [Tilldela användar- och enhetsprofiler](../configuration/device-profile-assign.md).

    Välj **Nästa**.

11. Granska inställningarna under **Granska + skapa**. När du väljer **Skapa** sparas dina ändringar och profilen tilldelas. Principen visas också i profillistan.

## <a name="add-custom-firewall-rules-for-windows-10-devices"></a>Lägga till anpassade brandväggsregler för Windows 10-enheter

När du konfigurerar Microsoft Defender-brandväggen som en del av en profil som innehåller Endpoint Protection-regler för Windows 10 kan du konfigurera anpassade regler för brandväggar. Med anpassade regler kan du utöka den fördefinierade uppsättningen brandväggsregler som stöds för Windows 10.

När du planerar profiler med anpassade brandväggsregler bör du tänka på följande information, som kan påverka hur du väljer att gruppera brandväggsregler i dina profiler:

- Varje profil har stöd för upp till 150 brandväggsregler. Om du använder mer än 150 regler skapar du ytterligare profiler, var och en med högst 150 regler.

- För varje profil gäller att om en enskild regel inte kan tillämpas, så misslyckas alla regler i profilen och ingen av reglerna tillämpas på enheten.

- När en regel inte kan tillämpas rapporteras alla regler i profilen som misslyckade. Intune kan inte identifiera vilken enskild regel som misslyckades.  

De brandväggsregler som Intune kan hantera beskrivs i avsnittet om [konfigurationstjänstprovidern (CSP) för Windows-brandväggen](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp). Om du vill granska listan med anpassade brandväggsinställningar för Windows 10-enheter som stöds av Intune läser du avsnittet om [anpassade brandväggsregler](endpoint-protection-windows-10.md#firewall-rules).

### <a name="to-add-custom-firewall-rules-to-an-endpoint-protection-profile"></a>Så här lägger du till anpassade brandväggsregler i en profil för slutpunktsskydd

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Välj **Enheter** > **Konfigurationsprofiler** > **Skapa profil**.

3. För *Plattform* väljer du **Windows 10 och senare** och sedan *Slutpunktsskydd* för **Profil**.

    Välj **Skapa**.

4. Ange ett **namn** för profilen >**Nästa**.
5. I **Konfigurationsinställningar** väljer du **Microsoft Defender-brandväggen**. För *Brandväggsregler* väljer du **Lägg till** för att öppna **sidan Skapa regel**.

6. Ange inställningar för brandväggsregeln och välj sedan **OK** för att spara den. Information om vilka alternativ som finns tillgängliga för anpassade brandväggsregler finns i avsnittet om [anpassade brandväggsregler](endpoint-protection-windows-10.md#firewall-rules).

    1. Regeln visas på sidan för *Microsoft Defender-brandväggen* i listan över regler.
    2. Om du vill ändra en regel väljer du regeln i listan för att öppna sidan **Redigera regel**.
    3. Om du vill ta bort en regel från en profil väljer du ellipsen **(...)** för regeln och väljer sedan **Ta bort**.
    4. Om du vill ändra visningsordningen för regler väljer du ikonen för *uppil, nedpil* längst upp i regellistan.

7. Välj **Nästa** tills du kommer till **Granska + skapa**. När du väljer **Skapa** sparas dina ändringar och profilen tilldelas. Principen visas också i profillistan.

## <a name="next-steps"></a>Nästa steg

Profilen skapas, men den kanske inte gör något än. [Tilldela profilen](../configuration/device-profile-assign.md) och [övervaka dess status](../configuration/device-profile-monitor.md).
