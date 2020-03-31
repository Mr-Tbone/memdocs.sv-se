---
title: Registrering för Azure AD-anslutna hybridenheter – Windows Autopilot
titleSuffix: ''
description: Använd Windows Autopilot till att registrera Azure AD-anslutna hybridenheter i Microsoft Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/01/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 8518d8fa-a0de-449d-89b6-8a33fad7b3eb
ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 84d14943a37cf29a224c94364317d899b65ffef0
ms.sourcegitcommit: bbb63f69ff8a755a2f2d86f2ea0c5984ffda4970
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/18/2020
ms.locfileid: "79526334"
---
# <a name="deploy-hybrid-azure-ad-joined-devices-by-using-intune-and-windows-autopilot"></a>Distribuera Azure AD-anslutna hybridenheter med hjälp av Intune och Windows Autopilot
Du kan använda Intune och Windows Autopilot för att konfigurera Azure Active Directory-anslutna hybridenheter. Du gör det genom att följa stegen i den här artikeln.

## <a name="prerequisites"></a>Krav

Konfigurera [Azure AD-anslutna hybridenheterna](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan). [Verifiera enhetsregistreringen](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains#verify-the-registration) med hjälp av cmdleten Get-MsolDevice.

Enheter som ska registreras måste också:
- Köra Windows 10, v1809 eller senare.
- Ha åtkomst till internet [genom att följa de dokumenterade kraven för Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot-requirements#networking-requirements).
- Ha åtkomst till en Active Directory-domänkontrollant. Den måste vara ansluten till organisationens nätverk (Där den kan omvandla DNS-posterna för AD-domänen och AD-domänkontrollanten samt kommunicera med domänkontrollanten för att autentisera användaren. VPN-anslutning stöds inte för tillfället).
- Kunna pinga domänkontrollanten på den domän som du försöker ansluta till.
- Om du använder en proxy måste inställningsalternativet WPAD Proxy vara aktiverat och konfigurerat.
- Gå igenom välkomstupplevelsen (OOBE, Out-of-Box Experience).
- Använd en auktoriseringstyp som Azure Active Directory stöder i OOBE.


## <a name="set-up-windows-10-automatic-enrollment"></a>Konfigurera automatisk registrering i Windows 10

1. Logga in på Azure och välj **Azure Active Directory** i det vänstra fönstret.

   ![Azure Portal](./media/windows-autopilot-hybrid/auto-enroll-azure-main.png)

1. Välj **Mobility (MDM och MAM)** .

   ![Azure Active Directory-fönstret](./media/windows-autopilot-hybrid/auto-enroll-mdm.png)

1. Välj **Microsoft Intune**.

   ![Fönstret Mobility (MDM och MAM)](./media/windows-autopilot-hybrid/auto-enroll-intune.png)

1. Kontrollera att användarna som distribuerar Azure AD-anslutna enheter med Intune och Windows är medlemmar i en grupp som ingår i ditt **MDM-användaromfång**.

   ![Fönstret Konfigurera i Mobility (MDM och MAM)](./media/windows-autopilot-hybrid/auto-enroll-scope.png)

1. Använd värdena i rutorna **MDM-användarvillkor-URL**, **Webbadress till MDM-identifiering** och **MDM-kompatibilitets-URL** och välj sedan **Spara**.

## <a name="increase-the-computer-account-limit-in-the-organizational-unit"></a>Öka gränsen för datorkontot i organisationsenheten

Intune Connector för Active Directory skapar Autopilot-registrerade datorer i den lokala Active Directory-domänen. Värddatorn för Intune Connector måste ha behörighet att skapa datorobjekt i domänen. 

I vissa domäner beviljas inte datorer behörighet att skapa datorer. Domäner har dessutom en inbyggd gräns (10 som standard) som gäller för alla användare och datorer som inte har delegerad behörighet att skapa datorobjekt. Därför måste behörigheter delegeras till datorer som är värdar för Intune Connector på organisationsenheten där de Azure AD-anslutna hybridenheterna skapas.

Organisationsenheten som beviljas behörighet att skapa datorer måste matcha:
- Organisationsenheten som anges i domänanslutningsprofilen.
- Om ingen profil valts, datorns domännamn för din domän.

1. Öppna **Active Directory – användare och datorer (DSA.msc)** .

1. Högerklicka på den organisationsenhet som du ska använda för att skapa Azure AD-anslutna hybriddatorer och välj sedan **Delegera kontroll**.

    ![Kommandot för delegering av kontroll](./media/windows-autopilot-hybrid/delegate-control.png)

1. I guiden för **delegering av kontroll** väljer du **Nästa** > **Lägg till** > **Objekttyper**.

1. I fönstret **Objekttyper** markerar du kryssrutan **Datorer** och väljer sedan **OK**.

    ![Fönstret Objekttyper](./media/windows-autopilot-hybrid/object-types-computers.png)

1. I dialogrutan **Välj användare, datorer eller grupper** går du till rutan för att **ange de objektnamn som du vill välja** och anger namnet på datorn där anslutningsappen är installerad.

    ![Fönstret Välj användare, datorer eller grupper](./media/windows-autopilot-hybrid/enter-object-names.png)

1. Välj **Check Names** (Kontrollera namn) för att validera uppgiften och välj **OK**. Välj sedan **Next** (Nästa).

1. Välj **Skapa en anpassad aktivitet och delegera kontroll för den** > **Nästa**.

1. Markera kryssrutan **Endast följande objekt i mappen** och markera sedan kryssrutorna **Datorobjekt**, **Skapa valda objekt i den här mappen** och **Ta bort valda objekt i den här mappen**.

    ![Fönstret Objekttyp för Azure Active Directory](./media/windows-autopilot-hybrid/only-following-objects.png)
    
1. Välj **Nästa**.

1. Under **Behörigheter** markerar du kryssrutan **Fullständig kontroll**.  
    Den här åtgärden markerar alla de andra alternativen.

    ![Fönstret Behörigheter](./media/windows-autopilot-hybrid/full-control.png)

1. Välj **Nästa** och sedan **Slutför**.

## <a name="install-the-intune-connector"></a>Installera Intune Connector

Intune Connector för Active Directory måste installeras på en dator som kör Windows Server 2016 eller senare. Datorn måste också ha åtkomst till internet och din Active Directory. Om du vill öka skalningen och tillgängligheten eller om du vill ha stöd för flera Active Directory-domäner kan du installera flera anslutningsprogram i din miljö. Vi rekommenderar att du installerar anslutningsappen på en server som inte kör några andra Intune-anslutningsappar.

1. I [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) väljer du **Enheter** > **Windows** > **Windows-registrering** > **Intune Connector för Active Directory** > **Lägg till**. 
2. Följ anvisningarna för att ladda ned Connector.
3. Öppna den nedladdade konfigurationsfilen för anslutningsappen, *ODJConnectorBootstrapper.exe*, för att installera Connector.
4. Välj **Konfigurera** i slutet av konfigurationen.
5. Välj **Logga in.**
6. Ange autentiseringsuppgifter för rollen Global administratör eller Intune-administratör.  
   Användarkontot måste ha en tilldelad Intune-licens.
7. Gå till **Enheter** > **Windows** > **Windows-registrering** > **Intune Connector för Active Directory** och bekräfta sedan att anslutningsstatusen är **Aktiv**.

> [!NOTE]
> När du har loggat in i Connector kan det ta några minuter innan det visas i [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431). Det visas bara om den kan kommunicera med Intune-tjänsten.

### <a name="turn-off-ie-enhanced-security-configuration"></a>Aktivera förbättrad säkerhetskonfiguration i IE
Som standard har Windows Server förbättrad säkerhetskonfiguration i Internet Explorer aktiverat. Om du inte kan logga in på Intune Connector för Active Directory ska du inaktivera Förbättrad säkerhetskonfiguration i IE för administratören. [Så här inaktiverar du Förbättrad säkerhetskonfiguration i Internet Explorer](https://blogs.technet.microsoft.com/chenley/2011/03/10/how-to-turn-off-internet-explorer-enhanced-security-configuration)

### <a name="configure-web-proxy-settings"></a>Konfigurera webbproxyinställningar

Om du har en webbproxy i nätverksmiljön kontrollerar du att Intune Connector för Active Directory fungerar korrekt, i [Arbeta med befintliga lokala proxyservrar](autopilot-hybrid-connector-proxy.md).


## <a name="create-a-device-group"></a>Skapa en enhetsgrupp
1. I [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) väljer du **Grupper** > **Ny grupp**.

1. I fönstret **Grupp** gör du följande:

    a. I **Grupptyp** väljer du **Säkerhet**.

    b. Ange ett **gruppnamn** och en **gruppbeskrivning**.

    c. Välj en **medlemskapstyp**.

1. Om du har valt **Dynamiska enheter** som medlemskapstyp väljer du **Dynamiska enhetsmedlemmar** i fönstret **Grupp** och gör sedan något av följande i **Avancerad regel**:
    - Om du vill skapa en grupp som innehåller alla dina Autopilot-enheter anger du `(device.devicePhysicalIDs -any _ -contains "[ZTDId]")`.
    - Intunes grupptaggfält mappar till OrderID-attributet på Azure AD-enheter. Om du vill skapa en grupp som innehåller alla dina Autopilot-enheter med en viss grupptagg (OrderID) måste du ange: `(device.devicePhysicalIds -any _ -eq "[OrderID]:179887111881")`
    - Om du vill skapa en grupp som innehåller alla dina Autopilot-enheter med ett visst beställnings-ID anger du `(device.devicePhysicalIds -any _ -eq "[PurchaseOrderId]:76222342342")`.
    
1. Välj **Spara**.

1. Välj **Skapa**.  

## <a name="register-your-autopilot-devices"></a>Registrera dina Autopilot-enheter

Välj något av följande sätt för att registrera dina Autopilot-enheter.

### <a name="register-autopilot-devices-that-are-already-enrolled"></a>Registrera Autopilot-enheter som redan har registrerats

1. Skapa en Autopilot-distributionsprofil med **Omvandla alla målenheter till Autopilot** inställt till **Ja**. 
2. Tilldela profilen till en grupp som innehåller de medlemmar som du vill registrera automatiskt med Autopilot.

Mer information finns i [Skapa en Autopilot-distributionsprofil](enrollment-autopilot.md#create-an-autopilot-deployment-profile).

### <a name="register-autopilot-devices-that-arent-enrolled"></a>Registrera Autopilot-enheter som inte har registrerats

Om dina enheter inte har registrerats än kan du registrera dem själv. Mer information finns i [Lägg till enheter](enrollment-autopilot.md#add-devices).

### <a name="register-devices-from-an-oem"></a>Registrera enheter från en OEM-tillverkare

Om du köper nya enheter kan vissa OEM-tillverkare registrera enheterna åt dig. Mer information finns på [Windows Autopilot-sidan](https://aka.ms/WindowsAutopilot).

När Autopilot-enheter har *registrerats* (och innan de har registrerats i Intune) visas de på tre platser (med namn som motsvarar deras serienummer):
- Fönstret **Autopilot-enheter** i Intune i Azure Portal. Välj **Enhetsregistrering** > **Windows-registrering** > **Enheter**.
- Fönstret **Azure AD-enheter** i Intune i Azure Portal. Välj **Enheter** > **Azure AD-enheter**.
- Fönstret **Alla enheter i Azure Active Directory** i Azure Portal (**Enheter** > **Alla enheter**).

När Autopilot-enheterna har *registrerats* visas de på fyra platser:
- Fönstret **Autopilot-enheter** i Intune i Azure Portal. Välj **Enhetsregistrering** > **Windows-registrering** > **Enheter**.
- Fönstret **Azure AD-enheter** i Intune i Azure Portal. Välj **Enheter** > **Azure AD-enheter**.
- Fönstret **Alla enheter i Azure Active Directory** i Azure Portal. Välj **Enheter** > **Alla enheter**.
- Fönstret **Alla enheter** i Intune i Azure Portal. Välj **Enheter** > **Alla enheter**.

När Autopilot-enheterna har registrerats ändras deras enhetsnamn till värdnamnet för enheten. Som standard börjar värdnamnet med *DESKTOP-* .


## <a name="create-and-assign-an-autopilot-deployment-profile"></a>Skapa och tilldela en Autopilot-distributionsprofil
Autopilot-distributionsprofiler används för att konfigurera Autopilot-enheterna.

1. Gå till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), välj **Enheter** > **Windows** > **Windows-registrering** > **Distributionsprofiler** > **Skapa profil**.
2. På sidan **Grundinställningar** anger du ett **Namn** och en valfri **Beskrivning**.
3. Om du vill att alla enheter i de tilldelade grupperna automatiskt ska omvandlas till Autopilot väljer du **Ja** för **Omvandla alla målenheter till Autopilot**. Enheter som ägs av företaget och som inte är Autopilot-enheter i tilldelade grupper registreras med Autopilot-distributionstjänsten. Personligt ägda enheter kommer inte att konverteras till autopilot. Det kan ta upp till 48 timmar för registreringen att bearbetas. När enheten har avregistrerats och återställts registreras den av Autopilot. När en enhet har registrerats på det här sättet tas inte enheten bort från Autopilot-distributionstjänsten om det här alternativet inaktiveras eller om profiltilldelningen tas bort. Du måste i stället [ta bort enheten direkt](enrollment-autopilot.md#delete-autopilot-devices).
4. Välj **Nästa**.
5. På sidan **Välkomstupplevelse (OOBE)** för **Distributionsläge** väljer du **Användarbaserat**.
6. I rutan **Anslut till Azure AD som** väljer du **Hybrid Azure AD-ansluten**.
7. Konfigurera de återstående alternativen på sidan **Välkomstupplevelse (OOBE)** efter behov.
8. Välj **Nästa**.
9. På sidan **Omfångstaggar** väljer du [omfångstaggar](../fundamentals/scope-tags.md) för den här profilen.
10. Välj **Nästa**.
11. På sidan **Tilldelningar** väljer du **Välj grupper att ta med** > sök efter och välj enhetsgruppen > **Välj**.
12. Välj **Nästa** > **Skapa**.

Det tar ungefär 15 minuter innan enhetsprofilens status ändras från *Inte tilldelad* till *Tilldelar* och slutligen till *Tilldelad*.

## <a name="optional-turn-on-the-enrollment-status-page"></a>(Valfritt) Aktivera registreringsstatussidan

1. Gå till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), välj **Enheter** > **Windows** > **Windows-registrering** > **Sidan för registreringsstatus**.
1. I fönstret **Statussidan för registrering** väljer du **Standard** > **Inställningar**.
1. I rutan **Show app and profile installation progress** (Visa installationsförlopp för appar och profiler) väljer du **Yes** (Ja).
1. Konfigurera de andra alternativen efter behov.
1. Välj **Spara**.

## <a name="create-and-assign-a-domain-join-profile"></a>Skapa och tilldela en profil för domänanslutning

1. I administrationscentret för [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) väljer du **Enheter** > **Konfigurationsprofiler** > **Skapa profil**.
2. Ange följande egenskaper:
   - **Namn**: Ange ett beskrivande namn på den nya profilen.
   - **Beskrivning**: Ange en beskrivning av profilen.
   - **Plattform**: Välj **Windows 10 och senare**.
   - **Profiltyp**: Välj **Domänanslutning (förhandsversion)** .
3. Välj **Inställningar** och ange sedan **datornamnprefix**, **domännamn**.
4. (Valfritt) Ange en **organisationsenhet** (OU) i [DN-format](https://docs.microsoft.com/windows/desktop/ad/object-names-and-identities#distinguished-name). Alternativen är:
   - Ange en organisationsenhet där du har delegerat kontrollen till Windows 2016-enheten som kör Intune Connector.
   - Ange en organisationsenhet där du har delegerat kontrollen till rotdatorerna i din lokala Active Directory.
   - Om du lämnar detta tomt skapas datorobjektet i Active Directory-standardcontainern (CN=Computers om du inte [ändrade det](https://support.microsoft.com/en-us/help/324949/redirecting-the-users-and-computers-containers-in-active-directory-dom)).
   
   Här följer några giltiga exempel:
   - OU=Level 1,OU=Level2,DC=contoso,DC=com
   - OU=Mine,DC=contoso,DC=com
   
   Här följer några exempel som inte är giltiga:
   - CN=Computers,DC=contoso,DC=com (du kan inte ange en container; i stället lämnar du värdet tomt om du vill använda standardvärdet för domänen)
   - OU=Mine (du måste ange domänen via attributen för DC=)
     
   > [!NOTE]
   > Använd inte citattecken runt värdet i **Organisationsenhet**.
5. Välj **OK** > **Skapa**.  
    Profilen skapas och visas i listan.
6. Om du vill tilldela profilen följer du anvisningarna under [Tilldela en enhetsprofil](../configuration/device-profile-assign.md#assign-a-device-profile) och tilldelar profilen till samma grupp som används i det här steget [Skapa en enhetsgrupp](windows-autopilot-hybrid.md#create-a-device-group). Alternativt kan olika grupper användas om det finns behov av att ansluta enheter till olika domäner eller organisationsenheter.

> [!NOTE]
> Namngivningsfunktionerna för Windows Autopilot för Azure AD-hybridanslutning stöder inte variabler såsom %SERIAL%, och stöder endast prefix för datornamnet.

## <a name="next-steps"></a>Nästa steg

När du har konfigurerat Windows Autopilot rekommenderar vi att du går vidare och lär dig hur du hanterar dessa enheter. Mer information finns i [Vad är Microsoft Intune-enhetshantering?](../remote-actions/device-management.md).
