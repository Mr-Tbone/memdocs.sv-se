---
title: Konfigurera en molnhanteringsgateway
titleSuffix: Configuration Manager
description: Använd den här steg-för-steg-processen för att konfigurera en CMG (Cloud Management Gateway).
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/26/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: e0ec7d66-1502-4b31-85bb-94996b1bc66f
ms.openlocfilehash: 36d256e674a0fe973eca4bc692a244af034d5cc1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82076772"
---
# <a name="set-up-cloud-management-gateway-for-configuration-manager"></a>Konfigurera Cloud Management Gateway för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Den här processen innehåller de steg som krävs för att konfigurera en CMG (Cloud Management Gateway).

> [!Note]  
> Configuration Manager aktiverar inte den här valfria funktionen som standard. Du måste aktivera den här funktionen innan du använder den. Mer information finns i avsnittet [Enable optional features from updates](../../../servers/manage/install-in-console-updates.md#bkmk_options).


## <a name="before-you-begin"></a>Innan du börjar

Börja med att läsa artikel [planen för Cloud Management Gateway](plan-cloud-management-gateway.md). Använd den artikeln för att fastställa din CMG design.

Använd följande check lista för att kontrol lera att du har nödvändig information och förutsättningar för att skapa en CMG:  

- Azure-miljön som ska användas. Till exempel det offentliga Azure-molnet eller Azure amerikanska myndigheters molnet.  

- Du behöver ett eller flera certifikat för CMG, beroende på din design. Mer information finns i [certifikat för Cloud Management Gateway](certificates-for-cloud-management-gateway.md).  

- Du behöver följande krav för en [Azure Resource Manager](plan-cloud-management-gateway.md#azure-resource-manager) -distribution av CMG:  

    - Integrering med [Azure AD](../../../servers/deploy/configure/azure-services-wizard.md) för **moln hantering**. Identifiering av Azure AD-användare krävs inte.  

    - Microsoft **. ClassicCompute** & **Microsoft. Storage** Resource providers måste vara registrerade i Azure-prenumerationen. Mer information finns i [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-supported-services).

    - En prenumerations administratör måste logga in.  

- Ett globalt unikt namn för tjänsten. Det här namnet är från [certifikatet för CMG](certificates-for-cloud-management-gateway.md#bkmk_serverauth).  

- Om du aktiverar CMG som en moln distributions plats måste samma globalt unika CMG-tjänst namn också vara tillgängligt som ett globalt unikt lagrings konto namn. Det här namnet är från [certifikatet för CMG](certificates-for-cloud-management-gateway.md#bkmk_serverauth).

- Azure-regionen för den här CMG-distributionen.  

- Hur många virtuella dator instanser du behöver för skalning och redundans.  

- Om du fortfarande behöver använda den klassiska Azure-tjänstedistributionen i Configuration Manager version 1810 eller tidigare behöver du följande krav:  

    > [!Important]  
    > Från och med version 1810 föråldras klassiska tjänst distributioner i Azure i Configuration Manager. Använd Azure Resource Manager distributioner för Cloud Management Gateway. Mer information finns i [plan for CMG](plan-cloud-management-gateway.md#azure-resource-manager).  
    >
    > Från och med Configuration Manager version 1902 är Azure Resource Manager den enda distributions metoden för nya instanser av Cloud Management Gateway.<!-- 3605704 -->

    - ID för Azure-prenumeration  

    - Hanterings certifikat för Azure  


## <a name="set-up-a-cmg"></a>Konfigurera en CMG

Gör den här proceduren på platsen på den översta nivån. Platsen är antingen en fristående primär plats eller en central administrations plats.

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **Cloud Services**och välj **Cloud Management Gateway**.  

2. Välj **skapa Cloud Management Gateway** i menyfliksområdet.  

3. På sidan Allmänt i guiden väljer du **Logga**in. Autentisera med ett administratörs konto för Azure-prenumeration. Guiden fyller automatiskt i de återstående fälten från den information som lagras under krav för Azure AD-integration. Om du äger flera prenumerationer väljer du det **prenumerations-ID** för önskad prenumeration som du vill använda.

    > [!Note]  
    > Från och med version 1810 var klassiska tjänst distributioner i Azure föråldrade i Configuration Manager. I version 1902 och tidigare väljer du **Azure Resource Manager distribution** som distributions metoden CMG.
    >
    > Om du behöver använda en klassisk tjänst distribution väljer du det alternativet på den här sidan. Ange först ditt ID för Azure **-prenumeration**. Välj sedan **Bläddra**och välj. PFX-fil för Azures hanterings certifikat.

4. Ange **Azure-miljön** för den här CMG. Alternativen i den nedrullningsbara listan kan variera beroende på distributions metoden.  

5. Välj **Nästa**. Vänta medan platsen testar anslutningen till Azure.  

6. På sidan Inställningar i guiden väljer du först **Bläddra** och väljer. PFX-fil för certifikatet för serverautentisering för CMG. Namnet från det här certifikatet fyller i fälten för obligatoriska **tjänst-FQDN** och **tjänst namn** .  

   > [!NOTE]  
   > Certifikatet för CMG-serverautentisering stöder jokertecken. Om du använder ett jokertecken, ersätter du asterisken`*`() i fältet för **tjänstens FQDN** med det önskade värd namnet för CMG.<!--491233-->  

7. Välj den **region** List rutan för att välja Azure-regionen för den här CMG.  

8. Välj ett alternativ för **resurs grupp** .
   1. Om du väljer **Använd befintlig**väljer du en befintlig resurs grupp i list rutan. Den valda resurs gruppen måste redan finnas i den region som du valde i steg 7. Om du väljer en befintlig resurs grupp och den finns i en annan region än den tidigare valda regionen kan CMG inte etableras.
   2. Ange namnet på den nya resurs gruppen om du väljer **Skapa ny**.

9. I fältet **VM-instans** anger du antalet virtuella datorer för den här tjänsten. Standardvärdet är ett, men du kan skala upp till 16 virtuella datorer per CMG.  

10. Välj **certifikat** för att lägga till betrodda rot certifikat för klienter. Lägg till alla certifikat i förtroende kedjan.  

    > [!Note]  
    > Från och med version 1806 behöver du inte längre ange ett betrott rot certifikat på sidan inställningar när du skapar en CMG. Detta certifikat krävs inte när du använder Azure Active Directory (Azure AD) för klientautentisering, men som används för att krävas i guiden. Om du använder certifikat för PKI-klientautentisering måste du fortfarande lägga till ett betrott rot certifikat till CMG.<!--SCCMDocs-pr issue #2872-->  
    >
    > I version 1902 och tidigare kan du bara lägga till två betrodda rot certifikat utfärdare och fyra mellanliggande certifikat utfärdare (underordnade).<!-- SCCMDocs-pr#4022 -->

11. Som standard aktiverar guiden alternativet att **Verifiera åter kallelse av klient certifikat**. En lista över återkallade certifikat måste publiceras offentligt för att den här kontrollen ska fungera. Mer information finns i [publicera listan över återkallade certifikat](security-and-privacy-for-cloud-management-gateway.md#bkmk_crl).  

12. Från och med version 1906 kan du **FRAMTVINGA TLS 1,2**. Den här inställningen gäller endast för den virtuella Azure-moln tjänsten. Den gäller inte för lokala Configuration Manager plats servrar eller klienter. Mer information om TLS 1,2 finns i [så här aktiverar du tls 1,2](../../../plan-design/security/enable-tls-1-2.md).<!-- SCCMDocs-pr#4021 -->

13. Från och med version 1806 aktiverar guiden följande alternativ: **Tillåt CMG att fungera som en moln distributions plats och hantera innehåll från Azure Storage**. Nu kan en CMG också hantera innehåll till klienter. Den här funktionen minskar de nödvändiga certifikaten och kostnaden för virtuella Azure-datorer.  

14. Välj **Nästa**.  

15. Om du vill övervaka CMG-trafik med ett tröskelvärde på 14 dagar markerar du kryss rutan för att aktivera aviserings tröskeln. Ange sedan tröskelvärdet och procent andelen för att höja de olika varnings nivåerna. Välj **Nästa** när du är klar.  

16. Granska inställningarna och välj **Nästa**. Configuration Manager börjar konfigurera tjänsten. När du har stängt guiden tar det mellan fem och 15 minuter att etablera tjänsten helt i Azure. Kontrol lera kolumnen **status** för den nya CMG för att avgöra när tjänsten är klar.  

    > [!Note]  
    > Om du vill felsöka CMG-distributioner använder du **CloudMgr. log** och **CMGSetup. log**. Mer information finns i [loggfiler](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway).


## <a name="configure-primary-site-for-client-certificate-authentication"></a>Konfigurera primär plats för autentisering av klient certifikat

Om du använder [certifikat för klientautentisering](certificates-for-cloud-management-gateway.md#bkmk_clientauth) för klienter för att AUTENTISERA med CMG följer du stegen nedan för att konfigurera varje primär plats.  

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**och välj **platser**.  

2. Välj den primära plats som de Internetbaserade klienterna ska tilldelas till och välj **Egenskaper**.  

3. Växla till fliken **klient dator kommunikation** i egenskaps bladet primär plats, markera **Använd PKI-klientcertifikat (klientautentisering) när det är tillgängligt**.  

    > [!Note]
    > Från och med version 1906 kallas den här fliken **kommunikations säkerhet**.<!-- SCCMDocs#1645 -->  

4. Om du inte publicerar en CRL avmarkerar du alternativet för **klienter kontrol lera listan över återkallade certifikat (CRL) för plats system**.  


## <a name="add-the-cmg-connection-point"></a>Lägg till anslutnings punkten CMG

Anslutnings punkten för CMG är plats system rollen för att kommunicera med CMG. Om du vill lägga till anslutnings punkten för CMG följer du de allmänna anvisningarna för att [Installera plats system roller](../../../servers/deploy/configure/install-site-system-roles.md). På sidan urval för system roll i guiden Lägg till plats system roll väljer du **Cloud Management Gateway-anslutnings punkt**. Välj sedan namnet på den **moln hanterings Gateway** som servern ansluter till. Guiden visar regionen för den valda CMG.

> [!Important]
> CMG-anslutnings punkten måste ha ett [certifikat för klientautentisering](certificates-for-cloud-management-gateway.md#bkmk_clientauth) i vissa scenarier.

Om du vill felsöka CMG-tjänstens hälsa använder du **CMGService. log** och **SMS_Cloud_ProxyConnector. log**. Mer information finns i [loggfiler](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway).


## <a name="configure-client-facing-roles-for-cmg-traffic"></a>Konfigurera klient riktade roller för CMG trafik

Konfigurera hanterings platsen och plats systemen för program uppdaterings platsen så att de accepterar CMG-trafik. Gör den här proceduren på den primära platsen för alla hanterings platser och program uppdaterings platser som hanterar Internetbaserade klienter.  

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**och välj noden **servrar och plats system roller** . På fliken Start i menyfliksområdet väljer du **servrar med roll**i gruppen Visa. Välj sedan **hanterings plats** i listan.  

2. Välj den plats system server som du vill konfigurera för CMG-trafik. Välj **hanterings plats** rollen i informations fönstret och välj sedan **Egenskaper** i menyfliksområdet.  

3. I egenskaps sidan för hanterings platser under klient anslutningar markerar du kryss rutan bredvid **tillåt Configuration Manager Cloud Management Gateway-trafik**.

    Beroende på din CMG-design och Configuration Manager version kan du behöva aktivera **https** -alternativet. Mer information finns i [Aktivera hanterings plats för https](certificates-for-cloud-management-gateway.md#bkmk_mphttps).  

4. Välj **OK** för att stänga fönstret Egenskaper för hanterings plats.  

Upprepa de här stegen för ytterligare hanterings platser vid behov och för alla program uppdaterings platser.


## <a name="configure-boundary-groups"></a>Konfigurera gränser grupper

<!--3640932-->
Från och med version 1902 kan du associera en CMG med en avgränsnings grupp. Den här konfigurationen gör det möjligt för klienter att default eller återgå till CMG för klient kommunikation baserat på gränser grupp relationer.

Mer information om avgränsnings grupper finns i [Konfigurera gränser grupper](../../../servers/deploy/configure/boundary-groups.md).

När du [skapar eller konfigurerar en avgränsnings grupp](../../../servers/deploy/configure/boundary-group-procedures.md), på fliken **referenser** , lägger du till en moln hanterings-Gateway. Den här åtgärden kopplar CMG till den här gränser gruppen.


## <a name="configure-clients-for-cmg"></a>Konfigurera klienter för CMG

När CMG-och plats system rollerna körs hämtar klienterna platsen för CMG-tjänsten automatiskt på nästa plats-begäran. Klienter måste finnas i intranätet för att kunna ta emot platsen för CMG-tjänsten, såvida du inte [installerar och tilldelar Windows 10-klienter med Azure AD för autentisering](../../deploy/deploy-clients-cmg-azure.md). Avsöknings cykeln för plats begär Anden är var 24: e timme. Om du inte vill vänta på den vanliga schemalagda plats förfrågan kan du framtvinga begäran genom att starta om värd tjänsten för SMS-agent (ccmexec. exe) på datorn.  

> [!Note]
> Som standard tar alla klienter emot CMG-principen. Styr det här beteendet med klient inställningen så att [klienter kan använda en moln hanterings-Gateway](../../deploy/about-client-settings.md#enable-clients-to-use-a-cloud-management-gateway).

Configuration Manager klienten avgör automatiskt om den finns på intranätet eller Internet. Om klienten kan kontakta en domänkontrollant eller en lokal hanterings plats, anger den sin Anslutnings typ till **intranätet för närvarande**. Annars växlar den till **för närvarande Internet**och använder platsen för CMG-tjänsten för att kommunicera med platsen.

>[!NOTE]
> Du kan tvinga klienten att alltid använda CMG oavsett om den är på intranätet eller Internet. Den här konfigurationen är användbar i testnings syfte eller för klienter som du vill tvinga att alltid använda CMG. Ange följande register nyckel på klienten:
>
> `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Security, ClientAlwaysOnInternet = 1`
>
> Du kan också ange den här inställningen under klient installationen med hjälp av egenskapen [CCMALWAYSINF](../../deploy/about-client-installation-properties.md#ccmalwaysinf) .
>
> Den här inställningen gäller alltid, även om klienten växlar till en plats där gränser för gränser grupper annars utnyttjar lokala resurser.


Kontrol lera att klienterna har principen som anger CMG genom att öppna en Windows PowerShell-kommandotolk som administratör på klient datorn och kör följande kommando:`Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}`

Det här kommandot visar alla Internetbaserade hanterings platser som klienten känner till. Även om CMG inte är tekniskt en Internetbaserad hanterings plats kan klienter Visa den som en.

> [!Note]  
> Om du vill felsöka CMG-klient trafiken använder du **CMGHttpHandler. log**, **CMGService. log**och **SMS_Cloud_ProxyConnector. log**. Mer information finns i [loggfiler](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway).


## <a name="modify-a-cmg"></a>Ändra en CMG

När du har skapat en CMG kan du ändra vissa inställningar. Välj CMG i Configuration Manager-konsolen och välj **Egenskaper**. Konfigurera inställningar på följande flikar:  

#### <a name="general"></a>Allmänt

- **Hanterings certifikat för Azure**: ändra Azures hanterings certifikat för CMG. Det här alternativet är användbart när du uppdaterar certifikatet innan det upphör att gälla.  

#### <a name="settings"></a>Inställningar

- **Certifikat fil**: ändra certifikatet för SERVERAUTENTISERING för CMG. Det här alternativet är användbart när du uppdaterar certifikatet innan det upphör att gälla.  

- **Virtuell dator instans**: ändra antalet virtuella datorer som tjänsten använder i Azure. Med den här inställningen kan du dynamiskt skala upp eller ned tjänsten baserat på användnings-eller kostnads överväganden.  

- **Certifikat**: Lägg till eller ta bort betrodda rot-eller mellanliggande CA-certifikat. Det här alternativet är användbart när du lägger till nya certifikat utfärdare eller drar tillbaka utgångna certifikat.  

- **Verifiera åter kallelse av klient certifikat**: om du inte ursprungligen aktiverar den här inställningen när du skapade CMG kan du aktivera den efteråt när du har publicerat listan över återkallade certifikat. Mer information finns i [publicera listan över återkallade certifikat](security-and-privacy-for-cloud-management-gateway.md#bkmk_crl).  

- **Tillåt CMG att fungera som en moln distributions plats och hantera innehåll från Azure Storage**: från och med version 1806 är det här nya alternativet aktiverat som standard. Nu kan en CMG också hantera innehåll till klienter. Den här funktionen minskar de nödvändiga certifikaten och kostnaden för virtuella Azure-datorer.<!--1358651-->  

#### <a name="alerts"></a>Aviseringar

Konfigurera om aviseringarna när som helst när du har skapat CMG.


### <a name="redeploy-the-service"></a>Distribuera om tjänsten

Mer betydande ändringar, till exempel följande konfigurationer, kräver omdistribution av tjänsten:

- Klassisk distributions metod för att Azure Resource Manager
- Prenumeration
- Tjänstnamn
- Privat till offentlig PKI
- Region

Behåll alltid minst en aktiv CMG för Internetbaserade klienter för att ta emot en uppdaterad princip. Internetbaserade klienter kan inte kommunicera med en borttagen CMG. Klienterna känner inte till en ny dator förrän de växlar tillbaka till intranätet. När du skapar en andra CMG-instans för att ta bort den första måste du också skapa en annan CMG-anslutnings punkt.

Klienterna uppdaterar principen som standard var 24: e timme, så vänta minst en dag efter att du har skapat en ny CMG innan du tar bort den gamla. Om klienterna är inaktiverade eller saknar Internet anslutning kan du behöva vänta längre.

Om du har en befintlig CMG för den klassiska distributions metoden måste du distribuera en ny CMG för att använda distributions metoden för Azure Resource Manager.<!--509753--> Det finns två alternativ:  

- Om du vill återanvända samma tjänst namn:  

    1. Ta först bort den klassiska CMG, med hänsyn till vägledningen att alltid ha minst en aktiv CMG för Internetbaserade klienter.  

    2. Skapa en ny CMG med hjälp av en Resource Manager-distribution. Återanvänd samma certifikat för serverautentisering.  

    3. Konfigurera om anslutnings punkten för CMG till att använda den nya CMG-instansen.  

- Om du vill använda ett nytt tjänst namn:  

    1. Skapa en ny CMG med hjälp av en Resource Manager-distribution. Använd ett nytt certifikat för serverautentisering.  

    2. Skapa en ny CMG-kopplings punkt och länka med den nya CMG.  

    3. Vänta minst en dag för att Internetbaserade klienter ska kunna ta emot principer om de nya CMG.  

    4. Ta bort den klassiska CMG.  

> [!Tip]  
> Så här fastställer du den aktuella distributions modellen för en CMG:<!--SCCMDocs issue #611-->  
>
> 1. I Configuration Manager-konsolen går du till arbets ytan **Administration** , expanderar **Cloud Services**och väljer noden **Cloud Management Gateway** .  
> 2. Välj CMG-instansen.  
> 3. I informations fönstret längst ned i fönstret letar du efter attributet för **distributions modellen** . För en Resource Manager-distribution är det här attributet **Azure Resource Manager**. Den äldre distributions modellen med hanterings certifikatet för Azure visas som **azure Service Manager**.
>
> Du kan också lägga till attributet för **distributions modell** som en kolumn i listvyn.  

### <a name="modifications-in-the-azure-portal"></a>Ändringar i Azure Portal

Ändra endast CMG från Configuration Manager-konsolen. Det går inte att göra ändringar i tjänsten eller underliggande virtuella datorer direkt i Azure. Eventuella ändringar kan gå förlorade utan föregående meddelande. Precis som med alla PaaS kan tjänsten återskapa de virtuella datorerna när som helst. Dessa återuppbyggnadar kan ske för maskin varu underhåll på Server sidan eller för att tillämpa uppdateringar på det virtuella dator operativ systemet.

### <a name="delete-the-service"></a>Ta bort tjänsten

Om du behöver ta bort CMG ska du också göra det från Configuration Manager-konsolen. Om du tar bort alla komponenter i Azure manuellt blir systemet inkonsekvent. Det här läget lämnar överblivna information och oväntade beteenden kan uppstå.


## <a name="next-steps"></a>Nästa steg

- [Övervaka klienter för Cloud Management Gateway](monitor-clients-cloud-management-gateway.md)
- [Vanliga frågor och svar om Cloud Management Gateway](cloud-management-gateway-faq.md)
