---
title: Innehållsbibliotek
titleSuffix: Configuration Manager
description: Läs om innehålls biblioteket som Configuration Manager använder för att minska den totala storleken på distribuerat innehåll.
ms.date: 07/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 65c88e54-3574-48b0-a127-9cc914a89dca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 253de522937e48fa1f3939c7303faf7e43e4e047
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720900"
---
# <a name="the-content-library-in-configuration-manager"></a>Innehålls biblioteket i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Innehålls biblioteket är en instans av innehåll i en instans i Configuration Manager. Webbplatsen använder den för att minska den sammanlagda storleken på den kombinerade innehålls innehållet som du distribuerar. Innehålls biblioteket lagrar alla innehållsfiler för program varu distributioner, till exempel: program uppdateringar, program och distributioner av operativ system.  

- Platsen skapar och underhåller automatiskt en kopia av innehålls biblioteket på varje plats Server och varje distributions plats.  

- Innan Configuration Manager lägger till innehållsfiler till plats servern eller kopierar filerna till distributions platser, verifierar den om varje innehålls fil redan finns i innehålls biblioteket.  

- Om innehålls filen är tillgänglig kopieras inte filen Configuration Manager. I stället associeras den befintliga innehålls filen med programmet eller paketet.  

Konfigurera följande alternativ på distributions plats servrar:

- En eller flera disk enheter som du vill skapa innehålls biblioteket på.  

- En prioritet för varje enhet som du använder.  

Configuration Manager kopierar innehållsfilerna till den enhet som har högst prioritet tills enheten innehåller mindre än den minsta mängd ledigt utrymme som du anger.  

- Du konfigurerar enhets inställningarna under installationen av distributions platsen.  

- Du kan inte konfigurera enhets inställningarna i egenskaperna för distributions platsen när installationen är slutförd.  

Mer information om hur du konfigurerar enhets inställningarna för distributions platsen finns i [Hantera innehåll och innehålls infrastruktur](../../servers/deploy/configure/manage-content-and-content-infrastructure.md).  

> [!IMPORTANT]
> Om du vill flytta innehålls biblioteket till en annan plats på en distributions plats efter installationen använder du verktyget för **överföring av innehålls bibliotek** i Configuration Manager verktyg. Mer information finns i [överförings verktyget för innehålls bibliotek](../../support/content-library-transfer.md).  


## <a name="about-the-content-library-on-the-central-administration-site"></a>Om innehålls biblioteket på den centrala administrations webbplatsen

Som standard skapar Configuration Manager ett innehålls bibliotek på den centrala administrations platsen när platsen installeras. Innehålls biblioteket placeras på enheten på den plats server som har mest ledigt disk utrymme. Eftersom du inte kan installera en distributions plats på den centrala administrations platsen kan du inte prioritera enheterna som ska användas av innehålls biblioteket. I likhet med innehålls biblioteket på andra plats servrar och distributions platser, och om den enhet som innehåller innehålls biblioteket tar slut på ledigt disk utrymme, sträcker sig innehålls biblioteket automatiskt till nästa tillgängliga enhet.  

Configuration Manager använder innehålls biblioteket på den centrala administrations webbplatsen i följande scenarier:  

- Du skapar innehåll på den centrala administrations webbplatsen  

- Du migrerar innehåll från en annan Configuration Manager webbplats och tilldelar den centrala administrations platsen som den plats som hanterar innehållet  

> [!NOTE]  
> När du skapar innehåll på en primär plats och sedan distribuerar det till en annan primär plats eller en sekundär plats under en annan primär plats, kommer den centrala administrations platsen tillfälligt att lagra innehållet i Inkorgen i Schemaläggaren på den centrala administrations platsen men inte lägga till innehållet i dess innehålls bibliotek.  

Använd följande alternativ för att hantera innehålls biblioteket på den centrala administrations webbplatsen:  

- Om du vill förhindra att innehålls biblioteket installeras på en speciell enhet skapar du en tom fil med namnet **No_sms_on_drive. SMS**. Kopiera den till enhetens rot innan innehålls biblioteket skapas.  

- När innehålls biblioteket har skapats använder du verktyget för **överföring av innehålls bibliotek** från Configuration Manager-verktyg för att hantera innehålls bibliotekets placering. Mer information finns i [överförings verktyget för innehålls bibliotek](../../support/content-library-transfer.md).  

> [!Note]  
> Moln distributions platser använder inte lagring med en instans. Platsen krypterar paket innan de skickas till Azure och varje paket har en unik krypterad nyckel. Även om två filer var identiska, skulle de krypterade versionerna inte vara identiska.  


## <a name="configure-a-remote-content-library-for-the-site-server"></a><a name="bkmk_remote"></a>Konfigurera ett fjärrinnehålls bibliotek för plats servern

<!--1357525-->
Från och med version 1806 kan du flytta innehålls biblioteket till en annan lagrings plats om du vill konfigurera en [hög tillgänglighet för plats servern](../../servers/deploy/configure/site-server-high-availability.md) eller frigöra hårddisk utrymme på den centrala administrations servern eller den primära plats servern. Flytta innehålls biblioteket till en annan enhet på plats servern, en separat server eller feltoleranta diskar i en storage area network (SAN). Ett SAN rekommenderas, eftersom det har hög tillgänglighet och ger elastisk lagring som växer eller minskar med tiden för att möta dina föränderliga innehålls krav. Mer information finns i [alternativ för hög tillgänglighet](../../servers/deploy/configure/site-server-high-availability.md).

Ett fjärran slutet innehålls bibliotek är ett krav för att [plats servern ska ha hög tillgänglighet](../../servers/deploy/configure/site-server-high-availability.md).

> [!Note]  
> Den här åtgärden flyttar bara innehålls biblioteket på plats servern. Innehålls bibliotekets placering påverkas inte av distributions platserna. 

> [!Tip]  
> Planera även hantering av paket käll innehåll, som är externt i innehålls biblioteket. Alla program varu objekt i Configuration Manager har en paket källa på en nätverks resurs. Överväg att centralisera alla källor till en enda resurs, men se till att platsen är redundant och hög tillgänglig.
>
> Om du flyttar innehålls biblioteket till samma lagrings volym som paket källorna kan du inte markera den här volymen för datadeduplicering. Innehålls biblioteket stöder datadeduplicering, men paketets käll volym stöder den inte. Mer information finns i [datadeduplicering](../configs/support-for-windows-features-and-networks.md#bkmmk_datadedup).<!--SCCMDOcs issue #831-->  

### <a name="prerequisites"></a>Krav  

- Plats serverns dator konto måste ha **fullständig** behörighet till nätverks Sök vägen som du flyttar innehålls biblioteket till. Den här behörigheten gäller både resursen och fil systemet. Inga komponenter är installerade på fjärrdatorn.

- Plats servern kan inte ha distributions plats rollen. Innehålls biblioteket används också av distributions platsen, och den här rollen stöder inte ett innehålls bibliotek för fjärrnätverk. När du har flyttat innehålls biblioteket kan du inte lägga till distributions plats rollen på plats servern.  

> [!Important]  
> Återanvänd inte en delad nätverks plats mellan flera platser. Använd exempelvis inte samma sökväg för både en central administrations plats och en underordnad primär plats. Den här konfigurationen kan skada innehålls biblioteket och kräver att du bygger om den.<!--SCCMDocs-pr issue 2764-->  

### <a name="process-to-manage-the-content-library"></a>Process för att hantera innehålls biblioteket

1. Skapa en mapp i en nätverks resurs som mål för innehålls biblioteket. Till exempel `\\server\share\folder`.  

    > [!Warning]  
    > Återanvänd inte en befintlig mapp med innehåll. Använd exempelvis inte samma mapp som paket källorna. Innan du kopierar innehålls biblioteket, Configuration Manager tar bort befintligt innehåll från den plats du anger.  

2. Växla till arbets ytan **Administration** i Configuration Manager-konsolen. Expandera **plats konfiguration**, välj noden **platser** och välj platsen. Lägg märke till en ny kolumn för **innehålls biblioteket**på fliken **Sammanfattning** längst ned i informations fönstret.  

3. Välj **Hantera innehålls bibliotek** i menyfliksområdet.  

4. I fönstret Hantera innehålls bibliotek visas den lokala enheten och sökvägen i fältet **aktuell plats** . Ange en giltig nätverks Sök väg för den **nya platsen**. Den här sökvägen är den plats där platsen flyttar innehålls biblioteket. Det måste innehålla ett mappnamn som redan finns på resursen, till exempel `\\server\share\folder`. Välj **OK**.  

5. Observera värdet **status** i kolumnen innehålls bibliotek på fliken Sammanfattning i informations fönstret. Den uppdaterar för att visa platsens förlopp när innehålls biblioteket flyttas.  

   - När det **pågår**, visar **flytt förloppet (%)** procent klart.  

        > [!Note]  
        > Om du har ett stort innehålls bibliotek kan du se `0%` förloppet i-konsolen en stund. Med ett bibliotek på 1 TB måste du till exempel kopiera 10 GB innan det visas `1%`. Granska **Distmgr. log**, som visar hur många filer och byte som har kopierats. Från och med version 1810 visar logg filen även en beräknad återstående tid.

   - Om det finns ett fel tillstånd visas felet i status. Vanliga fel är **åtkomst nekad** eller **disk full**.  

   - När du är klar visas **Slutför**.  

     Mer information finns i **Distmgr. log** . Mer information finns i [loggarna plats Server och plats system Server](log-files.md#BKMK_SiteSiteServerLog).  

Mer information om den här processen finns i [flödesschema – hantera innehålls bibliotek](manage-content-library-flowchart.md).

Webbplatsen *kopierar* innehålls bibliotekets filer till fjärrplatsen. Den här processen tar inte bort filerna för innehålls bibliotek på den ursprungliga platsen på plats servern. För att frigöra utrymme måste en administratör manuellt ta bort de ursprungliga filerna.

Om det ursprungliga innehålls biblioteket sträcker sig över två enheter, slås det samman i en enda mapp på det nya målet.

Från och med version 1810, under kopierings processen, bearbetar inte komponenterna för **despooler** -och **distributions hanteraren** nya paket. Den här åtgärden ser till att innehållet inte läggs till i biblioteket när det flyttas. Oavsett vilket schemalägger du den här ändringen under ett system underhåll.

Om du behöver flytta innehålls biblioteket tillbaka till plats servern upprepar du den här processen, men anger en lokal enhet och en sökväg för den **nya platsen**. Det måste innehålla ett mappnamn som redan finns på enheten, till exempel `D:\SCCMContentLib`. När det ursprungliga innehållet fortfarande finns flyttar processen snabbt konfigurationen till plats serverns lokala plats.

> [!Tip]  
> Om du vill flytta innehållet till en annan enhet på plats servern använder du verktyget för **överföring av innehålls bibliotek** . Mer information finns i [överförings verktyget för innehålls bibliotek](../../support/content-library-transfer.md).  


## <a name="inside-the-content-library"></a>Inuti innehålls biblioteket

> [!Warning]  
> Följande avsnitt tillhandahålls endast i informations syfte. Ändra inte, Lägg till eller ta bort några filer eller mappar i innehålls biblioteket. Om du gör det kan du skada paket, innehåll eller innehålls biblioteket som helhet. Om du misstänker att data som saknas, är skadade eller på annat sätt är ogiltiga använder du verifierings funktionen i Configuration Manager-konsolen för att upptäcka sådana problem. Distribuera sedan om det påverkade innehållet för att åtgärda problemen.

Som standard lagras innehålls biblioteket i roten på en enhet i en mapp med namnet **SCCMContentLib**. Den här mappen delas som standard som **SCCMContentLib $**. Mappen och resursen har begränsad behörighet för att förhindra oavsiktlig skada. Alla ändringar ska göras från Configuration Manager-konsolen. I den här mappen finns följande objekt:  

- Paket biblioteket (**PkgLib** -mappen): information om vilka paket som finns på distributions platsen.  

- Data biblioteket (**DataLib** -mapp): information om den ursprungliga strukturen i paketen.  

- Fil biblioteket (**FileLib** -mappen): de ursprungliga filerna i paketet. Den här mappen är vanligt vis vad som använder lagrings utrymmet.  

![Diagram översikt över Configuration Manager innehålls bibliotek](media/content-library-overview.png)

> [!Tip]  
> Använd verktyget **innehålls biblioteks Utforskaren** från Configuration Manager-verktyg för att bläddra i innehålls bibliotekets innehåll. Du kan inte använda det här verktyget för att ändra innehållet. Den ger inblick i vad som finns tillgängligt, samt för att tillåta validering och omdistribution. Mer information finns i [innehålls biblioteks Utforskaren](../../support/content-library-explorer.md).  

### <a name="package-library"></a>Paket bibliotek

Mappen paket bibliotek, **PkgLib**, innehåller en fil för varje paket som distribueras till distributions platsen. Fil namnet är paket-ID: t, till exempel `ABC00001.INI`. I den här filen under `[Packages]` avsnittet finns en lista med innehålls-id: n som ingår i paketet, samt annan information som version. Till exempel är **ABC00001** ett äldre paket vid version **1**. Innehålls-ID: t i den `ABC00001.1`här filen är.

### <a name="data-library"></a>Data bibliotek

Mappen data bibliotek, **DataLib**, innehåller en fil och en mapp för varje pakets innehåll. Till exempel heter `ABC00001.1.INI` `ABC00001.1`filen och mappen respektive. Filen innehåller information som ska verifieras. Mappen återskapar mappstrukturen från det ursprungliga paketet.

Filerna i data biblioteket ersätts av INI-filer med namnet på den ursprungliga filen i paketet. Till exempel `MyFile.exe.INI`. De här filerna innehåller information om original filen, till exempel storlek, tid ändrad och hash. Använd de första fyra tecknen i hashen för att hitta den ursprungliga filen i fil biblioteket. Till exempel är hash i filen. exe. INI **DEF98765**och de första fyra tecknen är **DEF9**.

### <a name="file-library"></a>Fil bibliotek

Om innehålls biblioteket sträcker sig över flera enheter, kan paketfilerna finnas i mappen fil bibliotek, **FileLib**, på någon av dessa enheter.

Hitta en speciell fil med de första fyra tecknen från den hash som finns i data biblioteket. I mappen fil bibliotek finns många mappar, var och en med ett namn på fyra bokstäver. Hitta mappen som matchar de första fyra tecknen från hashen. När du har hittat den här mappen innehåller den en eller flera uppsättningar av tre filer. Dessa filer delar samma namn, men en har fil namns tillägget INI, en har tillägget SIG, och en har inget fil namns tillägg. Den ursprungliga filen är den som inte har något tillägg, vars namn är lika med hash-värdet från data biblioteket.

Till exempel mapp **DEF9** innehåller `DEF98765.INI`, `DEF98765.SIG`och. `DEF98765` `DEF98765`är originalet `MyFile.exe`. INI-filen innehåller en lista över "användare" eller innehålls-id: n som delar samma fil. Platsen tar inte bort en fil om inte allt innehåll också tas bort.

### <a name="drive-spanning"></a>Enhets utsträckning

Innehålls biblioteket kan sträckas ut över flera enheter. Du väljer dessa enheter när du skapar distributions platsen. Som standard väljer Configuration Manager automatiskt enheterna när de spänner över innehålls biblioteket.

När du väljer enheter väljer du en primär och en sekundär enhet. Platsen lagrar alla metadata på den primära enheten. Den sträcker sig bara över fil biblioteket till den sekundära enheten. Mappens resurs namn för sekundära enheter omfattar enhets beteckningen. Om t. ex. D: och E: är sekundära enheter för innehålls biblioteket, är resurs namnen **SCCMContentLibD $** och **SCCMContentLibE $**.

Om du väljer alternativet **Automatisk** , Configuration Manager väljer enheten med mest tillgängligt ledigt utrymme som primär enhet. Den lagrar alla metadata på den här enheten. Platsen sträcker sig bara över fil biblioteket till sekundära enheter.

Du anger ett reserv utrymmes belopp under konfigurationen. Configuration Manager försöker använda en sekundär disk när den bästa tillgängliga disken bara har den här reserv utrymmes mängden kvar utan kostnad. Varje gång en ny enhet väljs för användning väljs enheten med mest tillgängligt ledigt utrymme.

Du kan inte ange att en distributions plats ska använda alla enheter, förutom en viss uppsättning. Förhindra det här problemet genom att skapa en tom fil i roten på enheten, som `NO_SMS_ON_DRIVE.SMS`kallas. Placera den här filen innan Configuration Manager väljer enheten för användning. Om Configuration Manager identifierar filen i enhetens rot använder den inte enheten för innehålls biblioteket.


## <a name="troubleshooting"></a>Felsökning

Följande tips kan hjälpa dig att felsöka problem med innehålls biblioteket:  

- Granska loggarna på plats servern (**Distmgr. log** och **PkgXferMgr. log**) och distributions platsen (**Smsdpprov. log**) för alla pekare till felen.  

- Använd verktyget [innehålls biblioteks Utforskaren](../../support/content-library-explorer.md) .  

- Sök efter fillås av andra processer, till exempel antivirus program. Undanta innehålls biblioteket på alla enheter från automatiska Antivirus genomsökningar, samt den tillfälliga uppsamlings katalogen **SMS_DP $**, på varje enhet.  

- Om du vill se om det finns någon hash-matchning, verifierar du paketet från Configuration Manager-konsolen.  

- Det sista alternativet är att distribuera om innehållet. Den här åtgärden bör lösa de flesta problem.  
