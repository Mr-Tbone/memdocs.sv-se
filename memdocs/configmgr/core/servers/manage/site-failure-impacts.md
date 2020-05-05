---
title: Påverkan av webbplatsfel
titleSuffix: Configuration Manager
description: Förstå effekterna av olika problem på en Configuration Manager webbplats.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6f0e08f8-f2e1-4823-90f6-7b1f4341eb46
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bf56aee2e9f73ea8c3c69737c749f2a599e1ac37
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723896"
---
# <a name="site-failure-impacts-in-configuration-manager"></a>Plats haveri påverkan i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Plats servern och andra plats system kan inte utföras och orsaka förlust av de tjänster som de tillhandahåller regelbundet. Om du installerar flera plats system på samma dator och den datorn Miss lyckas, är alla tjänster som tillhandahålls regelbundet av dessa plats system inte längre tillgängliga.

En del av planerings processen bör omfatta förståelse för hur tjänsten som du tillhandahåller din organisation har betydelse. Eftersom varje plats system på platsen har olika funktioner skiljer sig effekten av ett fel på platsen, beroende på den plats systemets roll som misslyckades. 

Använd [alternativ för hög tillgänglighet](../deploy/configure/high-availability-options.md) för att minimera fel i ett enskilt system. Planera även och öva på en [säkerhets kopierings-och återställnings](backup-and-recovery.md) strategi för att minska den tid som tjänsten inte är tillgänglig.

I följande avsnitt beskrivs effekterna när det angivna plats systemet inte fungerar:


### <a name="site-server"></a>Platsserver

- Ingen plats administration är möjlig. Det går inte att ansluta-konsolen till platsen.  

- Hanterings platsen samlar in klient information och cachelagrar den tills plats servern är online igen.  

- Användare kan köra befintliga distributioner och klienter kan ladda ned innehåll från distributions platser.  


### <a name="site-database"></a>Platsdatabas

- Ingen plats administration är möjlig.  

- Om den Configuration Manager-klienten redan har en princip tilldelning med nya principer, och om hanterings platsen har cachelagrat princip innehållet, kan klienten göra en begäran om princip brödtext och ta emot princip bröd svaret. Platsen kan dock inte betjäna några nya begär Anden om princip tilldelningar.  

- Klienter kan köra distributioner, endast om de redan har tagit emot principen och de tillhör ande källfilerna redan cachelagras lokalt på klienten.  


### <a name="management-point"></a>Hanteringsplats

- Även om du kan skapa nya distributioner tar klienterna inte emot dem förrän en hanterings plats är online.  

- Klienterna samlar fortfarande in inventering, avläsning av program vara och statusinformation. De lagrar dessa data lokalt tills hanterings platsen är tillgänglig.  

- Klienter kan köra distributioner, endast om de redan har tagit emot principen och de tillhör ande källfilerna redan cachelagras lokalt på klienten.  


### <a name="distribution-point"></a>Distributionsplats

- Configuration Manager-klienter kan köra distributioner, endast om de associerade källfilerna redan har hämtats lokalt eller är tillgängliga på en peer-källa.

