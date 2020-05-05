---
title: Skapa serverprogram för Linux och UNIX
titleSuffix: Configuration Manager
description: Se vilka överväganden du måste ta med i beräkningen när du skapar och distribuerar program för Linux-och UNIX-enheter.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 79cd131a-1a24-4751-87c8-7f275e45d847
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 3f5d0cfb930e6d1b8cf4cd6dfb0eabfa38ddab16
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075803"
---
# <a name="create-linux-and-unix-server-applications-with-configuration-manager"></a>Skapa Linux-och UNIX-serverprogrammen med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

> [!Important]  
> Från och med version 1902 stöder Configuration Manager inte Linux-eller UNIX-klienter. 
> 
> Överväg Microsoft Azure hantering för hantering av Linux-servrar. Azure-lösningar har omfattande Linux-support som i de flesta fall överskrider Configuration Manager-funktioner, inklusive slut punkt till slut punkt för korrigerings hantering för Linux.

Tänk på följande när du skapar och distribuerar program för datorer som kör Linux och UNIX.  

## <a name="general-considerations"></a>Generella saker att tänka på  
 Configuration Manager-klienten för Linux och UNIX stöder **program varu distributioner som använder paket och program**. Du kan inte distribuera Configuration Manager program till datorer som kör Linux och UNIX.  

 Funktionerna i program varu distributionen Linux och UNIX är:  

-   Program varu installation för Linux-och UNIX-servrar, inklusive följande funktioner:  

    -   Ny programvarudistribution  

    -   Program uppdateringar för program som redan finns på en dator  

    -   OS-uppdateringar  

-   Inbyggda Linux-och UNIX-kommandon och skript som finns på Linux-och UNIX-servrar  

-   Distributioner som är begränsade till de operativ system som du anger när du väljer program alternativet **endast på angivna klient plattformar**

-   Underhålls fönster för att styra när program installeras

-   Distributions status meddelanden för att övervaka distributioner  

-   Alternativet för klienten för att begränsa nätverks användningen när program vara laddas ned från en distributions plats  

### <a name="differences-between-deploying-to-linux-and-unix-computers-and-deploying-to-windows-devices"></a>Skillnader mellan att distribuera till Linux-och UNIX-datorer och distribuera dem till Windows-enheter
De viktigaste skillnaderna mellan att distribuera paket och program till Linux-och UNIX-datorer och att distribuera paket och program till Windows-enheter är följande:  

|Konfiguration|Information|  
|-------------------|-------------|  
|Använd bara konfigurationer som är avsedda för datorer och Använd inte konfigurationer som är avsedda för användare.|Configuration Manager-klienten för Linux och UNIX har inte stöd för konfigurationer som är avsedda för användare.|  
|Konfigurera program för att ladda ned program vara från distributions platsen och kör programmen från den lokala klientcachen.|Configuration Manager-klienten för Linux och UNIX har inte stöd för att köra program vara från distributions platsen. I stället måste du konfigurera program varan så att den laddas ned till klienten och sedan installeras.<br /><br /> Som standard tas program varan bort från klientens cacheminne när klienten för Linux och UNIX installerar program vara. Paket som har kon figurer ATS med **Behåll innehåll i klientcachen** tas dock inte bort från klienten och finns kvar i klientens cacheminne när program varan har installerats.<br /><br /> -Klienten för Linux och UNIX har inte stöd för konfigurationer för klientens cacheminne och den maximala storleken på klientens cacheminne begränsas bara av det lediga disk utrymmet på klient datorn.|  
|Konfigurera kontot för nätverksåtkomst för åtkomst till distributionsplats|Linux- och UNIX-datorer är utformade för att fungera som arbetsgruppdatorer. För att få åtkomst till paket från distributions platsen i Configuration Manager plats Server domän måste du konfigurera kontot för nätverks åtkomst för platsen. Du måste ange det här kontot som en komponentegenskap för programvarudistributionen och konfigurera kontot innan du distribuerar programvaran.<br /><br /> Du kan konfigurera flera konton för nätverksåtkomst på varje plats. Klienten för Linux och UNIX kan använda varje konto du konfigurerar som nätverksåtkomstkonto.<br /><br /> Mer information finns i [plats komponenter för Configuration Manager](../../core/servers/deploy/configure/site-components.md).|  

 Du kan distribuera paket och program till samlingar som bara innehåller Linux- eller UNIX-klienter eller distribuera dem till samlingar som innehåller en blandning av olika klienttyper, till exempel samlingen **Alla system**. Icke-Linux-och icke-UNIX-klienter kommer dock inte att installera program varan eller rapportera felen.  

 När Configuration Manager-klienten för Linux och UNIX tar emot och kör en distribution genereras status meddelanden. Du kan visa dessa status meddelanden i Configuration Manager-konsolen eller genom att använda rapporter för att övervaka distributions statusen.  

 Information om hur du använder paket och program finns i [paket och program](../../apps/deploy-use/packages-and-programs.md).  

##  <a name="configure-packages-programs-and-deployments-for-linux-and-unix-servers"></a>Konfigurera paket, program och distributioner för Linux-och UNIX-servrar  
 Du kan skapa och distribuera paket och program genom att använda de tillgängliga standard alternativen i Configuration Manager-konsolen. Klienten behöver inga unika konfigurationer.  

 Använd informationen i följande avsnitt när du konfigurerar paket och program samt distributioner.  

### <a name="packages-and-programs"></a>Paket och program  
 Om du vill skapa ett paket och program för en Linux-eller UNIX-server använder du **guiden Skapa paket och program** från Configuration Manager-konsolen. Klienten för Linux och UNIX har stöd för de flesta paket- och programinställningar. Det finns dock flera inställningar som inte stöds. Tänk på följande när du skapar eller konfigurerar ett paket och program:  

-   Inkludera de filtyper som stöds av mål datorerna.  

-   Definiera de kommando rader som är lämpliga för användning på mål datorn.  

-   Tänk på att inställningar som interagerar med användare inte stöds.  

I följande tabell visas egenskaper för paket och program som inte stöds:  

|Egenskap för paket och program|Beteende|Mer information|  
|----------------------------------|--------------|----------------------|  
|Paketresursinställningar:<br /><br /> – Alla alternativ|Ett fel genereras och installationen av program varan Miss lyckas|Klienten har inte stöd för den här konfigurationen. Klienten måste i stället ladda ned programvaran via HTTP eller HTTPS och sedan köra kommandoraden från den lokala cachen.|  
|Paketuppdateringsinställningar:<br /><br /> – Koppla från användare från distributions platser|Inställningarna ignoreras|Klienten har inte stöd för den här konfigurationen.|  
|Inställningar för distribution av operativsystem:<br /><br /> – Alla alternativ|Inställningarna ignoreras|Klienten har inte stöd för den här konfigurationen.|  
|Rapportering:<br /><br /> -Använd paket egenskaper för status-MIF-matchning<br /><br /> -Använd de här fälten för status-MIF-matchning|Inställningarna ignoreras|Klienten stöder inte användning av status-MIF-filer.|  
|**Kör**:<br /><br /> – Alla alternativ|Inställningarna ignoreras|Klienten kör alltid paket utan användargränssnitt.<br /><br /> Klienten ignorerar alla konfigurationsalternativ för Kör.|  
|Efter körning:<br /><br />-Configuration Manager startar om datorn<br /><br /> -Program kontroll omstart<br /><br /> -Configuration Manager loggar ut användaren|Ett fel genereras och installationen av program varan Miss lyckas|Inställningen för omstart av systemet och användarspecifika inställningar stöds inte.<br /><br /> Om någon annan inställning än **Ingen åtgärd krävs** används, genereras ett fel och programvaruinstallationen fortsätter utan att någon åtgärd krävs.|  
|Programmet kan köra:<br /><br /> – Endast när en användare är inloggad|Ett fel genereras och installationen av program varan Miss lyckas|Användarspecifika inställningar stöds inte.<br /><br /> När det här alternativet är konfigurerat genererar klienten ett fel och programvaran kan inte installeras.<br /><br /> Andra alternativ ignoreras och programvaruinstallationen fortsätter.|  
|Körningsläge:<br /><br /> -Kör med användarens rättigheter|Inställningarna ignoreras|Användarspecifika inställningar stöds inte.<br /><br /> Klienten stöder dock konfigurationen som körs med administrations behörighet.<br /><br /> När du anger **Kör med administratörs rättigheter**använder Configuration Manager klienten sina autentiseringsuppgifter för roten.<br /><br /> Den här inställningen genererar inte ett fel eller en loggpost. I stället Miss lyckas program varu installationen när klienten genererar ett fel för den obligatoriska konfigurationen för **programmet kan köras** = **endast när en användare är inloggad**.|  
|Tillåt att användare visar och interagerar med programinstallationen|Inställningarna ignoreras|Användarspecifika inställningar stöds inte.<br /><br /> Den här konfigurationen ignoreras och programvaruinstallationen fortsätter.|  
|Enhetsläge:<br /><br /> – Alla alternativ|Inställningarna ignoreras|Den här inställningen stöds inte eftersom innehållet alltid hämtas till klienten och körs lokalt.|  
|Kör ett annat program först|Ett fel genereras och installationen av program varan Miss lyckas|Det finns inte stöd för att installera rekursiva program.<br /><br /> När ett program har kon figurer ATS för att köra ett annat program först, Miss lyckas installationen av program varan och den andra programinstallationen startar inte.|  
|När det här programmet tilldelas en dator:<br /><br /> -Kör en gång för varje användare som loggar in|Inställningarna ignoreras|Användarspecifika inställningar stöds inte.<br /><br /> Klienten stöder dock konfigurationen som körs en gång för datorn.<br /><br /> Den här inställningen genererar inte ett fel eller en loggpost eftersom ett fel och en loggpost redan har skapats för den nödvändiga konfigurationen av **programmet kan bara köras** = **när en användare är inloggad**.|  
|Dölj program meddelanden|Inställningarna ignoreras|Klienten implementerar inget användar gränssnitt.<br /><br /> När den här konfigurationen är vald ignoreras den och program varu installationen fortsätter.|  
|Inaktivera det här programmet på datorer där det har distribuerats|Inställningarna ignoreras|Den här inställningen stöds inte och påverkar inte installationen av program varan.|  
|Tillåt att det här programmet installeras från aktivitetssekvensen installera paket utan att distribueras||Klienten har inte stöd för aktivitetssekvenser.<br /><br /> Den här inställningen stöds inte och påverkar inte installationen av program varan.|  
|Windows Installer:<br /><br /> – Alla alternativ|Inställningarna ignoreras|Klienten har inte stöd för Windows Installer filer eller inställningar.|  
|OpsMgr-underhållsläge:<br /><br /> – Alla alternativ|Inställningarna ignoreras|Klienten har inte stöd för den här konfigurationen.|  

### <a name="deploy-software-to-a-linux-or-unix-server"></a>Distribuera program vara till en Linux-eller UNIX-server
 Om du vill distribuera program vara till en Linux-eller UNIX-server med hjälp av ett paket och program kan du använda **guiden distribuera program vara** från Configuration Manager-konsolen. De flesta distributions inställningar stöds av klienten för Linux och UNIX. Det finns dock inte stöd för flera inställningar. Tänk på följande när du distribuerar program vara:  

- Etablera paketet på minst en distributions plats som är kopplad till en begränsande grupp som är konfigurerad för innehålls plats.  

- Klienten för Linux och UNIX som tar emot den här distributionen måste kunna komma åt den här distributions platsen från dess nätverks plats.  

- Klienten för Linux och UNIX laddar ned paketet från distributionsplatsen och kör programmet på den lokala datorn.  

- Klienten för Linux och UNIX kan inte ladda ned paket från delade mappar. Paket hämtas från IIS-aktiverade distributions platser som stöder HTTP eller HTTPS.  

  I följande tabell visas egenskaper för distributioner som inte stöds:  

|Distributionsegenskap|Beteende|Mer information|  
|-------------------------|--------------|----------------------|  
|Distributionsinställningar – syfte:<br /><br /> – Tillgängligt<br /><br /> – Krävs|Inställningarna ignoreras|Användarspecifika inställningar stöds inte.<br /><br /> Klienten stöder dock den inställning som **krävs**, vilket tillämpar den schemalagda installations tiden, men som inte har stöd för manuell installation före den schemalagda tiden.|  
|Skicka uppvakningspaket|Inställningarna ignoreras|Klienten har inte stöd för den här konfigurationen.|  
|Tilldelningsschema:<br /><br /> -Logga in<br /><br /> -Logga ut|Ett fel genereras och installationen av program varan Miss lyckas|Användarspecifika inställningar stöds inte.<br /><br /> Klienten har dock stöd för inställningen **Så snart som möjligt**.|  
|Meddelandeinställningar:<br /><br /> – Tillåt att användare kör programmet oberoende av tilldelningar|Inställningarna ignoreras|Klienten implementerar inget användar gränssnitt.|  
|När tidsgränsen för den schemalagda tilldelningen har uppnåtts kan du tillåta att följande aktiviteter utförs utanför underhållsfönstret:<br /><br /> -Systemomstart (om det krävs för att slutföra installationen)|Ett fel genereras|Klienten har inte stöd för omstart av systemet.|  
|Distributionsalternativ för snabba nätverk (LAN):<br /><br /> -Kör program från distributions plats|Ett fel genereras och installationen av program varan Miss lyckas|Klienten kan inte köra program vara från distributions platsen och måste i stället Ladda ned programmet innan det kan köras.|  
|Distributionsalternativ för långsamt eller instabilt nätverk eller återställningskällplats för innehåll:<br /><br /> -Tillåt att klienter delar innehåll med andra klienter i samma undernät|Inställningarna ignoreras|Klienten stöder inte delning av innehåll mellan peer-datorer.|  

 Mer information om innehålls plats finns i [Hantera innehåll och innehålls infrastruktur för Configuration Manager](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

 Mer information om hur du skapar en distribution finns i [distribuera program](../../apps/deploy-use/deploy-applications.md).  

##  <a name="manage-network-bandwidth-for-software-downloads-from-distribution-points"></a> Hantera nätverksbandbredd för nedladdning av programvara från distributionsplatser  
 Linux-och UNIX-klienten stöder nätverks bandbredds kontroller när program vara laddas ned från en distributions plats.  

 Klienten använder de inställningar för BITS (Background Intelligent Transfer) som du konfigurerar som klient inställningar i Configuration Manager, men implementerar inte BITS. För att begränsa användningen av nätverksbandbredd styr klienten storleken på HTTP-begäranssegmentet och fördröjningen mellan segment för nedladdning av programvara.  

 Om du vill konfigurera en klient så att den använder bandbreddskontroller konfigurerar du klientinställningar för **Background Intelligent Transfer** och använder sedan inställningarna på klientdatorn. Om du vill använda bandbredds kontroller måste klienten ta emot klient inställningar för **Background Intelligent Transfer** med följande inställningar konfigurerade som **Ja**:  

- **Begränsa den maximala nätverksbandbredden för BITS-bakgrundsöverföring**  

  Klienten har stöd för följande konfigurationer för Background Intelligent Transfer:  

  -   **Starttid för begränsningsfönstret**  

  -   **Sluttid för begränsningsfönstret**  

  -   **Maximal överföringshastighet under begränsningsfönstret (kbit/s)**  

  -   **Maximal överföringshastighet utanför begränsningsfönstret (kbit/s)**  

Följande konfiguration för Background Intelligent Transfer stöds inte och ignoreras av klienten för Linux och UNIX:  

- **Tillåt BITS-hämtningar utanför begränsningsfönstret**  

  Om nedladdningen av program vara till klienten från en distributions plats avbryts, kommer inte klienten för Linux och UNIX att återuppta nedladdningen. I stället startas om nedladdningen av hela program varu paketet.  

##  <a name="configure-operations-for-software-deployments"></a>Konfigurera åtgärder för program varu distributioner  
 På samma sätt som Windows-klienten, identifierar Configuration Manager-klienten för Linux och UNIX nya program varu distributioner när den avsöker och söker efter ny princip. Hur ofta en klient söker efter nya principer beror på klientinställningarna. Du kan konfigurera underhållsperioder för att styra när programvara ska distribueras.  

 Du kan konfigurera programvarudistributioner till Linux- och UNIX-servrar genom att använda paketegenskaper, programegenskaper och distributionsegenskaper.  

 När klienten får principen för en distribution skickar den ett statusmeddelande. Den skickar också status meddelanden när installationen av program varan påbörjas och installationen slutförs eller Miss lyckas.  

 Program för program varu distributioner körs med de autentiseringsuppgifter för roten som Configuration Manager-klienten för Linux och UNIX körs med. Slutkoden för programkommandot används för att fastställa om åtgärden lyckades eller misslyckades. Slutkoden 0 (noll) betyder att åtgärden lyckades. Dessutom kopieras standardutdataströmmen **stdout** och standardfelströmmen **stderr** till loggfilen när loggnivån är INFO eller TRACE.  

> [!TIP]  
>  Om den programvara du vill distribuera finns på en nätverksfilsystemresurs (NFS-resurs) som Linux- eller UNIX-servern har åtkomst till, behöver du inte använda någon distributionsplats för att ladda ned paketet. I det fallet markerar du inte kryssrutan **Det här paketet innehåller källfiler**när du skapar paketet. När du sedan konfigurerar programmet anger du lämplig kommandorad för att få direktåtkomst till paketet på NFS-monteringsplatsen.  
