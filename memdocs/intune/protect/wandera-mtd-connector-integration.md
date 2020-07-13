---
title: Konfigurera integrering av Wandera Mobile Threat Protection med Intune
titleSuffix: Intune on Azure
description: Konfigurera Wandera Mobile Threat Protection med Microsoft Intune för att styra mobil enhetsåtkomst till företagets resurser.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/26/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: fc44bb114d6ff9089a01da2d0b7db7aa7527f4b5
ms.sourcegitcommit: 7de54acc80a2092b17fca407903281435792a77e
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/06/2020
ms.locfileid: "85972155"
---
# <a name="integrate-wandera-mobile-threat-protection-with-intune"></a>Integrera Wandera Mobile Threat Protection med Intune  

Utför följande steg när du ska integrera Wandera Mobile Threat Defense-lösningen med Intune.  

## <a name="before-you-begin"></a>Innan du börjar  

Innan du påbörjar processen för att integrera Wandera med Intune behöver du uppfylla följande förhandskrav:

- Intune-prenumeration
- Azure Active Directory-autentiseringsuppgifter för administratör och tilldelad roll som kan bevilja följande behörigheter:

    - Logga in och läsa användarprofil
    - Gå till katalogen som den inloggade användaren
    - Läs katalogdata
    - Skicka enhetsriskinformation till Intune
 
- En giltig Wandera-prenumeration
    - Ett administratörskonto med superadministratörsbehörighet

## <a name="integration-overview"></a>Integreringsöversikt

Aktivering av Mobile Threat Defense-integrering mellan Wandera och Intune kräver:

- Aktivera Wanderas UEM Connect-tjänst för att synkronisera information med Azure och Intune. Detta omfattar LCM-metadata (Life Cycle Management) för användare och enheter, tillsammans med MTD-enhetens (Mobile Threat Defense) hotnivå.
- Skapa aktiveringsprofiler i Wandera för att definiera beteendet för enhetsregistrering.
- Distribuera Wandera trådlöst till hanterade iOS- och Android-enheter.
- Konfigurera Wandera för självbetjäning för slutanvändare med MAM-WE på ohanterade iOS- och Android-enheter.

## <a name="set-up-wandera-mobile-threat-defense-integration"></a>Ställ in Mobile Threat Defense-integrering

Att konfigurera integrering mellan Wandera och Intune kräver inte något stöd från Wanderas personal och kan enkelt utföras på några minuter.

### <a name="enable-support-for-wandera-in-intune"></a>Aktivera stöd för Wandera i Intune

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj **Administration av klientorganisation** > **Anslutning och token** > **Skydd mot mobilhot** > **Lägg till**.
3. På sidan **Lägg till anslutningsapp** använder du listrutan och väljer **Wandera**. Välj sedan **Skapa**.  
4. I Mobile Threat Defense-rutan väljer du MTD-anslutningsappen **Wandera** i listan över anslutningsappar för att öppna fönstret **Redigera anslutningsapp**. Välj **Öppna administratörskonsolen för Wandera** för att öppna [RADAR](https://radar.wandera.com/login), Wandera-administratörskonsolen, och logga in. 
5. På Wandera RADAR-konsolen går du till **Integreringar > UEM-integrering** och väljer fliken **UEM Connect**. Använd listrutan EMM-leverantör och välj **Microsoft Intune**.
6. En skärm som liknar den nedan visas med de behörigheter som behöver beviljas för att slutföra integreringen:

   ![Integreringar och behörigheter](./media/wandera-mtd-connector-integration/integrations-and-permissions.png) 

7. Bredvid synkronisering av Intune-användare och enheter klickar du på knappen Bevilja för att starta processen att ge medgivande för Wandera att utföra LCM-funktioner (Life Cycle Management) med Azure och Intune.
8. När du uppmanas till det väljer du eller anger dina autentiseringsuppgifter som Azure-administratör. Granska de begärda behörigheterna och välj sedan kryssrutan för att godkänna för din organisations räkning. Klicka slutligen på Acceptera för att auktorisera LCM-integreringen.

   ![Redigera behörigheter](./media/wandera-mtd-connector-integration/permissions.png)

10. Du kommer automatiskt tillbaka till RADAR-administratörskonsolen.  Om auktoriseringen lyckades visas en grön bock bredvid knappen Bevilja.
11. Upprepa medgivandeprocessen för de återstående integreringarna som visas genom att klicka på motsvarande Bevilja-knappar tills du har en grön bock bredvid var och en.

    ![Synkroniseringsgrupp](./media/wandera-mtd-connector-integration/sync-group-name.png)

12. Gå tillbaka till Intune-konsolen och fortsätt att redigera Wandera MTD-anslutningsprogrammet. Ställ alla tillgängliga växlar som På och spara konfigurationen.

    ![Aktivera Wandera](./media/wandera-mtd-connector-integration/enable-wandera.png)

Intune och Wandera är nu anslutna.

## <a name="create-activation-profiles-in-wandera"></a>Skapa aktiveringsprofiler i Wandera

Intune-baserade distributioner underlättas av användning av Wandera-aktiveringsprofiler som definierats i RADAR.  Varje aktiveringsprofil definierar särskilda konfigurationsalternativ som autentiseringskrav, tjänstfunktioner och inledande gruppmedlemskap.

När du har skapat en aktiveringsprofil i Wandera tilldelar du den till användare och enheter i Intune.  En aktiveringsprofil är universell för enhetsplattformar och hanteringsstrategier men nedan hittar du anvisningar för hur du konfigurerar Intune baserat på dessa skillnader.

Stegen nedan förutsätter att du har skapat en aktiveringsprofil i Wandera som du vill distribuera via Intune till målenheterna. Mer information om hur du skapar och använder Wandera-aktiveringsprofiler finns i [handboken om aktiveringsprofiler](https://radar.wandera.com/?return_to=https://wandera.force.com/Customer/s/article/Enrollment-Links).

> [!NOTE]
> När du skapar aktiveringsprofiler för distribution via Intune eller MAM-WE ska du se till att ställa in alternativet Autentiserad av identitetsprovider > Azure Active Directory för den associerade användaren för maximal säkerhet, plattformsoberoende kompatibilitet och en smidig slutanvändarupplevelse.

## <a name="deploying-wandera-over-the-air-to-mdm-managed-devices"></a>Distribuera Wandera trådlöst till MDM-hanterade enheter

För iOS- och Android-enheter som hanteras av Intune kan Wandera distribueras trådlöst för snabb push-baserad aktivering. Se till att du redan har skapat de aktiveringsprofiler du behöver innan du fortsätter med det här avsnittet. För distribution av Wandera till hanterade enheter gör du följande:
- Lägg till Wandera-konfigurationsprofiler i Intune och tilldela till målenheter.
- Lägg till Wandera-appen och respektive appkonfigurationer i Intune och tilldela till målenheter.

### <a name="configure-and-deploy-ios-configuration-profiles"></a>Konfigurera och distribuera iOS-konfigurationsprofiler 

I det här avsnittet laddar du ned **nödvändiga** konfigurationsfiler för iOS-enheter och levererar dem trådlöst via MDM till dina Intune-hanterade enheter.

1. I **RADAR** navigerar du till den aktiveringsprofil du vill distribuera (Enheter > Aktiveringar) och klickar sedan på **fliken Distributionsstrategier > Hanterade enheter > Microsoft Endpoint Manager**.
2. Expandera avsnittet för **Apple iOS-övervakade** eller **Apple iOS-oövervakade** baserat på konfigurationen av enhetssamlingen.
3. Ladda ned de tillhandahållna konfigurationsprofilerna och förbered överföringen i följande steg.
4. Öppna **Microsoft Intune-administratörskonsolen** och gå till **Enheter > iOS/iPad > Konfigurationsprofiler**.  Klicka på **Skapa profil**.
5. I panelen som visas väljer du **iOS/iPad** under **Plattform** och sedan **Anpassad** under Profil. Klicka sedan på **Skapa**.
6. I fältet **Namn** anger du en beskrivande rubrik för konfigurationen, helst något som matchar namnet du gav aktiveringsprofilen i RADAR. Detta underlättar korsreferenser i framtiden. Du kan också ange koden för aktiveringsprofilen om du vill. Vi rekommenderar att du anger om konfigurationen är för övervakade eller oövervakade enheter genom att ange det sist i namnet.
7. Du kan också ange en **Beskrivning** med mer information för andra administratörer om syftet/användningen av konfigurationen. Klicka på **Nästa**.
8. Klicka på **Välj en fil** och leta upp den nedladdade konfigurationsprofilen som motsvarar den aktiveringsprofil som laddades ned i steg 3. Var noga med att välja rätt profil för övervakade eller oövervakade om du har laddat ned båda. Klicka på **Nästa**.
   <!-- image placeholder - ending future availability -->
9.  Definiera **Omfångstaggar** enligt vad som krävs för dina Intune RBAC-metoder.  Klicka på **Nästa**.
10. **Tilldela** konfigurationsprofilen till grupper med användare eller enheter som ska ha Wandera installerat.  Vi rekommenderar att du börjar med en testgrupp och sedan expanderar när valideringen visar att aktiveringarna fungerar korrekt. Klicka på **Nästa**.
11. Granska konfigurationen och korrigera om det behövs och klicka sedan på **Skapa** för att skapa och distribuera konfigurationsprofilen.

> [!NOTE]
> Wandera erbjuder en förbättrad distributionsprofil för övervakade iOS-enheter. Om du har en blandad samling övervakade och oövervakade enheter upprepar du stegen ovan för den andra profiltypen efter behov. Samma steg måste följas för eventuella framtida aktiveringsprofiler som ska distribueras via Intune. Kontakta Wandera-supporten om du har en blandad samling övervakade och oövervakade iOS-enheter och behöver hjälp med principtilldelningar baserade på övervakat läge. 

## <a name="deploying-wandera-to-mam-we-devices"></a>Distribuera Wandera till MAM-WE-enheter
För enheter som inte hanteras av Intune och som är MAM-WE-enheter använder Wandera en integrerad autentiseringsbaserad introduktionsfunktion för att aktivera och skydda företagsdata i MAM-aktiverade appar. 

I följande avsnitt beskrivs hur du konfigurerar Wandera och Intune för att göra det möjligt för slutanvändare att sömlöst aktivera Wandera innan de kan komma åt företagets data. 

### <a name="configure-azure-device-provisioning-in-a-wandera-activation-profile"></a>Konfigurera Azure Device Provisioning i en Wandera-aktiveringsprofil
Aktiveringsprofiler som ska användas med MAM-WE måste ha en associerad användare angiven för alternativet Autentiserad av identitetsprovider > Azure Active Directory.
1. I **Wandera RADAR**-portalen väljer du en befintlig eller skapar en ny aktiveringsprofil som MAM-WE-enheter ska använda under registreringen i Enheter > Aktiveringar. 
2. Klicka på **fliken Distributionsstrategier och sedan Ohanterade enheter** och bläddra till avsnittet **Azure Device Provisioning**.
3. Ange **Azure AD-klient-ID** i lämpligt textfält. Om du inte har ditt klient-ID tillgängligt klickar du på länken **Hämta mitt klient-ID** för att öppna Azure AD på en ny flik där du enkelt kan kopiera det här värdet till Urklipp.
4. (Valfritt) Ange **Grupp-ID(n)** för att begränsa användaraktiveringar till vissa grupper.
   - Om ett eller flera **grupp-ID:n** definieras, måste användaren som aktiverar MAM-WE vara medlem i minst en av de angivna grupperna för att kunna aktivera med den här aktiveringsprofilen.
   - Du kan konfigurera flera aktiveringsprofiler som konfigurerats med samma Azure-klient-ID men med olika grupp-ID:n. På så sätt kan du registrera enheter i Wandera baserat på Azure-gruppmedlemskap, vilket möjliggör differentierade funktioner efter grupp vid aktiveringstillfället.
   - Du kan konfigurera en ”standardaktiveringsprofil” som inte anger några grupp-ID:n.  Den här gruppen fungerar som en universell grupp för alla aktiveringar där den autentiserade användaren inte är medlem i en grupp med en koppling till en annan aktiveringsprofil.
5. Klicka på **Spara** i det övre högra hörnet på sidan.

## <a name="next-steps"></a>Nästa steg
- När dina Wandera-aktiveringsprofiler har lästs in i RADAR kan du skapa klientappar i Intune för att distribuera Wandera-appen till Android- och iOS-/iPadOS-enheter. Wandera-appkonfigurationen tillhandahåller viktiga funktioner som kompletterar de enhetskonfigurationsprofiler som push-överförts och rekommenderas för alla distributioner. Se [Lägg till MTD-appar](mtd-apps-ios-app-configuration-policy-add-assign.md) för specifika procedurer och anpassad information för Wandera-appar. 
- Nu när du har Wandera integrerat med Endpoint Manager kan du finjustera konfigurationen, visa rapporter och distribuera bredare i din samling av mobila enheter. Läs mer om konfiguration i [Kom igång-guiden för Support Center](https://radar.wandera.com/?return_to=https://wandera.force.com/Customer/s/getting-started) i Wandera-dokumentationen.
