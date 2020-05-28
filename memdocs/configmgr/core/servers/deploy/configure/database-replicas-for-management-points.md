---
title: Databas repliker för hanterings plats
titleSuffix: Configuration Manager
description: Använd en databas replik för att minska processor belastningen på plats databas servern av hanterings platser.
ms.date: 05/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b06f781b-ab25-4d9a-b128-02cbd7cbcffe
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3daf23f17719e111dacd45e6176c5f697a3d3224
ms.sourcegitcommit: 4c129bb04ea4916c78446e89fbff956397cbe828
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/13/2020
ms.locfileid: "83343124"
---
# <a name="database-replicas-for-management-points-for-configuration-manager"></a>Databas repliker för hanterings platser för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Manager primära platser kan använda en databas replik för att minska processor belastningen på plats databas servern av hanterings platser när de hanterar begär Anden från klienter.  

-   När en hanteringsplats använder en databasreplik begär den data från SQL Server-datorn där databasrepliken finns i stället för från platsdatabasservern.  

-   Det kan minska kraven på processorbelastningen på platsdatabasservern genom att avlasta ofta förekommande bearbetningsuppgifter som är relaterade till klienterna.  Ett exempel på ofta förekommande bearbetningsuppgifter för klienter är platser där det finns ett stort antal klienter som ofta begär klientprincipen  


##  <a name="prepare-to-use-database-replicas"></a><a name="bkmk_Prepare"></a>Förbereda användningen av databas repliker  
**Om databasrepliker för hanteringsplatser:**  

-   Repliker är till viss del en kopia av platsdatabasen som replikeras till en separat instans av SQL Server:  

    -   Primära platser har stöd för en särskild databas replik för varje hanterings plats på platsen (sekundära platser stöder inte databas repliker)  

    -   En enda databasreplik kan användas av fler än en hanteringsplats från samma plats  

    -   En SQL-server kan vara värd för flera databasrepliker för användning av olika hanteringsplatser så länge varje replik körs i en separat instans av SQL Server  

-   Repliker synkroniserar en kopia av platsdatabasen enligt ett fast schema från data som publiceras av platsdatabasservern för detta ändamål.  

-   Hanteringsplatser kan konfigureras att använda en replik när du installerar hanteringsplatsen eller vid ett senare tillfälle genom att den tidigare installerade hanteringsplatsen konfigureras om så att den använder databasrepliken  

-   Granska platsdatabasservern och varje databasreplikserver med jämna mellanrum och se till att replikeringen mellan dem sker. Kontrollera dessutom att databasreplikserverns prestanda räcker för de plats- och klientprestanda som du behöver.  

**Förutsättningar för databasrepliker:**  

-   **SQL Server krav:**  

    -   Den SQL-server som innehåller databasreplikservern måste uppfylla samma krav som platsdatabasservern. Dock behöver replikservern inte köra samma version eller utgåva av SQL Server som platsdatabasservern, förutsatt att den kör en version eller utgåva av SQL Server som stöds. Mer information finns i [stöd för SQL Server versioner för Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md)  

    -   SQL Server-tjänsten på datorn där replikdatabasen lagras måste köras som ett **System** -konto.  

    -   Både den SQL Server som innehåller platsdatabasservern och databasreplikservern måste ha **SQL Server-replikering** installerat.  

    -   Platsdatabasen måste **publicera** databasrepliken och varje fjärransluten databasreplikserver måste **prenumerera** på publicerade data.  

    -   Både SQL Server som är värd för platsdatabasen och databasreplikservern måste konfigureras så att de stöder 2 GB som **Max Text Repl Size** . Ett exempel på hur du konfigurerar detta för SQL Server 2012 finns i [Configure the max text repl size Server Configuration Option ](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-the-max-text-repl-size-server-configuration-option?view=sql-server-ver15).  

-   **Självsignerat certifikat:** Om du vill konfigurera en databas replik måste du skapa ett självsignerat certifikat på databas replik servern och göra det tillgängligt för varje hanterings plats som ska använda databas replik servern.  

    -   Certifikatet är automatiskt tillgängligt för en hanteringsplats som är installerad på databasreplikservern.  

    -   Om detta certifikat ska vara tillgängligt för fjärrhanteringsplatser måste du exportera det och sedan lägga till det i certifikatarkivet **Betrodda personer** på fjärrhanteringsplatsen.  

-   **Klientmeddelande:** Om du vill använda klientmeddelanden med en databasreplik för en hanteringsplats måste du konfigurera **SQL Server Service Broker**för kommunikationen mellan platsdatabasservern och databasreplikservern. Detta kräver att du:  

    -   konfigurerar varje databas med information om den andra databasen  

    -   byter certifikat mellan de två databaserna för en säker kommunikation  

**Begränsningar när du använder databasrepliker:**  

-   Om platsen är konfigurerad att publicera databasrepliker bör du göra så här i stället för att följa den normala proceduren:  

    -   [Avinstallera en plats server som publicerar en databas replik](#BKMK_DBReplicaOps_Uninstall)  

    -   [Flytta en plats Server databas som publicerar en databas replik](#BKMK_DBReplicaOps_Move)  

-   **Uppgraderingar till Configuration Manager aktuella grenen**: innan du uppgraderar en plats måste du antingen från System Center 2012 Configuration Manager för att Configuration Manager aktuella grenen eller uppdatera Configuration Manager aktuella grenen till den senaste versionen, måste du inaktivera databas repliker för hanterings platser.  När platsen har uppgraderats kan du konfigurera om databasreplikerna för hanteringsplatser.  

-   **Flera repliker på samma SQL Server:**  Om du konfigurerar en databas replik server som värd för flera databas repliker för hanterings platser (varje replik måste finnas på en separat instans) måste du använda ett modifierat konfigurations skript (från steg 4 i följande avsnitt) för att förhindra att det självsignerade certifikatet som används av tidigare konfigurerade databas repliker skrivs över.  

- Användar distributioner i Software Center fungerar inte mot en hanterings plats med hjälp av en SQL-replik. <!--sccmdocs-1011-->

##  <a name="configure-database-replicas"></a><a name="BKMK_DBReplica_Config"></a>Konfigurera databas repliker  
Om du vill konfigurera en databasreplik följer du stegen nedan:  

-   [Steg 1 – Konfigurera platsdatabasservern för publicering av databasrepliken](#BKMK_DBReplica_ConfigSiteDB)  

-   [Steg 2 – Konfigurera databas replik servern](#BKMK_DBReplica_ConfigSrv)  

-   [Steg 3 – Konfigurera hanteringsplatser för att använda databasrepliken](#BKMK_DBReplica_ConfigMP)  

-   [Steg 4 – Konfigurera ett självsignerat certifikat för databasreplikservern](#BKMK_DBReplica_Cert)  

-   [Steg 5 – Konfigurera SQL Server Service Broker för databasreplikservern](#BKMK_DBreplica_SSB)  

###  <a name="step-1---configure-the-site-database-server-to-publish-the-database-replica"></a><a name="BKMK_DBReplica_ConfigSiteDB"></a>Steg 1 – Konfigurera plats databas servern för publicering av databas repliken  
 Använd proceduren nedan som exempel på hur du konfigurerar platsdatabasservern på en dator med Windows Server 2008 R2 så att den publicerar databasrepliken. Läs dokumentationen om operativsystemet och anpassa stegen i den här proceduren efter behov om du har en annan operativsystemsversion.  

##### <a name="to-configure-the-site-database-server"></a>Konfigurera platsdatabasservern  

1.  Ange att SQL Server Agent ska starta automatiskt på platsdatabasservern.  

2.  Skapa en lokal användar grupp med namnet **ConfigMgr_MPReplicaAccess**på plats databas servern. Du måste lägga till datorkontot för varje databasreplikserver som du använder på platsen till denna grupp. Då kan dessa databasreplikservrar synkroniseras med den publicerade databasrepliken.  

3.  Konfigurera en fil resurs med namnet **ConfigMgr_MPReplica**på plats databas servern.  

4.  Lägg till följande behörigheter till **ConfigMgr_MPReplica** resursen:  

    > [!NOTE]  
    >  Om SQL Server Agent använder ett annat konto än det lokala systemkontot ska SYSTEM ersättas med det kontonamnet i den följande listan.  

    -   **Resursbehörigheter**:  

        -   SYSTEM: **Skriva**  

        -   ConfigMgr_MPReplicaAccess: **Läs**  

    -   **NTFS-behörigheter**:  

        -   SYSTEM: **Fullständig behörighet**  

        -   ConfigMgr_MPReplicaAccess: **läsa**, **läsa & köra**, **Visa** mappinnehåll  

5.  Använd **SQL Server Management Studio** för att ansluta till platsdatabasen och kör följande lagrade procedur som en fråga: **spCreateMPReplicaPublication**  

När den lagrade proceduren har körts är platsdatabasservern konfigurerad att publicera databasrepliken.  

###  <a name="step-2---configuring-the-database-replica-server"></a><a name="BKMK_DBReplica_ConfigSrv"></a> Steg 2 – Konfigurera databasreplikservern  
Databasreplikservern är en dator som kör SQL Server och som har en replik av platsdatabasen som hanteringsplatser kan använda. Databasreplikservern synkroniserar sin kopia av databasen gentemot databasrepliken som publiceras av platsdatabasservern. Detta sker enligt ett fast schema.  

Databasreplikservern måste uppfylla samma krav som platsdatabasservern. Men databasreplikservern kan köra en annan utgåva eller version av SQL Server än platsdatabasservern. Information om vilka versioner av SQL Server som stöds finns i avsnittet [stöd för SQL Server versioner för Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md) .  

> [!IMPORTANT]  
>  SQL Server-tjänsten på datorn där replikdatabasen lagras måste köras som ett systemkonto.  

Använd proceduren nedan som exempel på hur du konfigurerar en databasreplikserver på en dator med Windows Server 2008 R2. Läs dokumentationen om operativsystemet och anpassa stegen i den här proceduren efter behov om du har en annan operativsystemsversion.  

##### <a name="to-configure-the-database-replica-server"></a>Konfigurera databasreplikservern  

1. Ange att SQL Server Agent ska starta automatiskt på databasreplikservern.  

2. Använd **SQL Server Management Studio** på databasreplikservern för att ansluta till den lokala servern, bläddra till mappen **Replication** , klicka på Local Subscriptions och välj **New Subscriptions** för att starta **New Subscription Wizard**:  

   1. På sidan **Publication**, i listrutan **Publisher**, väljer du **Find SQL Server Publisher**, anger namnet på platsens databassever och klickar sedan på **Connect**.  

   2. Välj **ConfigMgr_MPReplica**och klicka sedan på **Nästa**.  

   3. På sidan **distributions agentens plats** väljer du **Kör varje agent hos prenumeranten (pull-prenumerationer)** och klickar på **Nästa**.  

   4. Gör något av följande på sidan **Subscribers**:  

      -   Välj en befintlig databas från databasreplikservern som du vill använda för databasrepliken. Klicka sedan på **OK**.  

      -   Välj **New database** om du vill skapa en ny databas för databasrepliken. Ange ett databasnamn på sidan **New Database** och klicka sedan på **OK**.  

   5. Fortsätt genom att klicka på **Next** .  

   6. På sidan **distributions agent säkerhet** klickar du på knappen Egenskaper **(.** ..) i raden prenumerant anslutning i dialog rutan och konfigurerar sedan säkerhets inställningarna för anslutningen.  

      > [!TIP]  
      >  Knappen Egenskaper **(.**..) finns i den fjärde kolumnen i visnings rutan.  

      **Säkerhets inställningar:**  

      - Konfigurera kontot som kör distributions agent processen (process kontot):  

        -   Om SQL Server Agent körs som lokalt system väljer du **kör under SQL Server Agent tjänst konto (detta är inte en rekommenderad säkerhets metod.)**  

        -   Om SQL Server Agent körs med ett annat konto väljer du **Run under the following Windows account**, och konfigurerar sedan kontot. Du kan ange ett Windows-konto eller ett SQL Server-konto.  

        > [!IMPORTANT]  
        >  Du måste ge det konto som kör distributionsagenten behörigheter till utgivaren i form av en pull-prenumeration. Information om hur du konfigurerar dessa behörigheter finns i [säkerhet för distributions agent](https://docs.microsoft.com/sql/relational-databases/replication/distribution-agent-security?view=sql-server-ver15).  

      - Välj **By impersonating the process account**för **Connect to the Distributor**.  

      - Välj **By impersonating the process account**för **Connect to the Subscriber**.  

        Klicka på **OK** när du har konfigurerat anslutningens säkerhetsinställningar så att de sparas, och klicka sedan på **Next**.  

   7. På sidan **Synchronization Schedule**, i listrutan **Agent Schedule**, väljer du **Define schedule** och konfigurerar sedan **New Job Schedule**. Ange att frekvensen ska inträffa varje **dag**, upprepa var **5: e minut**och varaktigheten **utan slutdatum**. Spara schemat genom att klicka på **Next** och klicka sedan på **Next** igen.  

   8. På sidan **Guide åtgärder** markerar du kryss rutan för **skapa prenumerationer**och klickar sedan på **Nästa**.  

   9. Klicka på **Finish** på sidan **Complete the Wizard** och klicka sedan på **Close**.  

3. Omedelbart efter att du har slutfört guiden för ny prenumeration använder du **SQL Server Management Studio** för att ansluta till databasen för databasreplikservern och kör följande fråga för att aktivera databasegenskapen TRUSTWORTHY:  `ALTER DATABASE <MP Replica Database Name> SET TRUSTWORTHY ON;`  

4. Se igenom synkroniseringsstatusen för att verifiera att prenumerationen har lyckats:  

   -   På prenumerantdatorn:  

       -   Anslut till databasreplikservern och expandera **Replication** i **SQL Server Management Studio**.  

       -   Expandera **lokala prenumerationer**, högerklicka på prenumerationen på plats databasens publikation och välj sedan **Visa synkroniseringsstatus**.  

   -   På utgivardatorn:  

       -   I **SQL Server Management Studio**ansluter du till plats databas datorn, högerklickar på mappen **replikering** och väljer sedan **starta replikering**.  

5. Om du vill aktivera Common Language Runtime (CLR)-integration för databas repliken använder du **SQL Server Management Studio** för att ansluta till databas repliken på databas replik servern och kör följande lagrade procedur som en fråga: **exec sp_configure ' CLR Enabled ', 1; Konfigurera om med ÅSIDOSÄTTNING**  

6. För varje hanteringsplats som använder en databasreplikserver lägger du till platsens datorkonto till den lokala gruppen **Administratörer** på databasreplikservern.  

   > [!TIP]  
   >  Det här steget är inte nödvändigt för en hanteringsplats som körs på databasreplikservern.  

   Databasrepliken är nu redo att användas av hanteringsplatsen.  

###  <a name="step-3---configure-management-points-to-use-the-database-replica"></a><a name="BKMK_DBReplica_ConfigMP"></a>Steg 3 – Konfigurera hanterings platser för att använda databas repliken  
 Du kan konfigurera en hanteringsplats på en primär plats att använda en databasreplik när du installerar hanteringsplatsrollen, eller så kan du konfigurera om en befintlig hanteringsplats så att den använder en databasreplik.  

 Använd följande information för att konfigurera en hanteringsplats att använda en databasreplik:  

-   **Så här konfigurerar du en ny hanteringsplats:** Välj **Använd en databasreplikering** på sidan **Hanteringsplatsdatabas**i guiden som du använder för att installera hanteringsplatsen och ange det fullständiga domännamnet (FQDN) för den dator som är värd för databasrepliken. Ange sedan databasnamnet på databasrepliken på den datorn i **Databasnamn för ConfigMgr-plats**.  

-   **Så här konfigurerar du en tidigare installerad hanteringsplats**: Öppna hanteringsplatsens egenskapssida, välj fliken **Hanteringsplatsdatabas** , välj **Använd en databasreplikering**och ange sedan det fullständiga domännamnet (FQDN) på datorn som är värd för databasrepliken. Ange sedan databasnamnet på databasrepliken på den datorn i **Databasnamn för ConfigMgr-plats**.  

-   **För varje hanterings plats som använder en databas replik**måste du manuellt lägga till hanterings plats serverns dator konto till **db_datareader** rollen för databas repliken.  

Utöver att konfigurera hanteringsplatsen så att den använder databasreplikservern, måste du aktivera **Windows-autentisering** i **IIS** på hanteringsplatsen:  

1.  Öppna **Internet Information Services (IIS)-hanteraren**.  

2.  Välj webbplatsen som hanteringsplatsen använder och öppna **Autentisering**.  

3.  Ange **Windows-autentisering** som **aktive rad**och stäng sedan **Internet Information Services (IIS) Manager**.  

###  <a name="step-4--configure-a-self-signed-certificate-for-the-database-replica-server"></a><a name="BKMK_DBReplica_Cert"></a>Steg 4 – Konfigurera ett självsignerat certifikat för databas replik servern  
 Du måste skapa ett självsignerat certifikat på databas replik servern och göra det tillgängligt för varje hanterings plats som ska använda databas replik servern.  

 Certifikatet är automatiskt tillgängligt för en hanteringsplats som är installerad på databasreplikservern. Men om detta certifikat ska vara tillgängligt för fjärrhanteringsplatser, måste du exportera det och sedan lägga till det i certifikatarkivet Betrodda personer på fjärrhanteringsplatsen.  

 Använd följande procedurer som exempel på hur du konfigurerar det självsignerade certifikatet på databas replik servern för en Windows Server 2008 R2-dator. Läs dokumentationen om operativsystemet och anpassa stegen i de här procedurerna efter behov om du har en annan operativsystemsversion.  

##### <a name="to-configure-a-self-signed-certificate-for-the-database-replica-server"></a>Så här konfigurerar du ett självsignerat certifikat för databas replik servern  

1.  Öppna en PowerShell-kommandotolk med administratörs behörighet på databas replik servern och kör sedan följande kommando: **set-ExecutionPolicy unrestricted**  

2.  Kopiera följande PowerShell-skript och spara det som en fil med namnet **CreateMPReplicaCert.ps1**. Spara en kopia av den här filen i rotmappen på databasreplikserverns systempartition.  

    > [!IMPORTANT]  
    >  Om du konfigurerar mer än en databasreplik på en SQL-server måste du använda en modifierad version av skriptet för den här proceduren för varje replik du konfigurerar. Se  [Kompletterande skript för ytterligare databasrepliker på en SQL Server](#bkmk_supscript)  

    ``` PowerShell
    # Script for creating a self-signed certificate for the local machine and configuring SQL Server to use it.  

    Param($SQLInstance)  

    $ConfigMgrCertFriendlyName = "ConfigMgr SQL Server Identification Certificate"  

    # Get local computer name  
    $computerName = "$env:computername"  

    # Get the sql server name  
    #$key="HKLM:\SOFTWARE\Microsoft\SMS\MP"  
    #$value="SQL Server Name"  
    #$sqlServerName= (Get-ItemProperty $key).$value  
    #$dbValue="Database Name"  
    #$sqlInstance_DB_Name= (Get-ItemProperty $key).$dbValue  

    $sqlServerName = [System.Net.Dns]::GetHostByName("localhost").HostName   
    $sqlInstanceName = "MSSQLSERVER"  
    $SQLServiceName = "MSSQLSERVER"  

    if ($SQLInstance -ne $Null)  
    {  
        $sqlInstanceName = $SQLInstance  
        $SQLServiceName = "MSSQL$" + $SQLInstance  
    }  

    # Delete existing cert if one exists  
    function Get-Certificate($storename, $storelocation)  
    {   
        $store=new-object System.Security.Cryptography.X509Certificates.X509Store($storename,$storelocation)   
        $store.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)   
        $store.Certificates   
    }   

    $cert = Get-Certificate "My" "LocalMachine" | ?{$_.FriendlyName -eq $ConfigMgrCertFriendlyName}   
    if($cert -is [Object])  
    {  
        $store = new-object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")   
        $store.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)   
        $store.Remove($cert)  
        $store.Close()  

        # Remove this cert from Trusted People too...  
        $store = new-object System.Security.Cryptography.X509Certificates.X509Store("TrustedPeople","LocalMachine")   
        $store.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)   
        $store.Remove($cert)  
        $store.Close()      
    }  

    # Create the new cert  
    $name = new-object -com "X509Enrollment.CX500DistinguishedName.1"  
    $name.Encode("CN=" + $sqlServerName, 0)  

    $key = new-object -com "X509Enrollment.CX509PrivateKey.1"  
    $key.ProviderName = "Microsoft RSA SChannel Cryptographic Provider"  
    $key.KeySpec = 1  
    $key.Length = 1024  
    $key.SecurityDescriptor = "D:PAI(A;;0xd01f01ff;;;SY)(A;;0xd01f01ff;;;BA)(A;;0x80120089;;;NS)"  
    $key.MachineContext = 1  
    $key.Create()  

    $serverauthoid = new-object -com "X509Enrollment.CObjectId.1"  
    $serverauthoid.InitializeFromValue("1.3.6.1.5.5.7.3.1")  
    $ekuoids = new-object -com "X509Enrollment.CObjectIds.1"  
    $ekuoids.add($serverauthoid)  
    $ekuext = new-object -com "X509Enrollment.CX509ExtensionEnhancedKeyUsage.1"  
    $ekuext.InitializeEncode($ekuoids)  

    $cert = new-object -com "X509Enrollment.CX509CertificateRequestCertificate.1"  
    $cert.InitializeFromPrivateKey(2, $key, "")  
    $cert.Subject = $name  
    $cert.Issuer = $cert.Subject  
    $cert.NotBefore = get-date  
    $cert.NotAfter = $cert.NotBefore.AddDays(3650)  
    $cert.X509Extensions.Add($ekuext)  
    $cert.Encode()  

    $enrollment = new-object -com "X509Enrollment.CX509Enrollment.1"  
    $enrollment.InitializeFromRequest($cert)  
    $enrollment.CertificateFriendlyName = "ConfigMgr SQL Server Identification Certificate"  
    $certdata = $enrollment.CreateRequest(0x1)  
    $enrollment.InstallResponse(0x2, $certdata, 0x1, "")  

    # Add this cert to the trusted peoples store  
    [Byte[]]$bytes = [System.Convert]::FromBase64String($certdata)  

    $trustedPeople = new-object System.Security.Cryptography.X509certificates.X509Store "TrustedPeople", "LocalMachine"  
    $trustedPeople.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)  
    $trustedPeople.Add([Security.Cryptography.X509Certificates.X509Certificate2]$bytes)  
    $trustedPeople.Close()  

    # Get thumbprint from cert  
    $sha = new-object System.Security.Cryptography.SHA1CryptoServiceProvider  
    $certHash = $sha.ComputeHash($bytes)  
    $certHashCharArray = "";  
    $certThumbprint = "";  

    # Format the bytes into a hexadecimal string  
    foreach($byte in $certHash)  
    {  
        $temp = ($byte | % {"{0:x}" -f $_}) -join ""  
        $temp = ($temp | % {"{0,2}" -f $_})  
        $certHashCharArray = $certHashCharArray+ $temp;  
    }  
    $certHashCharArray = $certHashCharArray.Replace(' ', '0');  

    # SQL needs the thumbprint in lower case  
    foreach($char in $certHashCharArray)  
    {  
        [System.String]$myString = $char;  
        $certThumbprint = $certThumbprint + $myString.ToLower();  
    }  

    # Configure SQL to use this cert  
    $path = "HKLM:\SOFTWARE\Microsoft\Microsoft SQL Server\Instance Names\SQL"  
    $subKey = (Get-ItemProperty $path).$sqlInstanceName  
    $realPath = "HKLM:\SOFTWARE\Microsoft\Microsoft SQL Server\" + $subKey + "\MSSQLServer\SuperSocketNetLib"  
    $certKeyName = "Certificate"  
    Set-ItemProperty -path $realPath -name $certKeyName -Type string -Value $certThumbprint  

    # restart sql service  
    Restart-Service $SQLServiceName -Force  
    ```  

3.  Kör följande kommando på databasreplikservern. Det gäller konfigurationen av SQL Server:  

    -   För en standard instans av SQL Server: Högerklicka på filen **CreateMPReplicaCert. ps1** och välj **Kör med PowerShell**. När skriptet körs skapar det ett självsignerat certifikat och konfigurerar SQL Server att använda certifikatet.  

    -   För en namngiven instans av SQL Server: Använd PowerShell för att köra kommandot **%Path%\CreateMPReplicaCert.ps1 xxxxxx** där **xxxxxx** är namnet på SQL Server-instansen.  

    -   När skriptet är klart kontrollerar du att SQL Server Agent körs. Om inte, startar du om SQL Server Agent.  

##### <a name="to-configure-remote-management-points-to-use-the-self-signed-certificate-of-the-database-replica-server"></a>Konfigurera fjärrhanterings platser så att de använder det självsignerade certifikatet för databas replik servern  

1.  Utför följande steg på databas replik servern för att exportera serverns självsignerade certifikat:  

    1.  Klicka på **Start**, klicka på **Kör**och skriv **MMC. exe**. Klicka på **Arkiv**i den tomma konsolen och klicka sedan på **Lägg till/ta bort snapin-moduler**.  

    2.  I dialogrutan **Lägg till/ta bort snapin-modul** väljer du **Certifikat** i listan över **Tillgängliga snapin-moduler**och klickar sedan på **Lägg till**.  

    3.  I dialogrutan **Snapin-modulen Certifikat** väljer du **Datorkonto** och klickar sedan på **Nästa**.  

    4.  I dialogrutan **Välj dator** kontrollerar du att **Lokal dator: (den dator den här konsolen körs på)** har valts och klickar sedan på **Slutför**.  

    5.  I dialog rutan **Lägg till eller ta bort snapin-moduler** klickar du på **OK**.  

    6.  I-konsolen expanderar du **certifikat (lokal dator)**, expanderar **personliga**och väljer **certifikat**.  

    7.  Högerklicka på certifikatet med det egna namnet på ConfigMgr- **SQL Server identifierings certifikat**, klicka på **alla uppgifter**och välj sedan **Exportera**.  

    8.  Slutför **guiden Exportera certifikat** genom att använda standardalternativen och spara certifikatet med filnamnstillägget **.cer** .  

2.  Utför följande steg på hanterings plats datorn för att lägga till det självsignerade certifikatet för databas replik servern i certifikat arkivet Betrodda personer på hanterings platsen:  

    1.  Upprepa föregående steg 1.a till 1.e så här konfigurerar du snapin-modulen **certifikat** i MMC på hanterings plats datorn.  

    2.  Expandera **certifikat (lokal dator)** i konsolen, expandera **Betrodda personer**, högerklicka på **certifikat**, Välj **alla aktiviteter**och välj sedan **Importera** för att starta **guiden Importera certifikat**.  

    3.  På sidan **Fil som ska importeras** väljer du det certifikat som har sparats i steg 1h. Klicka sedan på **Nästa**.  

    4.  På sidan **Certifikatarkiv** väljer du **Placera alla certifikat i nedanstående arkiv**och kontrollerar att **Betrodda personer** har angetts för **Certifikatarkiv**. Klicka på **Nästa**.  

    5.  Klicka på **Slutför** för att stänga guiden och slutföra certifikatkonfigureringen på hanteringsplatsen.  

###  <a name="step-5---configure-the-sql-server-service-broker-for-the-database-replica-server"></a><a name="BKMK_DBreplica_SSB"></a>Steg 5 – Konfigurera SQL Server Service Broker för databas replik servern  
Om du vill använda klientmeddelanden med en databasreplik för en hanteringsplats, måste du konfigurera SQL Server Service Broker för kommunikationen mellan platsdatabasservern och databasreplikservern. Det innebär att du konfigurerar varje databas med information om den andra databasen, och att certifikaten utväxlas mellan de två databaserna, så att kommunikationen skyddas.  

> [!NOTE]  
>  Innan du kan utföra nedanstående procedur måste initial synkronisering mellan databasreplikservern och platsdatabasservern vara slutförd.  

 I följande procedur ändras inte den Service Broker-port som har konfigurerats i SQL Server för platsdatabasservern eller databasreplikservern. I stället konfigureras varje databas för kommunikation med den andra databasen, via rätt Service Broker-port.  

 Använd följande procedur för att konfigurera Service Broker för platsdatabasservern och databasreplikservern.  

##### <a name="to-configure-the-service-broker-for-a-database-replica"></a>Konfigurera Service Broker för en databasreplik  

1. Använd **SQL Server Management Studio** för att ansluta till databas replik serverns databas och kör sedan följande fråga för att aktivera Service Broker på databas replik servern: **Alter Database &lt; replica Database Name \> SET ENABLE_BROKER, HONOR_BROKER_PRIORITY på med omedelbar återgång**  

2. Konfigurera sedan Service Broker (på databasreplikservern) för klientmeddelanden och exportera Service Broker-certifikatet. Det gör du genom att köra en SQL Server-lagrad procedur som konfigurerar Service Broker och exporterar certifikatet i en enda åtgärd. När du kör den lagrade proceduren måste du ange ett FQDN för databasreplikservern och namnet på databasreplikdatabasen samt en plats dit certifikatfilen ska exporteras.  

    Kör följande fråga för att konfigurera den information som krävs på databas replik servern och exportera certifikatet för databas replik servern: **EXEC sp_BgbConfigSSBForReplicaDB &lt; replik SQL Server FQDN \> , &lt; replik databas namn \> , &lt; sökväg för certifikat säkerhets kopierings fil \> **  

   > [!NOTE]  
   >  Om databasreplikservern inte finns på standardinstansen av SQL Server, måste du i det här steget ange instansnamnet, utöver replikdatabasnamnet. Det gör du genom att ersätta ** &lt; replik databasens namn \> ** med ** &lt; instans namnet \\ replik \> databas namn**.  

    När du har exporterat certifikatet från databasreplikservern placerar du en kopia av certifikatet på den primära platsens databasserver.  

3. Använd **SQL Server Management Studio** för att ansluta till den primära platsens databas. När du har anslutit till den primära platsens databas kör du en fråga för att importera certifikatet och ange den Service Broker-port som används på databasreplikservern. Ange ett FQDN för databasreplikservern och namnet på databasreplikdatabasen. Därmed konfigureras den primära platsens databas att använda Service Broker för kommunikation med databasreplikserverns databas.  

    Kör följande fråga för att importera certifikatet från databas replik servern och ange nödvändig information: **EXEC SP_BGBCONFIGSSBFORREMOTESERVICE replik, &lt; SQL Service Broker port \> , &lt; certifikat fil sök väg \> , &lt; replik SQL Server FQDN \> , &lt; replik databas namn \> **  

   > [!NOTE]  
   >  Om databasreplikservern inte finns på standardinstansen av SQL Server, måste du i det här steget ange instansnamnet, utöver replikdatabasnamnet. Det gör du genom att ersätta ** &lt; namnet \> på replik databasen** med namnet på **\Instance \\ \> namn replik databasen**.  

4. Kör sedan följande kommando på plats databas servern för att exportera certifikatet för plats databas servern: **EXEC Sp_BgbCreateAndBackupSQLCert &lt; sökväg för certifikat säkerhets kopierings fil \> **  

    När du har exporterat certifikatet från platsdatabasservern placerar du en kopia av certifikatet på databasreplikservern.  

5. Använd **SQL Server Management Studio** för att ansluta till databasreplikserverns databas. När du har anslutit till databasreplikserverns databas kör du en fråga för att importera certifikatet. Ange platskoden för den primära platsen och ange den Service Broker-port som används på platsdatabasservern. Därmed konfigureras databasreplikservern att använda Service Broker för kommunikation med den primära platsens databas.  

    Kör följande fråga för att importera certifikatet från plats databas servern: **EXEC sp_BgbConfigSSBForRemoteService ' &lt; platskod \> ', ' &lt; SQL Service Broker port \> ', ' &lt; certifikat fil Sök väg \> '**  

   Några minuter efter att du har slutfört konfigureringen av platsdatabasen och databasreplikdatabasen, konfigureras Service Broker-konversation för klientmeddelanden från den primära platsdatabasen till databasrepliken.  

###  <a name="supplemental-script-for-additional-database-replicas-on-a-single-sql-server"></a><a name="bkmk_supscript"></a>Kompletterande skript för ytterligare databas repliker på en enda SQL Server  
 När du använder skriptet från steg 4 för att konfigurera ett självsignerat certifikat för databas replik servern på en SQL Server som redan har en databas replik som du planerar att använda, måste du använda en modifierad version av det ursprungliga skriptet. Följande ändringar förhindrar att skriptet tar bort ett befintligt certifikat på servern och skapar efterföljande certifikat med unika egna namn.  Redigera det ursprungliga skriptet på följande sätt:  

-   Kommentera ut (förhindra att den körs) varje rad mellan skript posterna **# ta bort befintligt certifikat om det finns ett sådant** och **# skapa det nya certifikatet**. Det gör du genom att lägga till ett **#** som första bokstaven för varje tillämplig rad.  

-   För varje efterföljande databasreplik använder du det här skriptet för att konfigurera och uppdatera det egna namnet för certifikatet.  Det gör du genom att redigera rad **$Enrollment. CertificateFriendlyName = "ConfigMgr SQL Server Identification Certificate"** och Ersätt **configmgr-SQL Server identifierings certifikat** med ett nytt namn, t. ex. **ConfigMgr SQL Server Identification Certificate1**.  

##  <a name="manage-database-replica-configurations"></a><a name="BKMK_DBReplicaOps"></a>Hantera konfigurationer av databas repliker  
 När en databasreplik används på en plats kan du använda följande avsnitt om du behöver information om hur du avinstallerar en databasreplik, avinstallerar en plats där en databasreplik används eller flyttar en platsdatabas till en ny installation av SQL Server. Om du använder informationen i nedanstående avsnitt när du tar bort publiceringar, ska du följa instruktionerna för borttagning av transaktionsreplikering för databasreplikeringens SQL Server-version. Mer information finns i [ta bort en publikation](https://docs.microsoft.com/sql/relational-databases/replication/publish/delete-a-publication?view=sql-server-ver15).  

> [!NOTE]  
>  När du har återställt en platsdatabas som var konfigurerad för databasreplikeringar, måste du konfigurera om alla databasreplikeringar innan du kan använda dem. Du måste då återskapa både publiceringarna och prenumerationerna.  

###  <a name="uninstall-a-database-replica"></a><a name="BKMK_UninstallDbReplica"></a> Avinstallera en databasreplik  
 När du använder en databasreplikering för en hanteringsplats kanske du måste avinstallera databasreplikeringen under en period och sedan konfigurera om den för användning. Du måste till exempel ta bort databas repliker innan du uppgraderar en Configuration Manager-plats till en ny service pack. När platsen har uppgraderats kan du återställa databasreplikeringen för användning.  

 Använd följande steg för att avinstallera en databasreplikering.  

1.  I arbets ytan **Administration** i Configuration Manager-konsolen expanderar du **plats konfiguration**och väljer sedan **system roller för servrar och platser**. i informations fönstret väljer du den plats system server som är värd för hanterings platsen som använder databas repliken som du vill avinstallera.  

2.  I rutan **Platssystemroller** högerklickar du på **Hanteringsplats** och väljer **Egenskaper**.  

3.  På fliken **Hanteringsplatsdatabas** väljer du **Använd platsdatabasen** för att konfigurera hanteringsplatsen att använda platsdatabasen i stället för databasrepliken. Klicka på **OK** för att spara konfigurationen.  

4.  Använd sedan **SQL Server Management Studio** för att utföra följande uppgifter:  

    -   Ta bort publiceringen av databasreplikeringen från platsserverdatabasen.  

    -   Ta bort prenumerationen för databasreplikeringen från databasreplikservern.  

    -   Ta bort replikdatabasen från databasreplikservern.  

    -   Inaktivera publicering och distribution på platsdatabasservern. Om du vill inaktivera publicering och distribution högerklickar du på mappen replikering och klickar sedan på **Inaktivera publicering och distribution**.  

5.  När du har tagit bort publicering, prenumeration och replikdatabasen och inaktiverat publicering på platsdatabasservern, är databasreplikeringen avinstallerad.  

###  <a name="uninstall-a-site-server-that-publishes-a-database-replica"></a><a name="BKMK_DBReplicaOps_Uninstall"></a> Avinstallera en platsserver som publicerar en databasreplik  
 Innan du installerar en plats som publicerar en databasreplikering ska du utföra nedanstående steg för att rensa publiceringen och eventuella prenumerationer.  

1.  Använd **SQL Server Management Studio** för att ta bort databasreplikpubliceringen från platsserverdatabasen.  

2.  Använd **SQL Server Management Studio** för att ta bort databasens replikprenumeration från varje fjärr-SQL Server som har en databasreplik för platsen.  

3.  Avinstallera platsen.  

###  <a name="move-a-site-server-database-that-publishes-a-database-replica"></a><a name="BKMK_DBReplicaOps_Move"></a> Flytta en platsserverdatabas som publicerar en databasreplik  
 Använd följande steg när du flyttar platsdatabasen till en ny dator:  

1.  Använd **SQL Server Management Studio** för att ta bort publiceringen av databasrepliken från platsserverdatabasen.  

2.  Använd **SQL Server Management Studio** för att ta bort publiceringen av databasrepliken från varje databasreplikserver för platsen.  

3.  Flytta databasen till den nya SQL Server-datorn. Mer information finns i avsnittet [ändra plats databasens konfiguration](../../../../core/servers/manage/modify-your-infrastructure.md#bkmk_dbconfig) i avsnittet [ändra Configuration Manager infrastruktur](../../../../core/servers/manage/modify-your-infrastructure.md) .  

4.  Återskapa publiceringen av databasreplikeringen på platsdatabasservern. Mer information finns i [Steg 1 – Konfigurera platsdatabasservern för publicering av databasrepliken](#BKMK_DBReplica_ConfigSiteDB) i det här avsnittet.  

5.  Återskapa prenumerationerna för databasreplikeringen på varje databasreplikserver. Mer information finns i [Steg 2 – Konfigurera databasreplikservern](#BKMK_DBReplica_ConfigSrv) i det här avsnittet.  
