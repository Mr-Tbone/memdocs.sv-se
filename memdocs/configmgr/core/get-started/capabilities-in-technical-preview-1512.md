---
title: Funktioner i Technical Preview 1512
titleSuffix: Configuration Manager
description: Lär dig mer om funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1512.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e4d9e414-1346-4ed4-85d0-64d602b68731
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: f52d6956cf860de8e45ac4e532500d32bcf077ba
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074511"
---
# <a name="capabilities-in-technical-preview-1512-for-configuration-manager"></a>Funktioner i Technical Preview 1512 för Configuration Manager

*Gäller för: Configuration Manager (Technical Preview Branch)*

Den här artikeln beskriver de funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1512. Du kan installera den här versionen för att uppdatera och lägga till nya funktioner till din Configuration Manager Technical Preview-webbplats. Innan du installerar den här versionen av Technical Preview kan du läsa introduktions avsnittet, [teknisk för hands version för Configuration Manager](technical-preview.md), för att bekanta dig med allmänna krav och begränsningar för att använda en teknisk för hands version, hur du uppdaterar mellan versioner och hur du ger feedback om funktionerna i en teknisk för hands version.  

 Följande är nya funktioner som du kan prova med den här versionen.  

##  <a name="device-health-attestation"></a><a name="bkmk_devicehealth"></a>Hälsoattestering för enhet  
 Från och med Technical Preview 1512 kan administratörer Visa status för Windows 10-Hälsoattestering för enhet i Configuration Manager-konsolen.  Den här funktionen är tillgänglig för Configuration Manager och Configuration Manager med Microsoft Intune. Med attestering av enhetens hälsotillstånd kan administratörer se till att klientdatorer har tillförlitliga konfigurationer av BIOS, TPM och startprogram. För att stödja hälsoattestering för enheter måste klient enheter köra Win10 med TPM 2 aktiverat. Attesteringen av enhetens hälsotillstånd visar antalet enheter som aktiverats för var och en av följande:  

-   Tidig lansering av program mot skadlig kod  

-   BitLocker  

-   Säker start  

-   Kodintegritet  

Konsolen visar också de viktigaste inställningarna för hälsoattestering som saknas med antalet enheter.  

För att förhandsgranska vyn enhetens hälsoattestering går du till arbets ytan **övervakning** i Configuration Manager-konsolen och klickar på noden **säkerhet** och sedan på **hälsoattestering**.  

##  <a name="in-console-monitoring-for-terms-and-conditions"></a><a name="bkmk_viewterms"></a>Övervakning i konsolen för allmänna villkor  
Från och med Technical Preview 1512 kan du använda Configuration Manager-konsolen för att se vilka användare som har accepterat de villkor som kon figurer ATS av IT-avdelningen och vilka användare som inte har gjort det när du integrerar Configuration Manager med Microsoft Intune.  

**Så här visar du sammanfattnings information:**  

-   I Configuration Manager-konsolen går du till **övervakning** > **Översikt** > **distributioner** och väljer den distribution av allmänna villkor som du vill visa.  

**Så här visar du detaljerad information:**  

1.  I Configuration Manager-konsolen går du till **till gångar och efterlevnad** > **Översikt över** > kompatibilitetsinställningar**Inställningar** > och**villkor**och väljer sedan de villkor som du vill visa.  

2.  Längst ned i konsolen, Välj fliken **distributioner** , Välj distributionen och klicka sedan på **Visa status.**  

##  <a name="improvements-to-endpoint-protection-policy-settings"></a><a name="bkmk_EPpolicy"></a>Förbättringar av princip inställningar för Endpoint Protection  
I 1512 Technical Preview har vi lagt till följande nya inställningar i Endpoint Protection princip för skadlig kod:  

-   Real tids skydd: **blockera potentiellt oönskade program vid nedladdning och före installation**  

    -   Eventuellt oönskade program är en hotklassificering baserat på rykte och databaserad identifiering. Oftast ingår dessa oönskade program i paket.  

    -   Inställningen för skydds principen är aktive rad (inställd på Ja) som standard. När den här inställningen är aktiverad blockeras oönskade program vid nedladdningen och installationen. Du kan dock undanta vissa filer eller mappar för att uppfylla de speciella behoven i din miljö.  

-   Genomsöknings inställningar: **Genomsök mappade nätverks enheter när en fullständig genomsökning körs**  

    -   Den här inställningen ger högre granularitet för administratören att tillåta genomsökningar av nätverksfiler på begäran utan risken att alltid genomsöka mappade nätverks enheter under en schemalagd fullständig genomsökning.  

    -   Inställningen **Genomsök nätverksfiler** måste först aktive ras (Ja) för att den här inställningen ska kunna konfigureras.  

    -   Som standard är den här inställningen "nej", vilket innebär att en fullständig genomsökning inte kommer åt mappade nätverks enheter.  

-   Inställningar för automatisk sändning av exempel fil:  

     Motorn för program mot skadlig kod kan begära att fil exempel skickas till Microsoft för ytterligare analys. Som standard får du alltid en fråga innan sådana exempelfiler skickas. Administratörer kan nu hantera följande inställningar för att konfigurera den här funktionen:  

    -   Avancerat: **Aktivera automatisk sändning av exempel fil för att hjälpa Microsoft att fastställa om vissa hittade objekt är skadliga**: ändra inställningen till "Ja" om du vill aktivera automatisk sändning av exempel fil. Som standard är den här inställningen "nej", vilket innebär att automatisk sändning av exempelfiler är inaktiverat och användarna får en fråga innan exempel skickas.   (Den här inställningen introducerades i System Center 2012 R2 Configuration Manager SP1)  

    -   Avancerat: **Tillåt användare att ändra inställningar för automatisk sändning av exempel fil**: den här inställningen avgör om en användare med lokala administratörs rättigheter på en enhet kan ändra inställningen för automatisk sändning av exempel fil i klient gränssnittet. Som standard är den här inställningen "nej", vilket innebär att inställningarna endast kan ändras från Configuration Manager-konsolen och lokala administratörer på en enhet kan inte ändra den här konfigurationen.  

         Följande visar till exempel inställningen Windows Defender i Windows 10 som anges av administratören som aktive rad och användaren får inte ändra den:  

         ![TechRef&#95;WinDefender](../../core/get-started/media/TechRef_WinDefender.png "TechRef_WinDefender")  

    Dessutom har den befintliga inställningen **undanta filer och mappar** i avsnittet undantags inställningar i Endpoint Protection-principen för program mot skadlig kod förbättrats för att tillåta enhets undantag. Nu kan du till exempel ange följande som undantag: **\device\mvfs** (för filsystem med flera versioner). Principen validerar inte enhetens sökväg. Endpoint Protection-principen anges för motorn för program mot skadlig kod på klienten som måste kunna tolka enhets strängen.  

**Krav för att använda Endpoint Protection-principer:**  

Innan du kan använda Endpoint Protection-principer måste du installera och hantera Endpoint Protection-klienten genom att använda klient inställningarna för Endpoint Protection. Detta görs med hjälp av System Center Endpoint Protection-klienten för Windows 7, Windows 8, Windows 8,1 eller Managed Windows Defender för Windows 10. Se [Endpoint Protection](../../protect/deploy-use/endpoint-protection.md).  
