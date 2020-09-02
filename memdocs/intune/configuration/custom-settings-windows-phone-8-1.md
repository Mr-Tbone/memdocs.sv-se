---
title: Lägga till anpassade inställningar för Windows Phone 8.1-enheter i Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Lägg till eller skapa en anpassad profil för att använda OMA-URI-inställningarna för enheter som kör Windows Phone 8.1 i Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/11/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ROBOTS: NOINDEX
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c0adb573dbb40f00a1b43b9fb356cdc20b97b669
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88910085"
---
# <a name="use-custom-settings-for-windows-phone-81-devices-in-intune"></a>Använda anpassade inställningar för Windows Phone 8.1-enheter i Intune

[!INCLUDE [windows-phone-81-windows-10-mobile-support](../includes/windows-phone-81-windows-10-mobile-support.md)]

Med Microsoft Intune kan du lägga till eller skapa anpassade inställningar för dina Windows Phone 8.1-enheter med hjälp av ”anpassade profiler”. Anpassade profiler är en funktion i Intune. De gör att du kan lägga till enhetsinställningar och funktioner som inte är inbyggda i Intune.

Anpassade profiler i Windows Phone 8.1 använder OMA-URI-inställningar (Open Mobile Alliance Uniform Resource Identifier) för att konfigurera olika funktioner. De här inställningarna används vanligtvis av tillverkare av mobila enheter till att styra funktioner på enheten. [Windows Phone 8.1 MDM-protokolldokumentationen](/previous-versions/windows/it-pro/windows-phone/dn499787(v=technet.10)) listar inställningarna.

Den här artikeln visar hur du skapar en anpassad profil för Windows Phone 8.1-enheter. 

## <a name="before-you-begin"></a>Innan du börjar

[Skapa en anpassad Windows Phone 8.1-profil](custom-settings-configure.md).

## <a name="custom-oma-uri-settings"></a>Anpassade OMA-URI-inställningar

- **OMA-URI-inställningar**: **Lägg till** följande inställningar:

  - **Namn**: Ange ett unikt namn för OMA-URI-inställningen som hjälper dig att identifiera den i listan över inställningar.
  - **Beskrivning**: Ange en beskrivning som ger en översikt över inställningen och eventuell annan relevant information som gör det enklare att hitta profilen.
  - **OMA-URI** (skiftlägeskänslig): Ange den OMA-URI som du vill använda som inställning.
  - **Datatyp**: Välj den datatyp som du vill använda för den här OMA-URI-inställningen. Alternativen är:

    - Sträng
    - Sträng (XML-fil)
    - Datum och tid
    - Heltal
    - Flyttal
    - Boolesk
    - Base64 (fil)

  - **Värde**: Ange det datavärde som du vill associera med den OMA-URI som du har angett. Värdet beror på vilken datatyp du valt. Om du till exempel valde **Datum och tid**, väljer du värdet från en datumväljare.

  När du har lagt till några inställningar kan du välja **Exportera**. **Exportera** skapar en lista över alla värden som du har lagt till i en fil med kommaavgränsade värden (.csv).

## <a name="example"></a>Exempel

I följande exempel hindras Windows 8.1-telefonenheter från att ändra mobila nätverk när du är utanför operatörens täckningsområde.

- **Namn**: Tillåt mobildata vid roaming
- **Beskrivning**: Tillåt eller neka mobildata vid roaming
- **OMA-URI** (skiftlägeskänsligt): ./Vendor/MSFT/PolicyManager/My/Connectivity/AllowCellularDataRoaming
- **Datatyp**: Heltal
- **Värde**: 0

## <a name="next-steps"></a>Nästa steg

[Tilldela profilen](device-profile-assign.md) och [övervaka dess status](device-profile-monitor.md).

Skapa en anpassad profil på [Windows 10-enheter](custom-settings-windows-10.md).