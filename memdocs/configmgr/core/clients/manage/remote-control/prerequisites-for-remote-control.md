---
title: Krav för fjärr styrning
titleSuffix: Configuration Manager
description: Hämta kraven för fjärr styrning i Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: c1b2057e-b74f-43fa-a293-763a8f866d3d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f19f8799dd90fc61c0bfeeee1dc60125ba491fef
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715118"
---
# <a name="prerequisites-for-remote-control-in-configuration-manager"></a>Krav för fjärr styrning i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Fjärr styrning i Configuration Manager har externa beroenden och beroenden i produkten.  

## <a name="dependencies-external-to-configuration-manager"></a>Beroenden utanför Configuration Manager  

|Beroende|Mer information|  
|----------------|----------------------|  
|Datorns grafikkortsdrivrutin|Se till att den senaste grafikkortsdrivrutinen är installerad på klientdatorerna för att få bästa möjliga fjärrstyrning.|  

 Enheter med Windows Embedded, Windows Embedded for Point of Service (POS) och Windows Fundamentals för äldre datorer har inte stöd för fjärrstyrningsvisaren, men de har stöd för fjärrstyrningsklienten.  

 Configuration Manager fjärr styrning kan inte användas för att fjärradministrera klient datorer som kör Systems Management Server 2003 eller Configuration Manager 2007.  

> [!NOTE]  
>  Det krävs inga Windows-tjänster som externt beroende för fjärrstyrning.  

### <a name="supported-operating-systems-for-the-remote-control-viewer"></a>Operativsystem som stöds för fjärrstyrningsvisaren  
Visnings programmet för fjärr styrning stöds på alla operativ system som stöds för Configuration Manager-konsolen. Mer information finns i [konfigurationer som stöds för Configuration Manager-konsoler](../../../../core/plan-design/configs/supported-operating-systems-consoles.md).   

## <a name="configuration-manager-dependencies"></a>Beroenden i Configuration Manager  

|Beroende|Mer information|  
|----------------|----------------------|  
|Fjärrstyrning måste vara aktiverat för klienter|Fjärr styrning är som standard inte aktive rad när du installerar Configuration Manager. Information om hur du aktiverar och konfigurerar fjärr styrning finns i [Konfigurera fjärr styrning](../../../../core/clients/manage/remote-control/configuring-remote-control.md).|  
|Rapporteringstjänstpunkt|Platssystemrollen Reporting Services-plats måste installeras innan du kan köra rapporter för fjärrstyrning. Mer information finns i [Introduktion till rapportering](../../../servers/manage/introduction-to-reporting.md).|  
|Säkerhetsbehörigheter för att använda fjärrstyrning|För att få åtkomst till samlings resurser och starta en fjärrstyrningssession från Configuration Manager-konsolen: **läsa**, **läsa resurs**och **fjärr styrnings** behörighet för objektet **samling** .<br /><br /> Säkerhets rollen **ansvarig för fjärrverktyg** omfattar de behörigheter som krävs för att hantera fjärr styrning i Configuration Manager.<br /><br /> Mer information finns i [Konfigurera rollbaserad administration för Configuration Manager](../../../../core/servers/deploy/configure/configure-role-based-administration.md).<br /><br /> Dessutom måste behöriga användare ha behörighet att använda fjärr styrning genom att lägga till dessa användare i listan **med tillåtna visnings program för fjärr styrning och Fjärrhjälp** i klient inställningarna för **fjärrverktyg** .
