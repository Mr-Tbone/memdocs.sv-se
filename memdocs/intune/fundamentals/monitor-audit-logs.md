---
title: Granskningsändringar och händelser i Microsoft Intune – Azure | Microsoft Docs
description: Lär dig att gå igenom granskningsloggar som registrerar Microsoft Intune-aktiviteter.
keywords: ''
ms.author: dougeby
author: dougeby
manager: dougeby
ms.date: 03/18/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 6ee841cc-5694-4ba1-8f66-1d58edec30a4
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1808743685c6907c11da23f92c5e263860098bea
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88909694"
---
# <a name="use-audit-logs-to-track-and-monitor-events-in-microsoft-intune"></a>Använd granskningsloggar för att spåra och övervaka händelser i Microsoft Intune

Granskningsloggar innehåller en post med aktiviteter som genererar en ändring i Microsoft Intune. Åtgärder för att skapa, uppdatera (redigera), ta bort och tilldela samt fjärråtgärder skapar granskningshändelser som administratörer kan granska för de flesta Intune-arbetsbelastningar. Som standard är granskning aktiverat för alla kunder. Det kan inte inaktiveras.

> [!NOTE]
> Granskningshändelser började registreras i lanseringen från december 2017. Tidigare händelser är inte tillgängliga.

## <a name="who-can-access-the-data"></a>Vem som kan komma åt data?

Användare med följande behörigheter kan gå igenom granskningsloggar:

- Global administratör
- Intune Service-administratör
- Administratörer som har tilldelats en roll för Intune med behörighet **Granska data** - **Läs**

## <a name="audit-logs-for-intune-workloads"></a>Granskningsloggar för arbetsbelastningar för Intune

Du kan gå igenom granskningsloggar i övervakningsgruppen för varje arbetsbelastning i Intune:

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj **Administration av klientorganisation** > **Granskningsloggar**.
3. Filtrera resultatet genom att välja **Filtrera** och förfina resultaten med hjälp av följande alternativ.
    - **Kategori**: till exempel **Efterlevnad**, **Enhet** och **Roll**.
    - **Aktivitet**: de alternativ som anges här begränsas av det alternativ som väljs under **Kategori**.
    - **Datumintervall**: du kan välja loggar för föregående månad, vecka eller dag.
4. Välj **Använd**.
4. Markera ett objekt i listan om du vill se aktivitetsdetaljerna.

## <a name="route-logs-to-azure-monitor"></a>Dirigera loggar till Azure Monitor

Granskningsloggar och arbetsloggar kan även dirigeras till Azure Monitor. I **Granskningsloggar** väljer du **Exportera datainställningar**:

![Exportera loggdata till Azure Monitor genom att Exportera datainställningar i Intune](./media/monitor-audit-logs/audit-logs-export-data-settings.png)

> [!NOTE]
> Mer information om den här funktionen och för att granska kraven för att använda den finns i [Skicka loggdata till lagring, händelsehubbar eller logganalys](review-logs-using-azure-monitor.md).

> [!NOTE]
> **Initierad av (aktör)** innehåller information om vem som körde uppgiften och var den kördes. Om du t.ex. utför aktiviteten i Intune i Azure Portal, visar **Program** alltid **Microsoft Intune-portaltillägg** och **Program-ID** använder alltid samma GUID.
>
> Avsnittet **Mål** anger flera mål och de egenskaper som har ändrats.  

## <a name="use-graph-api-to-retrieve-audit-events"></a>Använd Graph API för att hämta granskningshändelser

Mer information om hur du använder Graph API för att hämta upp till ett års granskningshändelser finns i [Lista över auditEvents](/graph/api/intune-auditing-auditevent-list?view=graph-rest-1.0).

## <a name="next-steps"></a>Nästa steg

[Skicka data till lagring, händelsehubbar eller logganalys](review-logs-using-azure-monitor.md).

[Granska loggarna för klientappskydd](../apps/app-protection-policy-settings-log.md).