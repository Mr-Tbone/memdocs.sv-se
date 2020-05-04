---
title: Skapa virtuella App-V-miljöer
titleSuffix: Configuration Manager
description: Skapa virtuella miljöer med Microsoft Application Virtualization så att appar kan dela data med varandra.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: b6b86078-fcc4-46cf-87d6-4b52b914b712
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2280218d3d237f91f0db3150dbc2031bad3e1816
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710421"
---
# <a name="create-app-v-virtual-environments-in-configuration-manager"></a>Skapa virtuella App-V-miljöer i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

I en virtuell miljö för Microsoft Application Virtualization (App-V) i Configuration Manager kan distribuerade virtuella program dela samma fil system och register på klientens Windows-datorer. Till skillnad från virtuella standard program kan dessa program dela data med varandra. Virtuella miljöer skapas eller ändras på klient datorer när programmet installeras eller nästa gång klienterna utvärderar sina installerade program. Du kan ordna dessa program så att när flera program försöker att modifiera ett filsystem eller ett registervärde så har programmet med den högsta prioriteten företräde.  

> [!IMPORTANT]  
>  Förlita dig inte på virtuella App-V-miljöer för att ge skydd, till exempel från skadlig kod.  

 Använd följande procedur för att skapa en virtuell App-V-miljö i Configuration Manager.  

## <a name="create-an-app-v-virtual-environment"></a>Skapa en virtuell App-V-miljö  

1.  I Configuration Manager-konsolen väljer du **program bibliotek program bibliotek** > **program hantering** > **App-V virtuella miljöer**.  

3.  På fliken **Start** går du till gruppen **skapa** och väljer **Skapa virtuell miljö**.  

4.  Ange följande information i dialog rutan **Skapa virtuell miljö** :  

    -   **Namn**.  Ange ett unikt namn för den virtuella miljön (högst 128 tecken).  

    -   **Beskrivning**. Valfritt Ange en beskrivning för den virtuella miljön.  

5.  Om du vill lägga till en ny distributions typ i den virtuella miljön väljer du **Lägg till**. Du måste lägga till minst en distributionstyp.  

6.  I dialog rutan **Lägg till program** anger du ett **grupp namn** (högst 128 tecken). Du kommer att använda det här namnet för att referera till gruppen med program som du lägger till i den virtuella miljön.  

7.  Välj **Lägg till**, Välj de App-V 5-program och distributions typer som du vill lägga till i gruppen och välj sedan **OK**.  

8.  I dialog rutan **Lägg till program** kan du välja **öka order** eller **minska ordning** för att ange det program som har prioritet om flera program försöker ändra fil systemet eller register inställningarna i samma virtuella miljö.  

9. Välj **OK**för att återgå till dialog rutan **Skapa virtuell miljö** .  

10. När du är klar med att lägga till grupper väljer du **OK** för att skapa den virtuella miljön. Den nya virtuella miljön visas i noden **App-V-virtuella miljöer** i Configuration Manager-konsolen. Du kan övervaka statusen för dina virtuella miljöer med status rapporten för den virtuella App-V-miljön.  

    > [!NOTE]  
    >  Den virtuella miljön läggs till eller ändras på klient datorer när programmet installeras eller nästa gång klienten utvärderar installerade program.  
