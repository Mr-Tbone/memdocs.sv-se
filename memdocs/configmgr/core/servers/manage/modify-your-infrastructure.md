---
title: Modifiera infrastruktur
titleSuffix: Configuration Manager
description: Gör ändringar eller vidta åtgärder som påverkar Configuration Manager-infrastrukturen.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a7975dc8-46ab-4dae-86b6-dc3e3cf3b2f0
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 92bf86225cf869622fd4b496fd3e8e852b651a70
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713676"
---
# <a name="modify-your-configuration-manager-infrastructure"></a>Ändra din Configuration Manager-infrastruktur

*Gäller för: Configuration Manager (aktuell gren)*

När du har installerat en eller flera platser kan du behöva ändra konfigurationer eller vidta åtgärder som påverkar din infrastruktur.

## <a name="manage-the-sms-provider"></a><a name="BKMK_ManageSMSprovider"></a>Hantera SMS-providern

SMS-providern tillhandahåller den administrativa kontakt punkten för en eller flera Configuration Manager-konsoler. När du installerar flera SMS-providrar kan du tillhandahålla redundans för kontakt punkter för att administrera din plats och hierarki.

På varje Configuration Manager plats kan du köra installations programmet på nytt för att:

- Lägg till ytterligare en instans av SMS-providern. Varje ytterligare instans av SMS-providern måste finnas på en separat dator.

- Ta bort en instans av SMS-providern. Om du vill ta bort den sista SMS-providern för en plats måste du avinstallera platsen.

Övervaka installationen eller borttagningen av SMS-providern genom att visa **ConfigMgrSetup. log** i rotmappen på plats servern där du kör installations programmet.

Innan du ändrar SMS-providern på en plats, se [Planera för SMS-providern](../../plan-design/hierarchy/plan-for-the-sms-provider.md).

### <a name="manage-the-sms-provider-configuration-for-a-site"></a>Hantera konfigurationen av SMS-providern för en plats  

1. Kör **Configuration Manager** -installationen `\BIN\X64\setup.exe` från i mappen Configuration Manager plats installation.

1. På sidan **komma igång** väljer du **utför plats underhåll eller Återställ den här platsen**.

1. På sidan **plats underhåll** väljer du **modifiera konfiguration av SMS-provider**.

1. På sidan **Hantera SMS-providers** väljer du ett av följande alternativ:

    - **Lägg till en ny SMS-provider**: Ange det fullständiga domän namnet för en dator som är värd för SMS-providern som inte är värd för den.

    - **Avinstallera den angivna SMS-providern**: Välj namnet på datorn från vilken du vill ta bort SMS-providern.

    > [!TIP]  
    > Om du vill flytta SMS-providern mellan två datorer måste du först installera den på den nya datorn. Ta sedan bort den från den ursprungliga platsen. Det finns inget alternativ för att flytta SMS-providern mellan datorer.

När installations guiden har slutförts slutförs konfigurationen av SMS-providern. I plats **egenskaperna**går du till fliken **Allmänt** och kontrollerar de datorer som har en SMS-provider installerad för en plats.

## <a name="manage-the-configuration-manager-console"></a><a name="bkmk_Console"></a>Hantera Configuration Manager-konsolen

Följande uppgifter hjälper dig att hantera Configuration Manager-konsolen:

- Information om hur du ändrar språket som visas i Configuration Manager-konsolen finns i avsnittet [hantera Configuration Manager konsol språk](#BKMK_ManageConsoleLanguages) .

- Information om hur du installerar ytterligare konsoler finns i [installera Configuration Manager-konsoler](../deploy/install/install-consoles.md).

- Information om hur du konfigurerar DCOM-behörigheter för att aktivera konsoler som är fjärranslutna från plats servern finns i avsnittet [Konfigurera DCOM-behörigheter för fjärranslutna Configuration Manager konsoler](#BKMK_ConfigDCOMforRemoteConsole) .

- Information om hur du ändrar administrativa behörigheter för att begränsa vad användarna kan se och göra i konsolen finns i [ändra den administrativa användarens administrativa omfattning](../deploy/configure/configure-role-based-administration.md#BKMK_ModAdminUser).

### <a name="manage-configuration-manager-console-language"></a><a name="BKMK_ManageConsoleLanguages"></a>Hantera Configuration Manager-konsolens språk

Under installationen av plats servern kopieras installationsfilerna för Configuration Manager-konsolen och de språk paket som stöds för platsen till `\Tools\ConsoleSetup` undermappen i Configuration Manager installations Sök väg på plats servern.

- När du startar installationen av Configuration Manager-konsolen från den här mappen på plats servern kopieras Configuration Manager-konsolen och språk pakets filerna som stöds till datorn.

- När ett språk paket är tillgängligt för den aktuella språk inställningen på datorn öppnas Configuration Manager-konsolen på det språket.

- Om det associerade språk paketet inte är tillgängligt för Configuration Manager-konsolen öppnas konsolen på engelska (USA).

Du kan till exempel installera Configuration Manager-konsolen från en plats server som stöder engelska, tyska och franska. Om du öppnar Configuration Manager-konsolen på en dator med en konfigurerad språk inställning på franska, öppnas konsolen på franska. Om du öppnar Configuration Manager-konsolen på en dator med ett konfigurerat språk som är japanska, öppnas konsolen på engelska eftersom det japanska språk paketet inte är tillgängligt.  

Varje gången som Configuration Manager-konsolen öppnas:

- Tt fastställer de konfigurerade språk inställningarna för datorn
- Verifierar om ett associerat språk paket är tillgängligt för Configuration Manager-konsolen
- Öppnar-konsolen med hjälp av lämpligt språk paket

När du vill öppna Configuration Manager-konsolen på engelska oberoende av de konfigurerade språk inställningarna på datorn tar du bort eller byter namn på språkpack-filerna på datorn.

Använd följande procedurer för att starta Configuration Manager-konsolen på engelska oberoende av de konfigurerade nationella inställningarna på datorn.  

#### <a name="install-an-english-only-version-of-the-configuration-manager-console-on-computers"></a>Installera en version av Configuration Manager-konsolen på engelska på datorer  

1. I Utforskaren bläddrar du till `\Tools\ConsoleSetup\LanguagePack` i Configuration Manager installations Sök väg.

1. Byt namn på **.msp**- och **.mst**-filerna. Du kan till exempel ändra ** &lt;fil namn\>. MSP** till ** &lt;fil namn\>. MSP. disabled**.

1. Installera Configuration Manager-konsolen på datorn.

    > [!IMPORTANT]
    > När nya server språk konfigureras för plats servern kopieras. msp-och. mst-filerna till mappen **LanguagePack** och du måste upprepa den här proceduren för att installera nya Configuration Manager-konsoler endast på engelska.  

#### <a name="temporarily-disable-a-console-language-on-an-existing-configuration-manager-console-installation"></a>Inaktivera tillfälligt ett konsol språk för en befintlig Configuration Manager-konsol installation

1. Stäng Configuration Manager-konsolen på den dator som kör Configuration Manager-konsolen.

1. I Utforskaren bläddrar du till &lt; *ConsoleInstallationPath*> \bin\ på Configuration Manager-konsol datorn.  

1. Byt namn på den lämpliga språkmappen för det språk som har konfigurerats på datorn. Om språkinställningarna för datorn till exempel har angetts för tyska så kan du byta namn på mappen **de** till **de.disabled**.  

1. Om du vill öppna Configuration Manager-konsolen på det språk som har kon figurer ATS för datorn byter du namn på mappen till det ursprungliga namnet. Byt till exempel namnet **de.disabled** till **de**.  

## <a name="configure-dcom-permissions-for-remote-consoles"></a><a name="BKMK_ConfigDCOMforRemoteConsole"></a>Konfigurera DCOM-behörigheter för fjärranslutna konsoler

Det användar konto som kör Configuration Manager-konsolen måste ha behörighet att komma åt plats databasen med hjälp av SMS-providern. En administrativ användare som använder en fjärran sluten Configuration Manager-konsol kräver dock även DCOM-behörigheter för **fjärraktivering** på:

- Platsserverdatorn

- Varje dator som är värd för en instans av SMS-providern

Säkerhets gruppen med namnet **SMS-administratörer** beviljar åtkomst till SMS-providern på en dator och kan även användas för att bevilja nödvändiga DCOM-behörigheter. Den här gruppen är lokal på datorn när SMS-providern körs på en medlems Server. Det är en domän lokal grupp när SMS-providern körs på en domänkontrollant.

> [!IMPORTANT]
> I Configuration Manager-konsolen används WMI för att ansluta till SMS-providern, och WMI använder DCOM internt. Om Configuration Manager-konsolen körs på en annan dator än SMS-providern måste den ha behörighet att aktivera en DCOM-server på SMS-providerns dator. Fjärraktivering beviljas som standard endast till medlemmarna i den inbyggda gruppen Administratörer.
>
> Om du tillåter att SMS Admins-gruppen har behörighet för fjärraktivering kan en medlem i den här gruppen försöka utföra DCOM-angrepp mot SMS-providerns dator. Denna konfiguration ökar även datorns angreppsyta. Minska hotet genom att vara noga med vilka som är medlemmar av gruppen SMS-administratörer.

Använd följande procedur för att konfigurera varje central administrations webbplats (CAS), primär plats Server och varje dator där SMS-providern är installerad för att ge administrativa användare fjärråtkomst till Configuration Manager konsolen.

### <a name="configure-dcom-permissions-for-remote-configuration-manager-console-connections"></a>Konfigurera DCOM-behörigheter för fjärranslutna Configuration Manager konsol anslutningar

1. Som administratör på mål datorn kör `Dcomcnfg.exe` du för att öppna **komponent tjänster**.

1. Expandera **komponent tjänster**, expandera **datorer**och välj sedan **den här datorn**. Välj **Egenskaper**på menyn **åtgärd** .

1. I fönstret **Egenskaper för min dator** växlar du till fliken **com-säkerhet** . I avsnittet **Start-och aktiverings behörigheter** väljer du **Redigera gränser**.

1. I fönstret **Start-och aktiverings behörigheter** väljer du **Lägg till**.

1. I fönstret **Välj användare, datorer, tjänst konton eller grupper** , i fältet **Ange de objekt namn som ska väljas** , skriver `SMS Admins`du och väljer sedan **OK**.

   > [!TIP]
   > För att hitta gruppen SMS-administratörer kan du behöva ändra inställningen: **från den här platsen**. Den här gruppen är lokal på datorn när SMS-providern körs på en medlems Server och är en domän lokal grupp när SMS-providern körs på en domänkontrollant.

1. I avsnittet **behörigheter för SMS-administratörer** för att tillåta fjärraktivering väljer du kolumnen **Tillåt** för **fjärraktivering** .

1. Välj **OK** för att spara ändringarna och Stäng alla fönster.

Datorn har nu kon figurer ATS för att tillåta fjärråtkomst till Configuration Manager konsolen till medlemmar i gruppen SMS-administratörer.

Upprepa proceduren på varje SMS-provider som stöder fjärrConfiguration Manager-konsoler.

## <a name="modify-the-site-database-configuration"></a><a name="bkmk_dbconfig"></a>Ändra plats databasens konfiguration

När du har installerat en-plats kan du ändra konfigurationen för plats databasen och plats databas servern. Kör Configuration Manager-installationen på en CAS-server eller primär plats Server för att göra ändringar. Du kan flytta platsdatabasen till en ny instans av SQL Server på samma dator, eller till en annan dator som kör en version av SQL Server som stöds. Dessa ändringar stöds inte för databas konfigurationen på sekundära platser.

Mer information om gränserna för support finns i [Supportpolicy för manuella databasändringar i en Configuration Manager-miljö](https://support.microsoft.com/kb/3106512).  

> [!NOTE]
> När du ändrar databas konfigurationen för en plats Configuration Manager startar om eller installerar om Configuration Manager tjänster på plats servern och fjärrplatsens system servrar som kommunicerar med databasen.

### <a name="modify-the-database-configuration"></a>Ändra databas konfigurationen

Kör Configuration Manager-installationen på plats servern och välj alternativet **utför plats underhåll eller Återställ den här platsen**. Välj sedan alternativet **ändra SQL Server konfiguration** . Du kan ändra följande platsdatabaskonfigurationer:

- Den Windows-baserade server som är värd för-databasen.

- Den instans av SQL Server som används på en server som är värd för SQL Server-databasen.

- Databasnamnet.

- SQL Server porten som används av Configuration Manager.

- SQL Server Service Broker porten som används av Configuration Manager.

### <a name="move-the-site-database"></a>Flytta plats databasen

Om du flyttar plats databasen granskar du även följande konfigurationer:

- När du flyttar plats databasen till en ny dator lägger du till dator kontot för plats servern i den lokala gruppen **Administratörer** på den dator som kör SQL Server. Om du använder ett SQL Server-kluster för plats databasen lägger du till dator kontot i gruppen lokala **Administratörer** på varje Windows Server-klusternod.

- När du flyttar databasen till en ny instans på SQL Server, eller till en ny SQL Server dator, aktiverar du integrering med Common Language Runtime (CLR). Använd **SQL Server Management Studio** för att ansluta till den instans av SQL Server som är värd för plats databasen. Kör sedan följande lagrade procedur som en fråga:`sp_configure 'clr enabled',1; reconfigure`

- Kontrol lera att den nya SQL Server har åtkomst till säkerhets kopierings platsen. När du använder en UNC för att lagra säkerhets kopian av plats databasen efter att ha flyttat databasen till en ny server, kontrollerar du att dator kontot för den nya SQL Server har **Skriv** behörighet till UNC-platsen. Den här konfigurationen omfattar när du flyttar till en SQL Server AlwaysOn-tillgänglighetsgruppen eller ett SQL Server-kluster.

> [!IMPORTANT]
> Innan du flyttar en databas som har en eller flera databas repliker för hanterings platser måste du först ta bort databas replikerna. När du har slutfört flyttningen av databasen kan du konfigurera om databasreplikerna. Mer information finns i [databas repliker för hanterings platser](../deploy/configure/database-replicas-for-management-points.md).

## <a name="manage-the-spn-for-the-site-database-server"></a><a name="bkmk_SPN"></a>Hantera SPN för plats databas servern

Du kan välja det konto som kör SQL-tjänster för plats databasen:

- När tjänsterna körs med datorns system konto registreras automatiskt tjänstens huvud namn (SPN).

- När tjänsterna körs med ett lokalt domän användar konto registrerar du SPN manuellt. SPN gör det möjligt för SQL-klienter och andra plats system att autentisera med Kerberos. Utan Kerberos-autentisering kan kommunikationen med databasen misslyckas.

Mer information om SPN-namn och Kerberos-anslutningar finns i [Registrera ett tjänst huvud namn för Kerberos-anslutningar](https://docs.microsoft.com/sql/database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections).

Registrera ett SPN för SQL Server tjänst kontot för plats databas servern med hjälp av verktyget **setspn** . Kör Setspn som domän administratör på en dator i samma domän som SQL Server.

Följande procedurer är exempel på hur du hanterar SPN för SQL Server tjänst konto. Mer information om Setspn finns i [Översikt över Setspn](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc731241\(v=ws.11\)).

### <a name="manually-create-a-domain-user-spn-for-the-sql-server-service-account"></a>Skapa ett SPN för domän användare för SQL Server tjänst kontot manuellt

1. Öppna en kommandotolk som administratör.

1. Ange ett giltigt kommando för att skapa tjänst huvud namnet för både NetBIOS-namnet och FQDN:

    > [!IMPORTANT]
    > När du skapar ett SPN för en klustrad SQL Server anger du det virtuella namnet på SQL Server klustret som SQL Server dator namn.

    - NetBIOS-namn:`setspn -A MSSQLSvc/<SQL Server computer name>:<port> <Domain\Account>`

        Exempelvis: `setspn -A MSSQLSvc/sqlserver:1433 contoso\sqlservice`

    - KVALIFICERADE`setspn -A MSSQLSvc/<SQL Server FQDN>:<port> <Domain\Account>`

        Exempelvis: `setspn -A MSSQLSvc/sqlserver.contoso.com:1433 contoso\sqlservice`

    > [!NOTE]
    > Kommandot för att registrera ett SPN för en SQL Server namngiven instans är detsamma som du använder när du registrerar ett SPN för en standard instans. Det enda undantaget är att port numret måste matcha porten som den namngivna instansen använder.

### <a name="verify-the-domain-user-spn-is-registered-correctly"></a>Verifiera att domän användarens SPN är korrekt registrerat

1. Öppna en kommandotolk som administratör.

1. Ange följande kommando:`setspn -L <domain\SQL service account>`

    Exempelvis: `setspn -L contoso\sqlservice`

1. Granska registrerade **servicePrincipalName**. Se till att du har skapat ett giltigt SPN för SQL Server.

### <a name="change-the-sql-server-service-account-from-local-system-to-a-domain-user-account"></a>Ändra SQL Server tjänst kontot från det lokala systemet till ett domän användar konto

1. Skapa eller välj en domän eller ett lokalt systemanvändarkonto som du vill använda som SQL Server-tjänstkonto.

1. Öppna **SQL Server Configuration Manager**.

1. Välj **SQL Server tjänster**och öppna **SQL Server&lt;\>instans namnet**.

1. Växla till fliken **Logga in** . Välj **det här kontot**och ange sedan användar namn och lösen ord för domän användar kontot från steg 1.

1. Bekräfta ändringen av tjänst kontot och starta om SQL Server tjänsten.

## <a name="run-a-site-reset"></a><a name="bkmk_reset"></a>Kör en plats återställning

När en plats återställning körs på en certifikat utfärdare eller primär plats, platsen:

- Tillämpar standard Configuration Manager fil-och Register behörigheter igen

- Installerar om alla plats komponenter och alla plats system roller

Sekundära platser har inte stöd för plats återställning.

Du kan manuellt återställa en plats. De kan också köras automatiskt när du har ändrat plats konfigurationen. Ett exempel:

- Om kontona som används av Configuration Manager-komponenter har ändrats bör du överväga en manuell plats återställning. Den här åtgärden kontrollerar att plats komponenterna uppdateras för att använda den nya konto informationen.

- Om du ändrar klient-eller Server språken på en plats kör Configuration Manager automatiskt en plats återställning. Webbplatsen måste återställas för att använda de nya språken.

> [!NOTE]
> En plats återställning återställer inte åtkomst behörighet till icke-Configuration Manager objekt.

### <a name="what-happens-during-a-site-reset"></a>Vad händer under en plats återställning

När en platsåterställning körs:

1. Installations programmet stoppar och startar om **SMS_SITE_COMPONENT_MANAGER** tjänsten och tråd komponenterna i **SMS_EXECUTIVEs** tjänsten.

1. Installations programmet tar bort och återskapar plats systemets delade mapp och **SMS Executive** -komponenten på den lokala datorn och på fjärrplatsens system datorer.

1. Installations programmet startar om tjänsten **SMS_SITE_COMPONENT_MANAGER** , som installerar **SMS_EXECUTIVE** och **SMS_SQL_MONITOR** tjänsterna.

Plats återställning återställer följande objekt:

- Registernycklarna **SMS** eller **NAL** samt eventuella standardundernycklar under de här nycklarna.

- Configuration Manager fil katalog träd och alla standardfiler eller under kataloger i det här fil katalog trädet.

### <a name="prerequisites-for-site-reset"></a>Krav för plats återställning

Det konto som du använder för att återställa en plats måste ha följande behörigheter:

- Så här återställer du CAS:

  - En lokal **administratör** på CAS-servern

  - Behörigheter som motsvarar den rollbaserade administrations säkerhets rollen **Fullständig administratör**

- Återställa en primär plats:

  - En lokal **administratör** på den primära plats servern

  - Behörigheter som motsvarar den rollbaserade administrations säkerhets rollen **Fullständig administratör**
  
  - Om den primära platsen finns i en hierarki med en certifikat utfärdare måste det här kontot även vara lokal **administratör** på CAS-servern.

### <a name="limitations-for-a-site-reset"></a>Begränsningar för en plats återställning

Om hierarkin är konfigurerad för att stödja [test av klient uppgraderingar i en för produktions samling](../../clients/manage/upgrade/test-client-upgrades.md)kan du inte använda en plats återställning för att ändra server-eller klient språk paket på platser.

### <a name="run-a-site-reset"></a>Kör en platsåterställning

1. Starta Configuration Manager-installationen på plats servern genom att använda någon av följande metoder:

    - På **Start** -menyn väljer du **Configuration Manager installationen**.

    - I katalogen för *installations mediet*för Configuration Manager öppnar `\SMSSETUP\BIN\X64\setup.exe`du. Kontrol lera att den här versionen är samma som plats versionen.

    - I katalogen där Configuration Manager har *installerats*öppnar `\BIN\X64\setup.exe`du.

1. På sidan **komma igång** väljer du **utför plats underhåll eller Återställ den här platsen**.

1. På sidan **plats underhåll** väljer du **Återställ plats utan konfigurations ändringar**.

1. Välj **Ja** för att påbörja plats återställningen.

## <a name="manage-language-packs-at-a-site"></a><a name="bkmk_sitelang"></a>Hantera språk paket på en plats

När en plats har installerats kan du ändra server-och klient språk paketen som används.

### <a name="server-language-packs"></a>Server språk paket

*Gäller för: Configuration Manager-konsol installationer, nya installationer av tillämpliga plats system roller*

När du har uppdaterat server språk paketen på en plats kan du lägga till stöd för språk paketen i Configuration Manager-konsoler.

Om du vill lägga till stöd för ett Server språk paket i en Configuration Manager-konsol installerar du Configuration Manager-konsolen från mappen **ConsoleSetup** på en plats server som innehåller det språk paket som du vill använda. Om Configuration Manager-konsolen redan har installerats måste du först avinstallera den för att kunna identifiera den aktuella listan över språk paket som stöds för den nya installationen.

### <a name="client-language-packs"></a>Klient språk paket

Ändringar av klient språk paketen uppdaterar källfilerna för klient installationen. Nya klient installationer och uppgraderingar lägger till stöd för den uppdaterade listan med klient språk.

När du har uppdaterat klient språk paketen på en plats installerar du varje klient som ska använda språk paketen med hjälp av källfiler som innehåller klient språk paketen.

Mer information om de klient-och Server språk som Configuration Manager stöder finns i [språk paket](../deploy/install/language-packs.md).

### <a name="modify-the-supported-language-packs-at-a-site"></a>Ändra de språk paket som stöds på en plats

1. Starta Configuration Manager-installationen på plats servern genom att använda någon av följande metoder:

    - På **Start** -menyn väljer du **Configuration Manager installationen**.

    - I katalogen för *installations mediet*för Configuration Manager öppnar `\SMSSETUP\BIN\X64\setup.exe`du. Kontrol lera att den här versionen är samma som plats versionen.

    - I katalogen där Configuration Manager har *installerats*öppnar `\BIN\X64\setup.exe`du.

1. På sidan **komma igång** väljer du **utför plats underhåll eller Återställ den här platsen**.

1. På sidan **plats underhåll** väljer du **ändra språk konfiguration**.

1. På sidan **nödvändiga hämtningar** väljer du ett av följande alternativ:

    - **Hämta nödvändiga filer**: Hämta uppdateringar till språk paket.

    - **Använd tidigare hämtade filer**: Använd tidigare hämtade filer som innehåller de språk paket som du vill lägga till på platsen.

1. På sidan **Val av Server språk** väljer du de Server språk som stöds av platsen.

1. På sidan **Val av klient språk** väljer du de klient språk som stöds av den här platsen.

1. Slutför guiden för att ändra språk stödet på platsen.

    > [!NOTE]
    > Configuration Manager initierar en plats återställning som också installerar om alla plats system roller på platsen.

## <a name="modify-the-database-server-alert-threshold"></a><a name="BKMK_ModDBAlert"></a>Ändra aviserings tröskeln för databas servern

Som standard genererar Configuration Manager aviseringar när det lediga disk utrymmet på en plats databas server är lågt:

- Generera en varning när det finns 10 GB eller mindre ledigt disk utrymme
- Generera en kritisk avisering när det finns 5 GB eller mindre ledigt disk utrymme

Du kan ändra dessa värden eller inaktivera aviseringar för varje plats:

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**och välj noden **platser** .

1. Välj den plats som du vill konfigurera. I menyfliksområdet väljer du **Egenskaper**.

1. Växla till fliken **avisering** och redigera sedan inställningarna.

## <a name="uninstall-sites-and-hierarchies"></a>Avinstallera platser och hierarkier

Du kan behöva avinstallera en Configuration Manager plats system roll, plats eller hierarki. Mer information finns i [avinstallera roller, platser och hierarkier](../deploy/install/uninstall-sites-and-hierarchies.md).

Från och med version 2002 kan du också ta bort CAS från en hierarki, men behålla den primära platsen. Mer information finns i [ta bort CAS](../deploy/install/remove-central-administration-site.md).
