---
title: Planera för rapportering
titleSuffix: Configuration Manager
description: Från installations information till säkerhet och nätverks bandbredd är det viktigt att planera för rapportering i Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ff920c84-d5c8-458c-b67f-bc7219b05690
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 2621a6a364734a1146700aa8eef8fded3a6e58ab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713683"
---
# <a name="plan-for-reporting-in-configuration-manager"></a>Planera för rapportering i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Rapportering i Configuration Manager innehåller en uppsättning verktyg och resurser som hjälper dig att använda de avancerade rapporterings funktionerna i SQL Server Reporting Services eller Power BI-rapportserver. Använd följande avsnitt för att få hjälp att planera för rapportering i Configuration Manager.

## <a name="where-to-install-the-reporting-services-point"></a>Var repor ting Services-platsen ska installeras

När du kör Configuration Manager rapporter på en plats har rapporterna till gång till informationen i den plats databas som den ansluter till. Använd följande avsnitt för att avgöra var du ska installera Reporting Services-platsen samt vilken datakälla du ska använda.

> [!NOTE]
> Mer information om hur du planerar för plats system i Configuration Manager finns i [lägga till plats system roller](../deploy/configure/add-site-system-roles.md).

### <a name="supported-site-system-servers"></a> Platssystemservrar som stöds

Du kan installera repor ting Services-platsen på en central administrations plats (ca) och primära platser. Den fungerar på flera plats system på en plats och på andra platser i hierarkin. Configuration Manager har inte stöd för repor ting Services-platsen på sekundära platser. Den första repor ting Services-platsen på en plats anges som standard rapport Server. Du kan lägga till fler repor ting Services-platser på en plats, men Configuration Manager rapporter aktivt använder standard rapport servern på varje plats. Installera repor ting Services-platsen på plats servern eller ett fjärrplatssystem. För bästa prestanda bör du använda SQL Server Reporting Services på en fjärrplats system Server.

### <a name="data-replication-considerations"></a> Överväganden för datareplikering

Överväg följande faktorer när du ska avgöra var du vill installera dina Reporting Services-platser:

- En repor ting Services-plats med CAS-databasen som rapport data källa har till gång till alla globala data och plats data i Configuration Manager hierarkin. Om du behöver rapporter som innehåller plats data för flera platser i en hierarki, bör du överväga att installera repor ting Services-platsen på ett plats system på certifikat utfärdarna. Använd sedan dess databas som rapport data källa.

- En repor ting Services-plats med en underordnad primär plats databas som rapport data källa har endast åtkomst till globala data och plats data för den lokala primära platsen och eventuella underordnade sekundära platser. Plats data för andra primära platser i Configuration Manager hierarkin replikeras inte till den primära platsen. Repor ting Services kan inte komma åt plats data för andra primära platser. Om du behöver rapporter som innehåller plats data för en viss primär plats eller globala data, och du inte vill att användaren ska ha åtkomst till plats data från andra primära platser, installerar du en repor ting Services-plats på ett plats system på den primära platsen. Använd sedan den primära platsens databas som rapport data källa.

Mer information om globala data och plats data finns i [typer av data](../../plan-design/hierarchy/database-replication.md#types-of-data).

### <a name="network-bandwidth-considerations"></a>Att tänka på när det gäller nätverksbandbredden

Beroende på hur du konfigurerar platsen kommunicerar plats systemen på samma plats med varandra med hjälp av SMB (Server Message Block), HTTP eller HTTPS. Configuration Manager hanterar inte den här kommunikationen. Det kan inträffa när som helst utan nätverkets bandbredds kontroll. Granska din tillgängliga nätverks bandbredd innan du installerar repor ting Services-plats rollen på ett plats system.

Mer information om hur du planerar för plats system finns i [lägga till plats system roller](../deploy/configure/add-site-system-roles.md).

## <a name="plan-for-role-based-administration"></a>Planera för rollbaserad administration

Säkerhet för rapportering är ungefär som andra objekt i Configuration Manager där du kan tilldela säkerhets roller och behörigheter till administrativa användare. Administrativa användare kan endast köra och modifiera rapporter som de har lämplig säkerhetsbehörighet för. För att kunna köra rapporter i Configuration Manager-konsolen behöver användarna **Läs** behörighet för **plats** behörigheten och behörigheterna som har kon figurer ATS för vissa objekt.

Till skillnad från andra objekt i Configuration Manager konfigureras även de säkerhets behörigheter som du ställer in för administrativa användare i Configuration Manager-konsolen i repor ting Services. När du konfigurerar säkerhets rättigheter i Configuration Manager-konsolen ansluter repor ting Services-platsen till repor ting Services och ställer in lämpliga behörigheter för rapporter.

Säkerhets rollen för **program uppdaterings hanteraren** har till exempel behörigheterna **Kör rapport** och **Ändra rapport** . Användare med rollen **program uppdaterings hanterare** kan bara köra och ändra rapporter för program uppdateringar. Configuration Manager-konsolen visar inte rapporter för andra objekt till den här rollen. Undantaget till det här problemet är att vissa rapporter inte är associerade med vissa Configuration Manager skydds bara objekt. För de här rapporterna måste administrativa användare ha **Läs** -behörighet för **Plats** -behörigheten för att köra rapporterna och **Ändra** -behörighet för **Plats** -behörigheten för att ändra rapporterna.  

> [!IMPORTANT]
> Upprätta ett dubbelriktat förtroende mellan de två domänerna för användare från en annan domän än den som kontot för repor ting Services-platsen ska köra rapporter på.

Rapporter är helt aktiverade för rollbaserad administration. Configuration Manager filtrerar data för alla inkluderade rapporter baserat på behörigheterna för den användare som kör rapporten. Användare med vissa roller kan bara visa information som definierats för deras roller.

Mer information om säkerhets behörighet för rapportering finns i [Konfigurera rapportering](configuring-reporting.md).

Mer information om rollbaserad administration i Configuration Manager finns i [Konfigurera rollbaserad administration](../deploy/configure/configure-role-based-administration.md).

## <a name="reporting-recommendations"></a>Rapporterings rekommendationer

Överväg följande rekommendationer och tips för rapportering i Configuration Manager:

- För bästa prestanda bör du installera repor ting Services-platsen på ett fjärrplatssystem. Även om du kan installera det på plats servern fungerar repor ting Services-platsen bäst när du installerar den på ett fjärrplatssystem. När den här rollen hanterar bakgrunds bearbetning kan det konkurrera om system resurser med andra roller. Det finns många variabler att överväga med plats-och roll prestanda, men i allmänhet förbättrar den här konfigurationen rapportering och övergripande plats prestanda.

- Optimera SQL Server Reporting Services-frågor. Normalt beror eventuella rapporterings förseningar på grund av den tid det tar att köra frågor och hämta resultaten. Microsoft SQL Server verktyg som Query Analyzer och profiler kan hjälpa dig att optimera frågor.

- Schemalägg rapport prenumerations bearbetningen så att den körs utanför standard kontors tid. När det är möjligt kan bearbetning av prenumerationer under andra tider minimera CPU-bearbetningen på Configuration Manager plats databas servern. Detta förbättrar även tillgängligheten för oförutsedda rapporbegäranden.

- Plats uppdateringar Behåll inbyggda rapporter. Om du ändrar en standard rapport och platsen uppdateras, byter den namn på rapporten med ett under streck (`_`). Det här beteendet ser till att plats uppdateringen inte skriver över den ändrade rapporten i standard rapporten.

## <a name="security-and-privacy"></a>Säkerhet och sekretess

Configuration Manager rapporter visar information som samlas in under standard åtgärder för Configuration Manager hantering. Du kan till exempel Visa en rapport med information som Configuration Manager samlats in från identifiering eller inventering. Rapporter kan även innehålla aktuell statusinformation för klienthanteringsoperationer, t.ex. distribution av program, och kompatibilitetskontroll.

Mer information om säkerhets rekommendationer och sekretess information för Configuration Manager åtgärder som kan generera data som du kan visa i rapporter finns i [säkerhet och sekretess för Configuration Manager](../../plan-design/security/security-and-privacy.md).  

## <a name="next-steps"></a>Nästa steg

[Krav för rapportering](prerequisites-for-reporting.md)
