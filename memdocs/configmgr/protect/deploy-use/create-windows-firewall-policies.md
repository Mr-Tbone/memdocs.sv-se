---
title: Principer för Windows-brandväggen för Endpoint Protection
titleSuffix: Configuration Manager
description: Lär dig hur du skapar och distribuerar brand Väggs principer för Endpoint Protection i System Center 2012 Configuration Manager.
ms.date: 03/07/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 6ecdfad1-6305-45a8-ae75-3f33b967cb8f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7c017e750e175e09a67deb4651cf7e8eb98f1bc1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715496"
---
# <a name="create-and-deploy-windows-firewall-policies-for-endpoint-protection-in-configuration-manager"></a>Skapa och distribuera principer för Windows-brandväggen för Endpoint Protection i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Med brand Väggs principer för Endpoint Protection i Configuration Manager kan du utföra grundläggande konfigurations-och underhålls åtgärder för Windows-brandväggen på klient datorer i hierarkin. Du kan använda Windows-brandväggsprinciper för att utföra följande uppgifter:  

-   Kontrollera om Windows-brandväggen är aktiverad eller inte.  

-   Kontrollera om inkommande anslutningar tillåts till klientdatorer.  

-   Styra om användare ska meddelas när Windows-brandväggen blockerar ett nytt program.  

1.  Klicka på **Tillgångar och efterlevnad** i Configuration Manager-konsolen.  

2.  I arbets ytan **till gångar och efterlevnad** expanderar du **Endpoint Protection**och klickar sedan på **principer för Windows-brandväggen**.  

3.  Klicka på **Skapa en princip för Windows-brandväggen** i gruppen **Skapa** på fliken **Start**.  

4.  På sidan **Allmänt** i guiden **Skapa princip för Windows-brandväggen**anger du ett namn och en valfri beskrivning för brandväggsprincipen och klickar sedan på **Nästa**.  

5.  På sidan **Profilinställningar** i guiden konfigurerar du följande inställningar för varje nätverksprofil:  

    > [!NOTE]  
    >  Mer information om nätverksprofiler finns i Windows-dokumentationen.  

    -   **Aktivera Windows-brandväggen**  

        > [!NOTE]  
        >  Om **Aktivera Windows-brandväggen** inte är aktiverad är de andra inställningarna på den här sidan i guiden inte tillgängliga.  

    -   **Blockera alla inkommande anslutningar, även de som finns i listan över tillåtna program**  

    -   **Meddela användaren när ett nytt program blockeras av Windows-brandväggen**  

6.  Granska åtgärderna som ska vidtas på sidan **Sammanfattning** i guiden och slutför sedan guiden.  

7.  Kontrollera att den nya principen för Windows-brandväggen visas i listan **Principer för Windows-brandväggen** .  

##  <a name="to-deploy-a-windows-firewall-policy"></a><a name="BKMK_Assign"></a> Så här distribuerar du en princip för Windows-brandväggen  

1.  Klicka på **Tillgångar och efterlevnad** i Configuration Manager-konsolen.  

2.  I arbets ytan **till gångar och efterlevnad** expanderar du **Endpoint Protection**och klickar sedan på **principer för Windows-brandväggen**.  

3.  I listan **Principer för Windows-brandväggen** väljer du den princip för Windows-brandväggen som du vill distribuera.  

4.  På fliken **Start** går du till gruppen **Distribution** och klickar på **Distribuera**.  

5.  I dialogrutan **Distribuera princip för Windows-brandväggen** anger du den samling som du vill tilldela den här principen för Windows-brandväggen till och anger ett tilldelningsschema. Principen för Windows-brandväggen utvärderas för kompatibilitet med hjälp av det här schemat och Windows-brandväggsinställningarna på klienter som ska konfigureras om för att matcha principen för Windows-brandväggen.  

6.  Klicka på **OK** . Dialogrutan **Distribuera princip för Windows-brandväggen** stängs och principen för Windows-brandväggen distribueras.  

    > [!IMPORTANT]  
    >  När du distribuerar en princip för Windows-brandväggen till en samling tillämpas den här principen på datorer i en slumpmässig ordning under en 2-timmarsperiod för att undvika att belasta nätverket för hårt.
