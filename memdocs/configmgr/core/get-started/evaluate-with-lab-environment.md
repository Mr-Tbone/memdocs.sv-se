---
title: Utvärdera i en labb miljö
titleSuffix: Configuration Manager
description: Skapa en labb miljö för att utvärdera Configuration Manager för användning i din organisation.
ms.date: 02/28/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 01b30260-f03a-4851-a549-d1b76e8cfc69
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: dd238319ba064f57911eee58e1299e17a2ce5b60
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713844"
---
# <a name="evaluate-configuration-manager-by-building-your-own-lab-environment"></a>Utvärdera Configuration Manager genom att skapa en egen labb miljö

*Gäller för: Configuration Manager (aktuell gren)*

 Lär dig hur du skapar en labb miljö för att utvärdera Configuration Manager för användning i din organisation.  

 Configuration Manager är ett komplext och kraftfullt verktyg för att hantera användare, enheter och program. Det är en bra idé att noggrant utvärdera Configuration Manager före fullständig distribution, så att du kan förstår konceptuell förståelse med praktiska övningar.  

 Den här guiden är främst avsedd för administratörer som utvärderar användningen av Configuration Manager i företags miljöer:  

-   Administratörer som vill ha en lösning för att fullständigt hantera datorer, servrar och mobila enheter  

-   Administratörer i hög säkerhets branscher som kräver säkerhet för lokal enhets hantering med flexibiliteten i molnbaserad enhets hantering  

-   Administratörer som vill hantera skalningen av sin lokala server arkitektur  

## <a name="what-this-lab-does"></a>Det här sker i labben  
 Det främsta målet med att skapa den här labb miljön är att ge dig den allmänna kunskapen att börja arbeta med Configuration Manager och förbättra din förståelse av Configuration Manager. Du går igenom en snabbare sammansättning av den aktuella versionen av Configuration Manager med två servrar:  

-   En som är värd för Active Directory, domänkontrollanten och DNS-servern  

-   En som är värd för Configuration Manager och alla tillhör ande SQL Servers komponenter  

Klientdatorer installeras i Hyper-V. Själva labben kan också köras som ett fullständigt virtualiserat system på en enskild server.  

## <a name="what-this-lab-does-not-do"></a>Det här sker inte i labben  
 Det här labbet tar dig inte igenom alla Configuration Manager scenarier. Den är inte avsedd att genast migreras till en aktiv miljö.  

 När du skapar den här labben får du en funktionell miljö att arbeta i. Den här miljön kommer dock inte att optimeras för faktorer som system prestanda, hantering av hårddisk utrymme och SQL Server lagring.  

##  <a name="recommended-reading-before-you-build-the-lab"></a><a name="BKMK_EvalRec"></a>Rekommenderad läsning innan du skapar labbet  
 Det finns en mängd innehåll som finns i [dokumentationen för Configuration Manager](https://docs.microsoft.com/sccm/). Vi rekommenderar att du läser följande avsnitt från det här biblioteket innan du börjar skapa labbet:  

-   Lär dig viktiga begrepp om Configuration Manager-konsolen, slut användar portaler och exempel scenarier i [Introduktion till Configuration Manager](../../core/understand/introduction.md).  

-   Lär dig mer om de viktigaste hanterings funktionerna i Configuration Manager i [funktioner och funktioner i Configuration Manager](../../core/plan-design/changes/features-and-capabilities.md).  

-   Stärka dina kunskaper med [grunderna i Configuration Manager](../../core/understand/fundamentals.md).  

-   Lär dig vikten av säkerhets roller i [grunderna i rollbaserad administration för Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

-   Lär dig mer om innehålls hantering i [koncept för innehålls hantering](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

-   Lär dig hur du kan stödja dagliga uppgifter i hela distributionen i [förstå hur klienter hittar plats resurser och tjänster för Configuration Manager](../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  
