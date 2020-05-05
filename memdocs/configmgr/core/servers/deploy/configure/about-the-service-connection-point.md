---
title: Tjänstanslutningspunkt
titleSuffix: Configuration Manager
description: Lär dig mer om den här Configuration Manager plats system rollen och förstå och planera för dess användnings område.
ms.date: 01/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bc2282d5-0571-465b-9528-a555855eaacd
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d167ea14537d88c31ca3930614fc24d8ebc92a02
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721187"
---
# <a name="about-the-service-connection-point-in-configuration-manager"></a>Om tjänst anslutnings punkten i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Tjänst anslutnings punkten är en plats system roll som tillhandahåller flera viktiga funktioner för hierarkin. Innan du konfigurerar tjänst anslutnings punkten bör du förstå och planera för dess användnings område. Att planera användningen kan påverka hur du konfigurerar den här plats system rollen:

- Hämta uppdateringar som gäller för din Configuration Manager-infrastruktur. Endast relevanta uppdateringar för din infrastruktur görs tillgängliga baserat på användnings data som du överför.

- Ladda upp användnings data från Configuration Manager-infrastrukturen. Du kan kontrol lera nivån eller mängden information som du överför. Mer information finns i [nivåer och inställningar för användnings data](../install/setup-reference.md#bkmk_usage).

- Distribuera en [Gateway för moln hantering](../../../clients/manage/cmg/plan-cloud-management-gateway.md) i Azure

- Synkronisera appar från [Microsoft Store för företag och utbildning](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)

- Identifiera användare och grupper i [Azure Active Directory (Azure AD)](about-discovery-methods.md#azureaddisc)

- Använd [Skriv bords analys](../../../../desktop-analytics/overview.md) för att få insikter om Windows 10-uppdatering och app-beredskap

Varje hierarki har stöd för en enda instans av den här rollen. Den kan bara installeras på platsen på den översta nivån i hierarkin, som är en central administrations plats (ca) eller en fristående primär plats. Om du expanderar en fristående primär plats till en större hierarki måste du avinstallera den här rollen från den primära platsen och sedan installera den på certifikat utfärdarna.

## <a name="modes-of-operation"></a><a name="bkmk_modes"></a>Drifts lägen

Tjänstanslutningspunkten har stöd för två olika driftlägen:

- **Online**: tjänst anslutnings punkten kontrol leras automatiskt var 24: e timme för uppdateringar. Den hämtar nya uppdateringar som är tillgängliga för den aktuella infrastrukturen och produkt versionen och gör dem tillgängliga i Configuration Manager-konsolen.

- **Offline**: tjänst anslutnings punkten ansluter inte till Microsofts moln tjänst. Om du vill importera tillgängliga uppdateringar manuellt använder du [tjänst anslutnings verktyget](../../manage/use-the-service-connection-tool.md).

### <a name="change-mode"></a>Ändra läge

Om du ändrar mellan online-eller offline-läge när du har installerat tjänst anslutnings punkten startar du om **SMS_DMP_DOWNLOADER** tråden för tjänsten SMS_EXECUTIVE. Om du startar om den här tråden börjar ändringen gälla. Om du vill starta om tråden använder du Configuration Manager Service Manager.

> [!TIP]
> Du kan också starta om tjänsten SMS_Executive Configuration Manager, som startar om de flesta plats komponenter. Du kan också vänta på en schemalagd aktivitet som en plats säkerhets kopiering, vilket stoppar och startar om SMS_Executive tjänsten åt dig.

För att använda Configuration Manager Service Manager för att starta om SMS_DMP_DOWNLOADER tråden:

1. I Configuration Manager-konsolen går du till arbets ytan **övervakning** , expanderar **system status**och väljer noden **komponent status** . Välj **Start**i menyfliksområdet och välj sedan **Configuration Manager Service Manager**.

1. I navigerings fönstret i Service Manager expanderar du platsen, expanderar **komponenter**och väljer sedan den komponent som du vill starta om: **SMS_DMP_DOWNLOADER**.

1. Gå till **komponent** -menyn och välj **fråga**.

1. Bekräfta komponentens aktuella status. Gå sedan till **komponent** -menyn och välj **stoppa**.  

1. **Fråga** komponenten igen för att bekräfta att den har stoppats. Välj sedan åtgärden **Starta** komponent för att starta om den.

## <a name="remote-site-system-requirements"></a>System krav för fjärrplats

När du installerar tjänst anslutnings punkten på en plats system server som är fjärran sluten till plats servern konfigurerar du följande krav:

- Plats serverns dator konto måste vara en lokal administratör på den dator som är värd för en fjärr anslutnings punkt för tjänsten.

- Konfigurera plats system servern som är värd för rollen med ett [konto för installation av plats system](../../../plan-design/hierarchy/accounts.md#site-system-installation-account). Distributions hanteraren på plats servern använder kontot för installation av plats system för att överföra uppdateringar från tjänst anslutnings punkten.

## <a name="internet-access-requirements"></a><a name="bkmk_urls"></a>Krav för Internet åtkomst

Om din organisation begränsar nätverkskommunikation med Internet med en brand vägg eller proxyserver, måste du tillåta att tjänst anslutnings punkten får åtkomst till Internet-slutpunkter.

Mer information finns i [krav för Internet åtkomst](../../../plan-design/network/internet-endpoints.md#bkmk_scp).

## <a name="install"></a>Installera

När du kör **installations programmet** för att installera platsen på den översta nivån i en hierarki kan du installera tjänst anslutnings punkten.

När installationen har körts, eller om du installerar om rollen, använder du guiden **Lägg till plats system roller** eller guiden **skapa plats system Server** . (Installera bara tjänst anslutnings punkten på platsen på den översta nivån i hierarkin.) Mer information finns i [Installera plats system roller](install-site-system-roles.md).

## <a name="move-the-role"></a><a name="bkmk_move"></a>Flytta rollen

<!-- SCCMDocs#922 -->
Det finns flera scenarier där du kan behöva flytta tjänst anslutnings punkten till en annan server:

- [Återställning](../../manage/recover-sites.md)
- [Platsserver hög tillgänglighet](site-server-high-availability.md)
- [Plats expansion](../install/use-the-setup-wizard-to-install-sites.md#bkmk_expand)

När du har flyttat tjänst anslutnings punkten kontrollerar du alla plats funktioner. Du kan till exempel behöva förnya den hemliga nyckeln för anslutningar till Azure Active Directory (Azure AD)-klient organisationer. Mer information finns i [förnya hemlig nyckel](azure-services-wizard.md#bkmk_renew).

## <a name="log-files"></a>Loggfiler

Om du vill visa information om överföringar till Microsoft kan du läsa **Dmpuploader. log** på den server som kör tjänst anslutnings punkten. Hämtnings förlopp för uppdateringar visas i **dmpdownloader. log**. En fullständig lista över loggar som är relaterade till tjänst anslutnings punkten finns i [loggfiler-tjänst anslutnings punkt](../../../plan-design/hierarchy/log-files.md#BKMK_WITLog).

## <a name="next-steps"></a>Nästa steg

Använd följande flödes diagram för att förstå posterna i process flödet och nyckel loggen. Den här processen omfattar uppdaterings nedladdning och replikering av uppdateringar till andra platser.

- [Flödesschema – hämta uppdateringar](../../manage/download-updates-flowchart.md)

- [Flödesschema – Uppdatera replikering](../../manage/update-replication-flowchart.md)
