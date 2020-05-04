---
title: Egenskaper för klient installation i Active Directory
titleSuffix: Configuration Manager
description: Publicera Configuration Manager klient installations egenskaper för Active Directory Domain Services.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 101d7d4d-92db-419d-b2ae-3c1c1dea68e9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 49b2edf7234e53c3fc03542f803933463190e8c1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712073"
---
# <a name="about-client-installation-properties-published-to-active-directory-domain-services"></a>Om klient installations egenskaper som publicerats till Active Directory Domain Services

*Gäller för: Configuration Manager (aktuell gren)*

När du utökar Active Directory-schemat för Configuration Manager och platsen publiceras till Active Directory Domain Services publiceras många klient installations egenskaper till Active Directory Domain Services. Om en dator kan hitta de här klient installations egenskaperna kan den använda dem under Configuration Manager klient distributionen.  

 Fördelarna med att använda Active Directory Domain Services för att publicera egenskaper för klientinstallation är bland annat:  

-   Klient installationer som baseras på program uppdaterings plats och grupprincip klient installationer kräver inte att installations parametrar konfigureras på varje dator.  

-   Eftersom den här informationen genereras automatiskt elimineras risken för handhavarfel vid manuell inmatning av installationsegenskaper.  

> [!NOTE]  
>  Mer information om hur du utökar Active Directory schema för Configuration Manager och hur du publicerar en plats finns i [schema tillägg för Configuration Manager](../../plan-design/network/schema-extensions.md).  

## <a name="client-installation-properties-published-to-active-directory-domain-services"></a>Klient installations egenskaper som publicerats till Active Directory Domain Services  
Följande är en lista över klient installations egenskaper. Mer information om varje objekt i listan nedan finns i [om klient installations egenskaper](../../../core/clients/deploy/about-client-installation-properties.md).  

- Den Configuration Manager plats koden.  

- Platsserverns signeringscertifikat.  

- Den betrodda rotnyckeln.  

- Klientkommunikationsportarna för HTTP och HTTPS.  

- Återställningsstatusplatsen. Om platsen har flera återställnings status punkter publiceras bara den första som installerades till Active Directory Domain Services.  

- En inställning som anger att klienten endast får kommunicera med HTTPS.  

- Inställningar relaterade till PKI-certifikat:  

  -   Huruvida ett klient-PKI-certifikat ska användas.  

  -   Urvals villkoren för val av certifikat. Detta kan krävas på grund av att klienten har mer än ett giltigt PKI-certifikat som kan användas för Configuration Manager.  

  -   En inställning som avgör vilket certifikat som ska användas om klienten har flera giltiga certifikat efter certifikaturvalsprocessen.  

  -   Den lista med certifikatutfärdare som innehåller en lista med betrodda rotcertifikatutfärdare.  

- Installationsegenskaper för Client.msi som definierats på fliken **Klient** i dialogrutan **Egenskaper för push-installation av klient** .

Klient installation (CCMSetup) använder de egenskaper som har publicerats till Active Directory Domain Services endast om inga andra egenskaper anges med något av följande:  

-   Den manuella installations metoden (beskrivs längre fram i den här artikeln)

-   Installations metoden för grupprincip (beskrivs längre fram i den här artikeln)

> [!NOTE]  
>  Egenskaperna för klient installation används för att installera-klienten. Dessa egenskaper kan skrivas över med nya inställningar från dess tilldelade plats efter att klienten har installerats och har tilldelats en Configuration Manager plats.  

 Använd informationen i följande avsnitt för att avgöra vilka Configuration Manager-klient installations metoder som använder Active Directory Domain Services för att hämta klient installations egenskaper.  

## <a name="client-push-installation"></a>Push-installation av klient  
 Push-installation av klienter använder inte Active Directory Domain Services för att hämta installationsegenskaper.  

 I stället kan du ange klient installations egenskaper på fliken **installations egenskaper** i dialog rutan **Egenskaper för push-installation av klient** . Dessa alternativ och klientrelaterade platsinställningar lagras i en fil som klienten läser vid klientinstallation.  

> [!NOTE]  
>  Du behöver inte ange några CCMSetup-egenskaper för push-installation av klienter, återställnings status punkten eller den betrodda rot nyckeln på fliken **installations egenskaper** . De här inställningarna tillhandahålls automatiskt till klienter när de installeras med push-installation av klienter.
Förutom client. msi-egenskaper, stöder CCMSetup följande parametrar:/forcereboot,/skipprereq,/logon,/BITSPriority,/downloadtimeout,/forceinstall

 De egenskaper som du anger på fliken **installations egenskaper** publiceras till Active Directory Domain Services om platsen publiceras till Active Directory Domain Services. De här inställningarna läses av klientinstallationer där CCMSetup körs utan installationsegenskaper.  

## <a name="software-update-point-based-installation"></a>Platsbaserad klientinstallation av programuppdateringar  
 Installationsmetoden som baseras på programuppdateringspunkten stöder inte tillägg av installationsegenskaper till CCMSetup-kommandoraden.  

 Om inga kommandoradsegenskaper har etablerats på klientdatorn med en grupprincip, söker CCMSetup i Active Directory Domain Services efter installationsegenskaper.  

## <a name="group-policy-installation"></a>Grupprincipinstallation  
 Installationsmetoden med grupprincip stöder inte tillägg av installationsegenskaper till CCMSetup-kommandoraden.  

 Om inga kommandoradsegenskaper har etablerats på klientdatorn, söker CCMSetup i Active Directory Domain Services efter installationsegenskaper.  

## <a name="manual-installation"></a>Manuell installation  
 CCMSetup söker i Active Directory Domain Services efter installationsegenskaper under följande förhållanden:  

-   Inga kommandoradsegenskaper har angetts efter kommandot CCMSetup.exe.  

-   Datorn har inte etablerats med installationsegenskaper genom att använda grupprincip.  

## <a name="logon-script-installation"></a>Installation av inloggningsskript  
 CCMSetup söker i Active Directory Domain Services efter installationsegenskaper under följande förhållanden:  

-   Inga kommandoradsegenskaper har angetts efter kommandot CCMSetup.exe.  

-   Datorn har inte etablerats med installationsegenskaper genom att använda grupprincip.  

## <a name="software-distribution-installation"></a>Programdistributionsinstallation  
 CCMSetup söker i Active Directory Domain Services efter installationsegenskaper under följande förhållanden:  

-   Inga kommandoradsegenskaper har angetts efter kommandot CCMSetup.exe.  

-   Datorn har inte etablerats med installationsegenskaper genom att använda grupprincip.  

## <a name="installations-for-clients-that-cannot-access-active-directory-domain-services"></a>Installationer för klienter som inte kan komma åt Active Directory Domain Services  
De här klient datorerna kan inte läsa eller komma åt de publicerade installations egenskaperna från Active Directory Domain Services.

 Dessa klienter omfattar:  

-   Arbets grupps datorer.  

-   Klienter som har tilldelats en Configuration Manager plats som inte har publicerats till Active Directory Domain Services.  

-   Klienter som installeras när de är på Internet.  
