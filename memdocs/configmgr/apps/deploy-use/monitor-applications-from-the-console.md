---
title: Övervaka program från konsolen
titleSuffix: Configuration Manager
description: Övervaka distribution av program vara, inklusive uppdateringar, kompatibilitetsinställningar och program med hjälp av arbets ytan övervakning i Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 784c295c-b8b8-4202-ab9f-665908d49d6d
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 892a55ad4f3518794bef017f1d4e3a7a4de14e13
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710057"
---
# <a name="monitor-applications-from-the-configuration-manager-console"></a>Övervaka program från Configuration Manager-konsolen

*Gäller för: Configuration Manager (aktuell gren)*


I Configuration Manager kan du övervaka distributionen av all program vara, inklusive program uppdateringar, kompatibilitetsinställningar, program, aktivitetssekvenser samt paket och program. Du kan övervaka distributioner med hjälp av arbets ytan **övervakning** i Configuration Manager-konsolen eller med hjälp av rapporter.  

 Program i Configuration Manager stöd för tillstånds övervakning, som gör att du kan spåra den senaste program distributions statusen för användare och enheter. De här statusmeddelandena visar information om enskilda enheter. Om ett program exempelvis distribueras till en samling användare kan du Visa kompatibilitetstillstånd för distributionen och distributions syftet i Configuration Manager-konsolen.  

## <a name="learn-about-compliance-states"></a>Läs om efterlevnadsprinciper
 En programdistributionsstatus har en av följande kompatibilitetsstatusar:  

-   **Klar** – Programdistributionen lyckades eller var redan installerad.  

-   **Pågår** – Programdistributionen pågår.  

-   **Okänd** – Det gick inte att avgöra statusen för programdistributionen. Den här statusen gäller inte för distributioner med syftet **Tillgänglig**. Den här statusen visas normalt när statusmeddelanden från klienten inte har tagits emot än.  

-   **Kraven har inte uppfyllts** – Programmet distribuerades inte eftersom det inte uppfyllde ett beroende eller en regel för krav eller eftersom operativsystemet som det distribuerades till inte var tillämpligt.  

-   **Fel** – Programmet kunde inte distribueras på grund av ett fel.  

Du kan visa ytterligare information för varje kompatibilitetstillstånd, inklusive under kategorier inom kompatibilitetstillstånd och antalet användare och enheter i den här kategorin. Till exempel innefattar kompatibilitetsstatusen **Fel** följande underkategorier:  

- Felutvärderingskrav  

- Innehållsrelaterade fel  

- Installationsfel  

  När fler än en kompatibilitetsstatus gäller för en programdistribution kan du se den samlade statusen som motsvarar den lägsta kompatibiliteten. Ett exempel:  

  -   Om en användare loggar in på två enheter och programmet har installerats på en enhet men inte kan installeras på den andra enheten, visas det sammanställda distributions läget för den användaren som **fel**.  

  -   Om ett program distribueras till alla användare som loggar in på en dator får du flera distributions resultat för den datorn. Om en av distributionerna misslyckas visas den samlade distributionsstatusen för datorn som **Fel**.  

Distributionsstatusen för paketdistribution och programdistribution sammanställs inte.  

 Använd de här underkategorierna för att snabbt kunna identifiera eventuella viktiga problem med en programdistribution. Du kan även visa ytterligare information om de enheter som faller inom en särskild underkategori av en kompatibilitetsstatus.  

 Program hanteringen i Configuration Manager innehåller ett antal inbyggda rapporter som gör att du kan övervaka information om program och distributioner. De här rapporterna tillhör rapportkategorin **Programdistribution – programövervakning**.  

 Mer information om hur du konfigurerar rapportering i Configuration Manager finns i [Introduktion till rapportering](../../core/servers/manage/introduction-to-reporting.md).  

## <a name="monitor-the-state-of-an-application-in-the-configuration-manager-console"></a>Övervaka status för ett program i Configuration Manager-konsolen  

1.  I Configuration Manager-konsolen väljer du **övervakning**av  >  **distributioner**.  

3.  Om du vill granska distributions information för varje kompatibilitetstillstånd och enheterna i det tillståndet väljer du en distribution och klickar sedan på Visa status i gruppen **distribution** på fliken **Start** . i fönstret distribution väljer du **Visa status** för att öppna fönstret **distributions status** . I det här fönstret kan du visa tillgångarna för varje kompatibilitetsstatus. Välj en till gång för att visa mer detaljerad information om distributions statusen för till gången.  

    > [!NOTE]  
    >  Antal objekt som kan visas i rutan **Distributionsstatus** är begränsat till 20 000. Om du behöver se fler objekt använder du Configuration Manager-rapporter för att visa information om program status.  
    >   
    >  Statusen för distributionstyperna samlas i fönstret **Distributionsstatus** . Du kan visa mer detaljerad information om distributionstyperna med rapporten **Fel i programinfrastrukturen** i rapportkategorin **Programdistribution – programövervakning**.  

4.  Om du vill granska allmän statusinformation om en program distribution väljer du en distribution och klickar sedan på fliken **Sammanfattning** i det **valda distributions** fönstret.  

5.  Om du vill granska information om program distributions typen väljer du en distribution och klickar sedan på fliken **distributions typer** i det **valda distributions** fönstret.  

Informationen som visas i fönstret **distributions status** när du har valt **Visa status** är real tids data från Configuration Manager databasen. Informationen som visas på fliken **Sammanfattning** och fliken **distributions typer** är sammanfattade data.

Om data som visas på fliken **Sammanfattning** och fliken **distributions typer** inte matchar de data som visas i fönstret **distributions status** väljer du **Kör sammanfattning** för att uppdatera data på dessa flikar. Du kan konfigurera standardsammanfattningsintervallet för programdistribution så här:  

1. I Configuration Manager-konsolen väljer du **Administration**  >  **plats konfiguration**  >  **platser**.

2. I listan **platser** väljer du den plats som du vill konfigurera sammanfattnings intervallet för. gå sedan till fliken **Start** . i gruppen **Inställningar** väljer du **status sammanfattningar**.

3. I dialog rutan **status sammanfattningar** väljer du **Sammanfattning för program distribution**och väljer sedan **Redigera**.  

4. I dialog rutan **Egenskaper för sammanfattning för program distribution** konfigurerar du de obligatoriska sammanfattnings intervallen och väljer sedan **OK**.  
