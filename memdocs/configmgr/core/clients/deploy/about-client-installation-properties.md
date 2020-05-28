---
title: Parametrar och egenskaper för klient installation
titleSuffix: Configuration Manager
description: Lär dig mer om kommando rads parametrar och egenskaper för CCMSetup för att installera Configuration Manager-klienten.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: c890fd27-7a8c-4f51-bbe2-f9908af1f42b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6ccfb523cc1abc3a64d396f32d55a4dc4551987c
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428600"
---
# <a name="about-client-installation-parameters-and-properties-in-configuration-manager"></a>Om parametrar och egenskaper för klient installation i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Använd kommandot CCMSetup. exe för att installera Configuration Manager-klienten. Om du anger klient installations *parametrar* på kommando raden ändrar de installations beteendet. Om du anger klient installations *Egenskaper* på kommando raden, ändrar de den inledande konfigurationen för den installerade klient agenten.

## <a name="about-ccmsetupexe"></a><a name="aboutCCMSetup"></a> Om CCMSetup.exe

Kommandot CCMSetup. exe laddar ned filer som behövs för att installera klienten från en hanterings plats eller en käll plats. De här filerna kan vara:  

- Den Windows Installer Package client. msi som installerar-klient program varan

- Klient krav

- Uppdateringar och korrigeringar för den Configuration Manager klienten

> [!NOTE]
> Du kan inte installera client. msi direkt.  

CCMSetup. exe innehåller kommando rads *parametrar* för att anpassa installationen. Parametrar föregås av ett snedstreck ( `/` ) och enligt praxis är gemener. Du anger värdet för en parameter när det behövs med ett kolon ( `:` ) omedelbart följt av värdet. Mer information finns i [kommando rads parametrar för CCMSetup. exe](#ccmsetupexe-command-line-parameters).

Du kan också ange *Egenskaper* på kommando raden för CCMSetup. exe för att ändra funktions sättet för Client. msi. egenskaper efter konvention är versaler. Du anger ett värde för en egenskap med ett likhets tecken ( `=` ) omedelbart följt av värdet. Mer information finns i [client. msi-egenskaper](#clientMsiProps).

> [!IMPORTANT]  
> Ange CCMSetup-parametrar innan du anger egenskaper för Client. msi.  

CCMSetup. exe och stödfilerna finns på plats servern i mappen **klient** i mappen Configuration Manager-installation. Configuration Manager delar den här mappen i nätverket under plats resursen. Till exempel `\\SiteServer\SMS_ABC\Client`.

I kommandotolken används följande format i CCMSetup.exe-kommandot:  

`CCMSetup.exe [<Ccmsetup parameters>] [<client.msi setup properties>]`  

Ett exempel:  

`CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=S01 FSP=SMSFSP01`  

Det här exemplet gör följande:  

- Anger hanterings platsen med namnet SMSMP01 för att begära en lista över distributions platser för att hämta klientens installationsfiler.  

- Anger att installationen ska avbrytas om det redan finns en version av klienten på datorn.  

- Instruerar client.msi att tilldela klienten platskoden S01.  

- Instruerar client.msi att använda återställningsstatuspunkten med namnet SMSFP01.  

> [!TIP]  
> Om ett parameter värde innehåller blank steg omger du det med citat tecken.  

Om du utökar Active Directory-schemat för Configuration Manager publicerar platsen många klient installations egenskaper i Active Directory Domain Services. Den Configuration Manager klienten läser automatiskt dessa egenskaper. Mer information finns i [om klient installations egenskaper som publiceras till Active Directory Domain Services](about-client-installation-properties-published-to-active-directory-domain-services.md)  

## <a name="ccmsetupexe-command-line-parameters"></a>Kommando rads parametrar för CCMSetup. exe

### <a name=""></a><a name="bkmk_help"></a> /?

Visar tillgängliga kommando rads parametrar för CCMSetup. exe.  

Exempel: `ccmsetup.exe /?`

### <a name="source"></a>/source

Anger fil hämtnings platsen. Använd en lokal sökväg eller UNC-sökväg. Enheten laddar ned filer med SMB-protokollet (Server Message Block). Om du vill använda **/Source**måste Windows-användarkontot för klient installationen ha **Läs** behörighet till platsen.

> [!TIP]  
> Du kan använda parametern **/Source** mer än en gång på en kommando rad för att ange alternativa hämtnings platser.  

Exempel: `ccmsetup.exe /source:"\\server\share"`

### <a name="mp"></a>/MP

Anger en käll hanterings plats för datorer att ansluta till. Datorer använder den här hanterings platsen för att hitta den närmaste distributions platsen för installationsfilerna. Om det inte finns några distributions platser eller om datorerna inte kan ladda ned filerna från distributions platserna efter fyra timmar, laddar de ned filerna från den angivna hanterings platsen.  

> [!IMPORTANT]  
> Den här parametern anger en första hanterings plats för datorer för att hitta en nedladdnings källa och kan vara vilken hanterings plats som helst på alla platser. Den *tilldelar* inte klienten till den angivna hanterings platsen.

Filerna laddas ned till datorerna över en HTTP- eller HTTPS-anslutning, beroende på platssystemrollens klientanslutningskonfiguration. Hämtningen kan också använda BITS-begränsning om du konfigurerar den. Om du bara konfigurerar alla distributions platser och hanterings platser för HTTPS-klientanslutningar kontrollerar du att klient datorn har ett giltigt klient certifikat.  

Du kan använda kommando rads parametern **/MP** för att ange fler än en hanterings plats. Om datorn inte kan ansluta till den första, försöker den härnäst i den angivna listan. Separera värdena med semikolon när du anger flera hanterings platser.

Om klienten ansluter till en hanterings plats med hjälp av HTTPS anger du FQDN inte dator namnet. Värdet måste matcha hanterings platsens PKI-certifikatets **ämne** eller **Alternativt namn för certifikat mottagare**. Även om Configuration Manager stöder användning av ett dator namn i certifikatet för anslutningar på intranätet, rekommenderas att du använder ett fullständigt domän namn.

Exempel med dator namn:`ccmsetup.exe /mp:SMSMP01`  

Exempel med FQDN:`ccmsetup.exe /mp:smsmp01.contoso.com`  

Den här parametern kan också ange URL: en för en CMG (Cloud Management Gateway). Använd den här URL: en för att installera-klienten på en Internetbaserad enhet. Använd följande steg för att hämta värdet för den här parametern:

- Skapa en CMG. Mer information finns i [Konfigurera en CMG](../manage/cmg/setup-cloud-management-gateway.md).
- Öppna en Windows PowerShell-kommandotolk som administratör på en aktiv klient.
- Kör följande kommando:

    ```PowerShell
    (Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}).MP
    ```

- Lägg till `https://` prefixet som ska användas med **/MP** -parametern.

Exempel för när du använder URL: en för Cloud Management Gateway:`ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057598037248100`

> [!Important]
> När du anger URL: en för en moln hanterings-Gateway för **/MP** -parametern måste den börja med `https://` .

### <a name="regtoken"></a>/regtoken

<!--5686290-->

Från och med version 2002 använder du den här parametern för att ange en token för Mass registrering. En Internetbaserad enhet använder denna token i registrerings processen via en Cloud Management Gateway (CMG). Mer information finns i [tokenbaserad autentisering för CMG](deploy-clients-cmg-token.md).

När du använder den här parametern inkluderar du även följande parametrar och egenskaper:

- [**/MP**](#mp)
- [**CCMHOSTNAME**](#ccmhostname)
- [**SMSSiteCode**](#smssitecode)
- [**SMSMP**](#smsmp)

Följande exempel på kommando raden innehåller andra obligatoriska konfigurations parametrar och egenskaper:

`ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC SMSMP=https://mp1.contoso.com /regtoken:eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik9Tbzh2Tmd5VldRUjlDYVh5T2lacHFlMDlXNCJ9.eyJTQ0NNVG9rZW5DYXRlZ29yeSI6IlN7Q01QcmVBdXRoVG9rZW4iLCJBdXRob3JpdHkiOiJTQ0NNIiwiTGljZW5zZSI6IlNDQ00iLCJUeXBlIjoiQnVsa1JlZ2lzdHJhdGlvbiIsIlRlbmFudElkIjoiQ0RDQzVFOTEtMEFERi00QTI0LTgyRDAtMTk2NjY3RjFDMDgxIiwiVW5pcXVlSWQiOiJkYjU5MWUzMy1wNmZkLTRjNWItODJmMy1iZjY3M2U1YmQwYTIiLCJpc3MiOiJ1cm46c2NjbTpvYXV0aDI6Y2RjYzVlOTEtMGFkZi00YTI0LTgyZDAtMTk2NjY3ZjFjMDgxIiwiYXVkIjoidXJuOnNjY206c2VydmljZSIsImV4cCI6MTU4MDQxNbUwNSwibmJmIjoxNTgwMTU2MzA1fQ.ZUJkxCX6lxHUZhMH_WhYXFm_tbXenEdpgnbIqI1h8hYIJw7xDk3wv625SCfNfsqxhAwRwJByfkXdVGgIpAcFshzArXUVPPvmiUGaxlbB83etUTQjrLIk-gvQQZiE5NSgJ63LCp5KtqFCZe8vlZxnOloErFIrebjFikxqAgwOO4i5ukJdl3KQ07YPRhwpuXmwxRf1vsiawXBvTMhy40SOeZ3mAyCRypQpQNa7NM3adCBwUtYKwHqiX3r1jQU0y57LvU_brBfLUL6JUpk3ri-LSpwPFarRXzZPJUu4-mQFIgrMmKCYbFk3AaEvvrJienfWSvFYLpIYA7lg-6EVYRcCAA`

### <a name="retry"></a>/retry

Om CCMSetup. exe inte kan ladda ned installationsfiler använder du den här parametern för att ange återförsöksintervall i minuter. CCMSetup fortsätter att försöka igen tills det når gränsen som anges i parametern [**/downloadtimeout**](#downloadtimeout) .

Exempel: `ccmsetup.exe /retry:20`  

### <a name="noservice"></a>/noservice

Den här parametern förhindrar att CCMSetup körs som en tjänst, vilket den gör som standard. När CCMSetup körs som en tjänst körs den i kontexten för det lokala system kontot på datorn. Det här kontot kanske inte har behörighet att komma åt nödvändiga nätverks resurser för installationen. Med **/noservice**körs CCMSetup. exe i kontexten för det användar konto som du använder för att starta installationen.

Exempel: `ccmsetup.exe /noservice`  

### <a name="service"></a>/service

Anger att CCMSetup ska köras som en tjänst som använder det lokala system kontot.  

> [!TIP]
> Om du använder ett skript för att köra CCMSetup. exe med parametern **/service** avslutas CCMSetup. exe när tjänsten har startats. Det kanske inte rapporterar installations information till skriptet korrekt.

Exempel: `ccmsetup.exe /service`  

### <a name="uninstall"></a>/uninstall

Använd den här parametern om du vill avinstallera Configuration Manager-klienten. Mer information finns i [Avinstallera-klienten](../manage/manage-clients.md#BKMK_UninstalClient).

Exempel: `ccmsetup.exe /uninstall`  

### <a name="logon"></a>/logon

Om någon version av klienten redan är installerad anger den här parametern att klient installationen ska stoppas.  

Exempel: `ccmsetup.exe /logon`  

### <a name="forcereboot"></a>/forcereboot

Använd den här parametern för att tvinga datorn att starta om vid behov för att slutföra installationen. Om du inte anger den här parametern avslutas CCMSetup när en omstart krävs. Den fortsätter sedan efter nästa manuella omstart.

Exempel: `CCMSetup.exe /forcereboot`

### <a name="bitspriority"></a>/BITSPriority

När enheten laddar ned klientens installationsfiler över en HTTP-anslutning använder du den här parametern för att ange hämtnings prioriteten. Ange ett av följande möjliga värden:

- `FOREGROUND`

- `HIGH`

- `NORMAL`objekt

- `LOW`

Exempel: `ccmsetup.exe /BITSPriority:HIGH`

### <a name="downloadtimeout"></a>/downloadtimeout

Om CCMSetup inte kan hämta klientens installationsfiler anger den här parametern den maximala tids gränsen i minuter. Efter denna tids gräns slutar CCMSetup att försöka ladda ned installationsfilerna. Standardvärdet är **1440** minuter (en dag).

Använd parametern [**/retry**](#retry) för att ange intervallet mellan nya försök.

Exempel: `ccmsetup.exe /downloadtimeout:100`

### <a name="usepkicert"></a>/UsePKICert

Ange den här parametern för att klienten ska använda ett certifikat för PKI-klientautentisering. Om du inte tar med den här parametern, eller om klienten inte kan hitta ett giltigt certifikat, använder den en HTTP-anslutning med ett självsignerat certifikat.

Exempel: `CCMSetup.exe /UsePKICert`  

> [!NOTE]
> I vissa fall behöver du inte ange den här parametern, men du kan fortfarande använda ett klient certifikat. Till exempel klient-push-installation och program uppdatering – baserad klient installation. Använd den här parametern när du installerar en klient manuellt och använder parametern **/MP** med en HTTPS-aktiverad hanterings plats.
>
> Ange även den här parametern när du installerar en klient för kommunikation via Internet. Använd egenskapen **CCMALWAYSINF = 1** tillsammans med egenskaperna för den Internetbaserade hanterings platsen (**CCMHOSTNAME**) och plats koden (**SMSSITECODE**). Mer information om Internetbaserad klient hantering finns i [överväganden för klient kommunikation från Internet eller en ej betrodd skog](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan).  

### <a name="nocrlcheck"></a>/NoCRLCheck

Anger att en klient inte ska kontrol lera listan över återkallade certifikat (CRL) när den kommunicerar via HTTPS med ett PKI-certifikat. När du inte anger den här parametern kontrollerar klienten listan över återkallade certifikat innan en HTTPS-anslutning upprättas. Mer information om CRL-kontroll för klienter finns i [Planera för återkallning av PKI-certifikat](../../plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs).

Exempel: `CCMSetup.exe /UsePKICert /NoCRLCheck`  

### <a name="config"></a>/config

Den här parametern anger en textfil som visar en lista över klient installations egenskaper.

- Om CCMSetup körs som en tjänst placerar du filen i mappen CCMSetup-system: `%Windir%\Ccmsetup` .

- Om du anger parametern [**/noservice**](#noservice) placerar du filen i samma mapp som CCMSetup. exe.

Exempel: `CCMSetup.exe /config:"configuration file name.txt"`

Använd filen **filen mobileclienttemplate. TCF** i `\bin\<platform>` mappen i Configuration Manager installations katalog på plats servern för att ange rätt fil format. Den här filen innehåller kommentarer om avsnitten och hur de används. Ange klient installations egenskaperna i `[Client Install]` avsnittet efter följande text: `Install=INSTALL=ALL` .

Exempel på `[Client Install]` avsnitts post:`Install=INSTALL=ALL SMSSITECODE=ABC SMSCACHESIZE=100`  

### <a name="skipprereq"></a>/skipprereq

Den här parametern anger att CCMSetup. exe inte ska installera den angivna förutsättningen. Du kan ange mer än ett värde. Använd semikolon ( `;` ) för att avgränsa varje värde.

Exempel:

- `CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe`

- `CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe;windowsupdateagent30_x86.exe`

Mer information om klient krav finns i [krav för Windows-klienten](prerequisites-for-deploying-clients-to-windows-computers.md).

### <a name="forceinstall"></a>/forceinstall

Ange att CCMSetup. exe avinstallerar en befintlig klient och installerar en ny klient.  

### <a name="excludefeatures"></a>/ExcludeFeatures

Den här parametern anger att CCMSetup. exe inte ska installera den angivna funktionen.

Exempel: `CCMSetup.exe /ExcludeFeatures:ClientUI` installerar inte Software Center på klienten.  

> [!NOTE]  
> `ClientUI`är det enda värde som parametern **/ExcludeFeatures** stöder.

## <a name="ccmsetupexe-return-codes"></a><a name="ccmsetupReturnCodes"></a>Retur koder för CCMSetup. exe

Kommandot CCMSetup. exe ger följande retur koder. Du kan felsöka genom att granska `%WinDir%\ccmsetup\ccmsetup.log` klienten för kontext och ytterligare information om retur koder.

|Returkod|Innebörd|  
|-----------|-------|  
|0|Klart|  
|6|Fel|  
|7|Omstart krävs|  
|8|Installationen körs redan|  
|9|Utvärderingen av krav misslyckades|  
|10|Installationsmanifestet för hash-verifieringen misslyckades|  

## <a name="ccmsetupmsi-properties"></a><a name="ccmsetupMsiProps"></a>CCMSetup. msi-egenskaper

Följande egenskaper kan ändra installations beteendet för CCMSetup. msi.

### <a name="ccmsetupcmd"></a>CCMSETUPCMD

Använd denna CCMSetup. *MSI* -egenskap för att skicka ytterligare kommando rads parametrar och egenskaper till CCMSetup. *exe*. Inkludera andra parametrar och egenskaper inom citat tecken ( `"` ). Använd den här egenskapen när du startar Configuration Manager-klienten med [INTUNE MDM-installations metoden](plan/client-installation-methods.md#microsoft-intune-mdm-installation).

Exempel: `ccmsetup.msi CCMSETUPCMD="/mp:https://mp.contoso.com CCMHOSTNAME=mp.contoso.com"`

> [!Tip]
> Microsoft Intune begränsar kommando raden till 1024 tecken.

## <a name="clientmsi-properties"></a><a name="clientMsiProps"></a>Client. msi-egenskaper

Följande egenskaper kan ändra installations beteendet för Client. msi, som CCMSetup. exe installerar. Om du använder [push-installation av klienter](plan/client-installation-methods.md#client-push-installation)anger du dessa egenskaper på fliken **klient** i egenskaperna för **push-installation av klienter** i Configuration Manager-konsolen.

### <a name="aadclientappid"></a>AADCLIENTAPPID

Anger Azure Active Directory (Azure AD)-klientens app-ID. Du skapar eller importerar klient appen när du [konfigurerar Azure-tjänster](../../servers/deploy/configure/azure-services-wizard.md) för moln hantering. En Azure-administratör kan hämta värdet för den här egenskapen från Azure Portal. Mer information finns i [Hämta program-ID](https://docs.microsoft.com/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in). Detta program-ID är för den **interna** program typen för egenskapen **AADCLIENTAPPID** .

Exempel: `ccmsetup.exe AADCLIENTAPPID=aa28e7f1-b88a-43cd-a2e3-f88b257c863b`

### <a name="aadresourceuri"></a>AADRESOURCEURI

Anger ID för Azure AD server-appen. Du skapar eller importerar Server-appen när du [konfigurerar Azure-tjänster](../../servers/deploy/configure/azure-services-wizard.md) för moln hantering. När du skapar Server-appen, i fönstret Skapa serverprogram, är den här egenskapen **app-ID-URI: n**.

En Azure-administratör kan hämta värdet för den här egenskapen från Azure Portal. I **Azure Active Directory**letar du reda på Server-appen under **Appregistreringar**. Sök efter program typ **Web App/API**. Öppna appen, Välj **Inställningar**och välj sedan **Egenskaper**. Använd **URI-värdet för app-ID** för den här **AADRESOURCEURI** -klientens installations egenskap.

Exempel: `ccmsetup.exe AADRESOURCEURI=https://contososerver`

### <a name="aadtenantid"></a>AADTENANTID

Anger ID för Azure AD-klient. Configuration Manager länkar till den här klienten när du [konfigurerar Azure-tjänster](../../servers/deploy/configure/azure-services-wizard.md) för moln hantering. Använd följande steg för att hämta värdet för den här egenskapen:

- Öppna en kommando tolk på en Windows 10-enhet som är ansluten till samma Azure AD-klient.
- Kör följande kommando:`dsregcmd.exe /status`
- I avsnittet enhets status söker du efter **TenantId** -värdet. Till exempel, `TenantId : 607b7853-6f6f-4d5d-b3d4-811c33fdd49a`

  > [!Note]
  > En Azure-administratör kan också hämta det här värdet i Azure Portal. Mer information finns i [Hämta klient-ID](https://docs.microsoft.com/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in).

Exempel: `ccmsetup.exe AADTENANTID=607b7853-6f6f-4d5d-b3d4-811c33fdd49a`

<!-- 
### AADTENANTNAME

Specifies the Azure AD tenant name. This tenant is linked to Configuration Manager when you [configure Azure services](../../servers/deploy/configure/azure-services-wizard.md) for Cloud Management. To obtain the value for this property, use the following steps:
- On a Windows 10 device that is joined to the same Azure AD tenant, open a command prompt.
- Run the following command: `dsregcmd.exe /status`
- In the Device State section, find the **TenantName** value. For example, `TenantName : Contoso`

Example: `ccmsetup.exe AADTENANTNAME=Contoso`
-->

### <a name="ccmadmins"></a>CCMADMINS  

Anger ett eller flera Windows-användarkonton eller grupper som ska få åtkomst till klientinställningar och rutiner. Den här egenskapen är användbar när du inte har lokal administratörs behörighet på klient datorn. Ange en lista över konton som är avgränsade med semikolon ( `;` ).

Exempel: `CCMSetup.exe CCMADMINS="domain\account1;domain\group1"`

### <a name="ccmallowsilentreboot"></a>CCMALLOWSILENTREBOOT

Om det behövs kan datorn tyst starta om efter klient installationen.

> [!IMPORTANT]  
> När du använder den här egenskapen startar datorn om utan varning. Det här beteendet inträffar även om en användare är inloggad i Windows.

Exempel: `CCMSetup.exe CCMALLOWSILENTREBOOT`

### <a name="ccmalwaysinf"></a>CCMALWAYSINF

Om du vill ange att klienten alltid är Internet-baserad och aldrig ansluter till intranätet anger du det här egenskap svärdet `1` . Klientens anslutningstyp är **Alltid Internet**.  

Använd den här egenskapen med [**CCMHOSTNAME**](#ccmhostname) för att ange det fullständiga domän namnet för den Internetbaserade hanterings platsen. Använd även den med CCMSetup-parametern [**/UsePKICert**](#usepkicert) och plats koden ([**SMSSITECODE**](#smssitecode)).

Mer information om Internetbaserad klient hantering finns i [överväganden för klient kommunikation från Internet eller en ej betrodd skog](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan).

Exempel: `CCMSetup.exe /UsePKICert CCMALWAYSINF=1 CCMHOSTNAME=SERVER3.CONTOSO.COM SMSSITECODE=ABC`

### <a name="ccmcertissuers"></a>CCMCERTISSUERS

Använd den här egenskapen för att ange listan med certifikat utfärdare. Den här listan innehåller certifikat information för betrodda rot certifikat utfärdare (CA) som Configuration Manager-platsen litar på.  

Det här värdet är en Skift läges känslig matchning för de attribut som finns i rot certifikat utfärdarens certifikat. Separera attribut med kommatecken ( `,` ) eller semikolon ( `;` ). Ange mer än ett rot certifikat för certifikat utfärdare med hjälp av ett avgränsnings streck ( `|` ).

Exempel: `CCMCERTISSUERS="CN=Contoso Root CA; OU=Servers; O=Contoso, Ltd; C=US | CN=Litware Corporate Root CA; O=Litware, Inc."`

> [!TIP]
> Använd värdet för attributet **CertificateIssuers** i filen **filen mobileclient. TCF** för platsen. Den här filen finns i `\bin\<platform>` undermappen i Configuration Manager installations katalog på plats servern.

Mer information om listan med certifikat utfärdare och hur klienter använder den under certifikat urvals processen finns i [Planera för val av PKI-klientcertifikat](../../plan-design/security/plan-for-security.md#BKMK_PlanningForClientCertificateSelection).

### <a name="ccmcertsel"></a>CCMCERTSEL

Om klienten har fler än ett certifikat för HTTPS-kommunikation anger den här egenskapen villkor för den för att välja ett giltigt certifikat för klientautentisering.

Använd följande nyckelord om du vill söka efter certifikatets ämnes namn eller alternativt namn för certifikat mottagare:

- **Ämne**: hitta en exakt matchning
- **SubjectStr**: hitta en partiell matchning

Exempel:

- `CCMCERTSEL="Subject:computer1.contoso.com"`: Sök efter ett certifikat med en exakt matchning till dator namnet `computer1.contoso.com` i ämnes namnet eller det alternativa ämnes namnet.

- `CCMCERTSEL="SubjectStr:contoso.com"`: Sök efter ett certifikat som innehåller `contoso.com` i ämnes namnet eller det alternativa certifikat mottagar namnet.

Använd nyckelordet **SubjectAttr** för att söka efter objekt IDENTIFIERARE (OID) eller attribut för unika namn i ämnes namnet eller det alternativa ämnes namnet.

Exempel:

- `CCMCERTSEL="SubjectAttr:2.5.4.11 = Computers"`: Sök efter attributet för organisationsenheten uttryckt som en objekt identifierare och namngett `Computers` .

- `CCMCERTSEL="SubjectAttr:OU = Computers"`: Sök efter attributet Organisations enhet som uttrycks som ett unikt namn och med namnet `Computers` .

> [!IMPORTANT]
> Om du använder ämnes namnet är nyckelordet **subject** Skift läges känsligt och nyckelordet **SubjectStr** är Skift läges okänsligt.
>
> Om du använder alternativt namn för certifikat mottagare är både **ämnet** och nyckelordet **SubjectStr** Skift läges okänsligt.

En fullständig lista över attribut som du kan använda för val av certifikat finns i [attributvärden som stöds för urvalskriterier för PKI-certifikat](#BKMK_attributevalues).

Om fler än ett certifikat matchar sökningen och du anger [**CCMFIRSTCERT**](#ccmfirstcert) till `1` , väljer klient installations programmet certifikatet med den längsta giltighets perioden.

### <a name="ccmcertstore"></a>CCMCERTSTORE

Om klient installations programmet inte kan hitta ett giltigt certifikat i det **personliga** standard certifikat arkivet för datorn använder du den här egenskapen för att ange ett alternativt certifikat Arkiv namn.

Exempel: `CCMSetup.exe /UsePKICert CCMCERTSTORE="ConfigMgr"`  

### <a name="ccmdebuglogging"></a>CCMDEBUGLOGGING

Den här egenskapen aktiverar fel söknings loggning när klienten installeras. Den här egenskapen gör att klienten loggar information på låg nivå för fel sökning. Undvik att använda den här egenskapen på produktions platser. Överdriven loggning kan inträffa, vilket kan göra det svårt att hitta relevant information i loggfilerna. Aktivera även [**CCMENABLELOGGING**](#ccmenablelogging).

Värden som stöds:

- `0`: Inaktivera fel söknings loggning (standard)
- `1`: Aktivera fel söknings loggning

Exempel: `CCMSetup.exe CCMDEBUGLOGGING=1`  

Mer information finns i [logg filen](../../plan-design/hierarchy/about-log-files.md).

### <a name="ccmenablelogging"></a>CCMENABLELOGGING

Configuration Manager aktiverar loggning som standard.

Värden som stöds:

- `TRUE`: Aktivera loggning (standard)
- `FALSE`: Inaktivera loggning

Exempel: `CCMSetup.exe CCMENABLELOGGING=TRUE`  

Mer information finns i [logg filen](../../plan-design/hierarchy/about-log-files.md).

### <a name="ccmevalinterval"></a>CCMEVALINTERVAL

Frekvensen i minuter då utvärderings verktyget för klient hälsa (ccmeval. exe) körs. Ange ett heltals värde från `1` till `1440` . Som standard körs ccmeval en gång om dagen (1440 minuter).

Exempel: `CCMSetup.exe CCMEVALINTERVAL=1440`

Mer information om utvärdering av klient hälsa finns i [övervaka klienter](../manage/monitor-clients.md#bkmk_health).

### <a name="ccmevalhour"></a>CCMEVALHOUR

Timmen under dagen då utvärderings verktyget för klient hälsa (ccmeval. exe) körs. Ange ett heltals värde från `0` (midnatt) till `23` (11:00 PM). Som standard körs ccmeval vid midnatt.

Mer information om utvärdering av klient hälsa finns i [övervaka klienter](../manage/monitor-clients.md#bkmk_health).

### <a name="ccmfirstcert"></a>CCMFIRSTCERT

Om du ställer in den här egenskapen på `1` väljer klienten PKI-certifikatet med den längsta giltighets perioden.

Exempel: `CCMSetup.exe /UsePKICert CCMFIRSTCERT=1`

### <a name="ccmhostname"></a>CCMHOSTNAME

Om klienten hanteras via Internet anger den här egenskapen FQDN för den Internetbaserade hanterings platsen.  

Ange inte det här alternativet med installations egenskapen **SMSSITECODE = Auto**. Tilldela Internet-baserade klienter direkt till en Internetbaserad plats.

Exempel: `CCMSetup.exe /UsePKICert CCMHOSTNAME="SMSMP01.corp.contoso.com"`  

Den här egenskapen kan ange adressen till en CMG (Cloud Management Gateway). Använd följande steg för att hämta värdet för den här egenskapen:

- Skapa en CMG. Mer information finns i [Konfigurera en CMG](../manage/cmg/setup-cloud-management-gateway.md).
- Öppna en Windows PowerShell-kommandotolk som administratör på en aktiv klient.
- Kör följande kommando:

    ```PowerShell
    (Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}).MP`
    ```

- Använd det returnerade värdet as-är med egenskapen **CCMHOSTNAME** .

Exempelvis: `ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057598037248100`

> [!Important]
> När du anger adressen till en CMG för egenskapen **CCMHOSTNAME** ska du inte lägga till ett prefix som `https://` . Använd bara det här prefixet med **/MP** -URL: en för en CMG.

### <a name="ccmhttpport"></a>CCMHTTPPORT

Anger vilken port som klienten ska använda när den kommunicerar via HTTP till plats system servrar. Som standard är det här värdet `80` .

Exempel: `CCMSetup.exe CCMHTTPPORT=80`

### <a name="ccmhttpsport"></a>CCMHTTPSPORT

Anger vilken port som klienten ska använda när den kommunicerar via HTTPS till plats system servrar. Som standard är det här värdet `443` .

Exempel: `CCMSetup.exe /UsePKICert CCMHTTPSPORT=443`

### <a name="ccminstalldir"></a>CCMINSTALLDIR

Använd den här egenskapen för att ange att mappen ska installera Configuration Manager-klientens filer. Som standard används `%WinDir%\CCM` .

> [!TIP]
> Oavsett var du installerar-klient filerna installeras filen **cmcore. dll** alltid i `%WinDir%\System32` mappen. På ett 64-bitars operativ system installerar den en kopia av cmcore. dll i `%WinDir%\SysWOW64` mappen. Den här filen stöder 32-bitars program som använder 32-bitars versionen av-klientens API: er från Configuration Manager SDK.

Exempel: `CCMSetup.exe CCMINSTALLDIR="C:\ConfigMgr"`

### <a name="ccmloglevel"></a>CCMLOGLEVEL

Använd den här egenskapen för att ange detalj nivån som ska skrivas till Configuration Manager loggfiler.

Värden som stöds:

- `0`: Utförlig
- `1`: Standard
- `2`: Varningar och fel
- `3`: Endast fel

Exempel: `CCMSetup.exe CCMLOGLEVEL=0`

Mer information finns i [logg filen](../../plan-design/hierarchy/about-log-files.md).

### <a name="ccmlogmaxhistory"></a>CCMLOGMAXHISTORY

När en Configuration Manager loggfil når den maximala storleken, byter klienten namn på den som en säkerhets kopia och skapar en ny loggfil. Den här egenskapen anger hur många tidigare versioner av logg filen som ska behållas. Standardvärdet är `1`. Om du ställer in värdet på `0` , behåller inte klienten logg fils historiken.

Exempel: `CCMSetup.exe CCMLOGMAXHISTORY=5`

Mer information finns i [logg filen](../../plan-design/hierarchy/about-log-files.md).

### <a name="ccmlogmaxsize"></a>CCMLOGMAXSIZE

Den här egenskapen anger den maximala logg fils storleken i byte. När en logg växer till den angivna storleken byter klienten namn på den som en historik fil och skapar en ny. Standard storleken är 250 000 byte, och den minsta storleken är 10 000 byte.

Exempel: `CCMSetup.exe CCMLOGMAXSIZE=300000` (300 000 byte)

### <a name="disablesiteopt"></a>DISABLESITEOPT

Ange den här egenskapen till `TRUE` om du vill blockera administratörer från att ändra den tilldelade platsen i Configuration Manager kontroll panelen.

Exempel: **CCMSetup.exe DISABLESITEOPT=TRUE**

### <a name="disablecacheopt"></a>DISABLECACHEOPT

Om värdet är TRUE inaktive ras möjligheten för administrativa användare från att ändra inställningarna för mappen för klientcachen i **Configuration Manager** kontroll panelen.  

Exempel: `CCMSetup.exe DISABLECACHEOPT=TRUE`  

### <a name="dnssuffix"></a>DNSSUFFIX

Ange en DNS-domän för klienter för att hitta hanterings platser som du publicerar i DNS. När klienten hittar en hanterings plats meddelar den klienten om andra hanterings platser i hierarkin. Det innebär att den hanterings plats som klienten hittar från DNS kan vara vilken som helst i hierarkin.

> [!NOTE]
> Du behöver inte ange den här egenskapen om klienten finns i samma domän som en publicerad hanterings plats. I så fall används klientens domän automatiskt för att söka efter DNS för hanterings platser.

Mer information om DNS-publicering som en tjänst plats metod för Configuration Manager-klienter finns i [tjänst lokalisering och hur klienter avgör sina tilldelade hanterings platser](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location).

> [!NOTE]  
> Som standard är Configuration Manager inte att aktivera DNS-publicering.

Exempel: `CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=contoso.com`

### <a name="fsp"></a>FSP

Ange återställnings status punkten som tar emot och bearbetar status meddelanden som skickas av Configuration Manager klienter.

Mer information finns i [avgöra om du behöver en återställnings status plats](plan/determine-the-site-system-roles-for-clients.md#fallback-status-point).

Exempel: `CCMSetup.exe FSP=SMSFP01`  

### <a name="ignoreappvversioncheck"></a>IGNOREAPPVVERSIONCHECK

Om du ställer in den här egenskapen på `TRUE` kontrollerar klient installations programmet inte den lägsta version som krävs för Microsoft Application Virtualization (App-V).

> [!IMPORTANT]  
> Om du installerar Configuration Manager-klienten utan att installera App-V kan du inte [distribuera virtuella program](../../../apps/get-started/deploying-app-v-virtual-applications.md).

Exempel: `CCMSetup.exe IGNOREAPPVVERSIONCHECK=TRUE`

### <a name="notifyonly"></a>NOTIFYONLY

När du aktiverar den här egenskapen rapporterar klienten status, men reparerar inte problem som hittas.

Exempel: `CCMSetup.exe NOTIFYONLY=TRUE`

Mer information finns i [så här konfigurerar du klient status](configure-client-status.md).

### <a name="provisionts"></a>ETABLERINGar

<!--5526972-->

Från och med version 2002 använder du den här egenskapen för att starta en aktivitetssekvens på en klient när den har registrerats på platsen.

Du kan till exempel etablera en ny Windows 10-enhet med Windows autopilot, registrera den automatiskt till Microsoft Intune och sedan installera Configuration Manager-klienten för samhantering. Om du anger det här nya alternativet Kör den nyligen etablerade klienten en aktivitetssekvens. Den här processen ger dig ytterligare flexibilitet för att installera program och program uppdateringar eller konfigurera inställningar.

Använd följande process:

1. [Skapa en aktivitetssekvens som inte är en operativ system distribution](../../../osd/deploy-use/create-a-task-sequence-for-non-operating-system-deployments.md) för att installera appar, installera program uppdateringar och konfigurera inställningar.

1. [Distribuera denna](../../../osd/deploy-use/deploy-a-task-sequence.md) aktivitetssekvens till den nya inbyggda samlingen, **alla etablerings enheter**. Anteckna distributions-ID för aktivitetssekvens till exempel `PRI20001` .

1. [Installera Configuration Manager-klienten](deploy-clients-to-windows-computers.md#BKMK_Manual) på en enhet och inkludera följande egenskap: `PROVISIONTS=PRI20001` . Ange värdet för den här egenskapen som distributions-ID för aktivitetssekvens.

    - Om du installerar-klienten från Intune under registreringen av samhantering, se så [här förbereder du Internetbaserade enheter för samhantering](../../../comanage/how-to-prepare-Win10.md).

      > [!NOTE]
      > Den här metoden kan ha ytterligare krav. Du kan till exempel registrera platsen till Azure Active Directory eller skapa en innehålls aktive rad Cloud Management Gateway.

När klienten har installerats och registrerats på rätt sätt på platsen startar den refererade aktivitetssekvensen. Om klient registreringen Miss lyckas startar inte aktivitetssekvensen.

### <a name="resetkeyinformation"></a>RESETKEYINFORMATION

Om en klient har fel Configuration Manager betrodd rot nyckel kan den inte kontakta en betrodd hanterings plats för att ta emot den nya betrodda rot nyckeln. Använd den här egenskapen för att ta bort den gamla betrodda rot nyckeln. Den här situationen kan inträffa när du flyttar en klient från en platshierarki till en annan. Den här egenskapen gäller klienter som använder HTTP- och HTTPS-kommunikation. Mer information finns i [Planera för den betrodda rot nyckeln](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).

Exempel: `CCMSetup.exe RESETKEYINFORMATION=TRUE`  

### <a name="sitereassign"></a>SITEREASSIGN

Aktiverar automatisk omtilldelning av platser för klient uppgraderingar när de används med [SMSSITECODE = Auto](#smssitecode).

Exempel: `CCMSetup.exe SMSSITECODE=AUTO SITEREASSIGN=TRUE`

### <a name="smscachedir"></a>SMSCACHEDIR

Anger platsen för mappen för klientcachen på klient datorn. Som standard är cache-platsen `%WinDir%\ccmcache` .

Exempel: `CCMSetup.exe SMSCACHEDIR="C:\Temp"`  

Använd den här egenskapen med egenskapen [**SMSCACHEFLAGS**](#smscacheflags) för att styra platsen för klientcachen. Om du till exempel vill installera mappen client cache på den största tillgängliga klient disk enheten:`CCMSetup.exe SMSCACHEDIR=Cache SMSCACHEFLAGS=MAXDRIVE`

### <a name="smscacheflags"></a>SMSCACHEFLAGS

Använd den här egenskapen för att ange ytterligare installations information för mappen client cache. Du kan använda **SMSCACHEFLAGS** -egenskaper individuellt eller i en kombination avgränsade med semikolon ( `;` ).

Om du inte tar med den här egenskapen:

- Klienten installerar cache-mappen enligt egenskapen [**SMSCACHEDIR**](#smscachedir)
- Mappen är inte komprimerad
- Klienten använder egenskapen [**SMSCACHESIZE**](#smscachesize) som storleks gräns i MB för cachen

När du uppgraderar en befintlig klient ignorerar klient installations programmet den här egenskapen.

#### <a name="values-for-the-smscacheflags-property"></a>Värden för egenskapen SMSCACHEFLAGS

- **PERCENTDISKSPACE**: Ange cache-storlek som en procent andel av det *totala* disk utrymmet. Om du anger den här egenskapen anger du också [**SMSCACHESIZE**](#smscachesize) till ett procent värde.

- **PERCENTFREEDISKSPACE**: Ange cache-storlek som en procent andel av det *lediga* disk utrymmet. Om du anger den här egenskapen anger du även [**SMSCACHESIZE**](#smscachesize) som ett procent värde. Disken har till exempel 10 MB ledigt och du anger `SMSCACHESIZE=50` . Klient installations programmet anger cache-storleken till 5 MB. Du kan inte använda den här egenskapen med egenskapen **PERCENTDISKSPACE** .

- **MAXDRIVE**: installera cachen på den största tillgängliga disken. Om du anger en sökväg med egenskapen [**SMSCACHEDIR**](#smscachedir) ignorerar klient installations programmet det här värdet.

- **MAXDRIVESPACE**: installera cachen på disk enheten med mest ledigt utrymme. Om du anger en sökväg med egenskapen [**SMSCACHEDIR**](#smscachedir) ignorerar klient installations programmet det här värdet.

- **NTFSONLY**: installera bara cachen på en NTFS-formaterad disk enhet. Om du anger en sökväg med egenskapen [**SMSCACHEDIR**](#smscachedir) ignorerar klient installations programmet det här värdet.

- **Komprimera**: lagra cacheminnet i en komprimerad form.

- **FAILIFNOSPACE**: om det inte finns tillräckligt med utrymme för att installera cachen tar du bort Configuration Manager-klienten.

Exempel: `CCMSetup.exe SMSCACHEFLAGS=NTFSONLY;COMPRESS`

### <a name="smscachesize"></a>SMSCACHESIZE

> [!IMPORTANT]
> Klient inställningar är tillgängliga för att ange mappens cachestorlek. Tillägget av dessa klientinställningar ersätter effektivt användningen av SMSCACHESIZE som client.msi-egenskap för att ange storleken på klientens cacheminne. Mer information finns i [klientinställningarna för cachestorlek](about-client-settings.md#client-cache-settings).  

När du uppgraderar en befintlig klient ignorerar klient installations programmet den här inställningen. Klienten ignorerar också cache-storleken när den laddar ned program uppdateringar.

Exempel: `CCMSetup.exe SMSCACHESIZE=100`

> [!NOTE]  
> Om du installerar om en klient kan du inte använda **SMSCACHESIZE** eller **SMSCACHEFLAGS** för att ange att cachestorleken ska vara mindre än tidigare. Den tidigare storleken är det lägsta värdet.

### <a name="smsconfigsource"></a>SMSCONFIGSOURCE

Använd den här egenskapen för att ange den plats och ordning som klient installations programmet söker efter konfigurations inställningar. Det är en sträng med ett eller flera tecken som var och en definierar en bestämd konfigurations Källa:

- `R`: Sök efter konfigurations inställningar i registret.

  Mer information finns i [etablera klient installations egenskaper](deploy-clients-to-windows-computers.md#BKMK_Provision).

- `P`: Sök efter konfigurations inställningar i installations egenskaperna från kommando raden.

- `M`: Sök efter befintliga inställningar när du uppgraderar en äldre klient.

- `U`: Uppgradera den installerade klienten till en nyare version och Använd den tilldelade plats koden.

Som standard används klient installations programmet `PU` . Först kontrol leras installations egenskaperna ( `P` ) och sedan de befintliga inställningarna ( `U` ).  

Exempel: `CCMSetup.exe SMSCONFIGSOURCE=RP`

<!--
### SMSDIRECTORYLOOKUP

Specifies whether the client can use Windows Internet Name Service (WINS) to find a management point that accepts HTTP connections. Clients use this method when they can't find a management point in Active Directory Domain Services or in DNS.  

 This property doesn't affect whether the client uses WINS for name resolution.  

 You can configure two different modes for this property:  

-   NOWINS: This value is the most secure setting for this property and prevents clients from finding a management point in WINS. When you use this setting, clients must have an alternative method to locate a management point on the intranet, such as Active Directory Domain Services or by using DNS publishing.  

-   WINSSECURE (default): In this mode, a client that uses HTTP communication can use WINS to find a management point. However, the client must have a copy of the trusted root key before it can successfully connect to the management point. For more information, see [Planning for the trusted root key](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

Example: `CCMSetup.exe SMSDIRECTORYLOOKUP=NOWINS`  
-->

### <a name="smsmp"></a>SMSMP

Anger en första hanterings plats för den Configuration Manager klienten som ska användas.  

> [!IMPORTANT]  
> Om hanterings platsen endast tar emot klient anslutningar via HTTPS ska du prefix för hanterings platsens namn med `https://` .

Exempel:

- `CCMSetup.exe SMSMP=smsmp01.contoso.com`

- `CCMSetup.exe SMSMP=https://smsmp01.contoso.com`  

### <a name="smspublicrootkey"></a>SMSPUBLICROOTKEY

Om klienten inte kan hämta Configuration Manager betrodda rot nyckeln från Active Directory Domain Services använder du den här egenskapen för att ange nyckeln. Den här egenskapen gäller för klienter som använder HTTP-och HTTPS-kommunikation. Mer information finns i [Planera för den betrodda rot nyckeln](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).

Exempel: `CCMSetup.exe SMSPUBLICROOTKEY=<keyvalue>`

> [!TIP]
> Hämta värdet för platsens betrodda rot nyckel från filen filen mobileclient. TCF på plats servern. Mer information finns i [Företablera en klient med den betrodda rot nyckeln med hjälp av en fil](../../plan-design/security/plan-for-security.md#bkmk_trk-provision-file).

### <a name="smsrootkeypath"></a>SMSROOTKEYPATH

Använd den här egenskapen för att installera om den Configuration Manager betrodda rot nyckeln. Den anger den fullständiga sökvägen och namnet på en fil som innehåller den betrodda rot nyckeln. Den här egenskapen gäller klienter som använder HTTP- och HTTPS-kommunikation. Mer information finns i [Planera för den betrodda rot nyckeln](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).

Exempel: `CCMSetup.exe SMSROOTKEYPATH=C:\folder\trk`

### <a name="smssigncert"></a>SMSSIGNCERT

Anger den fullständiga sökvägen och namnet på det exporterade självsignerade certifikatet på plats servern. Plats servern lagrar certifikatet i **SMS** -certifikatarkivet. Det har ämnes namnet **plats Server** och det egna namnet **signerings certifikat för plats Server**.

Exempel: `CCMSetup.exe /UsePKICert SMSSIGNCERT=C:\folder\smssign.cer`

### <a name="smssitecode"></a>SMSSITECODE

Den här egenskapen anger en Configuration Manager plats som du tilldelar klienten. Det här värdet kan antingen vara en platskod med tre tecken eller ordet `AUTO` . Om du anger `AUTO` eller inte anger den här egenskapen försöker klienten bestämma sin platstilldelning från Active Directory Domain Services eller från en angiven hanterings plats. Om du vill aktivera `AUTO` för klient uppgraderingar anger du även [SITEREASSIGN = True](#sitereassign).

> [!NOTE]  
> Om du också anger en Internetbaserad hanterings plats med egenskapen [**CCMHOSTNAME**](#ccmhostname) använder du inte `AUTO` med **SMSSITECODE**. Tilldela klienten en plats direkt genom att ange plats koden.

Exempel: `CCMSetup.exe SMSSITECODE=XZY`

## <a name="attribute-values-for-certificate-selection-criteria"></a><a name="BKMK_attributevalues"></a>Attributvärden för urvalskriterier för certifikat

Configuration Manager stöder följande attributvärden för urvalskriterier för PKI-certifikat:

|Objektidentifierarattribut|Attribut för unikt namn|Attributdefinition|
|-------------|----------------------------|--------------------|
|0.9.2342.19200300.100.1.25|DC|Domänkomponent|  
|1.2.840.113549.1.9.1|E eller E-mail|E-postadress|  
|2.5.4.3|CN|Allmänt namn|  
|2.5.4.4|SN|Mottagarnamn|  
|2.5.4.5|SERIALNUMBER|Serienummer|  
|2.5.4.6|C|Landskod|  
|2.5.4.7|L|Plats|  
|2.5.4.8|S eller ST|Namn på region|  
|2.5.4.9|STREET|Gatuadress|  
|2.5.4.10|O|Organisationsnamn|  
|2.5.4.11|OU|Organisationsenhet|  
|2.5.4.12|T eller Title|Titel|  
|2.5.4.42|G eller GN eller GivenName|Tilltalsnamn|  
|2.5.4.43|I eller Initials|Initialer|  
|2.5.29.17|(inget värde)|Alternativt namn för certifikatmottagare|  
