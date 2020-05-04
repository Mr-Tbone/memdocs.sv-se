---
title: Klient hälsa med samhantering
titleSuffix: Configuration Manager
description: Behåll synligheten för Configuration Manager klient hälsa från Intune på Azure Portal
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 5b243aac-8a1a-4f14-ba3f-5446bb483e92
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 11fbeaf76737a832afca7351e8587e0d9c4bacac
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711198"
---
# <a name="client-health-with-co-management"></a>Klient hälsa med samhantering

Nätverkets hälso tillstånd är direkt anslutet till hälso tillståndet för enheterna som flyttas in och ut ur det. Intune kan kommunicera med en klient som inte är felfri, även om den inte finns i nätverket. Använd Co-Management för att kombinera den här funktionen med Configuration Manager möjlighet att rapportera tillbaka 98% av kända felfria klienter. Sedan kan du identifiera, utvärdera och tillhandahålla synlighet för alla klienter i real tid. Intune lägger också till det stöd som krävs för att uppgradera kompatibiliteten över alla anslutna klienter.

I följande videoklipp är Senior program hanterare Anders York och Ainley för produkt marknadsförings hantering att diskutera och demonstrera klient hälsa med samhantering:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Client-Health-Monitoring-with-Co-Management/player]



## <a name="benefits"></a>Fördelar

Bedömning av klientens hälsa är en högsta prioritet. System Center 2012 Configuration Manager tillagt **CCMeval**. Det här verktyget är externt för Configuration Manager-klienten. Den tillhandahåller övervakning av klient hälsa och automatisk reparation. Den här rapporten förlitar sig dock på en enhet som är fysiskt eller i stort sett i det interna nätverket. Samhantering hjälper till att lösa det här problemet.

Med samhantering kan Intune rapportera om klientens hälso tillstånd. Den tillhandahåller tidsstämpel-information för att data ska vara giltiga. Den här informationen visar om enheterna är felfria, kan ansluta, kunna installera appar eller kan uppdatera till de nödvändiga OS-versionerna. 

En detaljerad översikt över den här funktionen finns i den här videon från [vad som är nytt i Configuration Manager](https://myignite.techcommunity.microsoft.com/sessions/64591) -sessionen vid antändning 2018.

> [!VIDEO https://www.youtube.com/embed/UAW2KBUq7DM?start=518]


När Configuration Manager tillhandahåller enhets status som klienten är installerad, men det inte är det kan Intune tillhandahålla mer information utan att behöva ansluta till klienten. Enhetens hälso information i Intune är lätt att förstå. Om statusen är något annat än **felfritt**ger den rekommendationer och nästa steg för att felsöka och åtgärda det.

> [!Note]  
> Följande förmåner planeras för framtida versioner:
> - Configuration Manager kommer att inkludera ytterligare funktioner i CCMeval  
> - Det blir enklare att identifiera potentiellt skadliga datorer i både Configuration Manager och Intune  
> - Du kan gruppera klient hälso data i Intune  



## <a name="value-proposition"></a>Värde förslag

Med den här funktionen har du nu en extern data källa med Intune. Det gör att du kan fastställa nästa steg när du felsöker en omfattande uppsättning klient problem. Nu behöver du inte skapa ytterligare rapporter eller använda andra verktyg för att hämta klient data.

När du har felfria klienter har du snabb uppdaterad korrigerings överensstämmelse. Bättre patch-kompatibilitet innebär bättre säkerhet.



## <a name="configure"></a>Konfigurera

Använd följande steg för att komma igång med den här funktionen:

- Uppdatera enheter till Windows 10, version 1709 eller senare  

- [Aktivera samhantering](how-to-enable.md)  
    - Du behöver inte byta arbets belastning till Intune  

- Uppdatera Configuration Manager-platsen och-klienterna till *version 1806* eller senare  


### <a name="review-configuration-manager-client-health-in-intune"></a>Granska Configuration Manager klient hälsa i Intune

1. Logga in på [Azure Portal](https://portal.azure.com/).  

2. Välj **alla tjänster** > **Intune**. Intune finns i avsnittet **Övervakning och hantering**.  

3. När du har öppnat fönstret **Microsoft Intune** går du till sidan **fel sökning** på menyn under **Hjälp och support**.  

4. Använd alternativet **Välj användare** , leta upp den aktuella enheten i **enhets** listan och öppna sidan enhet genom att välja den.  

5. Information om samhantering visas längst ned på enhets sidan. Den här informationen omfattar följande fält för klientens hälsa:  
    - **Configuration Manager agent tillstånd**  
    - **Check-tid för senaste Configuration Manager agent**  

> [!Tip]  
> Intune-registrerade enheter ansluter till moln tjänsten tre gånger om dagen, ungefär var åttonde timme. 
