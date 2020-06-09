---
title: Integrera Jamf Pro Cloud Connector med Microsoft Intune
titleSuffix: Microsoft Intune
description: Använd Jamf Cloud Connector med Microsoft Intunes efterlevnadsprinciper med Azure Active Directorys villkorsstyrda åtkomst för att integrera och skydda Jamf-hanterade enheter.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/29/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: arnab
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 734a1361d8889ca1463e8d8986239e088b90cd09
ms.sourcegitcommit: eb51bb38d484e8ef2ca3ae3c867561249fa413f3
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/29/2020
ms.locfileid: "84206374"
---
# <a name="use-the-jamf-cloud-connector-with-microsoft-intune"></a>Använda Jamf Cloud Connector med Microsoft Intune

Den här artikeln hjälper dig att installera JAMF Cloud Connector för att integrera Jamf Pro med Microsoft Intune. Cloud Connector automatiserar många av de steg som krävs när du konfigurerar integrering manuellt enligt beskrivningen i [Integrera Jamf Pro med Intune för efterlevnad](../protect/conditional-access-integrate-jamf.md).

När du konfigurerar Cloud Connector:

- Automatisk konfiguration skapar Jamf Pro-program i Azure och ersätter behovet av att konfigurera dem manuellt.
- Du kan integrera flera instanser av Jamf Pro med samma Azure-klient som är värd för din Intune-prenumeration.

Det går bara att ansluta flera instanser av Jamf Pro med en enda Azure-klient när du använder Cloud Connector. När du använder en manuellt konfigurerad anslutning kan endast en enda instans av Jamf integreras med en Azure-klient.

Det är valfritt att använda Cloud Connector:

- För nya klienter som ännu inte kan integreras med Jamf kan du välja att konfigurera Cloud Connector enligt beskrivningen i den här artikeln. Du kan också konfigurera integration manuellt enligt beskrivningen i [Integrera Jamf Pro med Intune för efterlevnad](../protect/conditional-access-integrate-jamf.md)
- För klienter som redan har en manuell konfiguration kan du välja att ta bort integreringen och sedan konfigurera Cloud Connector. Både borttagning av en befintlig integrering och konfiguration av Cloud Connector beskrivs i den här artikeln.

Om du planerar att ersätta din tidigare integrering med Jamf Cloud Connector:

- Använd [proceduren för att ta bort din aktuella konfiguration](#remove-the-jamf-pro-integration-for-a-previously-configured-tenant), vilket innefattar att ta bort företagsappar för Jamf Pro och att inaktivera manuell integrering. Sedan kan du använda [proceduren för att konfigurera Cloud Connector](#configure-the-cloud-connector-for-a-new-tenant).
- Du behöver inte registrera enheterna på nytt. Enheter som redan är registrerade kan använda Cloud Connector utan ytterligare konfiguration.
- Se till att konfigurera Cloud Connector inom 24 timmar från borttagningen av din manuella integrering för att se till att dina registrerade enheter kan fortsätta att rapportera sin status.

Mer information om Jamf Cloud Connector finns i [Konfigurera macOS Intune-integrering med hjälp av Cloud Connector](https://docs.jamf.com/technical-papers/jamf-pro/microsoft-intune/10.17.0/Configuring_the_macOS_Intune_Integration_using_the_Cloud_Connector.html) på docs.jamf.com.

## <a name="prerequisites"></a>Krav

**Produkter och tjänster**:  
- Jamf Pro 10.18 eller senare
- Ett Jamf Pro-användarkonto med behörighet för villkorlig åtkomst  
- Microsoft Intune
- Microsoft Azure AD Premium
- [Företagsportalappen för macOS](https://aka.ms/macoscompanyportal)
- macOS-enheter med OS X 10.12 Yosemite eller senare

**Nätverk**:  
Följande portar och slutpunkter måste vara tillgängliga för att Jamf och Intune ska kunna integreras korrekt:

- **Intune**: Port 443
- **Apple**: Portarna 2195, 2196 och 5223 (push-meddelanden till Intune)
- **Jamf**: Portarna 80 och 5223

- Slutpunkter:
  - login.microsoftonline.com
  - graph.windows.net  
  - *.manage.microsoft.com  

För att APN ska fungera korrekt i nätverket måste du aktivera utgående anslutningar till och omdirigerar från följande portar:

- Apple 17.0.0.0/8-blocket över TCP-portarna 5223 och 443 från alla klientnätverk.
- Portarna 2195 och 2196 från Jamf Pro-servrar.

Mer information om dessa portar finns i följande artiklar:

- [Krav för Intune-nätverkskonfiguration och bandbredd](../fundamentals/network-bandwidth-use.md).
- [Nätverksportar som används av Jamf Pro](https://www.jamf.com/jamf-nation/articles/34/network-ports-used-by-jamf-pro) på jamf.com.
- [TCP- och UDP-portar som används av Apples programvaruprodukter](https://support.apple.com/HT202944) på support.apple.com

**Konton**:  
Procedurer i den här artikeln kräver användning av konton med följande behörigheter:

- **Jamf Pro-konsol**: Ett konto med behörighet att hantera Jamf Pro
- **Administrationscenter för Microsoft Endpoint Management**: Global administratör
- **Azure-portalen**: Global administratör

## <a name="remove-the-jamf-pro-integration-for-a-previously-configured-tenant"></a>Ta bort Jamf Pro-integrering för en tidigare konfigurerad klient

Använd följande procedur för att ta bort en manuellt konfigurerad integrering av Jamf Pro från din Azure-klient *innan* du kan konfigurera molnanslutningsprogrammet.

Om du inte tidigare har konfigurerat en anslutning mellan Jamf Pro och Intune, eller om du har en eller flera anslutningar som redan använder molnanslutningen, hoppar du över den här proceduren och börjar med [Configure the Cloud Connector for a new tenant](#configure-the-cloud-connector-for-a-new-tenant) (konfigurera molnanslutningsprogrammet för en ny klientorganisation).

### <a name="remove-a-manually-configured-jamf-pro-integration"></a>Ta bort en manuellt konfigurerad Jamf Pro-integration

1. Logga in på Jamf Pro-konsolen.

2. Välj **Inställningar** (kugghjulsikonen i det övre högra hörnet) och gå sedan till **Global hantering** > **Villkorsstyrd åtkomst**.

   ![Navigera till villkorsstyrd åtkomst](./media/conditional-access-jamf-cloud-connector/navigate-jamf-console-1.png)

3. Välj **Redigera**.

4. Avmarkera kryssrutan **Enable Intune Integration for macOS** (Aktivera Intune-integrering för macOS).

   När du avmarkerar den här inställningen inaktiverar du anslutningen men sparar konfigurationen.

5. Logga in på [administrationscentret för Microsoft Endpoint Manager ](https://go.microsoft.com/fwlink/?linkid=2109431) och gå till **Innehavaradministration** > **Hantering av partnerenhet**.

   På noden **Hantering av partnerenhet** tar du bort **Program-ID** i fältet **Ange Azure Active Directory App-ID för Jamf** och väljer sedan **Spara**.

   Program-ID är ID:t för den Azure Enterprise-app som skapades i Azure när du konfigurerade en manuell integrering i Jamf Pro.

6. Logga in på [Azure-portalen](https://portal.azure.com/) med ett konto som har globala administratörsbehörigheter och gå till **Azure Active Directory** > **Företagsprogram**.

   Leta upp de två Jamf-apparna och ta bort dem. Nya program skapas automatiskt när du konfigurerar Jamf Cloud Connector i nästa procedur.

   ![Markera de Jamf-appar som ska tas bort](./media/conditional-access-jamf-cloud-connector/delete-jamf-apps.png)

   När du har inaktiverat integrering i Jamf Pro och tagit bort företagsprogrammen visas anslutningsstatusen för **Avslutade** i noden **Hantering av partnerenhet**.

   ![Avslutad anslutningsstatus](./media/conditional-access-jamf-cloud-connector/terminated-connection-status.png)

Nu när du har tagit bort den manuella konfigurationen för Jamf Pro-integrering kan du konfigurera integrering med hjälp av Cloud Connector. Information om hur du gör det finns i [Configure the Cloud Connector for a new tenant](#configure-the-cloud-connector-for-a-new-tenant) (konfigurera molnanslutningsprogrammet för en ny klientorganisation) i den här artikeln.

## <a name="configure-the-cloud-connector-for-a-new-tenant"></a>Konfigurera molnanslutningsprogrammet för en ny klientorganisation

Använd följande procedur för att konfigurera Jamf Cloud Connector för att integrera Jamf Pro och Microsoft Intune när:

- Du saknar integrering mellan Jamf Pro och Intune som konfigurerats för din Azure-klient.
- Du redan har konfigurerat en molnanslutning mellan Jamf Pro och Intune i din Azure-klientorganisation och vill integrera ytterligare en Jamf-instans med din prenumeration.

Om du för närvarande har en manuellt konfigurerad integrering mellan Intune och Jamf Pro kan du läsa i [Ta bort JAMF Pro-integrering för en tidigare konfigurerad klient](#remove-the-jamf-pro-integration-for-a-previously-configured-tenant) i den här artikeln för att ta bort den integrationen innan du fortsätter. Borttagning av en manuellt konfigurerad integrering krävs innan du kan konfigurera Jamf Cloud Connector.

### <a name="create-a-new-connection"></a>Skapa en ny anslutning

1. Logga in på Jamf Pro-konsolen.

2. Välj **Inställningar** (kugghjulsikonen i det övre högra hörnet) och gå sedan till **Global hantering** > **Villkorsstyrd åtkomst**.

   ![Navigera till villkorsstyrd åtkomst](./media/conditional-access-jamf-cloud-connector/navigate-jamf-console-1.png)

3. Välj **Redigera**.

4. Avmarkera kryssrutan för **Enable Intune Integration for macOS** (Aktivera Intune-integrering för macOS).
   - Välj den här inställningen om du vill att Jamf Pro ska skicka inventeringsuppdateringar till Microsoft Intune.
   - Du kan avmarkera den här inställningen om du vill inaktivera anslutningen men spara konfigurationen.

   > [!IMPORTANT]
   > Om **Aktivera Intune-integrering för macOS** (Aktivera Intune-integrering för macOS) redan är markerat och *Anslutningstyp* har angetts till **Manuell** måste du ta bort den integrationen innan du fortsätter. Se [Ta bort Jamf Pro-integrering för en tidigare konfigurerad klient](#remove-the-jamf-pro-integration-for-a-previously-configured-tenant) i den här artikeln innan du fortsätter.

5. Under *Anslutningstyp* väljer du **Cloud Connector**.

   ![Välja Cloud Connector på Jamf Pro-konsolen](./media/conditional-access-jamf-cloud-connector/select-cloud-connector.png)

6. På popup-menyn **Nationellt moln** väljer du platsen för det nationella molnet från Microsoft. Om du ersätter din tidigare integrering med JAMF Cloud Connector kan du hoppa över det här steget, förutsatt att platsen har angetts.

7. Välj något av följande alternativ för landningssidan för datorer som inte känns igen av Microsoft Azure:
   - **Standardsidan för Jamf Pro-enhetsregistrering** – Beroende på den aktuella macOS-enhetens status omdirigerar det här alternativet användarna till antingen Jamf Pro-portalen för enhetsregistrering (för registrering i Jamf Pro) eller Intunes företagsportal-app (för registrering i Azure AD).
   - **Sidan Åtkomst nekad**
   - **Anpassad URL**
  
   Om du ersätter din tidigare integrering med JAMF Cloud Connector kan du hoppa över det här steget, förutsatt att landningssidan har angetts.
  
8. Välj **Anslut**. Du omdirigeras för att registrera Jamf Pro-programmen i Azure.

   När du uppmanas till det anger du dina Microsoft Azure-autentiseringsuppgifter och följer anvisningarna på skärmen för att bevilja de begärda behörigheterna. Du beviljar behörigheter för **Cloud Connector** och sedan igen för **Cloud Connector-appen för användarregistrering**. Båda apparna är registrerade i Azure som företagsprogram.

   När behörigheter har beviljats för båda apparna öppnas sidan **Program-ID**.

9. På sidan **Program-ID** väljer du **Kopiera och öppna Intune**.

   ![Program-ID](./media/conditional-access-jamf-cloud-connector/copy-application-id.png)

   *Program-ID:t* kopieras till Urklipp på datorn för användning i nästa steg och noden **Hantering av partnerenhet** i *administrationscentret för Microsoft Endpoint Manager* öppnas. (**Innehavaradministration** > **Hantering av partnerenhet**).

10. På noden **Hantering av partnerenhet** *klistrar du in* **program-ID:t** i fältet **Ange Azure Active Directory App-ID för Jamf** och väljer sedan **Spara**.

    ![Konfigurera hantering av partnerenhet](./media/conditional-access-jamf-cloud-connector/partner-device-management.png)

11. Gå tillbaka till program-ID-sidan i Jamf Pro och välj **Bekräfta**.

12. Jamf Pro slutför och testar konfigurationen och visar om anslutningen har lyckats eller misslyckats på sidan Inställningar för villkorsstyrd åtkomst. Följande bild är ett exempel på framgång:

    ![Lyckad konfiguration har bekräftats i Jamf Pro](./media/conditional-access-jamf-cloud-connector/successful-configuration.png)

13. Uppdatera noden **Hantering av partnerenhet** i administrationscentret för Microsoft Endpoint Manager. Anslutningen ska nu visas som **Aktiv**:

    ![Anslutningsstatus är aktiv](./media/conditional-access-jamf-cloud-connector/active-connection-status.png)

När anslutningen mellan Jamf Pro och Microsoft Intune har upprättats skickar Jamf Pro inventeringsinformation till Microsoft Intune för varje dator som är registrerad i Azure AD (registrering med Azure AD är ett arbetsflöde för slutanvändare). Du kan visa inventeringsstatusen för villkorlig åtkomst för en användare och en dator i kategorin lokalt användarkonto för en dators inventeringsinformation i Jamf Pro.

När du har integrerat en instans av Jamf Pro med hjälp av Jamf Cloud Connector kan du använda samma procedur för att konfigurera ytterligare instanser av Jamf Pro med samma Intune-prenumeration i din Azure-klient.  

## <a name="set-up-compliance-policies-and-register-devices"></a>Ställ in efterlevnadsprinciper och registrera enheter

När du har konfigurerat integrationen mellan Intune och Jamf måste du [tillämpa efterlevnadsprinciper för enheter som hanteras av Jamf](../protect/conditional-access-assign-jamf.md).

## <a name="disconnect-jamf-pro-and-intune"></a>Koppla från Jamf Pro och Intune

Om du behöver ta bort integreringen av Jamf Pro med Intune kan du använda följande steg för att ta bort anslutningen från Jamf Pro-konsolen. Den här informationen gäller både för Cloud Connector och för en manuellt konfigurerad integrering.

1. I Jamf Pro går du till **Global Management** > **Conditional Access** (Global hantering > Villkorlig åtkomst). På fliken **macOS Intune Integration** (Intune-integrering för macOS) väljer du **Edit** (Redigera).

2. Avmarkera kryssrutan **Enable Intune Integration for macOS** (Aktivera Intune-integrering för macOS).

3. Välj **Spara**. Jamf Pro skickar din konfiguration till Intune och integreringen avslutas

4. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

5. Välj **Innehavaradministratör** > **Anslutningar och token** > **Hantering av partnerenhet** för att verifiera att statusen är **avslutad**.

   > [!NOTE]
   > Organisationens Mac-enheter tas bort på datumet (3 månader) som visas i konsolen.

## <a name="get-support-for-the-cloud-connector"></a>Få support för molnanslutningsprogrammet

Eftersom molnanslutningsprogrammet automatiskt skapar de Azure Enterprise-appar som krävs för integrering, bör din första kontakt för support vara **Jamf**. Alternativen är:

- Skicka e-post till support på `support@jamf.com`
- Använda supportportalen på Jamf Nation: https://www.jamf.com/support/ 


Innan du kontaktar supporten:

- Gå igenom kraven, till exempel portar och produktversion som du använder.
- Bekräfta att behörigheterna för följande två Jamf Pro-appar som skapats i Azure inte har ändrats. Ändringar av appens behörigheter stöds inte av Intune och kan orsaka att integreringen inte fungerar.

  **Cloud Connector-appen för användarregistrering**:
  - API-namn: Microsoft Graph
    - Behörighet: Logga in och läsa användarprofil
    - Typ: Delegerat
    - Beviljat genom: Administratörsmedgivande
    - Beviljat av: En administratör

  **Cloud Connector-appen**:
  - API-namn: Microsoft Graph (instans 1)
    - Behörighet: Logga in och läsa användarprofil
    - Typ: Delegerat
    - Beviljat genom: Administratörsmedgivande
    - Beviljat av: En administratör

  - API-namn: Microsoft Graph (instans 2)
    - Behörighet: Läs katalogdata
    - Typ: Program
    - Beviljat genom: Administratörsmedgivande
    - Beviljat av: En administratör

  - API-namn: Intune API
    - Behörighet: Skicka enhetsattribut till Microsoft Intune
    - Typ: Program
    - Beviljat genom: Administratörsmedgivande
    - Beviljat av: En administratör

## <a name="common-questions-about-the-jamf-cloud-connector"></a>Vanliga frågor om Jamf Cloud Connector

### <a name="what-data-is-shared-via-the-cloud-connector"></a>Vilka data delas via Cloud Connector?

Cloud Connector autentiserar med Microsoft Azure och skickar enhetsinventeringsdata från Jamf Pro till Azure. Dessutom hanterar Cloud Connector identifiering av tjänster i Azure, token-utväxling, kommunikationsfel och haveriberedskap.

### <a name="where-is-device-inventory-data-stored"></a>Var lagras enhetsinventeringsdata?

Enhetsinventeringsdata lagras i Jamf Pro-databasen.

### <a name="what-credentials-are-stored"></a>Vilka autentiseringsuppgifter sparas?

Inga autentiseringsuppgifter sparas. När Cloud Connector konfigureras måste administratörerna godkänna att Jamf-appen för flera klienter och den inbyggda macOS-anslutningsappen läggs till i Azure AD-klientorganisationen. När du har lagt till ett program med flera klientorganisationer begär Cloud Connector åtkomst till token för att interagera med Azure-API:et. Programåtkomsten kan när som helst återkallas i Microsoft Azure för att begränsa åtkomsten.

### <a name="how-is-data-encrypted"></a>Hur krypteras data?

Cloud Connector använder TLS (Transport Layer Security) för data som skickas mellan Jamf Pro och Microsoft Azure.

### <a name="how-does-jamf-know-which-device-is-associated-with-which-instance-of-jamf-pro"></a>Hur vet Jamf vilken enhet som är associerad med vilken instans av Jamf Pro?

Jamf Pro använder mikrotjänster i AWS för att dirigera enhetsinformationen korrekt till rätt instans.

### <a name="can-i-switch-from-using-the-cloud-connector-to-the-manual-connection-type"></a>Kan jag växla från att använda Cloud Connector till anslutningstypen Manuell?

Ja. Du kan ändra anslutningstypen till manuell igen och följa stegen för manuell konfiguration. Om du har frågor bör du vända dig till Jamf för att få hjälp.

### <a name="permissions-were-modified-on-one-or-both-required-apps-cloud-connector-and-cloud-connector-user-registration-app-and-registration-is-not-working-is-this-supported"></a>Behörigheter ändrades för en av eller båda de appar som krävs (*Cloud Connector* och *Cloud Connector-appen för användarregistrering*) och registreringen fungerar inte. Stöds detta?

Det finns inte stöd för att ändra behörigheterna för apparna.

### <a name="is-there-a-log-file-in-jamf-pro-that-shows-if-the-connection-type-has-been-changed"></a>Finns det en loggfil i Jamf Pro som visar om anslutningstypen har ändrats?

Ja, ändringarna loggas i filen JAMFChangeManagement.log. Om du vill visa loggen för ändringshantering loggar du in på Jamf Pro, går till **Inställningar** > **Systeminställningar** > **Ändringshantering** > **Loggar**, söker efter **Objekttyp** för **Villkorsstyrd åtkomst** och klickar sedan på **Information**, så visas ändringarna.

## <a name="next-steps"></a>Nästa steg

- [Tillämpa efterlevnadsprinciper för Jamf-hanterade enheter](../protect/conditional-access-assign-jamf.md)
- [Data som Jamf skickar till Intune](../protect/data-jamf-sends-to-intune.md)
