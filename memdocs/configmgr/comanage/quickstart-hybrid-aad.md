---
title: Använda Azure AD för samhantering
titleSuffix: Configuration Manager
description: Med Azure AD kan du dra nytta av förbättrad produktivitet för dina användare och säkerhet för dina resurser, i både moln-och lokal miljöer
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 2af37410-d04c-4059-801c-9edb8bf72d89
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c757632e96eb9bdaca829d4a19e5e156fcf52577
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694992"
---
# <a name="use-azure-ad-for-co-management"></a>Använda Azure AD för samhantering

I molnet är identitet det nya kontroll planet. Azure Active Directory (Azure AD) gör att du kan länka dina användare, enheter och program både i molnet och i lokala miljöer. Genom att registrera dina enheter i Azure AD kan du förbättra produktiviteten för dina användare och säkerhet för dina resurser. Att ha enheter i Azure AD är grunden för både samhantering och enhets-baserad villkorlig åtkomst.

Mer information om enhets-baserad villkorlig åtkomst finns i [så här gör du: Kräv hanterade enheter för åtkomst till Cloud App med villkorlig åtkomst](/azure/active-directory/conditional-access/require-managed-devices)

I följande videoklipp diskuterar Senior program hanteraren Sandeep Deo och Product Marketing Manager Adam, och demonstrerar Azure AD för samhantering:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Embedding-Co-management-With-Azure-Active-Directory/player]

Azure AD tillhandahåller två alternativ för företagsägda enheter som passar organisationens behov:  

- **Azure AD-ansluten enhet**: Anslut dina Windows 10-enheter till Azure AD utan att behöva ansluta dem till din lokala Active Directory  

  - Stöder Windows 10

  - Konfigurera utan att kräva ytterligare konfiguration för dina lokala miljöer  

  - Genom att aktivera några inställningar i Azure AD kan du göra det möjligt för användarna att ansluta enheter till Azure AD via Windows installations miljö (OOBE)  

  - Mer information finns i [How to: planing The Azure AD Join implementation](/azure/active-directory/devices/azureadjoin-plan)  

- **Hybrid Azure AD-ansluten enhet**: Anslut dina befintliga domänanslutna enheter till Azure AD  

  - Stöder Windows 10, Windows 8,1 och Windows 7

  - Konfigurera med AD FS anspråk eller Azure AD Connect  

  - För Windows 10 sker kopplingen i dator kontexten, så användarna behöver inte vidta några extra steg  

  - Mer information finns i [Planera hybrid Azure Active Directory Join-implementering](/azure/active-directory/devices/hybrid-azuread-join-plan)  

Båda alternativen tillhandahåller liknande funktioner för användare. Det är flexibelt så att du kan välja något utifrån dina behov. Du kan till exempel [komma åt dina lokala resurser](/azure/active-directory/devices/azuread-join-sso) från Azure AD-anslutna datorer, även om de inte är anslutna till Active Directory.

Du kan ansluta enheter till Azure AD i olika miljöer, oavsett din [autentiseringsmetod](/azure/active-directory/hybrid/choose-ad-authn). Till exempel federerad autentisering eller molnbaserad autentisering.

Om du redan har en lokal Active Directory är det enkelt att ställa in något av alternativen.

## <a name="benefits"></a>Fördelar

Att ansluta enheter till Azure AD ger följande fördelar för din organisation:

### <a name="single-sign-on-to-cloud-resources"></a>Enkel inloggning till moln resurser

På enheter som är anslutna till Azure AD får du en integrerad upplevelse för att komma åt moln resurser eller lokala resurser. När du har loggat in på en Windows-dator som är ansluten till Azure AD, får du enkel inloggning till alla program utan ytterligare inloggnings meddelanden.  

### <a name="windows-hello-for-business"></a>Windows Hello för företag

Windows Hello för företag ger starkt lösen ords mindre autentisering till Windows 10. Genom att ansluta dina enheter till Azure AD kan du aktivera Windows Hello för företag i användar basen för både moln resurser och lokala resurser. Windows Hello för företag eliminerar problemet med att komma ihåg komplexa lösen ord eller oavsiktligt exponera dem. Dess inloggnings process är både enkel och säker.

Mer information finns i [Windows Hello för företag](/windows/security/identity-protection/hello-for-business/hello-identity-verification).  

### <a name="device-based-conditional-access"></a>Enhetsbaserad villkorlig åtkomst

Aktivera villkorlig åtkomst baserat på enhetens tillstånd för att bättre skydda organisationens data. Enhets-baserad villkorlig åtkomst kräver en hanterad enhet. Enheten måste vara en kompatibel enhet eller en hybrid Azure AD-ansluten enhet. För Azure AD-anslutna enheter behöver du Intune för att markera enheten som kompatibel. Men för Hybrid Azure AD-anslutna enheter används själva enhets statusen för att utvärdera villkorlig åtkomst. Med samhantering får du ytterligare möjlighet att utvärdera efterlevnad genom Intune för Hybrid Azure AD-anslutna enheter. Den här funktionen kontrollerar att enhetens konfiguration är intakt.

Mer information om enhets beroende åtkomst finns i [så här gör du: Kräv hanterade enheter för åtkomst till Cloud App med villkorlig åtkomst](/azure/active-directory/conditional-access/require-managed-devices).  

### <a name="automatic-device-licensing"></a>Automatisk enhets licensiering

Alla Windows 10-enheter som är anslutna till Azure AD går igenom licens kontrollerna. Med de här kontrollerna kan du automatiskt uppgradera dem från Pro till företag via Microsoft-molnet. När du tar bort den relevanta prenumerationen från användaren degraderar enheten automatiskt sin licens. Den här funktionen ger en enda kontroll för att hantera Windows-licenser, utan några komplicerade processer eller lokala system.

### <a name="self-service-functionality"></a>Självbetjänings funktioner

I självbetjänings funktionerna ingår självbetjäning för återställning av lösen ord och BitLocker-återställningsnyckel. Azure AD tillhandahåller också direkta alternativ för att återställa lösen ordet eller komma åt BitLocker-återställningsnyckel. Du kan använda Azure AD för att återställa lösen ordet direkt från Windows Lås-skärmen i stället för från en webbläsare. Dessa funktioner minskar friktionen för användare och hjälper till att minska kostnaderna för supportavdelningen för din organisation.  

Mer information finns i [Självstudier: gör det möjligt för användare att låsa upp kontot eller återställa lösen ord med hjälp av Azure Active Directory självbetjäning för återställning av lösen ord](/azure/active-directory/authentication/tutorial-enable-sspr).

### <a name="enterprise-state-roaming"></a>Roaming för företags tillstånd

Alla enheter som är anslutna till Azure AD kan synkronisera sina inställningar till molnet. Alla enheter som en användare loggar in på synkroniserar alla inställningar för en mer produktiv upplevelse.  

## <a name="value-proposition"></a>Värde förslag

Genom att ansluta dina enheter till Azure AD via någon av metoderna påskyndas din digitala omvandling. Den aktiverar fler funktioner som tillhandahålls av Microsoft 365. Du har bättre erfarenhet och du får större säkerhet för dina data.

Azure AD tillhandahåller flera alternativ för att under lätta din arbets belastning, till exempel:

- Hantera alla enhets identiteter i organisationen från en enda plats  

- Sänk kostnaderna för supportavdelningen genom att aktivera lösen ords återställning via självbetjäning. Sedan kan användarna återställa ditt lösen ord från Lås skärmen på Windows 10 på enheten när som helst.  

## <a name="configure"></a>Konfigurera

Om du redan har en lokal Active Directory miljö och du vill ansluta dina domänanslutna enheter till Azure AD konfigurerar du hybrid Azure AD-anslutna enheter. Mer information finns [i så här planerar du hybrid Azure Active Directory Join-implementering](/azure/active-directory/devices/hybrid-azuread-join-plan).

Configuration Manager har en klient inställning för att [automatiskt registrera nya Windows 10-domänanslutna enheter med Azure AD](../core/clients/deploy/about-client-settings.md#automatically-register-new-windows-10-domain-joined-devices-with-azure-active-directory). Mer information om hur du konfigurerar klient inställningar finns i [Konfigurera klient inställningar](../core/clients/deploy/configure-client-settings.md).

Om du vill konfigurera Azure AD – Anslut till dina enheter utan att behöva ansluta dem till den lokala domänen bör du gå igenom överväganden för Azure AD-Join i din miljö. När du har bestämt dig för att använda Azure AD Join har du flera alternativ för att distribuera den utifrån organisationens behov. Mer information finns i följande artiklar:

- [Gör så här: planera din Azure AD Join-implementering](/azure/active-directory/devices/azureadjoin-plan)  
- [Förstå dina etablerings alternativ](/azure/active-directory/devices/azureadjoin-plan#understand-your-provisioning-options)