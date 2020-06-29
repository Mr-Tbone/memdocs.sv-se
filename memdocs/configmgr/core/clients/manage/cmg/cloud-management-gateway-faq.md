---
title: VANLIGA FRÅGOR OCH SVAR OM CMG
titleSuffix: Configuration Manager
description: Använd den här artikeln för att besvara vanliga frågor om Cloud Management Gateway
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 06/10/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 4c1a128d-22fb-49f1-8e0b-36513a8dc117
ms.openlocfilehash: ecc91168cc90af58c40903ea3d288eeaa82be7a0
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85502246"
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

### <a name="do-the-user-accounts-have-to-be-in-the-same-azure-ad-tenant-as-the-tenant-associated-with-the-subscription-that-hosts-the-cmg-cloud-service"></a><a name="bkmk_tenant"></a>Måste användar kontona finnas i samma Azure AD-klient som klienten som är associerad med den prenumeration som är värd för CMG-moln tjänsten?
<!--SCCMDocs-pr issue #2873-->
Nej, du kan distribuera CMG till alla prenumerationer som kan vara värdar för Azure Cloud Services.

För att klargöra villkoren:

- _Klienten_ är katalogen för användar konton och app-registreringar. En klient organisation kan ha flera prenumerationer.
- En _prenumeration_ delar upp fakturering, resurser och tjänster. Den är kopplad till en enda klient.

Den här frågan är gemensam i följande scenarier:  

- När du har distinkta test-och produktions Active Directory och Azure AD-miljöer, men en enda, centraliserad Azure-värd prenumeration.

- Din användning av Azure har vuxit ekologiskt över olika team

När du använder en Resource Manager-distribution ska du publicera Azure AD-klienten som är associerad med prenumerationen. Med den här anslutningen kan Configuration Manager autentisera till Azure för att skapa, distribuera och hantera CMG.  

Om du använder Azure AD-autentisering för användare och enheter som hanteras via CMG, kan du publicera Azure AD-klienten. Mer information om Azure-tjänster för moln hantering finns i [Konfigurera Azure-tjänster](../../../servers/deploy/configure/azure-services-wizard.md). När du integrerar varje Azure AD-klient kan en enda CMG tillhandahålla Azure AD-autentisering för flera klienter, oavsett värd platsen.

#### <a name="example-1-one-tenant-with-multiple-subscriptions"></a>Exempel 1: en klient med flera prenumerationer

Användar identiteter, enhets registreringar och app-registreringar finns i samma klient organisation. Du kan välja vilken prenumeration som CMG använder. Du kan distribuera flera CMG-tjänster från en plats till separata prenumerationer. Platsen har en 1-till-en-relation med klienten. Du bestämmer vilka prenumerationer som ska användas för olika orsaker, till exempel fakturering eller logisk avgränsning.

#### <a name="example-2-multiple-tenants"></a>Exempel 2: flera klienter

Med andra ord har din miljö fler än en Azure AD. Om du behöver stöd för användar-och enhets identiteter i båda klienterna måste du koppla platsen till varje klient. Den här processen kräver ett administratörs konto från varje klient organisation för att skapa app-registreringar i den klient organisationen. En plats kan sedan vara värd för CMG-tjänster i flera klienter. Du kan skapa en CMG i valfri tillgänglig prenumeration i någon av klient organisationerna. Enheter som är anslutna till eller är hybrid anslutna till Azure AD kan använda en CMG.

Om användar-och enhets identiteter finns i en klient, men CMG-prenumerationen finns i en annan klient, måste du koppla platsen till båda klienterna. Tekniskt sett behövs inte klient appen för den andra klienten som bara har CMG-tjänsten. Klient programmet ger endast autentisering av användare och enheter för klienter som använder CMG-tjänsten.<!-- SCCMDocs#1902 -->

### <a name="how-does-cmg-affect-my-clients-connected-via-vpn"></a>Hur påverkar CMG mina klienter som är anslutna via VPN?

Nätverks växlings klienter som ansluter till din miljö via ett VPN identifieras ofta som intranät. De försöker ansluta till din lokala infrastruktur, till exempel hanterings platser och distributions platser. Vissa kunder föredrar att ha dessa centrala klienter som hanteras av moln tjänster även när de är anslutna via VPN. Från och med version 1902 associerar du CMG med en avgränsnings grupp. Den här åtgärden tvingar dessa klienter att inte använda lokala plats system. Mer information finns i [Konfigurera gränser grupper](setup-cloud-management-gateway.md#configure-boundary-groups).

### <a name="if-i-enable-a-cmg-will-my-clients-only-connect-to-the-cmg-enabled-management-point-when-theyre-connected-to-the-intranet"></a>Om jag aktiverar en CMG ansluter bara mina klienter till den CMG-aktiverade hanterings platsen när de är anslutna till intranätet?

För att skydda känslig trafik som skickas via en CMG konfigurerar du antingen en HTTPS-hanterings plats eller använder förbättrad HTTP.

Om du väljer att distribuera en CMG och använder PKI-certifikat för HTTPS-kommunikation på den CMG-aktiverade hanterings platsen väljer du alternativet för att **tillåta Internet-klienter** på hanterings plats egenskaperna. Den här inställningen säkerställer att interna klienter fortsätter att använda HTTP-hanterings platser i din miljö.

Om du använder utökad HTTP behöver du inte konfigurera den här inställningen. Klienterna fortsätter att använda HTTP när de kommunicerar direkt med den CMG-aktiverade hanterings platsen. Mer information finns i [Enhanced http](../../../plan-design/hierarchy/enhanced-http.md).

### <a name="what-are-the-differences-with-client-authentication-between-azure-ad-and-certificates"></a>Vilka är skillnaderna mellan klientautentisering mellan Azure AD och certifikat?
<!-- MEMDocs#277 -->
Du kan använda Azure AD eller ett [certifikat för klientautentisering](certificates-for-cloud-management-gateway.md#bkmk_clientauth) för enheter för att AUTENTISERA till CMG-tjänsten.

Om du hanterar traditionella Windows-klienter med Active Directory domänanslutna identitet, behöver de PKI-certifikat för att skydda kommunikations kanalen. Dessa klienter kan omfatta Windows 8,1 och Windows 10. Du kan använda alla funktioner som stöds av CMG, men program varu distributionen är begränsad till endast enheter. Installera Configuration Manager-klienten innan enheten växlar till Internet, eller med version 2002 eller senare, Använd token-autentisering.

Du kan också hantera Windows 10-klienter med modern identitet, antingen hybrid eller en ren molnbaserad domän som är ansluten till Azure AD. Klienter använder Azure AD för att autentisera snarare än PKI-certifikat. Att använda Azure AD är enklare att konfigurera, konfigurera och underhålla än mer komplexa PKI-system. Du kan utföra alla samma hanterings aktiviteter och program varu distribution till användaren. Du kan också använda ytterligare metoder för att installera-klienten på en fjär renhet.

Microsoft rekommenderar att du ansluter enheter till Azure AD. Internet-baserade enheter kan använda Azure AD för att autentisera med Configuration Manager. Det aktiverar också både enhets-och användar scenarier oavsett om enheten är ansluten till Internet eller om den är ansluten till det interna nätverket. Mer information finns i [Installera och registrera klienten med hjälp av Azure AD-identitet](../../deploy/deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity).

## <a name="next-steps"></a>Nästa steg

- [Planera för en molnhanteringsgateway](plan-cloud-management-gateway.md)
- [Konfigurera en molnhanteringsgateway](setup-cloud-management-gateway.md)
- [Certifikat för molnhanteringsgateway](certificates-for-cloud-management-gateway.md)
- [Säkerhet och sekretess för molnhanteringsgateway](security-and-privacy-for-cloud-management-gateway.md)
- [Storlek och skalnings nummer för Cloud Management Gateway](../../../plan-design/configs/size-and-scale-numbers.md#bkmk_cmg)
