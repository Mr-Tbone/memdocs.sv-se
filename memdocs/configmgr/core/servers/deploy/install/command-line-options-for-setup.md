---
title: Kommando rads alternativ för installation
titleSuffix: Configuration Manager
description: Skapa Automation-skript för att installera Configuration Manager från en kommando rad.
ms.date: 08/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0da167f1-52cf-4dfd-8f73-833ca3eb8478
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8e4950e32fa5ddc0a4fc1a13ec8e584dc1ae9ff3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718254"
---
# <a name="command-line-options-for-configuration-manager-setup"></a>Kommando rads alternativ för installation av Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Använd följande information för att konfigurera skript eller för att installera Configuration Manager från en kommando rad.  

## <a name="command-line-options-for-setup"></a><a name="bkmk_setup"></a>Kommando rads alternativ för installation

Kör installations programmet från `\BIN\X64` katalogen i Configuration Manager installations Sök väg på plats servern.

### `/DEINSTALL`

Avinstallera platsen. Kör installations programmet från plats serverdatorn.  

### `/DONTSTARTSITECOMP`

Installera en plats, men förhindrar att Platskomponenthanterarens tjänsten startar. Platsen är inte aktiv förrän den Platskomponenthanteraren tjänsten startar. Platskomponenthanteraren ansvarar för att installera och starta tjänsten SMS_Executive och för ytterligare processer på platsen. När platsen har installerats installeras SMS_Executive-tjänsten och ytterligare processer som krävs för att platsen ska köras när du startar tjänsten Platskomponenthanteraren.  

### `/HIDDEN`

Dölj användar gränssnittet under installationen. Använd bara det här alternativet tillsammans med alternativet **/script** . Den obevakade skript filen måste innehålla alla alternativ som krävs, annars Miss lyckas installationen.  

### `/NOUSERINPUT`

Inaktivera användarindata under installationen, men visar installations guiden. Använd bara det här alternativet tillsammans med alternativet **/script** . Den obevakade skript filen måste innehålla alla alternativ som krävs, annars Miss lyckas installationen.  

### `/RESETSITE`

Kör en plats återställning som återställer databasen och tjänst kontona för platsen.

Mer information finns i [köra en plats återställning](../../manage/modify-your-infrastructure.md#bkmk_reset).  

### `/TESTDBUPGRADE`

Kör ett test på en säkerhets kopia av plats databasen för att kontrol lera att databasen kan uppgraderas.

> [!IMPORTANT]  
> Kör inte det här kommando rads alternativet på produktions plats databasen. Genom att köra det här kommando rads alternativet på produktions plats databasen uppgraderas plats databasen och det kan leda till att platsen inte fungerar.

#### <a name="usage"></a>Användning

Ange instans namnet och databas namnet för plats databasen. Om du bara anger databas namnet används standard instans namnet i installations programmet.  

`/TESTDBUPGRADE <Instance name>\<Database name>`

`/TESTDBUPGRADE CM_ABC`

`/TESTDBUPGRADE Named\CM_ABC`

### `/UPGRADE`

Kör en obevakad uppgradering av en plats. Ange produkt nyckeln inklusive bindestreck (`-`). Ange också sökvägen till de tidigare nedladdade nödvändiga filerna för installation.  

Mer information om nödvändiga installationsfiler finns i [installations hämtaren](setup-downloader.md).  

#### <a name="usage"></a>Användning

`setupwpf.exe /UPGRADE xxxxx-xxxxx-xxxxx-xxxxx-xxxxx <path to external component files>`  

### `/SCRIPT`

Kör en obevakad installation. Använd en initierings fil för installationen med det här alternativet. Mer information om hur du kör installationen obevakad finns i [Installera platser med hjälp av en kommando rad](use-a-command-line-to-install-sites.md).  

#### <a name="usage"></a>Användning

`/SCRIPT <setup script path>`

### `/SDKINST`

Installera SMS-providern på den angivna datorn. Ange det fullständigt kvalificerade domän namnet (FQDN) för SMS-providerns dator. Mer information om SMS-providern finns i [Planera för SMS-providern](../../../plan-design/hierarchy/plan-for-the-sms-provider.md).  

#### <a name="usage"></a>Användning

`/SDKINST <SMS Provider FQDN>`

### `/SDKDEINST`

Avinstallera SMS-providern på den angivna datorn. Ange FQDN för SMS-providerns dator.  

#### <a name="usage"></a>Användning

`/SDKDEINST <SMS Provider FQDN>`

### `/MANAGELANGS`

Hantera de språk som är installerade på en tidigare installerad plats. Ange platsen för den språk skript fil som innehåller språk inställningarna. Mer information finns i avsnittet [kommando rads alternativ för att hantera språk](#bkmk_Lang) .  

#### <a name="usage"></a>Användning

`/MANAGELANGS <Language script path>`


## <a name="command-line-options-to-manage-languages"></a><a name="bkmk_Lang"></a>Kommando rads alternativ för att hantera språk

### <a name="identification"></a>Identification

- **Nyckelnamn:** Action  

    - **Krävs:** Ja  

    - **Värden:**`ManageLanguages`  

    - **Information:** Hanterar språk stöd för servern, klienten och den mobila klienten på en plats.  

### <a name="options"></a>Alternativ

- **Nyckel namn:** AddServerLanguages  

    - **Krävs:** Nej  

    - **Värden:** DEU, FRA, ru: er, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, spår eller ZHH  

    - **Information:** Anger de Server språk som ska vara tillgängliga för Configuration Manager-konsolen, rapporter och Configuration Manager objekt. Engelska är tillgängligt som standard.  

- **Nyckel namn:** AddClientLanguages  

    - **Krävs:** Nej  

    - **Värden:** DEU, FRA, ru: er, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, spår eller ZHH  

    - **Information:** Anger de språk som ska vara tillgängliga för klient datorer. Engelska är tillgängligt som standard.  

- **Nyckel namn:** DeleteServerLanguages  

    - **Krävs:** Nej  

    - **Värden:** DEU, FRA, ru: er, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, spår eller ZHH  

    - **Information:** Anger de språk som ska tas bort och som inte längre kommer att vara tillgängliga för Configuration Manager-konsolen, rapporter och Configuration Manager objekt. Engelska är tillgängligt som standard och du kan inte ta bort det.  

- **Nyckel namn:** DeleteClientLanguages  

    - **Krävs:** Nej  

    - **Värden:** DEU, FRA, ru: er, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, spår eller ZHH  

    - **Information:** Anger de språk som ska tas bort och som inte längre kommer att vara tillgängliga för klient datorer. Engelska är tillgängligt som standard och du kan inte ta bort det.  

- **Nyckel namn:** MobileDeviceLanguage  

    - **Krävs:** Ja  

    - **Parametervärden**

        - `0`= Installera inte  

        - `1`= Installera  

    - **Information:** Anger om de mobila enhets klient språken är installerade.  

- **Nyckelnamn:** PrerequisiteComp  

    - **Krävs:** Ja  

    - **Parametervärden**

        - `0`= Ladda ned  

        - `1`= Redan nedladdat  

    - **Information:** Anger om nödvändiga filer för installations programmet redan har laddats ned. Om du till exempel använder värdet `0`, laddar installations programmet ned filerna.  

- **Nyckelnamn:** PrerequisitePath  

    - **Krävs:** Ja  

    - **Värden:** <*sökväg för att konfigurera nödvändiga filer*>  

    - **Information:** Anger sökvägen till de nödvändiga filerna för installationen. Beroende på **PrerequisiteComp** -värdet använder installations programmet den här sökvägen för att lagra hämtade filer eller för att hitta tidigare hämtade filer.  


## <a name="unattended-setup-script-file-keys"></a><a name="bkmk_Unattended"></a>Skript fils nycklar för obevakad installation

Använd följande avsnitt för att hjälpa dig att skapa skriptet för obevakad installation. Listorna visar:

- De tillgängliga installations skript nycklarna och deras motsvarande värden
- Om de är obligatoriska
- Vilken typ av installation de används för
- En kort beskrivning av nyckeln

### <a name="unattended-install-for-a-central-administration-site-cas"></a>Obevakad installation för en central administrations plats (CAS)

Använd följande information för att installera en certifikat utfärdare med hjälp av en obevakad installations skript fil.  

#### <a name="identification"></a>Identification

- **Nyckelnamn:** Action  

    - **Krävs:** Ja  

    - **Värden:**`InstallCAS`  

    - **Information:** Installerar en certifikat utfärdare.  

- **Nyckel namn:** CDLatest  

    - **Krävs:** Ja, bara när du använder media från CD: n. Senaste mappen.

    - **Parametervärden**

        - `1`= du använder media från CD. Nya

        - Ett annat värde än 1 = du använder inte CD. Senaste mediet

    - **Information:** När du installerar eller återställer en primär plats eller certifikat utfärdare och kör installations programmet från CD: n. Den senaste mappen inkluderar du den här nyckeln och värdet. Detta värde informerar installations programmet att du använder media från CD. Nya.

#### <a name="options"></a>Alternativ

- **Nyckelnamn:** ProductID  

    - **Krävs:** Ja  

    - **Parametervärden**

        - `<xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>`= en giltig produkt nyckel med streck

        - `Eval`= Installera utvärderings versionen av Configuration Manager

    - **Information:** Anger produkt nyckeln för Configuration Manager installation, inklusive streck.

- **Nyckelnamn:** SiteCode  

    - **Krävs:** Ja  

    - **Värden:** <*plats kod*>, till exempel`ABC`

    - **Information:** Anger tre alfanumeriska tecken som unikt identifierar platsen i hierarkin.  

- **Nyckel namn:** Plats namn  

    - **Krävs:** Ja  

    - **Värden:** <*plats namn*>  

    - **Information:** Anger namnet på den här platsen.  

- **Nyckelnamn:** SMSInstallDir  

    - **Krävs:** Ja  

    - **Värden:** <*Configuration Manager installations Sök väg*>  

    - **Information:** Anger installationsmappen för Configuration Manager program-filerna.  

- **Nyckelnamn:** SDKServer  

    - **Krävs:** Ja  

    - **Värden:** <*SMS-providerns FQDN*>  

    - **Information:** Anger det fullständiga domännamnet för servern som är värd för SMS-providern. Du kan konfigurera ytterligare SMS-providrar för platsen efter den första installationen.  

- **Nyckelnamn:** PrerequisiteComp  

    - **Krävs:** Ja  

    - **Parametervärden**

        - `0`= Ladda ned  

        - `1`= Redan nedladdat  

    - **Information:** Anger om nödvändiga filer för installations programmet redan har laddats ned. Om du till exempel använder värdet `0`, laddar installations programmet ned filerna.  

- **Nyckelnamn:** PrerequisitePath  

    - **Krävs:** Ja  

    - **Värden:** <*sökväg för att konfigurera nödvändiga filer*>  

    - **Information:** Anger sökvägen till de nödvändiga filerna för installationen. Beroende på **PrerequisiteComp** -värdet använder installations programmet den här sökvägen för att lagra hämtade filer eller för att hitta tidigare hämtade filer.  

- **Nyckelnamn:** AdminConsole  

    - **Krävs:** Ja  

    - **Parametervärden**

        - `0`= Installera inte  

        - `1`= Installera  

    - **Information:** Anger om Configuration Manager-konsolen ska installeras eller inte.  

- **Nyckelnamn:** JoinCEIP  

    > [!Note]  
    > Från och med Configuration Manager version 1802, tas CEIP-funktionen bort från produkten.

    - **Krävs:** Ja  

    - **Parametervärden**

        - `0`= Anslut inte  

        - `1`= Anslut  

    - **Information:** Anger om Customer Experience Improvement Program (CEIP) ska anslutas.  

- **Nyckel namn:** AddServerLanguages  

    - **Krävs:** Nej  

    - **Värden:** DEU, FRA, ru: er, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, spår eller ZHH  

    - **Information:** Anger de Server språk som ska vara tillgängliga för Configuration Manager-konsolen, rapporter och Configuration Manager objekt. Engelska är tillgängligt som standard.  

- **Nyckel namn:** AddClientLanguages  

    - **Krävs:** Nej  

    - **Värden:** DEU, FRA, ru: er, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, spår eller ZHH  

    - **Information:** Anger de språk som ska vara tillgängliga för klient datorer. Engelska är tillgängligt som standard.  

- **Nyckel namn:** DeleteServerLanguages  

    - **Krävs:** Nej  

    - **Värden:** DEU, FRA, ru: er, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, spår eller ZHH  

    - **Information:** Ändrar en plats efter att den har installerats. Anger de språk som ska tas bort och som inte längre kommer att vara tillgängliga för Configuration Manager-konsolen, rapporter och Configuration Manager objekt. Engelska är tillgängligt som standard och du kan inte ta bort det.  

- **Nyckel namn:** DeleteClientLanguages  

    - **Krävs:** Nej  

    - **Värden:** DEU, FRA, ru: er, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, spår eller ZHH  

    - **Information:** Ändrar en plats efter att den har installerats. Anger de språk som ska tas bort och som inte längre kommer att vara tillgängliga för klient datorer. Engelska är tillgängligt som standard och du kan inte ta bort det.  

- **Nyckel namn:** MobileDeviceLanguage  

    - **Krävs:** Ja  

    - **Parametervärden**

        - `0`= Installera inte  

        - `1`= Installera  

    - **Information:** Anger om de mobila enhets klient språken är installerade.  

#### <a name="sqlconfigoptions"></a>SQLConfigOptions

- **Nyckelnamn:** SQLServerName  

    - **Krävs:** Ja  

    - **Värden:** <*SQL Server-namn*>  

    - **Information:** Anger namnet på den server eller klustrade instans som kör SQL Server som värd för plats databasen.  

- **Nyckelnamn:** DatabaseName  

    - **Krävs:** Ja  

    - **Värden:** <*plats databas namn*> eller <*instans namn*>\\<*plats databas namn*>  

    - **Information:** Anger namnet på den SQL Server databas som ska skapas eller den SQL Server databasen som ska användas när installations programmet installerar CAS-databasen.  

        > [!IMPORTANT]  
        > Om du inte använder standard instansen anger du instans namn och plats databasens namn.  

- **Nyckelnamn:** SQLSSBPort  

    - **Krävs:** Nej  

    - **Värden:** <*SSB Port Number*>  

    - **Information:** Anger den SQL Server Service Broker-port (SSB) som SQL Server använder. Som standard använder SSB TCP-port 4022, men du kan använda en annan port.  

- **Nyckel namn:** SQLDataFilePath  

    - **Krävs:** Nej  

    - **Värden:** <*sökväg till databasen. mdb-fil*>  

    - **Information:** Anger en alternativ plats för att skapa en databas. mdb-fil.  

- **Nyckel namn:** SQLLogFilePath  

    - **Krävs:** Nej  

    - **Värden:** <*sökväg till databasen. LDF-fil*>  

    - **Information:** Anger en alternativ plats för att skapa en databas. LDF-fil.  

#### <a name="cloudconnectoroptions"></a>CloudConnectorOptions

- **Nyckel namn:** CloudConnector  

    - **Krävs:** Ja  

    - **Parametervärden**

        - `0`= Installera inte  

        - `1`= Installera  

    - **Information:** Anger om en tjänst anslutnings punkt ska installeras på den här platsen. Eftersom du bara kan installera tjänst anslutnings punkten på platsen på den översta nivån i en hierarki, ställer du in värdet på `1` för en underordnad primär plats.  

- **Nyckel namn:** CloudConnectorServer  

    - **Krävs:** Krävs när **CloudConnector** är lika med 1  

    - **Värden:** <*serverns FQDN för tjänst anslutnings punkt*>  

    - **Information:** Anger det fullständiga domän namnet för den server som ska vara värd för tjänst anslutnings punktens plats system roll.  

- **Nyckel namn:** UseProxy  

    - **Krävs:** Krävs när **CloudConnector** är lika med 1  

    - **Parametervärden**

        - `0`= Installera inte  

        - `1`= Installera  

    - **Information:** Anger om tjänst anslutnings punkten använder en proxyserver.  

- **Nyckel namn:** ProxyName  

    - **Krävs:** Krävs när **UseProxy** är lika med 1  

    - **Värden:** <*proxy serverns FQDN*>  

    - **Information:** Anger det fullständiga domän namnet för proxyservern som används av tjänst anslutnings punkten.  

- **Nyckel namn:** ProxyPort  

    - **Krävs:** Krävs när **UseProxy** är lika med 1  

    - **Värden:** <*port nummer*>  

    - **Information:** Anger det port nummer som ska användas för proxyservern.  

#### <a name="sabranchoptions"></a>SABranchOptions

<!-- SCCMDocs#390 -->

- **Nyckel namn:** SAActive

    - **Krävs:** Nej

    - **Parametervärden**

        - `0`= Du har inte Software Assurance

        - `1`= Software Assurance är aktiv

    - **Information:** Ange om du har en aktiv Software Assurance. Mer information finns i [vanliga frågor och svar om produkt och licensiering](../../../understand/product-and-licensing-faq.md).

- **Nyckel namn:** CurrentBranch

    - **Krävs:** Nej

    - **Parametervärden**

        - `0`= Installera LTSB

        - `1`= Installera aktuell gren

    - **Information:** Ange om du vill använda Configuration Manager aktuella grenen eller långtids service grenen (LTSB). Mer information finns i [vilken gren av Configuration Manager ska jag använda?](../../../understand/which-branch-should-i-use.md).

### <a name="unattended-install-for-a-primary-site"></a>Obevakad installation för en primär plats

Använd följande information för att installera en primär plats med hjälp av en obevakad installations skript fil.  

#### <a name="identification"></a>Identification

- **Nyckelnamn:** Action  

    - **Krävs:** Ja  

    - **Värden:**`InstallPrimarySite`  

    - **Information:** Installerar en primär plats.  

- **Nyckel namn:** CDLatest  

    - **Krävs:** Ja, bara när du använder media från CD: n. Senaste mappen.

    - **Parametervärden**

        - `1`= du använder media från CD. Nya

        - Ett annat värde än 1 = du använder inte CD. Senaste mediet

    - **Information:** När du installerar eller återställer en primär plats eller certifikat utfärdare och kör installations programmet från CD: n. Den senaste mappen inkluderar du den här nyckeln och värdet. Detta värde informerar installations programmet att du använder media från CD. Nya.

#### <a name="options"></a>Alternativ

- **Nyckelnamn:** ProductID  

    - **Krävs:** Ja  

    - **Parametervärden**

        - `<xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>`= en giltig produkt nyckel med streck

        - `Eval`= Installera utvärderings versionen av Configuration Manager

    - **Information:** Anger produkt nyckeln för Configuration Manager installation, inklusive streck.

- **Nyckelnamn:** SiteCode  

    - **Krävs:** Ja  

    - **Värden:** <*platskod*>  

    - **Information:** Anger tre alfanumeriska tecken som unikt identifierar platsen i hierarkin.  

- **Nyckelnamn:** SiteName  

    - **Krävs:** Ja  

    - **Värden:** <*plats namn*>  

    - **Information:** Anger namnet på den här platsen.  

- **Nyckelnamn:** SMSInstallDir  

    - **Krävs:** Ja  

    - **Värden:** <*Configuration Manager installations Sök väg*>

    - **Information:** Anger installationsmappen för Configuration Manager program-filerna.  

- **Nyckelnamn:** SDKServer  

    - **Krävs:** Ja  

    - **Värden:** <*SMS-providerns FQDN*>  

    - **Information:** Anger det fullständiga domännamnet för servern som är värd för SMS-providern. Du kan konfigurera ytterligare SMS-providrar för platsen efter den första installationen.  

- **Nyckelnamn:** PrerequisiteComp  

    - **Krävs:** Ja  

    - **Parametervärden**

        - `0`= Ladda ned  

        - `1`= Redan nedladdat  

    - **Information:** Anger om nödvändiga filer för installations programmet redan har laddats ned. Om du till exempel använder värdet `0`, laddar installations programmet ned filerna.  

- **Nyckelnamn:** PrerequisitePath  

    - **Krävs:** Ja  

    - **Värden:** <*sökväg för att konfigurera nödvändiga filer*>  

    - **Information:** Anger sökvägen till de nödvändiga filerna för installationen. Beroende på **PrerequisiteComp** -värdet använder installations programmet den här sökvägen för att lagra hämtade filer eller för att hitta tidigare hämtade filer.  

- **Nyckelnamn:** AdminConsole  

    - **Krävs:** Ja  

    - **Parametervärden**

        - `0`= Installera inte  

        - `1`= Installera  

    - **Information:** Anger om Configuration Manager-konsolen ska installeras eller inte.  

- **Nyckelnamn:** JoinCEIP  

    > [!Note]  
    > Från och med Configuration Manager version 1802, tas CEIP-funktionen bort från produkten.

    - **Krävs:** Ja  

    - **Parametervärden**

        - `0`= Anslut inte  

        - `1`= Anslut  

    - **Information:** Anger om du vill delta i CEIP.  

- **Nyckel namn:** ManagementPoint  

    - **Krävs:** Nej  

    - **Värden:** <*plats serverns FQDN för hanterings plats*>  

    - **Information:** Anger det fullständiga domän namnet för den server som ska vara värd för hanterings platsens plats system roll.  

- **Nyckel namn:** ManagementPointProtocol  

    - **Krävs:** Nej  

    - **Värden:** `HTTPS` eller`HTTP`  

    - **Information:** Anger vilket protokoll som ska användas för hanterings platsen.  

- **Nyckel namn:** DistributionPoint  

    - **Krävs:** Nej  

    - **Värden:** <*FQDN för plats Server för distributions plats*>  

    - **Information:** Anger det fullständiga domän namnet för den server som är värd för distributions platsens plats system roll.  

- **Nyckel namn:** DistributionPointProtocol  

    - **Krävs:** Nej  

    - **Värden:** `HTTPS` eller`HTTP`  

    - **Information:** Anger det protokoll som ska användas för distributions platsen.  

- **Nyckel namn:** RoleCommunicationProtocol  

    - **Krävs:** Ja  

    - **Värden:** `EnforceHTTPS` eller`HTTPorHTTPS`  

    - **Information:** Anger om alla plats system ska konfigureras så att de bara accepterar HTTPS-kommunikation från klienter eller konfigurerar kommunikations metoden för varje plats system roll. När du väljer `EnforceHTTPS`måste klienterna ha ett giltigt PKI-certifikat (Public Key Infrastructure) för klientautentisering.  

- **Nyckel namn:** ClientsUsePKICertificate  

    - **Krävs:** Ja  

    - **Parametervärden**

        - `0`= Använd inte  

        - `1`= Använd  

    - **Information:** Anger om klienter ska använda ett klient-PKI-certifikat för att kommunicera med plats system roller.  

- **Nyckel namn:** AddServerLanguages  

    - **Krävs:** Nej  

    - **Värden:** DEU, FRA, ru: er, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, spår eller ZHH  

    - **Information:** Anger de Server språk som ska vara tillgängliga för Configuration Manager-konsolen, rapporter och Configuration Manager objekt. Engelska är tillgängligt som standard.  

- **Nyckel namn:** AddClientLanguages  

    - **Krävs:** Nej  

    - **Värden:** DEU, FRA, ru: er, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, spår eller ZHH  

    - **Information:** Anger de språk som ska vara tillgängliga för klient datorer. Engelska är tillgängligt som standard.  

- **Nyckel namn:** DeleteServerLanguages  

    - **Krävs:** Nej  

    - **Värden:** DEU, FRA, ru: er, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, spår eller ZHH  

    - **Information:** Ändrar en plats efter att den har installerats. Anger de språk som ska tas bort och som inte längre kommer att vara tillgängliga för Configuration Manager-konsolen, rapporter och Configuration Manager objekt. Engelska är tillgängligt som standard och du kan inte ta bort det.  

- **Nyckel namn:** DeleteClientLanguages  

    - **Krävs:** Nej  

    - **Värden:** DEU, FRA, ru: er, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, spår eller ZHH  

    - **Information:** Ändrar en plats efter att den har installerats. Anger de språk som ska tas bort och som inte längre kommer att vara tillgängliga för klient datorer. Engelska är tillgängligt som standard och du kan inte ta bort det.  

- **Nyckel namn:** MobileDeviceLanguage  

    - **Krävs:** Ja  

    - **Parametervärden**

        - `0`= Installera inte  

        - `1`= Installera  

    - **Information:** Anger om de mobila enhets klient språken är installerade.  

#### <a name="sqlconfigoptions"></a>SQLConfigOptions

- **Nyckelnamn:** SQLServerName  

    - **Krävs:** Ja  

    - **Värden:** <*SQL Server-namn*>  

    - **Information:** Anger namnet på den server eller klustrade instans som kör SQL Server som värd för plats databasen.  

- **Nyckelnamn:** DatabaseName  

    - **Krävs:** Ja  

    - **Värden:** <*plats databas namn*> eller <*instans namn*>\\<*plats databas namn*>  

    - **Information:** Anger namnet på SQL Server databasen som ska skapas eller SQL Server databasen som ska användas för att installera den primära plats databasen.  

        > [!IMPORTANT]  
        > Om du inte använder standard instansen anger du instans namn och plats databasens namn.  

- **Nyckelnamn:** SQLSSBPort  

    - **Krävs:** Nej  

    - **Värden:** <*SSB Port Number*>  

    - **Information:** Anger den SSB-port som SQL Server använder. Som standard använder SSB TCP-port 4022, men du kan använda en annan port.  

- **Nyckel namn:** SQLDataFilePath  

    - **Krävs:** Nej  

    - **Värden:** <*sökväg till databasen. mdb-fil*>  

    - **Information:** Anger en alternativ plats för att skapa en databas. mdb-fil.  

- **Nyckel namn:** SQLLogFilePath  

    - **Krävs:** Nej  

    - **Värden:** <*sökväg till databasen. LDF-fil*>  

    - **Information:** Anger en alternativ plats för att skapa en databas. LDF-fil.  

#### <a name="hierarchyexpansionoption"></a>HierarchyExpansionOption

- **Nyckelnamn:** CCARSiteServer  

    - **Krävs:** Nej  

    - **Värden:** <*FQDN för central administrations webbplats*>  

    - **Information:** Anger de ca: er som en primär plats kopplas till när den ansluter till Configuration Manager-hierarkin. Ange certifikat utfärdare under installationen.  

- **Nyckelnamn:** CASRetryInterval  

    - **Krävs:** Nej  

    - **Värden:** <*intervall i minuter*>  

    - **Information:** Anger intervallet för återförsök i minuter för att försöka ansluta till CAS när anslutningen Miss lyckas. Om det till exempel inte går att ansluta till CAS, väntar den primära platsen det antal minuter som du anger för **CASRetryInterval** -värdet och försöker sedan ansluta igen.  

- **Nyckelnamn:** WaitForCASTimeout  

    - **Krävs:** Nej  

    - **Värden:** <*timeout i minuter från 0 till 100*>  

    - **Information:** Anger det maximala timeout-värdet i minuter för en primär plats att ansluta till certifikat utfärdarna. Om en primär plats till exempel inte kan ansluta till en certifikat utfärdare, försöker den primära platsen att ansluta till certifikat utfärdarna baserat på värdet **CASRetryInterval** tills **WaitForCASTimeout** -perioden har uppnåtts. Du kan ange ett värde från `0` till `100`.  

#### <a name="cloudconnectoroptions"></a>CloudConnectorOptions

- **Nyckel namn:** CloudConnector  

    - **Krävs:** Ja  

    - **Parametervärden**

        - `0`= Installera inte  

        - `1`= Installera  

    - **Information:** Anger om en tjänst anslutnings punkt ska installeras på den här platsen. Eftersom du bara kan installera tjänst anslutnings punkten på platsen på den översta nivån i en hierarki, ställer du in värdet på `0` för en underordnad primär plats.  

- **Nyckel namn:** CloudConnectorServer  

    - **Krävs:** Krävs när **CloudConnector** är lika med 1  

    - **Värden:** <*serverns FQDN för tjänst anslutnings punkt*\>  

    - **Information:** Anger det fullständiga domän namnet för den server som ska vara värd för tjänst anslutnings punktens plats system roll.  

- **Nyckel namn:** UseProxy  

    - **Krävs:** Krävs när **CloudConnector** är lika med 1  

    - **Parametervärden**

        - `0`= Installera inte  

        - `1`= Installera  

    - **Information:** Anger om tjänst anslutnings punkten använder en proxyserver.  

- **Nyckel namn:** ProxyName  

    - **Krävs:** Krävs när **UseProxy** är lika med 1  

    - **Värden:** <*proxy serverns FQDN*>  

    - **Information:** Anger det fullständiga domän namnet för proxyservern som används av tjänst anslutnings punkten.  

- **Nyckel namn:** ProxyPort  

    - **Krävs:** Krävs när **UseProxy** är lika med 1  

    - **Värden:** <*port nummer*>  

    - **Information:** Anger det port nummer som ska användas för proxyservern.  

#### <a name="sabranchoptions"></a>SABranchOptions

<!-- SCCMDocs#390 -->

- **Nyckel namn:** SAActive

    - **Krävs:** Nej

    - **Parametervärden**

        - `0`= Du har inte Software Assurance

        - `1`= Software Assurance är aktiv

    - **Information:** Ange om du har en aktiv Software Assurance. Mer information finns i [vanliga frågor och svar om produkt och licensiering](../../../understand/product-and-licensing-faq.md).

- **Nyckel namn:** CurrentBranch

    - **Krävs:** Nej

    - **Parametervärden**

        - `0`= Installera LTSB

        - `1`= Installera aktuell gren

    - **Information:** Ange om du vill använda Configuration Manager aktuella grenen eller långtids service grenen (LTSB). Mer information finns i [vilken gren av Configuration Manager ska jag använda?](../../../understand/which-branch-should-i-use.md).

### <a name="unattended-recovery-for-a-cas"></a>Obevakad återställning för en certifikat utfärdare

Använd följande information för att återställa en certifikat utfärdare med hjälp av en obevakad installations skript fil.  

#### <a name="identification"></a>Identification

- **Nyckelnamn:** Action  

    - **Krävs:** Ja  

    - **Värden:**`RecoverCCAR`  

    - **Information:** Återställer en certifikat utfärdare.  

- **Nyckel namn:** CDLatest  

    - **Krävs:** Ja, bara när du använder media från CD: n. Senaste mappen.

    - **Parametervärden**

        - `1`= du använder media från CD. Nya

        - Ett annat värde än 1 = du använder inte CD. Senaste mediet

    - **Information:** När du installerar eller återställer en primär plats eller certifikat utfärdare och kör installations programmet från CD: n. Den senaste mappen inkluderar du den här nyckeln och värdet. Detta värde informerar installations programmet att du använder media från CD. Nya.

#### <a name="recoveryoptions"></a>RecoveryOptions

- **Nyckelnamn:** ServerRecoveryOptions  

    - **Krävs:** Ja  

    - **Parametervärden**

        - `1`= Återställ plats Server och SQL Server

        - `2`= Återställ endast plats Server

        - `4`= Återställ endast SQL Server  

    - **Information:** Anger om installations programmet återställer plats servern, SQL Server eller båda. Följande alternativ krävs också baserat på det angivna värdet:  

        - **1** eller **2**: om du vill återställa platsen med en plats säkerhets kopia anger du ett värde för **nyckeln SiteServerBackupLocation**. Om du inte anger något värde installerar installations programmet om platsen utan att återställa den från en säkerhets kopia.  

        - **4**: **BackupLocation** -nyckeln krävs när du konfigurerar värdet **10** för **nyckeln DatabaseRecoveryOptions** -nyckeln, som är att återställa plats databasen från en säkerhets kopia.  

- **Nyckelnamn:** DatabaseRecoveryOptions  

    - **Krävs:** Den här nyckeln är obligatorisk när inställningen **inställningen ServerRecoveryOptions** har värdet **1** eller **4**.  

    - **Parametervärden**

        - `10`= Återställ plats databasen från en säkerhets kopia.  

        - `20`= Använd en plats databas som du återställde manuellt med en annan metod.  

        - `40`= Skapa en ny databas för platsen. Använd det här alternativet om det inte finns någon säkerhets kopia av plats databasen. Platsen återställer globala data och plats data via replikering från andra platser.  

        - `80`= Hoppa över databas återställning.  

    - **Information:** Anger hur installations programmet återställer plats databasen i SQL Server.  

- **Nyckelnamn:** ReferenceSite  

    - **Krävs:** Den här nyckeln är obligatorisk när inställningen **nyckeln DatabaseRecoveryOptions** har värdet **40**.  

    - **Värden:** <*referens platsens FQDN*>  

    - **Information:** Om säkerhets kopian av databasen är äldre än kvarhållningsperioden för ändrings spårning, eller när du återställer platsen utan en säkerhets kopia, anger du den primära referens platsen som CAS använder för att återställa globala data.  

        Om du inte anger en referens plats och säkerhets kopian är äldre än bevarande perioden för ändrings spårning, initieras alla primära platser om med återställda data från certifikat utfärdarna.  

        När du inte anger en referens plats och säkerhets kopian ligger inom kvarhållningsperioden för ändrings spårning replikeras endast ändringar som görs efter säkerhets kopieringen från primära platser. När det finns motstridiga ändringar från olika primära platser, använder CAS den första som den tar emot.  

- **Nyckelnamn:** SiteServerBackupLocation  

    - **Krävs:** Nej  

    - **Värden:** <*sökväg till plats serverns säkerhets kopia*>  

    - **Information:** Anger sökvägen till den säkerhetskopierade platsservern. Den här nyckeln är valfri när inställningen **ServerRecoveryOptions** har värdet **1** eller **2**. Ange ett värde för nyckeln **SiteServerBackupLocation** för att återställa platsen med hjälp av en säkerhetskopia. Om du inte anger något värde installerar installations programmet om platsen utan att återställa den från en säkerhets kopia.  

- **Nyckelnamn:** BackupLocation  

    - **Krävs:** Den här nyckeln krävs när du konfigurerar ett värde på **1** eller **4** för **inställningen ServerRecoveryOptions** -nyckeln och du konfigurerar värdet **10** för **nyckeln DatabaseRecoveryOptions** -nyckeln.  

    - **Värden:** <*sökväg till säkerhets kopian av plats databasen*>  

    - **Information:** Anger sökvägen till den säkerhetskopierade platsdatabasen.  

#### <a name="options"></a>Alternativ

- **Nyckelnamn:** ProductID  

    - **Krävs:** Ja  

    - **Parametervärden**

        - `<xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>`= en giltig produkt nyckel med streck

        - `Eval`= Installera utvärderings versionen av Configuration Manager

    - **Information:** Anger produkt nyckeln för Configuration Manager installation, inklusive streck.

- **Nyckelnamn:** SiteCode  

    - **Krävs:** Ja  

    - **Värden:** <*platskod*>  

    - **Information:** Anger tre alfanumeriska tecken som unikt identifierar platsen i hierarkin. Ange den platskod som platsen använde före åtgärden.

- **Nyckelnamn:** SiteName  

    - **Krävs:** Nej  

    - **Värden:** <*plats namn*>  

    - **Information:** Anger namnet på den här platsen.  

- **Nyckelnamn:** SMSInstallDir  

    - **Krävs:** Ja  

    - **Värden:** <*Configuration Manager installations Sök väg*>  

    - **Information:** Anger installationsmappen för Configuration Manager program-filerna.  

- **Nyckelnamn:** SDKServer  

    - **Krävs:** Ja  

    - **Värden:** <*SMS-providerns FQDN*>  

    - **Information:** Anger FQDN för den server som är värd för SMS-providern. Ange den server som är värd för SMS-providern före det här problemet.  

        Efter den första installationen kan du konfigurera ytterligare SMS-providrar för platsen. Mer information om SMS-providern finns i [Planera för SMS-providern](../../../plan-design/hierarchy/plan-for-the-sms-provider.md).  

- **Nyckelnamn:** PrerequisiteComp  

    - **Krävs:** Ja  

    - **Parametervärden**

        - `0`= Ladda ned  

        - `1`= Redan nedladdat  

    - **Information:** Anger om nödvändiga filer för installations programmet redan har laddats ned. Om du till exempel använder värdet **0**laddar installations programmet ned filerna.  

- **Nyckelnamn:** PrerequisitePath  

    - **Krävs:** Ja  

    - **Värden:** <*sökväg för att konfigurera nödvändiga filer*>  

    - **Information:** Anger sökvägen till de nödvändiga filerna för installationen. Beroende på **PrerequisiteComp** -värdet använder installations programmet den här sökvägen för att lagra hämtade filer eller för att hitta tidigare hämtade filer.  

- **Nyckelnamn:** AdminConsole  

    - **Krävs:** Den här nyckeln är obligatorisk, förutom när **inställningen ServerRecoveryOptions** -inställningen har värdet **4**.  

    - **Parametervärden**

        - `0`= Installera inte  

        - `1`= Installera  

    - **Information:** Anger om Configuration Manager-konsolen ska installeras eller inte.  

- **Nyckelnamn:** JoinCEIP  

    > [!Note]  
    > Från och med Configuration Manager version 1802, tas CEIP-funktionen bort från produkten.

    - **Krävs:** Ja  

    - **Parametervärden**

        - `0`= Anslut inte  

        - `1`= Anslut  

    - **Information:** Anger om du vill delta i CEIP.  

#### <a name="sqlconfigoptions"></a>SQLConfigOptions

- **Nyckelnamn:** SQLServerName  

    - **Krävs:** Ja  

    - **Värden:** <*SQL Server-namn*>  

    - **Information:** Anger namnet på den server eller klustrade instans som kör SQL Server och som är värd för plats databasen. Ange samma server som är värd för plats databasen före felen.  

- **Nyckelnamn:** DatabaseName  

    - **Krävs:** Ja  

    - **Värden:** <*plats databas namn*> eller <*instans namn*>\\<*plats databas namn*>  

    - **Information:** Anger namnet på SQL Server databasen som ska skapas eller SQL Server databasen som ska användas för att installera CAS-databasen. Ange samma databas namn som användes före det här problemet.  

        > [!IMPORTANT]  
        > Om du inte använder standard instansen anger du instans namn och plats databasens namn.  

- **Nyckelnamn:** SQLSSBPort  

    - **Krävs:** Ja  

    - **Värden:** <*SSB Port Number*>  

    - **Information:** Anger den SSB-port som SQL Server använder. Som standard använder SSB TCP-port 4022. Ange samma SSB-port som användes före det här problemet.  

- **Nyckel namn:** SQLDataFilePath  

    - **Krävs:** Nej  

    - **Värden:** <*sökväg till databasen. mdb-fil*>  

    - **Information:** Anger en alternativ plats för att skapa en databas. mdb-fil.  

- **Nyckel namn:** SQLLogFilePath  

    - **Krävs:** Nej  

    - **Värden:** <*sökväg till databasen. LDF-fil*>  

    - **Information:** Anger en alternativ plats för att skapa en databas. LDF-fil.  

#### <a name="cloudconnectoroptions"></a>CloudConnectorOptions

- **Nyckel namn:** CloudConnector  

    - **Krävs:** Ja  

    - **Parametervärden**

        - `0`= Installera inte  

        - `1`= Installera  

    - **Information:** Anger om en tjänst anslutnings punkt ska installeras på den här platsen. Eftersom du bara kan installera tjänst anslutnings punkten på platsen på den översta nivån i en hierarki, måste värdet vara **0** för en underordnad primär plats.  

- **Nyckel namn:** CloudConnectorServer  

    - **Krävs:** Krävs när **CloudConnector** är lika med 1  

    - **Värden:** <*serverns FQDN för tjänst anslutnings punkt*>  

    - **Information:** Anger det fullständiga domän namnet för den server som ska vara värd för tjänst anslutnings punktens plats system roll.  

- **Nyckel namn:** UseProxy  

    - **Krävs:** Krävs när **CloudConnector** är lika med 1  

    - **Parametervärden**

        - `0`= Installera inte  

        - `1`= Installera  

    - **Information:** Anger om tjänst anslutnings punkten använder en proxyserver.  

- **Nyckel namn:** ProxyName  

    - **Krävs:** Krävs när **CloudConnector** är lika med 1  

    - **Värden:** <*proxy serverns FQDN*>  

    - **Information:** Anger det fullständiga domän namnet för proxyservern som används av tjänst anslutnings punkten.  

- **Nyckel namn:** ProxyPort  

    - **Krävs:** Krävs när **CloudConnector** är lika med 1  

    - **Värden:** <*port nummer*>  

    - **Information:** Anger det port nummer som ska användas för proxyservern.  

### <a name="unattended-recovery-for-a-primary-site"></a>Obevakad återställning för en primär plats

Använd följande information för att återställa en primär plats med hjälp av en obevakad installations skript fil.  

#### <a name="identification"></a>Identification

- **Nyckelnamn:** Action  

    - **Krävs:** Ja  

    - **Värden:**`RecoverPrimarySite`  

    - **Information:** Återställer en primär plats.  

- **Nyckel namn:** CDLatest  

    - **Krävs:** Ja, bara när du använder media från CD: n. Senaste mappen.

    - **Parametervärden**

        - `1`= du använder media från CD. Nya

        - Ett annat värde än 1 = du använder inte CD. Senaste mediet

    - **Information:** När du installerar eller återställer en primär plats eller certifikat utfärdare och kör installations programmet från CD: n. Den senaste mappen inkluderar du den här nyckeln och värdet. Detta värde informerar installations programmet att du använder media från CD. Nya.

#### <a name="recoveryoptions"></a>RecoveryOptions

- **Nyckelnamn:** ServerRecoveryOptions  

    - **Krävs:** Ja  

    - **Parametervärden**

        - `1`= Återställ plats Server och SQL Server

        - `2`= Återställ endast plats Server

        - `4`= Återställ endast SQL Server  

    - **Information:** Anger om installations programmet återställer plats servern, SQL Server eller båda. Följande alternativ krävs också baserat på det angivna värdet:  

        - **1** eller **2**: om du vill återställa platsen med en plats säkerhets kopia anger du ett värde för **nyckeln SiteServerBackupLocation**. Om du inte anger något värde installerar installations programmet om platsen utan att återställa den från en säkerhets kopia.  

        - **4**: **BackupLocation** -nyckeln krävs när du konfigurerar värdet **10** för **nyckeln DatabaseRecoveryOptions** -nyckeln, som är att återställa plats databasen från en säkerhets kopia.  

- **Nyckelnamn:** DatabaseRecoveryOptions  

    - **Krävs:** Den här nyckeln är obligatorisk när inställningen **inställningen ServerRecoveryOptions** har värdet **1** eller **4**.  

    - **Parametervärden**

        - `10`= Återställ plats databasen från en säkerhets kopia.  

        - `20`= Använd en plats databas som du återställde manuellt med en annan metod.  

        - `40`= Skapa en ny databas för platsen. Använd det här alternativet om det inte finns någon säkerhets kopia av plats databasen. Platsen återställer globala data och plats data via replikering från andra platser.  

        - `80`= Hoppa över databas återställning.  

    - **Information:** Anger hur installations programmet återställer plats databasen i SQL Server.  

- **Nyckelnamn:** SiteServerBackupLocation  

    - **Krävs:** Nej  

    - **Värden:** <*sökväg till plats serverns säkerhets kopia*>  

    - **Information:** Anger sökvägen till den säkerhetskopierade platsservern. Den här nyckeln är valfri när inställningen **ServerRecoveryOptions** har värdet **1** eller **2**. Ange ett värde för nyckeln **SiteServerBackupLocation** för att återställa platsen med hjälp av en säkerhetskopia. Om du inte anger något värde installerar installations programmet om platsen utan att återställa den från en säkerhets kopia.  

- **Nyckelnamn:** BackupLocation  

    - **Krävs:** Den här nyckeln krävs när du konfigurerar värdet **1** eller **4** för **inställningen ServerRecoveryOptions** -nyckeln och konfigurerar värdet **10** för **nyckeln DatabaseRecoveryOptions** -nyckeln.  

    - **Värden:** <*sökväg till säkerhets kopian av plats databasen*>  

    - **Information:** Anger sökvägen till den säkerhetskopierade platsdatabasen.  

#### <a name="options"></a>Alternativ

- **Nyckelnamn:** ProductID  

    - **Krävs:** Ja  

    - **Parametervärden**

        - `<xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>`= en giltig produkt nyckel med streck

        - `Eval`= Installera utvärderings versionen av Configuration Manager

    - **Information:** Anger produkt nyckeln för Configuration Manager installation, inklusive streck.

- **Nyckelnamn:** SiteCode  

    - **Krävs:** Ja  

    - **Värden:** <*platskod*>  

    - **Information:** Anger tre alfanumeriska tecken som unikt identifierar platsen i hierarkin. Ange den platskod som platsen använde före åtgärden.

- **Nyckelnamn:** SiteName  

    - **Krävs:** Nej  

    - **Värden:** <*plats namn*>  

    - **Information:** Anger namnet på den här platsen.  

- **Nyckelnamn:** SMSInstallDir  

    - **Krävs:** Ja  

    - **Värden:** <*Configuration Manager installations Sök väg*>  

    - **Information:** Anger installationsmappen för Configuration Manager program-filerna.  

- **Nyckelnamn:** SDKServer  

    - **Krävs:** Ja  

    - **Värden:** <*SMS-providerns FQDN*>  

    - **Information:** Anger FQDN för den server som är värd för SMS-providern. Ange den server som är värd för SMS-providern före det här problemet. Efter den första installationen kan du konfigurera ytterligare SMS-providrar för platsen. Mer information om SMS-providern finns i [Planera för SMS-providern](../../../plan-design/hierarchy/plan-for-the-sms-provider.md).  

- **Nyckelnamn:** PrerequisiteComp  

    - **Krävs:** Ja  

    - **Parametervärden**

        - `0`= Ladda ned  

        - `1`= Redan nedladdat  

    - **Information:** Anger om nödvändiga filer för installations programmet redan har laddats ned. Om du till exempel använder värdet **0**laddar installations programmet ned filerna.  

- **Nyckelnamn:** PrerequisitePath  

    - **Krävs:** Ja  

    - **Värden:** <*sökväg för att konfigurera nödvändiga filer*>  

    - **Information:** Anger sökvägen till de nödvändiga filerna för installationen. Beroende på **PrerequisiteComp** -värdet använder installations programmet den här sökvägen för att lagra hämtade filer eller för att hitta tidigare hämtade filer.  

- **Nyckelnamn:** AdminConsole  

    - **Krävs:** Den här nyckeln är obligatorisk, förutom när **inställningen ServerRecoveryOptions** -inställningen har värdet **4**.  

    - **Parametervärden**

        - `0`= Installera inte  

        - `1`= Installera  

    - **Information:** Anger om Configuration Manager-konsolen ska installeras eller inte.  

- **Nyckelnamn:** JoinCEIP  

    > [!Note]  
    > Från och med Configuration Manager version 1802, tas CEIP-funktionen bort från produkten.

    - **Krävs:** Ja  

    - **Parametervärden**

        - `0`= Anslut inte  

        - `1`= Anslut  

    - **Information:** Anger om du vill delta i CEIP.  

#### <a name="sqlconfigoptions"></a>SQLConfigOptions

- **Nyckelnamn:** SQLServerName  

    - **Krävs:** Ja  

    - **Värden:** <*SQL Server-namn*>  

    - **Information:** Anger namnet på den server eller klustrade instans som kör SQL Server som värd för plats databasen. Ange samma server som är värd för plats databasen före felen.  

- **Nyckelnamn:** DatabaseName  

    - **Krävs:** Ja  

    - **Värden:** <*plats databas namn*> eller <*instans namn*>\\<*plats databas namn*>

    - **Information:** Anger namnet på SQL Server databasen som ska skapas eller SQL Server databasen som ska användas för att installera CAS-databasen. Ange samma databas namn som användes före det här problemet.  

        > [!IMPORTANT]  
        > Om du inte använder standard instansen anger du instans namn och plats databasens namn.  

- **Nyckelnamn:** SQLSSBPort  

    - **Krävs:** Ja  

    - **Värden:** <*SSB Port Number*>  

    - **Information:** Anger den SSB-port som SQL Server använder. Som standard använder SSB TCP-port 4022. Ange samma SSB-port som användes före det här problemet.  

- **Nyckel namn:** SQLDataFilePath  

    - **Krävs:** Nej  

    - **Värden:** <*sökväg till databasen. mdb-fil*>  

    - **Information:** Anger en alternativ plats för att skapa en databas. mdb-fil.  

- **Nyckel namn:** SQLLogFilePath  

    - **Krävs:** Nej  

    - **Värden:** <*sökväg till databasen. LDF-fil*>  

    - **Information:** Anger en alternativ plats för att skapa en databas. LDF-fil.  

#### <a name="hierarchyexpansionoptions"></a>HierarchyExpansionOptions

- **Nyckelnamn:** CCARSiteServer  

    - **Krävs:** Se information.  

    - **Värden:** <*Platskod för certifikat utfärdare*>  

    - **Information:** Anger de ca: er som en primär plats kopplas till när den ansluter till Configuration Manager-hierarkin. Den här inställningen är obligatorisk om den primära platsen har kopplats till en CAS före felet. Ange den platskod som användes för certifikat utfärdarna före felen.  

- **Nyckelnamn:** CASRetryInterval  

    - **Krävs:** Nej  

    - **Värden:** <*intervall i minuter*>  

    - **Information:** Anger intervallet för återförsök i minuter för att försöka ansluta till CAS när anslutningen Miss lyckas. Om det till exempel inte går att ansluta till CAS, väntar den primära platsen det antal minuter som du anger för **CASRetryInterval** -värdet och försöker sedan ansluta igen.  

- **Nyckelnamn:** WaitForCASTimeout  

    - **Krävs:** Nej  

    - **Värden:** <*timeout i minuter*>  

    - **Information:** Anger det maximala timeout-värdet i minuter för en primär plats att ansluta till certifikat utfärdarna. Om en primär plats till exempel inte kan ansluta till en certifikat utfärdare, försöker den primära platsen att ansluta till certifikat utfärdarna baserat på värdet **CASRetryInterval** tills **WaitForCASTimeout** -perioden har uppnåtts. Du kan ange värdet `0` till. `100`  

#### <a name="cloudconnectoroptions"></a>CloudConnectorOptions

- **Nyckel namn:** CloudConnector  

    - **Krävs:** Ja  

    - **Parametervärden**

        - `0`= Installera inte  

        - `1`= Installera  

    - **Information:** Anger om en tjänst anslutnings punkt ska installeras på den här platsen. Eftersom du bara kan installera tjänst anslutnings punkten på platsen på den översta nivån i en hierarki måste det här värdet vara `0` för en underordnad primär plats.  

- **Nyckel namn:** CloudConnectorServer  

    - **Krävs:** Krävs när **CloudConnector** är lika med 1  

    - **Värden:** <*serverns FQDN för tjänst anslutnings punkt*>  

    - **Information:** Anger det fullständiga domän namnet för den server som ska vara värd för tjänst anslutnings punktens plats system roll.  

- **Nyckel namn:** UseProxy  

    - **Krävs:** Krävs när **CloudConnector** är lika med 1  

    - **Parametervärden**

        - `0`= Installera inte  

        - `1`= Installera  

    - **Information:** Anger om tjänst anslutnings punkten använder en proxyserver.  

- **Nyckel namn:** ProxyName  

    - **Krävs:** Krävs när **CloudConnector** är lika med 1  

    - **Värden:** <*proxy serverns FQDN*>  

    - **Information:** Anger det fullständiga domän namnet för proxyservern som används av tjänst anslutnings punkten.  

- **Nyckel namn:** ProxyPort  

    - **Krävs:** Krävs när **CloudConnector** är lika med 1  

    - **Värden:** <*port nummer*>  

    - **Information:** Anger det port nummer som ska användas för proxyservern.  
