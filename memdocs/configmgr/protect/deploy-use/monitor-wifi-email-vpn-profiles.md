---
title: Övervaka e-post, Wi-Fi-och VPN-profiler
titleSuffix: Configuration Manager
description: Lär dig hur du övervakar kompatibilitetsstatus för e-post, Wi-Fi och VPN-profiler i Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e2315b8b-98bc-40e1-8ef9-bfb5e69ab109
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 59e372641c303e77f0d88e655bb917660c9e677c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724498"
---
# <a name="monitor-email-wi-fi-and-vpn-profiles-in-configuration-manager"></a>Övervaka e-post, Wi-Fi-och VPN-profiler i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

När du har distribuerat Configuration Manager e-post, Wi-Fi-eller VPN-profiler till användare i hierarkin kan du använda följande procedurer för att övervaka profilens kompatibilitetsstatus:  

-   [Visa resultat för kompatibilitet i Configuration Manager-konsolen](#BKMK_console)  

-   [Så här visar du resultatet av efterlevnaden med hjälp av rapporter](#BKMK_Reports)  

##  <a name="how-to-view-compliance-results-in-the-configuration-manager-console"></a><a name="BKMK_console"></a>Visa resultat för kompatibilitet i Configuration Manager-konsolen  
 Använd den här proceduren för att visa information om kompatibiliteten för distribuerade profiler i Configuration Manager-konsolen.  

#### <a name="to-view-compliance-results-in-the-configuration-manager-console"></a>Så här visar du kompatibilitetsresultat i Configuration Manager-konsolen  

1.  Klicka på **övervakning**i Configuration Manager-konsolen.  

2.  I arbetsytan **Övervakning** klickar du på **Distributioner**.  

3.  I listan **distributioner** väljer du den profil distribution som du vill visa kompatibilitetsinformation för.  

4.  Du kan granska sammanfattnings information om kompatibiliteten för profil distributionen på huvud sidan. Om du vill visa mer detaljerad information väljer du profil distributionen och på fliken **Start** går du till gruppen **distribution** och klickar på **Visa status** för att öppna sidan **distributions status** .  

     På sidan **Distributionsstatus** finns följande flikar:  

    -   **Kompatibel:** Visar kompatibiliteten för profilen som baseras på antalet påverkade till gångar. Du kan dubbelklicka på en regel om du vill skapa en tillfällig nod under noden **Användare** i arbetsytan **Tillgångar och efterlevnad** , som innehåller alla användare som är kompatibla med profilen. I fönstret **till gångs Detaljer** visas de användare som är kompatibla med profilen. Om du dubbelklickar på en användare i listan visas mer information.  

        > [!IMPORTANT]  
        >  En profil utvärderas inte om den inte är tillämplig på en klienten het. den returneras dock som kompatibel.  

    -   **Fel:** Visar en lista över alla fel för den valda profil distributionen som baseras på antalet påverkade till gångar. Du kan dubbelklicka på en regel om du vill skapa en tillfällig nod under noden **Användare** i arbetsytan **Tillgångar och efterlevnad** , som innehåller alla användare som inte är kompatibla med profilen. När du väljer en användare kan du visa alla användare som påverkas av problemet i fönstret **Tillgångsinformation** . Om du dubbelklickar på en användare i listan visas mer information om problemet.  

    -   **Icke-kompatibel:** Visar en lista över alla inkompatibla regler i profilen baserat på antalet till gångar som påverkas. Du kan dubbelklicka på en regel om du vill skapa en tillfällig nod under noden **Användare** i arbetsytan **Tillgångar och efterlevnad** , som innehåller alla användare som inte är kompatibla med profilen. När du väljer en användare kan du visa alla användare som påverkas av problemet i fönstret **Tillgångsinformation** . Om du dubbelklickar på en användare i listan visas ytterligare information om problemet.  

    -   **Okänd:** Visar en lista över alla användare som inte rapporterades som kompatibla för den valda profil distributionen tillsammans med enheternas aktuella klient status.  

5.  På sidan **distributions status** kan du granska detaljerad information om kompatibiliteten för den distribuerade profilen. Under noden **Distributioner** skapas en tillfällig nod som gör att du snabbt hittar den här informationen igen.  

##  <a name="how-to-view-compliance-results-by-using-reports"></a><a name="BKMK_Reports"></a> How to View Compliance Results by Using Reports  
 Kompatibilitetsinställningar, som inkluderar profiler i Configuration Manager, innehåller också ett antal inbyggda rapporter som gör att du kan övervaka information om profiler. De här rapporterna tillhör rapportkategorin **Hantering av efterlevnad och inställningar**.  

> [!IMPORTANT]  
>  Du måste använda ett jokertecken (%) När du använder parametrarna **enhets filter** och **användar filter** i rapporterna för kompatibilitetsinställningar.  

 Mer information om hur du konfigurerar rapportering i Configuration Manager finns i [Introduktion till rapportering](../../core/servers/manage/introduction-to-reporting.md).  
