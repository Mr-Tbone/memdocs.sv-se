---
title: Hantera LTSB
titleSuffix: Configuration Manager
description: Hanterings skillnader för LTSB av System Center Configuration Manager.
ms.date: 05/01/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8da2887a-fd8e-438c-b926-849c121f7fdf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 86e7579832a5a59c3609d24744eb646e1a4c1fd1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722706"
---
# <a name="manage-the-long-term-servicing-branch-of-configuration-manager"></a>Hantera Long Term Servicing Branch av Configuration Manager

*Gäller för: System Center Configuration Manager (långsiktig service gren)*

När du använder LTSB (Long-term Servicing Branch) för System Center Configuration Manager kan följande hjälpa dig att förstå viktiga ändringar som påverkar hur du hanterar din infrastruktur.

Eftersom LTSB motsvarar Current Branch version 1606 (med vissa undantag som Intune-integrering och molnbaserade funktioner) är de flesta uppgifter som du använder för planering, distribution, konfiguration och daglig hantering detsamma.

Till exempel stöder LTSB samma antal platser, plats typer, klienter och allmän infrastruktur som Current Branch. Därför använder du rikt linjerna i avsnittet planering och design för plats och hierarki för Current Branch. Om du har funktioner med LTSB som stöds av båda grenarna, t. ex. program uppdateringar eller operativ Systems distribution, använder du rikt linjerna i dessa avsnitt i Current Branch-dokumentationen med de varningar som inte har åtkomst till funktions ändringar som införts efter version 1606 av Current Branch.

I följande avsnitt finns information om hur du hanterar aktiviteter som inte liknar varandra.

## <a name="updates-and-servicing"></a>Uppdateringar och service
Endast kritiska säkerhets uppdateringar görs tillgängliga som uppdateringar i konsolen i LTSB.  

Information om vanliga uppdateringar för de efterföljande Current Branch-versionerna visas i-konsolen, men görs inte tillgänglig för LTSB. De laddas inte ned och kan inte installeras.

För att stödja uppdateringar i konsolen för viktiga säkerhets korrigeringar måste en LTSB-plats använda [tjänst anslutnings punkten](../servers/deploy/configure/about-the-service-connection-point.md). Du kan konfigurera den här plats system rollen i offline-eller onlineläge, precis som för Current Branch. LTSB samlar in och skickar samma telemetri och användnings data som Current Branch.

LTSB har stöd för användning av installations programmet för snabb korrigeringar och uppdaterings registrerings verktyget, som dokumenterat för Current Branch.

Allmän information om uppdateringar och underhåll finns i [uppdateringar för Configuration Manager](../servers/manage/updates.md).


## <a name="changes-for-site-expansion-and-the-cdlatest-folder"></a>Ändringar för plats expansion och CD. Senaste mappen
När du kör LTSB och expanderar en fristående primär plats genom att installera en ny central administrations plats måste du använda installations programmet och källfilerna från bas linje mediet för version 1606. För Current Branch kör du installationen och använder källfiler från CD-skivan. Senaste mappen.

Även om du inte kör installations programmet för plats expansion från CD: n. Senaste mappen fortsätter du att använda CD: n. Den senaste mappen för Site Recovery och för att installera en ny underordnad primär plats när din första LTSB-plats var en central administrations plats.

Mer information om plats expansion finns i [expandera en fristående primär plats](../servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand). För ytterligare information om CD: n. Senaste mappen finns [på CD-skivan. Senaste mappen](../servers/manage/the-cd.latest-folder.md).


## <a name="recovery"></a>Återställning
När du återställer en plats måste du återställa platsen eller plats databasen till den ursprungliga grenen. Det går inte att återställa en Current Branch plats databas till en LTSB-installation eller vice versa.
