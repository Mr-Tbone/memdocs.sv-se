---
title: Installera och konfigurera en program uppdaterings plats
titleSuffix: Configuration Manager
description: Primära platser kräver en program uppdaterings plats på den centrala administrations platsen för utvärdering av program uppdateringar och för att distribuera program uppdateringar till klienter.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 03/27/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: b099a645-6434-498f-a408-1d438e394396
ms.openlocfilehash: 0cddb8df51624a562597da17ea310db0a26081f3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715475"
---
# <a name="install-and-configure-a-software-update-point"></a>Installera och konfigurera en program uppdaterings plats  

*Gäller för: Configuration Manager (aktuell gren)*


> [!IMPORTANT]  
>  Innan du installerar program uppdaterings platsens plats system roll (SUP) måste du kontrol lera att servern uppfyller de nödvändiga beroendena och fastställer program uppdaterings platsens infrastruktur på platsen. Mer information om hur du planerar för program uppdateringar och fastställer infrastrukturen för program uppdaterings platsen finns i [planera program uppdateringar](../plan-design/plan-for-software-updates.md).  

 Program uppdaterings platsen krävs på den centrala administrations platsen och på de primära platserna för att aktivera utvärdering av kompatibilitet för program uppdateringar och för att distribuera program uppdateringar till klienter. Programuppdateringsplatsen på sekundära platser är valfri. Platssystemrollen för programuppdateringen måste skapas på en server där WSUS är installerat. Programuppdateringsplatsen samverkar med WSUS-tjänsterna för att konfigurera programuppdateringsinställningarna och för att begära synkronisering av programuppdateringsmetadata. När du har en Configuration Manager-hierarki, installerar och konfigurerar du först program uppdaterings platsen på den centrala administrations platsen, sedan på underordnade primära platser och eventuellt på sekundära platser. Om du har en fristående primär plats och inte en central administrationsplats, installerar och konfigurerar du programuppdateringsplatsen på den primära platsen först och därefter, vid behov, på sekundära platser. Vissa inställningar är bara tillgängliga när du konfigurerar programuppdateringsplatsen på platsen på den översta nivån. Det finns flera olika alternativ som du måste ta ställning till beroende på var du installerade programuppdateringsplatsen.  

> [!IMPORTANT]  
>  Du kan installera fler än en plats för programuppdatering på en plats. Den första programuppdateringsplats du installerar konfigureras som synkroniseringskälla, och synkroniserar uppdateringarna från Microsoft Update eller från den överordnade synkroniseringskällan. De andra programuppdateringsplatserna på platsen konfigureras som repliker av den första programuppdateringsplatsen. Därför är inte alla inställningar tillgängliga när du har installerat och konfigurerat den första programuppdateringsplatsen.  

> [!IMPORTANT]  
>  Det går inte att installera plats system rollen för program uppdaterings platsen på en server som har kon figurer ATS och använts som en fristående WSUS-server eller som använder en program uppdaterings plats för att direkt hantera WSUS-klienter. Befintliga WSUS-servrar stöds bara som överordnade synkroniseringstjänst för den aktiva program uppdaterings platsen. Se [Synkronisera från en överordnad data käll plats](#BKMK_wsussync)

 Du kan lägga till programuppdateringens platssystemroll i en befintlig platssystemserver eller skapa en ny. På sidan **urval för system roll** i guiden **skapa plats system Server** eller **guiden Lägg till plats system roller**, beroende på om du lägger till plats system rollen till en ny eller befintlig plats Server, väljer du **program uppdaterings plats**och konfigurerar sedan inställningarna för program uppdaterings platsen i guiden. Inställningarna varierar beroende på vilken version av Configuration Manager som du använder. Mer information om hur du installerar plats system roller finns i [Installera plats system roller](../../core/servers/deploy/configure/install-site-system-roles.md).  

 I följande avsnitt finns information om inställningarna för en programuppdateringsplats på en plats.  

## <a name="proxy-server-settings"></a>Proxyserverinställningar  
 Du kan konfigurera inställningarna för proxyservern på olika sidor i **guiden skapa plats system Server** eller **guiden Lägg till plats system roller** beroende på vilken version av Configuration Manager som du använder.  

-   Du måste konfigurera proxyservern och sedan ange när den ska användas för programuppdateringar. Konfigurera följande inställningar:  

    -   Ange inställningarna för proxyservern på sidan **Proxy** i guiden eller på fliken **Proxy** i platssystemegenskaperna. Inställningarna för proxyserver är plats system, vilket innebär att alla plats system roller använder de proxyserverinställningar som du anger.  

    -   Ange om proxyservern ska användas när Configuration Manager synkroniserar program uppdateringar och laddar ned innehåll med hjälp av en automatisk distributions regel. Ange inställningarna för programuppdateringsplatsens proxyserver på sidan **Inställningar för proxy och konto** i guiden, eller på fliken **Inställningar för proxy och konto** i egenskaperna för programuppdateringsplatsen.  

        > [!NOTE]  
        >  Inställningen **Använd en proxyserver när du hämtar innehåll genom att använda automatiska distributionsregler** är tillgänglig men används inte för en programuppdateringsplats på en sekundär plats. Det är bara programuppdateringsplatsen på den centrala administrationsplatsen och på den primära platsen som laddar ned innehåll från Microsoft Update-sidan.  

> [!IMPORTANT]  
>  Kontot **Lokalt system** för den server där en regel för automatisk distribution skapades, används som standard för att ansluta till Internet och ladda ned programuppdateringar när reglerna för automatisk distribution körs. Om det här kontot inte har åtkomst till Internet går det inte att ladda ned programuppdateringar och följande post loggas i ruleengine.log: **Det gick inte att hämta uppdateringen från Internet. Fel = 12007**. Konfigurera autentiseringsuppgifterna för att ansluta till proxyservern när kontot Lokalt system inte har Internetåtkomst.  


## <a name="wsus-settings"></a>WSUS-inställningar  
 Du måste konfigurera WSUS-inställningarna på olika sidor i **guiden skapa plats system Server** eller **guiden Lägg till plats system roller** beroende på vilken version av Configuration Manager som du använder, och i vissa fall bara i egenskaperna för program uppdaterings platsen, även kallat egenskaper för plats komponent för program uppdatering. Konfigurera WSUS-inställningarna med hjälp av informationen i följande avsnitt.  

### <a name="wsus-port-settings"></a><a name="BKMK_wsusport"></a>WSUS-portinställningar  
 Du måste konfigurera WSUS-portinställningarna på sidan Programuppdateringsplats i guiden eller i programuppdateringsplatsens egenskaper. Använd följande metod för att kontrollera vilka portinställningar som används av WSUS.  

#### <a name="to-determine-the-port-settings-used-in-iis"></a>Kontrollera vilka portinställningar som används i IIS  

 1.  Öppna IIS-hanteraren på WSUS-servern.  

 2.  Expandera **Webbplatser**och högerklicka på webbplatsen för WSUS-servern. Klicka sedan på **Redigera bindningar**. HTTP- och HTTPS-portarna visas i kolumnen **Port** i dialogrutan Bindningar för webbplats.


### <a name="configure-ssl-communications-to-wsus"></a>Konfigurera SSL-kommunikation till WSUS  
 Du kan konfigurera SSL-kommunikation på sidan **Allmänt** i guiden eller på fliken **Allmänt** i egenskaperna för programuppdateringsplatsen.  

 Mer information om hur du använder SSL finns i [Avgöra om WSUS ska konfigureras för användning av SSL](../plan-design/plan-for-software-updates.md#BKMK_WSUSandSSL).  

### <a name="wsus-server-connection-account"></a>WSUS-serveranslutningskonto  
 Du kan konfigurera ett konto som ska användas av platsservern när den ansluts till WSUS som körs på programuppdateringsplatsen. När du inte konfigurerar det här kontot använder Configuration Manager dator kontot för plats servern för att ansluta till WSUS. Konfigurera inställningarna för WSUS-serveranslutningskontot på sidan **Inställningar för proxy och konto** i guiden eller på fliken **Inställningar för proxy och konto** i egenskaperna för platsen för programuppdatering.  Du kan konfigurera kontot på olika ställen i guiden beroende på vilken version av Configuration Manager du använder.  

 Mer information om Configuration Manager-konton finns i [konton som används](../../core/plan-design/hierarchy/accounts.md).  

## <a name="synchronization-source"></a>Synkroniseringskälla  
 Du kan konfigurera den överordnade synkroniseringstjänsten för synkronisering av program uppdateringar på sidan **synkroniserings källa** i guiden, eller på fliken **synkroniseringsinställningar** i egenskaperna för komponenten för program uppdaterings plats. Alternativen för synkroniseringskälla beror på vilken plats som används.  

 I följande tabell visas tillgängliga alternativ när du konfigurerar programuppdateringsplatsen på en plats.  

|Plats|Tillgängliga alternativ för synkroniseringskälla|  
|----------|----------------------------------------------|  
|– Central administrationsplats<br />– Fristående primär plats|– Synkronisera från Microsoft Update-webbplatsen<br />– Synkronisera från en överordnad datakällplats<br />– Synkronisera inte från Microsoft Update eller en överordnad datakälla|  
|– Ytterligare platser för programuppdatering på en plats<br />– Underordnad primär plats<br />– Sekundär plats|– Synkronisera från en överordnad datakällplats|  

 I följande lista finns mer information om varje alternativ som kan användas som synkroniseringskälla:  

-   **Synkronisera från Microsoft Update**: Använd den här inställningen om du vill synkronisera programuppdateringsmetadata från Microsoft Update. Den centrala administrationsplatsen måste ha Internetåtkomst för att det ska gå att synkronisera. Den här inställningen är bara tillgänglig när du konfigurerar programuppdateringsplatsen på platsen på den översta nivån.  

    > [!NOTE]  
    >  Om det finns en brandvägg mellan platsen för programuppdatering och Internet kan du behöva ställa in brandväggen så att den godkänner de HTTP- och HTTPS-portar som används för WSUS-webbplatsen. Du kan också välja att begränsa åtkomsten på brandväggen till vissa domäner. Mer information om hur du planerar för en brandvägg som har stöd för programuppdateringar finns i [Konfigurera brandväggar](../plan-design/plan-for-software-updates.md#BKMK_ConfigureFirewalls).  

-   **Synkronisera från en överordnad data käll plats: Använd den här inställningen för att synkronisera program uppdateringarnas metadata från den överordnade synkroniseringen. <a name="BKMK_wsussync"> </a>** De underordnade primära och sekundära platserna konfigureras automatiskt för att använda den överordnade platsens webbadress för den här inställningen. Du kan synkronisera programuppdateringar från en befintlig WSUS-server. Ange en URL, till exempel `https://WSUSServer:8531`, där 8531 är den port som används för att ansluta till WSUS-servern.  

-   **Synkronisera inte från Microsoft Update eller en överordnad datakälla**: Använd den här inställningen för att synkronisera programuppdateringar manuellt när programuppdateringsplatsen på platsen på den översta nivån är bortkopplad från Internet. Mer information finns i avsnittet [Synkronisera programuppdateringar från en frånkopplad programuppdateringsplats](synchronize-software-updates-disconnected.md).  

> [!NOTE]  
>  Om det finns en brandvägg mellan platsen för programuppdatering och Internet kan du behöva ställa in brandväggen så att den godkänner de HTTP- och HTTPS-portar som används för WSUS-webbplatsen. Du kan också välja att begränsa åtkomsten på brandväggen till vissa domäner. Mer information om hur du planerar för en brandvägg som har stöd för programuppdateringar finns i [Konfigurera brandväggar](../plan-design/plan-for-software-updates.md#BKMK_ConfigureFirewalls).  

 Du kan också konfigurera om du vill skapa WSUS-rapporterings händelser på sidan **synkroniserings källa** i guiden eller på fliken **synkroniseringsinställningar** i egenskaperna för komponenten för program uppdaterings plats. Configuration Manager använder inte dessa händelser. Därför ska du normalt välja standardinställningen **skapa inte WSUS-rapporterings händelser**.  

## <a name="synchronization-schedule"></a>Synkroniseringsschema  
 Konfigurera synkroniseringsschemat på sidan **Synkroniseringsschema** i guiden eller i Egenskaper för platskomponent för programuppdatering. Den här inställningen konfigureras bara på programuppdateringsplatsen på webbplatsen på den översta nivån.  

 Om du aktiverar schemat kan du ställa in ett återkommande enkelt eller anpassat synkroniseringsschema. När du konfigurerar ett enkelt schema baseras start tiden på den lokala tiden för den dator som kör Configuration Manager-konsolen vid den tidpunkt då du skapar schemat. När du konfigurerar start tiden för ett anpassat schema baseras den på den lokala tiden för den dator som kör Configuration Manager-konsolen.  

> [!TIP]  
>  Schemalägg programuppdateringssynkroniseringen så att den körs enligt en tidsram som passar din miljö. Ett vanligt scenario är att schemalägga synkroniseringen till strax efter Microsofts regelbundna säkerhetsuppdatering den andra tisdagen i månaden, korrigeringstisdagen. Ett annat vanligt scenario är att schemalägga synkroniseringen till att köras dagligen när du använder programuppdateringar för att leverera uppdateringar av Endpoint Protection-definitioner och definitionsmotorn.  

> [!NOTE]  
>  Om du väljer att inte aktivera programuppdateringssynkronisering enligt ett schema kan du synkronisera programuppdateringar manuellt från noden **Alla programuppdateringar** eller **Programuppdateringsgrupper** i arbetsytan Programbibliotek. Mer information finns i [Synkronisera program uppdateringar](synchronize-software-updates.md).  

## <a name="supersedence-rules"></a>Ersättningsregler  
 Ange ersättningsinställningarna på sidan **Ersättningsregler** i guiden eller på fliken **Ersättningsregler** i Egenskaper för platskomponent för programuppdatering. Du kan bara ange regler för ersättning på platsen på den översta nivån. Från och med Configuration Manager version 1810 kan du ange beteendet för ersättnings regler för **funktions uppdateringar** separat från **uppdateringar som inte är**av en funktion. <!--3098809, 2977644-->

 På den här sidan kan du ange att de ersatta programuppdateringarna ska upphöra att gälla direkt, vilket förhindrar att de inkluderas i nya distributioner och vilket aktiverar en flagga som visar att de ersatta programuppdateringarna innehåller en eller flera utgångna programuppdateringar. Alternativt kan du ange en tidpunkt för när ersatta programuppdateringar upphör att gälla, så att du kan fortsätta distribuera dem. Mer information finns i [Ersättningsregler](../plan-design/plan-for-software-updates.md#BKMK_SupersedenceRules).  

> [!NOTE]  
>  Sidan **Ersättningsregler** i guiden är bara tillgänglig när du konfigurerar den första platsen för programuppdatering på platsen. Den här sidan visas inte när du installerar ytterligare platser för programuppdatering.  

## <a name="classifications"></a>Klassificeringar  
 Konfigurera klassificerings inställningarna på sidan **klassificeringar** i guiden eller på fliken **klassificeringar** i egenskaper för plats komponent för program uppdatering. Mer information om klassificering av programuppdateringar finns i [Uppdateringsklassificeringar](../plan-design/plan-for-software-updates.md#BKMK_UpdateClassifications).  

> [!NOTE]  
>  Sidan **Klassificeringar** i guiden är bara tillgänglig när du konfigurerar den första platsen för programuppdatering på platsen. Den här sidan visas inte när du installerar ytterligare platser för programuppdatering.  

> [!TIP]  
>  När du först installerar programuppdateringsplatsen på toppnivåplatsen ska du rensa alla programuppdateringsklassificeringar. Efter den första programuppdateringssynkroniseringen konfigurerar du klassificeringar från en uppdaterad lista och startar sedan om synkroniseringen. Den här inställningen konfigureras bara på programuppdateringsplatsen på webbplatsen på den översta nivån.  

## <a name="products"></a>Produkter  
 Konfigurera produkt inställningarna på sidan **produkter** i guiden eller på fliken **produkter** i egenskaperna för komponenten för program uppdaterings plats.  

> [!NOTE]  
>  Sidan **Produkter** i guiden är bara tillgänglig när du konfigurerar den första platsen för programuppdatering på platsen. Den här sidan visas inte när du installerar ytterligare platser för programuppdatering.  

> [!TIP]  
>  När du först installerar programuppdateringsplatsen på toppnivåplatsen ska du rensa alla produkter. Efter den första programuppdateringssynkroniseringen konfigurerar du produkterna från en uppdaterad lista och startar sedan om synkroniseringen. Den här inställningen konfigureras bara på programuppdateringsplatsen på webbplatsen på den översta nivån.  

## <a name="languages"></a>Språk  
 Konfigurera språk inställningarna på sidan **språk** i guiden eller på fliken **språk** i egenskaperna för komponenten för program uppdaterings plats. Ange de språk för vilka du vill synkronisera programuppdateringsfiler och sammanfattningsinformation. Inställningen **program uppdaterings fil** konfigureras vid varje program uppdaterings plats i Configuration Manager hierarkin. Inställningarna för **Sammanfattningsinformation** anges endast på programuppdateringsplatsen på den översta nivån. Mer information finns i [Språk](../plan-design/plan-for-software-updates.md#BKMK_UpdateLanguages).  

> [!NOTE]  
>  Sidan **Språk** i guiden är bara tillgänglig när du installerar platsen för programuppdatering på den centrala administrationsplatsen. Du kan konfigurera språk för programuppdateringsfilen på underordnade platser på fliken **Språk** i Egenskaper för platskomponent för programuppdatering.  

## <a name="third-party-updates"></a>Uppdateringar från tredje part
Från och med Configuration Manager version 1802 kan du aktivera uppdateringar från tredje part för Configuration Manager-klienter. När du aktiverar program uppdateringar från tredje part i egenskaperna för komponenten SUP hämtar SUP det signerings certifikat som används av WSUS för uppdateringar från tredje part. Det här alternativet är inte tillgängligt under installationen av program uppdaterings platsen och bör konfigureras när SUP har installerats. Information om hur du aktiverar klient inställningarna för uppdateringar från tredje part finns i artikeln [om klient inställningar](../../core/clients/deploy/about-client-settings.md#enable-third-party-software-updates) .

## <a name="next-steps"></a>Nästa steg
Du har installerat program uppdaterings platsen från den översta platsen i din Configuration Manager-hierarki. Upprepa procedurerna i den här artikeln för att installera program uppdaterings platsen på underordnade platser.

När du har installerat program uppdaterings platserna går du till [Synkronisera program uppdateringar](synchronize-software-updates.md).
