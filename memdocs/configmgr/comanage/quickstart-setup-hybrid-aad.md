---
title: Konfigurera Hybrid Azure AD
titleSuffix: Configuration Manager
description: Om din miljö för närvarande har domänanslutna Windows 10-enheter konfigurerar du hybrid Azure AD innan du aktiverar samhantering
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 27dd26d1-e99c-4431-b2f8-60406394b6db
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 405303b3988e8c853ba30e8fb6d620d782b0474e
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694907"
---
# <a name="set-up-hybrid-azure-ad-for-co-management"></a>Konfigurera hybrid Azure AD for Co-Management

Om du har Windows 10-enheter som är anslutna till en lokal Active Directory, innan du aktiverar samhantering i Configuration Manager, ansluter du först enheterna till Azure Active Directory (Azure AD). Den här processen kallas för Hybrid Azure AD-anslutning. 

I följande video diskuterar Senior program hanteraren Sandeep Deo och Product Marketing Manager Adam-avdelningen och demonstrationen att konfigurera enheter i Azure AD:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Configuring-Devices-in-Azure-Active-Directory/player]

Hybrid Azure AD-Join-processen registrerar automatiskt lokala domänanslutna enheter med Azure AD. Mer information om den här processen finns i följande artiklar:
- [Introduktion till enhetshantering i Azure Active Directory](/azure/active-directory/device-management-introduction) 
- [Planera din hybrid Azure AD-anslutning](/azure/active-directory/devices/hybrid-azuread-join-plan)

Hybrid Azure AD Join är en av de viktigaste grunderna för samhantering. Den här processen kan vara utmanande för vissa kunder, till exempel:
- Din organisation använder en identitets lösning från tredje part 
- De komplexa inställningarna för att konfigurera Active Directory Federation Services (AD FS) (ADFS)

Det kan ta lite vägledning att lösa dessa utmaningar. Den här artikeln hjälper till att minimera eventuella fördröjningar.


## <a name="how-to-do-it"></a>Gör så här

Enheter liknar användarna när de skapar en identitet som du vill skydda. För att skydda en enhets identitet när som helst och var som helst måste du ta med identiteten för enheten i Azure AD.

Beroende på vilken typ av domän du använder finns det två huvudsakliga sätt att göra det. Konfigurera hybrid Azure AD-anslutning för någon av följande domän typer:  
- [Federerade domäner](/azure/active-directory/devices/hybrid-azuread-join-federated-domains)  
- [Hanterade domäner](/azure/active-directory/devices/hybrid-azuread-join-managed-domains)  

De två föregående metoderna ger bästa möjliga upplevelse. Mer detaljerad information, inklusive den helt manuella processen, finns i följande artiklar:
- [Konfigurera hybrid Azure AD-anslutna enheter manuellt](/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup)  
- [AD FS-direktautentisering för Hybrid Azure AD](/windows-server/identity/ad-fs/ad-fs-overview), som innehåller identifiering av Azure AD  

Fel söknings anvisningar finns i [fel söknings guiden för Windows 10 hybrid Azure AD Join](/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current).



## <a name="case-study"></a>Fallstudie

Ett stort europeiskt program företag med över 100 000 användare i sitt nätverk tog en detaljerad och stegvis metod för att aktivera hybrid Azure AD-anslutning.

I planerings fasen, eftersom hybrid Azure AD Join är ett nyckel element som stöder samhantering, Configuration Manager-administratörer som arbetar med identitets teamet. Det här program företaget har många ADFS-regler och en del av dem var komplexa. För att åtgärda denna utmaning granskade identitets teamet befintliga ADFS-regler innan de aktiverade hybrid Azure AD Join. IT-teamet väljer också att uppgradera Azure AD Connect till den senaste versionen. Azure AD Connect nu innehåller ett automatiserat process flöde för att aktivera hybrid Azure AD-anslutning.

Efter en lyckad distribution och testning i sin för produktions miljö har kunden aktiverat hybrid Azure AD Join för hela produktions fastigheten. Inom en vecka hade de alla samhanterade Windows 10-enheter.



## <a name="contact-fasttrack"></a>Kontakta FastTrack

Om du behöver hjälp med att konfigurera Azure AD vid något tillfälle i processen går du till [Microsoft FastTrack](https://Microsoft.com/FastTrack/), loggar in och ber om hjälp. 

Mer information finns i [få hjälp från FastTrack](quickstart-fasttrack.md).