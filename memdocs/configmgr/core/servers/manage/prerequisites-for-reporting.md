---
title: Krav för rapportering
titleSuffix: Configuration Manager
description: Förstå olika beroenden som påverkar din användning av rapportering i Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9cc508a5-5023-4833-b776-ae9a6971138f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e08833a5ef560a0f958fe68b4ade0d4717dffc73
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720144"
---
# <a name="prerequisites-for-reporting-in-configuration-manager"></a>Krav för rapportering i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Rapportering i Configuration Manager har följande beroenden:

- SQL Server Reporting Services
- Rapporteringstjänstpunkt
- Power BI-rapportserver (valfritt, från och med version 2002)

## <a name="sql-server-reporting-services"></a>SQL Server Reporting Services

Innan du kan använda repor ting i Configuration Manager installerar och konfigurerar du SQL Server Reporting Services.

Mer information om hur du planerar och distribuerar repor ting Services finns i [installations SQL Server Reporting Services](https://docs.microsoft.com/sql/reporting-services/install-windows/install-reporting-services).

Installera repor ting Services-databasen antingen på standard instansen eller en namngiven instans av en 64-bitars SQL Server-installation. Samplacera SQL Server-instansen med plats system servern eller konfigurera den på en fjärrdator.

Configuration Manager stöder samma versioner av SQL Server för rapportering som för plats databasen. Mer information finns i [SQL Server-versioner som stöds](../../plan-design/configs/support-for-sql-server-versions.md#bkmk_SQLVersions).

## <a name="reporting-services-point"></a>Rapporteringstjänstpunkt

Innan du kan använda rapportering i Configuration Manager konfigurerar du plats system rollen för repor ting Services-platsen.

Mer information finns i [krav för plats och plats system](../../plan-design/configs/site-and-site-system-prerequisites.md#bkmk_2012RSpoint).

## <a name="power-bi-report-server"></a>Power BI-rapportserver

Från och med version 2002 kan du integrera rapporter med Power BI-rapportserver. Mer information, inklusive krav, finns i [integrera med Power BI-rapportserver](powerbi-report-server.md).

## <a name="next-steps"></a>Nästa steg

[Konfigurera rapporter](configuring-reporting.md)
