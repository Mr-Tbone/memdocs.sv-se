---
title: Skapa samlingar
titleSuffix: Configuration Manager
description: Skapa samlingar i Configuration Manager för att enklare hantera grupper av användare och enheter.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1401a35e-4312-4d3b-8ceb-0abbb10d4f05
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e3f178b41fbb305ef938063bd9b9743daa6b5c69
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714362"
---
# <a name="how-to-create-collections-in-configuration-manager"></a>Skapa samlingar i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Samlingar är grupperingar av användare eller enheter. Använd samlingar för uppgifter som hantering av program, distribution av kompatibilitetsinställningar eller installation av program uppdateringar. Du kan även använda samlingar för att hantera grupper av klientinställningar eller använda dem med rollbaserad administration för att ange vilka resurser som en administrativ användare kan komma åt. Configuration Manager innehåller flera inbyggda samlingar. Mer information finns i [Introduktion till samlingar](introduction-to-collections.md).  

> [!NOTE]  
> En samling kan innehålla användare eller enheter, men inte båda.  


Informationen i den här artikeln kan hjälpa dig att skapa samlingar i Configuration Manager. Du kan också importera samlingar som har skapats på den aktuella Configuration Managers platsen eller till en annan. Mer information om hur du exporterar och importerar samlingar finns i [hantera samlingar](manage-collections.md).  


## <a name="collection-rules"></a>Samlings regler

Det finns olika typer av regler som du kan använda för att konfigurera medlemmarna i en samling i Configuration Manager.  


### <a name="direct-rule"></a>Direktregel

Använd direkta regler för att välja de användare eller datorer som du vill lägga till i en samling. Medlemskapet ändras inte om du inte tar bort en resurs från Configuration Manager. Innan du kan lägga till resurserna i en samling med direkt regler måste Configuration Manager ha identifierat dem eller så måste du importera dem. Samlingar med direkt regler har mer administrativt arbete än samlingar med Frågeregler eftersom de kräver manuella ändringar.


### <a name="query-rule"></a>Frågeregel

Uppdatera medlemskapet i en samling dynamiskt baserat på en fråga som Configuration Manager körs enligt ett schema. Du kan till exempel skapa en samling användare som tillhör personalorganisationsenheten i Active Directory Domain Services. Den här samlingen uppdateras automatiskt när nya användare läggs till eller tas bort från organisationsenheten personal.

Till exempel frågor som du kan använda för att skapa samlingar, se [så här skapar du frågor](../../../servers/manage/create-queries.md).


### <a name="device-category-rule"></a>Enhets kategori regel

Du kan göra hanteringen av dina enheter enklare genom att associera enhets kategorier med enhets samlingar. 

Mer information finns i [kategorisera enheter automatiskt i samlingar](automatically-categorize-devices-into-collections.md).<!-- SCCMDocs issue 552 -->


### <a name="include-collection-rule"></a>Regeln Inkludera samling

Inkludera medlemmar i en annan samling i en Configuration Manager-samling. Om den inkluderade samlingen ändras, Configuration Manager uppdaterar medlemskapet för den aktuella samlingen enligt ett schema.

Du kan lägga till flera regler av typen Inkludera samling till en samling.


### <a name="exclude-collection-rule"></a>Regeln Utelämna samlingar

Med utelämna samlings regler kan du undanta medlemmar i en samling från en annan Configuration Manager-samling. Om den exkluderade samlingen ändras, uppdaterar Configuration Manager medlemskapet för den aktuella samlingen enligt ett schema.

Du kan lägga till flera regler av typen Utelämna samlingar till en samling. Om en samling inkluderar både inkludera insamling och utelämna samlings regler och det uppstår en konflikt, prioriteras regeln för exkluderings samling.

#### <a name="example"></a>Exempel
Du skapar en samling som har en regel för att inkludera samlingar och en regel för exkluderings samling. Regeln Inkludera samling gäller för en samling stationära Dell-datorer. Exkluderings samlingen är för en samling datorer som har mindre än 4 GB RAM-minne. Den nya samlingen innehåller Station ära Dell-datorer med minst 4 GB RAM-minne.



## <a name="create-a-collection"></a><a name="bkmk_create"></a>Skapa en samling  

1. Gå till arbets ytan **till gångar och efterlevnad** i Configuration Manager-konsolen.  

    - Om du vill skapa en *enhets samling*väljer du noden **enhets samlingar** . Sedan väljer du **skapa enhets samling**i gruppen **skapa** på fliken **Start** i menyfliksområdet.  

    - Om du vill skapa en *användar samling*väljer du noden **användar samlingar** . Välj sedan **skapa användar samling**i gruppen **skapa** på fliken **Start** i menyfliksområdet.  

2. Ange ett **namn** och en **kommentar**på sidan **Allmänt** i guiden. I avsnittet **begränsa samling** väljer du **Bläddra**och väljer sedan en begränsande samling. Den samling som du skapar innehåller bara medlemmar från den begränsande samlingen.  

4. På sidan **medlemskaps regler** i listan **Lägg till regel** väljer du den typ av medlemskaps regel som du vill använda för samlingen. Du kan konfigurera flera regler för varje samling. Konfigurationen för varje regel varierar. Mer information om hur du konfigurerar varje regel finns i följande avsnitt i den här artikeln:  
    - [Direktregel](#bkmk-direct)
    - [Frågeregel](#bkmk-query)
    - [Enhets kategori regel](#bkmk-category)
    - [Regeln Inkludera samling](#bkmk-include)
    - [Regeln Utelämna samlingar](#bkmk-exclude)

5. Granska även följande inställningar på sidan **medlemskaps regler** .

    - **Använd stegvisa uppdateringar för samlingen**: Välj det här alternativet om du regelbundet vill söka efter och uppdatera nya eller ändrade resurser från den tidigare samlings utvärderingen. Den här processen är oberoende av en fullständig samlings utvärdering. Som standard sker stegvisa uppdateringar med intervall på 5 minuter.  

        > [!IMPORTANT]  
        >  Samlingar med Frågeregler som använder följande klasser stöder inte stegvisa uppdateringar:  
        >   
        > -   SMS_G_System_CollectedFile  
        > -   SMS_G_System_LastSoftwareScan  
        > -   SMS_G_System_AppClientState  
        > -   SMS_G_System_DCMDeploymentState  
        > -   SMS_G_System_DCMDeploymentErrorAssetDetails  
        > -   SMS_G_System_DCMDeploymentCompliantAssetDetails  
        > -   SMS_G_System_DCMDeploymentNonCompliantAssetDetails  
        > -   SMS_G_User_DCMDeploymentCompliantAssetDetails (endast för samlingar med användare)  
        > -   SMS_G_User_DCMDeploymentNonCompliantAssetDetails (endast för samlingar med användare)  
        > -   SMS_G_System_SoftwareUsageData  
        > -   SMS_G_System_CI_ComplianceState  
        > -   SMS_G_System_EndpointProtectionStatus  
        > -   SMS_GH_System_*  
        > -   SMS_GEH_System_*  

    - **Schemalägg en fullständig uppdatering för den här samlingen**: Schemalägg en regelbunden fullständig utvärdering av samlings medlemskapet.  

        Från och med version 1810 kan dessa ändringar i insamlings utvärderings beteende förbättra platsens prestanda:<!--3607726-->  

        - När du tidigare konfigurerade ett schema för en certifikatbaserad samling, fortsätter platsen att utvärdera frågan oavsett om du har aktiverat samlings inställningen för att **Schemalägga en fullständig uppdatering av den här samlingen**. Om du vill inaktivera schemat fullständigt, var du tvungen att ändra schemat till **inget**.

            Nu rensar platsen schemat när du inaktiverar den här inställningen. Om du vill ange ett schema för samlings utvärdering aktiverar du alternativet för att **Schemalägga en fullständig uppdatering av den här samlingen**.  

            När du uppdaterar platsen, för en befintlig samling som du har angett ett schema för, gör platsen det möjligt att **Schemalägga en fullständig uppdatering av den här samlingen**. Även om den här konfigurationen kanske inte är din avsikt, var det faktiska beteendet för schemat innan du uppdaterade platsen. Inaktivera det här alternativet om du vill stoppa platsen genom att utvärdera en samling enligt ett schema.  

        - Du kan inte inaktivera utvärderingen av inbyggda samlingar som **alla system**, men nu kan du konfigurera schemat. Med det här beteendet kan du anpassa den här åtgärden i en tid som uppfyller dina krav. 

            > [!TIP]  
            > På inbyggda samlingar ändrar du bara **tiden** för det anpassade schemat. Ändra inte **upprepnings mönstret**. Framtida iterationer kan framtvinga ett bestämt upprepnings mönster.  

6. Skapa den nya samlingen genom att slutföra guiden. Den nya samlingen visas under noden **Enhetssamlingar** på arbetsytan **Tillgångar och efterlevnad** .  

> [!NOTE]  
> Du måste uppdatera eller läsa in Configuration Manager-konsolen för att se medlemmarna i samlingen. De visas inte i samlingen förrän efter den första schemalagda uppdateringen. Du kan också välja **uppdaterings medlemskap** för samlingen manuellt. Det kan ta några minuter innan en samlings uppdatering har slutförts.  

        
### <a name="configure-a-direct-rule"></a><a name="bkmk-direct"></a>Konfigurera en direkt regel  

1. Ange följande information på sidan **Sök efter resurser** i **guiden Skapa regel för direkt medlemskap**.  

    - **Resurs klass**: Välj den typ av resurs som du vill söka efter och lägga till i samlingen. Ett exempel:
        - **System resurs**: Sök efter inventerings data som har returnerats från klient datorer.
        - **Okänd dator**: Välj från värden som returneras av okända datorer.
        - **Användar resurs**: Sök efter användar information som samlats in av Configuration Manager.
        - **Användar grupp resurs**: Sök efter användar grupps information som samlats in av Configuration Manager.

    - **Attributnamn**: Välj det attribut som är associerat med den valda resurs klass som du vill söka efter. Ett exempel:  

        - Om du vill välja datorer efter deras NetBIOS-namn väljer du **system resurs** i listan **resurs klass** och **NetBIOS-namn** i listan **attributnamn** .  

        - Om du vill välja användare efter namnet på organisationsenheten (OU) väljer du **användar resurs** i listan **resurs klass** och **användar namn för OU** i listan **attributnamn** .  

    - **Exkludera resurser som marker ATS som föråldrade**: om en klient dator har marker ATS som föråldrad inkluderar du inte det här värdet i Sök resultaten.  

    - **Exkludera resurser som inte har Configuration Manager-klienten installerad**: dessa resurser visas inte i Sök resultaten.  

    - **Värde**: Ange ett värde för att söka efter det valda attributnamnet. Använd procent tecknen (%) som jokertecken. Ett exempel:  
        - Om du vill söka efter datorer som har ett NetBIOS-namn som börjar med "M" anger du **m%** i det här fältet.  
        - Om du vill söka efter användare i Contoso OU, anger du **contoso** i det här fältet.

2. På sidan **Välj resurser** väljer du de resurser som du vill lägga till i samlingen i listan **resurser** och väljer sedan **Nästa**.  


### <a name="configure-a-query-rule"></a><a name="bkmk-query"></a>Konfigurera en frågeregel  

Ange följande information i dialog rutan **Egenskaper för frågeregel** .  

- **Namn**: Ange ett unikt namn för frågan.  

- **Importera frågeuttryck**: öppnar dialog rutan **Bläddra efter fråga** . Välj en [Configuration Manager fråga](../../../servers/manage/create-queries.md) som ska användas som frågeregel för samlingen.   

- **Resurs klass**: Välj den typ av resurs som du vill söka efter och lägga till i samlingen. Välj ett värde från **system resurs** om du vill söka efter inventerings data som returnerats från klient datorer eller från en **okänd dator** för att välja från värden som returneras av okända datorer.  

- **Redigera frågeuttryck**: öppnar dialog rutan **Egenskaper för frågeuttryck** där du kan skriva en fråga som ska användas som regel för samlingen. Mer information om frågor finns i [Introduktion till frågor](../../../servers/manage/introduction-to-queries.md).  

        
        > [!TIP]  
        > On the General tab, selecting the checkbox to **Omit duplicate rows (select distinct)** may result in less rows returned and potentially quicker results. 

### <a name="device-category-rule"></a><a name="bkmk-category"></a>Enhets kategori regel

Följande åtgärder är tillgängliga i fönstret **Välj enhets kategorier** .

- **Skapa**: Ange ett namn för att skapa en ny kategori.
- **Byt namn**: Byt namn på den valda kategorin.
- **Ta bort**: Välj en eller flera kategorier och ta bort dem från listan med den här åtgärden.

Mer information finns i [kategorisera enheter automatiskt i samlingar](automatically-categorize-devices-into-collections.md).<!-- SCCMDocs issue 552 -->


### <a name="configure-an-include-collection-rule"></a><a name="bkmk-include"></a>Konfigurera en regel för Inkludera samling  

I dialog rutan **Välj samlingar** väljer du de samlingar som du vill inkludera i den nya samlingen och väljer sedan **OK**.  


### <a name="configure-an-exclude-collection-rule"></a><a name="bkmk-exclude"></a>Konfigurera en regel för att utesluta samlingar  

I dialog rutan **Välj samlingar** väljer du de samlingar som du vill undanta från den nya samlingen och väljer sedan **OK**.  



## <a name="import-a-collection"></a><a name="bkmk_import"></a>Importera en samling  

När du exporterar en samling från en plats Configuration Manager sparar den som en Managed Object Format fil (MOF). Använd den här proceduren för att importera filen till din plats databas. För att slutföra den här proceduren måste du **skapa** behörigheter för klassen Collections.

> [!IMPORTANT]  
> - Se till att filen bara innehåller samlings data, kommer från en betrodd källa och inte har manipulerats.  
> 
> - Kontrol lera att filen har exporter ATS från en plats som kör samma version av Configuration Manager som du använder.  

Mer information om hur du exporterar samlingar finns i [hantera samlingar](manage-collections.md).


1. Gå till arbets ytan **till gångar och efterlevnad** i Configuration Manager-konsolen. Välj antingen noden **användar samlingar** eller **enhets samlingar** .  

2. På fliken **Start** i menyfliksområdet väljer du **Importera samlingar**i gruppen **skapa** .  

3. På sidan **Allmänt** i **guiden Importera samlingar**väljer du **Nästa**.  

4. På sidan **namn på MOF-fil** väljer du **Bläddra**. Bläddra till MOF-filen som innehåller den samlings information som du vill importera.  

5. Importera samlingen genom att slutföra guiden. Den nya samlingen visas under noden **Användarsamlingar** eller noden **Enhetssamlingar** på arbetsytan **Tillgångar och efterlevnad** . Uppdatera eller Läs in Configuration Manager-konsolen igen för att se medlemmarna i samlingen för den nyligen importerade samlingen.  

## <a name="synchronize-collection-membership-results-to-azure-active-directory-groups"></a><a name="bkmk_aadcollsync"></a>Synkronisera samlings medlemskaps resultat till Azure Active Directory grupper

<!--3607475-->
> [!Tip]  
> Den här funktionen introducerades först i version 1906 som en [för hands versions funktion](../../../servers/manage/pre-release-features.md). Från och med version 2002 är det inte längre en för hands versions funktion.  

Du kan aktivera synkronisering av samlings medlemskap till en Azure Active Directory (Azure AD)-grupp. Med den här synkroniseringen kan du använda dina befintliga regler för lokal gruppering i molnet genom att skapa Azure AD-gruppmedlemskap baserat på samlings medlemskaps resultat. Du kan synkronisera enhets samlingar. Endast enheter med en Azure Active Directory-post avspeglas i Azure AD-gruppen. Både hybrid Azure AD-anslutna och Azure Active Director-anslutna enheter stöds.

Azure AD-synkroniseringen sker var femte minut. Det är en enkelriktad process, från Configuration Manager till Azure AD. Ändringar som görs i Azure AD återspeglas inte i Configuration Manager samlingar, men skrivs inte över av Configuration Manager. Exempel: om samlingen Configuration Manager har två enheter och Azure AD-gruppen har tre olika enheter efter synkroniseringen har Azure AD-gruppen fem enheter.


### <a name="prerequisites"></a>Krav

- [Moln hantering](../../../servers/deploy/configure/azure-services-wizard.md)
- [Azure Active Directory användar identifiering](../../../servers/deploy/configure/about-discovery-methods.md#azureaddisc)

### <a name="create-a-group-and-set-the-owner-in-azure-ad"></a>Skapa en grupp och ange ägaren i Azure AD

1. Gå till [https://portal.azure.com](https://portal.azure.com).
1. Navigera till **Azure Active Directory** > **grupper** > **alla grupper**.
1. Klicka på **ny grupp** och ange ett **grupp namn** och eventuellt **grupp Beskrivning**.
1. Se till att **medlemskaps typen** är **tilldelad**.
1. Välj **ägare**och Lägg sedan till den identitet som ska skapa synkroniseringsrelation i Configuration Manager.
1. Klicka på **skapa** för att slutföra skapandet av Azure AD-gruppen.

### <a name="enable-collection-synchronization-for-the-azure-service"></a>Aktivera synkronisering av samling för Azure-tjänsten

1. I Configuration Manager-konsolen går du till **administrations** > **Översikt** > **Cloud Services** > **Azure-tjänster**.
1. Högerklicka på Azure AD-klienten där du skapade gruppen och välj **Egenskaper**.
1. På fliken **samlings synkronisering** markerar du kryss rutan **Aktivera synkronisering av Azure Directory-grupp**.
1. Spara inställningen genom att klicka på **OK** .

### <a name="enable-the-collection-to-synchronize"></a>Aktivera samlingen för synkronisering

1. I Configuration Manager-konsolen går du till **till gångar och efterlevnad** > **Översikt över** > **enhets samlingar**.
1. Högerklicka på den samling som du vill synkronisera och klicka sedan på **Egenskaper**. 
1. Klicka på **Lägg till**i fliken för att **Synkronisera AAD-grupp** .
1. På den nedrullningsbara menyn väljer du den **klient** där du skapade din Azure AD-grupp.
1. Skriv dina Sök kriterier i fältet **namn börjar med** och klicka sedan på **Sök**.
  - Om du uppmanas att logga in använder du den identitet som du har angett som ägare för Azure AD-gruppen.
1. Välj mål gruppen och klicka sedan på **OK** för att lägga till gruppen och **OK** igen för att avsluta Samlingens egenskaper.
1. Du måste vänta cirka 5 till 7 minuter innan du kan verifiera grupp medlemskapen i Azure Portal.
   - Om du vill starta en fullständig synkronisering högerklickar du på samlingen och väljer sedan **Synkronisera medlemskap**.


### <a name="verify-the-azure-ad-group-membership"></a>Verifiera medlemskapet för Azure AD-gruppen

1. Gå till [https://portal.azure.com](https://portal.azure.com).
1. Navigera till **Azure Active Directory** > **grupper** > **alla grupper**.
1. Leta upp gruppen som du skapade och välj **medlemmar**. 
1. Bekräfta att medlemmarna återspeglar de i Configuration Manager samlingen.
   - Endast enheter med Azure AD-identitet visas i gruppen.


![Synkronisera samlingar till Azure AD](media/3607475-sync-collection-to-azuread.png)

## <a name="using-powershell"></a><a name="bkmk_powershell"></a>Använda PowerShell

Du kan använda PowerShell för att skapa och importera samlingar. Mer information finns i:

* [New-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmcollection)
* [Set-CMCollection](https://docs.microsoft.com/powershell/module/ConfigurationManager/Set-CMCollection)
* [Importera – CMCollection](https://docs.microsoft.com/powershell/module/ConfigurationManager/Import-CMCollection)

## <a name="next-steps"></a>Nästa steg

[Hantera samlingar](manage-collections.md)
