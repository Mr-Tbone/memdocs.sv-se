---
title: Konfigurationsprinciper för hanterade appar utan enhetsregistrering
titleSuffix: Microsoft Intune
description: Läs om hur du konfigurerar principer för hanterade appar utan enhetsregistrering.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: E61C1618-79D0-41A1-B61F-4123FB6672FC
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 20b5b3de16023ac475cc41a633e5d3ab915a1bd0
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88910731"
---
# <a name="add-app-configuration-policies-for-managed-apps-without-device-enrollment"></a>Lägg till appkonfigurationsprinciper för hanterade appar utan enhetsregistrering

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Du kan använda appkonfigurationsprinciper med hanterade appar som har stöd för Intune App SDK på enheter som inte har registrerats. 

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj **Appar** > **Appkonfigurationsprinciper** > **Lägg till** > **Hanterade appar**.
3. Ange följande information på sidan **Grundläggande**:
    - **Namn**: Namnet på den profil som visas i Azure Portal.
    - **Beskrivning**: Beskrivning av den profil som visas i Azure Portal.
    - **Enhetsregistreringstyp**: Hanterade appar har valts.
4. Välj den app du vill konfigurera genom att välja **Välj offentliga appar** eller **Välj anpassade appar**. Välj appen i listan över appar som du har godkänt och synkroniserat med Intune.
5. Visa sidan **Inställningar** genom att klicka på **Nästa**.
6. På sidan **Inställningar** visas alternativ som varierar beroende på vilken app du konfigurerar:

    - **Allmänna konfigurationsinställningar** – Ange **Namn** och **Värde** för varje allmän konfigurationsinställning som stöds av appen. 
 
        Intune App SDK-aktiverade appar har stöd för konfigurationer i nyckel/värde-par. Läs dokumentationen för varje app om du vill lära dig mer om vilka nyckel/värde-konfigurationer som stöds. Observera att du kan använda token som fylls i dynamiskt med data som skapas av programmet. Välj ellipsen ( **...** ) och sedan **Ta bort** om du vill ta bort en allmän konfigurationsinställning. Mer information finns i [Konfigurationsvärden för att använda token](app-configuration-policies-managed-app.md#configuration-values-for-using-tokens). 

    - **Konfigurationsinställningar för Outlook** – I Outlook för iOS och Android kan administratörer anpassa standardkonfigurationen för flera inställningar i appen. Mer information finns i [Outlook för iOS och Android – Allmänna scenarier för appkonfiguration](/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune#general-app-configuration-scenarios).
   
    - **S/MIME** – S/MIME (Secure Multipurpose Internet Mail Extensions) är en specifikation som gör att användarna kan skicka och ta emot digitalt signerad och krypterad e-post.
        - **Aktivera S/MIME** – Ange om S/MIME-kontroller ska aktiveras när du skriver e-post. Standardvärde: **Inte konfigurerat**.
        - **Tillåt att användaren ändrar inställningen** – Ange om användaren får ändra inställningen. S/MIME måste vara aktiverat. Standardvärde: **Ja**.
        
    Mer information om Outlook-policyinställningar för appkonfiguration finns i [Distriburera appkonfigurationsinställningar för Outlook för iOS och Android](/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune).

7. Klicka på **Nästa** för att visa sidan **Tilldelningar**.
8. Klicka på **Välj de grupper som ska inkluderas**.
9. Välj en grupp i rutan **Välj grupper att inkludera** och klicka på **Välj**.
10. Klicka på **Välj grupper att utesluta** för att visa det relaterade fönstret.
11. Välj de grupper som du vill exkludera och klicka sedan på **Välj**.

    >[!NOTE]
    >Om någon annan grupp redan har inkluderats för en viss tilldelning när du lägger till en grupp så blir den förvald och kan inte ändras för andra tilldelningstyper för inkludering. Gruppen som har använts kan därför inte användas som en undantagen grupp.

12. Visa sidan **Granska och skapa** genom att klicka på **Nästa**.
13. Klicka på **Skapa** för att lägga till konfigurationsprincipen i Intune.

## <a name="configuration-values-for-using-tokens"></a>Konfigurationsvärden för att använda token

Intune kan generera vissa token och skicka dem till det hanterade programmet. Om din appkonfiguration kan använda en e-postinställning så kan du lägga till en dynamisk e-postadress med hjälp av en token. Ange det namn som förväntas av appen i fältet **Namn** och ange sedan `{{mail}}` i fältet **Värde**.

Intune stöder följande typer av token i konfigurationsinställningarna. Andra anpassade nyckel/värde-par stöds inte.

- \{\{userprincipalname\}\} – till exempel John@contoso.com
- \{\{mail\}\} – till exempel John@contoso.com
- \{\{partialupn\}\} – till exempel John
- \{\{accountid\}\} – till exempel fc0dc142-71d8-4b12-bbea-bae2a8514c81
- \{\{userid\}\} – till exempel 3ec2c00f-b125-4519-acf0-302ac3761822
- \{\{username\}\} – till exempel Johan Danielsson
- \{\{PrimarySMTPAddress\}\} – till exempel testuser@ad.domain.com

> [!Note]  
> Tecknen \{\{ och \}\} används endast av tokentyper och får inte användas för andra ändamål.

## <a name="next-steps"></a>Nästa steg

Fortsätt sedan med att [tilldela](apps-deploy.md) och [övervaka](apps-monitor.md) appen som vanligt.