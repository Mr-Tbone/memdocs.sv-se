---
title: Registrera macOS-enheter – Apple Business Manager eller Apple School Manager
titleSuffix: ''
description: Lär dig hur du registrerar företagsägda macOS-enheter.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 12/06/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1070c7b396ac3c19c340a69b6e2eb8db9d6707b6
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "80327188"
---
# <a name="automatically-enroll-macos-devices-with-the-apple-business-manager-or-apple-school-manager"></a>Registrera macOS-enheter automatiskt med Apple Business Manager eller Apple School Manager

> [!IMPORTANT]
> Apple har nyligen övergått från att använda Apples program för enhetsregistrering (DEP) till Apples program för automatisk enhetsregistrering (ADE). Intune-gränssnittet håller på att uppdateras för att återspegla detta. Till dess att vi har slutfört ändringarna kommer det att stå *Programmet för enhetsregistrering* i Intune-portalen. När du ser det används nu Automatisk enhetsregistrering.

Du kan konfigurera Intune-registrering av macOS-enheter som köpts via Apples [Apple Business Manager](https://business.apple.com/) eller [Apple School Manager](https://school.apple.com/). Du kan använda endera av dessa registreringsmetoder för ett stort antal enheter utan att behöva röra dem. Du kan leverera macOS-enheter direkt till användare. När användaren sätter på enheten körs installationsassistenten med de konfigurerade inställningarna och enheten registreras i Intune-hanteringen.

Om du vill konfigurera registrering kan du använda både Intunes och Apples portaler. Du kan skapa registreringsprofiler som innehåller inställningar som verkställs på enheterna under registreringen.

Varken Apple Business Manager-registrering eller Apple School Manager fungerar dock med [enhetsregistreringshanteraren](device-enrollment-manager-enroll.md).

<!--
**Steps to enable enrollment programs from Apple**
1. [Get an Apple DEP token and assign devices](#get-the-apple-dep-token)
2. [Create an enrollment profile](#create-an-apple-enrollment-profile)
3. [Synchronize DEP-managed devices](#sync-managed-device)
4. [Assign DEP profile to devices](#assign-an-enrollment-profile-to-devices)
5. [Distribute devices to users](#end-user-experience-with-managed-devices)
-->
## <a name="prerequisites"></a>Krav

- Enheter som köpts i [Apple School Manager](https://school.apple.com/) eller [Apples enhetsregistreringsprogram](http://deploy.apple.com)
- En lista över serienummer eller ett inköpsordernummer.
- [MDM-utfärdare](../fundamentals/mdm-authority-set.md)
- [Apple MDM-pushcertifikat](../enrollment/apple-mdm-push-certificate-get.md)

## <a name="get-an-apple-ade-token"></a>Hämta en Apple ADE-token

Innan du kan registrera macOS-enheter med ADE eller Apple School Manager behöver du en tokenfil (.p7m) från Apple. Med denna token kan Intune synkronisera information om de enheter som ditt företag äger. Intune kan också ladda upp registreringsprofiler till Apple och olika enheter.

Du kan skapa en token med hjälp av Apple-portalen. Du kan också använda Apple-portalen för att tilldela enheter till Intune för hantering.

> [!NOTE]
> Om du tar bort denna token från den klassiska Intune-portalen innan du migrerar till Azure, kan Intune återställa en borttagen Apple-token. Du kan ta bort token från Azure Portal igen.

### <a name="step-1-download-the-intune-public-key-certificate-required-to-create-the-token"></a>Steg 1. Ladda ned certifikatet för den offentliga Intune-nyckeln som krävs för att skapa token

1. Gå till [Administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) och välj **Enheter** > **macOS** > **macOS-registrering** > **Token för registreringsprogram** > **Lägg till**.

    ![Hämta en registreringsprogramtoken.](./media/device-enrollment-program-enroll-macos/image01.png)

2. Välj **Jag godkänner** för att ge Microsoft behörighet att skicka information om användare och enhet till Apple.

   ![Skärmbild av rutan Registreringsprogramtoken i arbetsytan för Apple-certifikat. Nedladdning av offentlig nyckel.](./media/device-enrollment-program-enroll-macos/add-enrollment-program-token-pane.png)

3. Välj **Hämta den offentliga nyckeln** om du vill hämta och spara krypteringsnyckelfilen (.pem) lokalt. .pem-filen används för att begära ett förtroendecertifikat från Apple-portalen.

### <a name="step-2-use-your-key-to-download-a-token-from-apple"></a>Steg 2. Använd din nyckel för att hämta en token från Apple

1. Välj **Skapa en token för Apples enhetsregistreringsprogram** eller **Skapa en token via Apple School Manager** när du vill öppna lämplig Apple-portal och logga in med ditt företags Apple-ID. Du kan förnya din token genom att använda detta Apple-ID.
2. När det gäller DEP väljer du **Kom igång** i Apple-portalen för **Enhetsregistreringsprogram** > **Hanteringsservrar** > **Lägg till MDM Server**.
3. När det gäller Apple School Manage väljer du **MDM-servrar** > **Lägg till MDM-server** i Apple-portalen.
4. Ange **MDM-servernamnet** och välj **Nästa**. Servernamnet är för din egen referens och hjälper dig att identifiera MDM-servern (hantering av mobilenheter). Det är inte namnet eller URL-adressen för Microsoft Intune-servern.

5. Dialogrutan **Lägg till &lt;ServerName&gt;** öppnas med meddelandet **Upload Your Public Key** (Överför din offentliga nyckel). Välj **Välj fil** för att överföra PEM-filen och välj sedan **Nästa**.

6. Gå till **Distributionsprogram** &gt; **Programmet för enhetsregistrering** &gt; **Hantera enheter**.
7. Under **Choose Devices By** (Välj enheter efter) anger du hur enheterna ska identifieras:
    - **Serienummer**
    - **Ordernummer**
    - **Ladda upp CSV-fil**.

   ![Skärmbild av någon som anger enheterna ska visas efter serienummer, väljer åtgärden Assign to Server (Tilldela till server) och sedan servernamnet.](./media/device-enrollment-program-enroll-macos/enrollment-program-token-specify-serial.png)

8. Välj **Assign to Server** (Tilldela till server) för **Välj åtgärd** och välj **servernamnet** som angetts för Microsoft Intune och sedan &lt;OK&gt;. Apples portal tilldelar de angivna enheterna till Intune-servern för hantering och visar sedan meddelandet **Assignment Complete** (Tilldelningen är klar).

### <a name="step-3-save-the-apple-id-used-to-create-this-token"></a>Steg 3. Spara det Apple-ID som användes för att skapa den här token

I [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) anger du Apple-ID:t för framtida referens.

![Skärmbild av någon som anger det Apple-ID som användes för att skapa registreringsprogramtoken och bläddrat till denna token.](./media/device-enrollment-program-enroll-macos/image03.png)

### <a name="step-4-upload-your-token"></a>Steg 4. Överför din token
I rutan **Apple-token**, bläddrar du till certifikatfilen (.pem), väljer **Öppna** och väljer sedan **Skapa**. Med pushcertifikatet kan Intune registrera och hantera macOS-enheter genom push-överföring av principer till registrerade enheter. Intune synkroniseras automatiskt med Apple och visar ditt registreringsprogramkonto.

## <a name="create-an-apple-enrollment-profile"></a>Skapa en Apple-registreringsprofil

Nu när du har installerat din token kan skapa du en registreringsprofil för enheter. En enhetsregistreringsprofil definierar inställningarna som tillämpas på en grupp av enheter vid registreringen.

1. Gå till [Administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) och välj **Enheter** > **macOS** > **macOS-registrering** > **Token för registreringsprogram**.
2. Välj en token, välj **Profiler** och välj sedan **Skapa profil**.

    ![Skärmbild av Skapa en profil.](./media/device-enrollment-program-enroll-macos/image04.png)

3. Under **Skapa profil**, anger du ett **Namn** och **Beskrivning** för profilen för administrationssyfte. Användarna kan inte se den här informationen. Du kan använda fältet **Namn** för att skapa en dynamisk grupp i Azure Active Directory. Använd profilnamnet för att definiera parametern enrollmentProfileName för att tilldela registreringsprofilen till enheter. Läs mer om [dynamiska Azure Active Directory-grupper](https://docs.microsoft.com/azure/active-directory/users-groups-roles/groups-dynamic-membership#rules-for-devices).

    ![Profilnamn och beskrivning.](./media/device-enrollment-program-enroll-macos/createprofile.png)

4. För **Plattform**, välj **macOS**.

5. Ange om enheter med den här profilen måste registreras med eller utan en tilldelad användare under **Användartillhörighet**.
    - **Registrera med användartillhörighet** – välj det här alternativet för enheter som tillhör användare och som vill använda Intune-företagsportalappen för tjänster som installation av appar. Om du använder ADFS kräver användartillhörighet [WS-Trust 1.3 användarnamn/kombinerad slutpunkt](https://technet.microsoft.com/library/adfs2-help-endpoints). [Mer information](https://technet.microsoft.com/itpro/powershell/windows/adfs/get-adfsendpoint). Multifaktorautentisering stöds inte för ADE-enheter för macOS med mappning mellan användare och enhet.

    - **Registrera utan användartillhörighet** – välj det här alternativet för enheter som inte är kopplade till en enda användare. Använd det här för enheter som utför uppgifter utan att komma åt lokala användardata. Appar som företagsportalappen fungerar inte.

6. Välj **Enhetshanteringsinställningar** och välj om du vill tillämpa låst registrering för enheter som använder den här profilen. **Låst registrering** inaktiverar macOS-inställningarna som tillåter att hanteringsprofilen tas bort från menyn **Systeminställningar** eller via **Terminal**. När enhetsregistreringen är klar går det inte att ändra inställningen utan att göra en rensning av enheten.

    ![Skärmbild för Enhetshanteringsinställningar.](./media/device-enrollment-program-enroll-macos/devicemanagementsettingsblade-macos.png)

7. Välj **OK**.

8. Välj **Inställningar för inställningsassistenten** och konfigurera följande profilinställningar:  ![Anpassning av installationsassistenten.](./media/device-enrollment-program-enroll-macos/setupassistantcustom-macos.png)

    | Avdelningsinställningar | Beskrivning |
    |---|---|
    | <strong>Avdelningsnamn</strong> | Visas när användare trycker på <strong>Om konfiguration</strong> vid aktiveringen. |
    | <strong>Avdelningens telefonnummer</strong> | Visas när användaren klickar på knappen <strong>Behöver hjälp</strong> vid aktiveringen. |

    Du kan välja att visa eller dölja en mängd olika skärmar i Installationsassistenten på enheten för användaren.
    - Om du väljer **Dölj** visas inte skärmen under installationen. När enheten har konfigurerats kan användaren fortfarande använda menyn **Inställningar** för att ställa in funktionen.
    - Om du väljer **Visa** så visas skärmen under installationen. Användaren kan ibland hoppa över skärmen utan att vidta några åtgärder. Det går dock att öppna menyn **Inställningar** på enheten för att ställa in funktionen. 

    | Inställningar på skärm i Installationsassistenten | Om du väljer **Visa** kommer enheten under installationen att ... |
    |------------------------------------------|------------------------------------------|
    | <strong>Lösenord</strong> | Fråga användaren om ett lösenord. Kräv alltid ett lösenord om inte enheten är skyddad eller åtkomstkontrolleras på något annat sätt (t.ex. helskärmsläge som begränsar enheten till en app). |
    | <strong>Platstjänster</strong> | Fråga användaren om deras plats. |
    | <strong>Återställa</strong> | Visa skärmen Appar och data. På den här skärmen kan användaren återställa eller överföra data från säkerhetskopieringen i iCloud när enheten konfigureras. |
    | <strong>iCloud och Apple-ID</strong> | Ge användaren möjlighet att logga in med sitt **Apple-ID** och använda **iCloud**.                         |
    | <strong>Villkor</strong> | Kräva att användaren godkänner Apples användarvillkor. |
    | <strong>Touch ID</strong> | Ge användaren möjlighet att ställa in identifiering med fingeravtryck för enheten. |
    | <strong>Apple Pay</strong> | Ge användaren möjlighet att konfigurera Apple Pay på enheten. |
    | <strong>Zoom</strong> | Ge användaren möjlighet att zooma in på skärmen under konfigurationen. |
    | <strong>Siri</strong> | Ge användaren möjlighet att ställa in Siri. |
    | <strong>Diagnostikdata</strong> | Visa skärmen Diagnostik för användaren. På den här skärmen kan användaren välja att skicka diagnostikdata till Apple. |
    | <strong>FileVault</strong> | Ge användaren möjlighet att ställa in kryptering med FileVault. |
    | <strong>iCloud Diagnostics</strong> | Ge användaren möjlighet att skicka diagnostikdata för iCloud till Apple. |
    | <strong>iCloud Storage</strong> | Ge användaren möjlighet att använda iCloud-lagring. |    
    | <strong>Visningston</strong> | Ge användaren möjlighet att aktivera Visningston. |
    | <strong>Utseende</strong> | Visa skärmen Utseende för användaren. |
    | <strong>Registrering</strong>| Kräva att användaren registrerar enheten. |
    | <strong>Sekretess</strong>| Visa sekretesskärmen för användaren. |
    | <strong>Skärmtid</strong>| Visa skärmen Skärmtid för användaren. |

9. Välj **OK**.

10. Spara profilen genom att välja **Skapa**.

## <a name="sync-managed-devices"></a>Synkronisera hanterade enheter

Nu när Intune har fått behörighet att hantera dina enheter, kan du synkronisera Intune med Apple och se dina hanterade enheter i Intune på Azure-portalen.

1. I [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) väljer du **Enheter** > **macOS** > **macOS-registrering** > **Token för registreringsprogram** > välj en token i listan > **Enheter** > **Synkronisera**. ![Skärmbild där noden Registreringsprogramenheter har valts och länkvärde håller på att väljas.](./media/device-enrollment-program-enroll-macos/image06.png)

   För att följa Apples villkor för godkänd registreringsprogramtrafik tillämpar Intune följande begränsningar:
   - En fullständig synkronisering kan inte köras oftare än en gång var sjunde dag. Under en fullständig synkronisering, hämtar Intune den fullständigt uppdaterade listan med serienummer som tilldelats den Apple MDM-server som är ansluten till Intune. Om en registreringsprogramenhet har tagits bort från Intune-portalen utan att tilldelningen till Apple MDM-servern har tagits bort i Apple-portalen så importeras den inte igen förrän den fullständiga synkroniseringen körs.   
   - En synkronisering körs automatiskt var 24:e timme. Du kan också synkronisera genom att klicka på **Synkronisera**-knappen (högst en gång var 15:e minut). Alla synkroniseringsbegäranden ges 15 minuter att slutföras. **Synkronisera**-knappen är inaktiverad tills att en synkronisering har slutförts. Synkroniseringen kommer att uppdatera status för befintliga enheter och importera nya enheter som tilldelats Apple MDM-servern.

## <a name="assign-an-enrollment-profile-to-devices"></a>Tilldela enheterna en registreringsprofil

Du måste tilldela en registreringsprogramprofil till enheterna innan de kan registreras.

1. I [Administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) väljer du **Enheter** > **macOS** > **macOS-registrering** > **Token för registreringsprogram** > välj en token i listan.
2. Välj **Enheter** > välj enheter i listan > **Tilldela profil**.
3. Välj en profil för enheterna under **Tilldela profil** och välj sedan **Tilldela**.

### <a name="assign-a-default-profile"></a>Ange som standardprofil

Du kan välja en macOS- och iOS/iPadOS-profil av standardtyp som ska tillämpas för alla enheter som registreras med en specifik token. 

1. I [Administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) väljer du **Enheter** > **macOS** > **macOS-registrering** > **Token för registreringsprogram** > välj en token i listan.
2. Välj **Ange standardprofil**, välj en profil i listmenyn och välj sedan **Spara**. Den här profilen kommer att tillämpas på alla enheter som registreras med token.

## <a name="distribute-devices"></a>Distribuera enheter

Du har aktiverat hantering och synkronisering mellan Apple och Intune, och har tilldelat en profil så att enheterna kan registreras. Du kan nu distribuera enheter till användare. Enheter med användartillhörighet kräver att varje användare tilldelas en Intune-licens. Enheter utan användartillhörighet kräver en enhetslicens. En aktiverad enhet kan inte använda en registreringsprofil förrän enheten har rensats.

## <a name="renew-an-ade-token"></a>Förnya en ADE-token

1. Gå till deploy.apple.com.  
2. Under **Hantera servrar**, väljer du din MDM-server som är associerad med den tokenfil som du vill förnya.
3. Välj **Skapa ny Token**.

    ![Skärmbild av Skapa ny token.](./media/device-enrollment-program-enroll-macos/generatenewtoken.png)

4. Välj **Din servertoken**.  
5. I [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) väljer du **Enhetsregistrering** > **Apple-registrering** > **Token för registreringsprogram** > välj token.
    ![Skärmbild av registreringsprogramtoken.](./media/device-enrollment-program-enroll-macos/enrollmentprogramtokens.png)

6. Välj **Förnya token** och ange det Apple-ID som användes för att skapa den ursprungliga token.  
    ![Skärmbild av Skapa ny token.](./media/device-enrollment-program-enroll-macos/renewtoken.png)

7. Överför den nyligen hämtade token.  
8. Välj **Förnya token**. Du får se en bekräftelse att token har förnyats.
    ![Skärmbild av bekräftelse.](./media/device-enrollment-program-enroll-macos/confirmation.png)

## <a name="next-steps"></a>Nästa steg

När du har registrerat macOS-enheter kan du börja [hantera dem](../remote-actions/device-management.md).
