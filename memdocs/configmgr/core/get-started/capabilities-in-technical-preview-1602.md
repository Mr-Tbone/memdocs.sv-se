---
title: Funktioner i Technical Preview 1602
titleSuffix: Configuration Manager
description: Lär dig mer om funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1602.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1b9265d1-b461-47f8-b7ef-885da0fdd969
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 64d01598f3d5feb162898761645ac84b1c73b175
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074477"
---
# <a name="capabilities-in-technical-preview-1602-for-configuration-manager"></a>Funktioner i Technical Preview 1602 för Configuration Manager

*Gäller för: Configuration Manager (Technical Preview Branch)*

Den här artikeln beskriver de funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1602. Du kan installera den här versionen för att uppdatera och lägga till nya funktioner till din Configuration Manager Technical Preview-webbplats. Innan du installerar den här versionen av Technical Preview kan du läsa introduktions avsnittet, [teknisk för hands version för Configuration Manager](../../core/get-started/technical-preview.md), för att bekanta dig med allmänna krav och begränsningar för att använda en teknisk för hands version, hur du uppdaterar mellan versioner och hur du ger feedback om funktionerna i en teknisk för hands version.  

 Följande är nya funktioner som du kan prova med den här versionen.  

##  <a name="improvements-to-mobile-device-management"></a><a name="BKMK_MDM"></a>Förbättringar av hantering av mobila enheter  

### <a name="ios-activation-lock"></a>iOS-Aktiveringslås  
 Configuration Manager kan hjälpa dig att hantera iOS Aktiveringslås, en funktion i Hitta min iPhone-appen för enheter med iOS 7,1 och senare. Aktiveringslås aktiveras automatiskt när Hitta Min iPhone appen används på en enhet. När den har aktiverats måste användarens Apple-ID och lösenord anges innan någon kan:  

- Inaktivera Hitta Min iPhone  

- Rensa enheten  

- Återaktivera enheten  

  Configuration Manager kan begära Aktiveringslås status för både övervakade och oövervakade enheter som kör iOS 7,1 och senare. För övervakade enheter kan Intune hämta koden för att förbikoppla aktiveringslås och skicka den direkt till enheten.  

##  <a name="improvements-to-software-center-in-version-1602"></a><a name="BKMK_SC1601"></a>Förbättringar av Software Center i version 1602  

### <a name="refresh-pc-machine-and-user-policy-from-software-center"></a>Uppdatera dator-och användar princip från Software Center  
 Ett nytt alternativ, **Synkronisera princip** har lagts till på sidan **alternativ** > **dator underhåll** i Software Center som gör att datorn uppdaterar den Configuration Manager dator-och användar principer.  

##  <a name="improvements-to-windows-10-servicing"></a><a name="BKMK_Win10Servicing"></a>Förbättringar av service för Windows 10  
 I 1602 Technical Preview har vi lagt till följande förbättringar för Windows 10-underhåll:  

-   Nya filter alternativ för Service planer.  Nu kan du filtrera efter **språk**, **obligatorisk**och **rubrik**. Det är enbart uppgraderingar som uppfyller de angivna kriterierna som läggs till i den associerade distributionen.  

-   När du väljer klassificeringen **uppgraderingar** för synkronisering av program uppdateringar visas en varnings dialog ruta där du kan se att WSUS [Hotfix 3095113](https://support.microsoft.com/kb/3095113) krävs för att kunna synkronisera program uppdateringar och för att Windows 10-underhållet ska fungera korrekt.  I dialog rutan kan du gå till kunskaps bas artikeln för snabb korrigeringen.  

-   Tillgängliga Windows 10-uppgraderingar visas nu bara i noden **Windows 10** \ -**uppdateringar för alla Windows 10-uppdateringar** i Configuration Manager-konsolen. De här uppdateringarna visas inte längre i noden **program** \ uppdateringar**alla program uppdateringar** .  

-   Slutanvändare som startar ett Windows 10-uppgraderings paket uppmanas att ange en dialog ruta där de kan se att de kommer att uppgradera sitt operativ system.  
