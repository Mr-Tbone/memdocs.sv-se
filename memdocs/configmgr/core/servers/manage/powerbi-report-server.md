---
title: Integrera med Power BI-rapportserver
titleSuffix: Configuration Manager
description: Integrera Power BI-rapportserver med Configuration Manager rapportering för modern visualisering och bättre prestanda.
ms.date: 04/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 315e2613-dc71-46b1-80cb-26161d08103a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: dc8aa57bda5f5a29d72af854be9a18e4f32760f8
ms.sourcegitcommit: 7b656712cc9340d18211c7754cb99bcaae91b0ca
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/03/2020
ms.locfileid: "89432548"
---
# <a name="integrate-with-power-bi-report-server"></a>Integrera med Power BI-rapportserver

*Gäller för: Configuration Manager (aktuell gren)*

<!--3721603-->

Från och med version 2002 kan du integrera [Power BI-rapportserver](/power-bi/report-server/get-started) med Configuration Manager repor ting. Den här integrationen ger modern visualisering och bättre prestanda. Det lägger till konsol stöd för Power BI rapporter på liknande sätt som redan finns med SQL Server Reporting Services.

Spara Power BI Desktop rapportmallar (. PBIX) och distribuera dem till Power BI-rapportserver. Den här processen liknar SQL Server Reporting Services rapport-filer (. RDL). Du kan också starta rapporterna i webbläsaren direkt från Configuration Manager-konsolen.

## <a name="prerequisites"></a>Krav

- Power BI-rapportserver licens. Mer information finns i [licens Power BI-rapportserver](/power-bi/report-server/get-started#licensing-power-bi-report-server).

- Ladda ned [Microsoft Power BI-rapportserver – September 2019](https://www.microsoft.com/download/details.aspx?id=57270)eller senare.

    > [!NOTE]
    > Installera inte Power BI-rapportserver direkt. En lämplig process baserad på din miljö finns i [Konfigurera repor ting Services-platsen](#configure-the-reporting-services-point).

- Hämta [Microsoft Power BI Desktop (optimerad för Power BI-rapportserver – September 2019)](https://www.microsoft.com/download/details.aspx?id=57271)eller senare.

    > [!IMPORTANT]
    > - Använd inte en version från Microsoft Store för att endast använda versioner av Power BI Desktop från [Microsoft Download Center](https://www.microsoft.com/download/).
    > - Använd bara en version av [Power BI Desktop som anger att den är **optimerad för Power BI-rapportserver**](/power-bi/report-server/install-powerbi-desktop).

- Power BI integration använder samma rollbaserad administration för rapportering.
    > [!NOTE]
    > Power BI-rapportserver stöder inte RBAC-aktiverade rapporter, men alla visnings program för rapporterna kommer att se samma resultat oavsett tilldelad omfattning.

## <a name="configure-the-reporting-services-point"></a>Konfigurera repor ting Services-platsen

Den här processen varierar beroende på om du redan har den här rollen på-platsen.

### <a name="you-have-a-reporting-services-point"></a>Du har en repor ting Services-plats

Använd bara den här processen om du redan har en repor ting Services-plats på platsen. Gör alla steg i den här processen på samma server:

1. Säkerhetskopiera **krypterings nycklarna**i **Configuration Manager rapport Server**. Mer information finns i [SSRS-krypterings nycklar – säkerhetskopiera och återställa krypterings nycklar](/sql/reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys).

    > [!WARNING]
    > Om du hoppar över det här steget förlorar du åtkomsten till anpassade rapporter i SQL Server Reporting Services.

1. Ta bort repor ting Services-plats rollen från-platsen.

1. Avinstallera SQL Server Reporting Services, men behåll databasen.

1. Installera Power BI-rapportserver.

1. Konfigurera Power BI-rapportserver

    1. Använd den föregående rapport Server databasen.

    1. Använd **repor ting Server-Configuration Manager** för att återställa **krypterings nycklarna**.

1. Lägg till rollen repor ting Services-plats i Configuration Manager.

### <a name="you-dont-have-a-reporting-services-point"></a>Du har ingen repor ting Services-plats

Använd bara den här processen om du inte redan har en repor ting Services-plats på platsen. Gör alla steg i den här processen på samma server:

1. Installera Power BI-rapportserver.

2. Lägg till rollen repor ting Services-plats i Configuration Manager. Mer information finns i [Konfigurera rapportering](configuring-reporting.md).

## <a name="configure-the-configuration-manager-console"></a>Konfigurera Configuration Manager-konsolen

1. Uppdatera Configuration Manager-konsolen till den senaste versionen på en dator som har Configuration Manager-konsolen.

1. Installera Power BI Desktop. Se till att språket är detsamma.

1. När den har installerats startar du Power BI Desktop minst en gång innan du öppnar Configuration Manager-konsolen.

## <a name="create-power-bi-reports"></a>Skapa Power BI rapporter

1. I Configuration Manager-konsolen går du till arbets ytan **övervakning** , expanderar **rapportering**och väljer noden ny **Power BI rapporter** .

1. I menyfliksområdet väljer du **Skapa rapport**. Den här åtgärden öppnar Power BI Desktop.

1. Skapa en rapport i Power BI Desktop.

    - När du i Power BI Desktop ansluter till en data källa väljer du **DirectQuery** för anslutnings inställningarna.

    - Använd endast SQL-vyer som stöds i dessa rapporter. Mer information finns i [skapa anpassade rapporter med hjälp av SQL Server vyer i Configuration Manager](../../../develop/core/understand/sqlviews/create-custom-reports-using-sql-server-views.md).

1. När rapporten är klar att spara går du till **Arkiv** -menyn, väljer **Spara som**och väljer **Power BI-rapportserver**.

1. I fönstret **Power BI-rapportserver val** anger du URL: en för repor ting Services-platsen som den **nya rapport Server adressen**. Till exempel `https://rsp.contoso.com/Reports`. Välj **OK**.

1. I fönstret **Spara rapport** dubbelklickar du på `ConfigMgr_<SiteCode>` mappen. Till exempel `ConfigMgr_PS1` , där `PS1` är plats koden för ConfigMgr. Alternativt kan du välja eller skapa (från rapport servern) en undermapp för att lagra den i.
    > [!TIP]
    > Rapporter och rapport-mappar med Power BI rapporter måste finnas i `ConfigMgr_<SiteCode>` mappen på rapport servern eller visas inte i Configuration Manager-konsolen.

1. I **fil namn**anger du ett namn för rapporten.

I Configuration Manager-konsolen visas den nya rapporten i listan över Power BI rapporter. Om du inte ser dina rapporter kontrollerar du att du har sparat rapporterna i `ConfigMgr_<SiteCode>` mappen.

## <a name="next-steps"></a>Nästa steg

När du har skapat en rapport använder du följande åtgärder i Configuration Manager-konsolen:

- **Kör i webbläsare**: öppnar Power BI rapporten i webbläsaren. Dela denna URL med andra, till exempel: `https://rsp.contoso.com/Reports/POWERBI/ConfigMgr_ABC/Windows%2010/Windows10%20Dashboard?rs:embed=true`

    > [!TIP]
    > Du kan bara visa rapporterna i webbläsaren.

- **Redigera**: gör ändringar i rapporten i Power BI Desktop. För en befintlig rapport använder du alternativet **Spara** för att spara ändringarna på rapport servern.

Mer information om loggfiler som ska användas för rapportering finns i [logg filen referens-rapportering](../../plan-design/hierarchy/log-files.md#BKMK_ReportLog).
