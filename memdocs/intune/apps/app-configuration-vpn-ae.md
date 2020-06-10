---
title: Konfigurera VPN för Android Enterprise-enheter
titleSuffix: Microsoft Intune
description: Använd en appskyddsprincip för att konfigurera VPN för Android Enterprise-enheter.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/01/2020
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
ms.openlocfilehash: bcb7bd506d92befa3c73faf7270de28765f5b192
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347424"
---
# <a name="configure-a-vpn-for-android-enterprise-devices"></a>Konfigurera VPN för Android Enterprise-enheter

I det här avsnittet beskrivs hur du skapar en appkonfigurationsprincip som kan distribueras tillsammans med en VPN-klient på Android Enterprise-enheter. Den här konfigurationen gör att nätverkstrafiken för utvalda program får åtkomst till företagsresurser.

> [!NOTE]
> Android-plattformen stöder för närvarande inte automatisk utlösning av en VPN-klientanslutning när något av de valda programmen öppnas. VPN-anslutningen måste först initieras manuellt, eller så kan du använda [VPN alltid på](../configuration/vpn-settings-android-enterprise.md).

Förhandskraven för att skapa en konfigurationsprincip som ger VPN-åtkomst inkluderar att den valda VPN-klienten har stöd för hanterade programkonfigurationsprofiler. VPN-klienter som har stöd för konfigurationsprincipen för Intune-appar omfattar för närvarande:
- Cisco AnyConnect
- Citrix SSO
- F5 Access
- Palo Alto Global Connect
- Pulse Secure
- SonicWall Mobile Connect

Om metoden för autentiserad åtkomst till VPN-slutpunkten kräver att klientcertifikat används måste certifikatprofilerna skapas i förväg för att få hjälp att fylla i de värden som krävs för appkonfigurationsprincipen.

> [!NOTE]
> Även om scenarier för Android Enterprise-arbetsprofiler stöder både SCEP- och PKCS-certifikat, stöder Android Enterprise-enhetsägarscenarier endast SCEP-certifikat. 

Det grundläggande flödet för att skapa och testa VPN-profilen per app är följande:
1.  Välj lämpligt VPN-klientprogram för din infrastruktur.
2.  Identifiera programpaket-ID:na för de produktivitetsprogram som du vill använda med VPN-anslutningen.
3.  Distribuera eventuella certifikatprofiler som krävs för att uppfylla kraven på autentisering för VPN-anslutningen. Kontrollera att distributionen lyckades.
4.  Distribuera VPN-klientprogrammet.
5.  Förbered den appkonfigurationsbaserade VPN-profilen med hjälp av informationen som samlats in under tidigare steg.
6.  Distribuera den nyligen skapade VPN-profilen.
7.  Verifiera att VPN-klientappen ansluter till din VPN-serverinfrastruktur.
8.  Verifiera att trafiken från dina valda produktivitetsappar överför VPN-nätverket när det är aktivt.

## <a name="get-the-app-package-id"></a>Hämta appaketets ID

Identifiera paket-ID för varje program som du vill ge VPN-åtkomst till. För allmänt tillgängliga program kan du fundera på att hämta paket-ID:n för vart och ett av programmen i Google Play Butik. Den URL som visas för varje program inkluderar paket-ID. Paket-ID för Android-versionen av Microsoft Edge-webbläsaren är till exempel `com.microsoft.emmx`. Paket-ID ingår som en del av URL:en.

![Ett exempel på hur du hittar programpaket-ID:t.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-01.png)

När det gäller verksamhetsspecifika appar kan du be leverantören eller programutvecklingsteamet att tillhandahålla relevant paket-ID.

## <a name="certificates"></a>Certifikat

I det här avsnittet förutsätter vi att din VPN-anslutning kommer att använda certifikatbaserad autentisering och att du har distribuerat alla certifikat i kedjan som krävs för att klientautentisering ska fungera. Detta är vanligtvis klientcertifikatet, alla mellanliggande certifikat samt rotcertifikatet.
Om du vill ha mer information om certifikatdistribution för Android Enterprise kan du börja med avsnittet [Använda certifikat för autentisering i Microsoft Intune](../protect/certificates-configure.md).

När din certifikatprofil för klientautentisering har distribuerats behöver du viss information om profilen för att skapa konfigurationsprincipen för VPN-appen.
Om du inte vet hur du skapar konfigurationsprofiler för appar går du till avsnittet [Lägga till appkonfigurationsprinciper för hanterade Android Enterprise-enheter](../apps/app-configuration-policies-use-android.md).
 

## <a name="build-the-vpn-profile"></a>Skapa VPN-profilen

Det finns två sätt att skapa appkonfigurationsprincipen för VPN-appen. Du kan använda **Configuration Designer** eller alternativet **JSON-data**. Alternativet **JSON-data** krävs om inte alla nödvändiga VPN-inställningar är tillgängliga i **Configuration Designer**-metoden. Kontakta VPN-leverantören om du anser att JSON-alternativet krävs för support. I det här avsnittet visas exempel på båda metoderna. I båda metoderna **JSON-data** och **Configuration Designer** kan du lägga till certifikatbaserad autentisering. När du använder metoden **JSON-data** kan du börja genom att använda **Configuration Designer** för att extrahera de nödvändiga profilvärdena.

> [!NOTE]
> Även om många av konfigurationsparametrarna för VPN-klienten är likartade, har varje app sina unika nycklar och alternativ. Kontakta din VPN-leverantör om det uppstår några frågor. 

## <a name="use-the-configuration-designer-flow"></a>Använda Configuration Designer-flödet

1.  Börja med att lägga till en ny appkonfigurationsprincip för **Hanterade enheter**.
2.  Ange ett lämpligt namn.
3.  Välj **Android Enterprise** som plattform.
4.  Välj antingen **Endast arbetsprofil** eller **Endast enhetens ägare** som profiltyp om certifikatbaserad autentisering krävs. **Profilen för arbetsägare och enhetsägare** är inte kompatibel med certifikatbaserad autentisering.
5.  För målprogrammet väljer du den VPN-klient som du har distribuerat. I det här exemplet använder vi den tidigare distribuerade VPN-klienten Cisco AnyConnect

  ![Exempel på hur du skapar en appkonfigurationsprincip – Grunderna.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-02.png)

6. På nästa sida använder du listrutan Konfigurationsinställningar och väljer alternativet **Använd Configuration Designer**.

  ![Exempel på hur du använder Configuration Designer-flödet – Inställningar.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-03.png)

7. Klicka på **Lägg till** för att ta fram listan över konfigurationsnycklar.
8.  Välj alla konfigurationsnycklar du behöver för den valda konfigurationen. I det här exemplet använder vi en minimal lista att ange för en AnyConnect VPN, inklusive certifikatbaserad autentisering och per app-VPN.
  
  <img alt="Example of using the Configuration Designer Flow - Configuration keys." src="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-04.png" width="350">

9. Ange lämpliga värden för nycklarna **Anslutningsnamn**, **Värd** och **Protokoll**.

  ![Exempel på hur du använder Configuration Designer-flödet – Val av konfigurationsnyckel.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-05.png)  

  > [!NOTE]
  > Namnen på dessa nycklar kan variera beroende på vilket VPN-klientprogram som du skapar principen för.

10. Ange det/de programpaket-ID som du samlade in tidigare i nyckeln **Tillåtna appar för per app VPN**.

  ![Exempel på hur du använder Configuration Designer-flödet – Programpaket-ID:n.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-06.png)  

11. I nyckeln **Nyckelringscertifikatets alias** (valfritt) växlar du **Värdetyp** från **sträng** till **certifikat**. Detta gör att du kan välja rätt klientcertifikatprofil som ska användas med VPN-autentisering.

  ![Exempel på hur du använder Configuration Designer-flödet – Uppdatera nyckelringscertifikatets alias.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-07.png)  

12. På nästa sida väljer du lämpliga omfångstaggar.
13. På nästa sida anger du lämpliga grupper som du vill distribuera appkonfigurationsprincipen till.
14. Välj **Skapa** för att skapa och distribuera principen.

  ![Exempel på hur du använder Configuration Designer-flödet – Granska.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-08.png)  

## <a name="use-the-json-flow"></a>Använda JSON-flödet

Skapa en tillfällig profil:
1.  Börja med att lägga till en ny appkonfigurationsprincip för **Hanterade enheter**.
2.  Ange ett lämpligt namn (användningen av den här profilen är tillfällig eftersom den INTE kommer att sparas).
3.  Välj **Android Enterprise** som plattform.
4.  För målprogrammet väljer du den VPN-klient som du har distribuerat.
5.  Välj antingen **Endast arbetsprofil** eller **Endast enhetens ägare** som profiltyp om certifikatbaserad autentisering krävs. **Profilen för arbetsägare och enhetsägare** är inte kompatibel med certifikatbaserad autentisering.

  ![Exempel på hur du använder JSON-flödet – Grunderna.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-09.png)  

6.  På nästa sida använder du listrutan **Konfigurationsinställningar** och väljer alternativet **Använd Configuration Designer**.

  ![Exempel på hur du använder JSON-flödet – Format för konfigurationsinställningar.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-10.png)  

7.  Klicka på **Lägg till** för att ta fram listan över konfigurationsnycklar.
8.  Välj någon av nycklarna med **värdetypen** **sträng** och klicka på **OK**.

  <img alt="Example of using the JSON Flow - Select a key." src="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-11.png" width="350">

9.  Ändra nu **Värdetyp** från **sträng** till **certifikat**. Detta gör att du kan välja rätt klientcertifikatprofil som ska användas med VPN-autentisering.

  ![Exempel på hur du använder JSON-flödet – Anslutningsnamn.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-12.png)  

10. Ändra omedelbart tillbaka **Värdetyp** till **sträng**. Observera att **Konfigurationsvärde** ändras till en token i formatet `{{cert:GUID}}`.
11. Välj och kopiera certifikatets tokenrepresentation till en annan plats, till exempel en textredigerare.

  ![Exempel på hur du använder JSON-flödet – konfigurationsvärde.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-13.png)  

12. Ta bort profilen som skapas – det enda syftet med föregående steg var att fastställa certifikatets token.

### <a name="create-the-vpn-profile"></a>Skapa VPN-profilen

1.  Börja med att lägga till en ny appkonfigurationsprofil för **Hanterade enheter**.
2.  Ange ett lämpligt namn.
3.  Välj **Android Enterprise** som plattform.
4.  För målprogrammet väljer du den VPN-klient som du har distribuerat.
5.  Välj antingen **Endast arbetsprofil** eller **Endast enhetens ägare** som profiltyp om certifikatbaserad autentisering krävs. **Profilen för arbetsägare och enhetsägare** är inte kompatibel med certifikatbaserad autentisering.
6.  Använd listrutan **Konfigurationsinställningar** och välj alternativet **Ange JSON-data**.
7.  Du kan redigera JSON direkt eller, om du vill, använda knappen **Ladda ned JSON-mall** för att ladda ned och sedan ändra mallen i en valfri extern redigerare. Var försiktig med textredigerare som har alternativet att använda **Typografiska citattecken**, eftersom de skulle resultera i att JSON blir ogiltig.

  ![Exempel på hur du använder JSON-flödet – Redigera JSON.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-14.png)  

8.  Oavsett vilken metod du använder måste du ta bort alla återstående inställningar med värdet "STRING_VALUE" eller STRING_VALUE i hela JSON när du har fyllt i de värden som krävs för den önskade konfigurationen.

#### <a name="example-json-for-f5-access-vpn"></a>Exempel på JSON för F5 Access VPN

Följande är ett exempel på JSON-data för F5 Access VPN.

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

## <a name="summary"></a>Sammanfattning

Med hjälp av en appkonfigurationsprincip för Android Enterprise kan du med registrerade enheter utnyttja VPN-beteende per app trots att det inte finns direkt stöd för det på plattformen. 

## <a name="additional-information"></a>Ytterligare information

Relaterad information finns i följande avsnitt:
- [Lägga till konfigurationsprinciper för hanterade Android Enterprise-enheter](../apps/app-configuration-policies-use-android.md)
- [Inställningar för Android Enterprise-enhet för att konfigurera VPN i Intune](../configuration/vpn-settings-android-enterprise.md)

## <a name="next-steps"></a>Nästa steg

- [Skapa VPN-profiler för att ansluta till VPN-servrar i Intune](../configuration/vpn-settings-configure.md)
