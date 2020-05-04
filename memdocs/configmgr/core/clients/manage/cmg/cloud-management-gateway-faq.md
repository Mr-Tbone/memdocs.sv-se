---
title: VANLIGA FRÅGOR OCH SVAR OM CMG
titleSuffix: Configuration Manager
description: Använd den här artikeln för att besvara vanliga frågor om Cloud Management Gateway
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/05/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 4c1a128d-22fb-49f1-8e0b-36513a8dc117
ms.openlocfilehash: 2bd3824df18ecdf426720a99db8720ef4b678733
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714075"
---
# <a name="frequently-asked-questions-about-the-cloud-management-gateway"></a>Vanliga frågor och svar om Cloud Management Gateway

*Gäller för: Configuration Manager (aktuell gren)*

I den här artikeln får du svar på vanliga frågor om Cloud Management Gateway. Mer information finns i [Planera för Cloud Management Gateway](plan-cloud-management-gateway.md).


## <a name="frequently-asked-questions"></a>Vanliga frågor och svar

### <a name="what-certificates-do-i-need"></a>Vilka certifikat behöver jag?

Mer detaljerad information finns i [certifikat för Cloud Management Gateway](certificates-for-cloud-management-gateway.md).


### <a name="do-i-need-azure-expressroute"></a>Behöver jag Azure ExpressRoute?

Nej. Med [Azure ExpressRoute](/azure/expressroute/expressroute-introduction) kan du utöka ditt lokala nätverk till Microsoft-molnet. ExpressRoute eller andra sådana virtuella nätverks anslutningar krävs inte för den Configuration Manager Cloud Management Gateway. Designen av Cloud Management Gateway gör det möjligt för Internetbaserade klienter att kommunicera via Azure-tjänsten till lokala plats system utan ytterligare nätverks konfiguration. Mer information finns i [Planera för Cloud Management Gateway](plan-cloud-management-gateway.md)

<!-- SCCMDocs#1659 -->

### <a name="do-i-need-to-maintain-the-azure-virtual-machines"></a>Behöver jag underhålla Azure Virtual Machines?

Inget underhåll krävs. Designen av Cloud Management Gateway använder Azure Platform as a Service (PaaS). Med den prenumeration du anger skapar Configuration Manager de virtuella datorer, lagring och nätverk som behövs. Azure säkrar och uppdaterar den virtuella datorn. De här virtuella datorerna är inte en del av din lokala miljö, som är fallet med IaaS (Infrastructure as a Service). Cloud Management Gateway är en PaaS som utökar din Configuration Manager miljö i molnet. Mer information finns i [skydda PaaS-distributioner](/azure/security/security-paas-deployments).


### <a name="how-can-i-ensure-service-continuity-during-service-updates"></a>Hur kan jag garantera tjänste kontinuitet under tjänst uppdateringar?

Genom att skala CMG till att omfatta två eller fler instanser får du automatiskt nytta av uppdaterings domäner i Azure. Se [Uppdatera en moln tjänst](/azure/cloud-services/cloud-services-update-azure-service).


### <a name="im-already-using-ibcm-if-i-add-cmg-how-do-clients-behave"></a>Jag använder redan IBCM. Hur fungerar klienterna om jag lägger till CMG?

Om du redan har distribuerat [Internetbaserad klient hantering](../plan-internet-based-client-management.md) (IBCM) kan du även distribuera Cloud Management Gateway. Klienterna tar emot principer för båda tjänsterna. När de är på Internet väljer de slumpmässigt och använder en av dessa Internetbaserade tjänster.


### <a name="do-the-user-accounts-have-to-be-in-the-same-azure-ad-tenant-as-the-tenant-associated-with-the-subscription-that-hosts-the-cmg-cloud-service"></a>Måste användar kontona finnas i samma Azure AD-klient som klienten som är associerad med den prenumeration som är värd för CMG-moln tjänsten?
<!--SCCMDocs-pr issue #2873-->
Om din miljö har fler än en prenumeration kan du distribuera CMG till alla prenumerationer som kan vara värdar för Azure Cloud Services. 

Den här frågan är gemensam i följande scenarier:  

- När du har distinkta test-och produktions Active Directory och Azure AD-miljöer, men en enda, centraliserad Azure-värd prenumeration  

- Din användning av Azure har vuxit ekologiskt över olika team  

När du använder en Resource Manager-distribution ska du publicera Azure AD-klienten som är associerad med prenumerationen. Med den här anslutningen kan Configuration Manager autentisera till Azure för att skapa, distribuera och hantera CMG.  

Om du använder Azure AD-autentisering för användare och enheter som hanteras via CMG, kan du publicera Azure AD-klienten. Mer information om Azure-tjänster för moln hantering finns i [Konfigurera Azure-tjänster](../../../servers/deploy/configure/azure-services-wizard.md). När du integrerar varje Azure AD-klient kan en enda CMG tillhandahålla Azure AD-autentisering för flera klienter, oavsett värd platsen.

### <a name="how-does-cmg-affect-my-clients-connected-via-vpn"></a>Hur påverkar CMG mina klienter som är anslutna via VPN?

Nätverks växlings klienter som ansluter till din miljö via ett VPN identifieras ofta som intranät. De försöker ansluta till din lokala infrastruktur, till exempel hanterings platser och distributions platser. Vissa kunder föredrar att ha dessa centrala klienter som hanteras av moln tjänster även när de är anslutna via VPN. Från och med version 1902 associerar du CMG med en avgränsnings grupp. Den här åtgärden tvingar dessa klienter att inte använda lokala plats system. Mer information finns i [Konfigurera gränser grupper](setup-cloud-management-gateway.md#configure-boundary-groups).

### <a name="if-i-enable-a-cmg-will-my-clients-only-connect-to-the-cmg-enabled-management-point-when-theyre-connected-to-the-intranet"></a>Om jag aktiverar en CMG ansluter bara mina klienter till den CMG-aktiverade hanterings platsen när de är anslutna till intranätet?

För att skydda känslig trafik som skickas via en CMG konfigurerar du antingen en HTTPS-hanterings plats eller använder förbättrad HTTP.

Om du väljer att distribuera en CMG och använder PKI-certifikat för HTTPS-kommunikation på den CMG-aktiverade hanterings platsen väljer du alternativet för att **tillåta Internet-klienter** på hanterings plats egenskaperna. Den här inställningen säkerställer att interna klienter fortsätter att använda HTTP-hanterings platser i din miljö.

Om du använder utökad HTTP behöver du inte konfigurera den här inställningen. Klienterna fortsätter att använda HTTP när de kommunicerar direkt med den CMG-aktiverade hanterings platsen. Mer information finns i [Enhanced http](../../../plan-design/hierarchy/enhanced-http.md).

## <a name="next-steps"></a>Nästa steg

- [Planera för en molnhanteringsgateway](plan-cloud-management-gateway.md)
- [Konfigurera en molnhanteringsgateway](setup-cloud-management-gateway.md)
- [Certifikat för molnhanteringsgateway](certificates-for-cloud-management-gateway.md)
- [Säkerhet och sekretess för molnhanteringsgateway](security-and-privacy-for-cloud-management-gateway.md)
- [Storlek och skalnings nummer för Cloud Management Gateway](../../../plan-design/configs/size-and-scale-numbers.md#bkmk_cmg)
