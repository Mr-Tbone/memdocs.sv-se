---
title: Metod tips för samlingar
titleSuffix: Configuration Manager
description: Få rekommendationer för att konfigurera samlingar och samlings utvärdering i Configuration Manager.
ms.date: 06/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 7a2abb79-9ae5-4a25-9e18-5dcf528de3bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b1bc72a3691e4a6f47c29a5a91ef11c92f0f7e7c
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88693292"
---
# <a name="best-practices-for-collections-in-configuration-manager"></a>Metod tips för samlingar i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

En del samlings hanterings råd kan vara motstridiga. Av prestanda skäl bör du till exempel begränsa antalet samlingar som uppdateras ofta. Men uppdatering av samlingar är ofta användbart eftersom de flesta Configuration Manager-funktionerna är beroende av samlingar. Överväg noggrant både prestanda påverkan och affärs krav när du utformar och konfigurerar samlingar och samlings utvärdering.

Använd följande metod tips för samlingar i Configuration Manager.  

## <a name="configure-maintenance-window-for-updates"></a>Konfigurera underhålls perioden för uppdateringar

Du kan konfigurera underhålls fönster för enhets samlingar för att begränsa de tider som Configuration Manager kan installera program vara på dessa enheter. Om du konfigurerar underhålls perioden så att den är för liten, kanske inte klienten kan installera kritiska program uppdateringar, vilket gör att klienten är sårbar för problem som uppdateringen minskar.

Viktiga överväganden att tänka på när du planerar underhålls Fönstren:

- Standard körnings tiden för program uppdatering är 60 minuter.
- När Configuration Manager beräknar om en uppdatering kan installeras lägger den till fem minuter till den maximala kör tiden för en omstart.
- Den återstående varaktigheten för ett underhålls fönster måste vara längre än den maximala kör tiden för program uppdateringen plus fem minuter.

## <a name="avoid-frequent-collection-evaluation"></a>Undvik regelbunden samlings utvärdering

En fullständig samlings utvärdering utvärderar inte bara mål samlingen, utan även samlingar som samlingen begränsar om en uppdatering sker. En samling utan schema utvärderas heller fortfarande om dess begränsade samlings uppdateringar uppdateras. Det är därför möjligt att vissa samlingar kan utvärderas oftare än förväntat.

I en upptagen Configuration Managers miljö kan du förbättra prestanda för samlings utvärdering genom att skala tillbaka scheman för att undvika utvärdering av upprepad samling. I ett djup träd kan du minska samlings utvärderings frekvensen som samlingarna fallande djupare i trädet, eftersom utvärderingar på högre nivå även utlöser insamlings utvärderingar på lägre nivå.

## <a name="understand-the-collection-evaluation-graph"></a>Förstå diagrammet för samlings utvärdering

Tänk på hur samlings utvärderings diagrammet fungerar så att du kan utforma en lämplig samlings struktur. Förlita dig inte på fullständig samlings utvärdering för att alltid uppdatera alla samlingar. Om det finns en stegvis uppdaterad samlings uppdatering enligt ett schema, kan det hända att referens samlingar som inte är aktiverade för stegvisa uppdateringar inte uppdateras. Eftersom uppdateringar troligen uppstod under stegvisa utvärderingar, kan en fullständig utvärdering inte uppdatera samlingen, vilket avslutar samlings utvärderings diagrammet för den cykeln. I så fall sker inga utvärderingar av insamlings samlingar. Mer information finns i [diagram över samlings utvärdering](collection-evaluation.md#collection-evaluation-graph).

## <a name="limit-incremental-updates"></a><a name="bkmk_incremental"></a> Begränsa stegvisa uppdateringar

Att aktivera stegvisa uppdateringar för många samlingar kan orsaka fördröjningar i utvärderingen. Det är bäst att begränsa antalet stegvis uppdaterade samlingar till 200. Det exakta antalet beror på:

- Totalt antal samlingar
- Hur ofta nya resurser läggs till och ändras i hierarkin
- Antalet klienter i en hierarki
- Komplexiteten vid samlings medlemskaps regler i en hierarki

Om den stegvisa utvärderings cykeln tar längre tid än den konfigurerade uppdaterings frekvensen bearbetar Configuration Manager hela samlings utvärderingarna, vilket kan påverka systemets prestanda. Minska antalet stegvis uppdaterade samlingar eller öka tiden mellan stegvisa utvärderings cykler.

Med tanke på den potentiella påverkan av stegvisa samlingar är det viktigt att ha en princip eller procedur för att skapa samlingarna och tilldela uppdaterings scheman. Exempel på princip överväganden kan vara:

- Använd endast stegvisa uppdateringar för samlingar som används för säkerhets omfattning, klient inställningar och underhålls fönster. De här samlings uppdateringarna påverkar klientens beteende och åtkomst till resurser.
- För program utan licens godkännande, annonsera program till befintliga samlingar och Använd globala villkor för att begränsa tillgängligheten.
- Disponera lämpliga perioder för andra samlingar som har fullständig samlings uppdateringar schemalagda.

## <a name="avoid-evaluation-of-large-trees-from-the-cas"></a>Undvik utvärdering av stora träd från CAS

Den centrala administrations platsen (CAS) utvärderar inte samlings medlemskap i en Configuration Managers miljö. Primära platser är de enda platser som utvärderar samlingar. Sekundära platser fungerar som proxyservrar som bara använder data som de replikerar från den primära platsen.

För att begära en samlings uppdatering skickar CAS en begäran till varje primär plats. De primära platserna utvärderar samlingen och skickar tillbaka resultatet till CAS. Utvärderings resultatet för samlingen visas bara när alla instruktioner för insamlings utvärdering replikeras till alla platser, alla platser utvärderar alla samlingar och alla data återgår till certifikat utfärdarna och konsoliderar.

Följande diagram visar flödet när CAS begär en manuell samlings uppdatering:

![Manuell samlings uppdatering från en certifikat utfärdare](media/manual-collection-update-from-cas.png)

En samlings uppdatering från en certifikat utfärdare med flera primära platser kan ta lång tid. Om en samling inte utvärderas inom rimlig tid, är det frestande att upprepa begäran.

När en samlings utvärderings tråd börjar och läser in utvärderings diagrammet fortsätter utvärderingen tills samlings utvärderings diagrammet är tomt. Tråden avslutas sedan och blir tillgänglig för nästa utvärdering. Men om en annan samling utvärderings cykel köer medan tråden utvärderar samlingar, startar tråden omedelbart om för att försöka utvärdera den "missade" cykeln.

Varje utvärderings metod körs i sin egen tråd. Det är möjligt att Configuration Manager i tråden kan försöka att grafa samma samling mer än en gång. Configuration Manager släpper sedan den andra och efterföljande begär Anden.

Undvik de här scenarierna genom att undvika manuell samlings utvärdering av stora träd, särskilt när du arbetar från certifikat utfärdare med flera platser.

## <a name="consider-collection-depth-and-cross-referencing"></a>Överväg samlings djupet och kors referensen

För att skapa ett saldo mellan verksamhets krav och prestanda är det viktigt att förstå samlings strukturen som du skapar och dess beroenden för andra samlingar. Om du skapar en samling med regler som refererar till en eller flera samlingar som också hänvisar till andra samlingar, utvärderas alla samlingar för att skapa medlemskapet i samlingen.

Samlings reglerna inkludera och utelämna i Configuration Manager göra referens samlingar enklare än att skriva en anpassad WQL-fråga. Men om du använder include-och exclude Collection-resultat i en högpresterande avgift kan du använda WQL-fråge metoden i stället:

Omfattar

`Select * from SMSRSystem where SMSRSystem.ResourceId in (select ResourceID from SMS_CM_RES_COLL_[collection id])`

Ingå

`Select * from SMSRSystem where SMSRSystem.ResourceId not in (select ResourceID from SMS_CM_RES_COLL_[collection id])`

## <a name="use-ceviewer-to-monitor-collection-evaluation"></a>Använd CEViewer för att övervaka samlings utvärdering

Du kan använda [CEViewer (Collection Evaluation Viewer)](../../../support/ceviewer.md) för att övervaka hur många samlingar som utvärderas och hur lång tid varje samling tar att uppdatera. CEViewer finns i *CD-skivan. Den senaste* mappen på plats servern.

Om du vill utföra en liknande kontroll med SQL manuellt kan du använda följande fråga:

```sql
SELECT [t2].[CollectionName], [t2].[SiteID], [t2].[value] AS [Seconds], [t2].[LastIncrementalRefreshTime], [t2].[IncrementalMemberChanges] AS [IncChanges], [t2].[LastMemberChangeTime] AS [MemberChangeTime]
FROM (
    SELECT [t0].[CollectionName], [t0].[SiteID], DATEDIFF(Millisecond, [t1].[IncrementalEvaluationStartTime], [t1].[LastIncrementalRefreshTime]) * 0.001 AS [value], [t1].[LastIncrementalRefreshTime], [t1].[IncrementalMemberChanges], [t1].[LastMemberChangeTime], [t1].[IncrementalEvaluationStartTime], v1.[RefreshType]
    FROM [dbo].[Collections_G] AS [t0]
    INNER JOIN [dbo].[Collections_L] AS [t1] ON [t0].[CollectionID] = [t1].[CollectionID]
    inner join v_Collection v1 on [t0].[siteid] = v1.CollectionID
    ) AS [t2]
WHERE ([t2].[IncrementalEvaluationStartTime] IS NOT NULL) AND ([t2].[LastIncrementalRefreshTime] IS NOT NULL) and (refreshtype='4' or refreshtype='6')
ORDER BY [t2].[value] DESC
```