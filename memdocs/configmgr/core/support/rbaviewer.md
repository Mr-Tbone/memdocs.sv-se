---
title: Rollbaserad administrations verktyg
titleSuffix: Configuration Manager
description: Använd rollbaserad administration och gransknings verktyg för att modellera och granska säkerhets roller och omfattningar i Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6372ff17-7f56-4d7b-a21b-87fb8bdd6d3a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ff940db21711aabb5d57a45b05d90d04415639bb
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723189"
---
# <a name="role-based-administration-and-auditing-tool"></a>Verktyget för rollbaserad administration och granskning

*Gäller för: Configuration Manager (aktuell gren)*

Det rollbaserade administrations-och gransknings verktyget är ett av de [Configuration Manager verktygen](tools.md). Använd det här verktyget för följande uppgifter:

- Modell säkerhets roller med vissa behörigheter  

- Granska säkerhets omfattningar och säkerhets roller som andra användare har



## <a name="requirements"></a>Krav

- Kör den på samma dator som Configuration Manager-konsolen  

- Du har rollen **Fullständig administratör**, **skrivskyddad analytiker**eller **säkerhets administratör**  

- Tilldela ditt konto till området **alla** säkerhets omfattningar och alla samlingar  

- (*Valfritt*) För att analysera rapportens mappinnehåll måste du ha SQL-åtkomst  

- (*Valfritt*) Om du vill analysera rapporten genom att köra det här verktyget på plats system servern med rapporterings punkt rollen



## <a name="procedures"></a>Procedurer


### <a name="model-permissions-for-a-new-role"></a>Modell behörigheter för en ny roll

Använd följande procedur för att modellera behörigheter för en ny roll som du vill skapa: 

1. Kör **RBAViewer. exe**.  

2. Välj de grundläggande säkerhets roller som du vill skapa på eller starta från en tom behörighets uppsättning. Välj de behörigheter som krävs.  

3. Klicka på **analysera** för att se användar gränssnittet som den här anpassade rollen kommer att se.  

    > [!Note]  
    > Om du vill se om det finns en befintlig säkerhets roll som uppfyller dina krav växlar du till fliken **likhet** .  

4. Klicka på **Exportera** för att spara rollen som en XML-fil. Importera den sedan till Configuration Manager-konsolen. Mer information finns i [skapa anpassade säkerhets roller](../servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole).


### <a name="audit-existing-security-scopes"></a>Granska befintliga säkerhets omfattningar

Använd följande procedur för att granska alla befintliga administrativa användare, samlingar och säkerhets omfattningar i Configuration Manager:

1. Kör **RBAViewer. exe**.  

2. Välj knappen **Granska RBA** i verktygsfältet.  

    1. Om du vill visa Collection-begränsade relationer i en trädvy växlar du till fliken **samlings Sammanfattning** .  

    2. Om du vill visa objekt som har tilldelats en säkerhets roll växlar du till fliken **omfattnings Sammanfattning** .  


### <a name="audit-a-specific-user"></a>Granska en speciell användare

Använd följande procedur för att granska den rollbaserade administrations konfigurationen för en speciell användare:

1. Kör **RBAViewer. exe**.  

2. Välj knappen **Kör som** i verktygsfältet.  

3. Mata in det angivna användar namnet för att kontrol lera behörigheterna för det kontot.  

4. Verktyget visar de säkerhets roller som tilldelats användaren eller den säkerhets grupp användaren tillhör. Den visar också de objekt som den här användaren kan se och de åtgärder som de kan utföra i-konsolen.  



## <a name="see-also"></a>Se även

- [Grunderna i rollbaserad administration](../understand/fundamentals-of-role-based-administration.md)
- [Konfigurera rollbaserad administration](../servers/deploy/configure/configure-role-based-administration.md)
