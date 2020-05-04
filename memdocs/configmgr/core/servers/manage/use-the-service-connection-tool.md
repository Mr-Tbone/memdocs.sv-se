---
title: Tjänst anslutnings verktyg
titleSuffix: Configuration Manager
description: Lär dig mer om det här verktyget som gör att du kan ansluta till Configuration Manager moln tjänsten för manuell uppladdning av användnings information.
ms.date: 09/06/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6e4964c5-43cb-4372-9a89-b62ae6a4775c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e535653e0f31e186a6bdbde8da77750f2afdfdb0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710820"
---
# <a name="use-the-service-connection-tool-for-configuration-manager"></a>Använd tjänst anslutnings verktyget för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Använd **tjänst anslutnings verktyget** när tjänst anslutnings punkten är i offlineläge eller när Configuration Manager plats system servrar inte är anslutna till Internet. Verktyget kan hjälpa dig att hålla din webbplats uppdaterad med de senaste uppdateringarna för Configuration Manager.  

När det körs ansluter verktyget manuellt till Configuration Manager moln tjänsten för att ladda upp användnings information för din hierarki och för att hämta uppdateringar. Överföring av användningsdata krävs för att göra det möjligt för molntjänsten att tillhandahålla rätt uppdateringar för distributionen.  

## <a name="prerequisites-for-using-the-service-connection-tool"></a>Krav för att använda tjänst anslutnings verktyget
Följande är förutsättningar och kända problem.

**Krav**

- Du har en tjänstanslutningspunkt installerad och den är inställd på **Offline, anslutning på begäran**.  

- Verktyget måste köras från en kommandotolk.  

- Varje dator där verktyget körs (tjänstanslutningspunktens dator och datorn som är ansluten till Internet) måste vara ett x64-bitarssystem och ha följande installerat:  

  - Filer för både **Visual C++ Redistributable** x86 och x64.   Som standard installerar Configuration Manager x64-versionen på datorn som är värd för tjänst anslutnings punkten.  

    Du kan hämta en kopia av Visual C++-filerna genom att gå till [Visual C++ Redistributable-paket för Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=40784) i Microsoft Download Center.  

  - .NET Framework 4.5.2 eller senare.  

- Kontot du använder för att köra verktyget måste ha:
  - **Lokal administratörs** behörighet på datorn som är värd för tjänstanslutningspunkten (där verktyget körs).
  - **Läs** -behörighet till platsdatabasen.  



- Du behöver en USB-enhet med tillräckligt mycket ledigt utrymme för att spara filer och uppdateringar eller någon annan metod för att överföra filer mellan tjänstanslutningspunktens dator och den dator som har åtkomst till Internet. (Det här scenariot förutsätter att platsen och de hanterade datorerna inte har en direktanslutning till Internet.)  



## <a name="use-the-service-connection-tool"></a>Använd tjänstanslutningsverktyget  

 Du hittar tjänst anslutnings verktyget (**serviceconnectiontool. exe**) i mappen Configuration Manager installations medium i **%Path%\smssetup\tools\ServiceConnectionTool** -mappen. Använd alltid tjänst anslutnings verktyget som matchar den version av Configuration Manager som du använder.


 I den här processen använder kommandoradsexemplen följande filnamn och platser för mappar (du behöver inte använda dessa sökvägar och filnamn utan kan använda alternativ som passar din miljö och dina önskemål):  

- Sökvägen till ett USB-minne där data har lagrats för överföring mellan servrar: **D:\USB\\**  

- Namnet på CAB-filen med data som har exporterats från platsen: **UsageData.cab**  

- Namnet på den tomma mapp där hämtade uppdateringar för Configuration Manager sparas för överföring mellan servrar: **UpdatePacks**  

På datorn som är värd för tjänstanslutningspunkten:  

- Öppna en kommandotolk med administrativ behörighet och ändra sedan katalogerna till den plats som innehåller **serviceconnectiontool.exe**.  

  Som standard hittar du verktyget i installations mediet för Configuration Manager i **%Path%\smssetup\tools\ServiceConnectionTool** -mappen. Alla filer i den här mappen måste finnas i samma mapp för att tjänstanslutningsverktyget ska fungera.  

När du kör följande kommando förbereds en CAB-fil som innehåller information om användningen och informationen kopieras sedan till en plats du anger. Data i CAB-filen baseras på nivån för diagnostikanvändningsdata som webbplatsen är konfigurerad för att samla in. (se [diagnostik-och användnings data för Configuration Manager](../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)).  Kör följande kommando för att skapa CAB-filen:  

- **serviceconnectiontool.exe -prepare -usagedatadest D:\USB\UsageData.cab**  

Du måste också kopiera mappen ServiceConnectionTool med dess innehåll till USB-enheten eller på annat sätt göra den tillgänglig på datorn som du ska använda i steg 3 och 4.  

### <a name="overview"></a>Översikt
#### <a name="there-are-three-primary-steps-to-using-the-service-connection-tool"></a>Det finns tre huvudsakliga steg för att använda tjänst anslutnings verktyget  

1.  **Förbered**: det här steget körs på den dator som är värd för tjänst anslutnings punkten. När verktyget körs placeras användnings data i en CAB-fil och lagras på en USB-enhet (eller en alternativ överförings plats som du anger).  

2.  **Anslut**: i det här steget kör du verktyget på en fjärrdator som ansluter till Internet så att du kan ladda upp dina användnings data och sedan hämta uppdateringar.  

3.  **Importera**: det här steget körs på den dator som är värd för tjänst anslutnings punkten. När det körs importerar verktyget de uppdateringar som du laddade ned och lägger till dem på platsen så att du kan visa och installera uppdateringarna från Configuration Manager-konsolen.  

När du ansluter till Microsoft från och med version 1606, kan du överföra flera CAB-filer på en gång (alla från en annan hierarki), samt ange en proxyserver och en användare för proxyservern.   

#### <a name="to-upload-multiple-cab-files"></a>Ladda upp flera CAB-filer
- Placera varje CAB-fil som du har exporterat från olika hierarkier i samma mapp. Namnet på varje fil måste vara unikt och du kan manuellt byta namn på dem vid behov.
- När du sedan kör kommandot för att överföra data till Microsoft anger du den mapp som innehåller CAB-filerna. (Före uppdateringen 1606 kunde du bara överför data från en hierarki åt gången och i verktyget var du tvungen att ange namnet på CAB-filen i mappen.)
- Senare, när du importerar i tjänstanslutningspunkten i en hierarki, importerar verktyget automatiskt endast data för den hierarkin.  

#### <a name="to-specify-a-proxy-server"></a>Ange en proxyserver
Du kan använda följande valfria parametrar för att ange en proxyserver (Mer information om hur du använder dessa parametrar finns i avsnittet med kommandoradsparametrar):
- **-proxyserveruri [FQDN_of_proxy_server]**  Använd den här parametern för att ange den proxyserver som ska användas för den här anslutningen.
- **-proxyusername [användarnamn]**  Använd den här parametern om du måste ange en användare för proxyservern.

#### <a name="specify-the-type-of-updates-to-download"></a>Ange vilken typ av uppdateringar som ska hämtas
Från och med version 1706 har verktygens standard hämtnings beteende ändrats och verktyget stöder alternativ för att styra vilka filer som du hämtar.
- Som standard hämtar verktyget bara den senaste tillgängliga uppdateringen som gäller för din webbplats version. Snabb korrigeringar laddas inte ned.

Ändra det här beteendet genom att använda någon av följande parametrar för att ändra vilka filer som ska laddas ned. 

> [!NOTE]
> Din webbplats version bestäms av data i CAB-filen som laddas upp när verktyget körs.
>
> Du kan kontrol lera versionen genom att leta efter filen *SiteVersion*. txt i CAB-filen.

- **– DownloadAll**  Med det här alternativet hämtas allt, inklusive uppdateringar och snabb korrigeringar, oavsett vilken version av webbplatsen som används.
- **– downloadhotfix**  Med det här alternativet hämtas alla snabb korrigeringar oavsett vilken version av webbplatsen du har.
- **– downloadsiteversion**  Med det här alternativet hämtas uppdateringar och snabb korrigeringar som har en version som är högre än din webbplats version.

Exempel kommando rad som använder *-downloadsiteversion*:
- **serviceconnectiontool. exe-Connect *-downloadsiteversion* -usagedatasrc D:\USB-updatepackdest D:\USB\UpdatePacks**




### <a name="to-use-the-service-connection-tool"></a>Använda tjänsteanslutningsverktyget  

1. På datorn som är värd för tjänstanslutningspunkten:  

   - Öppna en kommandotolk med administrativ behörighet och ändra sedan katalogerna till den plats som innehåller **serviceconnectiontool.exe**.   

2. När du kör följande kommando förbereder verktyget en CAB-fil som innehåller information om användningen och kopierar den sedan till en plats du anger:  

   - **serviceconnectiontool.exe -prepare -usagedatadest D:\USB\UsageData.cab**  

   Om du kommer att överföra CAB-filer från mer än en hierarki på samma gång, måste varje CAB-fil i mappen ha ett unikt namn. Du kan manuellt byta namn på filer som du lägger till i mappen.

   Om du vill visa användningsinformation som samlas in och som ska överföras till molntjänsten för Configuration Manager, kör du följande kommando för att exportera samma data som en CSV-fil som du kan visa med hjälp av ett program som t.ex. Excel:  

   - **serviceconnectiontool.exe -export -dest D:\USB\UsageData.csv**  

3. När förberedelsesteget har slutförts flyttar du USB-enheten (eller överför exporterade data med hjälp av någon annan metod) till en dator som har åtkomst till Internet.  

4. På datorn med Internetåtkomst öppnar du en kommandotolk med administrativ behörighet och ändrar sedan sökvägen till den plats som innehåller en kopia av verktyget  **serviceconnectiontool.exe** och de ytterligare filerna från den mappen.  

5. Kör följande kommando för att börja överföra användningsinformation och hämta uppdateringar för Configuration Manager:  

   - **serviceconnectiontool. exe-Connect-usagedatasrc D:\USB-updatepackdest D:\USB\UpdatePacks**

   Fler exempel på kommandoraden finns i [kommandoradsalternativ](../../../core/servers/manage/use-the-service-connection-tool.md#bkmk_cmd) senare i det här avsnittet.

   > [!NOTE]  
   >  När du kör kommandoraden för att ansluta till molntjänsten för Configuration Manager kan det uppstå ett fel som liknar följande:  
   >   
   > - Ohanterat undantag: System.UnauthorizedAccessException:  
   >   
   >      Åtkomst till sökvägen 'C:\  
   >     Users\br\AppData\Local\Temp\extractmanifestcab\95F8A562.sql' nekas.  
   >   
   > Det här felet kan ignoreras och du kan stänga fönstret med felet och fortsätta.  

6. När hämtningen av uppdateringar för Configuration Manager har slutförts flyttar du USB-enheten (eller överför exporterade data på något annat sätt) till den dator som är värd för tjänstanslutningspunkten.  

7. På den dator som är värd för tjänstanslutningspunkten öppnar du en kommandotolk med administrativ behörighet, ändrar sökvägen till den plats som innehåller **serviceconnectiontool.exe**och kör sedan följande kommando:  

   - **serviceconnectiontool.exe -import -updatepacksrc D:\USB\UpdatePacks**  

8. Stäng kommandotolken när importen har slutförts. (Endast uppdateringar för tillämplig hierarki importeras).  

9. Öppna Configuration Manager-konsolen och gå till **Administration** > **uppdateringar och underhåll**. Uppdateringarna som importerades är nu tillgängliga för installation. (Före version 1702 har uppdateringar och underhåll under **administrations** > **Cloud Services**.)

   Information om hur du installerar uppdateringar finns [i installera uppdateringar i konsolen för Configuration Manager](../../../core/servers/manage/install-in-console-updates.md).  

## <a name="log-files"></a><a name="bkmk_cmd"></a>Loggfiler

**ServiceConnectionTool. log**

Varje gången du kör tjänst anslutnings verktyget skapas en loggfil på samma plats som verktyget **ServiceConnectionTool. log**.  Logg filen ger enkel information om körningen av verktyget baserat på vilka kommandon som används.  En befintlig loggfil kommer att ersättas varje gången du kör verktyget.

**ConfigMgrSetup.log**

När du använder verktyget för att ansluta och hämta uppdateringar kommer en loggfil att skapas i roten på system enheten som kallas **ConfigMgrSetup. log**.  I den här logg filen får du mer detaljerad information, till exempel vilka filer som hämtas, extraheras och om hash-kontrollerna lyckas.

## <a name="command-line-options"></a><a name="bkmk_cmd"></a> kommandoradsalternativ  
Om du vill se hjälpinformation för verktyget för tjänsteanslutningspunkten öppnar du kommandotolken till den mapp som innehåller verktyget och kör kommandot:  **serviceconnectiontool.exe**.  


|Kommandoradsalternativ|Information|  
|---------------------------|-------------|  
|**-prepare -usagedatadest [enhet:][sökväg][filnamn.cab]**|Det här kommandot lagrar aktuella användningsdata i en .cab-fil.<br /><br /> Kör det här kommandot som **lokal administratör** på den server som är värd för tjänstanslutningspunkten.<br /><br /> Exempel:   **-prepare -usagedatadest D:\USB\Usagedata.cab**|    
|**-connect -usagedatasrc [enhet:][sökväg] -updatepackdest [enhet:][sökväg] -proxyserveruri [FQDN för proxyserver] -proxyusername [användarnamn]** <br /> <br /> Om du använder en version av Configuration Manager som är tidigare än 1606, måste du ange namnet på CAB-filen och kan inte använda alternativen för en proxyserver.  Kommandoparametrarna som stöds är: <br /> **-connect -usagedatasrc [enhet:][sökväg][filnamn] -updatepackdest [enhet:][sökväg]** |Det här kommandot ansluter till molntjänsten i Configuration Manager och överför användningsdatans CAB-filer från den angivna platsen. Den hämtar även tillgängliga uppdateringspaket och konsolinnehåll. Alternativen för proxyservrar är valfria.<br /><br /> Kör det här kommandot som **lokal administratör** på en dator som kan ansluta till Internet.<br /><br /> Exempel för att ansluta utan en proxyserver: **-connect -usagedatasrc D:\USB\ -updatepackdest D:\USB\UpdatePacks** <br /><br /> Exempel för att ansluta när du använder en proxyserver: **-connect -usagedatasrc D:\USB\Usagedata.cab -updatepackdest D:\USB\UpdatePacks -proxyserveruri itgproxy.redmond.corp.microsoft.com -proxyusername Meg** <br /><br /> Du måste ange ett filnamn för CAB-filen om du använder en tidigare version än 1606, och du kan inte ange någon proxyserver. Använd följande exempel på en kommandorad: **-connect -usagedatasrc D:\USB\Usagedata.cab -updatepackdest D:\USB\UpdatePacks**|      
|**-import -updatepacksrc [enhet:][sökväg]**|Det här kommandot importerar uppdateringspaket och konsolinnehåll som du har hämtat tidigare till Configuration Manager-konsolen.<br /><br /> Kör det här kommandot som **lokal administratör** på den server som är värd för tjänstanslutningspunkten.<br /><br /> Exempel:  **-import -updatepacksrc D:\USB\UpdatePacks**|  
|**-export -dest [enhet:][sökväg][filnamn.csv]**|Det här kommandot exporterar användningsdata till en .csv-fil, som du sedan kan visa.<br /><br /> Kör det här kommandot som **lokal administratör** på den server som är värd för tjänstanslutningspunkten.<br /><br /> Exempel: **-export -dest D:\USB\usagedata.csv**|  
