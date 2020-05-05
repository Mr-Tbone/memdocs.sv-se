---
title: Kommando rads installation
titleSuffix: Configuration Manager
description: Lär dig hur du kör Configuration Manager-installationen i en kommando tolk för en rad olika plats installationer.
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e7cdb1a9-140a-436e-ac71-72d083110223
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c46e7f4dde0fb4719daf0f5c1f1293f627063f2a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717960"
---
# <a name="use-a-command-line-to-install-configuration-manager-sites"></a>Använda en kommando rad för att installera Configuration Manager-platser

*Gäller för: Configuration Manager (aktuell gren)*

 Du kan köra installations programmet för Configuration Manager vid en kommando tolk för att installera en rad olika plats typer.

## <a name="supported-tasks-for-command-line-installations"></a>Åtgärder som stöds för kommando rads installationer
 Den här metoden för att köra installations programmet har stöd för följande plats-och plats underhålls aktiviteter:

- **Installera en central administrations plats eller en primär plats från en kommando tolk**  
  Visa [kommando rads alternativ för installation](../../../../core/servers/deploy/install/command-line-options-for-setup.md)

- **Ändra de språk som används på en central administrations plats eller en primär plats**  
   Om du vill ändra de språk som installeras på en plats från en kommando tolk (inklusive språk för mobila enheter) måste du:  

  - Kör installations programmet ** &lt;från\>ConfigMgrInstallationPath \BIN\X64** på plats servern,
  - Använd kommando rads alternativet **/MANAGELANGS**
  - Ange en språk skript fil som anger de språk som du vill lägga till eller ta bort.  

    Använd till exempel följande Kommandosyntax: **setupwpf. exe/MANAGELANGS &lt;Language Script File\> **  

    Skapa språk skript filen genom att använda informationen i [kommando rads alternativ för att hantera språk](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Lang)  

- **Använd en installationsskriptfil för obevakad platsinstallation eller webbplatsåterställning**  
   Du kan köra installations programmet från en kommando tolk genom att använda ett installations skript och köra en obevakad plats installation. Du kan också använda det här alternativet för att återställa en plats.    

   Använda ett skript med installations programmet:  

  - Kör installations programmet med kommando rads alternativet **/script** och ange en skript fil.  

  - Skript filen måste konfigureras med obligatoriska nycklar och värden.  

    För en obevakad installation av en central administrations plats eller primär plats måste skript filen ha följande avsnitt:  

  - Identification    
  - Alternativ    
  - SQLConfigOptions    
    -   HierarchyOptions    
  - CloudConnectorOptions   

    Om du vill återställa en plats måste du även inkludera följande delar av skript filen:  

  - Identification  
  - Återställning

Mer information finns i [obevakad webbplats återställning för Configuration Manager](../../manage/unattended-recovery.md).  

En lista över nycklar och värden som ska användas i en obevakad installations skript fil finns i [skript fil nycklar för obevakad](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Unattended)installation.  

## <a name="about-the-command-line-script-file"></a>Om kommando rads skript filen  
 För obevakade installationer av Configuration Manager kan du köra installations programmet med kommando rads alternativet **/script**och ange en skript fil som innehåller installations alternativ. Följande åtgärder stöds med den här metoden:  

-   Installera en central administrations plats  
-   Installera en primär plats  
-   Installera en Configuration Manager-konsol  
-   Återställa en plats  

> [!NOTE]  
>  Du kan inte använda den obevakade skript filen för att uppgradera en utvärderings plats till en licensierad installation av Configuration Manager.  

### <a name="the-cdlatest-key-name"></a>CDLatest nyckel namn
När du använder media från CD: n. Senaste mappen om du vill köra en skriptad installation av följande fyra installations alternativ måste skriptet innehålla **CDLatest** -nyckeln med värdet **1**:
- Installera en ny central administrations webbplats
- Installera en ny primär plats
- Återställa en central administrations plats
- Återställa en primär plats

Det här värdet stöds inte för användning med installationsmedia som du får från Microsoft volym licens webbplatsen.
Se [kommando rads alternativ](command-line-options-for-setup.md) för information om hur du använder det här nyckel namnet i skript filen.



### <a name="create-the-script"></a>Skapa skriptet
Installations skriptet skapas automatiskt när du [Kör installations programmet för att installera en plats med hjälp av användar gränssnittet](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md).  När du bekräftar inställningarna på sidan **Sammanfattning** i guiden händer följande:  

-   Installations programmet skapar skriptet **%Temp%\ConfigMgrAutoSave.ini**.  Du kan byta namn på den här filen innan du använder den, men den måste innehålla fil namns tillägget. ini.  
-   Skriptet för obevakad installation innehåller de inställningar som du valde i guiden.  
-   När skriptet har skapats kan du ändra skriptet så att det installerar andra platser i hierarkin.  
-   Du kan sedan använda det här skriptet för att utföra en obevakad installation av Configuration Manager.  

Den här skript filen innehåller samma information som installations guiden efterfrågar, förutom att det inte finns några standardinställningar.   
Du måste ange alla värden för de installations nycklar som gäller för den typ av installation du använder.   

När installations skriptet för obevakad installation skapas, fylls det i med det produkt nyckel värde som du anger under installationen. Detta kan vara en giltig produkt nyckel, eller en **utvärderings** version när du installerar en utvärderings version av Configuration Manager. Produkt nyckel svärdet i skriptet fylls i så att krav kontrollen kan slutföras.   

När installations programmet startar den faktiska plats installationen skrivs det automatiskt skapade skriptet till igen för att ta bort värdet för produkt nyckeln i skriptet som det skapar. Innan du använder skriptet för en obevakad installation av en ny plats kan du redigera skriptet för att ange en giltig produkt nyckel eller ange en utvärderings installation av Configuration Manager.  

### <a name="section-names-key-names-and-values"></a>Avsnitts namn, nyckel namn och värden
Skriptet innehåller avsnittsnamnen, nyckelnamn och värden. Notera följande information:
-   Nödvändiga avsnitts nyckel namn varierar beroende på vilken Installations typ som du använder skript för.
-   Ordningen på nycklarna i avsnitten och ordningen på avsnitten i filen är inte viktig.     
-   Nycklarna är inte Skift läges känsliga.  
-   När du anger värden för nycklar måste namnet på nyckeln följas av ett likhets tecken (=) och värdet för nyckeln.    

> [!TIP]  
>  Om du vill visa en fullständig uppsättning alternativ, se [kommando rads alternativ för installation och skript](../../../../core/servers/deploy/install/command-line-options-for-setup.md).  

## <a name="use-the-script-setup-command-line-option"></a>Använd kommando rads alternativet/SCRIPT setup

-   Du måste använda en installations skript fil och ange fil namnet efter kommando rads alternativet **/script** setup. Notera följande information:   
    -   Namnet på filen måste ha fil namns tillägget **. ini** .  
    -   När du refererar till installations skript filen i kommando tolken måste du ange den fullständiga sökvägen till filen. Om installations initierings filen till exempel heter setup. ini och lagras i mappen C:\Setup i kommando tolken skriver du: **Setup/Script c:\setup\setup.ini**.  

-   Kontot som kör installations programmet måste ha **Administratörs** behörighet på datorn. När du kör installations programmet med det obevakade skriptet öppnar du kommando tolkens fönster med alternativet **Kör som administratör** .   
