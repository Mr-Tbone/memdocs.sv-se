---
title: 'Synkronisera uppdateringar utan Internet anslutning '
titleSuffix: Configuration Manager
description: Kör synkronisering av program uppdateringar på den översta program uppdaterings platsen som är frånkopplad från Internet.
ms.date: 02/13/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 1a997c30-8e71-4be5-89ee-41efb2c8d199
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: c2fd85ea9d72e0986f56e24c7ccb66826829079b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710379"
---
# <a name="synchronize-software-updates-from-a-disconnected-software-update-point"></a>Synkronisera programuppdateringar från en frånkopplad plats för programuppdatering  

*Gäller för: Configuration Manager (aktuell gren)*

 Om programuppdateringsplatsen på toppnivåplatsen är frånkopplad från Internet måste du använda export- och importfunktionerna i WSUSUtil-verktyget för att synkronisera programuppdateringarnas metadata. Du kan välja en befintlig WSUS-server som inte finns i din Configuration Manager-hierarki som synkroniserings källa. Den här artikeln innehåller information om hur du använder export-och import funktionerna i WSUSUtil-verktyget.  

 Om du vill exportera programuppdateringsmetadata måste du exportera programuppdateringsmetadata från WSU-databasen på en angiven exportserver, därefter kopiera de lokalt sparade licensvillkorsfilerna till den frånkopplade programuppdateringsplatsen och sedan importera programuppdateringsmetadata till WSUS-databasen på den frånkopplade programuppdateringsplatsen.  

 Använd följande tabell för att identifiera den exportserver som metadata för programuppdateringarna ska exporteras till.  

|Programuppdateringsplats|Överordnad uppdateringskälla för anslutna programuppdateringsplatser|Exportserver för en frånkopplad programuppdateringsplats|  
|---------------------------|-----------------------------------------------------------------|------------------------------------------------------------|  
|Central administrationsplats|Microsoft Update (Internet)<br /><br /> Befintlig WSUS-server|Välj en WSUS-server som är synkroniserad med Microsoft Update med hjälp av program uppdaterings klassificeringar, produkter och språk som du behöver i din Configuration Manager-miljö.|  
|Fristående primär plats|Microsoft Update (Internet)<br /><br /> Befintlig WSUS-server|Välj en WSUS-server som är synkroniserad med Microsoft Update med hjälp av program uppdaterings klassificeringar, produkter och språk som du behöver i din Configuration Manager-miljö.|  

 Innan du startar exportprocessen kontrollerar du att synkroniseringen av programuppdateringarna har slutförts på den valda exportservern för att säkerställa att metadata till de senaste programuppdateringarna har synkroniserats. Om du vill kontrollera att synkroniseringen av programuppdateringen av har slutförts använder du följande procedur.  

#### <a name="to-verify-that-software-updates-synchronization-has-completed-successfully-on-the-export-server"></a>Kontrollera att synkroniseringen av programuppdateringen har slutförts på exportservern  

1.  Öppna WSUS-administrationskonsolen och anslut till WSUS-databasen på exportservern.  

2.  Klicka på **Synkroniseringar**i WSUS-administrationskonsolen. En lista över försök att synkronisera programuppdateringar visas i resultatfönstret.  

3.  Gå till resultatfönstret och leta upp de senaste försöken att synkronisera programuppdateringar och kontrollerar att processen har slutförts.  

> [!IMPORTANT]  
> - WSUSUtil-verktyget måste köras lokalt på exportservern för det ska gå att exportera programuppdateringarnas metadata, och det måste även köras på den frånkopplade programuppdateringsplatsservern för att importera metadata för programuppdateringarna. Dessutom måste den användare som kör verktyget WSUSUtil vara medlem av den lokala administratörsgruppen på varje server.  
> - Om du använder Windows Server 2012 kontrollerar du att [KB2819484](https://support.microsoft.com/help/2819484/cab-file-that-is-exported-by-using-the-wsusutil-exe-command-is-display) är installerat på WSUS-servrarna.

## <a name="export-process-for-software-updates"></a>Exportprocess för programuppdateringar  
 Exportprocessen för programuppdateringar består av två huvudsteg: att kopiera de lokalt sparade licensvillkorsfilerna på den frånkopplade programuppdateringsplatsen och att exportera programuppdateringsmetadata från WSUS-databasen på exportservern.  

 Använd följande procedur för att kopiera metadata för lokala licensvillkor till den frånkopplade programuppdateringsplatsen.  

#### <a name="to-copy-local-files-from-the-export-server-to-the-disconnected-software-update-point-server"></a>Kopiera lokala filer från exportservern till den frånkopplade programuppdateringsplatsservern  

1. Navigera till den mapp på exportservern där programuppdateringarna och licensvillkoren för programuppdateringarna finns sparade. Som standard sparar WSUS-servern filerna på <*WSUSInstallationDrive*>\WSUS\WSUSContent\\, där *WSUSInstallationDrive* är den enhet där WSUS finns installerat.  

2. Kopiera alla filer och mappar från den här platsen till mappen WSUSContent på den frånkopplade programuppdateringsplatsservern.  

   Använd följande procedur för att exportera programuppdateringsmetadata från WSUS-databasen på exportservern.  

#### <a name="to-export-software-updates-metadata-from-the-wsus-database-on-the-export-server"></a>Exportera programuppdateringsmetadata från WSUS-databasen på exportservern  

1.  Vid kommandotolken på exportservern navigerar du till den mapp som innehåller WSUSutil.exe. Som standard finns verktyget under %*ProgramFiles*%\Update Services\Tools. Om verktyget exempelvis finns på standardplatsen skriver du **cd %ProgramFiles%\Update Services\Tools**.  

2.  Skriv följande om du vill exportera programuppdateringsmetadata till en paketfil:  

     **wsusutil.exe export**  *packagename*  *logfile*  
 
     Ett exempel:  

     **WSUSUtil. exe export export. xml. gz export. log**  

     Formatet kan sammanfattas på följande sätt: WSUSutil. exe följs av export alternativet, namnet på filen export. xml. gz som skapas under export åtgärden och namnet på en loggfil. WSUSutil.exe exporterar metadata från exportservern och skapar en loggfil över åtgärden.  

    > [!NOTE]  
    >  Paketet (. xml. gz-filen) och logg fils namnet måste vara unikt i den aktuella mappen.  

3.  Flytta exportpaketet till den mapp som innehåller WSUSutil.exe på WSUS-importservern.  

    > [!NOTE]  
    >  Om du flyttar paketet till den här mappen kan importen underlättas. Du kan flytta paketet till valfri plats som importservern har åtkomst till, och sedan ange platsen när du kör WSUSutil.exe.  

## <a name="import-software-updates-metadata"></a>Importera programuppdateringsmetadata  
 Använd följande procedur om du vill importera programuppdateringsmetadata från exportservern till den frånkopplade programuppdateringsplatsen.  

> [!IMPORTANT]  
>  Importera aldrig några exporterade data från en källa som du inte litar på. Om du importerar innehåll från en källa som du inte litar på kan detta kompromettera säkerheten för din WSUS-server.  

#### <a name="to-import-metadata-to-the-database-of-the-import-server"></a>Importera metadata till importserverns databas  

1.  I kommandotolken på WSUS-importservern navigerar du till den mapp som innehåller WSUSutil.exe. Som standard finns verktyget under %*ProgramFiles*%\Update Services\Tools.  

2.  Skriv in följande:  

     **wsusutil.exe import**  *packagename*  *logfile*  

     Ett exempel:  

     **WSUSUtil. exe import export. xml. gz import. log**  

     Formatet kan sammanfattas på följande sätt: WSUSutil. exe följs av import kommandot, namnet på den paketfil (. xml. gz) som skapas under export åtgärden, sökvägen till paket filen om den finns i en annan mapp och namnet på en loggfil. WSUSutil.exe importerar metadata från exportservern och skapar en loggfil över åtgärden.  

## <a name="next-steps"></a>Nästa steg
När du har synkroniserat program uppdateringar för första gången, eller när det finns nya klassificeringar eller produkter tillgängliga, måste du [Konfigurera de nya klassificeringarna och produkterna](configure-classifications-and-products.md) för att synkronisera program uppdateringar med de nya kriterierna.

När du har synkroniserat program uppdateringar med de villkor som du behöver [hanterar du inställningar för program uppdateringar](manage-settings-for-software-updates.md).   
