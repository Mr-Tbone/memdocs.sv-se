---
title: Installera klienten med Azure AD
titleSuffix: Configuration Manager
description: Installera och tilldela Configuration Manager-klienten på Windows 10-enheter med Azure Active Directory för autentisering
ms.date: 06/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a44006eb-8650-49f6-94e1-18fa0ca959ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1b447e5c8d34a4b8758fa0fd6109113b0675a635
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347023"
---
# <a name="install-and-assign-configuration-manager-windows-10-clients-using-azure-ad-for-authentication"></a>Installera och tilldela Configuration Manager Windows 10-klienter med Azure AD för autentisering

Om du vill installera Configuration Manager-klienten på Windows 10-enheter med Azure AD-autentisering, integrera Configuration Manager med Azure Active Directory (Azure AD). Klienter kan finnas i intranätet som kommunicerar direkt med en HTTPS-aktiverad hanterings plats eller en hanterings plats på en plats som är aktive rad för utökad HTTP. De kan också vara internetbaserada som kommunicerar via CMG eller med en Internetbaserad hanterings plats. Den här processen använder Azure AD för att autentisera klienter till Configuration Manager-platsen. Azure AD ersätter behovet av att konfigurera och använda certifikat för klientautentisering.

Det kan vara enklare för vissa kunder att konfigurera Azure AD än att konfigurera en infrastruktur för offentliga nycklar för certifikatbaserad autentisering. Det finns funktioner som kräver att du registrerar platsen på Azure AD, men kräver inte nödvändigt vis att klienterna är anslutna till Azure AD.<!-- SCCMDocs issue 1259 --> Mer information finns i följande artiklar:

- [Planera för Azure Active Directory](../../plan-design/security/plan-for-security.md#bkmk_planazuread)
- [Använda Azure AD för samhantering](../../../comanage/quickstart-hybrid-aad.md)

## <a name="before-you-begin"></a>Innan du börjar

- En Azure AD-klient är en förutsättning  

- Enhets krav:  

  - Windows 10  

  - Ansluten till Azure AD, antingen rent molnbaserad domänanslutna eller hybrid Azure AD-ansluten  

- Användar krav:  

  - Den inloggade användaren måste vara en Azure AD-identitet.

  - Om användaren är en federerad eller synkroniserad identitet konfigurerar du både Configuration Manager [Active Directory identifiering av användare](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser) och [identifiering av Azure AD-användare](../../servers/deploy/configure/about-discovery-methods.md#azureaddisc). Mer information om Hybrid identiteter finns i [definiera en strategi för Hybrid identitets införande](https://docs.microsoft.com/azure/active-directory/hybrid/plan-hybrid-identity-design-considerations-identity-adoption-strategy).<!--497750-->

- Förutom de [befintliga kraven](../../plan-design/configs/site-and-site-system-prerequisites.md#bkmk_2012MPpreq) för hanterings platsens plats system roll aktiverar du även **ASP.NET 4,5** på den här servern. Inkludera andra alternativ som väljs automatiskt när du aktiverar ASP.NET 4,5.  

- Ta reda på om din hanterings plats behöver HTTPS. Mer information finns i [Aktivera hanterings plats för https](../manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_mphttps).  

- Du kan också konfigurera en [Cloud Management Gateway](../manage/cmg/plan-cloud-management-gateway.md) (CMG) för att distribuera Internetbaserade klienter. För lokala klienter som autentiseras med Azure AD behöver du inte någon CMG.  

> [!TIP]
> Från och med version 2002,<!--5686290--> Configuration Manager utökar sitt stöd för Internetbaserade enheter som inte ofta ansluter till det interna nätverket, kan inte ansluta Azure Active Directory (Azure AD) och har inte någon metod för att installera ett PKI-utfärdat certifikat. Mer information finns i [tokenbaserad autentisering för CMG](deploy-clients-cmg-token.md).

## <a name="configure-azure-services-for-cloud-management"></a>Konfigurera Azure-tjänster för moln hantering

Anslut Configuration Manager-platsen till Azure AD som det första steget. Mer information om den här processen finns i [Konfigurera Azure-tjänster](../../servers/deploy/configure/azure-services-wizard.md). Skapa en anslutning till **moln hanterings** tjänsten.

Aktivera [identifiering av Azure AD-användare](../../servers/deploy/configure/configure-discovery-methods.md#azureaadisc) som en del av onboarding i **Cloud Management**.

När du har slutfört de här åtgärderna är din Configuration Managers webbplats ansluten till Azure AD.

## <a name="configure-client-settings"></a>Konfigurera klientinställningar

Dessa klient inställningar hjälper till att konfigurera Windows 10-enheter så att de blir hybrid anslutna. De gör det också möjligt för Internetbaserade klienter att använda CMG och moln distributions platsen.

1. Konfigurera följande klient inställningar i **Cloud Servicess** gruppen. Mer information finns i [så här konfigurerar du klient inställningar](configure-client-settings.md).

    - **Tillåt åtkomst till moln distributions platsen**: Aktivera den här inställningen för att hjälpa Internetbaserade enheter att hämta det innehåll som krävs för att installera Configuration Manager-klienten. Om innehållet inte är tillgängligt på moln distributions platsen kan enheterna hämta innehållet från CMG. Start programmet för klient installation försöker med moln distributions platsen i fyra timmar innan den återgår till CMG.<!--495533-->  

    - **Registrera automatiskt nya Windows 10-domänanslutna enheter med Azure Active Directory**: ange **Ja** eller **Nej**. Standardinställningen är **Ja**. Detta är också standardvärdet i Windows 10, version 1709.

        > [!TIP]
        > Hybrid-anslutna enheter är anslutna till en lokal Active Directory-domän och är registrerad i Azure AD. Mer information finns i avsnittet om [hybrid Azure AD-anslutna enheter](https://docs.microsoft.com/azure/active-directory/devices/concept-azure-ad-join-hybrid).<!-- MEMDocs#325 -->

    - **Gör det möjligt för klienter att använda en Cloud Management Gateway**: Ange som **Ja** (standard) eller **Nej**.  

2. Distribuera klient inställningarna till den obligatoriska samlingen av enheter. Distribuera inte inställningarna till användar samlingar.

För att bekräfta att enheten är hybrid-ansluten, kör du `dsregcmd.exe /status` i en kommando tolk. Om enheten är Azure AD-ansluten eller hybrid-ansluten visas **Ja**i fältet **AzureAdjoined** i resultatet. Mer information finns i [dsregcmd-kommando enhets tillstånd](https://docs.microsoft.com/azure/active-directory/devices/troubleshoot-device-dsregcmd).

## <a name="install-and-register-the-client-using-azure-ad-identity"></a>Installera och registrera klienten med hjälp av Azure AD-identitet

Om du vill installera klienten manuellt med Azure AD-identitet läser du först igenom den allmänna processen för [hur du installerar klienter manuellt](deploy-clients-to-windows-computers.md#BKMK_Manual).

> [!Note]  
> Enheten behöver åtkomst till Internet för att kontakta Azure AD, men behöver inte vara Internet-baserad.

I följande exempel visas den allmänna strukturen för kommando raden:`ccmsetup.exe /mp:<source management point> CCMHOSTNAME=<internet-based management point> SMSSiteCode=<site code> SMSMP=<initial management point> AADTENANTID=<Azure AD tenant identifier> AADCLIENTAPPID=<Azure AD client app identifier> AADRESOURCEURI=<Azure AD server app identifier>`

Mer information finns i [Egenskaper för klient installation](about-client-installation-properties.md).

**/MP** -parametern och egenskapen **CCMHOSTNAME** anger något av följande, beroende på scenariot:

- Lokal hanterings plats. Ange endast parametern **/MP** . Egenskapen **CCMHOSTNAME** är inte obligatorisk.
- Gateway för molnhantering
- Internetbaserad hanterings plats

Egenskapen **SMSMP** anger antingen den lokala eller Internetbaserade hanterings platsen.

I det här exemplet används en gateway för moln hantering. Den ersätter exempel värden:`ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC SMSMP=https://mp1.contoso.com AADTENANTID=daf4a1c2-3a0c-401b-966f-0b855d3abd1a AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver`

Platsen publicerar ytterligare Azure AD-information till Cloud Management Gateway (CMG). En Azure AD-ansluten klient hämtar den här informationen från CMG under CCMSetup-processen och använder samma klient organisation som den är ansluten till. Med det här beteendet blir det enklare att installera klienten i en miljö med fler än en Azure AD-klient. De enda två obligatoriska CCMSetup-egenskaperna är **CCMHOSTNAME** och **SMSSiteCode**.<!--3607731-->

Information om hur du automatiserar klient installationen med hjälp av Azure AD-identitet via Microsoft Intune finns i [så här förbereder du Internetbaserade enheter för samhantering](../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client).

## <a name="next-steps"></a>Nästa steg

När du är klar kan du fortsätta att [övervaka och hantera klienter](../manage/monitor-clients.md).
