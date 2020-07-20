---
title: Intune som drivs av 21Vianet i Kina
titleSuffix: ''
description: Intune som drivs av 21Vianet i Kina.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/07/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: ''
ms.reviewer: amsaeedi
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1c4e567c7812f53a7497f368ded47d72640443f6
ms.sourcegitcommit: 678104677ad36b789630befdc5e0f1efc572c14b
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "86137386"
---
# <a name="intune-operated-by-21vianet-in-china"></a>Intune som drivs av 21Vianet i Kina  

Intune som drivs av 21Vianet har utformats för att uppfylla behovet av säkra, pålitliga och skalbara molntjänster i Kina. Intune som en tjänst skapas på Microsoft Azure. Microsoft Azure som drivs av 21Vianet är en fysiskt separerad instans av molntjänster som finns i Kina. Den drivs och hanteras helt fristående av 21Vianet. Den här tjänsten drivs av teknik som Microsoft har licensierat till 21Vianet.

Microsoft driver inte själva tjänsten. 21Vianet driver, tillhandahåller och hanterar leveransen av tjänsten. 21Vianet är en Internet-datacentertjänstprovider i Kina. Den tillhandahåller värdbaserade, hanterade nätverkstjänster och infrastrukturtjänster för molnbaserad databehandling. Genom att licensiera Microsofts tekniker använder 21Vianet lokala datacenter, vilket ger dig möjlighet att använda Intune-tjänsten samtidigt som dina data finns i Kina. 21Vianet tillhandahåller även prenumerations-, fakturerings- och supporttjänster.

[!INCLUDE [GDPR-related guidance](../includes/gdpr-dsr-and-stp-note.md)]

## <a name="feature-differences-in-intune-operated-by-21vianet"></a>Funktionsskillnader i Intune som drivs av 21Vianet

Att Kina-tjänsterna drivs av en partner från Kina medför vissa funkionella skillnader i Intune. 

- Intune som drivs av 21Vianet stöder endast fristående distributioner. Stöd för samhantering med System Center Configuration Manager är för närvarande under utveckling.
- Migreringar från offentliga moln till nationella moln stöds inte. Kunder som är intresserade av att flytta till Intune som drivs av 21Vianet måste migrera manuellt.
- Klientanslutningsfunktionen (synkronisering av enheter till Intune utan registrering som stöd för molnkonsolscenarier) stöds inte för närvarande.
- Härledda autentiseringsuppgifter stöds inte med Intune som drivs av 21Vianet.
- Intune som drivs av 21Vianet stöder inte Intune-agenten och stöder därför inte äldre datorhantering.
- Hantering av Windows 10 stöds med hjälp av den moderna MDM-kanalen.
- Intune som drivs av 21Vianet stöder inte lokalt Exchange-anslutningsprogram.
- Windows Autopilot- och Business Store-funktionerna är inte tillgängliga för närvarande.
- Eftersom Google Mobile Services inte är tillgängligt i Kina, så kan kunder i Intune som drivs av 21Vianet inte använda funktioner som kräver Google Mobile Services. Funktionerna är:
  - Google Play Protect-funktioner som SafetyNet-enhetsattestering.
  - Hantera appar från Google Play Butik.
  - Android Enterprise-funktioner. Mer information finns i denna [Google-dokumentation](https://support.google.com/work/android/answer/6270910?hl=en).
- Appen Intune-företagsportal för Android använder Google Mobile Services för att kommunicera med Microsoft Intune-tjänsten. Eftersom Google Play-tjänsterna inte är tillgängliga i Kina, kan vissa uppgifter kräva upp till åtta timmar att slutföra. Mer information finns i den här [artikeln](https://docs.microsoft.com/mem/intune/apps/manage-without-gms#limitations-of-intune-device-administrator-management-when-gms-is-unavailable). 
- Om Intunes klientfunktion (företagsportalappen) ska kunna att följa lokala föreskrifter och tillhandahålla förbättrade funktioner, så kan den avvika något i Kina.
- Avgränsning är inte tillgängligt.
- Tillgängligheten av hantering av mobilprogram (MAM) är beroende av att dessa appar är tillgängliga i Folkrepubliken Kina.

## <a name="you-control-customer-data"></a>Du kontrollerar kunddata

I Microsoft Azure, Intune, Office 365 och Power BI som drivs av 21Vianet har du fullständig kontroll över dina data:
- Du vet var kunddata finns.
- Du styr åtkomsten till dina kunddata.
- Du styr dina kunddata om du lämnar tjänsten.
- Du har olika alternativ för att kontrollera dina kunddatas säkerhet.

Med Microsoft Azure, Intune, Office 365 och Power BI som drivs av 21Vianet äger du dina data:
- 21Vianet använder inte kunddata för reklam.
- Du avgör vem som har åtkomst till dina kunddata.
- Vi använder logisk isolering för att åtskilja varje kunds data.
- Vi tillhandahåller enkla, transparenta dataanvändningsprinciper och inhämtar oberoende granskningar.
- Våra underleverantörer omfattas av kontrakt som garanterar att de uppfyller våra sekretesskrav.

## <a name="data-subject-requests"></a>Begäranden från registrerad person

Rollen som klientorganisationsadministratör för Intune som drivs av 21Vianet kan begära data för registrerade personer på följande sätt:

- Med hjälp av administrationscentret för Azure Active Directory kan en klientorganisationsadministratör ta bort data från Azure Active Directory och relaterade tjänster permanent. Mer information finns i [Azure Data Subject-begäranden – ta bort](https://docs.microsoft.com/microsoft-365/compliance/gdpr-dsr-azure?view=o365-worldwide#step-5-delete)
- Systemgenererade loggar för Microsoft-tjänster som drivs av 21Vianet kan exporteras av klientadministratörer med hjälp av dataloggexporten. Mer information finns i [Azure Data Subject-begäranden – exportera](https://docs.microsoft.com/microsoft-365/compliance/gdpr-dsr-azure?view=o365-worldwide#step-6-export).

## <a name="next-steps"></a>Nästa steg

[Läs mer om konfigurationer som stöds av Intune](supported-devices-browsers.md)