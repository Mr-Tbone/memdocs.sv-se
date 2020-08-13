---
title: Installera Power BI-exempelrapporter
titleSuffix: Configuration Manager
description: Lär dig hur du installerar Power BI exempel rapporter i Configuration Manager
ms.date: 08/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7e9bc22c-67ac-4a86-b613-944a4928e583
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 450c76617cf12a3201aa990c90843cb2e0f0edee
ms.sourcegitcommit: d1bfd5b8481439babc7eae43493f28edaebe647a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/13/2020
ms.locfileid: "88179442"
---
# <a name="install-power-bi-sample-reports"></a>Installera Power BI-exempelrapporter
<!--5679791-->
*Gäller för: Configuration Manager (aktuell gren)*

Från och med version 2002 kan du integrera [Power BI-rapportserver](https://docs.microsoft.com/power-bi/report-server/get-started) med Configuration Manager repor ting. Det finns exempel rapporter som kan laddas ned som du kan installera i Configuration Manager. I den här artikeln beskrivs hur du installerar Power BI exempel rapporter i Configuration Manager.

## <a name="prerequisites"></a>Förutsättningar

- Configuration Manager repor ting Services-platsen med [Power BI-rapportserver integrerad](powerbi-report-server.md)

- [Microsoft Power BI Desktop (optimerad för Power BI-rapportserver – September 2019)](https://www.microsoft.com/download/details.aspx?id=57271)eller senare

- Den [samlade uppdateringen (4560496) för version 2002](https://support.microsoft.com/help/4560496) rekommenderas, men krävs inte.

    > [!IMPORTANT]
    > Använd endast versioner av Power BI Desktop från [Microsoft Download Center](https://www.microsoft.com/download/). Använd inte en version från Microsoft Store.
    >
    > Använd bara en version av Power BI Desktop som är [optimerad för Power BI-rapportserver](https://docs.microsoft.com/power-bi/report-server/install-powerbi-desktop).

## <a name="download-the-sample-reports"></a>Hämta exempel rapporterna

Så här hämtar du exempel rapporterna:

1. Hämta Power BI exempel rapporter från [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=101452).

1. Spara filen `ConfigMgrSamplePowerBIReports.exe`.

1. Flytta filen till en dator med Microsoft Power BI Desktop (optimerad för Power BI-rapportserver) installerad om du har hämtat den från en annan enhet.

1. Kör `ConfigMgrSamplePowerBIReports.exe` filen för att extrahera. pbit-filerna.

## <a name="install-the-sample-reports"></a>Installera exempel rapporterna

Så här installerar du exempel rapporterna:

1. Skapa en ny mapp `Sample Reports` som heter i mappen rotmapp Configuration Manager rapportering på rapport servern för Power BI.

    :::image type="content" source="media/create-sample-reports-folder.png" alt-text="Skapa exempel rapporten i mappen rot Configuration Manager rapportering från" lightbox="media/create-sample-reports-folder.png":::

1. Starta Microsoft Power BI Desktop (optimerad för Power BI-rapportserver).

1. Välj **Arkiv** och sedan **Öppna** och navigera till den plats där du sparade de extraherade. pbit-filerna.

1. Välj en av de. pbit-filer som du extraherade från `ConfigMgrSamplePowerBIReports.exe` filen.

1. Ange Configuration Manager databas namn och databas server namn när du uppmanas till det och välj sedan **Läs in**.

    När du läser in eller använder data modellen, ignorera eventuella fel om du kommer över en.

    :::image type="content" source="media/sample-report-database.png" alt-text="Ange databas-och databas Server namnet" lightbox="media/sample-report-database.png":::

1. När rapport data har lästs in väljer du **Arkiv**  >  **Spara som**och väljer sedan **Power BI-rapportserver**.

    :::image type="content" source="media/save-powerbi-report-server.png" alt-text="Spara som Power BI-rapportserver" lightbox="media/save-powerbi-report-server.png":::

1. Spara rapporten till `Sample Reports` mappen som du skapade på rapporterings platsen.

    :::image type="content" source="media/save-sample-report.png" alt-text="Spara i mappen exempel rapporter" lightbox="media/save-sample-report.png":::

1. Upprepa stegen för alla andra exempel rapporter. När du är klar stänger du Microsoft Power BI Desktop (optimerad för Power BI-rapportserver).

1. I Configuration Manager-konsolen går du till **övervakning**  >  **Power BI rapporter**  >  **exempel rapporter**.

1. Högerklicka på en av rapporterna och välj **Kör i webbläsare** för att starta rapporten.

    :::image type="content" source="media/view-powerbi-report.png" alt-text="Kör exempel rapporten från Configuration Manager-konsolen" lightbox="media/view-powerbi-report.png":::
