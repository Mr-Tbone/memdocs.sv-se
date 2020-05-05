---
title: Övervaka certifikatprofiler
titleSuffix: Configuration Manager
description: Lär dig hur du övervakar kompatibilitetsstatus för Configuration Manager certifikat profiler.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 98feaa06-64b1-4e86-a122-93017c97cd4f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ee1f43e113aa91f75c09bd264e8b3bc2704220a8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722300"
---
# <a name="how-to-monitor-certificate-profiles-in-configuration-manager"></a>Övervaka certifikat profiler i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*


##  <a name="view-compliance-results-in-the-configuration-manager-console"></a>Visa resultat för kompatibilitet i Configuration Manager-konsolen  

Om du vill övervaka kompatibilitet för SCEP-certifikat använder du inte-konsolen istället, använder du [rapporter](#view-compliance-results-by-using-reports). 

1. I Configuration Manager-konsolen väljer du **övervakning**>  av**distributioner**.  

2. Välj certifikat profil distributionen av intresse.  

3. Granska information om Sammanfattning av certifikat på huvud sidan. Om du vill ha mer detaljerad information markerar du certifikat profilen och väljer sedan **Visa status** i gruppen **distribution** på fliken **Start** , så öppnas sidan **distributions status** .  

    På sidan **Distributionsstatus** finns följande flikar:  

   -   **Kompatibel**: Visar certifikatprofilens efterlevnad baserat på antalet tillgångar som påverkas. Du kan dubbelklicka på en regel om du vill skapa en tillfällig nod under noden **Användare** i arbetsytan **Tillgångar och efterlevnad** . Den här noden innehåller alla användare som är kompatibla med certifikatprofilen. I rutan **Tillgångsdetaljer** visas även användare som är kompatibla med profilen. Dubbelklicka på en användare i listan om du vill ha mer information.  

       > [!IMPORTANT]  
       >  En certifikatprofil utvärderas inte om den inte är tillämplig på en klientenhet. Den visas dock som kompatibel.  

   -   **Fel**: Innehåller en lista med alla fel för den valda certifikatprofildistributionen, baserat på antalet tillgångar som påverkas. Du kan dubbelklicka på en regel om du vill skapa en tillfällig nod under noden **Användare** i arbetsytan **Tillgångar och efterlevnad** . Den här noden innehåller alla användare som gav upphov till fel när profilen användes. När du väljer en användare kan du visa alla användare som påverkas av problemet i fönstret **Tillgångsinformation** . Dubbelklicka på en användare i listan om du vill visa mer information.  

   -   **Icke-kompatibel**: Visar en lista med alla inkompatibla regler inom certifikatprofilen, baserat på antalet tillgångar som påverkas. Du kan dubbelklicka på en regel om du vill skapa en tillfällig nod under noden **Användare** i arbetsytan **Tillgångar och efterlevnad** . Den här noden innehåller alla användare som inte är kompatibla med profilen. När du väljer en användare kan du visa alla användare som påverkas av problemet i fönstret **Tillgångsinformation** . Om du dubbelklickar på en användare i listan visas ytterligare information om problemet.  

   -   **Okänd**: Visar en lista med alla användare som inte rapporterades som kompatibla för den valda certifikatprofildistributionen, tillsammans med enheternas aktuella klientstatusar.  

4. På sidan **distributions status** granskar du detaljerad information om kompatibiliteten för den distribuerade certifikat profilen. Under noden **Distributioner** skapas en tillfällig nod som gör att du snabbt hittar den här informationen igen.  

    Certifikatets registreringsstatus visas som ett siffervärde. Följande tabell kan användas för att tolka siffervärdenas innebörd:  


   | Registreringsstatus |                                                                                                                   Beskrivning                                                                                                                   |
   |-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |    0x00000001     |                                                                                         Registreringen lyckades och certifikatet har utfärdats.                                                                                          |
   |    0x00000002     |                                                                    Begäran har skickats och registrering inväntas eller så har begäran utfärdats out-of-band.                                                                    |
   |    0x00000004     |                                                                                                          Registreringen måste senareläggas.                                                                                                           |
   |    0x00000010     |                                                                                                               Ett fel inträffade.                                                                                                                |
   |    0x00000020     |                                                                                                        Registreringsstatusen är okänd.                                                                                                        |
   |    0x00000040     | Statusinformationen har hoppats över. Detta kan inträffa om HYPERLÄNKen<https://msdn.microsoft.com/windows/ms721572>"\l" _security_certification_authority_gly "certifikat utfärdare inte är giltig eller inte har valts för övervakning. |
   |    0x00000100     |                                                                                                           Registrering har nekats.                                                                                                           |

##  <a name="view-compliance-results-by-using-reports"></a>Visa resultat för kompatibilitet med hjälp av rapporter

Kompatibilitetsinställningar i Configuration Manager innehåller inbyggda rapporter som du kan använda för att övervaka information om certifikat profiler. De här rapporterna tillhör rapportkategorin **Hantering av efterlevnad och inställningar**.  

> [!IMPORTANT]  
>  Jokertecken (%) måste användas om du använder parametrarna **Enhetsfilter** och **Användarfilter** i rapporterna för kompatibilitetsinställningar.  

Om du vill övervaka SCEP-certifikatets kompatibilitet använder du dessa certifikat rapporter under rapporten **företagets resurs åtkomst**:  

-   Historik för certifikat som utfärdats  
-   Lista över tillgångar med certifikat som snart slutar att gälla  
-   Visar en lista över tillgångar efter status för certifikatutfärdande  



 Mer information om hur du konfigurerar rapportering i Configuration Manager finns i [Introduktion till rapportering](../../core/servers/manage/introduction-to-reporting.md).  
