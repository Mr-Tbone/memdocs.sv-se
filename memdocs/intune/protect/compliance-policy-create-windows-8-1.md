---
title: Kompatibilitetsinställningar för Windows 8.1 i Microsoft Intune – Azure | Microsoft Docs
description: Visa en lista över alla inställningar som du kan använda när du ställer in kompatibilitet för Windows 8.1 i Microsoft Intune. Kontrollera kompatibiliteten med den lägsta och högsta operativsystemversionen, ange begränsningar och längd för lösenord, aktivera kryptering för datalagring och mycket mer.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/14/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9b423d289e81c48479adcaa7a594974b23a9476c
ms.sourcegitcommit: cb12dd341792c0379bebe9fd5f844600638c668a
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252715"
---
# <a name="windows-81-settings-to-mark-devices-as-compliant-or-not-compliant-using-intune"></a>Windows 8.1-inställningar för att markera enheter som kompatibla eller inkompatibla med hjälp av Intune

[!INCLUDE [windows-phone-81-windows-10-mobile-support](../includes/windows-phone-81-windows-10-mobile-support.md)]
Den här artikeln innehåller en lista över och beskriver de olika kompatibilitetsinställningar som du kan konfigurera på Windows 8.1-enheter i Intune. Använd dessa inställningar som en del av din MDM-lösning för hantering av mobilenheter för att blockera enkla lösenord, ange en lägsta och högsta tillåten operativsystemversion och mycket mer.

Den här funktionen gäller för:

- Windows 8.1 och senare

Som Intune-administratör kan du använda dessa kompatibilitetsinställningar för att skydda din organisations resurser. Mer om kompatibilitetsprinciper och vad de gör finns i [Komma igång med kompatibilitet](device-compliance-get-started.md).

## <a name="before-you-begin"></a>Innan du börjar

[Skapa en efterlevnadsprincip](create-compliance-policy.md#create-the-policy). För **Plattform** väljer du **Windows 8.1 och senare**.

## <a name="device-properties"></a>Egenskaper för enhet

### <a name="operating-system-version"></a>Operativsystemversion

**Windows 8.1 och senare**
- **Lägsta version av operativsystemet**:  
  Ange den lägsta tillåtna versionen. När en enhet inte uppfyller minimikravet på operativsystemversion, rapporteras den som inkompatibel. En länk med information om hur du uppgraderar visas. Användaren av enheten kan välja att uppgradera enheten för att sedan få åtkomst till företagets resurser.

- **Högsta version av operativsystemet**:  
  Ange den högsta tillåtna versionen. När en enhet använder en senare version av operativsystemet än den version som har angetts i regeln, så blockeras åtkomsten till organisationens resurser. Användaren av enheten ombeds att kontakta IT-administratören. Enheten får inte åtkomst till organisationens resurser förrän en regel ändras så att operativsystemversionen stöds.

Datorer med Windows 8.1 returnerar en **3**-version. Om regeln för operativsystemsversion är inställd på Windows 8.1 för Windows rapporteras enheten som inkompatibel även om den har Windows 8.1.

## <a name="system-security"></a>Systemsäkerhet

### <a name="password"></a>lösenordsinställning

- **Kräv ett lösenord för att låsa upp mobila enheter**:  
  - **Ej konfigurerad** (*standard*) – Ingen kompatibilitetskontroll görs för den här inställningen.
  - **Kräv** – Användarna måste ange ett lösenord innan de får åtkomst till sina enheter.

- **Enkla lösenord**:  
  - **Inte konfigurerad** (*standard*) – Användare kan skapa enkla lösenord som **1234** eller **1111**.
  - **Blockera** – Användarna kan inte skapa enkla lösenord, som exempelvis **1234** eller **1111**.  

- **Minsta lösenordslängd**:  
  Ange det minsta antal siffror eller tecken som lösenordet måste innehålla.

  För enheter som kör Windows och som öppnas med ett Microsoft-konto, kan inte efterlevnadsprincipen göra någon korrekt utvärdering ifall något av följande villkor uppfylls:  
  - Minimilängden för lösenord är mer än åtta tecken
  - Det minsta antalet teckenuppsättningar är mer än två

- **Lösenordstyp**:  
  Ange om ett lösenord endast ska ha **numeriska** tecken, eller om det ska vara en blandning av siffror och andra tecken (**alfanumeriska**).

  Om värdet är *Alfanumeriskt* är nedanstående inställning tillgänglig.  

  - **Antal icke-alfanumeriska tecken i lösenord**:  
    Om alternativet för *lösenordstyp* är **Alfanumeriskt** anger du det minsta antal teckenuppsättningar som lösenordet måste innehålla. Alternativen är **0** till **4** uppsättningar, med standardvärdet **1**.
    
    De fyra teckenuppsättningarna är:
    - Gemener
    - Versaler
    - Symboler
    - Tal

    Om du anger en högre siffra måste användaren skapa ett lösenord som är mer komplext. För enheter som öppnas med ett Microsoft-konto, kan inte efterlevnadsprincipen göra någon korrekt utvärdering ifall något av följande villkor uppfylls:

    - Minimilängden för lösenord är mer än åtta tecken
    - Det minsta antalet teckenuppsättningar är mer än två

- **Maximalt antal minuters inaktivitet innan lösenord krävs**:  
  Ange efter hur lång tids inaktivitet som användaren måste ange sitt lösenord igen.

- **Lösenordets giltighetstid (dagar)** :  
  Ange antalet dagar tills lösenordet upphör att gälla och användarna måste skapa ett nytt.

- **Antal tidigare lösenord för att förhindra återanvändning**:  
  Ange antal tidigare använda lösenord som inte får återanvändas.

### <a name="encryption"></a>Kryptering

- **Kryptering av datalagring på enheten**:  
  - **Ej konfigurerat** (*standard*)
  - **Kräv** – Använd *Kräv* när du ska kryptera datalagring på dina enheter.


<!-- not on phone   
- **Require encryption on mobile device**: **Require** the device to be encrypted to connect to data storage resources.
--> 

## <a name="next-steps"></a>Nästa steg

- [Lägga till åtgärder för inkompatibla enheter](actions-for-noncompliance.md) och [Filtrera principer med hjälp av omfångstaggar](../fundamentals/scope-tags.md).
- [Övervaka dina kompatibilitetsprinciper](compliance-policy-monitor.md).
- Mer information finns i [Inställningar för kompatibilitetsprinciper för enheter med Windows 10 och senare](compliance-policy-create-windows.md).