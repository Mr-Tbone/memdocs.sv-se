---
title: Automatiskt kategorisera enheter i samlingar
titleSuffix: Configuration Manager
description: Kategorisera enheter automatiskt i samlingar.
ms.date: 04/23/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 98b038b4-1a13-4228-bdb8-a12194e32b0e
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: f91f150a095838484c516226da0d3e44e1f5b331
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714313"
---
# <a name="automatically-categorize-devices-into-collections"></a>Automatiskt kategorisera enheter i samlingar

*Gäller för: Configuration Manager (aktuell gren)*

Du kan skapa enhets kategorier, som kan användas för att automatiskt placera enheter i enhets samlingar när du använder Configuration Manager med Microsoft Intune. Användarna måste sedan välja en enhets kategori när de registrerar en enhet i Intune. Du kan ändra en enhets kategori från Configuration Manager-konsolen.

> [!IMPORTANT]
>  Den här funktionen fungerar med **2016** -versionen av Microsoft Intune och senare. Se till att du har uppdaterat till den här versionen innan du provar de här procedurerna.

## <a name="create-device-categories"></a>Skapa enhets kategorier

1.  Gå till **till gångar och efterlevnad** > **Översikt över** > **enhets samlingar**.
2.  På fliken **Start** i gruppen **enhets samlingar** väljer du **Hantera enhets kategorier**.
3.  Skapa, redigera eller ta bort kategorier.

## <a name="associate-a-collection-with-a-device-category"></a>Koppla en samling till en enhets kategori

När du associerar en samling med en enhets kategori kommer alla enheter i den kategorin att läggas till i samlingen. Du kan inte lägga till en enhets kategori regel i en inbyggd samling, till exempel **alla system**.

1.  Välj **Lägg till regel** > **enhets kategori regel**på fliken **medlemskaps regler** i dialog rutan **Egenskaper** för en enhets samling.
2.  I dialog rutan **Välj enhets kategorier** väljer du en eller flera enhets kategorier som ska användas för alla enheter i samlingen.

## <a name="change-the-category-of-a-device"></a>Ändra kategori för en enhet

1.  I**översikts** > **enheter**för **till gångar och efterlevnad** > väljer du en enhet från listan **enheter** .
2.  Välj **Ändra kategori**i gruppen **enhet** på fliken **Start** .
3.  Välj en kategori och välj sedan **OK**.

## <a name="view-which-category-a-device-belongs-to"></a>Visa vilken kategori en enhet tillhör

I enhets **listan visas** kategorin i kolumnen **enhets kategori** i **till gångar och efterlevnad** > **Översikt** > av**enheter**.

Om kolumnen **enhets kategori** inte visas högerklickar du på rubriken för en av kolumnerna **i enhets listan (** som **namn**) och väljer sedan **enhets kategori**.

Om du tilldelar en enhet till en kategori och sedan tar bort kategorin, visar rapport **listan över enheter som registrerats per användare i Microsoft Intune** ett GUID i kolumnen **enhets kategori** i stället för ett kategori namn.
