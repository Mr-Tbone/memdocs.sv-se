---
title: Grunderna om platser och hierarkier
titleSuffix: Configuration Manager
description: Få grundläggande information om Configuration Manager-platser och hierarkier.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4db1e15f-e832-4cf9-be33-d3971e635a55
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 04ed22436d750572fed8ce898c5ed3a23b71f239
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722818"
---
# <a name="fundamentals-of-sites-and-hierarchies-for-configuration-manager"></a>Grunderna i platser och hierarkier för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

En Configuration Manager-distribution måste installeras i en Active Directory-domän. Grunden för den här distributionen omfattar en eller flera Configuration Manager-platser som utgör en hierarki av platser. Från en enskild plats till en hierarki med flera platser ger den typ och placering av platser som du installerar möjlighet att skala upp (expandera) din distribution vid behov och leverera viktiga tjänster för att hanterade användare och enheter.

## <a name="hierarchies-of-sites"></a>Platshierarkier
När du installerar Configuration Manager för första gången bestäms omfånget för hierarkin av den första Configuration Managers platsen som du installerar. Den första Configuration Managers platsen är den grund som du använder för att hantera enheter och användare i företaget. Den första platsen måste vara antingen en central administrations plats eller en fristående primär plats.  

 En *Central administrations plats* lämpar sig för storskaliga distributioner, ger en central plats för administration och ger flexibiliteten att stödja enheter som distribueras i en global nätverks infrastruktur. När du har installerat en central administrations plats måste du installera en eller flera primära platser som underordnade platser. Den här konfigurationen är nödvändig eftersom en central administrations plats inte har stöd för hantering av enheter, vilket är en primär platss funktion. En central administrations plats har stöd för flera underordnade primära platser. Underordnade-primära platser används för att hantera enheter direkt och för att kontrol lera nätverks bandbredden när de hanterade enheterna finns på olika geografiska platser.  

 En *fristående primär plats* är lämplig för mindre distributioner och kan användas för att hantera enheter utan att behöva installera ytterligare platser. Även om en fristående primär plats kan begränsa storleken på distributionen, har den stöd för ett scenario för att utöka hierarkin vid ett senare tillfälle genom att installera en ny central administrations plats. Med det här scenariot för webbplats expansion blir den fristående primära platsen en underordnad primär plats och du kan sedan installera ytterligare underordnade primära platser under den nya centrala administrations platsen. Sedan kan du utöka din första distribution för framtida tillväxt av företaget.  

> [!TIP]  
>  En fristående primär plats och en underordnad primär plats är egentligen samma typ av plats: en primär plats. Namnskillnaden bygger på det hierarkiförhållande som skapas när du även använder en central administrationsplats. Den här hierarkin relationen kan även begränsa installationen av vissa plats system roller som utökar Configuration Manager funktionerna. Den här begränsningen av roller inträffar eftersom vissa plats system roller bara kan installeras på platsen på den översta nivån i hierarkin, en central administrations plats eller en fristående primär plats.  

 När du har installerat din första plats kan du installera ytterligare platser. Om den första platsen är en central administrations plats kan du installera en eller flera underordnade primära platser. När du har installerat en primär plats (fristående eller underordnad primär) kan du sedan installera en eller flera sekundära platser.  

 En *sekundär plats* kan endast installeras som en underordnad plats under en primär plats. Den här platstypen kan utöka räckvidden för en primär plats för hantering av enheter som har långsam nätverksanslutning till den primära platsen. Även om en sekundär plats utökar den primära platsen, hanterar den primära platsen alla klienter. Den sekundära platsen har stöd för enheter på fjärrplatsen. Det ger stöd genom komprimering och hantering av överföring av information i ditt nätverk som du skickar (distribuerar) till klienter och som klienter skickar tillbaka till platsen.  

 Följande diagram visar några platsdesignexempel.  

 ![Hierarki-exempel](media/Hierarchy_examples.png)  

 Mer information finns i följande avsnitt:  

-   [Introduktion till Configuration Manager](../../core/understand/introduction.md)  

-   [Skapa en hierarki med webbplatser för Configuration Manager](../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md)  

-   [Installera Configuration Manager-platser](../servers/deploy/install/installing-sites.md)  

## <a name="site-system-servers-and-site-system-roles"></a>Platssystemservrar och platssystemroller  
 Varje Configuration Manager plats installerar *plats system roller* som stöder hanterings åtgärder. Följande roller installeras som standard när du installerar en-plats:

-   Plats Server rollen tilldelas till den dator där du installerar platsen.

-   Plats databasens server roll tilldelas SQL Server som är värd för plats databasen.

Andra plats system roller är valfria och används bara när du vill använda de funktioner som är aktiva i en plats system roll. Alla datorer som har en platssystemsroll kallas för platssystemservrar.  

 För en mindre distribution av Configuration Manager kan du först köra alla plats system roller direkt på plats serverdatorn. När din hanterade miljö och behoven växer kan du sedan installera ytterligare plats system servrar som värd för ytterligare plats system roller för att förbättra platsens effektivitet i att tillhandahålla tjänster till fler enheter.  

 Information om olika plats system roller finns i [plats system roller](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles) i [Planera för plats system servrar och plats system roller för Configuration Manager](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).

## <a name="publishing-site-information-to-active-directory-domain-services"></a>Publicera platsinformation på Active Directory Domain Services  
 För att förenkla hanteringen av Configuration Manager kan du utöka Active Directory-schemat så att det stöder information som används av Configuration Manager och sedan låta platser publicera sin viktig information till Active Directory Domain Services (AD DS). De datorer som du vill hantera kan på ett säkert sätt Hämta plats relaterad information från den betrodda källan till AD DS. Den information som klienter kan hämta identifierar tillgängliga platser, platssystemservrar och tjänster som dessa platssystemservrar tillhandahåller.  

 Det går bara att *utöka Active Directory schemat* en tid för varje skog och kan göras innan eller efter att du har installerat Configuration Manager.   När du utökar schemat måste du skapa en ny Active Directory-behållare med namnet System Management i varje domän. Behållaren innehåller en Configuration Manager-plats som ska publicera data som klienter ska hitta. Mer information finns i [förbereda Active Directory för webbplats publicering](../../core/plan-design/network/extend-the-active-directory-schema.md).  

 Om du *publicerar plats data* förbättras säkerheten för din Configuration Manager-hierarki och administrativa kostnader minskas, men det krävs inte för grundläggande Configuration Manager-funktioner.  
