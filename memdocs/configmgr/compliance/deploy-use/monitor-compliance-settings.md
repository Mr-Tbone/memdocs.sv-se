---
title: Övervaka kompatibilitetsinställningar
titleSuffix: Configuration Manager
description: Använd en eller flera av procedurerna i det här avsnittet för att Visa konfigurations bas linjens kompatibilitetsstatus.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 92c1ccca-a748-44cd-a52e-e41d34bf981d
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: e2a378c1f54eb9bccbcc21f50419176bd39cb3ac
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240056"
---
# <a name="monitor-compliance-settings-in-configuration-manager"></a>Övervaka kompatibilitetsinställningar i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

När du har distribuerat Configuration Manager konfigurations bas linjer till enheter i hierarkin kan du använda en eller flera av procedurerna i det här avsnittet för att Visa konfigurations bas linjens kompatibilitetsstatus:

> [!NOTE]  
>  Fälten för verifieringsvillkor i rapporterna för kompatibilitetsinställningar ( **Begränsningar**i rapporten på klientsidan) visar det underliggande SML-språket (Service Modeling Language). Detta kan göra det svårt för administratörer som har skapat konfigurationsobjektet i Configuration Manager-konsolen att förstå vad verifierings villkoren är om de inte har kunskap om SML. I det här fallet använder du arbets ytan **övervakning** i Configuration Manager-konsolen för att visa egenskaperna för konfigurationsobjektet och dess verifierings villkor.  

##  <a name="view-compliance-results-in-the-configuration-manager-console"></a>Visa kompatibilitetsresultat i Configuration Manager-konsolen  
 Använd den här proceduren för att visa information om kompatibiliteten för distribuerade konfigurations bas linjer i Configuration Manager-konsolen.  

### <a name="view-compliance-results-in-the-configuration-manager-console"></a>Visa kompatibilitetsresultat i Configuration Manager-konsolen  

1.  I Configuration Manager-konsolen klickar du på **övervakning**av  >  **distributioner**.  

3.  Välj den konfigurationsbaslinjedistribution som du vill visa kompatibilitetsinformation om i listan **Distributioner** .  

4.  Du kan granska sammanfattningsinformationen om distributionens kompatibilitet på huvudsidan. Om du vill visa mer detaljerad information markerar du konfigurationsbaslinjedistributionen och öppnar sidan **Distributionsstatus** genom att klicka på **Visa status** i gruppen **Distribution** på fliken **Start** .  

     På sidan **Distributionsstatus** finns följande flikar:  

    -   **Kompatibel**: Visar konfigurationsbaslinjens kompatibilitet baserat på antalet tillgångar som påverkas. Du kan klicka på en regel om du vill skapa en tillfällig nod under noden **Användare** eller **Enheter** i arbetsytan **Tillgångar och efterlevnad**, som innehåller alla användare eller enheter som är kompatibla med regeln. I rutan **Tillgångsdetaljer** visas de användare eller enheter som är kompatibla med konfigurationsbaslinjen. Dubbelklicka på en användare eller enhet i listan om du vill visa mer information.  

        > [!IMPORTANT]  
        >  En konfigurations objekt regel utvärderas inte om den inte identifieras eller inte är tillämplig på en klienten het. regeln returneras dock som kompatibel.  

    -   **Fel**: Visar en lista med alla fel för den valda konfigurationsbaslinjedistributionen baserat på antalet tillgångar som påverkas. Du kan klicka på en regel om du vill skapa en tillfällig nod under noden **Användare** eller **Enheter** i arbetsytan **Tillgångar och efterlevnad**, som innehåller alla användare eller enheter som genererade fel med den här regeln. När du väljer en användare eller enhet kan du visa alla användare eller enheter som påverkas av problemet i fönstret **Tillgångsinformation**. Dubbelklicka på en användare eller enhet i listan om du vill visa mer information om problemet.  

    -   **Inkompatibel**: Visar en lista över alla inkompatibla regler i konfigurationsbaslinjen baserat på antalet tillgångar som påverkas. Du kan klicka på en regel om du vill skapa en tillfällig nod under noden **Användare** eller **Enheter** i arbetsytan **Tillgångar och efterlevnad**, som innehåller alla användare eller enheter som inte är kompatibla med den här regeln. När du väljer en användare eller enhet kan du visa alla användare eller enheter som påverkas av problemet i fönstret **Tillgångsinformation**. Om du dubbelklickar på en användare eller enhet i listan visas ytterligare information om problemet.  

    -   **Okänd**: Visar en lista över alla användare och enheter som inte rapporterade kompatibilitet för den valda konfigurationsbaslinjedistributionen jämte enheternas aktuella klientstatus.  

5.  På sidan **Distributionsstatus** kan du granska detaljerad information om kompatibiliteten för den distribuerade baslinjen. Under noden **Distributioner** skapas en tillfällig nod som gör att du snabbt hittar den här informationen igen.  

##  <a name="view-compliance-results-by-using-reports"></a>Visa resultat för kompatibilitet med hjälp av rapporter  
 Kompatibilitetsinställningar i Configuration Manager innehåller ett antal inbyggda rapporter som gör att du kan övervaka information om konfigurations objekt, konfigurations bas linjer och distributioner. De här rapporterna tillhör rapportkategorin **Hantering av efterlevnad och inställningar**.  

> [!IMPORTANT]  
>  Du måste använda ett jokertecken ( **%** ) när du använder parametrarna **enhets filter** och användar filter i rapporterna för kompatibilitetsinställningar.  

 Mer information om hur du konfigurerar rapportering i Configuration Manager finns i [Introduktion till rapportering](../../core/servers/manage/introduction-to-reporting.md).

##  <a name="view-compliance-results-on-a-configuration-manager-windows-client-computer"></a>Visa resultat för kompatibilitet på en Configuration Manager Windows-klientdator

> [!NOTE]  
>  Du kan inte Visa information på Configuration Manager Windows-klienten om du är inloggad med ett gäst konto för domänen.    

1.  Gå till **Configuration Manager** på Kontrollpanelen på klientdatorn och dubbelklicka för att öppna dess egenskaper.  

2.  Klicka på fliken **Konfigurationer** så visas listan med distribuerade konfigurationsbaslinjer.  

3.  Visa **Kompatibilitetstillstånd** för varje konfigurationsbaslinje:  

    > [!IMPORTANT]  
    >  Utvärderingsresultatet cachelagras på klienten i 15 minuter. Om du startar en ny utvärdering inom 15-minutersperioden returneras kompatibilitetsresultaten från det här cacheminnet i stället för en ny utvärdering. Om du gör en ändring på klienten som kan påverka resultatet från kompatibilitetsutvärderingen väntar du därför tills de 15 minuterna har förflutit innan du påbörjar en ny utvärdering.  

    -   **Kompatibel**: Klientdatorn är kompatibel med den utvärderade konfigurationsbaslinjen.  

    -   **Inkompatibel**: Klientdatorn är inte kompatibel med den utvärderade konfigurationsbaslinjen.  

    -   **Okänd**: Klientdatorn har inte utvärderat konfigurationsbaslinjen än. Om du vill initiera utvärderingen utanför kompatibilitetsutvärderingsschemat väljer du de konfigurationsbaslinjer som du vill utvärdera och klickar sedan på **Utvärdera**.  

        > [!NOTE]  
        >  Om du har behörighet som lokal administratör på klientdatorn kan du visa information om varje utvärderad konfigurationsbaslinje för att se vilket konfigurationsobjekt som rapporterar status som inkompatibel. Om du vill göra det väljer du konfigurationsbaslinjen och klickar på **Visa rapport**.  

4.  Klicka på **OK**.  

##  <a name="create-collections-based-on-configuration-baseline-compliance"></a>Skapa samlingar baserat på konfigurations bas linjernas kompatibilitet  
 Använd följande procedur för att skapa en Configuration Manager samling baserat på enheter med en angiven kompatibilitet. Du kan skapa samlingar baserat på följande kompatibilitetstillstånd:  

-   **Kompabilitet**  

-   **Fel**  

-   **Ej kompatibel**  

-   **Okänt**  

1.  I Configuration Manager-konsolen klickar du på **till gångar och efterlevnad**  >  **kompatibilitetsinställningar**  >  **konfigurations bas linjer**.  

3.  Välj den konfigurationsbaslinje i listan **Konfigurationsbaslinjer** som du vill skapa en samling från.  

4.  Klicka på **Skapa ny samling** i **Distributionsgrupp**på fliken **Distribution** och välj den kompatibilitetsnivå i listrutan som du vill skapa en samling för.  

5.  Guiden **Skapa användarsamling** eller guiden **Skapa enhetssamling** öppnas beroende på om konfigurationsobjektet distribueras till användare eller enheter. Guiden fylls i automatiskt med korrekta värden för att skapa samlingen, men du kan ändra värdena.  

6.  När du har slutfört guiden visas samlingen under noden **Användarsamlingar** eller **Enhetssamlingar** på arbetsytan **Tillgångar och efterlevnad** .  
