---
title: Skapa Windows Embedded-program
titleSuffix: Configuration Manager
description: Se vilka överväganden du måste ta med i beräkningen när du skapar och distribuerar program för Windows Embedded-enheter.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 16acfd63-0c40-424c-82f4-8c63f7f1c30b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: bec9765e5152863bb8b55a0b75f1e5c2fc580550
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710498"
---
# <a name="create-windows-embedded-applications-with-configuration-manager"></a>Skapa Windows Embedded-program med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Förutom de andra Configuration Manager krav och procedurer för att skapa ett program måste du även tänka på följande när du skapar och distribuerar program för Windows Embedded-enheter.  

## <a name="general-considerations"></a>Generella saker att tänka på  

-   När du distribuerar program till Windows Embedded-enheter som är aktiverade för Skriv filtrering kan du ange om Skriv filtret ska inaktive ras på enheten under distributionen av appen. Du kan sedan välja att starta om Skriv filtret när du har distribuerat appen. Om Skriv filtret inte är inaktiverat distribueras program varan till ett tillfälligt överlägg. Det innebär att om inte en annan distribution tvingar fram ändringar, kommer program varan inte längre att installeras när enheten startas om.  

-   När du distribuerar ett program på en Windows Embedded-enhet bör du se till att enheten tillhör en samling som har en konfigurerad underhållsperiod. På så vis kan du hantera när skrivfiltret ska inaktiveras och aktiveras och när enheten ska startas om.  

-   Inställningen som styr Skriv filter beteendet är en kryss ruta med namnet **genomför ändringar efter deadline eller under ett underhålls fönster (omstart krävs)**.  

## <a name="tips-for-deploying-applications"></a>Tips för att distribuera program  

**Använd nödvändiga program snarare än tillgängliga program för Windows Embedded-enheter med aktiverade Skriv filter.** Eftersom användarna inte kan installera appar från Software Center på en Windows Embedded-enhet med aktiverade Skriv filter ska du alltid distribuera program med ett distributions syfte som **krävs** i **stället för dessa** enheter. Vanligt vis är detta inte ett problem eftersom datorer som kör ett Windows Embedded-operativsystem ofta kör ett enda program som måste köras på samma sätt för flera användare. På grund av detta administreras dessa enheter hårt och spärras av IT-avdelningen. Nödvändiga program passar det här scenariot bra.

 Om användarna däremot kör fler än ett program på inbäddade enheter när skrivfilter är aktiverade ska dessa användare informeras om följande begränsningar:  

-   Användarna kan inte installera nödvändiga program från Software Center.  

-   Användarna kan inte ändra sin arbetstid på fliken Alternativ i Software Center.  

-   Användarna kan inte skjuta upp installationen av ett nödvändigt program.  

Dessutom kan användare med låg behörighet inte logga in under en underhålls period om Configuration Manager genomför ändringar för program varu installationer och uppdateringar. Under den här perioden visas ett meddelande för användarna om att enheten inte är tillgänglig eftersom den underhålls.  

**Distribuera inte program till Windows Embedded-enheter som har Skriv filter aktiverade om programmen kräver att användaren accepterar licens villkoren.** När Skriv filter har inaktiverats så att Configuration Manager kan installera program vara på inbäddade enheter kan användare med låg behörighet inte logga in på enheten. Om installationen kräver att användaren accepterar licensvillkoren är detta inte möjligt och installationen misslyckas. Se till att du inte distribuerar program till Windows Embedded-enheter om installationen kräver interaktion från användaren. Du kan använda listan Tillämpliga plattformar för att filtrera de här operativsystemen.  
