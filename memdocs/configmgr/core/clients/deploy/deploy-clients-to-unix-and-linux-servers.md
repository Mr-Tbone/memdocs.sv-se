---
title: Distribuera UNIX/Linux-klienter
titleSuffix: Configuration Manager
description: Lär dig hur du distribuerar en-klient till en UNIX-eller Linux-server i Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 15a4e323-9f42-4fea-bb14-f2b905d1f77c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c9e8e40a6bdfa129a03e6042985e4956ffb21b5c
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906319"
---
# <a name="how-to-deploy-clients-to-unix-and-linux-servers-in-configuration-manager"></a>Distribuera klienter till UNIX-och Linux-servrar i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

> [!Important]  
> Från och med version 1902 stöder Configuration Manager inte Linux-eller UNIX-klienter. 
> 
> Överväg Microsoft Azure hantering för hantering av Linux-servrar. Azure-lösningar har omfattande Linux-support som i de flesta fall överskrider Configuration Manager-funktioner, inklusive slut punkt till slut punkt för korrigerings hantering för Linux.


Innan du kan hantera en Linux-eller UNIX-server med Configuration Manager måste du installera Configuration Manager-klienten för Linux och UNIX på varje Linux-eller UNIX-server. Du kan utföra installationen av klienten manuellt på varje dator eller använda ett kommandoskript som installerar klienten via en fjärranslutning. Configuration Manager stöder inte användning av push-installation av klienter för Linux-eller UNIX-servrar. Du kan också konfigurera en Runbook för System Center Orchestrator för att automatisera installation av klienten på Linux- eller UNIX-servern.  

 Oavsett vilken installationsmetod du använder krävs ett skript som heter **install** för att hantera installationen. Det här skriptet ingår när du hämtar klienten för Linux och UNIX.  

 Installations skriptet för Configuration Manager-klienten för Linux och UNIX stöder kommando rads egenskaper. Vissa kommando rads egenskaper är obligatoriska, medan andra är valfria. När du installerar klienten måste du till exempel ange en hanteringsplats från den plats som används av Linux- eller UNIX-servern för den första kontakten med platsen. En fullständig lista över kommando rads egenskaper finns i [kommando rads egenskaper för att installera klienten på Linux-och UNIX-servrar](#BKMK_CmdLineInstallLnUClient).  

 När du har installerat-klienten anger du klient inställningar i Configuration Manager-konsolen för att konfigurera klient agenten på samma sätt som Windows-baserade klienter. Mer information finns i  [Klientinställningar för Linux- och UNIX-servrar](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ClientSettingsforLnU).  

##  <a name="about-client-installation-packages-and-the-universal-agent"></a><a name="BKMK_AboutInstallPackages"></a>Om klient installations paket och Universal Agent  
 Om du vill installera klienten för Linux och UNIX på en viss plattform måste du använda lämpligt klientinstallationspaket för datorn där du installerar klienten. Lämpliga klientinstallationspaket ingår som en del av varje klientnedladdning från [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=47719). Utöver klientinstallationspaketen omfattar klientnedladdningen **install** -skriptet som hanterar installationen av klienten på varje dator.  

 När du installerar en-klient kan du använda samma process och kommando rads egenskaper oavsett vilket klient installations paket du använder.  

 Information om operativ system, plattformar och klient installations paket som stöds av varje version av Configuration Manager-klienten för Linux och UNIX finns i [Linux-och UNIX-servrar](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#linux-and-unix-servers).  

##  <a name="install-the-client-on-linux-and-unix-servers"></a><a name="BKMK_InstallLnUClient"></a>Installera klienten på Linux-och UNIX-servrar  
 Om du vill installera klienten för Linux och UNIX kör du ett skript på varje Linux- eller UNIX-dator. Skriptet heter **Installera** och stöder kommando rads egenskaper som ändrar installations beteendet och hänvisar till klient installations paketet. Installationsskriptet och klientinstallationspaketet måste finnas på klienten. Klient installations paketet innehåller Configuration Manager-klientdatorer för ett särskilt operativ system och plattform för Linux eller UNIX.
Varje klient installations paket innehåller alla filer som krävs för att slutföra klient installationen och till skillnad från Windows-baserade datorer, hämtar inte ytterligare filer från en hanterings plats eller annan käll plats.  

 När du har installerat Configuration Manager-klienten för Linux och UNIX behöver du inte starta om datorn. Så snart programvaruinstallationen är klar är klienten redo för användning. Om du startar om datorn startas Configuration Manager klienten om automatiskt.  

 Den installerade klienten körs med rotautentiseringsuppgifter. Autentiseringsuppgifter för roten krävs för att samla in maskin varu inventering och utföra program varu distributioner.  

 Använd följande kommando format:  

 `./install -mp <computer> -sitecode <sitecode> <property #1> <property #2> <client installation package>`  

-   `install`är namnet på den skript fil som installerar-klienten för Linux och UNIX. Filen tillhandahålls med klientprogramvaran.  

-   `-mp <computer>`anger den första hanterings platsen som används av klienten. Exempel: `smsmp.contoso.com`  

-   `-sitecode <site code>`anger den platskod som klienten är tilldelad till. Exempel: `S01`  

-   `<property #1> <property #2>`anger de kommando rads egenskaper som ska användas med installations skriptet.  

    > [!NOTE]  
    >  Mer information finns i [kommando rads egenskaper för att installera-klienten på Linux-och UNIX-servrar](#BKMK_CmdLineInstallLnUClient).  

-   **client installation package** är namnet på .tar-paketet för installationspaketet för denna version av datorns operativsystem, version och processorarkitektur. Klientinstallationens .tar-fil måste anges sist. Exempel: `ccm-Universal-x64.<build>.tar`  

###  <a name="to-install-the-configuration-manager-client-on-linux-and-unix-servers"></a><a name="BKMK_ToInstallLnUClinent"></a>Så här installerar du Configuration Manager-klienten på Linux-och UNIX-servrar  

1.  På en Windows-dator [hämtar du lämplig klientfil för den Linux- eller UNIX-server](https://www.microsoft.com/download/details.aspx?id=47719) som du vill hantera.  

2.  Kör den självextraherande .exe-filen på Windows-datorn för att extrahera installationsskriptet och .tar-filen för klientinstallation.  

3.  Kopiera skriptet **install** och .tar-filen till en mapp på den server som du vill hantera.  

4.  På UNIX-eller Linux-servern kör du följande kommando för att göra det möjligt för skriptet att köras som ett program:`chmod +x install`  

    > [!IMPORTANT]  
    >  Du måste använda rotautentiseringsuppgifter för att installera klienten.  

5.  Kör sedan följande kommando för att installera Configuration Manager-klienten:`./install -mp <hostname> -sitecode <code> ccm-Universal-x64.<build>.tar`  

     När du anger det här kommandot använder du ytterligare kommandoradsegenskaper som du behöver. En lista över kommando rads egenskaper finns i [kommando rads egenskaper för att installera klienten på Linux-och UNIX-servrar](#BKMK_CmdLineInstallLnUClient)  

6.  När skriptet har körts validerar du installationen genom att granska filen **/var/opt/microsoft/scxcm.log** . Dessutom kan du bekräfta att-klienten är installerad och att den kommunicerar med platsen genom att visa information om klienten i noden **enheter** i arbets ytan **till gångar och efterlevnad** i Configuration Manager-konsolen.  

###  <a name="command-line-properties-for-installing-the-client-on-linux-and-unix-servers"></a><a name="BKMK_CmdLineInstallLnUClient"></a>Kommando rads egenskaper för att installera klienten på Linux-och UNIX-servrar  
 Följande egenskaper är tillgängliga för att ändra beteendet för installations skriptet:  

> [!NOTE]  
>  Använd egenskapen `-h` för att visa den här listan över egenskaper som stöds.  

-   `-mp <server FQDN>`  

     Krävs. Anger efter FQDN, hanterings plats servern som klienten använder som en första kontakt punkt.  

    > [!IMPORTANT]  
    >  Den här egenskapen anger inte den hanterings plats som klienten är tilldelad efter installationen.  

    > [!NOTE]  
    >  När du använder `-mp` egenskapen för att ange en hanterings plats som är konfigurerad för att endast godkänna HTTPS-klientanslutningar måste du också använda `-UsePKICert` egenskapen.  

-   `-sitecode <sitecode>`  

     Krävs. Anger Configuration Manager primära platsen som Configuration Manager klienten ska tilldelas till. Exempel: `-sitecode S01`  

-   `-fsp <server_FQDN>`  

     Valfritt. Anger efter FQDN den återställningsstatuspunktserver som klienten använder för att skicka statusmeddelanden. Mer information finns i [avgöra om du behöver en återställnings status plats](plan/determine-the-site-system-roles-for-clients.md#fallback-status-point).  

-   `-dir <directory>`  

     Valfritt. Anger en alternativ plats för att installera Configuration Manager-klientens filer. Som standard installeras-klienten på följande plats:`/opt/microsoft`  

-   `-nostart`  

     Valfritt. Förhindrar automatisk start av Configuration Manager-klienttjänsten, **ccmexec. bin**, efter att klient installationen har slutförts.  

     När klienten har installerats kan du starta klienttjänsten manuellt.  

     Klienttjänsten startar som standard efter att klientinstallationen har slutförts och varje gång datorn startas om.  

-   `-clean`  

     Valfritt. Anger borttagning av alla klientfiler och data från en tidigare installerad klient för Linux och UNIX innan den nya installationen börjar. Den här åtgärden tar bort klientens databas och certifikat arkiv.  

-   `-keepdb`  

     Valfritt. Anger att den lokala klient databasen behålls och återanvänds när du installerar om en klient. När du installerar om en klient tas den här databasen bort som standard.  

-   `-UsePKICert <parameter>`  

     Valfritt. Anger den fullständiga sökvägen och filnamnet för ett X.509 PKI-certifikat i Public Key Certificate Standard-format (PKCS#12). Det här certifikatet används för klientautentisering. Om ett certifikat inte har angetts under installationen och du behöver lägga till eller ändra ett certifikat använder du verktyget **certutil** . Mer information finns i [Hantera certifikat på klienten för Linux och UNIX](../manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ManageLinuxCerts).  

     När du använder `-UsePKICert` måste du också ange lösen ordet som är kopplat till PKCS # 12-filen med hjälp av `-certpw` kommando rads parametern.  

     Om du inte använder den här egenskapen för att ange ett PKI-certifikat använder klienten ett självsignerat certifikat och all kommunikation till plats systemen är över HTTP.  

     Inga fel returneras om du anger ett ogiltigt certifikat på klientens kommandorad för installation. Certifikat verifieringen sker efter att klienten har installerats. När klienten startas val IDE ras certifikaten med hanterings platsen. Om ett certifikat inte kan verifieras visas följande meddelande i **scxcm. log**: **Det gick inte att validera certifikatet för hanterings platsen**. Standardplatsen för loggfilen är  **/var/opt/microsoft/scxcm.log**.  

     > [!NOTE]  
     > Du måste ange den här egenskapen när du installerar en klient och använder `-mp` egenskapen för att ange en hanterings plats som har kon figurer ATS för att endast godkänna HTTPS-klientanslutningar.  

     Exempel: `-UsePKICert <full path and filename> -certpw <password>`  

-   `-certpw <parameter>`  

     Valfritt. Anger det lösen ord som är kopplat till PKCS # 12-filen som du angav genom att använda `-UsePKICert` egenskapen.  

     Exempel: `-UsePKICert <full path and filename> -certpw <password>`  

-   `-NoCRLCheck`  

     Valfritt. Anger att en klient inte ska kontrol lera listan över återkallade certifikat (CRL) när den kommunicerar via HTTPS genom att använda ett PKI-certifikat. När det här alternativet inte anges kontrollerar klienten listan över återkallade certifikat innan en HTTPS-anslutning upprättas med hjälp av PKI-certifikat. Mer information om klientens kontroll av listan över återkallade certifikat finns i Planera för att återkalla PKI-certifikat.  

     Exempel: `-UsePKICert <full path and filename> -certpw <password> -NoCRLCheck`  

-   `-rootkeypath <file location>`  

     Valfritt. Anger den fullständiga sökvägen och fil namnet till den betrodda rot nyckeln för Configuration Manager. Den Configuration Manager betrodda rot nyckeln är en mekanism som Linux-och UNIX-klienter använder för att kontrol lera att de är anslutna till ett plats system som tillhör rätt hierarki.  

     Om du inte anger den betrodda rot nyckeln på kommando raden litar klienten på den första hanterings platsen som den kommunicerar med och hämtar automatiskt den betrodda rot nyckeln från den hanterings platsen.  

     Mer information finns i  [Planera för den betrodda rotnyckeln](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

     Exempel: `-rootkeypath <full path and filename>`  

-   `-httpport <port>`  

     Valfritt. Anger den port som är konfigurerad på hanteringsplatser som klienten använder vid kommunikation med hanteringsplatser över HTTP. Om porten inte anges används standardvärdet 80.  

     Exempel: `-httpport 80`  

-   `-httpsport <port>`  

     Valfritt. Anger den port som är konfigurerad på hanteringsplatser som klienten använder vid kommunikation med hanteringsplatser över HTTPS. Om porten inte anges används standardvärdet 443.  

     Exempel: `-UsePKICert <full path and certificate name> -httpsport 443`  

-   `-ignoreSHA256validation`  

     Valfritt. Anger att klientinstallationen hoppar över SHA-256-verifiering. Använd det här alternativet när du installerar klienten på operativ system som inte släpptes med en version av OpenSSL som har stöd för SHA-256. Mer information finns i [om Linux-och UNIX-operativsystem som inte stöder SHA-256](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_NoSHA-256).  

-   `-signcertpath <file location>`  

     Valfritt. Anger den fullständiga sökvägen och **. cer** -fil namnet på det exporterade självsignerade certifikatet på plats servern. Om PKI-certifikat inte är tillgängliga genererar Configuration Manager plats servern automatiskt självsignerade certifikat.  

     Dessa certifikat används för att verifiera att klientprinciperna som hämtats från hanteringsplatsen skickades från den avsedda platsen. Om ett självsignerat certifikat inte har angetts under installationen eller om du behöver ändra certifikatet använder du verktyget **certutil** . Mer information finns i [Hantera certifikat på klienten för Linux och UNIX](../manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ManageLinuxCerts).  

     Det här certifikatet kan hämtas från **SMS** -certifikatarkivet och har mottagarnamnet **Platsserver** och det egna namnet **Signeringscertifikat för platsserver**.  

     Om det här alternativet inte anges under installationen litar Linux-och UNIX-klienter på den första hanterings platsen som de kommunicerar med. De hämtar automatiskt signerings certifikatet från den hanterings platsen.  

     Exempel: `-signcertpath <full path and file name>`  

-   `-rootcerts`  

     Valfritt. Anger ytterligare PKI-certifikat att importera som inte ingår i en CA-hierarki (Management Points Certificate Authority). Om du anger flera certifikat på kommandoraden ska de vara kommaavgränsade.  

     Använd det här alternativet om du använder PKI-klientcertifikat som inte är kedjade till ett rot certifikat för certifikat utfärdare som är betrodda av plats hanterings platserna. Hanterings platser avvisar klienten om klient certifikatet inte är kedja till ett betrott rot certifikat i platsens lista över certifikat utfärdare.  

     Om du inte använder det här alternativet verifierar Linux-och UNIX-klienten den betrodda hierarkin med bara certifikatet i `-UsePKICert` alternativet.  

     Exempel: `-rootcerts <full path and file name>,<full path and file name>`  

###  <a name="uninstalling-the-client-from-linux-and-unix-servers"></a><a name="BKMK_UninstallLnUClient"></a>Avinstallera klienten från Linux-och UNIX-servrar  
 Om du vill avinstallera Configuration Manager-klienten för Linux och UNIX använder du avinstallations verktyget **Uninstall**. Den här filen finns som standard i mappen **/opt/microsoft/configmgr/bin/** på klientdatorn. Detta avinstallations kommando har inte stöd för kommando rads parametrar och tar bort alla filer som är relaterade till klient programmet från servern.  

 Om du vill avinstallera en klient använder du följande kommandorad: **/opt/microsoft/configmgr/bin/uninstall**  

 Du behöver inte starta om datorn när du har avinstallerat Configuration Manager-klienten för Linux och UNIX.  

##  <a name="configure-request-ports-for-the-client-for-linux-and-unix"></a><a name="BKMK_ConfigLnUClientCommuincations"></a> Konfigurera begärandeportar för klienten för Linux och UNIX  
 På samma sätt som Windows-baserade klienter använder Configuration Manager-klienten för Linux och UNIX HTTP och HTTPS för att kommunicera med Configuration Manager-plats system. De portar som den Configuration Manager klienten använder för att kommunicera kallas begär ande portar.  

 När du installerar Configuration Manager-klienten för Linux och UNIX kan du ändra klientens standard begär ande portar genom att ange installations egenskaperna **-HttpPort** och **-HttpsPort** . Om du inte anger installations egenskapen och ett anpassat värde använder klienten standardvärdena. Standardvärdena är **80** för HTTP-trafik och **443** för HTTPS-trafik.  

 När du har installerat-klienten kan du inte ändra konfigurationen för den begär ande porten. Om du vill ändra portkonfigurationen måste du i stället installera om klienten och ange den nya portkonfigurationen. När du installerar om klienten för att ändra begär ande port nummer, kör du kommandot **Installera** som liknar den nya klient installationen, men använder den ytterligare kommando rads egenskapen för **-keepdb**. Den här växeln instruerar installationen att behålla klient databasen och filerna, inklusive klient-GUID och certifikat arkiv.  

 Mer information om port nummer för klient kommunikation finns i [så här konfigurerar du klient kommunikations portar](../../../core/clients/deploy/configure-client-communication-ports.md).  

##  <a name="configure-the-client-for-linux-and-unix-to-locate-management-points"></a><a name="BKMK_ConfigClientMP"></a> Konfigurera klienten för Linux och UNIX för att hitta hanteringsplatser  
 När du installerar Configuration Manager-klienten för Linux och UNIX måste du ange en hanterings plats som ska användas som första kontakt punkt.  

 Configuration Manager-klienten för Linux och UNIX kontaktar den här hanterings platsen när klienten installeras. Om klienten inte kan kontakta hanteringsplatsen fortsätter klientprogrammet att försöka tills det lyckas.  

 Mer information om hur klienter hittar hanteringsplatser finns i [Hitta hanteringsplatser](assign-clients-to-a-site.md#locating-management-points).
