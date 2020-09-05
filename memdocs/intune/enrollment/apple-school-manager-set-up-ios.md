---
title: Registrering av Apple School Manager-programmet för iOS/iPadOS-enheter
titleSuffix: Microsoft Intune
description: Lär dig hur du konfigurerar Apple School Manager-programmets registrering av företagsägda iOS/iPadOS-enheter med Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 4c35a23e-0c61-11e8-ba89-0ed5f89f718b
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 431dc3fec49609c4f163c9d7f471b60565611bc3
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/27/2020
ms.locfileid: "88992845"
---
# <a name="set-up-iosipados-device-enrollment-with-apple-school-manager"></a>Konfigurera registrering av iOS/iPadOS-enheter med Apple School Manager

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Du kan konfigurera Intune till att registrera iOS/iPadOS-enheter som köpts via [Apple School Manager](https://school.apple.com/)-programmet. Med hjälp av Intune med Apple School Manager kan du registrera många iOS/iPadOS-enheter utan att ens behöva röra dem. När en student eller en lärare sätter på enheten körs installationsassistenten med de konfigurerade inställningarna och enheten registreras i hanteringen.

Om du vill aktivera Apple School Manager-registrering använder du både Intune-portalen och Apple School Manager-portalen. En lista med serienummer eller inköpsordernummer krävs så att du kan tilldela enheter till Intune för hantering. Du kan skapa registreringsprofiler för Automated Device Enrollment (ADE) som innehåller inställningar som verkställs på enheterna under registreringen.

Apple School Manager-registrering kan inte användas med [automatisk enhetsregistrering](device-enrollment-program-enroll-ios.md) eller [enhetsregistreringshanteraren](device-enrollment-manager-enroll.md).

**Förutsättningar**
- [Push-certifikat för hantering av mobila enheter (MDM)](apple-mdm-push-certificate-get.md)
- [MDM-utfärdare](../fundamentals/mdm-authority-set.md)
- Om du använder ADFS kräver användartillhörighet [WS-Trust 1.3 användarnamn/kombinerad slutpunkt](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff608241(v=ws.10)). [Läs mer](/powershell/module/adfs/get-adfsendpoint?view=win10-ps).
- Enheter som köpts från programmet [Apple School Management](http://school.apple.com)

## <a name="get-an-apple-token-and-assign-devices"></a>Skaffa en Apple-token och tilldela enheter

Innan du kan registrera företagsägda iOS/iPadOS-enheter med Apple School Manager behöver du en tokenfil (.p7m) från Apple. Med denna token kan Intune synkronisera information om enheter som är anslutna till Apple School Manager. Intune kan även utföra överföringar av registreringsprofilen till Apple och tilldela enheter till dessa profiler. I Apples portal kan du också tilldela de enhetsserienummer som ska hanteras.

### <a name="step-1-download-the-intune-public-key-certificate-required-to-create-an-apple-token"></a>Steg 1. Ladda ned certifikatet för den offentliga Intune-nyckel som krävs för att skapa en Apple-token

1. I [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) väljer du **Enheter** > **iOS/iPadOS** > **iOS/iPadOS-registrering** > **Registreringsprogramtoken** > **Lägg till**.

   ![Hämta en registreringsprogramtoken.](./media/apple-school-manager-set-up-ios/image01.png)

2. På bladet **Token för registreringsprogram** väljer du **Ladda ned din offentliga nyckel** för att ladda ned och spara krypteringsnyckelfilen (.pem) lokalt. .pem-filen används för att begära ett förtroendecertifikat från Apple School Manager-portalen.
     ![Registreringsprogramtokenbladet.](./media/apple-school-manager-set-up-ios/image02.png)

### <a name="step-2-download-a-token-and-assign-devices"></a>Steg 2. Ladda ned en token och tilldela enheter
1. Välj **Skapa en token via Apple School Manager** och logga in på Apple School med ditt företags Apple-ID. Du kan använda detta Apple-ID när du behöver förnya din Apple School Manager-token.
2. I [Apple School Manager-portalen](https://school.apple.com) går du till **MDM-servrar** och väljer sedan **Lägg till MDM-server** (längst upp till höger).
3. Ange **MDM-serverns namn**. Servernamnet är för din egen referens och hjälper dig att identifiera MDM-servern (hantering av mobilenheter). Det är inte namnet eller URL-adressen för Microsoft Intune-servern.
   ![Skärmbild av Apple School Manager-portalen med serienummeralternativet markerat](./media/apple-school-manager-set-up-ios/asm-server-assignment.png)

4. Välj **Ladda upp fil...**  i Apples portal, bläddra till .pem-filen och välj **Spara MDM-server** (längst ned till höger).
5. Välj **Hämta token** och ladda ned servertokenfilen (.p7m) till datorn.
6. Gå till **Enhetstilldelningar** och **Välj enhet** med manuell inmatning av **Serienummer**, **Ordernummer** eller **Överför CSV-fil**.
     ![Skärmbild av Apple School Manager-portalen med serienummeralternativet markerat](./media/apple-school-manager-set-up-ios/asm-device-assignment.png)
7. Välj åtgärden **Tilldela till server** och välj den **MDM-server** som du skapade.
8. Ange alternativ för **Välj enheter** och ange sedan enhetsinformation.
9. Välj **Tilldela till server** och välj &lt;servernamnet&gt; som angetts för Microsoft Intune och sedan **OK**.

### <a name="step-3-save-the-apple-id-used-to-create-this-token"></a>Steg 3. Spara det Apple-ID som användes för att skapa den här token

I [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) anger du Apple-ID:t för framtida referens.

![Skärmbild av någon som anger det Apple-ID som användes för att skapa registreringsprogramtoken och bläddrat till denna token.](./media/apple-school-manager-set-up-ios/image03.png)

### <a name="step-4-upload-your-token"></a>Steg 4. Överför din token
I rutan **Apple-token**, bläddrar du till certifikatfilen (.pem), väljer **Öppna** och väljer sedan **Skapa**. Med pushcertifikatet kan Intune registrera och hantera iOS/iPadOS-enheter genom push-överföring av principer till registrerade mobila enheter. Intune synkroniserar automatiskt dina Apple School Manager-enheter från Apple.

## <a name="create-an-apple-enrollment-profile"></a>Skapa en Apple-registreringsprofil
Nu när du har installerat din token, kan du skapa en registreringsprofil för Apple School-enheter. En enhetsregistreringsprofil definierar inställningarna som tillämpas på en grupp av enheter vid registreringen.

1. I [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) väljer du **Enheter** > **iOS/iPadOS** > **iOS/iPadOS-registrering** > **Token för registreringsprogram**.
2. Välj en token, välj **Profiler** och välj sedan **Skapa profil**.

3. Under **Skapa profil**, anger du ett **Namn** och **Beskrivning** för profilen för administrationssyfte. Användarna kan inte se den här informationen. Du kan använda fältet **Namn** för att skapa en dynamisk grupp i Azure Active Directory. Använd profilnamnet för att definiera parametern enrollmentProfileName för att tilldela registreringsprofilen till enheter. Läs mer om [dynamiska Azure Active Directory-grupper](/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal#rules-for-devices).

    ![Profilnamn och beskrivning.](./media/apple-school-manager-set-up-ios/image05.png)

4. Ange om enheter med den här profilen måste registreras med eller utan en tilldelad användare under **Användartillhörighet**.
    - **Registrera med användartillhörighet** – välj det här alternativet för enheter som tillhör användare och som vill använda företagsportalen för tjänster som installation av appar. Det här alternativet låter också användare autentisera sina enheter med företagsportalen. Om du använder ADFS kräver användartillhörighet [WS-Trust 1.3 användarnamn/kombinerad slutpunkt](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff608241(v=ws.10)). [Läs mer](/powershell/module/adfs/get-adfsendpoint?view=win10-ps).   Det delade iPad-läget i Apple School Manager innebär att användarna måste registrera sig utan användartillhörighet.

    - **Registrera utan användartillhörighet** – välj det här alternativet för enheter som inte är kopplade till en enda användare, till exempel en delad enhet. Använd det här alternativet för enheter som utför uppgifter utan att komma åt lokala användardata. Appar som Företagsportal fungerar inte.

5. Om du väljer **Registrera med användartillhörighet**, kan du låta användare autentisera sig med företagsportalen istället för Apple Installationsassistenten.

    ![Autentisera med Företagsportalen.](./media/apple-school-manager-set-up-ios/authenticatewithcompanyportal.png)

    > [!NOTE]
    > Om du vill göra något av följande, ställer du in **Autentisera med Intune-företagsportalen istället för Apple Installationsassistenten** till **Ja**:
    >    - använda multifaktorautentisering
    >    - ge en uppmaning till användare som behöver ändra sina lösenord när de loggar in första gången
    >    - be användarna att återställa sina utgångna lösenord under registreringen.
    >
    > Dessa stöds inte vid autentisering med Apples installationsassistent.

6. Välj **Inställningar för enhetshantering** och välj om du vill att enheter som använder den här profilen ska övervakas.
    **Övervakade** enheter ger dig fler hanteringsalternativ och inaktiverar aktiveringslåset som standard. Microsoft rekommenderar att ADE används som mekanism för att aktivera övervakat läge i Intune, särskilt för organisationer som distribuerar större antal iOS-/iPadOS-enheter.

    Användare meddelas att deras enheter är övervakade på två sätt:

   - Låsskärmen säger: ”Denna iPhone hanteras av Contoso.”
   - Skärmen **Inställningar** > **Allmänt** > **Om** säger: ”Denna iPhone är övervakad. Contoso can monitor your Internet traffic and locate this device." (Denna iPhone är övervakad. Contoso kan övervaka din Internettrafik och hitta denna enhet.)

     > [!NOTE]
     > En enhet som registrerats utan övervakning kan bara återställas genom att använda Apple Configurator. Om du återställer enheten på det här sättet, måste du ansluta en iOS/iPadOS-enhet till en Mac-dator med en USB-kabel. Läs mer om detta i [dokumentation för Apple Configurator](http://help.apple.com/configurator/mac/2.3).

7. Välj om du vill ha låst registrering för enheter som använder den här profilen. **Låst registrering** inaktiverar iOS/iPadOS-inställningarna som tillåter att hanteringsprofilen tas bort från menyn **Inställningar**. När enhetsregistreringen är klar går det inte att ändra inställningen utan att göra en rensning av enheten. Sådana enheter måste ha hanteringsläget **Övervakad** inställt på *Ja*. 

8. Flera användare kan logga in på iPad-enheter som har registrerats med hjälp av ett hanterat Apple-ID. Det gör du genom att välja **Ja** under **Delad iPad** (det här alternativet kräver att **Registrera utan användartillhörighet** och **Övervakat** är inställda på **Ja**). Hanterade Apple-ID:n skapas i Apple School Manager-portalen. Läs mer om [Delad iPad](../fundamentals/education-settings-configure-ios-shared.md) och [Apples krav för delad iPad](https://help.apple.com/classroom/ipad/2.0/#/cad7e2e0cf56).

9. Välj om du vill att enheter som använder den här profilen ska kunna **Synkronisera med datorer**. **Neka alla** innebär att ingen av de enheter som använder den här profilen kan synkronisera med data på någon dator. Om du väljer **Tillåt Apple Configurator efter certifikat** måste du välja ett certifikat under **Apple Configurator-certifikat**.

10. Om du väljer **Tillåt Apple Configurator efter certifikat** i föregående steg, väljer du ett Apple Configurator-certifikat att importera.

11. Du kan ange ett namngivningsformat för enheter som tillämpas automatiskt när de registreras. För att göra detta anger du **Ja** under **Använd mall för enhetsnamn**. I rutan **Mall för enhetsnamn** anger du sedan den mall som ska användas för de namn som använder den här profilen. Du kan ange ett mallformat som innehåller enhetstyp och serienummer.

12. Välj **OK**.

13. Välj **Inställningar för inställningsassistenten** och konfigurera följande profilinställningar: ![Anpassning av installationsassistenten.](./media/apple-school-manager-set-up-ios/setupassistantcustom.png)


    |                 Inställningen                  |                                                                                               Beskrivning                                                                                               |
    |------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    |     <strong>Avdelningsnamn</strong>     |                                                             Visas när användare trycker på <strong>Om konfiguration</strong> vid aktiveringen.                                                              |
    |    <strong>Avdelningens telefonnummer</strong>     |                                                          Visas när användaren klickar på knappen <strong>Behöver hjälp</strong> vid aktiveringen.                                                          |
    | <strong>Alternativ för installationsassistenten</strong> |                                                     Följande valfria inställningar kan du ställa in senare på menyn <strong>Inställningar</strong> i iOS/iPadOS.                                                      |
    |        <strong>Lösenord</strong>         | Fråga efter lösenord under aktiveringen. Kräv alltid ett lösenord för osäkrade enheter om inte åtkomsten kontrolleras på något annat sätt (t.ex. helskärmsläge som begränsar enheten till en app). |
    |    <strong>Platstjänster</strong>    |                                                                 Om den här funktionen är aktiverad frågar installationsassistenten efter tjänsten under aktivering.                                                                  |
    |         <strong>Återställa</strong>         |                                                                Om den här funktionen är aktiverad frågar Installationsassistenten om iCloud-säkerhetskopiering vid aktivering.                                                                 |
    |   <strong>iCloud och Apple-ID</strong>   |                         Om det här alternativet är aktiverat, ber installationsassistenten användaren att logga in med ett Apple-ID och skärmen Appar och Data låter enheten återställas från iCloud-säkerhetskopiering.                         |
    |  <strong>Villkor</strong>   |                                                   Om det här alternativet är aktiverat, ber installationsassistenten användare att godkänna Apples villkor vid aktiveringen.                                                   |
    |        <strong>Touch ID</strong>         |                                                                 Om det här alternativet är aktiverat, frågar installationsassistenten efter den här tjänsten under aktivering.                                                                 |
    |        <strong>Apple Pay</strong>        |                                                                 Om det här alternativet är aktiverat, frågar installationsassistenten efter den här tjänsten under aktivering.                                                                 |
    |          <strong>Zoom</strong>           |                                                                 Om det här alternativet är aktiverat, frågar installationsassistenten efter den här tjänsten under aktivering.                                                                 |
    |          <strong>Siri</strong>           |                                                                 Om det här alternativet är aktiverat, frågar installationsassistenten efter den här tjänsten under aktivering.                                                                 |
    |     <strong>Diagnostikdata</strong>     |                                                                 Om det här alternativet är aktiverat, frågar installationsassistenten efter den här tjänsten under aktivering.                                                                 |


14. Välj **OK**.

15. Spara profilen genom att välja **Skapa**.

## <a name="connect-school-data-sync"></a>Ansluta School Data Sync
(Valfritt) Apple School Manager stöder synkronisering av klasslistdata till Azure Active Directory (AD) med hjälp av Microsoft SDS (School Data Sync). Du kan bara synkronisera en token med SDS. Om du ställer in en annan token med School Data Sync (SDS), kommer SDS att tas bort från den token som tidigare hade det. En ny anslutning ersätter den aktuella token. Utför följande steg om du vill använda SDS till att synkronisera skolans data.

1. I [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) väljer du **Enheter** > **iOS/iPadOS** > **iOS/iPadOS-registrering** > **Token för registreringsprogram**.
2. Välj en Apple School Manager-token och välj sedan **School Data Sync**.
3. Under **School Data Sync**, väljer du **Tillåt**. Den här inställningen innebär att Intune kan ansluta med SDS i Microsoft 365.
4. För att aktivera en anslutning mellan Apple School Manager och Azure AD väljer du **Ställ in Microsoft School Data Sync**. Lär dig mer om [hur du ställer in School Data Sync](https://support.office.com/article/Install-the-School-Data-Sync-Toolkit-8e27426c-8c46-416e-b0df-c29b5f3f62e1).
5. Klicka på **Spara** > **OK**.

## <a name="sync-managed-devices"></a>Synkronisera hanterade enheter

Efter det att Intune har tilldelats behörighet att hantera Apple School Manager-enheterna kan du synkronisera Intune med Apple-tjänsten och se dina hanterade enheter i Intune.

Gå till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) och välj **Enheter** > **iOS/iPadOS** > **iOS/iPadOS-registrering** > **Token för registreringsprogram** > välj en token i listan > **Enheter** > **Synkronisera**. ![Skärmbild på noden Registreringsprogramenheter och länken Synkronisera.](./media/device-enrollment-program-enroll-ios/image06.png)

För att följa Apples villkor för godkänd registreringsprogramtrafik tillämpar Intune följande begränsningar:
- En fullständig synkronisering kan inte köras oftare än en gång var sjunde dag. Vid en fullständig synkronisering uppdateras Intune med alla Apple-serienummer som tilldelats till Intune. Om du försöker köra en fullständig synkronisering inom sju dagar efter den föregående fullständiga synkroniseringen uppdaterar Intune endast serienummer som inte redan visas i Intune.
- Varje synkroniseringsbegäran har 15 minuter på sig att slutföras. Under den här tiden, eller tills begäran slutförts, är knappen **Synkronisera** inaktiverad.
- Intune synkroniserar nya och borttagna enheter med Apple var 24:e timme.

>[!NOTE]
>Du kan också tilldela Apple School Manager-serienummer till profiler från bladet **Registreringsprogramenheter**.

## <a name="assign-a-profile-to-devices"></a>Tilldela en profil till enheter
Apple School Manager-enheter som hanteras av Intune måste tilldelas en registreringsprogramprofil innan de registreras.

1. Gå till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) och välj **Enheter** > **iOS/iPadOS** > **iOS/iPadOS-registrering** > **Token för registreringsprogram** > och välj en token i listan.
2. Välj **Enheter** > välj enheter i listan > **Tilldela profil**.
3. Välj en profil för enheterna under **Tilldela profil** och välj sedan **Tilldela**.

## <a name="distribute-devices-to-users"></a>Distribuera enheter till användare

Du har aktiverat hantering och synkronisering mellan Apple och Intune och har tilldelat en profil så att dina Apple School-enheter kan registreras. Du kan nu distribuera enheter till användare. När en Apple School Manager-enhet i iOS/iPadOS aktiveras registreras den för hantering av Intune. Profiler kan inte tilldelas till aktiverade enheter som används för tillfället förrän enheten har rensats.