---
title: Konfigurera Azure-tjänster
titleSuffix: Configuration Manager
description: Anslut din Configuration Manager-miljö med Azure-tjänster för moln hantering, Microsoft Store för företag och Log Analytics.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
ms.assetid: a26a653e-17aa-43eb-ab36-0e36c7d29f49
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7cb0a2c71a3ea326348b87d6b34e3109a8ef9f20
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700137"
---
# <a name="configure-azure-services-for-use-with-configuration-manager"></a>Konfigurera Azure-tjänster för användning med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Använd **guiden Azure-tjänster** för att förenkla processen med att konfigurera Azure Cloud Services som du använder med Configuration Manager. Den här guiden ger en gemensam konfigurations upplevelse med hjälp av Azure Active Directory (Azure AD)-webbappens registreringar. De här apparna tillhandahåller prenumerations-och konfigurations information och autentiserar kommunikationen med Azure AD. Appen ersätter samma information varje gång du konfigurerar en ny Configuration Manager komponent eller tjänst med Azure.

## <a name="available-services"></a>Tillgängliga tjänster

Konfigurera följande Azure-tjänster med hjälp av den här guiden:  

- **Moln hantering**: den här tjänsten gör det möjligt för webbplatsen och klienter att autentisera med hjälp av Azure AD. Den här autentiseringen möjliggör andra scenarier, t. ex.:  

  - [Installera och tilldela Configuration Manager Windows 10-klienter med Azure AD för autentisering](../../../clients/deploy/deploy-clients-cmg-azure.md)  

  - [Konfigurera identifiering av Azure AD-användare](configure-discovery-methods.md#azureaadisc)  

  - [Konfigurera identifiering av användar grupper i Azure AD](configure-discovery-methods.md#bkmk_azuregroupdisco)

  - Stöd för vissa [scenarier med Cloud Management Gateway](../../../clients/manage/cmg/plan-cloud-management-gateway.md#scenarios)  

  - [E-postmeddelanden för app-godkännande](../../../../apps/deploy-use/app-approval.md#bkmk_email-approve)

- **Log Analytics koppling**: [anslut till Azure Log Analytics](/azure/azure-monitor/platform/collect-sccm). Synkronisera samlings data till Log Analytics.  

    > [!Note]  
    > Den här artikeln hänvisar till *Log Analytics-anslutningen*, som tidigare kallades *OMS-anslutningen*. Det finns ingen funktionell skillnad. Mer information finns i [hantering av Azure-övervakning](/azure/azure-monitor/terminology#log-analytics).  

- **Microsoft Store för företag**: anslut till [Microsoft Store för företag](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md). Få Store-appar för din organisation som du kan distribuera med Configuration Manager.  

### <a name="service-details"></a>Tjänst information

I följande tabell visas information om var och en av tjänsterna.  

- **Klienter**: antalet tjänst instanser som du kan konfigurera. Varje instans måste vara en distinkt Azure AD-klient.  

- **Moln**: alla tjänster har stöd för det globala Azure-molnet, men alla tjänster har inte stöd för privata moln, t. ex. Azure amerikanska myndigheters moln.  

- **Webbapp**: om tjänsten använder en Azure AD-App av typen *webbapp/API*, kallas även server-app i Configuration Manager.  

- **Inbyggd app**: om tjänsten använder en Azure AD-App av typen *Native*, kallas även för en klient app i Configuration Manager.  

- **Åtgärder**: om du kan importera eller skapa de här apparna i guiden Configuration Manager Azure-tjänster.  

|Tjänst  |Klientorganisationer  |Moln  |Webbapp  |Inbyggd app  |Åtgärder  |
|---------|---------|---------|---------|---------|---------|
|Moln hantering med<br>Identifiering av Azure AD | Flera | Offentlig, privat | ![Stöds](media/green_check.png) | ![Stöds](media/green_check.png) | Importera, skapa |
|Log Analytics koppling | En | Offentlig, privat | ![Stöds](media/green_check.png) | ![Stöds inte](media/Red_X.png) | Importera |
|Microsoft Store för<br>Företag | En | Offentlig | ![Stöds](media/green_check.png) | ![Stöds inte](media/Red_X.png) | Importera, skapa |

### <a name="about-azure-ad-apps"></a>Om Azure AD-appar

Olika Azure-tjänster kräver distinkta konfigurationer som du gör i Azure Portal. Dessutom kan apparna för varje tjänst kräva separata behörigheter till Azure-resurser.  

Du kan använda en enda app för mer än en tjänst. Det finns bara ett objekt att hantera i Configuration Manager och Azure AD. När säkerhets nyckeln i appen upphör att gälla behöver du bara uppdatera en nyckel.

När du skapar ytterligare Azure-tjänster i guiden är Configuration Manager utformad för att återanvända information som är gemensam mellan tjänsterna. Med det här beteendet kan du behöva skriva in samma information mer än en gång.

Mer information om vilka program behörigheter och konfigurationer som krävs för varje tjänst finns i relevant Configuration Manager artikel i [tillgängliga tjänster](#available-services).

Om du vill ha mer information om Azure Apps börjar du med följande artiklar:

- [Autentisering och auktorisering i Azure App Service](/azure/app-service/app-service-authentication-overview)
- [Översikt över Web Apps](/azure/app-service-web/app-service-web-overview)
- [Grunderna i att registrera ett program i Azure AD](/azure/active-directory/develop/authentication-scenarios)  
- [Registrera ditt program med din Azure Active Directory-klient](/azure/active-directory/active-directory-app-registration)

## <a name="before-you-begin"></a>Innan du börjar

När du har bestämt vilken tjänst du vill ansluta till, se tabellen i [tjänst information](#service-details). Den här tabellen innehåller information som du behöver för att slutföra guiden Azure-tjänst. Få en diskussion i förväg med din Azure AD-administratör. Bestäm vilken av följande åtgärder som ska vidtas:

- Skapa apparna manuellt i förväg i Azure Portal. Importera sedan appens information till Configuration Manager.  

- Använd Configuration Manager för att direkt skapa apparna i Azure AD. Om du vill samla in nödvändiga data från Azure AD kan du läsa informationen i de andra avsnitten i den här artikeln.  

Vissa tjänster kräver att Azure AD-apparna har särskilda behörigheter. Granska informationen för varje tjänst för att avgöra vilka behörigheter som krävs. Innan du kan importera en webbapp måste du till exempel först skapa en Azure-administratör i [Azure Portal](https://portal.azure.com).

När du konfigurerar Log Analytics-anslutningen ger du den nya behörigheten för webb program *deltagare* i resurs gruppen som innehåller den relevanta arbets ytan. Med den här behörigheten kan Configuration Manager komma åt arbets ytan. När du tilldelar behörigheten söker du efter namnet på appens registrering i avsnittet **Lägg till användare** i Azure Portal. Den här processen är samma som när [du tillhandahåller Configuration Manager med behörighet att Log Analytics](/azure/log-analytics/log-analytics-sccm#grant-configuration-manager-with-permissions-to-log-analytics). En Azure-administratör måste tilldela dessa behörigheter innan du importerar appen till Configuration Manager.

## <a name="start-the-azure-services-wizard"></a>Starta guiden Azure-tjänster

1. I Configuration Manager-konsolen går du till arbets ytan **Administration** , expanderar **Cloud Services**och väljer noden **Azure-tjänster** .  

2. På fliken **Start** i menyfliksområdet i gruppen Azure- **tjänster** väljer du **Konfigurera Azure-tjänster**.  

3. På sidan **Azure-tjänster** i guiden Azure-tjänster:  

    1. Ange ett **namn** för objektet i Configuration Manager.  

    2. Ange en valfri **Beskrivning** som hjälper dig att identifiera tjänsten.  

    3. Välj den Azure-tjänst som du vill ansluta till Configuration Manager.  

4. Välj **Nästa** för att fortsätta till sidan [Egenskaper för Azure-appen](#azure-app-properties) i guiden Azure-tjänster.  

## <a name="azure-app-properties"></a>Egenskaper för Azure-App

På sidan **app** i guiden Azure-tjänster väljer du först Azure- **miljön** i listan. Se tabellen i [tjänst information](#service-details) för vilken miljö som för närvarande är tillgänglig för tjänsten.

Resten av appens sida varierar beroende på vilken tjänst som är angiven. Se tabellen i [tjänst information](#service-details) för vilken typ av app tjänsten använder och vilken åtgärd du kan använda.

- Om appen har stöd för både importera och skapa åtgärder väljer du **Bläddra**. Den här åtgärden öppnar [dialog rutan Server App](#server-app-dialog) eller [dialog rutan för klient program](#client-app-dialog).  

- Om appen bara har stöd för import åtgärden väljer du **Importera**. Den här åtgärden öppnar [dialog rutan importera appar (Server)](#import-apps-dialog-server) eller [Importera appar (klient)](#import-apps-dialog-client).

När du har angett apparna på den här sidan väljer du **Nästa** för att fortsätta till sidan [konfiguration eller identifiering](#configuration-or-discovery) i guiden Azure-tjänster.

### <a name="web-app"></a>Webbapp

Den här appen är Azure AD *-typen webbapp/API*, även kallat server-app i Configuration Manager.

#### <a name="server-app-dialog"></a>Dialog rutan Server App

När du väljer **Bläddra** för **webbappen** på App-sidan i guiden Azure-tjänster öppnas dialog rutan Server App. Den visar en lista som visar följande egenskaper för alla befintliga webb program:

- Eget namn på klient organisation
- Eget namn på App
- Typ av tjänst

Det finns tre åtgärder du kan vidta från dialog rutan Server App:

- Om du vill återanvända en befintlig webbapp väljer du den i listan.
- Välj **Importera** för att öppna [dialog rutan importera appar](#import-apps-dialog-server).
- Välj **skapa** för att öppna [dialog rutan skapa serverprogram](#create-server-application-dialog).

När du har valt, importera eller skapat en webbapp väljer du **OK** för att stänga dialog rutan Server App. Den här åtgärden återgår till [app-sidan](#azure-app-properties) i guiden Azure-tjänster.

#### <a name="import-apps-dialog-server"></a>Dialog rutan importera appar (Server)

När du väljer **Importera** från dialog rutan Server App eller appen app i guiden Azure-tjänster öppnas dialog rutan importera appar. På den här sidan kan du ange information om en Azure AD-webbapp som redan har skapats i Azure Portal. Den importerar metadata om webbappen till Configuration Manager. Ange följande information:

- **Namn på Azure AD-klient organisation**: namnet på din Azure AD-klient.
- **Azure AD-klient-ID**: GUID för din Azure AD-klient.
- **Program namn**: ett eget namn för appen, visnings namnet i appens registrering.
- **Klient-ID**: **programmets (klient) ID-** värde för appens registrering. Formatet är ett standard-GUID.
- **Hemlig nyckel**: du måste kopiera den hemliga nyckeln när du registrerar appen i Azure AD.
- **Förfallo datum för hemlig nyckel**: Välj ett framtida datum i kalendern.
- **App-ID-URI**: det här värdet måste vara unikt i din Azure AD-klient. Den finns i åtkomsttoken som används av Configuration Manager-klienten för att begära åtkomst till tjänsten. Värdet är **program-ID-URI: n** för app Registration-posten i Azure AD-portalen. Formatet liknar `https://ConfigMgrService` .

När du har angett informationen väljer du **Verifiera**. Välj **OK** för att stänga dialog rutan importera appar. Den här åtgärden återgår till antingen [sidan app](#azure-app-properties) i guiden Azure-tjänster eller i [dialog rutan Server App](#server-app-dialog).

> [!TIP]
> När du registrerar appen i Azure AD kan du behöva ange följande **omdirigerings-URI**manuellt: `ms-appx-web://Microsoft.AAD.BrokerPlugin/<ClientID>` . Ange appens klient-ID-GUID, till exempel: `ms-appx-web://Microsoft.AAD.BrokerPlugin/a26a653e-17aa-43eb-ab36-0e36c7d29f49` .<!-- SCCMDocs#1135 -->

#### <a name="create-server-application-dialog"></a>Dialog rutan skapa serverprogram

När du väljer **skapa** i dialog rutan Server App öppnas dialog rutan skapa serverprogram. Den här sidan automatiserar skapandet av en webbapp i Azure AD. Ange följande information:

- **Program namn**: ett eget namn för appen.
- **Start sidans URL**: det här värdet används inte av Configuration Manager, men krävs av Azure AD. Det här värdet är som standard `https://ConfigMgrService`.  
- **App-ID-URI**: det här värdet måste vara unikt i din Azure AD-klient. Den finns i åtkomsttoken som används av Configuration Manager-klienten för att begära åtkomst till tjänsten. Det här värdet är som standard `https://ConfigMgrService`.  
- **Giltighets period för hemlig nyckel**: Välj antingen **1 år** eller **2 år** i list rutan. Ett år är standardvärdet.

Välj **Logga** in för att autentisera till Azure som en administrativ användare. Autentiseringsuppgifterna sparas inte av Configuration Manager. Den här personen behöver inte behörigheter i Configuration Manager och behöver inte vara samma konto som kör guiden Azure-tjänster. När du har autentiserat till Azure visar sidan namnet på **Azure AD-klienten** för referensen.

Välj **OK** för att skapa webbappen i Azure AD och Stäng dialog rutan skapa serverprogram. Den här åtgärden återgår till [serverns app-dialogruta](#server-app-dialog).

> [!NOTE]
> Om du har definierat en princip för villkorlig åtkomst för Azure AD och gäller **alla molnappar** , måste du exkludera det skapade Server programmet från den här principen. Mer information om hur du undantar vissa appar finns i [dokumentationen för villkorlig åtkomst för Azure AD](/azure/active-directory/conditional-access/).

### <a name="native-client-app"></a>Inbyggd klient app

Den här appen är Azure AD-typen *Native*, som även kallas klient-app i Configuration Manager.

#### <a name="client-app-dialog"></a>Dialog rutan för klient program

När du väljer **Bläddra** för den **interna klient appen** på sidan app i guiden Azure-tjänster öppnas dialog rutan klient program. Den visar en lista som visar följande egenskaper för befintliga inbyggda appar:

- Eget namn på klient organisation
- Eget namn på App
- Typ av tjänst

Det finns tre åtgärder du kan vidta från dialog rutan klient app:

- Om du vill återanvända en befintlig inbyggd app väljer du den i listan. 
- Välj **Importera** för att öppna [dialog rutan importera appar](#import-apps-dialog-client).
- Välj **skapa** för att öppna [dialog rutan skapa klient program](#create-client-application-dialog).

När du har valt, importerat eller skapat en inbyggd app väljer du **OK** för att stänga dialog rutan klient program. Den här åtgärden återgår till [app-sidan](#azure-app-properties) i guiden Azure-tjänster.

#### <a name="import-apps-dialog-client"></a>Dialog rutan importera appar (klient)

När du väljer **Importera** från dialog rutan för klient program öppnas dialog rutan importera appar. På den här sidan kan du ange information om en inbyggd Azure AD-app som redan har skapats i Azure Portal. Den importerar metadata om den inbyggda appen till Configuration Manager. Ange följande information:

- **Program namn**: ett eget namn för appen.
- **Klient-ID**: **programmets (klient) ID-** värde för appens registrering. Formatet är ett standard-GUID.

När du har angett informationen väljer du **Verifiera**. Välj **OK** för att stänga dialog rutan importera appar. Den här åtgärden återgår till dialog rutan för [klientens app](#client-app-dialog).

#### <a name="create-client-application-dialog"></a>Dialog rutan skapa klient program

När du väljer **skapa** i dialog rutan för klient program öppnas dialog rutan skapa klient program. Den här sidan automatiserar skapandet av en inbyggd app i Azure AD. Ange följande information:

- **Program namn**: ett eget namn för appen.
- **Svars-URL**: det här värdet används inte av Configuration Manager, men krävs av Azure AD. Det här värdet är som standard `https://ConfigMgrService`.

Välj **Logga** in för att autentisera till Azure som en administrativ användare. Autentiseringsuppgifterna sparas inte av Configuration Manager. Den här personen behöver inte behörigheter i Configuration Manager och behöver inte vara samma konto som kör guiden Azure-tjänster. När du har autentiserat till Azure visar sidan namnet på **Azure AD-klienten** för referensen.

Välj **OK** för att skapa den inbyggda appen i Azure AD och Stäng dialog rutan skapa klient program. Den här åtgärden återgår till dialog rutan för [klientens app](#client-app-dialog).

## <a name="configuration-or-discovery"></a>Konfiguration eller identifiering

När du har angett webb-och interna appar på sidan appar, fortsätter guiden Azure-tjänster till antingen en **konfigurations** -eller **identifierings** sida, beroende på vilken tjänst som du ansluter till. Informationen om den här sidan varierar från tjänst till tjänst. Mer information finns i någon av följande artiklar:  

- **Moln hanterings** tjänst, **Discovery** -sida: [Konfigurera identifiering av Azure AD-användare](configure-discovery-methods.md#azureaadisc)  

- **Log Analytics anslutnings** tjänst, **konfigurations** sida: [Konfigurera anslutningen till Log Analytics](/azure/azure-monitor/platform/collect-sccm)  

- Sidan **Microsoft Store for Business** service, **Configurations** : [Konfigurera Microsoft Store för affärs synkronisering](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md#bkmk_config)  

Slutligen avslutar du guiden Azure-tjänster via sidorna Sammanfattning, förlopp och slut för ande. Du har slutfört konfigurationen av en Azure-tjänst i Configuration Manager. Upprepa den här processen om du vill konfigurera andra Azure-tjänster.

## <a name="renew-secret-key"></a><a name="bkmk_renew"></a> Förnya hemlig nyckel

Du måste förnya Azure AD-appens hemliga nyckel innan giltighets perioden är slut. Om du låter nyckeln förfalla kan Configuration Manager inte autentiseras med Azure AD, vilket gör att dina anslutna Azure-tjänster slutar fungera.

Från och med version 2006 visar Configuration Manager-konsolen aviseringar under följande omständigheter:<!--6386392-->

- En eller flera Azure AD-appens hemliga nycklar upphör snart att gälla
- En eller flera Azure AD-appens hemliga nycklar har upphört att gälla

Förnya den hemliga nyckeln för att minimera båda fallen.

Mer information om hur du interagerar med dessa meddelanden finns i [Configuration Manager konsol meddelanden](../../manage/admin-console-notifications.md).

### <a name="renew-key-for-created-app"></a>Förnya nyckel för den skapade appen

1. I Configuration Manager-konsolen går du till arbets ytan **Administration** , expanderar **Cloud Services**och väljer noden **Azure Active Directory klienter** .

1. I informations fönstret väljer du Azure AD-klienten för appen.

1. I menyfliksområdet väljer du **förnya hemlig nyckel**. Ange autentiseringsuppgifterna för antingen appens ägare eller en Azure AD-administratör.

### <a name="renew-key-for-imported-app"></a>Förnya nyckel för importerad app

Om du har importerat Azure-appen i Configuration Manager använder du Azure Portal för att förnya. Notera den nya hemliga nyckeln och förfallo datumet. Lägg till den här informationen i guiden **förnya hemlig nyckel** .  

> [!NOTE]
> Spara den hemliga nyckeln innan du stänger Azure-programmets egenskaps **nyckel** sida. Den här informationen tas bort när du stänger sidan.

## <a name="view-the-configuration-of-an-azure-service"></a>Visa konfigurationen för en Azure-tjänst

Visa egenskaperna för en Azure-tjänst som du har konfigurerat för användning. Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **Cloud Services**och välj Azure- **tjänster**. Välj den tjänst som du vill visa eller redigera och välj sedan **Egenskaper**.

Om du väljer en tjänst och väljer **ta bort** i menyfliksområdet, tar den här åtgärden bort anslutningen i Configuration Manager. Appen tas inte bort i Azure AD. Be Azure-administratören att ta bort appen när den inte längre behövs. Eller kör guiden Azure-tjänst för att importera appen.<!--483440-->

## <a name="cloud-management-data-flow"></a>Moln hanterings data flöde

Följande diagram är ett konceptuellt data flöde för interaktionen mellan Configuration Manager, Azure AD och anslutna moln tjänster. I det här exemplet används **moln hanterings** tjänsten, som innehåller en Windows 10-klient och både server-och klient program. Flöden för andra tjänster liknar varandra.

![Data flödes diagram för Configuration Manager med Azure AD och Cloud Management](media/aad-auth.png)

1. Configuration Manager-administratören importerar eller skapar klient-och Server appar i Azure AD.  

2. Configuration Manager identifierings metoden för Azure AD-användare körs. Webbplatsen använder Azure AD servers app-token för att fråga Microsoft Graph för användar objekt.  

3. Platsen lagrar data om användar objekt. Mer information finns i [identifiering av Azure AD-användare](about-discovery-methods.md#azureaddisc).  

4. Configuration Manager klienten begär Azure AD-användartoken. Klienten gör anspråk med program-ID: t för Azure AD-klientprogrammet och Server-appen som mål grupp. Mer information finns i [anspråk i Azure AD](/azure/active-directory/develop/authentication-scenarios#security-tokens)-säkerhetstoken.  

5. Klienten autentiserar med platsen genom att presentera Azure AD-token i Cloud Management Gateway och den lokala HTTPS-aktiverade hanterings platsen.  

Mer detaljerad information finns i [arbets flödet för Azure AD-autentisering](../../../clients/manage/azure-ccmsetup.md).