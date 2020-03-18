---
title: Konfigurera inställningar för slutpunktsskydd i Microsoft Intune – Azure | Microsoft Docs
description: Skapa inställningar för slutpunktsskydd när du skapar en profil för macOS- eller Windows 10-enheter i Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/18/2019
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
ms.openlocfilehash: 64a11cf9dca110a4a802ddff3e9176ec1ce88345
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79352182"
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

## <a name="create-a-device-profile-containing-endpoint-protection-settings"></a>Skapa en enhetsprofil med inställningar för slutpunktsskydd

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Välj **Enheter** > **Konfigurationsprofiler** > **Skapa profil**.

3. Ange **Namn** och **Beskrivning** för slutpunktsskyddsprofilen.

4. Välj den enhetsplattform på vilken du vill tillämpa anpassade inställningar från listrutan **Plattform**. För närvarande kan du välja någon av följande plattformar för inställning av enhetsbegränsningar:

   - **macOS**
   - **Windows 10 och senare**

5. Välj **Endpoint Protection** i listrutan **Profiltyp**.

6. Vilka inställningar du kan konfigurera varierar beroende på vilken plattform du väljer. Se:

   - [Inställningar för macOS](endpoint-protection-macos.md)
   - [Inställningar för Windows 10](endpoint-protection-windows-10.md)

7. När du har konfigurerat tillämpliga inställningar väljer du **Skapa** på sidan **Skapa profil**.

   Profilen skapas och visas på sidan med profillistan. Om du vill tilldela profilen till grupper kan du läsa [Tilldela enhetsprofiler](../configuration/device-profile-assign.md).

## <a name="add-custom-firewall-rules-for-windows-10-devices"></a>Lägga till anpassade brandväggsregler för Windows 10-enheter

När du konfigurerar Microsoft Defender-brandväggen som en del av en profil som innehåller Endpoint Protection-regler för Windows 10 kan du konfigurera anpassade regler för brandväggar. Med anpassade regler kan du utöka den fördefinierade uppsättningen brandväggsregler som stöds för Windows 10.

När du planerar profiler med anpassade brandväggsregler bör du tänka på följande information, som kan påverka hur du väljer att gruppera brandväggsregler i dina profiler:

- Varje profil har stöd för upp till 150 brandväggsregler. Om du använder mer än 150 regler skapar du ytterligare profiler, var och en med högst 150 regler.

- För varje profil gäller att om en enskild regel inte kan tillämpas, så misslyckas alla regler i profilen och ingen av reglerna tillämpas på enheten.

- När en regel inte kan tillämpas rapporteras alla regler i profilen som misslyckade. Intune kan inte identifiera vilken enskild regel som misslyckades.  

De brandväggsregler som Intune kan hantera beskrivs i avsnittet om [konfigurationstjänstprovidern (CSP) för Windows-brandväggen]( https://docs.microsoft.com/windows/client-management/mdm/firewall-csp). Om du vill granska listan med anpassade brandväggsinställningar för Windows 10-enheter som stöds av Intune läser du avsnittet om [anpassade brandväggsregler](endpoint-protection-windows-10.md#firewall-rules).

### <a name="to-add-custom-firewall-rules-to-an-endpoint-protection-profile"></a>Så här lägger du till anpassade brandväggsregler i en profil för slutpunktsskydd

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Välj **Enheter** > **Konfigurationsprofiler** > **Skapa profil**.

3. För *Plattform* väljer du **Windows 10 och senare** och sedan *Slutpunktsskydd* för **Profiltyp**.

4. Välj **Microsoft Defender-brandväggen** för att öppna konfigurationssidan och välj sedan **Lägg till** för *Brandväggsregler* för att öppna sidan **Skapa regel**.

5. Ange inställningar för brandväggsregeln och välj sedan **OK** för att spara den. Information om vilka alternativ som finns tillgängliga för anpassade brandväggsregler finns i avsnittet om [anpassade brandväggsregler](endpoint-protection-windows-10.md#firewall-rules).

6. När du har sparat regeln visas den på sidan för *Microsoft Defender-brandväggen* i listan över regler.

7. Om du vill ändra en regel väljer du regeln i listan för att öppna sidan **Redigera regel**.

8. Om du vill ta bort en regel från en profil väljer du ellipsen **(...)** för regeln och väljer sedan **Ta bort**.

9. Om du vill ändra visningsordningen för regler väljer du ikonen för *uppil, nedpil* längst upp i regellistan.

## <a name="next-steps"></a>Nästa steg

Om du vill tilldela profilen till grupper kan du läsa mer i [Tilldela enhetsprofiler](../configuration/device-profile-assign.md).
