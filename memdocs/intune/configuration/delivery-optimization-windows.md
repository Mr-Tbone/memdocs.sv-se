---
title: Leveransoptimeringsinställningar för Windows 10 i Microsoft Intune – Azure | Microsoft Docs
description: Konfigurera hur Windows 10-enheter du hanterar med Intune använder leveransoptimering. Skapa en enhetskonfigurationsprofil i Intune med vilken du kan installera uppdateringar från Internet. Se även hur du kan ersätta befintliga uppdateringsringar med en leveransoptimeringsprofil.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: kerimh
ms.openlocfilehash: 3ffef32f4f33e79b25145dd4c0257b8a5bcfd32a
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88913774"
---
# <a name="delivery-optimization-settings-in-microsoft-intune"></a>Inställningar för leveransoptimering i Microsoft Intune

Med Intune kan du använda inställningar för leveransoptimering till dina Windows 10-enheter för att minska bandbreddsförbrukningen när enheterna laddar ned program och uppdateringar. Konfigurera leveransoptimering som en del av dina enhetskonfigurationsprofiler.  

I den här artikeln beskrivs hur du konfigurerar inställningar för leveransoptimering som en del av en enhetskonfigurationsprofil. När du har skapat en profil tilldelar eller distribuerar du profilen till Windows 10-enheterna.

Du kan se en lista med de inställningar för leveransoptimering som Intune ha stöd för i [Inställningar för leveransoptimering för Intune](delivery-optimization-settings.md).  

Information om leveransoptimering i Windows 10 finns i [Uppdateringar av leveransoptimering](/windows/deployment/update/waas-delivery-optimization) i Windows-dokumentationen.  

## <a name="create-the-profile"></a>Skapa profilen

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Välj **Enheter** > **Konfigurationsprofiler** > **Skapa profil**.

3. Ange följande egenskaper:

   - **Plattform**: Välj **Windows 10 och senare**.
   - **Profil**: Välj **Leveransoptimering**.

4. Välj **Skapa**.

5. Ange följande egenskaper i **Grundinställningar**:

   - **Namn**: Ange ett beskrivande namn på den nya profilen.
   - **Beskrivning**: Ange en beskrivning av profilen. Denna inställning är valfri, men rekommenderas.

6. Välj **Nästa**.

7. På sidan **Konfigurationsinställningar** anger du hur du vill att uppdateringar och appar ska laddas ned. Information om tillgängliga inställningar finns i [Inställningar för leveransoptimering för Intune](delivery-optimization-settings.md).

   När du har konfigurerat inställningarna väljer du **Nästa**.

8. På sidan **Omfång (taggar)** väljer du **Välj omfångstaggar** för att öppna fönstret *Välj taggar* för att tilldela omfångstaggar till profilen.
  
   Fortsätt genom att välja **Nästa**.

9. På sidan **Tilldelningar** väljer du de grupper som profilen ska tillämpas på. Mer information om hur du tilldelar profiler finns i [Tilldela användar- och enhetsprofiler](../configuration/device-profile-assign.md).

   Välj **Nästa**.

10. På sidan **Tillämplighetsregler** använder du alternativen **Regel**, **Egenskap** och **Värde** för att definiera hur profilen ska tillämpas i tilldelade grupper.

11. Välj **Skapa**på sidan **Granska + skapa** när du är klar. Profilen skapas och visas i listan.

Nästa gång varje enhet checkar in tillämpas principen.

## <a name="remove-delivery-optimization-from-windows-10-update-rings"></a>Ta bort leveransoptimering från Windows 10-uppdateringsgrupper

Leveransoptimering konfigurerades tidigare som en del av programuppdateringsgrupperna. Från och med februari 2019 konfigureras inställningarna för leveransoptimering som en del av en enhetskonfigurationsprofil med leveransoptimering, med ytterligare inställningar som påverkar mer än leveransen av programuppdateringar till enheter. Om du inte redan har gjort det tar du bort inställningen för leveransoptimering från dina uppdateringsgrupper genom att ange den som *Inte konfigurerad*. Sedan använder du en leveransoptimeringsprofil till att hantera det större intervallet av tillgängliga alternativ.

1. Skapa en enhetskonfigurationsprofil för leveransoptimering:

    1. I administrationscentret för Microsoft Endpoint Manager väljer du **Enheter** > **Konfigurationsprofiler** > **Skapa profil**.
    2. Ange följande egenskaper:

        - **Plattform**: Välj **Windows 10 och senare**.
        - **Profil**: Välj **Leveransoptimering**.

    3. Välj **Skapa**.
    4. Ange följande egenskaper i **Grundinställningar**:

        - **Namn**: Ange ett beskrivande namn på den nya profilen.
        - **Beskrivning**: Ange en beskrivning av profilen. Denna inställning är valfri, men rekommenderas.

    5. Välj **Nästa**.
    6. För **Konfigurationsinställningar** > **Nedladdningsläge** väljer du samma läge som används av den befintliga programuppdateringsringen såvida du *inte* vill ändra de inställningar du tillämpar för dina enheter. Alternativen är:

        - **Inte konfigurerat**
        - **Endast HTTP, ingen peering**
        - **HTTP blandat med peering bakom samma NAT**
        - **HTTP blandat med peering i en privat grupp**
        - **HTTP blandat med Internet-peering**
        - **Läge för enkel nedladdning utan peering**
        - **Förbigångsläge**

    7. Konfigurera [eventuella ytterligare inställningar](delivery-optimization-settings.md) du vill hantera och fortsätt att skapa profilen.

        Under **Tilldelningar** tilldelar du den nya profilen till samma enheter och användare som den befintliga programuppdateringsringen. Mer information finns i [Tilldela profilen](device-profile-assign.md).

2. Ta bort konfiguration för den befintliga programringen:

    1. I administrationscentret för Microsoft Endpoint Manager går du till **Programuppdateringar** > Windows 10-uppdateringsringar.
    2. Välj din uppdateringsring i listan.
    3. Gå till inställningarna och ställ in **Nedladdningsläge för leveransoptimering** på **Inte konfigurerat**.
    4. **OK** > **Spara** ändringarna.

## <a name="next-steps"></a>Nästa steg

När du har [tilldelat profilen](device-profile-assign.md) [övervakar du dess status](device-profile-monitor.md).

Visa [inställningarna för leveransoptimering](delivery-optimization-settings.md) för Intune.