---
title: Konfigurera platser och hierarkier
titleSuffix: Configuration Manager
description: Läs igenom den här check listan för att se till att du anser de vanligaste konfigurationerna som påverkar både platser och hierarkier.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9efb4061-f642-48bd-8332-3357ff5b3118
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e996c31a4f1aaa9224e4c6d1d435f79adf7ac23c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720998"
---
# <a name="configure-sites-and-hierarchies-for-configuration-manager"></a>Konfigurera platser och hierarkier för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

När du har installerat din första Configuration Manager-plats eller lagt till fler platser i hierarkin använder du den här check listan för att se till att du anser de vanligaste konfigurationerna som påverkar både platser och hierarkier.  

Följande konfigurations anmärkningar gäller för de flesta distributioner:  

- Vissa alternativ bygger på varandra, till exempel Active Directory identifiering av skogar, gränser och gräns grupper.  

- Flera konfigurationer har standardvärden som du kan använda utan konfigurations ändringar, åtminstone för att starta.  

- Andra konfigurationer, till exempel gränser grupper och distributions plats grupper, kräver att du konfigurerar dem innan du använder.  

| Action | Information |  
|------------|-------------|  
| Konfigurera rollbaserad administration | Åtskilj administrations tilldelningar för att styra vilka administrativa användare som kan visa och hantera olika objekt och data i din Configuration Managers miljö.<br /><br /> Konfigurationer för rollbaserad administration delas med alla platser i en hierarki.   <br/><br/>Mer information finns i [Konfigurera rollbaserad administration](configure-role-based-administration.md). |  
| Publicera plats data till Active Directory Domain Services | Gör det enkelt för klienter att hitta tjänster och effektivt använda plats resurser.<br /><br /> [Utöka först Active Directory-schemat](../../../plan-design/network/extend-the-active-directory-schema.md). Konfigurera varje plats för att [publicera plats data](publish-site-data.md) individuellt |  
| Konfigurera en tjänstanslutningspunkt | Planera för att installera och konfigurera tjänst anslutnings punkten på platsen på den översta nivån i hierarkin. Mer information finns i [om tjänst anslutnings punkten](about-the-service-connection-point.md). |  
| Lägga till platssystemroller | Installera en eller flera ytterligare plats system roller för enskilda platser. Mer information finns i [lägga till plats system roller](add-site-system-roles.md). |  
| Konfigurera platsgränser och gränsgrupper | Ange gränser som definierar nätverks platser i intranätet som kan innehålla enheter som du vill hantera. Konfigurera sedan gränser grupper så att klienter på dessa nätverks platser kan hitta Configuration Manager resurser. Mer information finns i [definiera plats gränser och gräns grupper](define-site-boundaries-and-boundary-groups.md). |  
| Konfigurera distributionsplatsgrupper | Konfigurera logiska grupper av distributions platser för att förenkla hanteringen av distributioner. Mer information finns i [Hantera distributions plats grupper](install-and-configure-distribution-points.md#bkmk_manage). |  
| Kör Discovery | Kör identifiering för att hitta resurser i nätverket, inklusive nätverks infrastruktur, enheter och användare.<br /><br /> Mer information finns i [Kör identifiering](run-discovery.md). |  
| Lägg till redundans och kapacitet för administratörer | Installera ytterligare SMS-providers och Configuration Manager-konsoler för att utöka kapaciteten för administratörer att hantera din infrastruktur:<br /><br /> **Installera ytterligare SMS-providers** för att tillhandahålla redundans för konsol-och API-anslutningar till platsen. Mer information finns i [Hantera SMS-providern](../../manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider).<br /><br /> **Installera ytterligare Configuration Manager-konsoler** för att ge åtkomst till ytterligare administrativa användare. Mer information finns i [installera Configuration Manager-konsoler](../install/install-consoles.md). |  
| Konfigurera platskomponenter | Konfigurera plats komponenter på varje plats för att ändra beteendet för plats system roller och rapportering av plats status. Mer information finns i [plats komponenter](site-components.md). |  
| Skapa anpassade samlingar | Med hjälp av information som platsen identifierar om enheter och användare skapar du anpassade samlingar med objekt för att förenkla framtida hanterings uppgifter. Mer information finns i [så här skapar du samlingar](../../../clients/manage/collections/create-collections.md). |  
| Konfigurera inställningar för att hantera högriskdistributioner | Konfigurera inställningar på en plats för att varna administratörer när de skapar en högrisk distribution. Mer information finns i [Inställningar för att hantera distributioner med hög risk](../../manage/settings-to-manage-high-risk-deployments.md). |  
| Konfigurera databasrepliker för hanteringsplatser | Konfigurera en databas replik för att minska processor belastningen som placeras på plats databas servern av hanterings platser när de hanterar begär Anden från klienter. Mer information finns i [databas repliker för hanterings platser](database-replicas-for-management-points.md). |  
| Konfigurera en SQL Server Always on-tillgänglighetsgrupper | Konfigurera tillgänglighets grupper som lösningar med hög tillgänglighet och katastrof återställning för att vara värd för plats databasen på primära platser och den centrala administrations platsen. Mer information finns i [SQL Server AlwaysOn för en plats databas med hög](sql-server-alwayson-for-a-highly-available-site-database.md)tillgänglighet. |  
| Ändra replikering mellan platser | Se [data överföringar mellan platser](../../../plan-design/hierarchy/data-transfers-between-sites.md) för att lära dig mer om följande ämnen:<br /><br /> Konfigurera [filbaserad replikering](../../../plan-design/hierarchy/file-based-replication.md) mellan sekundära platser<br /><br /> Konfigurera [Länkar för databasreplikering](../../../plan-design/hierarchy/database-replication.md)<br /><br /> Konfigurera [distribuerade vyer](../../../plan-design/hierarchy/database-replication.md#bkmk_distviews) |  
| Konfigurera plats servrar i passivt läge | Från och med version 1806 konfigurerar du en plats server i passivt läge för varje primär plats och den centrala administrations platsen. Den här funktionen tillhandahåller en plats server med hög tillgänglighet. Mer information finns i [hög tillgänglighet för plats Server](site-server-high-availability.md). |  
