---
title: Konfigurera identifiering
titleSuffix: Configuration Manager
description: Konfigurera identifierings metoder för att hitta resurser som ska hanteras från nätverket, Active Directory och Azure Active Directory.
ms.date: 06/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 49505eb1-d44d-4121-8712-e0f3d8b15bf5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: cfda27df7df537ededb1f103afdd6107354af786
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347295"
---
# <a name="configure-discovery-methods-for-configuration-manager"></a>Konfigurera identifierings metoder för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Konfigurera identifierings metoder för att hitta resurser som ska hanteras från nätverket, Active Directory och Azure Active Directory (Azure AD). Börja med att aktivera och konfigurera sedan varje metod som du vill använda för att söka i din miljö. Du kan också inaktivera en metod genom att använda samma procedur som du använder för att aktivera den. De enda undantagen i den här processen är pulsslags identifiering och Server identifiering:  

- Som standard är **pulsslags identifiering** redan aktiverat när du installerar en Configuration Manager primär plats. Den har kon figurer ATS för att köras enligt ett Basic-schema. Behåll pulsslags identifiering aktiverat. Det säkerställer att identifierings data posterna (DDR) för enheterna är uppdaterade. Mer information om pulsslags identifiering finns i [om pulsslags identifiering](about-discovery-methods.md#bkmk_aboutHeartbeat).  

- **Server identifiering** är en automatisk identifierings metod. Den hittar datorer som du använder som plats system. Du kan inte konfigurera eller inaktivera den.  


## <a name="active-directory-forest-discovery"></a><a name="BKMK_ConfigADForestDisc"></a>Active Directory skogs identifiering  

För att slutföra konfigurationen av Active Directory skogs identifiering konfigurerar du inställningarna på följande platser i Configuration Manager-konsolen:  

- I noden **identifierings metoder** :

  - Aktivera den här identifierings metoden.  

  - Ange ett avsöknings schema.  

  - Välj om identifieringen automatiskt ska skapa gränser för de Active Directory-platser och undernät som identifieras.  

- I noden **Active Directory skogar** :

  - Lägg till skogar som du vill identifiera.  

  - Aktivera identifiering av Active Directory platser och undernät i den skogen.  

  - Konfigurera inställningar som gör att Configuration Manager-platser kan publicera sin plats information till skogen.  

  - Tilldela ett konto som ska användas som Active Directory skogs konto för varje skog.  

Använd följande procedurer för att aktivera identifiering av Active Directory skogar och för att konfigurera enskilda skogar för användning med Active Directory identifiering av skogar.  

### <a name="configure-active-directory-forest-discovery"></a>Konfigurera identifiering av Active Directory skog  

1. I Configuration Manager-konsolen går du till arbets ytan **Administration** , expanderar **konfiguration av hierarki**och väljer noden **identifierings metoder** .  

2. Välj identifierings metoden för Active Directory skogen för den plats där du vill konfigurera identifiering.  

3. På fliken **Start** i menyfliksområdet väljer du **Egenskaper**.  

4. Konfigurera följande inställningar på fliken **Allmänt** i egenskaperna:  

    - Aktivera identifierings metoden.

    - Ange alternativ för att skapa plats gränser för identifierade platser.  

    - Ange ett schema för när identifieringen ska köras.  

5. Välj **OK** för att spara konfigurationen.  

### <a name="configure-a-forest-for-active-directory-forest-discovery"></a>Konfigurera en skog för identifiering av Active Directory skogar  

1. I arbets ytan **Administration** expanderar du **konfiguration av hierarki**och väljer noden **Active Directory skogar** . Om Identifiering av Active Directory-skogar har körts tidigare, visas alla skogar som har identifierats i resultatfönstret. När den här identifierings metoden körs identifieras den lokala skogen och eventuella betrodda skogar. Lägg till obetrodda skogar manuellt.  

    - Om du vill konfigurera en tidigare identifierad skog väljer du skogen i resultat fönstret. I menyfliksområdet väljer du **Egenskaper** för att öppna skogs egenskaperna.

    - Om du vill konfigurera en ny skog som inte finns med i listan väljer du **Lägg till skog**i gruppen **skapa** på fliken **Start** i menyfliksområdet. Den här åtgärden öppnar dialog rutan **Lägg till skogar** .

2. På fliken **Allmänt** slutför du konfigurationerna för den skog som du vill identifiera och anger **Active Directory skogs konto**. Mer information om det här kontot finns i [konton](../../../plan-design/hierarchy/accounts.md#active-directory-forest-account).  

    > [!NOTE]  
    > Active Directory-skogskontot måste vara ett globalt konto om det ska gå att identifiera och publicera i skogar som inte är betrodda. Om du inte använder plats serverns dator konto kan du bara välja ett globalt konto.  

3. Om du planerar att låta platser publicera plats data till den här skogen går du till fliken **publicering** och slutför konfigurationer för publicering till den här skogen.  

    > [!NOTE]  
    > Om du låter platser publicera till en skog ska du utöka Active Directory schemat för den skogen för Configuration Manager. Active Directory skogs kontot måste ha fullständig behörighet till system behållaren i den skogen.  

4. Välj **OK** för att spara konfigurationen.  


## <a name="active-directory-discovery-for-computers-users-or-groups"></a><a name="BKMK_ConfigADDiscGeneral"></a>Active Directory identifiering för datorer, användare eller grupper  

Om du vill konfigurera identifiering av datorer, användare eller grupper börjar du med dessa vanliga steg:

1. I Configuration Manager-konsolen går du till arbets ytan **Administration** , expanderar **konfiguration av hierarki**och väljer noden **identifierings metoder** .  

2. Välj metoden för den plats där du vill konfigurera identifiering.  

3. På fliken **Start** i menyfliksområdet väljer du **Egenskaper**.  

4. På fliken **Allmänt** i egenskaperna markerar du kryss rutan för att aktivera identifiering. Du kan också konfigurera identifiering nu och sedan återgå till att aktivera identifiering senare.  

Använd informationen i följande avsnitt för att konfigurera de olika identifierings metoderna:  

- [Identifiering av Active Directory-grupper](#bkmk_config-adgd)  

- [Identifiering av Active Directory-system](#bkmk_config-adgd)  

- [Identifiering av Active Directory-användare](#bkmk_config-adud)  

> [!NOTE]  
> Informationen i det här avsnittet gäller inte för identifiering av Active Directory skogar.  

Även om var och en av dessa identifierings metoder är oberoende av de andra, delar de liknande alternativ. Mer information om dessa konfigurations alternativ finns i [delade alternativ för grupp-, system-och användar identifiering](about-discovery-methods.md#bkmk_shared).  

> [!WARNING]  
> Active Directory avsökningen av var och en av dessa identifierings metoder kan generera betydande nätverks trafik. Överväg att schemalägga varje identifierings metod så att den körs vid en tidpunkt när den här nätverks trafiken inte påverkar företagets användning av nätverket negativt.  

### <a name="configure-active-directory-group-discovery"></a><a name="bkmk_config-adgd"></a>Konfigurera Active Directory grupp identifiering  

1. På fliken **Allmänt** i Active Directory grupp identifiering fönstret Egenskaper väljer du **Lägg till** för att konfigurera ett identifierings omfång. Välj antingen **grupper** eller **plats**. Slutför sedan följande konfigurationer i dialog rutan **Lägg till grupper** eller **Lägg till Active Directory plats** :  

    1. Ange ett **namn** för det här identifierings omfånget.  

    2. Ange en **Active Directory-domän** eller **plats** att söka efter:  

        - Om du väljer **grupper**anger du en eller flera Active Directory grupper som ska identifieras.  

        - Om du valde **plats**anger du en Active Directory behållare som en plats att identifiera. Du kan också aktivera en rekursiv sökning efter Active Directory underordnade behållare för den här platsen.  

    3. Ange det **konto för Active Directory grupp identifiering** som platsen använder för att söka i det här identifierings omfånget. Mer information finns i [konton](../../../plan-design/hierarchy/accounts.md#active-directory-group-discovery-account).  

    4. Välj **OK** för att spara konfigurationen för identifierings omfång.  

2. Upprepa föregående steg för varje ytterligare identifierings omfång som du vill definiera.  

3. På fliken **avsöknings schema** konfigurerar du både den fullständiga identifieringen av avsöknings schema och delta identifiering.

4. På fliken **alternativ** konfigurerar du inställningar för att filtrera bort eller undanta inaktuella dator poster från identifiering. Konfigurera även identifieringen av medlemskap i distributions grupper.  

    > [!NOTE]  
    > Som standard identifierar Active Directory Group Discovery endast medlemskap i säkerhets grupper.  

5. Välj **OK** för att spara konfigurationen.  

### <a name="configure-active-directory-system-discovery"></a><a name="bkmk_config-adsd"></a>Konfigurera Active Directory system identifiering  

1. På fliken **Allmänt** i Active Directory System identifiering fönstret Egenskaper **väljer du ikonen ny ikon** ny ikon ![ ](media/Disc_new_Icon.gif) för att ange en ny Active Directory behållare. I dialog rutan **Active Directory behållare** slutför du följande konfigurationer:  

    1. Skriv eller bläddra till en plats för **sökvägen**. Det här värdet är en giltig LDAP-sökväg till en behållare eller organisationsenhet (OU). Platsen frågar efter resurser på den här sökvägen. Till exempel, `LDAP://CN=Computers,DC=contoso,DC=com`  

    2. Ange alternativ för att ändra Sök beteendet:  

        - **Identifiera objekt i Active Directory grupper**: webbplatsen tittar också på medlemskapet i grupper i den här sökvägen.  

        - **Sök rekursivt i Active Directory underordnade behållare**: om du aktiverar det här alternativet söker platsen efter ytterligare behållare eller organisationsenheter inom sökvägen ovan. Om du inaktiverar det här alternativet söker platsen bara efter resurser i den angivna sökvägen.  

          Från och med version 1806 väljer du under behållare som ska undantas från den här rekursiva sökningen. Det här alternativet hjälper till att minska antalet identifierade objekt. Välj **Lägg till** för att välja behållarna under ovanstående sökväg. I dialog rutan Välj ny behållare väljer du en underordnad behållare att undanta. Välj **OK** för att stänga dialog rutan Välj ny behållare.<!--1358143-->

          > [!Tip]  
          > Listan över Active Directory behållare i Active Directory system identifierings Fönstret Egenskaper innehåller en kolumn **med undantag**. Värdet är **Ja**när du väljer behållare som ska undantas.  

    3. Ange det konto som ska användas som **Active Directory identifierings konto**för varje plats. Mer information finns i [konton](../../../plan-design/hierarchy/accounts.md#active-directory-system-discovery-account).  

        > [!TIP]  
        > För varje angiven plats kan du konfigurera en uppsättning identifierings alternativ och ett unikt Active Directory identifierings konto.  

    4. Välj **OK** för att spara Active Directory container-konfigurationen.  

2. På fliken **avsöknings schema** konfigurerar du både den fullständiga identifieringen av avsöknings schema och delta identifiering.  

3. På fliken **Active Directory attribut** konfigurerar du ytterligare Active Directory attribut för datorer som du vill identifiera. Den här fliken listar standardattributen för objekt.  

    > [!Tip]  
    > Din organisation använder till exempel attributet **Description** på dator kontot i Active Directory. Välj **anpassad**och Lägg till `Description` som ett anpassat attribut. När den här identifierings metoden körs visas detta attribut på fliken enhets egenskaper i Configuration Manager-konsolen.<!--513948-->  

4. På fliken **alternativ** konfigurerar du inställningar för att filtrera bort eller undanta inaktuella dator poster från identifiering.  

5. Välj **OK** för att spara konfigurationen.  

### <a name="configure-active-directory-user-discovery"></a><a name="bkmk_config-adud"></a>Konfigurera identifiering av Active Directory användare  

1. På fliken **Allmänt** i Active Directory användar identifiering fönstret Egenskaper **väljer du ikonen ny ikon** ny ikon ![ ](media/Disc_new_Icon.gif) för att ange en ny Active Directory behållare. I dialog rutan **Active Directory behållare** slutför du följande konfigurationer:  

    1. Ange en eller flera platser att söka i.  

    2. Ange alternativ som ändrar Sök beteendet för varje plats.  

    3. Ange det konto som ska användas som **Active Directory identifierings konto**för varje plats. Mer information finns i [konton](../../../plan-design/hierarchy/accounts.md#active-directory-user-discovery-account).  

        > [!NOTE]  
        > För varje angiven plats kan du konfigurera en unik uppsättning identifierings alternativ och ett unikt Active Directory identifierings konto.  

    4. Välj **OK** för att spara Active Directory container-konfigurationen.  

2. På fliken **avsöknings schema** konfigurerar du både den fullständiga identifieringen av avsöknings schema och delta identifiering.  

3. På fliken **Active Directory attribut** konfigurerar du ytterligare Active Directory attribut för datorer som du vill identifiera. Den här fliken listar standardattributen för objekt.  

4. Välj **OK** för att spara konfigurationen.  


## <a name="azure-ad-user-discovery"></a><a name="azureaadisc"></a>Identifiering av Azure AD-användare

Identifiering av Azure AD-användare är inte aktiverat eller har kon figurer ATS på samma sätt som andra identifierings metoder. Konfigurera den när du har publicerat Configuration Manager-platsen till Azure AD.

Mer information finns i [identifiering av Azure AD-användare](about-discovery-methods.md#azureaddisc).

### <a name="prerequisites"></a>Förutsättningar

Om du vill aktivera och konfigurera den här identifierings metoden [konfigurerar du Azure-tjänster](azure-services-wizard.md) för **moln hantering**.

Om du använder Configuration Manager för att *skapa* Azure-appen konfigurerar den appen med de behörigheter som krävs.

Om du skapar appen i Azure först och sedan *importerar* den till Configuration Manager måste du konfigurera appen manuellt. Den här konfigurationen inkluderar beviljar behörigheten Server program att läsa katalog data.

1. Öppna [Azure Portal](https://portal.azure.com) som en användare med *globala administratörs* behörigheter. Gå till **Azure Active Directory**och välj **Appregistreringar**. Växla till **alla program** om det behövs.

1. Välj mål programmet.

1. I menyn **Hantera** väljer du **API-behörigheter**.  

    1. I panelen **API-behörigheter** väljer du **Lägg till en behörighet**.  

    2. I panelen **API-behörigheter för begäran** växlar du till de **API: er som används i organisationen**.  

    3. Sök efter och välj **Microsoft Graph** -API: et.  

        > [!Tip]
        > I version 1810 och tidigare använder du **Azure Active Directory Graph** API.

    4. Välj gruppen **program behörigheter** . Expandera **katalogen**och välj **Directory. Read. all**.  

    5. Välj **Lägg till behörigheter**.  

1. På panelen **API-behörigheter** i avsnittet **bevilja godkännande** väljer du **bevilja administratörs medgivande...**. Välj **Ja**.  

### <a name="configure-azure-ad-user-discovery"></a>Konfigurera identifiering av Azure AD-användare

När du konfigurerar Azure-tjänsten för **moln hantering** :

- På sidan **identifiering** i guiden väljer du alternativet för att **Aktivera Azure Active Directory användar identifiering**.
- Välj **Inställningar**.
- Konfigurera ett schema för när identifiering sker i dialog rutan inställningar för identifiering av Azure AD-användare. Du kan också aktivera delta identifiering, som bara söker efter nya eller ändrade konton i Azure AD.

> [!Note]  
> Om användaren är en federerad eller synkroniserad identitet måste du använda Configuration Manager [Active Directory användar identifiering](about-discovery-methods.md#bkmk_aboutUser) samt identifiering av Azure AD-användare. Mer information om Hybrid identiteter finns i [definiera en strategi för Hybrid identitets införande](/azure/active-directory/active-directory-hybrid-identity-design-considerations-identity-adoption-strategy).<!--497750-->


## <a name="azure-ad-user-group-discovery"></a><a name="bkmk_azuregroupdisco"></a>Identifiering av Azure AD-användargrupp

<!--3611956-->
> [!Tip]  
> Den här funktionen introducerades först i version 1906 som en [för hands versions funktion](../../manage/pre-release-features.md). Från och med version 2002 är det inte längre en för hands versions funktion.  

Du kan identifiera användar grupper och medlemmar i dessa grupper från Azure AD. När platsen hittar användare i Azure AD-grupper som den inte har identifierat tidigare läggs de till som nya användar resurser i Configuration Manager. En resurs post för användar grupp skapas när gruppen är en säkerhets grupp.

### <a name="prerequisites"></a>Förutsättningar

- [Azure-tjänst](azure-services-wizard.md) för moln hantering
- Behörighet att läsa och söka i Azure AD-grupper

### <a name="limitations"></a>Begränsningar

Delta identifiering för identifiering av Azure AD-användargrupp är inaktiverat i version 1906. Du kan aktivera den från Configuration Manager version 1910.

### <a name="log-files"></a>Loggfiler

Använd SMS_AZUREAD_DISCOVERY_AGENT. log för fel sökning. Den här loggen delas även med identifiering av Azure AD-användare. Mer information finns i [loggfiler](../../../plan-design/hierarchy/log-files.md#BKMK_ServerLogs).

### <a name="enable-azure-ad-user-group-discovery"></a>Aktivera identifiering av användar grupper i Azure AD

Aktivera identifiering i en befintlig Azure-tjänst för **moln hantering** :

1. Gå till arbets ytan **Administration** , expandera **Cloud Services**och välj sedan noden **Azure-tjänster** .
1. Välj en av dina Azure-tjänster och välj sedan **Egenskaper** i menyfliksområdet.
1. På fliken **identifiering** markerar du kryss rutan **Aktivera Azure Active Directory grupp identifiering**och väljer sedan **Inställningar**.
1. Välj **Lägg till** under fliken **identifierings omfång** .
    - Du kan ändra **avsöknings schemat** på fliken Övrigt.
1. Välj en eller flera användar grupper. Du kan **söka** efter namn och välja om du bara vill se **säkerhets grupper**.
    - Du uppmanas att logga in på Azure när du väljer **Sök** första gången.
1. Välj **OK** när du är klar med att välja grupper.
1. När identifieringen är klar kan du bläddra bland Azure AD-användargrupperna i noden **användare** .

Aktivera identifiering när du konfigurerar en ny **Cloud Management** Azure-tjänst:

- På sidan **identifiering** i guiden väljer du alternativet för att **Aktivera Azure Active Directory grupp identifiering**.
- Välj **Inställningar**.
- Konfigurera identifierings omfånget och ett schema för när identifiering sker i dialog rutan inställningar för identifiering av Azure AD-grupp.


## <a name="heartbeat-discovery"></a><a name="BKMK_ConfigHBDisc"></a>Pulsslags identifiering

Configuration Manager aktiverar metoden för pulsslags identifiering när du installerar en primär plats. Om du vill använda standardschemat var sjunde dag, behöver du inte konfigurera något annat. Annars behöver du bara konfigurera schemat för hur ofta klienter skickar data posten för pulsslags identifiering till en hanterings plats.  

> [!NOTE]  
> Om du aktiverar både push-installation av klienter och plats underhålls aktiviteten för **Rensa installations flagga** på samma plats, ställer du in schemat för pulsslags identifieringen som är mindre än den **period för omidentifiering av klienter** som är på plats underhålls aktiviteten **Rensa installations flagga** . Mer information om plats underhålls aktiviteter finns i [underhålls aktiviteter](../../manage/maintenance-tasks.md).  

### <a name="configure-the-heartbeat-discovery-schedule"></a>Konfigurera schemat för pulsslags identifiering  

1. I Configuration Manager-konsolen går du till arbets ytan **Administration** , expanderar **konfiguration av hierarki**och väljer noden **identifierings metoder** .  

2. Välj **identifierings** metoden för pulsslag för den plats där du vill konfigurera pulsslags identifiering.  

3. På fliken **Start** i menyfliksområdet väljer du **Egenskaper**.  

4. Konfigurera den frekvens med vilken klienter skickar en data post för pulsslags identifiering. Välj **OK** för att spara konfigurationen.  


<a name="BKMK_AboutConfigNetworkDisc"></a>

## <a name="network-discovery"></a><a name="BKMK_ConfigNetworkDisc"></a>Nätverks identifiering  

Innan du konfigurerar nätverks identifiering förstår du följande avsnitt:  

- Tillgängliga nivåer av nätverks identifiering  

- Tillgängliga alternativ för nätverks identifiering  

- Begränsa nätverks identifiering i nätverket  

Mer information finns i [om nätverks identifiering](about-discovery-methods.md#bkmk_aboutNetwork).  

I följande avsnitt finns information om vanliga konfigurationer för nätverks identifiering. Du kan konfigurera en eller flera av de här konfigurationerna för användning under samma identifierings körning. Om du använder flera konfigurationer bör du planera för de interaktioner som kan påverka identifierings resultaten.  

Du kan till exempel identifiera alla Simple Network Management Protocol-enheter (SNMP) som använder ett angivet SNMP-gruppnamn. För samma identifierings körning inaktiverar du identifieringen på ett speciellt undernät. När identifieringen körs identifierar inte nätverks identifieringen SNMP-enheter med det angivna grupp namnet på det undernät som du har inaktiverat.  

### <a name="determine-your-network-topology"></a><a name="BKMK_DetermineNetTopology"></a>Fastställ nätverk sto pol Ogin  

Du kan använda en topologi-endast identifiering för att mappa nätverket. Den här typen av identifiering identifierar inte potentiella klienter. Nätverks identifiering med enbart topologi är beroende av SNMP.  

När du mappar nätverk sto pol Ogin konfigurerar du **maximalt antal hopp** på fliken **SNMP** i dialog rutan **Egenskaper för nätverks identifiering** . Bara några hopp kan hjälpa dig att kontrol lera den nätverks bandbredd som används när identifieringen körs. När du upptäcker fler nätverk ökar du antalet hopp för att få en bättre förståelse för nätverk sto pol Ogin.  

När du har förstått nätverk sto pol Ogin konfigurerar du ytterligare egenskaper för nätverks identifiering. Dessa egenskaper hjälper dig att identifiera potentiella klienter och deras operativ system. Konfigurera även nätverks identifieringen så att de begränsar de nätverks segment som kan söka.  

Mer information finns i [så här avgör du nätverk sto pol Ogin](#bkmk_proc-top)

### <a name="network-discovery-search-options"></a>Sök alternativ för nätverks identifiering

Configuration Manager stöder följande metoder för att söka i nätverket:

- [Begränsa sökningar med hjälp av undernät](#BKMK_LimitBySubnet)
- [Sök i en speciell domän](#BKMK_SearchByDomain)
- [Begränsa sökningar med namn på SNMP-grupper](#BKMK_LimitBySNMPname)
- [Sök efter en bestämd DHCP-server](#BKMK_SearchByDHCP)

#### <a name="limit-searches-by-using-subnets"></a><a name="BKMK_LimitBySubnet"></a>Begränsa sökningar med hjälp av undernät  

Du kan konfigurera nätverks identifiering att söka i vissa undernät under en identifierings körning. Som standard söker nätverks identifiering i under nätet för den server som kör identifieringen. Alla ytterligare undernät som du konfigurerar och aktiverar gäller endast för alternativ för SNMP och DHCP. När nätverks identifiering söker i domäner begränsas den inte av konfigurationer för undernät.  

Om du anger ett eller flera undernät på fliken **undernät** i dialog rutan Egenskaper för **nätverks identifiering** genomsöks bara de undernät som du markerar som **aktiverade**.  

När du inaktiverar ett undernät tar platsen bort den från identifieringen och följande villkor gäller:  

- SNMP-baserade frågor körs inte på under nätet.  

- DHCP-servrar svarar inte med en lista med resurser som finns i under nätet.  

- Domänbaserade frågor kan identifiera resurser som finns i under nätet.  

#### <a name="search-a-specific-domain"></a><a name="BKMK_SearchByDomain"></a>Sök i en speciell domän  

Du kan konfigurera nätverks identifiering för att söka i en speciell domän eller uppsättning domäner under en identifierings körning. Som standard söker nätverks identifiering i den lokala domänen på den server som kör identifieringen.  

Om du anger en eller flera domäner på fliken **domäner** i dialog rutan **Egenskaper för nätverks identifiering** söker den bara igenom de domäner som du markerar som **aktiverade**.  

När du inaktiverar en domän tar platsen bort den från identifieringen och följande villkor gäller:  

- Nätverks identifiering frågar inte domänkontrollanter i domänen.  

- SNMP-baserade frågor kan fortfarande köras på undernät i domänen.  

- DHCP-servrar kan fortfarande svara med en lista med resurser som finns i domänen.  

#### <a name="limit-searches-by-using-snmp-community-names"></a><a name="BKMK_LimitBySNMPname"></a>Begränsa sökningar med namn på SNMP-grupper  

Du kan konfigurera nätverks identifiering för att söka i en bestämd SNMP-grupp eller grupp grupper under en identifierings körning. Som standard konfigurerar metoden den **offentliga** gruppens namn.  

Nätverks identifiering använder grupp namn för att få åtkomst till routrar som är SNMP-enheter. En router kan tillhandahålla nätverks identifiering med information om andra routrar och undernät som är länkade till den första routern.  

> [!NOTE]  
> SNMP-gruppens namn liknar lösen ord. Nätverks identifiering kan bara hämta information från en SNMP-enhet som du har angett ett grupp namn för. Varje SNMP-enhet kan ha ett eget grupp namn, men ofta delas samma grupp namn mellan flera enheter. Dessutom har de flesta SNMP-enheter ett standard grupp namn som är **offentligt**. Men vissa organisationer tar bort det **offentliga** grupp namnet från sina enheter som en säkerhets åtgärd.  

Om du inkluderar fler än en SNMP-grupp på fliken **SNMP** i dialog rutan **Egenskaper för nätverks identifiering** genomsöks de i den ordning som de visas. Kontrol lera att de mest använda namnen finns överst i listan. Den här konfigurationen hjälper till att minimera den nätverks trafik som platsen genererar när den försöker kontakta en enhet med hjälp av olika namn.

> [!NOTE]  
> Förutom att använda SNMP-gruppnamnet kan du ange IP-adressen eller det matchade namnet på en speciell SNMP-enhet. Den här åtgärden visas på fliken **SNMP-enheter** i dialog rutan **Egenskaper för nätverks identifiering** .  

#### <a name="search-a-specific-dhcp-server"></a><a name="BKMK_SearchByDHCP"></a>Sök efter en bestämd DHCP-server  

Du kan konfigurera nätverks identifiering så att den använder en bestämd DHCP-server eller flera servrar för att identifiera DHCP-klienter under en identifierings körning.  

Nätverks identifiering söker igenom varje DHCP-server som du anger på fliken **DHCP** i dialog rutan **Egenskaper för nätverks identifiering** . Om den server som kör identifieringen lånar sin IP-adress från en DHCP-server kan du konfigurera identifieringen så att den söker efter DHCP-servern. Aktivera det här beteendet med alternativet att **inkludera den DHCP-server som plats servern är konfigurerad att använda**.  

> [!NOTE]  
> För att kunna konfigurera en DHCP-server i nätverks identifiering måste din miljö ha stöd för IPv4. Du kan inte konfigurera nätverks identifiering att använda en DHCP-server i en intern IPv6-miljö.  

### <a name="how-to-configure-network-discovery"></a><a name="BKMK_HowToConfigNetDisc"></a>Så här konfigurerar du nätverks identifiering  

Använd följande procedurer för att först upptäcka nätverk sto pol Ogin och konfigurera nätverks identifieringen så att den identifierar potentiella klienter genom att använda ett eller flera av de tillgängliga alternativen för nätverks identifiering.  

#### <a name="how-to-determine-your-network-topology"></a><a name="bkmk_proc-top"></a>Så här avgör du nätverk sto pol Ogin  

1. I Configuration Manager-konsolen går du till arbets ytan **Administration** , expanderar **konfiguration av hierarki**och väljer noden **identifierings metoder** .  

2. Välj **nätverks identifierings** Metod för den plats där du vill identifiera nätverks resurser.  

3. På fliken **Start** i menyfliksområdet väljer du **Egenskaper**.  

    - På fliken **Allmänt** väljer du alternativet för att **Aktivera nätverks identifiering**. Välj sedan **topologi** från **typen av identifierings** alternativ.  

    - På fliken **undernät** väljer du alternativet **Sök lokalt undernät** .  

      > [!TIP]  
      > Om du känner till de speciella undernät som utgör ditt nätverk avmarkerar du kryss rutan **Sök i lokala undernät** . Välj sedan ikonen **ny** ikon ![ ny ikon ](media/Disc_new_Icon.gif) och Lägg till de angivna undernät som du vill söka efter. För stora nätverk söker du bara efter ett eller två undernät i taget för att minimera användningen av nätverks bandbredd.  

    - På fliken **domäner** väljer du alternativet för att söka i den **lokala domänen**.  

    - På fliken **SNMP** väljer du ett alternativ i list rutan **maximalt antal hopp** . Det här alternativet anger hur många router hopp som nätverks identifieringen kan ta för att mappa din topologi.  

      > [!TIP]  
      > När du först mappar nätverk sto pol Ogin konfigurerar du bara ett par router hopp för att minimera användningen av nätverks bandbredd.  

4. På fliken **Schemaläggning** väljer du ikonen **ny** ikon ![ ny ikon ](media/Disc_new_Icon.gif) och anger ett schema för att köra identifiering.  

    > [!NOTE]  
    > Du kan inte tilldela en annan identifierings konfiguration till separata scheman för nätverks identifiering. Varje gången en nätverks identifiering körs används den aktuella identifierings konfigurationen.  

5. Välj **OK** för att acceptera konfigurationerna. Nätverks identifiering körs vid den schemalagda tiden.  

#### <a name="how-to-configure-network-discovery"></a><a name="bkmk_proc-config"></a>Så här konfigurerar du nätverks identifiering  

1. I Configuration Manager-konsolen går du till arbets ytan **Administration** , expanderar **konfiguration av hierarki**och väljer noden **identifierings metoder** .  

2. Välj **nätverks identifierings** Metod för den plats där du vill identifiera nätverks resurser.  

3. På fliken **Start** i menyfliksområdet väljer du **Egenskaper**.  

4. På fliken **Allmänt** väljer du alternativet för att **Aktivera nätverks identifiering**.  

    - Välj från **typen av identifierings** alternativ vilken typ av identifiering du vill köra.  

    - Aktivera alternativet för **långsamt nätverk** för Configuration Manager att göra automatiska justeringar för nätverk med låg bandbredd.  

5. Om du vill konfigurera identifieringen för att söka i undernät växlar du till fliken **undernät** . Konfigurera sedan ett eller flera av följande alternativ:  

    - Om du vill köra identifiering på undernät som är lokala på den dator där identifieringen körs, aktiverar du alternativet att **söka i lokala undernät**.  

    - Om du vill söka i ett särskilt undernät kontrollerar du att under nätet visas i **undernät att söka** och har ett **Sök** värde **aktiverat**:  

      1. Om under nätet inte visas väljer du ikonen **ny** ikon ![ ny ](media/Disc_new_Icon.gif) . I dialog rutan **ny under näts tilldelning** anger du information om **undernät** och **mask** och väljer sedan **OK**. Som standard är ett nytt undernät aktiverat för sökning.  

      2. Om du vill ändra **Sök** värdet för ett undernät i listan väljer du det i listan. Välj sedan **växlings** ikonen för att växla värdet mellan **inaktive rad** och **aktive rad**.  

6. Om du vill konfigurera identifieringen för att söka i domäner växlar du till fliken **domäner** . Konfigurera sedan ett eller flera av följande alternativ:  

    - Om du vill köra identifiering på domänen på den dator där identifieringen körs aktiverar du alternativet att söka i den **lokala domänen**.  

    - Om du vill söka i en speciell domän kontrollerar du att domänen är listad i **domäner** och att **Sök** värdet är **aktiverat**:  

      1. Om domänen inte finns med i listan väljer du ikonen **ny** ikon ![ ny ](media/Disc_new_Icon.gif) . I dialog rutan **domän egenskaper** anger du **domän** informationen och väljer sedan **OK**. Som standard är en ny domän aktive rad för sökning.  

      2. Om du vill ändra **Sök** värdet för en listad domän väljer du det i listan. Välj sedan **växlings** ikonen för att växla värdet mellan **inaktive rad** och **aktive rad**.  

7. Om du vill konfigurera identifieringen så att den söker efter vissa SNMP-gruppnamn för SNMP-enheter växlar du till fliken **SNMP** . Konfigurera sedan ett eller flera av följande alternativ:  

    - Om du vill lägga till ett SNMP-gruppnamn i listan med **namn på SNMP-grupper**väljer du ikonen **ny** ikon ![ ny ](media/Disc_new_Icon.gif) . I dialog rutan **nytt SNMP-gruppnamn** anger du **namnet** på SNMP-gruppen och väljer sedan **OK**.  

    - Om du vill ta bort ett SNMP-gruppnamn väljer du grupp namnet och väljer sedan ikonen ta **bort** ikon ![ ta bort ](media/Disc_delete_Icon.gif) .  

    - Om du vill justera Sök ordningen för SNMP-gruppnamnen väljer du ett grupp namn i listan. Välj sedan ikonen Flytta **objekt uppåt** eller flytta ned-ikonen ![ ](media/Disc_moveUp_Icon.gif) **Move Item Down** ![ Flytta ned ](media/Disc_moveDown_Icon.gif) . När identifieringen körs genomsöks gruppens namn i en uppifrån och ned-ordning. 

    - Om du vill konfigurera maximalt antal router hopp för användning av SNMP-sökningar väljer du antalet hopp från List rutan **maximalt antal hopp** .  

8. Om du vill konfigurera en SNMP-enhet växlar du till fliken **SNMP-enheter** . Om enheten inte visas väljer du ikonen **ny** ikon ![ ny ](media/Disc_new_Icon.gif) . I dialog rutan **ny SNMP-enhet** anger du IP-adress eller enhets namn för SNMP-enheten och väljer sedan **OK**.  

    > [!NOTE]  
    > Om du anger ett enhets namn måste Configuration Manager kunna matcha NetBIOS-namnet till en IP-adress.  

9. Om du vill konfigurera identifieringen så att den frågar efter vissa DHCP-servrar växlar du till fliken **DHCP** . Konfigurera sedan ett eller flera av följande alternativ:  

    - Om du vill fråga DHCP-servern på den dator där identifieringen körs ska du aktivera alternativet att **alltid använda plats serverns DHCP-server**.  

      > [!NOTE]  
      > Om du vill använda det här alternativet måste servern låna ut sin IP-adress från en DHCP-server och kan inte använda en statisk IP-adress.  

    - Om du vill fråga en speciell DHCP-server väljer du ikonen **ny** ikon ![ ny ](media/Disc_new_Icon.gif) . I dialog rutan **ny DHCP-server** anger du IP-adressen eller Server namnet för DHCP-servern och väljer sedan **OK**.  

      > [!NOTE]  
      > Om du anger ett server namn måste Configuration Manager kunna matcha NetBIOS-namnet till en IP-adress.  

10. Om du vill konfigurera när identifieringen ska köras växlar du till fliken **schema** . Välj sedan ikonen **ny** ikon ![ ny ikon ](media/Disc_new_Icon.gif) för att ange ett schema för att köra nätverks identifiering. Du kan konfigurera flera återkommande scheman och flera scheman som inte har någon upprepning.  

    > [!NOTE]  
    > Om fliken **Schemaläggning** visar fler än ett schema samtidigt körs nätverks identifieringen för alla scheman när den har kon figurer ATS vid den tidpunkt som anges i schemat. Det här beteendet gäller även för återkommande scheman.  

11. Välj **OK** för att spara dina konfigurationer.  

### <a name="how-to-verify-that-network-discovery-has-finished"></a><a name="BKMK_HowToVerifyNetDisc"></a>Så här kontrollerar du att nätverks identifieringen har avslut ATS  

Tiden som nätverks identifieringen kräver för att slutföras kan variera beroende på en eller flera av följande faktorer:  

- Nätverkets storlek  

- Nätverkets topologi  

- Maximalt antal hopp som kon figurer ATS för att hitta routrar i nätverket  

- Den typ av identifiering som körs  

Nätverks identifiering skapar inte meddelanden för att varna dig när den är färdig. Använd följande procedur för att kontrol lera när identifieringen är färdig:  

1. Gå till arbets ytan **övervakning** i Configuration Manager-konsolen. Expandera **system status**och välj sedan noden **status meddelande frågor** .  

2. Välj frågan **alla status meddelanden** .  

3. På fliken **Start** i menyfliksområdet väljer du **Visa meddelanden**i gruppen **status meddelande frågor** .  

4. I fönstret alla status meddelanden väljer du ett värde i list rutan **Välj datum och tid** som innehåller hur länge sedan identifieringen startades. Klicka sedan på **OK** för att öppna **Configuration Manager visnings program för status meddelanden**.  

    > [!TIP]  
    > Du kan också använda alternativet **Ange datum och tid** för att välja ett visst datum och en tidpunkt då du körde identifieringen. Det här alternativet är användbart när du körde nätverks identifiering vid ett visst datum och bara vill hämta meddelanden från det datumet.  

5. Du kan kontrol lera att nätverks identifieringen är klar genom att söka efter ett status meddelande med följande information:  

    - Meddelande-ID: **502**  

    - Komponent: **SMS_NETWORK_DISCOVERY**  

    - Beskrivning: **den här komponenten stoppades**  

    Om det här status meddelandet inte finns har nätverks identifieringen inte avslut ATS.  

6. Om du vill verifiera att nätverks identifieringen har startat söker du efter ett status meddelande med följande information:  

    - Meddelande-ID: **500**  

    - Komponent: **SMS_NETWORK_DISCOVERY**  

    - Beskrivning: **den här komponenten startades**  

    Den här informationen kontrollerar att nätverks identifieringen har startats. Om den här informationen inte finns kan du schemalägga nätverks identifieringen igen.  
