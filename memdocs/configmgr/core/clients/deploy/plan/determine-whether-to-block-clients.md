---
title: Blockera klienter
titleSuffix: Configuration Manager
description: Blockera klient åtkomst för systemsäkerhet med hjälp av Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 54ef5fbb-521d-4ca5-a1c5-61e6f538d71e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b01fd7944d8a6ab726712f6ebeb4cb5374896072
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713242"
---
# <a name="determine-whether-to-block-clients-in-configuration-manager"></a>Avgöra om klienter ska blockeras i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Om en klient dator eller en klients mobila enhet inte längre är betrodd kan du blockera klienten i System Center 2012 Configuration Manager-konsolen. Blockerade klienter avvisas av Configuration Manager-infrastrukturen så att de inte kan kommunicera med plats system för att ladda ned principer, ladda upp inventerings data eller skicka tillstånds-eller status meddelanden.  

 Du måste blockera och avblockera en klient från dess tilldelade plats i stället för från en sekundär plats eller en central administrationsplats.  

> [!IMPORTANT]  
>  Även om blockering i Configuration Manager kan hjälpa till att skydda Configuration Manager-platsen ska du inte förlita dig på den här funktionen för att skydda platsen från ej betrodda datorer eller mobila enheter om du tillåter klienter att kommunicera med plats system via HTTP, eftersom en blockerad klient kan ansluta till platsen igen med ett nytt självsignerat certifikat och maskinvaru-ID. Använd istället blockeringsfunktionen för att blockera borttappade eller komprometterade startmedia som du använder för att distribuera operativsystem samt när platssystem accepterar HTTPS-klientanslutningar.  

 Klienter som kommer åt platsen med ISV-proxycertifikat går inte att blockera. Mer information om ISV-proxyns certifikat finns i Configuration Manager Software Development Kit (SDK).  

 Om dina platssystem accepterar HTTPS-klientanslutningar och din PKI (Public Key Infrastructure) stöder en lista över återkallade certifikat (CRL) bör du alltid se återkallande av certifikat som det första försvaret mot potentiellt komprometterade certifikat. Att blockera klienter i Configuration Manager ger en extra försvars linje för att skydda din hierarki.  

##  <a name="considerations-for-blocking-clients"></a><a name="BKMK_Block_vs_CRL"></a> Att tänka på vid blockering av klienter  

-   Alternativet är tillgängligt för HTTP- och HTTPS-klientanslutningar, men har begränsad säkerhet när klienter ansluter till platssystem med HTTP.  

-   Configuration Manager administrativa användare har behörighet att blockera en klient, och åtgärden utförs i Configuration Manager-konsolen.  

-   Klient kommunikation avvisas endast från Configuration Manager hierarki.  

    > [!NOTE]  
    >  Samma klient kan registreras med en annan Configuration Manager-hierarki.  

-   Klienten blockeras omedelbart från Configuration Managers platsen.  

-   Hjälper till att skydda platssystem från potentiellt komprometterade datorer och mobila enheter.  

## <a name="considerations-for-using-certificate-revocation"></a>Att tänka på vid återkallande av certifikat  

-   Alternativet är tillgängligt för HTTPS Windows-klientanslutningar om den infrastruktur som bygger på offentliga nycklar stöder en lista med återkallade certifikat (CRL).  

     Mac-klienter utför alltid CRL-kontroll och denna funktion går inte att inaktivera.  

     Även om mobila enhets klienter inte använder listor över återkallade certifikat för att kontrol lera certifikat för plats system, kan deras certifikat återkallas och kontrol leras av Configuration Manager.  

-   Administratörer av infrastruktur för offentliga nycklar har behörighet att återkalla ett certifikat, och åtgärden utförs utanför Configuration Manager-konsolen.  

-   Klientkommunikation kan avvisas från alla datorer och mobila enheter som kräver det här klientcertifikatet.  

-   Det uppstår antagligen en fördröjning mellan återkallandet av ett certifikat och att platssystemen laddar ned den ändrade listan med återkallade certifikat (CRL).  

-   För många PKI-distributionen kan fördröjningen vara en dag eller ännu längre. I Active Directory Certificate Services är t.ex. utgångsperioden som standard en vecka för en fullständig CRL och en dag för en lista över ändringar i återkallade certifikat.  

-   Hjälper till att skydda platssystem och klienter från potentiellt komprometterade datorer och mobila enheter.  

    > [!NOTE]  
    >  Du kan ge ytterligare skydd till platssystem som kör IIS från okända klienter genom att konfigurera en lista över betrodda certifikat (CTL) i IIS.  
