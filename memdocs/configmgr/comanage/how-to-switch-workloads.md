---
title: Växla mellan hanterings arbets belastningar
titleSuffix: Configuration Manager
description: Lär dig hur du växlar arbets belastningar som för närvarande hanteras av Configuration Manager att Microsoft Intune.
ms.prod: configuration-manager
ms.technology: configmgr-comanage
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 09/06/2019
ms.topic: how-to
ms.assetid: 60e2022f-a4f9-40dd-af01-9ecb37b43878
ms.openlocfilehash: 88c8b34437ba52e700ef97885aafed40734a0f32
ms.sourcegitcommit: 7b2f7918d517005850031f30e705e5a512959c3d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/15/2020
ms.locfileid: "84776964"
---
# <a name="how-to-switch-configuration-manager-workloads-to-intune"></a>Så här växlar du Configuration Manager-arbetsbelastningar till Intune

En av fördelarna med samtidig hantering är att byta arbets belastningar från Configuration Manager till Microsoft Intune. När en Windows 10-enhet har Configuration Manager-klienten och har registrerats i Intune får du fördelarna med båda tjänsterna. Du kan kontrol lera vilka arbets belastningar, om du vill, byta utfärdare från Configuration Manager till Intune. Configuration Manager fortsätter att hantera alla andra arbets belastningar, inklusive de arbets belastningar som du inte växlar till Intune, och alla andra funktioner i Configuration Manager den samhanteringen inte stöder.

Om du växlar en arbets belastning till Intune, men ändrar dig senare, kan du växla tillbaka till Configuration Manager.

Mer information om de arbets belastningar som stöds finns i [arbets belastningar](workloads.md).

## <a name="switch-workloads-starting-in-version-1906"></a>Växla arbets belastningar från och med version 1906
<!--3555750 FKA 1357954 -->
Från och med version 1906 kan du konfigurera olika pilot samlingar för var och en av arbets belastningarna för samtidig hantering. Genom att använda olika pilot samlingar kan du ta en mer detaljerad metod när du byter arbets belastningar. Du kan byta arbets belastning när du aktiverar samhantering eller senare när du är klar. Om du inte redan har aktiverat samhantering gör du det först. Mer information finns i [så här aktiverar du samhantering](how-to-enable.md). När du har aktiverat samhantering ändrar du inställningarna i egenskaperna för samhantering.

1. I Configuration Manager-konsolen går du till arbets ytan **Administration** , expanderar **Cloud Services**och väljer noden för **samtidig hantering** .  
2. Välj objektet för samtidig hantering och välj sedan **Egenskaper** i menyfliksområdet.  
3. Växla till fliken **arbets belastningar** . Som standard anges alla arbets belastningar till inställningen **Configuration Manager** . Om du vill växla en arbets belastning flyttar du skjutreglaget för arbets belastningen till önskad inställning.  

    ![Skärm bild av fliken arbets belastningar på sidan Egenskaper för samhantering](media/3555750-co-management-workloads-tab.png)

    - **Configuration Manager**: Configuration Manager fortsätter att hantera arbets belastningen.  

    - **Pilot Intune**: Byt endast den här arbets belastningen för enheterna i pilot samlingen. Du kan ändra **pilot samlingarna** på fliken **mellanlagring** på sidan Egenskaper för samhantering.  

    - **Intune**: växla den här arbets belastningen för alla Windows 10-enheter som har registrerats i samhantering.  

4. Gå till fliken **mellanlagring** och ändra **pilot samlingen** för någon av arbets belastningarna om det behövs.
  
   ![Skärm bild av fliken arbets belastningar på sidan Egenskaper för samhantering](media/3555750-co-management-staging-tab.png)

> [!Important]  
> - Innan du växlar över arbets belastningar måste du kontrol lera att du har konfigurerat och distribuerat motsvarande arbets belastning i Intune. Se till att arbets belastningarna alltid hanteras av ett av hanterings verktygen för dina enheter.
> - Från och med Configuration Manager version 1806, när du växlar en samhanterings arbets belastning, synkroniserar de samhanterade enheterna automatiskt MDM-principen från Microsoft Intune. Den här synkroniseringen inträffar även när du startar åtgärden **Ladda ned dator princip** från klient meddelanden i Configuration Manager-konsolen. Mer information finns i [Starta klient princip hämtning med hjälp av klient meddelanden](../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval). <!--1357377-->

## <a name="switch-workloads-in-version-1902-and-earlier"></a>Växla arbets belastningar i version 1902 och tidigare

Du kan byta arbets belastning när du aktiverar samhantering eller senare när du är klar. Om du inte redan har aktiverat samhantering gör du det först. Mer information finns i [så här aktiverar du samhantering](how-to-enable.md). När du har aktiverat samhantering ändrar du inställningarna i egenskaperna för samhantering.

1. I Configuration Manager-konsolen går du till arbets ytan **Administration** , expanderar **Cloud Services**och väljer noden för **samtidig hantering** .  

2. Välj objektet för samtidig hantering och välj sedan **Egenskaper** i menyfliksområdet.
   - Du uppmanas att logga in på Azure AD. Frågan hindrar dig inte från att uppdatera din onboarding. Du får dock en fråga varje gången du öppnar **egenskaps** sidan tills du har loggat in.

3. Växla till fliken **arbets belastningar** . Som standard anges alla arbets belastningar till inställningen **Configuration Manager** . Om du vill växla en arbets belastning flyttar du skjutreglaget för arbets belastningen till önskad inställning.  

    ![Skärm bild av fliken arbets belastningar på sidan Egenskaper för samhantering](media/properties-workloads.png)

    - **Configuration Manager**: Configuration Manager fortsätter att hantera arbets belastningen.  

    - **Pilot Intune**: Byt endast den här arbets belastningen för enheterna i pilot samlingen. Du kan ändra **pilot samlingen** på fliken **mellanlagring** på sidan Egenskaper för samhantering.  

    - **Intune**: växla den här arbets belastningen för alla Windows 10-enheter som har registrerats i samhantering.  

4. På fliken **mellanlagring** på sidan Egenskaper för samhantering ändrar du **pilot samlingen** för dina arbets belastningar om det behövs.

5. Klicka på **OK** för att spara och avsluta egenskaper för samhantering.

> [!Important]  
> - Innan du växlar över arbets belastningar måste du kontrol lera att du har konfigurerat och distribuerat motsvarande arbets belastning i Intune. Se till att arbets belastningarna alltid hanteras av ett av hanterings verktygen för dina enheter. 
> - Från och med Configuration Manager version 1806, när du växlar en samhanterings arbets belastning, synkroniserar de samhanterade enheterna automatiskt MDM-principen från Microsoft Intune. Den här synkroniseringen inträffar även när du startar åtgärden **Ladda ned dator princip** från klient meddelanden i Configuration Manager-konsolen. Mer information finns i [Starta klient princip hämtning med hjälp av klient meddelanden](../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval). <!--1357377-->

## <a name="next-steps"></a>Nästa steg

[Övervaka samhantering](how-to-monitor.md)
