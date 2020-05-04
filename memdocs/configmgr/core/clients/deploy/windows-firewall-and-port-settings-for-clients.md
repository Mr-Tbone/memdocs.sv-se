---
title: Windows-klientens brand vägg och port inställningar
titleSuffix: Configuration Manager
description: Välj Windows-brandväggen och port inställningar för klienter i Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: dce4b640-c92f-401a-9873-ce9aa9262014
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2290899c0159221c5f45ce6c34332b766984e4c1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713970"
---
# <a name="windows-firewall-and-port-settings-for-clients-in-configuration-manager"></a>Windows-brandväggen och port inställningar för klienter i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Klient datorer i Configuration Manager som kör Windows-brandväggen kräver ofta att du konfigurerar undantag för att tillåta kommunikation med deras plats. De undantag som du måste konfigurera beror på de hanterings funktioner som du använder med Configuration Manager-klienten.  

 Använd följande avsnitt för att identifiera dessa hanteringsfunktioner och för mer information om hur du konfigurerar Windows-brandväggen för de här undantagen.  

##  <a name="modifying-the-ports-and-programs-permitted-by-windows-firewall"></a><a name="BKMK_ModifyingWindowsFirewall"></a> Ändra vilka portar och program som tillåts av Windows-brandväggen  
 Använd följande procedur för att ändra portar och program i Windows-brandväggen för Configuration Manager-klienten.  

#### <a name="to-modify-the-ports-and-programs-permitted-by-windows-firewall"></a>Ändra vilka portar och program som tillåts av Windows-brandväggen  

1.  Öppna Kontrollpanelen på den dator där Windows-brandväggen körs.  

2.  Högerklicka på **Windows-brandväggen**och klicka sedan på **Öppna**.  

3.  Konfigurera eventuella undantag som krävs och eventuella anpassade program och portar som du vill ha.  

## <a name="programs-and-ports-that-configuration-manager-requires"></a>Program och portar som krävs för Configuration Manager  
 Följande Configuration Manager funktioner kräver undantag i Windows-brand väggen:  

### <a name="queries"></a>Frågor  
 Om du kör Configuration Manager-konsolen på en dator som kör Windows-brandväggen går det inte att köra frågor första gången de körs och operativ systemet visar en dialog ruta där du tillfrågas om du vill avblockera statview. exe. Om du avblockerar statview.exe körs efterföljande frågor utan problem. Du kan även manuellt lägga till Statview.exe i listan med program och tjänster på fliken **Undantag** i Windows-brandväggen innan du kör en fråga.  

### <a name="client-push-installation"></a>Push-installation av klient  
 Om du vill använda push-installation för att installera Configuration Manager-klienten lägger du till följande som undantag till Windows-brand väggen:  

-   Utgående och inkommande: **Fil- och skrivardelning**  

-   Inkommande: **WMI (Windows Management Instrumentation)**  

### <a name="client-installation-by-using-group-policy"></a>Klientinstallation med grupprincip  
 Om du vill använda grupprincip för att installera Configuration Manager-klienten lägger du till **fil-och skrivar delning** som ett undantag i Windows-brandväggen.  

### <a name="client-requests"></a>Klientbegäranden  
 För att klient datorer ska kunna kommunicera med Configuration Manager-plats system lägger du till följande som undantag till Windows-brand väggen:  

 Utgående: TCP-port **80** (för HTTP-kommunikation)  

 Utgående: TCP-port **443** (för HTTPS-kommunikation)  

> [!IMPORTANT]  
>  Detta är standard port nummer som kan ändras i Configuration Manager. Mer information finns i så här [konfigurerar du klient kommunikations portar](../../../core/clients/deploy/configure-client-communication-ports.md). Om de här portarna har ändrats från standardvärdena måste du även konfigurera matchande undantag i Windows-brandväggen.  

### <a name="client-notification"></a>Klientmeddelande  
 För att hanterings platsen ska meddela klient datorer om en åtgärd som måste vidtas när en administrativ användare väljer en klient åtgärd i Configuration Manager-konsolen, till exempel Ladda ned dator princip eller initiera en genomsökning av skadlig kod, lägger du till följande som ett undantag till Windows-brand väggen:  

 Utgående: TCP-port **10123**  

 Om den här kommunikationen Miss lyckas återgår Configuration Manager automatiskt till att använda den befintliga kommunikations porten för klient-till-hantering-platsen för HTTP eller HTTPS:  

 Utgående: TCP-port **80** (för HTTP-kommunikation)  

 Utgående: TCP-port **443** (för HTTPS-kommunikation)  

> [!IMPORTANT]  
>  Detta är standard port nummer som kan ändras i Configuration Manager. Mer information finns i [så här konfigurerar du klient kommunikations portar](../../../core/clients/deploy/configure-client-communication-ports.md). Om de här portarna har ändrats från standardvärdena måste du även konfigurera matchande undantag i Windows-brandväggen.  

### <a name="remote-control"></a>Fjärrstyrning  
 Om du vill använda Configuration Manager fjärr styrning kan du tillåta följande port:  

-   Inkommande: TCP-port **2701**  

### <a name="remote-assistance-and-remote-desktop"></a>Fjärrhjälp och fjärrskrivbord  
 Om du vill starta Fjärrhjälp från Configuration Manager-konsolen lägger du till det anpassade programmet **Helpsvc. exe** och den inkommande anpassade porten TCP **135** i listan över tillåtna program och tjänster i Windows-brandväggen på klient datorn. Du måste även tillåta **Fjärrhjälp** och **Fjärrskrivbord**. Om du startar Fjärrhjälp från klientdatorn konfigurerar och Windows-brandväggen automatiskt **Fjärrhjälp** och **Fjärrskrivbord**.  

### <a name="wake-up-proxy"></a>Aktiveringsproxy  
 Om du aktiverar klientinställningen för aktiveringsproxy använder den nya tjänsten ConfigMgr-aktiveringsproxy ett peer-to-peer-protokoll för att kontrollera om andra datorer är aktiva på undernätet och aktivera dem vid behov. Den här kommunikationen använder följande portar:  

 Utgående: UDP-port **25536**  

 Utgående: UDP-port **9**  

 Detta är standard port nummer som kan ändras i Configuration Manager med hjälp av inställningarna för **energispar funktioner** för **Wake-up proxy Port Number (udp)** och **Wake on LAN port nummer (UDP)**. Om du anger klientinställningen **Energisparfunktioner**: **Undantag för aktiveringsproxy i Windows-brandväggen** konfigureras dessa portar automatiskt i Windows-brandväggen för klienter. Om en annan brandvägg körs på klienten måste du dock konfigurera undantagen för dessa portnummer manuellt.  

 Förutom dessa portar använder aktiveringsproxyn även ICMP (Internet Control Message Protocol) meddelanden om ekobegäranden från en klientdator till en annan. Den här kommunikationen används för att bekräfta huruvida den andra klientdatorn är aktiv i nätverket. ICMP kallas ibland TCP/IP-pingkommandon.  

 Mer information om Wake-up proxy finns i [Planera aktivering av klienter](../../../core/clients/deploy/plan/plan-wake-up-clients.md).  

### <a name="windows-event-viewer-windows-performance-monitor-and-windows-diagnostics"></a>Windows Loggboken, Windows Prestandaövervakaren samt Windows Diagnostik  
 Om du vill komma åt Windows Loggboken, Windows prestanda övervakaren och Windows-diagnostik från Configuration Manager-konsolen aktiverar du **fil-och skrivar delning** som ett undantag i Windows-brandväggen.  

## <a name="ports-used-during-configuration-manager-client-deployment"></a>Portar som används vid klientdistribution med Configuration Manager  
 Följande tabeller visar vilka portar som används under klientinstallationen.  

> [!IMPORTANT]  
>  Om det finns en brandvägg mellan platsens systemservrar och klientdatorn måste du bekräfta att brandväggen tillåter trafik för de portar som krävs för den klientinstallationsmetod du valt. Brandväggar förhindrar t.ex. ofta push-installation av klienter eftersom de blockerar SMB (Server Message Block) och RPC (Remote Procedure Calls). I en sådan situation använder du en annan metod för klientinstallation, t.ex. manuell installation (kör CCMSetup.exe) eller klientinstallation baserad på grupprincip. Dessa metoder för klientinstallation kräver inte SMB eller RPC.  

 Information om hur du konfigurerar Windows-brandväggen på klientdatorn finns i [Ändra vilka portar och program som tillåts av Windows-brandväggen](#BKMK_ModifyingWindowsFirewall).  

### <a name="ports-that-are-used-for-all-installation-methods"></a>Portar som används för alla installationsmetoder  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP (Hypertext Transfer Protocol) från klientdatorn till en återställningsstatusplats, om en återställningsstatusplats tilldelats klienten.|--|80 (Se anteckning 1, **Alternativ port tillgänglig**)|  

### <a name="ports-that-are-used-with-client-push-installation"></a>Portar som används med push-installation av klienter  
 Förutom de portar som visas i följande tabell använder push-installation av klienter även ICMP-ekobegäransmeddelanden (Internet Control Message Protocol) från platsservern till klientdatorn för att bekräfta att klientdatorn är tillgänglig i nätverket. ICMP kallas ibland TCP/IP-pingkommandon. ICMP har inte ett UDP- eller TCP-protokollnummer, och finns därför inte i följande tabell. Dock måste alla mellanliggande nätverksenheter, t.ex. brandväggar, tillåta ICMP-trafik för att push-installation av klienter ska kunna genomföras.  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block) mellan platsservern och klientdatorn.|--|445|  
|RPC-slutpunktsavbildare mellan platsservern och klientdatorn.|135|135|  
|Dynamiska RPC-portar mellan platsservern och klientdatorn.|--|DYNAMIC|  
|HTTP (Hypertext Transfer Protocol) från klientdatorn till en hanteringsplats när anslutningen är över HTTP.|--|80 (Se anteckning 1, **Alternativ port tillgänglig**)|  
|HTTPS (säkert Hypertext Transfer Protocol) från klientdatorn till en hanteringsplats när anslutningen är över HTTPS.|--|443 (se anmärkning 1, **Alternativ port tillgänglig**)|  

### <a name="ports-that-are-used-with-software-update-point-based-installation"></a>Portar som används med installation baserad på programuppdateringsplats  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP (Hypertext Transfer Protocol) från klientdatorn till programuppdateringsplatsen.|--|80 eller 8530 (Se anteckning 2, **Windows Server Update Services**)|  
|HTTPS (säkert Hypertext Transfer Protocol) från klientdatorn till programuppdateringsplatsen.|--|443 eller 8531 (se anmärkning 2, **Windows Server Update Services**)|  
|SMB (Server Message Block) mellan käll servern och klient datorn när du anger kommando rads egenskapen **/Source:&lt;Path\>** för CCMSetup.|--|445|  

### <a name="ports-that-are-used-with-group-policy-based-installation"></a>Portar som används med installation baserad på grupprincip  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP (Hypertext Transfer Protocol) från klientdatorn till en hanteringsplats när anslutningen är över HTTP.|--|80 (Se anteckning 1, **Alternativ port tillgänglig**)|  
|HTTPS (säkert Hypertext Transfer Protocol) från klientdatorn till en hanteringsplats när anslutningen är över HTTPS.|--|443 (se anmärkning 1, **Alternativ port tillgänglig**)|  
|SMB (Server Message Block) mellan käll servern och klient datorn när du anger kommando rads egenskapen **/Source:&lt;Path\>** för CCMSetup.|--|445|  

### <a name="ports-that-are-used-with-manual-installation-and-logon-script-based-installation"></a>Portar som används med manuell installation och installation baserad på inloggningsskript  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block) mellan klientdatorn och en nätverksresurs från vilken du kör CCMSetup.exe.<br /><br /> När du installerar Configuration Manager kopieras källfilerna för klient installationen och delas automatiskt från mappen * &lt;InstallationPath\>* \Client på hanterings platser. Du kan dock kopiera dessa filer och skapa en ny resurs på valfri dator i nätverket. Du kan även eliminera denna nätverkstrafik genom att köra CCMSetup.exe lokalt, t.ex. genom att använda media som går att ta bort.|--|445|  
|Hypertext Transfer Protocol (HTTP) från klient datorn till en hanterings plats när anslutningen är över HTTP och du inte anger kommando rads egenskapen/source för CCMSetup **:&lt;Path\>**.|--|80 (Se anteckning 1, **Alternativ port tillgänglig**)|  
|Skydda Hypertext Transfer Protocol (HTTPS) från klient datorn till en hanterings plats när anslutningen är över HTTPS och du inte anger kommando rads egenskapen/source för CCMSetup **:&lt;Path\>**.|--|443 (se anmärkning 1, **Alternativ port tillgänglig**)|  
|SMB (Server Message Block) mellan käll servern och klient datorn när du anger kommando rads egenskapen **/Source:&lt;Path\>** för CCMSetup.|--|445|  

### <a name="ports-that-are-used-with-software-distribution-based-installation"></a>Portar som används med installation baserad på programdistribution  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block) mellan distributionsplatsen och klientdatorn.|--|445|  
|HTTP (Hypertext Transfer Protocol) från klienten till en distributionsplats när anslutningen är över HTTP.|--|80 (Se anteckning 1, **Alternativ port tillgänglig**)|  
|HTTPS (säkert Hypertext Transfer Protocol) från klienten till en distributionsplats när anslutningen är över HTTPS.|--|443 (se anmärkning 1, **Alternativ port tillgänglig**)|  

## <a name="notes"></a>Obs!  
 **1 alternativ port tillgänglig** I Configuration Manager kan du definiera en alternativ port för det här värdet. Om en anpassad port har definierats ersätter du den anpassade porten när du definierar IP-filterinformation för IPsec-principer eller för att konfigurera brandväggar.  

 **2 Windows Server Update Services** Du kan installera Windows Server Update Service (WSUS) antingen på standardwebbplatsen (port 80) eller en anpassad webbplats (port 8530).  

 Efter installationen kan du byta port. Du behöver inte använda samma portnummer i hela platshierarkin.  

 Om HTTP-porten är 80 måste HTTPS-porten vara 443.  

 Om HTTP-porten är något annat måste HTTPS-porten vara 1 högre. Till exempel 8530 och 8531.
