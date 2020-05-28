---
title: Skapa ett labb
titleSuffix: Configuration Manager
description: Konfigurera ett labb för att utvärdera Configuration Manager med simulerade aktiviteter i real tid.
ms.date: 09/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b1970688-0cd2-404f-a17f-9e2aa4a78758
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 216c61a671d7d06e434fa399bb3bae12e12f7275
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905171"
---
# <a name="set-up-a-configuration-manager-lab"></a>Konfigurera ett Configuration Manager labb

*Gäller för: Configuration Manager (aktuell gren)*

Genom att följa anvisningarna i det här avsnittet kan du konfigurera ett labb för att utvärdera Configuration Manager med simulerade aktiviteter i real tid.  

> [!NOTE]
> Microsoft erbjuder en förkonfigurerad version av labbet med en utvärderings version av Configuration Manager. Mer information finns i [distributions-och hanterings labb paket för Windows och Office](https://docs.microsoft.com/microsoft-365/enterprise/modern-desktop-deployment-and-management-lab). 

##  <a name="core-components"></a><a name="BKMK_LabCore"></a> Huvudkomponenter  
 Att konfigurera din miljö för Configuration Manager kräver vissa kärn komponenter för att stödja installationen av Configuration Manager.    

-   **Labb miljön använder Windows Server 2012 R2**, där vi kommer att installera Configuration Manager.  

     Du kan ladda ned en utvärderings version av Windows Server 2012 R2 från [utvärderings centret](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012).  

     Överväg att ändra eller inaktivera Förbättrad säkerhets konfiguration i Internet Explorer för att lättare komma åt några av de hämtade filerna som refereras till under de här övningarna. Mer information finns i [Internet Explorer: förbättrad säkerhets konfiguration](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd883248(v=ws.10)).  

-   **I labbmiljön används SQL Server 2012 SP2** för platsdatabasen.  

     Du kan ladda ned en utvärderings version av SQL Server 2012 från [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=43340).  

     SQL Server har [versioner av SQL Server som stöds](../../core/plan-design/configs/support-for-sql-server-versions.md#bkmk_SQLVersions) och som måste uppfyllas för användning med Configuration Manager.  

    -   Configuration Manager kräver en 64-bitars version av SQL Server som värd för plats databasen.  

    -   **SQL_Latin1_General_CP1_CI_AS** som klassen **SQL-sortering** .  

    -   **Windows-autentisering**, [och inte SQL-autentisering](https://docs.microsoft.com/sql/relational-databases/security/choose-an-authentication-mode?view=sql-server-ver15), krävs.  

    -   En dedikerad **SQL Server instans** krävs.  

    -   Begränsa inte **system Adressable-minnet** för SQL Server.  

    -   Konfigurera **SQL Server tjänst kontot** att köras med ett domän användar konto med låg behörighet.  

    -   Du måste installera **SQL Server repor ting Services**.  

    -   **Kommunikation mellan platser** använder SQL Server Service Broker på standardporten TCP 4022.  

    -   **Kommunikation mellan platser** mellan SQL Server databas motor och välj Configuration Manager plats system roller Använd standard porten TCP 1433.  

-   Domänkontrollanten **använder Windows Server 2008 R2** med Active Directory Domain Services installerat. Domänkontrollanten fungerar även som värd för DHCP-och DNS-servrarna för användning med ett fullständigt kvalificerat domän namn.  

     Mer information finns i [Översikt över Active Directory Domain Services](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831484(v=ws.11)).  

-   **Hyper-V används med ett fåtal virtuella datorer** för att kontrol lera att de hanterings steg som vidtas i de här övningarna fungerar som förväntat. Minst tre virtuella datorer rekommenderas med Windows 10 installerat.  

     Mer information finns i [Översikt över Hyper-V](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831531(v=ws.11)).  

-   **Administratörsbehörighet** krävs för samtliga komponenter.  

    -   Configuration Manager kräver en administratör med lokala behörigheter i Windows Server-miljön  

    -   Active Directory kräver en administratör med behörighet att ändra schemat  

    -   Virtuella datorer kräver behörighet till själva datorerna  

Även om det inte krävs för det här labbet kan du granska de [konfigurationer som stöds för Configuration Manager](../../core/plan-design/configs/supported-configurations.md) ytterligare information om kraven för att implementera Configuration Manager. Läs dokumentationen för andra program varu versioner än de som hänvisas till här.  

När du har installerat alla dessa komponenter måste du vidta ytterligare åtgärder för att konfigurera Windows-miljön för Configuration Manager:  

##  <a name="prepare-active-directory-content-for-the-lab"></a><a name="BKMK_LabADPrep"></a> Förbered Active Directory-innehåll för övningen  
 I den här övningen ska du skapa en säkerhetsgrupp och sedan lägga till en domänanvändare i den.  

-   Säkerhetsgrupp: **Evaluation**  

    -   Gruppomfång: **Universal**  

    -   Grupptyp: **säkerhet**  

-   Domänanvändare: **ConfigUser**  

     I vanliga fall beviljar du inte universell åtkomst till alla användare i miljön. I det här fallet gör du det med den här användaren för att förenkla övningen online.  

Nästa steg som krävs för att göra det möjligt för Configuration Manager klienter att fråga Active Directory Domain Services för att hitta plats resurser visas i nästa procedur.  

##  <a name="create-the-system-management-container"></a><a name="BKMK_CreateSysMgmtLab"></a> Skapa System Management-containern  
 Configuration Manager skapar inte automatiskt den begärda System Management-behållaren i Active Directory Domain Services när schemat utökas. Du måste därför själv skapa den för övningen. Det här steget kräver att du [installerar ADSI Edit](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc773354(v=ws.10)).

 Kontrollera att du är inloggad som ett konto med behörighet för att **Skapa alla underordnade objekt** för **System**-containern i Active Directory Domain Services.  

#### <a name="to-create-the-system-management-container"></a>Skapa System Management-containern:  

1.  Kör **ADSI Edit**och anslut till den domän där platsservern finns.  

2.  Expandera **domän &lt; datorns fullständigt kvalificerade domän \> namn**, expandera **<unikt \> namn**, högerklicka på **CN = System**, klicka på **ny**och klicka sedan på **objekt**.  

3.  I dialogrutan **Skapa objekt** väljer du **Container** och klickar sedan på **Nästa**.  

4.  I rutan **Värde** skriver du **System Management**och klickar sedan på **Nästa**.  

5.  Slutför proceduren genom att klicka på **Slutför** .  

##  <a name="set-security-permissions-for-the-system-management-container"></a><a name="BKMK_SetSecPermLab"></a> Ange säkerhetsbehörighet för System Management-containern  
 Ge platsserverns datorkonto behörighet att publicera platsinformation i containern. Du kommer även använda ADSI-redigering för den här uppgiften.  

> [!IMPORTANT]  
>  Kontrollera att du är ansluten till platsserverdomänen innan du fortsätter.  

#### <a name="to-set-security-permissions-for-the-system-management-container"></a>Ange säkerhetsbehörighet för System Management-containern:  

1.  Expandera **plats serverns domän**i konsol fönstret, expandera **DC = &lt; serverns unika namn \> **och expandera sedan **CN = System**. Högerklicka på **CN=System Management**och klicka sedan på **Egenskaper**.  

2.  I dialogrutan **Egenskaper för CN=System Management** klickar du på fliken **Säkerhet** . Klicka sedan på **Lägg till** och lägg till platsserverns datorkonto. Ge kontot behörigheten **Fullständig behörighet** .  

3.  Klicka på **Avancerat**, Välj plats serverns dator konto och klicka sedan på **Redigera**.  

4.  I listan **Tillämpa på** väljer du **Objektet och alla underordnade objekt**.  

5.  Klicka på **OK** . Konsolen **ADSI-redigering** stängs och proceduren slutförs.  

     Mer information finns i [utöka Active Directory-schemat för Configuration Manager](../../core/plan-design/network/extend-the-active-directory-schema.md)  

##  <a name="extend-the-active-directory-schema-using-extadschexe"></a><a name="BKMK_ExtADSchLab"></a> Utöka Active Directory-schemat med extadsch.exe  
 Du utökar Active Directory schema för den här övningen så att du kan använda alla Configuration Manager funktioner och funktioner med minsta möjliga administrativa kostnader. Utökning av Active Directory-schemat är en konfiguration för hela skogen som görs en gång per skog. När du utökar schemat permanent ändras uppsättningen av klasser och attribut i den grundläggande Active Directory-konfigurationen. Den här åtgärden går inte att ångra. Genom att utöka schemat kan Configuration Manager få åtkomst till komponenter som gör det möjligt för dem att fungera effektivt i din labb miljö.  

> [!IMPORTANT]  
>  Kontrollera att du är inloggad på schemats huvuddomänkontrollant med ett konto som tillhör säkerhetsgruppen **Schemaadministratörer** . Det går inte använda alternativa autentiseringsuppgifter.  

#### <a name="to-extend-the-active-directory-schema-using-extadschexe"></a>Utöka Active Directory-schemat med extadsch.exe:  

1.  Skapa en säkerhets kopia av system tillstånd för schemats huvuddomänkontrollant. Mer information om hur du säkerhetskopierar huvud domänkontrollanten finns [Windows Server Backup](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770757(v=ws.11))  

2.  Gå till **\SMSSETUP\BIN\X64** på installationsmediet.  

3.  Kör **extadsch.exe**.  

4.  Kontrollera att schemat har utökats genom att titta i **extadsch.log** som finns i rotmappen på enheten.  

     Mer information finns i [utöka Active Directory-schemat för Configuration Manager](../../core/plan-design/network/extend-the-active-directory-schema.md).  

##  <a name="other-required-tasks"></a><a name="BKMK_OtherTasksLab"></a> Andra nödvändiga uppgifter  
 Följande uppgifter måste utföras före installationen.  

 **Skapa en mapp där nedladdade filer ska lagras**  

 Under den här övningen kommer du behöva ladda ned många filer för installationsmediets komponenter. Innan du börjar bör du utse en plats där filerna kan sparas tills du är färdig med labbövningen. Bäst är att använda en enda mapp med separata undermappar.  

 **Installera .NET och aktivera Windows Communication Foundation**  

 Du måste installera två .NET Framework-program: först .NET 3.5.1 och sedan .NET 4.5.2+. Du måste också aktivera WCF (Windows Communication Foundation). WCF är utformat för att göra det lättare att hantera distribuerad datorbehandling, med bred samverkan och direktstöd för tjänstorientering, och underlättar dessutom utvecklingen av anslutna program via en tjänstorienterad programmeringsmodell. Mer information finns i [Vad är Windows Communication Foundation?](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms731082(v=vs.90)).

#### <a name="to-install-net-and-activate-windows-communication-foundation"></a>Installera .NET och aktivera Windows Communication Foundation:  

1.  Öppna **Server Manager**och gå till **Hantera**. Klicka på **Lägg till roller och funktioner** för att öppna **guiden Lägg till roller och funktioner.**  

2.  Läs igenom informationen i fönstret **Innan du börjar** och klicka sedan på **Nästa**.  

3.  Välj **Rollbaserad eller funktionsbaserad installation**och klicka sedan på **Nästa**.  

4.  Markera din server i **Serverpool**och klicka sedan på **Nästa**.  

5.  Läs igenom informationen i fönstret **Serverroller** och klicka sedan på **Nästa**.  

6.  Lägg till följande **funktioner** genom att markera dem i listan:  

    -   **Funktioner i .NET Framework 3.5**  

        -   **.NET Framework 3.5 (inklusive.NET 2.0 och 3.0)**  

    -   **Funktioner i .NET Framework 4.5**  

        -   **.NET Framework 4.5**  

        -   **ASP.NET 4.5**  

        -   **WCF-tjänster**  

            -   **HTTP-aktivering**  

            -   **Delning av TCP-port**  

7.  Läs igenom informationen på skärmen **Webbserverroll (IIS)** och **Rolltjänster** och klicka sedan på **Nästa**.  

8.  Läs igenom informationen på skärmen **Bekräftelse** och klicka sedan på **Nästa**.  

9. Klicka på **Installera** och kontrollera att installationen har slutförts ordentligt i fönstret **Meddelanden** i **Serverhanteraren**.  

10. När grundinstallationen av .NET är klar går du till [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=42643) för att hämta webbinstallationsprogrammet för .NET Framework 4.5.2. Klicka på knappen **Ladda ned** och sedan på **Kör** så att installationsprogrammet körs. Alla komponenter som måste installeras upptäcks automatiskt och installeras på det språk du valt.  

**Aktivera BITS, IIS och RDC**  

[BITS (Background Intelligent Transfer Service)](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn282296(v=ws.11)) används för program där filer måste överföras asynkront mellan en klient och en server. Med BITS bevaras svarstiden hos andra nätverksprogram genom att flödet av överföringar mäts i förgrunden och bakgrunden. Filöverföringar återupptas automatiskt om en överföring avbryts.  

För den här övningen installerar du BITS eftersom platsservern även ska användas som hanteringsplats.  

IIS (Internet Information Services) är en flexibel och skalbar webbserver som kan användas som värd för vad som helst på webben. Den används av Configuration Manager för ett antal plats system roller. Om du vill ha mer information om IIS granskar du [webbplatser för plats system servrar](../../core/plan-design/network/websites-for-site-system-servers.md).  

[RDC (Remote Differential Compression)](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754372(v=ws.11)) är en uppsättning API:er som kan användas av program för att ta reda på om några ändringar gjorts i en grupp filer. Tack vare RDC replikeras endast de ändrade delarna av en fil vilket håller nere nätverkstrafiken till et minimum.  

#### <a name="to-enable-bits-iis-and-rdc-site-server-roles"></a>Aktivera BITS-, IIS- och RDC-platssystemroller:  

1.  Öppna **Server Manager**på platsservern. Navigera till **Hantera**. Klicka på **Lägg till roller och funktioner** och öppna **Guiden Lägg till roller och funktioner**.  

2.  Läs igenom informationen i fönstret **Innan du börjar** och klicka sedan på **Nästa**.  

3.  Välj **Rollbaserad eller funktionsbaserad installation**och klicka sedan på **Nästa**.  

4.  Markera din server i **Serverpool**och klicka sedan på **Nästa**.  

5.  Lägg till följande **serverroller** genom att markera dem i listan:  

    -   **Web Server (IIS)**  

        -   **Vanliga HTTP-funktioner**  

            -   **Standard dokument**  

            -   **Katalogbläddring**  

            -   **HTTP-fel**  

            -   **Statiskt innehåll**  

            -   **HTTP-omdirigering**  

        -   **Hälsa och diagnostik**  

            -   **HTTP-loggning**  

            -   **Loggningsverktyg**  

            -   **Övervakare för begäran**  

            -   **Spårning**  

    -   **Prestanda**  

        -   **Komprimering av statiskt innehåll**  

        -   **Komprimering av dynamiskt innehåll**  

    -   **Säkerhet**  

        -   **Filtrering av förfrågningar**  

        -   **Grundläggande autentisering**  

        -   **Autentisering av klient certifikats mappning**  

        -   **IP-och domän begränsningar**  

        -   **URL-auktorisering**  

        -   **Windows-autentisering**  

    -   **Program utveckling**  

        -   **.NET Extensibility 3.5**  

        -   **.NET Extensibility 4.5**  

        -   **ASP**  

        -   **ASP.NET 3.5**  

        -   **ASP.NET 4.5**  

        -   **ISAPI-tillägg**  

        -   **ISAPI-filter**  

        -   **SSI (SSI (Server Side Includes))**  

    -   **FTP-server**  

        -   **FTP-tjänst**  

    -   **Hanteringsverktyg**  

        -   **IIS-hanteringskonsol**  

        -   **IIS 6-hanteringskompatibilitet**  

            -   **IIS 6-metabaskompatibilitet**  

            -   **IIS 6-hanteringskonsol**  

            -   **IIS 6-skriptverktyg**  

            -   **IIS 6 WMI-kompatibilitet**  

        -   **IIS 6-hanteringsskript och verktyg**  

        -   **Hanteringstjänst**  

6.  Lägg till följande **funktioner** genom att markera dem i listan:  

    -   **Background Intelligent Transfer Service (BITS)**  

          -   **IIS-servertillägg**  

    -   **Fjärradministrationsverktyg för server**  

          -   **Funktionsadministrationsverktyg**  

          -   **Verktyg för BITS-servertillägg**  

7.  Klicka på **Installera** och kontrollera att installationen har slutförts ordentligt i fönstret **Meddelanden** i **Serverhanteraren**.  

Som standard blockerar IIS flera filnamnstillägg och platser från åtkomst via HTTP eller HTTPS. Om du vill att filerna ska kunna distribueras på klientsystem måste du ställa in begäransfiltrering för IIS på distributionsplatsen. Mer information finns i [filtrering av IIS-förfrågningar för distributions platser](../../core/plan-design/network/prepare-windows-servers.md#BKMK_IISFiltering).  

#### <a name="to-configure-iis-filtering-on-distribution-points"></a>Ställa in IIS-filtrering på distributionsplatser:  

1.  Öppna **IIS Manager** och markera namnet på din server i sidopanelen. Du kommer då till **Start** -skärmen.  

2.  Kontrollera att **Visa funktioner** är markerat längst ned på **Start** -skärmen. Gå till **IIS** och öppna **Begäransfiltrering**.  

3.  I fönstret **Åtgärder** klickar du på **Tillåt filnamnstillägg...**  

4.  Skriv **.msi** i dialogrutan och klicka på **OK**.  

##  <a name="installing-configuration-manager"></a><a name="BKMK_InstallCMLab"></a> Installera Configuration Manager  
Du kan skapa ett [avgörande när du ska använda en primär plats](../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md#BKMK_ChoosePriimary) för att hantera klienter direkt. Detta gör det möjligt för din labb miljö att stödja hantering av [plats system skala](../plan-design/configs/size-and-scale-numbers.md) för potentiella enheter.  
Under den här processen installerar du också Configuration Manager-konsolen som används för att hantera dina utvärderings enheter framåt.  

Innan du påbörjar installationen startar du  [Prerequisite Checker](../servers/deploy/install/prerequisite-checker.md) på Windows Server 2012-servern och kontrollerar att alla inställningar är korrekta.  

#### <a name="to-download-and-install-configuration-manager"></a>Ladda ned och installera Configuration Manager:  

1.  Gå till sidan [System Center-utvärderingar](https://www.microsoft.com/evalcenter/evaluate-system-center-2012-configuration-manager-and-endpoint-protection) för att ladda ned den senaste utvärderings versionen av Configuration Manager.  

2.  Dekomprimera de nedladdade filerna på den plats du bestämt.  

3.  Följ installations proceduren som visas i [installera en plats med hjälp av installations guiden för Configuration Manager](../servers/deploy/install/use-the-setup-wizard-to-install-sites.md). Under installationen anger du följande:  

    |Steg under platsinstallationen:|Urval|  
    |-----------------------------------------|---------------|  
    |Steg 4: sidan **Produktnyckel**|Välj **Utvärdering**.|  
    |Steg 7:  **Nödvändiga nedladdningar**|Välj **Ladda ned nödvändiga filer** och ange den fördefinierade platsen.|  
    |Steg 10: **Plats- och installationsinställningar**|-   **Platskod:LAB**<br />-   **Platsnamn:Evaluation**<br />-   **Installationsmapp:** ange den fördefinierade platsen.|  
    |Steg 11: **Installation av primär plats**|Välj **Installera den primära platsen som en fristående plats**och klicka sedan på **Nästa**.|  
    |Steg 12: **Databasinstallation**|-   **SQL Server-namn (FQDN):** ange fullständigt domännamn här.<br />-   **Instansnamn:** lämna det tomt eftersom du ska använda standardinstansen av SQL som du redan har installerat.<br />-   **Service Broker-port:** låt stå som standardport 4022.|  
    |Steg 13: **Databasinstallation**|Låt standardinställningarna stå kvar.|  
    |Steg 14: **SMS-provider**|Låt standardinställningarna stå kvar.|  
    |Steg 15: **Klientkommunikationsinställningar**|Kontrollera att **Alla roller för platssystem accepterar endast HTTPS-kommunikation från kunder** är avmarkerat|  
    |Steg 16: **Platssystemroller**|Ange fullständigt domännamn och kontrollera att alternativet **Alla roller för platssystem accepterar endast HTTPS-kommunikation från kunder** fortfarande är avmarkerat.|  

##  <a name="enable-publishing-for-the-configuration-manager-site"></a><a name="BKMK_EnablePubLab"></a>Aktivera publicering för den Configuration Manager webbplatsen  
Varje Configuration Manager-plats publicerar sin egen sitespecifika information till System Management-behållaren inom dess katalogpartition i Active Directory schemat. Dubbelriktade kanaler för kommunikation mellan Active Directory och Configuration Manager måste öppnas för att hantera den här trafiken. Du aktiverar dessutom Forest Discovery för att avgöra vissa komponenter i din Active Directory- och nätverksinfrastruktur.  

#### <a name="to-configure-active-directory-forests-for-publishing"></a>Konfigurera Active Directory-skogar för publicering:  

1.  Klicka på **Administration**i det nedre vänstra hörnet i Configuration Manager-konsolen.  

2.  I arbetsytan **Administration** visar du **Hierarkikonfiguration**och klickar sedan på **Identifieringsmetoder**.  

3.  Välj **Identifiering av Active Directory-skogar** och klicka på **Egenskaper**.  

4.  I dialogrutan **Egenskaper** väljer du **Aktivera identifiering av Active Directory-skogar**. Välj sedan **Skapa Active Directory-platsgränser automatiskt när de identifieras**. En dialogruta visas med texten **Vill du köra fullständig identifiering så snart som möjligt?** Klicka på **Ja**.  

5.  I gruppen **Identifieringsmetod** längst upp på skärmen, klickar du på **Kör identifiering av skog nu**och går sedan till **Active Directory-skogar** i sidopanelen. Nu bör din Active Directory-skog visas i listan över identifierade skogar.  

6.  Gå till fliken **Allmänt** längst upp på skärmen.  

7.  I arbetsytan **Administration** visar du **Hierarkikonfiguration**och klickar sedan på **Active Directory-skogar**.  

#### <a name="to-enable-a-configuration-manager-site-to-publish-site-information-to-your-active-directory-forest"></a>Så här aktiverar du en Configuration Manager webbplats för att publicera plats information till din Active Directory-skog:  

1.  Klicka på **Administration**i Configuration Manager-konsolen.  

2.  Du ska konfigurera en ny skog som ännu inte har identifierats.  

3.  Klicka på **Active Directory-skogar** på arbetsytan **Administration**.  

4.  På fliken **Publicering** i platsegenskaperna väljer du den anslutna skogen och klickar sedan på **Ok** för att spara konfigurationen.
