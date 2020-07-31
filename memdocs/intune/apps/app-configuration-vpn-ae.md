---
title: Konfigurera ett VPN eller ett per app-VPN för Android Enterprise-enheter i Microsoft Intune | Microsoft Docs
titleSuffix: Microsoft Intune
description: Använd en appkonfigurationsprincip när du ska lägga till eller skapa en VPN- eller per app-VPN-profil för Android Enterprise-enheter i Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/23/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7e869ad933e86d9330dbb8d6a26b1886a71cee07
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/28/2020
ms.locfileid: "87262905"
---
# <a name="use-a-vpn-and-per-app-vpn-policy-on-android-enterprise-devices-in-microsoft-intune"></a>Använd en VPN- och per app-VPN-princip på Android Enterprise-enheter i Microsoft Intune

Med virtuella privata nätverk (VPN) kan användarna få åtkomst till organisationens resurser via en fjärranslutning, från t. ex. hemmet, ett hotell, ett kafé eller något annat ställe. I Microsoft Intune kan du konfigurera VPN-klientappar på Android Enterprise-enheter med hjälp av en konfigurationsprincip för appar. Distribuera sedan den här principen med VPN-konfigurationen till enheter i din organisation.

Du kan också skapa VPN-principer som används av vissa appar. Den här funktionen kallas för per app-VPN. När appen är aktiv kan den ansluta till VPN-nätverket och få åtkomst till resurser via det virtuella privata nätverket. När appen inte är aktiv används inte VPN.

Den här funktionen gäller för:

- Android enterprise

Det finns två sätt att skapa appkonfigurationsprincipen för VPN-klientappen:

- Configuration Designer
- JSON-data

I den här artikeln visas hur du kan skapa en konfigurationsprincip för ett per app-VPN och en VPN-app med båda alternativen.

> [!NOTE]
> Många av VPN-klientkonfigurationssparametrarna liknar varandra. Men varje app har sina egna unika nycklar och alternativ. Kontakta din VPN-leverantör om du har några frågor.

## <a name="before-you-begin"></a>Innan du börjar

- Android utlöser inte automatiskt någon VPN-klientanslutning när en app öppnas. VPN-anslutningen måste startas manuellt. Du kan också starta anslutningen genom att använda [Always-on VPN](../configuration/vpn-settings-android-enterprise.md).

- Följande VPN-klienter stöder konfigurationsprinciperna för Intune-appar:

  - Cisco AnyConnect
  - Citrix SSO
  - F5 Access
  - Palo Alto Networks GlobalProtect
  - Pulse Secure
  - SonicWall Mobile Connect

- När du skapar VPN-principen i Intune väljer du olika nycklar som ska konfigureras. Dessa nyckelnamn varierar beroende på de olika VPN-klientappararna. Nyckelnamnen i din miljö kan alltså skilja sig från exemplen i den här artikeln.

- Konfigurationsdesignerdata och JSON-data kan använda certifikatbaserad autentisering. Om VPN-autentiseringen kräver klientcertifikat måste du skapa certifikatprofilerna innan du skapar VPN-principen. VPN-appkonfigurationsprinciperna använder värden från certifkatprofilerna.

  Android Enterprise-arbetsprofilenheterna stöder SCEP- och PKCS-certifikat. Fullständigt Android Enterprise-hanterade, dedikerade och företagsägda profilenheter stöder endast SCEP-certifikat. Mer information om certifikat finns i [Använda certifikat för autentisering i Microsoft Intune](../protect/certificates-configure.md).

## <a name="per-app-vpn-overview"></a>Översikt över per app-VPN

När du skapar och testar per app-VPN så inkluderar det grundläggande flödet följande steg:

1. Välj VPN-klientprogrammet. [Innan du börjar](#before-you-begin) (i den här artikeln) listar de appar som stöds.
2. Hämta programpakets-ID:na för de appar som ska använda VPN-anslutningen. [Hämta appakets-ID](#get-the-app-package-id) (i den här artikeln) visar hur du gör detta.
3. Om du använder certifikat för att autentisera VPN-anslutningen, så skapa och distribuera sedan certifikatprofilerna innan du distribuerar VPN-principen. Kontrollera att certifikatprofilerna distribueras korrekt. Mer information om certifikat finns i [Använda certifikat för autentisering i Microsoft Intune](../protect/certificates-configure.md).
4. Lägg till [VPN-klientprogrammet](apps-add-android-for-work.md) till Intune och distribuera appen till dina användare och enheter.
5. Skapa VPN-appkonfigurationsprincipen. Använd appakets-ID:na och certifikatsinformationen i principen.
6. Distribuera den nya VPN-principen.
7. Bekräfta att VPN-klientprogramvaran ansluter till VPN-servern.
8. När appen är aktiv bekräftar du att trafik från din app har genomförts via VPN.

## <a name="get-the-app-package-id"></a>Hämta appaketets ID

Hämta paket-ID:t för varje program som ska använda VPN. För allmänt tillgängliga program kan du hämta appakets-ID:t i Google Play-butiken. Den URL som visas för varje program inkluderar paket-ID.

I följande exempel är paket-ID:t för Microsoft Edge-webbläsarappen `com.microsoft.emmx`. Paket-ID:t ingår som en del av URL:en:

:::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-01.png" alt-text="Hämta appakets-ID:t i URL:en i Google Play-butiken.":::

För branschspecifika appar (LOB) hämtar du paket-ID:t från leverantören eller programutvecklaren.

## <a name="certificates"></a>Certifikat

Den här artikeln förutsätter att din VPN-anslutning använder certifikatbaserad autentisering. Det förutsätter också att du har distribuerat alla certifikat i kedjan som krävs för att klienter ska kunna autentisera sig. Den här certifikatkedjan innehåller vanligtvis klientcertifikatet, alla mellanliggande certifikat samt rotcertifikatet.

Mer information om certifikat finns i [Använda certifikat för autentisering i Microsoft Intune](../protect/certificates-configure.md).

När din certifikatprofil för klientautentisering distribueras skapas en certifikattoken i certifikatprofilen. Den här token används för att skapa VPN-appkonfigurationsprincipen.

Om du inte vet hur man skapar appkonfigurationsprinciper, så läs informationen i [Lägga till appkonfigurationsprinciper för hanterade Android Enterprise-enheter](app-configuration-policies-use-android.md).

## <a name="use-the-configuration-designer"></a>Använd Configuration Designer

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj **Appar** > **Appkonfigurationsprinciper** > **Lägg till** > **Hanterade enheter**.
3. Ange följande egenskaper i **Grundinställningar**:

    - **Namn**: Ange ett beskrivande namn på principen. Namnge dina principer så att du enkelt kan identifiera dem senare. Ett bra principnamn kan t. ex. vara **Appkonfigurationsprincip: Cisco AnyConnect VPN-princip för Android Enterprise-arbetsprofilsenheter**.
    - **Beskrivning**: Ange en beskrivning av principen. Denna inställning är valfri, men rekommenderas.
    - **Plattform**: Välj **Android Enterprise**.
    - **Profiltyp**: Alternativen är:
      - **Alla profiltyper**: Det här alternativet stöder autentisering med användarnamn och lösenord. Använd inte det här alternativet om du använder certifikatbaserad autentisering.
      - **Endast fullständigt hanterade, dedikerade och företagsägda arbetsprofilsenheter**: Det här alternativet har stöd för certifikatbaserad autentisering och autentisering med användarnamn och lösenord.
      - **Endast arbetsprofil**: Det här alternativet har stöd för certifikatbaserad autentisering och autentisering med användarnamn och lösenord.
    - **Målapp**: Välj den VPN-app som du lade till tidigare. I följande exempel används Cisco AnyConnect VPN-klientappen:

      :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-02.png" alt-text="Skapa en konfigurationsprincip för appar så att du kan konfigurera VPN eller per app-VPN i Microsoft Intune":::

4. Välj **Nästa**.
5. Ange följande egenskaper i **Inställningar**:

    - **Format för konfigurationsinställningar**: Välj **Använd Configuration Designer**:

      :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-03.png" alt-text="Skapa en VPN-princip för programkonfiguration i Microsoft Intune med hjälp av Configuration Designer-exempel.":::

    - **Lägg till**: Visar listan över konfigurationsnycklar. Välj alla konfigurationsnycklar du behöver för konfigurationen > **OK**.

      I följande exempel använder vi en minimal lista för AnyConnect VPN, inklusive certifikatbaserad autentisering och per app-VPN:
  
      :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-04.png" alt-text="Lägg till konfigurationsnycklar till en VPN-appskonfigurationsprincip i Microsoft Intune med hjälp av Configuration Designer-exempel.":::

    - **Konfigurationsvärde**: Ange värdena för de konfigurationsnycklar som du har valt. Kom ihåg att nyckelnamnen varierar beroende på vilken VPN-klient som du använder. I de nycklar som valts i vårt exempel:

      - **Per app-VPN-tillåtna appar**: Ange det eller de programpakets-ID:n som du samlade in tidigare. Exempel:

        :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-06.png" alt-text="Lägg till de tillåtna appakets-ID:na till en VPN-appskonfigurationsprincip i Microsoft Intune med hjälp av Configuration Designer-exempel.":::

      - **KeyChain-certifikatalias** (valfritt): Ändra **Värdetyp** från **sträng** till **certifikat**. Välj den klientcertifikatsprofil som ska användas med VPN-autentisering. Exempel:

        :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-07.png" alt-text="Ändra KeyChain-klientcertifikatets alias i en konfigurationsprincip för VPN-appar i Microsoft Intune med hjälp av Configuration Designer-exempel.":::

      - **Protokoll**: Välj **SSL**- eller **IPsec**-tunnelprotokoll för VPN.
      - **Anslutningens namn**: Ange ett användarvänligt namn för den här VPN-anslutningen. Användarna ser det här anslutningsnamnet på sina enheter. Ange till exempel `ContosoVPN`.
      - **Värd**: Ange värdnamnets URL till Headend-routern. Ange till exempel `vpn.contoso.com`.

        :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-05.png" alt-text="Exempel på protokoll, anslutningsnamn och värdnamn i en konfigurationsprincip för VPN-appar i Microsoft Intune som använder Configuration Designer":::

6. Välj **Nästa**.
7. Välj i **Tilldelningar** de grupper som ska tilldelas VPN-appskonfigurationsprincipen.

    Välj **Nästa**.

8. Granska inställningarna under **Granska + skapa**. När du väljer **Skapa** sparas dina ändringar och principen distribueras till dina grupper. Principen visas också i listan med appkonfigurationsprinciper.

    :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-08.png" alt-text="Granska appkonfigurationsprincipen med hjälp av Configuration Designer-flödet i Microsoft Intune-exemplet.":::

## <a name="use-json"></a>Använd JSON

Använd det här alternativet om du inte har, eller om du inte känner till alla nödvändiga VPN-inställningar som används i **Configuration Designer**. Om du behöver hjälp kan du kontakta din VPN-leverantör.

### <a name="get-the-certificate-token"></a>Hämta certifikatstoken

I de här stegen skapar du en tillfällig princip. Det går inte att spara principen. Avsikten är att kopiera certifikattoken. Du använder den här token när du skapar VPN-principen med JSON (nästa avsnitt).

1. I [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) väljer du **Appar** > **Appkonfigurationsprinciper** > **Lägg till** > **Hanterade enheter**.
2. Ange följande egenskaper i **Grundinställningar**:

    - **Namn**: Ange valfritt namn. Den här principen är temporär och kommer inte att sparas.
    - **Plattform**: Välj **Android Enterprise**.
    - **Profiltyp**: Välj **Endast arbetsprofil**.
    - **Målapp**: Välj den VPN-app som du lade till tidigare.

3. Välj **Nästa**.
4. Ange följande egenskaper i **Inställningar**:

    - **Format för konfigurationsinställningar**: Välj **Använd Configuration Designer**.
    - **Lägg till**: Visar listan över konfigurationsnycklar. Välj en nyckel med **värdetyp** för **sträng**. Välj **OK**.

      :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-11.png" alt-text="I Configuration Designer väljer du en nyckel av strängvärdestyp i Microsoft Intune VPN-appens konfigurationsprincip":::

5. Ändra **Värdetyp** från **sträng** till **certifikat**. I det här steget kan du välja rätt klientcertifikatsprofil som autentiserar VPN:

    :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-12.png" alt-text="Ändra anslutningsnamnet i en konfigurationsprincip för VPN-appar i Microsoft Intune-exemplet":::

6. Ändra omedelbart tillbaka **Värdetyp** till **sträng**. Observera att **Konfigurationsvärde** ändras till en token `{{cert:GUID}}`:

    :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-13.png" alt-text="Konfigurationsvärdet visar certifikatets token i en VPN-appskonfigurationsprincip i Microsoft Intune":::

7. Kopiera och klistra in den här certifikattoken i en annan fil, t. ex. en textredigerare.

8. Ta bort den här principen. Spara den inte. Det enda syftet är att kopiera och klistra in certifikattoken.

### <a name="create-the-vpn-policy-using-json"></a>Skapa VPN-principen med JSON

1. I [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) väljer du **Appar** > **Appkonfigurationsprinciper** > **Lägg till** > **Hanterade enheter**.

2. Ange följande egenskaper i **Grundinställningar**:

    - **Namn**: Ange ett beskrivande namn på principen. Namnge dina principer så att du enkelt kan identifiera dem senare. Ett bra principnamn kan t. ex. vara **Appkonfigurationsprincip: JSON Cisco AnyConnect VPN-princip för Android Enterprise-arbetsprofilsenheter i hela företaget**.
    - **Beskrivning**: Ange en beskrivning av principen. Denna inställning är valfri, men rekommenderas.
    - **Plattform**: Välj **Android Enterprise**.
    - **Profiltyp**: Alternativen är:
      - **Alla profiltyper**: Det här alternativet stöder autentisering med användarnamn och lösenord. Använd inte det här alternativet om du använder certifikatbaserad autentisering.
      - **Endast fullständigt hanterade, dedikerade och företagsägda arbetsprofilsenheter**: Det här alternativet har stöd för certifikatbaserad autentisering och autentisering med användarnamn och lösenord.
      - **Endast arbetsprofil**: Det här alternativet har stöd för certifikatbaserad autentisering och autentisering med användarnamn och lösenord.
    - **Målapp**: Välj den VPN-app som du lade till tidigare. 

3. Välj **Nästa**.
4. Ange följande egenskaper i **Inställningar**:

    - **Format för konfigurationsinställningar**: Välj **Ange JSON-data**. Du kan redigera JSON direkt.
    - **Ladda ned JSON-mall**: Använd det här alternativet när du ska ladda ned och uppdatera mallen i ett valfritt externt redigeringsprogram. Var försiktig med textredigeringsprogram som använder **typografiska citattecken**, eftersom de kan skapa ogiltig JSON.

    När du har angett de värden som krävs för konfigurationen tar du bort alla inställningar med `"STRING_VALUE"` eller `STRING_VALUE`.

    :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-14.png" alt-text="Exempel på hur du använder JSON-flödet – Redigera JSON.":::

5. Välj **Nästa**.
6. Välj i **Tilldelningar** de grupper som ska tilldelas VPN-appskonfigurationsprincipen.

    Välj **Nästa**.

7. Granska inställningarna under **Granska + skapa**. När du väljer **Skapa** sparas dina ändringar och principen distribueras till dina grupper. Principen visas också i listan med appkonfigurationsprinciper.

#### <a name="json-example-for-f5-access-vpn"></a>Exempel på JSON för F5 Access VPN

``` JSON
{
    "kind": "androidenterprise#managedConfiguration",
    "productId": "app:com.f5.edge.client_ics",
    "managedProperty": [
        {
            "key": "disallowUserConfig",
            "valueBool": false
        },
        {
            "key": "vpnConfigurations",
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "name",
                            "valueString": "MyCorpVPN"
                        },
                        {
                            "key": "server",
                            "valueString": "vpn.contoso.com"
                        },
                        {
                            "key": "weblogonMode",
                            "valueBool": false
                        },
                        {
                            "key": "fipsMode",
                            "valueBool": false
                        },
                        {
                            "key": "clientCertKeychainAlias",
                            "valueString": "{{cert:77333880-14e9-0aa0-9b2c-a1bc6b913829}}"
                        },
                        {
                            "key": "allowedApps",
                            "valueString": "com.microsoft.emmx"
                        },
                        {
                            "key": "mdmAssignedId",
                            "valueString": ""
                        },
                        {
                            "key": "mdmInstanceId",
                            "valueString": ""
                        },
                        {
                            "key": "mdmDeviceUniqueId",
                            "valueString": ""
                        },
                        {
                            "key": "mdmDeviceWifiMacAddress",
                            "valueString": ""
                        },
                        {
                            "key": "mdmDeviceSerialNumber",
                            "valueString": ""
                        },
                        {
                            "key": "allowBypass",
                            "valueBool": false
                        }
                    ]
                }
            ]
        }
    ]
}
```

## <a name="additional-information"></a>Ytterligare information

- [Lägga till konfigurationsprinciper för hanterade Android Enterprise-enheter](app-configuration-policies-use-android.md)
- [Inställningar för Android Enterprise-enhet för att konfigurera VPN i Intune](../configuration/vpn-settings-android-enterprise.md)

## <a name="next-steps"></a>Nästa steg

- [Skapa VPN-profiler för att ansluta till VPN-servrar i Intune](../configuration/vpn-settings-configure.md)
