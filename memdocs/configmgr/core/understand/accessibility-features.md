---
title: Tillgänglighet
titleSuffix: Configuration Manager
description: Lär dig mer om de funktioner som gör Configuration Manager tillgängliga för alla.
ms.date: 05/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1cb96666-98bf-49a9-85ca-dbb53f0655e9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: a6e406d55524caca71bf75b087c9fd78a470c939
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699389"
---
# <a name="accessibility-features-in-configuration-manager"></a>Hjälpmedels funktioner i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*


Configuration Manager innehåller funktioner som hjälper dig att göra den tillgänglig för alla.

> [!Note]  
> Från och med version 1902 kan du uppdatera .NET till version 4,7 eller senare på datorn som kör-konsolen för att förbättra hjälpmedels funktionerna i Configuration Manager-konsolen. <!-- SCCMDocs-pr issue #3228 -->  
> 
> Mer information om de hjälpmedels ändringar som görs i .NET-4.7.1 och 4.7.2 finns i [Nyheter i hjälpmedel i .NET Framework](/dotnet/framework/whats-new/whats-new-in-accessibility).  



## <a name="keyboard-shortcuts"></a>Kortkommandon

### <a name="console-workspaces"></a>Konsol arbets ytor

Använd följande kortkommandon för att få åtkomst till en arbets yta:  

|Kortkommando| Arbetsyta|
|--------|--------|  
|Ctrl + 1| Till gångar och efterlevnad|
|CTRL + 2|  Program varu bibliotek|
|Ctrl + 3|  Övervakning|
|CTRL + 4|  Administration|


### <a name="other-console-shortcuts"></a>Andra konsol gen vägar

|Kortkommando|  Syfte|
|--------|--------|  
|Ctrl + M|Ange fokus i huvud fönstret (Central).|
|Ctrl + T|Ange fokus till den översta noden i navigerings fönstret. Om fokus redan finns i fönstret är fokus inställt på den sista noden som du besökte.|
|Ctrl + I|Ange fokus till fältet för dynamiska länkar under menyfliksområdet.|
|CTRL + L|Ange fokus till **Sök** fältet när det är tillgängligt.|
|CTRL + D|Ange fokus till informations fönstret när det är tillgängligt.|
|Alt     |Ändra fokus till och från menyfliksområdet.|

### <a name="cmpivot-shortcuts"></a><a name="bkmk_cmpshortcuts"></a> CMPivot-genvägar

De flesta kortkommandona för [webb läsar tangenter](https://support.microsoft.com/help/17456/windows-internet-explorer-ease-of-access-options) kommer att fungera i CMPivot.

|Kortkommando|Syfte|
|--------|--------|  
|Ctrl + 1|Ange fokus på den första fliken.|
|Alt + &lt;|Tillbaka till adressen|


## <a name="other-accessibility-features"></a>Andra hjälpmedels funktioner

- Om du vill navigera i navigerings fönstret anger du bokstäverna för ett nodnamn.

- Tangent bords navigering i huvudvyn och menyfliksområdet är cirkulärt.

- Tangent bords navigering i informations fönstret är cirkulär. Om du vill återgå till föregående objekt eller fönster, använder du Ctrl + D och sedan Shift + TABB.

- När du har uppdaterat vyn arbets yta är fokus inställt på arbets ytans huvud fönster.

- Om du vill komma åt en arbets yta-meny väljer du tabbtangenten tills ikonen Expandera/komprimera är i fokus. Välj sedan nedåtpilen för att komma åt menyn för arbets ytan.  

- Använd piltangenterna för att navigera i en arbets yta-meny.  

- Om du vill komma åt olika områden i arbets ytan använder du TABB-tangenten och SKIFT + TABB-tangenterna. Använd piltangenterna för att navigera inom ett område i arbets ytan, till exempel menyfliksområdet.  

- Använd Shift + TABB tre gånger för att få åtkomst till adress fältet när du är i fokus på trädnoden.  

- I en guide eller egenskaps sida kan du växla mellan rutorna med kortkommandon. Välj alternativ tangenten plus det understrukna tecknet (Alt + _) för att markera en ruta.     

- För att navigera till de olika noderna i en arbets yta, anger du den första bokstaven i namnet på en nod. Varje tangenttryckning flyttar markören till nästa nod som börjar med den bokstaven. När du använder en skärm läsare läser läsaren ut namnet på den noden.



## <a name="see-also"></a>Se även

Mer information om grunderna i hur du navigerar Configuration Manager användar gränssnitt finns i följande artiklar:
- [Använda Configuration Manager-konsolen](../servers/manage/admin-console.md)
- [Användarhandbok för Software Center](software-center.md)

> [!NOTE]  
> Informationen i den här artikeln kan endast gälla användare som har licens för Microsoft-produkter i USA. Om du har köpt den här produkten utanför USA kan du använda informations kortet för dotter bolag som medföljde ditt program varu paket eller besöka [webbplatsen Microsoft Accessibility](https://www.microsoft.com/accessibility/) för kontakt information för Microsoft Support Services. Du kan kontakta ditt dotter bolag för att ta reda på om den typ av produkter och tjänster som beskrivs i det här avsnittet är tillgängliga i ditt område. Informationen om hjälpmedelsfunktioner är tillgänglig på andra språk, däribland japanska och franska.