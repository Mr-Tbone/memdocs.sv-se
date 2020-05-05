---
title: Grunderna i att hantera enheter
titleSuffix: Configuration Manager
description: Lär dig hur du använder Configuration Manager för att hantera enheter.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2bca3db9-115a-451d-8c93-f073ceefe0c7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bbe7f3a69694395f95596f7f1497c7356b33715f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722846"
---
# <a name="fundamentals-of-managing-devices-with-configuration-manager"></a>Grunderna i hantering av enheter med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Manager kan hantera två breda kategorier av enheter:

- *Klienter* är enheter som arbets stationer, bärbara datorer, servrar och mobila enheter där du installerar Configuration Manager-klient program varan. Vissa hanterings funktioner, som maskin varu inventering, kräver den här klient program varan.  

- *Hanterade enheter* kan omfatta *klienter*, men vanligt vis är det en mobil enhet där Configuration Manager klient program varan inte är installerad. På den här typen av enhet hanterar du med hjälp av den inbyggda lokala mobila enhets hanteringen i Configuration Manager.

Du kan också gruppera och identifiera enheter baserat på användaren, inte bara klient typen.

## <a name="managing-devices-with-the-configuration-manager-client"></a>Hantera enheter med Configuration Manager-klienten

Det finns två sätt att använda Configuration Manager klient program vara för att hantera en enhet. Det första sättet är att identifiera enheten i nätverket och sedan distribuera klient program varan till den enheten. Det andra sättet är att installera klient program varan manuellt på en ny dator och sedan ansluta datorn till din plats när den ansluter till nätverket. Kör en eller flera av de inbyggda identifierings metoderna för att identifiera enheter där klient programmet inte är installerat. När en enhet har identifierats kan du använda en av flera metoder för att installera-klient program varan. Information om hur du använder identifiering finns i [Kör identifiering för Configuration Manager](../servers/deploy/configure/run-discovery.md).  

När du har identifierat vilka enheter som har stöd för att köra Configuration Manager-klient program varan kan du använda en av flera metoder för att installera program varan. När programvaran har installerats och klienten har tilldelats till en primär plats kan du börja hantera enheten. Vanliga installations metoder är:

- Push-installation av klient

- Installation baserad på program uppdatering

- Grup princip

- Manuell installation på en dator

- Inklusive-klienten som en del av en OS-avbildning som du distribuerar  

När klienten har installerats kan du förenkla hanteringen av enheter med hjälp av samlingar. Samlingar är grupper av enheter eller användare som du skapar så att du kan hantera dem som en grupp. Du kanske till exempel vill installera ett program för mobila enheter på alla mobila enheter som Configuration Manager registrerar. I så fall kan du använda samlingen Alla mobila enheter.  

Mer information finns i dessa artiklar:  

- [Välja en lösning för enhetshantering](../plan-design/choose-a-device-management-solution.md)  

- [Installationsmetoder för klient](../clients/deploy/plan/client-installation-methods.md)  

- [Introduktion till samlingar](../clients/manage/collections/introduction-to-collections.md)  

### <a name="client-settings"></a>Klientinställningar

När du först installerar Configuration Manager konfigureras alla klienter i hierarkin med hjälp av de standard klient inställningar som du kan ändra. Klient inställningarna omfattar följande konfigurations alternativ:

- Hur ofta enheterna kommunicerar med platsen.

- Om klienten har kon figurer ATS för program uppdateringar och andra hanterings åtgärder.

- Om användarna kan registrera sina mobila enheter så att de hanteras av Configuration Manager.  

Du kan skapa anpassade klient inställningar och tilldela dem till samlingar. Medlemmar i samlingen konfigureras för att ha anpassade inställningar och du kan skapa flera anpassade klient inställningar som används i den ordning som du anger (med numerisk ordning). Om inställningarna krockar med varandra används inställningen med det lägsta ordningsnumret först.  

I följande diagram visas ett exempel på hur du skapar och använder anpassade klient inställningar.  

![Klientinställningar](media/ClientSettings.gif)  

Mer information om klient inställningar finns i följande artiklar:

- [Konfigurera klientinställningar](../clients/deploy/configure-client-settings.md)
- [Om klientinställningar](../clients/deploy/about-client-settings.md)


## <a name="managing-devices-without-the-configuration-manager-client"></a>Hantera enheter med Configuration Manager-klienten

Configuration Manager stöder hantering av vissa enheter som inte har installerat klient program varan och som inte hanteras av Intune. Mer information finns i [Hantera mobila enheter med lokal infrastruktur i Configuration Manager](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) och [Hantera mobila enheter med Configuration Manager och Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

## <a name="user-based-management"></a>Användarbaserad hantering

Configuration Manager stöder samlingar av Azure Active Directory och Active Directory Domain Services användare. När du använder en användar samling kan du installera program vara på alla datorer som medlemmarna i samlingen använder. För att se till att den program vara som du distribuerar bara installeras på enheter som har angetts som en användares primära enhet ställer du in mappning mellan användare och enhet. En användare kan ha en eller flera primära enheter.  

Ett av de sätt som användarna kan använda för att styra sin program distribution är att använda **Software Center** -klientens gränssnitt. **Software Center** installeras automatiskt på klient datorer och körs från **Start** -menyn i Windows. I **Software Center** kan användarna hantera sin egen program vara och utföra följande uppgifter:  

- Installera programvara  

- Schemalägga att programvara ska installeras automatiskt efter kontorstid  

- Konfigurera när Configuration Manager kan installera program vara på en enhet  

- Konfigurera åtkomst inställningar för fjärr styrning, om fjärr styrning har kon figurer ATS i Configuration Manager  

- Konfigurera alternativ för energispar funktioner, om en administratör konfigurerar det här alternativet  

- Bläddra efter, installera och begär program vara

- Konfigurera inställningar för inställningar

- När den har kon figurer ATS anger du en primär enhet för mappning mellan användare och enhet

Mer information finns i följande artiklar:

- [Planera för Software Center](../../apps/plan-design/plan-for-software-center.md)
- [Länka användare och enheter med mappning mellan användare och enhet](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)
- [Användarhandbok för Software Center](software-center.md)
