---
title: Tillgångsinformation förutsättningar
titleSuffix: Configuration Manager
description: Hämta kraven för Tillgångsinformation i Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 23ab4f94-7bfe-436e-8a6a-029409a2730c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: dfed0f2c2e8149abb05d4b21047d4d494f034e53
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714131"
---
# <a name="prerequisites-for-asset-intelligence-in-configuration-manager"></a>Krav för Tillgångsinformation i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Tillgångsinformation i Configuration Manager har externa beroenden och beroenden inom produkten.  

## <a name="dependencies-external-to-configuration-manager"></a>Beroenden utanför Configuration Manager  
 Följande tabell innehåller beroenden för Tillgångsinformation som är externa för att Configuration Manager.  

|Beroende|Mer information|  
|----------------|----------------------|  
|Krav för granskningen av lyckade inloggningshändelser|Fyra tillgångsinformationsrapporter visar information som samlats in från händelseloggarna för Windows-säkerhet på klientdatorer. Om logginställningarna för säkerhetshändelser inte har konfigurerats att logga alla lyckade inloggningshändelser innehåller dessa rapporter ingen information även om rätt rapportklass för maskinvaruinventering är aktiverad.<br /><br /> Följande tillgångsinformationsrapporter beror på insamlad information från händelseloggarna för Windows-säkerhet:<br /><br /> – Maskin vara 03A – primära dator användare<br />– Maskin vara 03B – datorer för en speciell primär konsol användare<br />– Maskin vara 04A-delade datorer (flera användare)<br />– Maskin vara 05A – konsol användare på en angiven dator<br /><br /> Om du vill aktivera klientagenten för maskinvaruinventering så att informationen som krävs för dessa rapporter inventeras måste du först ändra logginställningarna för Windows-säkerhet på klienterna så att alla lyckade inloggningshändelser loggas, samt aktivera rapportklassen **SMS_SystemConsoleUser** för maskinvaruinventering. Mer information om hur du ändrar logginställningarna för säkerhetshändelser så att alla lyckade inloggningshändelser loggas finns i [Enable auditing of success logon events](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md#BKMK_EnableSuccessLogonEvents).|  

> [!NOTE]  
>  Rapportklassen **SMS_SystemConsoleUser** för maskinvaruinventering sparar bara data om lyckade inloggningshändelser för de senaste 90 dagarna i säkerhetshändelseloggen oavsett loggens längd. Om säkerhetshändelseloggen innehåller mindre än 90 dagars data kommer hela loggen att läsas.  

## <a name="dependencies-internal-to-configuration-manager"></a>Beroenden inom Configuration Manager  
 Följande tabell innehåller beroenden för Tillgångsinformation som är interna för Configuration Manager.  

|Beroende|Mer information|  
|----------------|----------------------|  
|Krav för klientagenten|Tillgångsinformationsrapporter är beroende av klientinformation som erhålls genom maskin- och programvaruinventeringsrapporter på klienter. Följande klientagenter måste vara aktiverade för att det ska gå att samla in informationen som krävs av tillgångsinformationsrapporterna:<br /><br /> -Klientagent för maskinvaruinventering<br />– Klient agent för avläsning av program vara|  
|Beroenden för klientagent för maskinvaruinventering|För att det ska gå att samla in de inventeringsdata som krävs för vissa tillgångsinformationsrapporter måste klientagenten för maskinvaruinventering vara aktiverad. Dessutom måste vissa rapportklasser för maskinvaruinventering som tillgångsinformationsrapporterna är beroende av vara aktiverade på primära platsservrar.<br /><br /> Information om hur du aktiverar klientagent för maskinvaruinventering finns i [så här utökar du maskin varu inventeringen](../../../../core/clients/manage/inventory/extend-hardware-inventory.md).|  
|Beroenden för klientagenten för programmätare|Ett antal programvarurapporter i Tillgångsinformation är beroende av klientagenten för programmätare för att tillhandahålla data. Information om hur du aktiverar klient agenten för program varu avläsning finns i [övervaka app-användning med avläsning av program vara](../../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).<br /><br /> Följande tillgångsinformationsrapporter är beroende av klientagenten för programmätare för att tillhandahålla data:<br /><br /> – Program vara 07A – nyligen använda körbara filer efter antal datorer<br />– Program vara 07B – datorer som nyligen har använt en angiven körbar fil<br />– Program vara 07C – nyligen använda körbara filer på en speciell dator<br />– Program vara 08A – nyligen använda körbara filer per antal användare<br />– Program vara 08B – användare som nyligen har använt en angiven körbar fil<br />– Program vara 08C – nyligen använda körbara filer av en angiven användare|  
|Krav för rapportklasser för maskinvaruinventering i Tillgångsinformation|Tillgångsinformation rapporter i Configuration Manager är beroende av vissa rapporterings klasser för maskin varu inventering. Rapportklasserna för maskinvaruinventering måste aktiveras och klienterna måste rapportera maskinvaruinventering baserat på dessa klasser för att de associerade tillgångsinformationsrapporterna ska innehåller data. Du kan aktivera följande rapportklasser för maskinvaruinventering för att uppfylla kraven för tillgångsinformationsrapporterna:<br /><br /> – SMS_SystemConsoleUsage<sup>1</sup><br />– SMS_SystemConsoleUser<sup>1</sup><br />-SMS_InstalledSoftware<br />-SMS_AutoStartSoftware<br />-SMS_BrowserHelperObject<br />-Win32_USBDevice<br />-SMS_InstalledExecutable<br />-SMS_SoftwareShortcut<br />– Program<br />– Produkt<br />-SMS_SoftwareTag<br /><br /> <sup>1</sup> Rapportklasserna **SMS_SystemConsoleUsage** och **SMS_SystemConsoleUser** för maskinvarurapportering i Tillgångsinformation är aktiverade som standard.<br /><br /> Du kan redigera rapport klasserna Tillgångsinformation maskin varu inventering i Configuration Manager-konsolen, på arbets ytan **till gångar och efterlevnad** , när du klickar på noden **tillgångsinformation** . Mer information finns i avsnittet [aktivera tillgångsinformation maskin varu inventerings rapporterings klasser](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md#BKMK_EnableAssetIntelligence) i avsnittet [Konfigurera tillgångsinformation](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md) .|  
|Rapporteringstjänstpunkt|Platssystemrollen för Reporting Services-platsen måste installeras innan rapporter för programvaruuppdateringar kan visas. Mer information om hur du skapar en Reporting Services-plats finns i [Konfigurera rapportering i Configuration Manager](https://go.microsoft.com/fwlink/p/?LinkId=232661).|  
