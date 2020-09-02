---
title: Lägga till anpassade inställningar för Windows 10-enheter i Microsoft Intune – Azure | Microsoft Docs
description: Lägg till eller skapa en anpassad profil för att använda OMA-URI-inställningarna för enheter som kör Windows 10 i Microsoft Intune. Använd en anpassad profil för att lägga till anpassade inställningar.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 28a867c735a05cfa4a4765534d200b806711f9b5
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88913026"
---
# <a name="use-custom-settings-for-windows-10-devices-in-intune"></a>Använda anpassade inställningar för Windows 10-enheter i Intune

Den här artikeln beskriver de olika anpassade inställningar du kan styra på enheter med Windows 10 och senare. Inom ramen för din MDM-lösning (hantering av mobilenheter) kan du använda de här inställningarna till att konfigurera inställningar som inte är inbyggda i Intune.

Mer information om anpassade profiler finns i [Skapa en profil med anpassade inställningar](custom-settings-configure.md).

Dessa inställningar läggs till en profil för enhetskonfiguration i Intune som sedan tilldelas eller distribueras till dina Windows 10-enheter.

Den här funktionen gäller för:

- Windows 10 och senare

Anpassade profiler i Windows 10 använder OMA-URI-inställningar (Open Mobile Alliance Uniform Resource Identifier) för att konfigurera olika funktioner. De här inställningarna används vanligtvis av tillverkare av mobila enheter till att styra funktioner på enheten.

I Windows 10 finns flera CSP-inställningar (Configuration Service Provider), t.ex. [Princip-CSP (Policy Configuration Service Provider)](/windows/configuration/provisioning-packages/how-it-pros-can-use-configuration-service-providers).

Glöm inte att [enhetsbegränsningsprofilen i Windows 10](device-restrictions-windows-10.md) innehåller många inbyggda inställningar som du kan använda. Det betyder att du kanske inte behöver ange anpassade värden.

## <a name="before-you-begin"></a>Innan du börjar

[Skapa en anpassad Windows 10-profil](custom-settings-configure.md#create-the-profile).

## <a name="oma-uri-settings"></a>OMA-URI-inställningar

**Lägg till**: Ange följande inställningar:

- **Namn**: Ange ett unikt namn för OMA-URI-inställningen som hjälper dig att identifiera den i listan över inställningar.
- **Beskrivning**: Ange en beskrivning som ger en översikt över inställningen, samt annan viktig information.
- **OMA-URI** (skiftlägeskänslig): Ange den OMA-URI som du vill använda som inställning.
- **Datatyp**: Välj den datatyp som du vill använda för den här OMA-URI-inställningen. Alternativen är:

  - Base64 (fil)
  - Boolesk
  - Sträng (XML-fil)
  - Datum och tid
  - Sträng
  - Flyttal
  - Heltal

- **Värde**: Ange det datavärde som du vill associera med den OMA-URI som du har angett. Värdet beror på vilken datatyp du valt. Om du till exempel valde **Datum och tid**, väljer du värdet från en datumväljare.

När du har lagt till några inställningar kan du välja **Exportera**. **Exportera** skapar en lista över alla värden som du har lagt till i en fil med kommaavgränsade värden (.csv).

## <a name="find-the-policies-you-can-configure"></a>Hitta principer som du kan konfigurera

Du hittar en lista med alla konfigurationstjänstleverantörer (CSP) som Windows 10 har stöd för i [referensen till konfigurationstjänstleverantörer](/windows/client-management/mdm/configuration-service-provider-reference).

Alla inställningar är inte kompatibla med alla versioner av Windows 10. I [referensen till konfigurationstjänstleverantörer](/windows/client-management/mdm/configuration-service-provider-reference) står det vilka versioner som stöds för varje CSP.

Observera att Intune inte stöder alla inställningar i [referensen för konfigurationstjänstleverantörer](/windows/client-management/mdm/configuration-service-provider-reference). Om du vill veta om Intune har stöd för den inställning som du vill använda, kan du öppna artikeln för den inställningen. Varje inställningssida visar den åtgärd som stöds. Om du vill arbeta med Intune måste inställningen ha stöd för åtgärderna **Add** (Lägg till), **Replace** (Ersätt) och **Get** (Hämta). Om det värde som returneras av åtgärden **Get** (Hämta) inte matchar det värde som anges av åtgärderna **Add** (Lägg till) eller **Replace** (Ersätt) rapporterar Intune ett efterlevnadsfel.

## <a name="next-steps"></a>Nästa steg

[Tilldela profilen](device-profile-assign.md) och [övervaka dess status](device-profile-monitor.md).

[Läs mer om anpassade profiler i Intune](custom-settings-configure.md).