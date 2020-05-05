---
title: Funktioner i Technical Preview 1612
titleSuffix: Configuration Manager
description: Lär dig mer om funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1612.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bceab2e8-2f05-4a17-9ac8-a7a558670fb7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 0c2464bfba05d640868af7d5c8be7c32c0999946
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721509"
---
# <a name="capabilities-in-technical-preview-1612-for-configuration-manager"></a>Funktioner i Technical Preview 1612 för Configuration Manager

*Gäller för: Configuration Manager (Technical Preview Branch)*



Den här artikeln beskriver de funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1612. Du kan installera den här versionen för att uppdatera och lägga till nya funktioner till din Configuration Manager Technical Preview-webbplats. Innan du installerar den här versionen av Technical Preview kan du läsa introduktions avsnittet, [teknisk för hands version för Configuration Manager](../../core/get-started/technical-preview.md), för att bekanta dig med allmänna krav och begränsningar för att använda en teknisk för hands version, hur du uppdaterar mellan versioner och hur du ger feedback om funktionerna i en teknisk för hands version.    


**Följande är nya funktioner som du kan prova med den här versionen.**  

## <a name="the-data-warehouse-service-point"></a>Informations lager service punkten
Från och med den tekniska för hands versionen av version 1612 kan du lagra och rapportera långsiktiga historiska data för din Configuration Manager-distribution i informations lager service punkten. Detta görs genom automatiska synkroniseringar från Configuration Manager plats databasen till en informations lager databas. Den här informationen är sedan tillgänglig från repor ting Services-platsen.

Som standard när du installerar den nya plats system rollen skapar Configuration Manager informations lager databasen åt dig på en SQL Server instans som du anger. Informations lagret har stöd för upp till 2 TB data, med tidsstämplar för ändrings spårning.  Som standard innehåller data som synkroniseras från plats databasen data grupper för globala data, plats data, Global_Proxy, moln data och databasvyer. Du kan också ändra vad som ska synkroniseras för att inkludera ytterligare tabeller eller undanta vissa tabeller från standardreplikerings uppsättningarna.
Standard data som synkroniseras innehåller information om:
- Infrastruktur hälsa
- Säkerhet
- Efterlevnad
- Skadlig kod   
- Programdistributioner
- Inventerings information (men inventerings historiken synkroniseras inte)

Förutom att installera och konfigurera informations lager databasen installeras flera nya rapporter så att du enkelt kan söka efter och rapportera om dessa data.

### <a name="data-warehouse-dataflow"></a>Data lager data flöde   
![Datawarehouse_flow](./media/datawarehouse.png)

| Steg         | Information  |
|:------:|-----------|  
| **1** | Plats servern överför och lagrar data i plats databasen.  |  
| **2** | Baserat på schema och konfiguration hämtar data lager service punkten data från plats databasen.  |  
| **3** | Informations lager service punkten överför och lagrar en kopia av de synkroniserade data i informations lager databasen. |  
| **A** | Med hjälp av inbyggda rapporter görs en begäran om data som skickas till repor ting Services-platsen med hjälp av SQL Server Reporting Services. |  
| **T** | De flesta rapporter är för aktuell information och dessa begär Anden körs mot plats databasen. |  
| **C** | När en rapport begär historiska data, genom att använda en av rapporterna med en *kategori* av **informations lager**, körs begäran mot informations lager databasen.   |  

### <a name="prerequisites-for-the-data-warehouse-service-point-and-database"></a>Krav för data lager service punkten och databasen
- Hierarkin måste ha en repor ting Services-plats system roll installerad.
- Datorn där du installerar plats system rollen kräver .NET Framework 4.5.2 eller senare.
- Dator kontot för den dator där du installerar plats system rollen måste ha lokal administratörs behörighet på den dator som ska vara värd för informations lager databasen.
- Det administratörs konto som du använder för att installera plats system rollen måste vara en DBO på den instans av SQL Server som ska vara värd för informations lager databasen.  
- -Databasen stöds:
  - Med SQL Server 2012 eller senare, Enterprise eller data Center Edition.
  - På en standard-eller namngiven instans
  - I ett *SQL Server-kluster*. Även om den här konfigurationen ska fungera har den inte testats och support är bäst.
  - Vid samplacering med antingen plats databasen eller rapport tjänst plats databasen. Vi rekommenderar dock att den installeras på en separat server.  
- Kontot som används som *repor ting Services-plats-kontot* måste ha **db_datareader** behörighet till informations lager databasen.  
- Databasen stöds inte på en *SQL Server AlwaysOn-tillgänglighetsgrupper*.

### <a name="install-the-data-warehouse"></a>Installera data lagret
Du installerar plats system rollen för data lagret på en central administrations plats eller en primär plats med hjälp av **guiden Lägg till plats system roller** eller **guiden skapa plats system Server**. Mer information finns i [Installera plats system roller](../servers/deploy/configure/install-site-system-roles.md) . En hierarki stöder flera instanser av den här rollen, men endast en instans stöds på varje plats.  

När du installerar rollen skapar Configuration Manager informations lager databasen åt dig på den instans av SQL Server som du anger. Om du anger namnet på en befintlig databas (som du skulle göra om du [flyttar data lager databasen till en ny SQL Server](#move-the-data-warehouse-database)), skapas inte en ny databas Configuration Manager, utan i stället används den som du anger.

#### <a name="configurations-used-during-installation"></a>Konfigurationer som används under installationen
Använd följande information för att slutföra installationen av plats system rollen:

Sidan **urval för system roll** :  
Innan guiden visar ett alternativ för att välja och installera tjänsten för data lager måste du ha installerat en repor ting Services-plats.

Sidan **Allmänt** : följande allmänna information krävs:
- **Configuration Manager databas inställningar:**   
  - **Server namn** – Ange FQDN för den server som är värd för plats databasen. Om du inte använder en standard instans av SQL Server måste du ange instansen efter FQDN i följande format: *** &lt;Sqlserver_FQDN>\&lt; Instance_name>***
  - **Databas namn** – ange namnet på plats databasen.
  - **Verifiera** – Klicka på **Verifiera** för att kontrol lera att anslutningen till plats databasen har slutförts.
</br></br>
- **Inställningar för informations lager databas:**
  - **Server namn** – Ange FQDN för den server som är värd för informations lager tjänst punkten och databasen. Om du inte använder en standard instans av SQL Server måste du ange instansen efter FQDN i följande format: *** &lt;Sqlserver_FQDN>\&lt; Instance_name>***
  - **Databas namn** – Ange FQDN för informations lager databasen.  Configuration Manager skapar databasen med det här namnet. Om du anger ett databas namn som redan finns på SQL Server-instansen kommer Configuration Manager använda databasen.
  - **Verifiera** – Klicka på **Verifiera** för att kontrol lera att anslutningen till plats databasen har slutförts.

Sidan **Inställningar för synkronisering** :   
- **Data inställningar:**
  - **Replikeringsgrupper som ska synkroniseras** – Välj de data grupper som du vill synkronisera. Information om olika typer av data grupper finns i [databasreplikering](../plan-design/hierarchy/data-transfers-between-sites.md#bkmk_dbrep) och **distribuerade vyer** i [data överföringar mellan platser](../plan-design/hierarchy/data-transfers-between-sites.md).
  - **Tabeller som ingår för att synkronisera** – ange namnet på varje ytterligare tabell som du vill synkronisera. Separera flera tabeller med kommatecken. Tabellerna kommer att synkroniseras från plats databasen förutom de replikeringsgrupper du väljer.
  - **Tabeller som uteslutits för synkronisering** – ange namnet på enskilda tabeller från replikeringsgrupper som du synkroniserar. De tabeller du anger kommer att uteslutas från. Separera flera tabeller med kommatecken.
- **Synkroniseringsinställningar:**
  - **Intervall för synkronisering (minuter)** – ange ett värde i minuter. När intervallet har nåtts startar en ny synkronisering. Detta stöder ett intervall från 60 till 1440 minuter (24 timmar).
  - **Schema** – ange de dagar som du vill att synkroniseringen ska köras.

**Åtkomst till rapporterings punkt**:   
När data lager rollen har installerats kontrollerar du att kontot som används som *repor ting Services-plats-kontot* har **db_datareader** behörighet till informations lager databasen.

#### <a name="troubleshoot-installation-and-data-synchronization"></a>Felsöka installation och datasynkronisering
Använd följande loggar för att undersöka problem med installationen av informations lager service punkten eller synkronisering av data:
- **DWSSMSI. log** och **DWSSSetup. log** – Använd dessa loggar för att undersöka fel när du installerar informations lager service punkten.
- **Microsoft. ConfigMgrDataWarehouse. log** – Använd den här loggen för att undersöka datasynkronisering mellan plats databasen och informations lager databasen.

### <a name="reporting"></a>Rapportering
När du har installerat en plats system roll för data lager är följande rapporter tillgängliga på repor ting Services-platsen med en *kategori* av **informations lager:**

|Rapport                   | Information                                  |
|-------------------------|------------------------------------------|
| **Program distributions rapport** | Visa information om program distribution för ett särskilt program och en specifik dator.|
| **Endpoint Protection-och program varu Uppdateringsefterlevnad rapport**   | Visa datorer som saknar program uppdateringar.|
| **Rapporten allmän maskin varu inventering**  | Visa all maskin varu inventering för en angiven dator.|
| **Rapport över allmän program varu inventering**  | Visa all program varu inventering för en angiven dator.|
| **Översikt över infrastruktur hälsa**  |Visar en översikt över hälso tillståndet för din Configuration Manager-infrastruktur.|
| **Lista över identifierad skadlig kod**  |Visa skadlig kod som har identifierats i organisationen.|
| **Sammanfattnings rapport över program varu distribution** | En sammanfattning av program varu distributionen för en speciell annons och dator.|

### <a name="move-the-data-warehouse-database"></a>Flytta informations lager databasen
Använd följande steg för att flytta informations lager databasen till en ny SQL Server:

1. Granska den aktuella databas konfigurationen och registrera konfigurations informationen, inklusive:  
   - De data grupper som du synkroniserar
   - Tabeller som du tar med eller undantar från synkronisering       

   Du kommer att konfigurera om dessa data grupper och tabeller när du har återställt databasen till en ny server och installerat om plats system rollen.  

2. Använd SQL Server Management Studio för att säkerhetskopiera informations lager databasen och återställ sedan databasen till en SQL Server på den nya datorn som ska vara värd för data lagret.

   När du har återställt databasen till den nya servern måste du kontrol lera att åtkomst behörigheterna för databasen är samma i den nya informations lager databasen som i den ursprungliga informations lager databasen.

3. Använd Configuration Manager-konsolen för att ta bort plats system rollen för data lager service platsen från den aktuella servern.

4. Installera en ny informations lager service punkt och ange namnet på den nya SQL Server och instansen som är värd för den data lager databas som du har återställt.

5. När plats system rollen har installerats slutförs flyttningen.

Du kan granska följande Configuration Manager loggar för att bekräfta att plats system rollen har installerats om:  
- **DWSSMSI. log** och **DWSSSetup. log** – Använd dessa loggar för att undersöka fel när du installerar informations lager service punkten.
- **Microsoft. ConfigMgrDataWarehouse. log** – Använd den här loggen för att undersöka datasynkronisering mellan plats databasen och informations lager databasen.


## <a name="content-library-cleanup-tool"></a>Rensnings verktyg för innehålls bibliotek
Från och med Technical Preview version 1612 kan du använda ett nytt kommando rads verktyg (**ContentLibraryCleanup. exe**) för att ta bort innehåll som inte längre är kopplat till något paket eller program från en distributions plats (frånkopplat innehåll). Verktyget kallas för rensnings verktyget för innehålls bibliotek.

Det här verktyget påverkar endast innehållet på den distributions plats som du anger när du kör verktyget och det går inte att ta bort innehåll från innehålls biblioteket på plats servern.

När du har installerat Technical Preview 1612 hittar du **ContentLibraryCleanup. exe** i mappen *% CM_Installation_Path% \ CD. latest\SMSSETUP\TOOLS\ContentLibraryCleanup\* på den tekniska för hands versionen av plats servern.

Verktyget som lanseras med den här tekniska för hands versionen är avsett att ersätta äldre versioner av liknande verktyg som har publicerats för tidigare Configuration Manager produkter. Även om den här verktygs versionen inte längre kommer att fungera efter den 1 mars 2017 kommer nya versioner att lanseras med framtida tekniska för hands versioner tills det här verktyget släpps som en del av Current Branch eller en out-of-band-version.

### <a name="requirements"></a>Krav  
- Verktyget kan köras direkt på den dator som är värd för distributions platsen, eller via fjärr anslutning från en annan server. Verktyget kan bara köras mot en enskild distributions plats i taget.
- Det användar konto som kör verktyget måste ha rollbaserade administrations behörigheter som är lika med fullständig administratör i Configuration Manager hierarkin.  Verktyget fungerar inte när användar kontot beviljas behörighet som medlem i en Windows-säkerhetsgrupp som har fullständig administratörs behörighet.

### <a name="modes-of-operation"></a>Lägen för åtgärden
Verktyget kan köras i två lägen:
1. **Konsekvens läge**:   
   När du inte anger växeln **/Delete** körs verktyget i konsekvens läge och identifierar det innehåll som skulle tas bort från distributions platsen, men inga data tas bort.

   - När verktyget körs i det här läget skrivs information om det innehåll som skulle tas bort automatiskt till logg filen verktyg. Användaren uppmanas inte att bekräfta varje möjlig borttagning.
   - Som standard skrivs logg filen till användarnas Temp-mapp på den dator där du kör verktyget, men du kan använda växeln/log för att omdirigera logg filen till en annan plats.  
   </br>

   Vi rekommenderar att du kör verktyget i det här läget och granskar den resulterande logg filen innan du kör verktyget med växeln/Delete.  

2. **Borttagnings läge**: när du kör verktyget med **/Delete** -växeln körs verktyget i borttagnings läge.

   - När verktyget körs i det här läget kan överblivna innehåll som finns på den angivna distributions platsen tas bort från distributions platsens innehålls bibliotek.
   -  Innan du tar bort varje fil uppmanas användaren att bekräfta att filen ska tas bort.  Du kan välja, **j** för Ja, **N** för nej eller **Ja till alla** för att hoppa över ytterligare frågor och ta bort allt överblivna innehåll.  
   </br>

   Vi rekommenderar att du kör verktyget i konsekvens läge och granskar den resulterande logg filen innan du kör verktyget med växeln/Delete.  

När rensnings verktyget för innehålls bibliotek körs i båda lägena skapas automatiskt en logg med ett namn som innehåller det läge som verktyget körs i, distributions platsens namn, datum och tid för åtgärden. Logg filen öppnas automatiskt när verktyget har slutförts. Som standard skrivs loggen till användarens **Temp** -mapp på den dator där du kör verktyget. du kan dock använda en kommando rads växel för att omdirigera logg filen till en annan plats, inklusive en nätverks resurs.   


### <a name="run-the-tool"></a>Kör verktyget
Så här kör du verktyget:
1. Öppna en administrativ kommando tolk till en mapp som innehåller **ContentLibraryCleanup. exe**.  
2. Ange sedan en kommando rad som innehåller de nödvändiga kommando rads växlarna och valfria växlar som du vill använda.

**Känt problem** När verktyget körs kan ett fel som liknar följande returneras när ett paket eller en distribution har misslyckats eller pågår:
-  *System. InvalidOperationException: det går inte att rensa det här innehålls biblioteket just nu eftersom \<package PackageID> inte är fullständigt installerat.*

**Lösning:** Ingen. Verktyget kan inte tillförlitligt identifiera överblivna filer när innehåll pågår eller inte har kunnat distribueras. Verktyget tillåter därför inte att du rensar innehåll förrän problemet har lösts.



### <a name="command-line-switches"></a>Kommando rads växlar  
Följande kommando rads växlar kan användas i valfri ordning.   

|Växel|Information|
|---------|-------|
|**/Delete**  |**Valfritt** </br> Använd den här växeln när du vill ta bort innehåll från distributions platsen. Du tillfrågas innan innehållet tas bort. </br></br> När den här växeln inte används loggar verktyget resultatet om vilket innehåll som skulle tas bort, men tar inte bort något innehåll från distributions platsen. </br></br> Exempel: ***ContentLibraryCleanup. exe/dp server1.contoso.com/Delete*** |
| **/q**       |**Valfritt** </br> Kör verktyget i tyst läge som förhindrar alla prompter (t. ex. uppmaningar när du tar bort innehåll) och öppna inte logg filen automatiskt. </br></br> Exempel: ***ContentLibraryCleanup. exe/q/dp server1.contoso.com*** |
| **fullständigt &lt;domän namn för/DP-distributions plats>**  | **Obligatoriskt** </br> Ange det fullständigt kvalificerade domän namnet (FQDN) för den distributions plats som du vill rensa. </br></br> Exempel: ***ContentLibraryCleanup. exe/dp server1.contoso.com***|
| **/PS &lt;primär plats-FQDN>**       | **Valfritt** när innehåll rensas från en distributions plats på en primär plats.</br>**Krävs** när innehåll rensas från en distributions plats på en sekundär plats. </br></br> Ange det fullständiga domän namnet för den primära platsen som distributions platsen tillhör, eller för överordnad primär överordnad plats när distributions platsen finns på en sekundär plats. </br></br> Exempel: ***ContentLibraryCleanup. exe/dp server1.contoso.com/ps siteserver1.contoso.com*** |
| **/SC &lt;Primary site Code>**  | **Valfritt** när innehåll rensas från en distributions plats på en primär plats.</br>**Krävs** när innehåll rensas från en distributions plats på en sekundär plats. </br></br> Ange plats koden för den primära plats som distributions platsen tillhör eller för den överordnade primära platsen när distributions platsen finns på en sekundär plats.</br></br> Exempel: ***ContentLibraryCleanup. exe/dp server1.contoso.com/SC ABC*** |
| **/log \<logg fils katalog>**       |**Valfritt** </br> Ange en katalog för att placera loggfiler i. Detta kan vara en lokal enhet eller en nätverks resurs.</br></br> När den här växeln inte används placeras loggfilerna automatiskt i Temp-mappen användare.</br></br> Exempel på lokal enhet: ***ContentLibraryCleanup. exe/dp server1.contoso.com/log C:\Users\Administrator\Desktop*** </br></br>Exempel på nätverks resurs: ***ContentLibraryCleanup. exe/DP server1.contoso.com/log \\ &lt;resurs>\&lt; mapp>***|


## <a name="improvements-for-in-console-search"></a>Förbättringar för i konsols ökning
Vi har lagt till följande förbättringar i sökning i konsolen, baserat på feedback från användarens röst:
- **Objekt Sök väg:**  
  Många objekt har nu stöd för en ny kolumn med namnet **objekt Sök väg**.  När du söker efter och tar med den här kolumnen i dina visnings resultat kan du Visa sökvägen till varje objekt. Om du till exempel kör en sökning efter appar i noden program och även söker efter underordnade noder, visas sökvägen till varje objekt som returneras i kolumnen *objekt Sök väg* i resultat fönstret.   

- **Bevarande av söktext:**  
  När du anger text i sökrutan och sedan växlar mellan att söka i en underordnad nod och den aktuella noden, behålls texten som du har angett och är tillgänglig för en ny sökning utan att du behöver skriva om den.

- **Bevarande av ditt beslut om att söka efter underordnade noder:**  
  Det alternativ du väljer för att antingen söka i den *aktuella noden* eller *alla undernoder* är nu kvar när du ändrar noden som du arbetar i.   Det här nya beteendet innebär att du inte behöver återställa beslutet hela tiden när du förflyttar dig runt i-konsolen.  Som standard när du öppnar-konsolen är alternativet endast att söka igenom den aktuella noden.

## <a name="prevent-installation-of-an-application-if-a-specified-program-is-running"></a>Förhindra installation av ett program om ett angivet program körs.
Nu kan du konfigurera en lista med körbara filer (med fil namns tillägget. exe) i egenskaper för distributions typ som, om den körs, blockerar installationen av ett program. När installationen har utförts visas en dialog ruta där användaren uppmanas att stänga de processer som blockerar installationen.

### <a name="try-it-out"></a>Prova nu
Konfigurera en lista över körbara filer
1. På sidan Egenskaper för valfri distributions typ väljer du fliken **installations hantering** .
2. Klicka på **Lägg**till för att lägga till en eller flera körbara filer i listan (till exempel **Edge. exe**)
3. Klicka på **OK** för att stänga dialog rutan Egenskaper för distributions typ.

När du nu distribuerar det här programmet till en användare eller en enhet och en av de körbara filer som du har lagt till körs, visas en dialog ruta i Software Center där användaren kan se att installationen misslyckades eftersom ett program körs.

## <a name="new-windows-hello-for-business-notification-for-end-users"></a>Nytt Windows Hello för företag-aviseringar för slutanvändare

Ett nytt meddelande i Windows 10 informerar slutanvändarna om att de måste vidta ytterligare åtgärder för att slutföra installationen av Windows Hello för företag (till exempel att ställa in en PIN-kod).

## <a name="windows-store-for-business-support-in-configuration-manager"></a>Support för Windows Store för företag i Configuration Manager

Nu kan du distribuera licensierade appar online med ett distributions syfte **tillgängligt** från Windows Store för företag till datorer som kör Configuration Manager-klienten.
Mer information finns i [Hantera appar från Windows Store för företag med Configuration Manager](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).

Stöd för den här funktionen är för närvarande bara tillgängligt för datorer som kör Windows 10 RS2 Preview-versionen.

## <a name="return-to-previous-page-when-a-task-sequence-fails"></a>Gå tillbaka till föregående sida när en aktivitetssekvens Miss lyckas
Du kan nu gå tillbaka till en föregående sida när du kör en aktivitetssekvens och det uppstår ett problem. Innan den här versionen var du tvungen att starta om aktivitetssekvensen när det uppstod ett problem. Du kan till exempel använda knappen **föregående** i följande scenarier:

- När en dator startas i Windows PE kan start dialog rutan för aktivitetssekvens visas innan aktivitetssekvensen är tillgänglig. När du klickar på nästa i det här scenariot visas den sista sidan i aktivitetssekvensen med ett meddelande om att det inte finns några tillgängliga aktivitetssekvenser. Nu kan du klicka på **föregående** för att söka igen efter tillgängliga aktivitetssekvenser. Du kan upprepa den här processen tills aktivitetssekvensen är tillgänglig.
- När du kör en aktivitetssekvens, men beroende innehålls paket ännu inte är tillgängliga på distributions platser, Miss lyckas aktivitetssekvensen. Nu kan du distribuera det innehåll som saknas (om det inte distribuerats ännu) eller vänta tills innehållet är tillgängligt på distributions platserna och klicka sedan på **föregående** om du vill att aktivitetssekvensen ska sökas igen för innehållet.

## <a name="express-installation-files-support-for-windows-10-updates"></a>Stöd för Express-installationsfiler för Windows 10-uppdateringar
Vi har lagt till stöd för Express installations filer i Configuration Manager för Windows 10-uppdateringar. När du använder en version av Windows 10 som stöds kan du nu använda Configuration Manager inställningar för att hämta endast delta mellan den kumulativa Windows 10-uppdateringen och föregående månads uppdatering. I Configuration Manager Current Branch hämtas fullständig kumulativ uppdatering för Windows 10 (inklusive alla uppdateringar från föregående månader) varje månad. Med hjälp av Express-installationsfiler kan du få mindre hämtningar och snabbare installations tider på klienter.

> [!IMPORTANT]
> Även om inställningarna för att stödja användningen av Express-installationsfiler är tillgängliga i Configuration Manager, stöds den här funktionen endast i Windows 10 version 1607 med en Windows Update Agent uppdatering som ingår i uppdateringarna som publicerades den 10 januari 2017 (korrigerings tisdag). Mer information om de här uppdateringarna finns i [Support artikel 3213986](https://support.microsoft.com/help/4009938/january-10-2017-kb3213986-os-build-14393-693). Du kan dra nytta av Express-installationsfiler när nästa uppdaterings uppsättning publiceras den 14 februari 2017. Windows 10 version 1607 utan Update och tidigare versioner stöder inte installationsfiler för Express installation.


### <a name="to-enable-the-download-of-express-installation-files-for-windows-10-updates-on-the-server"></a>Så här aktiverar du hämtning av Express-installationsfiler för Windows 10-uppdateringar på servern
Om du vill starta synkroniseringen av metadata för Windows 10 Express-installationsfiler måste du aktivera den i egenskaperna för program uppdaterings platsen.
1. I Configuration Manager-konsolen navigerar du till **Administration** > **plats konfiguration** > **platser**.
2. Välj den centrala administrations platsen eller den fristående primära platsen.
3. Klicka på **Konfigurera platskomponenter** i gruppen **Inställningar** på **Start**-fliken och klicka sedan på **Programuppdateringsplats**. På fliken **uppdateringsfiler** väljer du **Hämta fullständiga filer för alla godkända uppdateringar och installationsfiler för Express installation för Windows 10**.

### <a name="to-enable-support-for-clients-to-download-and-install-express-installation-files"></a>Så här aktiverar du stöd för klienter för att ladda ned och installera installationsfiler för Express
Om du vill aktivera stöd för Express-installationsfiler på-klienter måste du aktivera Express-installationsfiler på klienter i avsnittet program uppdateringar i klient inställningar. Detta skapar en ny HTTP-lyssnare som lyssnar efter begär Anden om att hämta installationsfiler för Express på den port som du anger. När du har distribuerat klient inställningar för att aktivera den här funktionen på klienten försöker den att ladda ned deltaet mellan den kumulativa Windows 10-uppdateringen och den föregående månadens uppdatering (klienter måste köra en version av Windows 10 som stöder installationsfiler).
1. Aktivera stöd för installationsfiler för Express-installation i egenskaperna för komponenten för program uppdaterings plats (föregående procedur).
2. I Configuration Manager-konsolen går du till **Administration** > **klient inställningar**.
3. Välj lämpliga klient inställningar och klicka sedan på **Egenskaper**på fliken **Start** .
4. Välj sidan **program uppdateringar** , konfigurera **Ja** för inställningen **Aktivera installation av Express uppdateringar på klienter** och konfigurera porten som används av http-lyssnaren på klienten för den **port som används för att ladda ned innehåll för inställningen för Express uppdateringar** .


## <a name="odata-endpoint-data-access"></a>Data åtkomst för OData-slutpunkt

 Configuration Manager tillhandahåller nu en RESTful OData-slutpunkt för åtkomst till Configuration Manager data. Slut punkten är kompatibel med OData version 4, vilket gör att verktyg som Excel och Power BI enkelt kan komma åt Configuration Manager data via en enda slut punkt. Technical Preview 1612 stöder bara Läs åtkomst till objekt i Configuration Manager.  

Data som för närvarande är tillgängliga i [Configuration Manager WMI-providern](../../develop/reference/configuration-manager-reference.md) är nu även tillgängliga med den nya OData RESTful-slutpunkten. Enhets uppsättningarna som exponeras av OData-slutpunkten gör det möjligt att räkna upp över samma data som du kan fråga med WMI-providern.

### <a name="try-it-out"></a>Prova nu

Innan du kan använda OData-slutpunkten måste du aktivera den för platsen.

1.  Gå till **Administration** > **plats konfiguration** > **platser**.
2.  Välj den primära platsen och klicka på **Egenskaper**.
3.  På fliken Allmänt i egenskaps sidan primär plats klickar du på **Aktivera REST-slutpunkt för alla providers på den här platsen**och klickar sedan på **OK**.

I ditt favorit visnings program för OData-frågor kan du prova frågor som liknar följande exempel för att returnera olika objekt i Configuration Manager:

| Syfte | OData-fråga |
|---|---|
| Hämta alla samlingar | `http://localhost/CMRestProvider/Collection` |
| Hämta en samling | `http://localhost/CMRestProvider/Collection('SMS00001')`
| Hämta de 100 främsta enheterna i samlingen | `http://localhost/CMRestProvider/Collection('SMS00001')/Device?$top=100` |
| Hämta en enhet med ett resurs-ID i samlingen | `http://localhost/CMRestProvider/Collection('SMS00001')/Device(16777573)` |
| Hämta enhetens operativ system i samlingen | `http://localhost/CMRestProvider/Collection('SMS00001')/Device(16777573)/OPERATING_SYSTEM` |
| Hämta användare i samlingen | `http://localhost/CMRestProvider/Collection('SMS00001')/User` |

> [!NOTE]
> Exempel frågorna som visas i tabellen använder *localhost* som värd namn i URL: en och kan användas på den dator som kör SMS-providern. Om du kör dina frågor från en annan dator ersätter du localhost med det fullständiga domän namnet för servern där SMS-providern är installerad.

## <a name="azure-active-directory-onboarding"></a>Azure Active Directory onboarding

Azure Active Directory (AD) onboarding skapar en anslutning mellan Configuration Manager och Azure Active Directory som ska användas av andra moln tjänster. Detta kan för närvarande användas för att skapa den anslutning som krävs för Cloud Management Gateway.

Utför den här uppgiften med en Azure-administratör eftersom du behöver autentiseringsuppgifter för Azure admin.

#### <a name="to-create-the-connection"></a>Så här skapar du anslutningen:

2. I arbets ytan **Administration** väljer du **Cloud Services** > **Azure Active Directory** > **Lägg till Azure Active Directory**.
2. Välj **Logga** in för att skapa anslutningen till Azure AD.

#### <a name="configuration-manager-client-requirements"></a>Configuration Manager klient krav

Det finns flera krav för att göra det möjligt att skapa användar principer i Cloud Management Gateway.

- Onboarding-processen för Azure AD måste vara fullständig och klienten måste först anslutas till företags nätverket för att få anslutnings information.
- Klienterna måste vara både domänanslutna (registrerade i Active Directory) och molnbaserad (a-domänanslutna) (registrerade i Azure AD).
- Du måste köra [Active Directory användar identifiering](../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser).
- Du måste ändra Configuration Manager-klienten för att tillåta begäran om användar principer via Internet och distribuera ändringen till klienten. Eftersom den här ändringen av klienten äger rum *på klient enheten*kan den distribueras via Cloud Management Gateway, även om du inte har slutfört konfigurations ändringarna som krävs för användar principen.
- Hanterings platsen måste konfigureras för att använda HTTPS för att skydda token i nätverket och måste ha .NET 4,5 installerat.

När du har gjort dessa konfigurations ändringar kan du skapa en användar princip och flytta klienter till Internet för att testa principen. Användar princip begär Anden via Cloud Management Gateway kommer att autentiseras med Azure AD-tokenbaserad autentisering.

## <a name="change-to-configuring-multi-factor-authentication-for-device-enrollment"></a>Ändra till att konfigurera Multi-Factor Authentication för enhets registrering

Nu när du har konfigurerat Multi-Factor Authentication (MFA) för enhets registrering i Azure Portal, har MFA-alternativet tagits bort i Configuration Manager-konsolen. Du hittar mer information om hur du konfigurerar MFA för registrering [i det här Microsoft Intune avsnittet](/mem/intune/enrollment/multi-factor-authentication).
