---
title: Visa maskin- och programvaruinventering för Windows-datorer
titleSuffix: Microsoft Intune
description: Så här visar du maskin- och programvaruinformation om stationära Windows-datorer som du hanterar som datorer med Intune-programvaruklienten.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 06/26/2019
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 3c10f4c9-520b-4864-92fc-a45a9f640ad4
ms.reviewer: owenyen
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic-keep
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9e2d5e3f1e5839040c3ffd2229c34f3063a3ce87
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "79354704"
---
# <a name="view-hardware-and-software-inventory-for-windows-pcs"></a>Visa maskin- och programvaruinventering för Windows-datorer

[!INCLUDE [classic-portal](../includes/classic-portal.md)]

> [!NOTE]
> Informationen i det här avsnittet gäller endast för stationära Windows-datorer som du hanterar som datorer med Intune-klientprogramvaran. Om du vill visa inventering för Windows-datorer som registrerats som mobila enheter kan du läsa [Visa enhetsinformation i Intune](../remote-actions/device-inventory.md).

Intune samlar in detaljerad information om maskinvara och programvara för stationära datorer som hanteras som datorer med hjälp av Intune programvaruklienten. Använd informationen i följande procedurer för att lära dig skapa:

- En rapport som visar information om maskinvarukapaciteten hos de datorer som du hanterar.

- En rapport som visar en lista över vilka program som finns installerade på varje dator.

- Så här uppdaterar du en datorinventering för att säkerställa att data i rapporten är aktuella.

## <a name="to-display-information-about-pcs-you-manage"></a>Så här visar du information om de datorer du hanterar

1. I [Microsoft Intune-administrationskonsolen](https://manage.microsoft.com/) väljer du **Rapporter** &gt; **Datorinventeringsrapporter**.

2. På sidan **Skapa ny rapport** accepterar du standardvärdena eller anpassar dem om du vill filtrera resultatet som rapporten skickar tillbaka. Du kan till exempel välja att endast de datorer som kör Windows 8.1 ska visas i rapporten.

3. Välj **Visa rapport** för att öppna **Datorinventeringsrapporter** i ett nytt fönster.

    Du kan sortera rapporten på valfri kolumn, t.ex. **Namn**, **Chassityp** eller **Tillverkare** genom att välja kolumnens rubrik.

## <a name="to-display-software-installed-on-pcs-you-manage"></a>Så här visar du vilka program som har installerats på de datorer du hanterar

1. I [Microsoft Intune-administrationskonsolen](https://manage.microsoft.com/) väljer du **Rapporter** &gt; **Rapporter med identifierad programvara**.

2. På sidan **Skapa ny rapport** accepterar du standardvärdena eller anpassar dem om du vill filtrera resultatet som rapporten skickar tillbaka. Du kan till exempel välja att endast program som är utgivna av Microsoft ska visas i rapporten.

3. Välj **Visa rapport** för att öppna **Upptäckta programvarurapporter** i ett nytt fönster.

    Du kan sortera rapporten på valfri kolumn, t.ex. **Namn**, **Utgivare** eller **Kategori** genom att välja kolumnens rubrik. Du kan expandera uppdateringarna i listan om du vill visa mer information (t.ex. vilka datorer som programmet har installerats på) genom att klicka på riktningspilen bredvid listposten.

## <a name="to-refresh-computer-inventory-to-ensure-it-is-current"></a>Så här uppdaterar du datorinventeringen för att säkerställa att den är aktuell

1. I [Microsoft Intune-administrationskonsolen](https://manage.microsoft.com/) väljer du **Grupper** &gt; **Alla enheter** (eller en annan grupp som innehåller den dator du vill uppdatera inventeringen för).

2. Välj en dator eller tryck och håll ned **Ctrl** för att välja flera datorer.

3. I aktivitetsfältet klickar du på **Fjärruppgifter** &gt; **Uppdatera inventering**.

4. Om du vill visa aktivitetens status väljer du **Fjärruppgifter** längst ner till höger på sidan.

    Dialogrutan **Aktivitetsstatus** visar aktuella fjärrhanteringsaktiviteter, aktivitetsstatus, enhetsnamn och eventuella rapporterade fel och innehåller en länk till felsökningsinformation.

## <a name="see-also"></a>Se även

[Vanliga hanteringsuppgifter för Windows-datorer med Intune-klientprogrammet](common-windows-pc-management-tasks-with-the-microsoft-intune-computer-client.md)
