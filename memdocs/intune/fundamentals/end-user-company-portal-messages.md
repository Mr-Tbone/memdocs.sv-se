---
title: Meddelanden i företagsportalen som användare kan se på enheterna
titleSuffix: Microsoft Intune
description: Förstå de olika meddelanden som slutanvändarna kan se i företagsportalen.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 03/09/2017
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 3df993aa-48c5-4799-b68d-c85fe4f7b02c
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 91c79ae7ca7fc70c361fba0a7ad6becf8d035b5a
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79362777"
---
# <a name="help-end-users-understand-company-portal-app-messages"></a>Hjälpa slutanvändarna att förstå meddelanden i företagsportalappen

> [!NOTE]
> Följande information gäller endast på enheter med Android 6.0+ och iOS 10+.

Förstå de olika appmeddelanden som slutanvändarna kan se i företagsportalen. Dessa appmeddelanden visas vanligtvis vid olika tillfällen i registreringen. Läs om var meddelanden visas, vad de innebär och vad som händer om användarna nekar åtkomst. Läs dessutom hur du förklarar meddelandena för användarna på bästa sätt.

- __Tillåt att företagsportalen kan ringa och hantera telefonsamtal?__
- __Tillåt att företagsportalen kommer åt foton, media och filer på enheten?__

> [!NOTE]
> Vi säljer inte några data som samlas in av vår tjänst till någon tredje part av någon anledning.

## <a name="allow-company-portal-to-make-and-manage-phone-calls"></a>Tillåt att företagsportalen kan ringa och hantera telefonsamtal?

### <a name="where-it-appears"></a>Var det visas

Meddelandet är **Tillåt att företagsportalen kan ringa och hantera telefonsamtal?** och visas när användare trycker på **Registrera** i företagsportalen för första gången för att börja registrera sin enhet.

### <a name="what-it-means"></a>Betydelse

Genom att acceptera varningen kan användarna låta telefonnummer och IMEI-nummer för deras enhet skickas till tjänsten Intune. Dessa visas i administrationskonsolen på sidan __Maskinvara__.

> [!NOTE]
> **Företagsportalappen ringer eller hanterar aldrig telefonsamtal!** Meddelandetexten styrs av Google och kan inte ändras.

För att öppna sidan **Maskinvara** måste du gå till **Grupper** > **Alla mobila enheter** > **Enheter**. Välj användarens enhet och gå till **Visa egenskaper** > **Maskinvara**.

### <a name="what-happens-if-users-deny-access"></a>Vad händer om användarna nekar åtkomst

Om användarna nekar åtkomst kan de fortsätta att använda programmet för företagsportalen och registrera sina enheter. Enhetens telefonnummer och IMEI saknar data på sidan __Maskinvara__ i administrationskonsolen. Den andra gången användarna loggar in på företagsportalappen efter att de nekat åtkomst visas kryssrutan **Fråga inte igen** som de kan markera för att inte se meddelandet fler gånger.

Om användare först tillåter men senare nekar åtkomst, visas meddelandet nästa gång användaren loggar in på företagsportalappen efter registreringen.

Om användare senare bestämmer sig för att tillåta åtkomst kan de gå till **Inställningar** > **Appar** > **Företagsportal** > **Behörigheter** > **Telefon** och aktivera den.

### <a name="how-to-explain-this-to-your-users"></a>Så här förklarar du detta till dina användare

Hänvisa dina användare till [Registrera Android-enhet i Intune](../user-help/enroll-device-android-company-portal.md) för mer information.

## <a name="allow-company-portal-to-access-your-contacts"></a>Tillåta att företagsportalappen får åtkomst till dina kontakter?

### <a name="where-it-appears"></a>Var det visas

Meddelandet är **Allow Company Portal to access your contacts?** (Tillåt att företagsportalen får åtkomst till dina kontakter?) och visas när användare trycker på **Registrera** i företagsportalen för första gången för att börja registrera sin enhet.

### <a name="what-it-means"></a>Betydelse

Meddelandet uppmanar användarna att låta Intune skapa ett arbetskonto och hantera den Azure Active Directory-identitet som har registrerats för användaren på enheten.

> [!NOTE]
> **Microsoft bereder sig aldrig åtkomst till dina kontakter!** Meddelandetexten styrs av Google och kan inte ändras.

### <a name="what-happens-if-users-deny-access"></a>Vad händer om användarna nekar åtkomst

Om användarna nekar åtkomst kommer enheten inte att registreras i Intune och kan inte hanteras. Den andra gången användarna loggar in på företagsportalappen efter att de nekat åtkomst visas kryssrutan **Fråga inte igen** som de kan markera så att meddelandet inte visas igen.

Om användare tillåter men senare nekar åtkomst visas meddelandet nästa gång användaren loggar in på företagsportalappen efter registreringen.

Om användare senare bestämmer sig för att tillåta åtkomst kan de gå till **Inställningar** > **Appar** > **Företagsportal** > **Behörigheter** > **Telefon** och aktivera den.

### <a name="how-to-explain-this-to-your-users"></a>Så här förklarar du detta till dina användare

Hänvisa dina användare till [Registrera Android-enhet i Intune](../user-help/enroll-device-android-company-portal.md) för mer information.  

## <a name="allow-company-portal-to-access-photos-media-and-files-on-your-device"></a>Tillåt att företagsportalen kommer åt foton, media och filer på enheten?

### <a name="where-it-appears"></a>Var det visas

Meddelandet **Tillåt att företagsportalen kommer åt foton, media och filer på enheten?** visas när användarna trycker på **Skicka Data** för att skicka dataloggar till sin IT-administratör.

### <a name="what-it-means"></a>Betydelse

När användarna accepterar meddelandet kan deras enheter skriva dataloggar till enhetens SD-kort. Det innebär också att loggarna kan flyttas med hjälp av en USB-kabel.   

> [!NOTE]
> **Företagsportalappen bereder sig aldrig åtkomst till användarnas foton, media och filer!** Meddelandetexten styrs av Google och kan inte ändras.

### <a name="what-happens-if-users-deny-access"></a>Vad händer om användarna nekar åtkomst

Om användarna nekar åtkomst kan de fortfarande skicka loggar via e-post, men loggarna kopieras inte till enhetens SD-kort.

Den andra gången användarna loggar in på företagsportalappen efter att de nekat åtkomst visas kryssrutan **Fråga inte igen** som de kan markera så att meddelandet inte visas igen. Om användare tillåter men senare nekar åtkomst visas meddelandet nästa gång användaren försöker skicka loggar. Om användarna senare bestämmer sig för att tillåta åtkomst kan de gå till **Inställningar** > **Appar** > **Företagsportal** > **Behörigheter** > **Lagring** och aktivera behörigheten.


### <a name="how-to-explain-this-to-your-users"></a>Så här förklarar du detta till dina användare

Hänvisa dina användare till [Skicka loggar till IT-administratören via e-post](../user-help/send-logs-to-your-it-admin-by-email-android.md). 

## <a name="your-company-support-needs-to-give-you-access-to-company-resources"></a>Din företagssupport måste ge dig åtkomst till företagsresurser

### <a name="where-it-appears"></a>Var det visas

Om du inte har lagt till företagsportalappen i listan **Tillåtna appar** eller **Undanta appar** och en användare försöker logga in, så misslyckas inloggningen. Följande meddelande visas:

> **Your company support needs to give you access to company resources (Din företagssupport måste ge dig åtkomst till företagsresurser)**  
> Ditt företag skyddar din enhet med Windows Information Protection-principer. Din företagssupport måste se till att företagsportalen kan komma åt resurserna.

### <a name="what-it-means"></a>Betydelse

Lägg till appen Företagsportal i listan **Tillåtna appar** eller **Undanta appar** i WIP-appskyddsprincipen (Windows Information Protection). Mer information finns i [Skapa och distribuera en WIP-appskyddsprincip med Intune](../apps/windows-information-protection-policy-create.md).

## <a name="approve-a-iosipados-company-app-line-of-business-app-on-your-iosipados-device"></a>Godkänna en iOS/iPadOS-företagsapp (verksamhetsspecifik app) på din iOS/iPadOS-enhet 

### <a name="where-it-appears"></a>Var det visas

iOS-appar som har utvecklats av din organisation och som inte är tillgängliga i App Store är inte betrodda av din enhet som standard. När du installerar dessa appar med hjälp av företagsportalen och startar appen, visas följande meddelande:

![iOS-appmeddelande – Ej betrodd företagsutvecklare](./media/end-user-company-portal-messages/end-user-company-portal-messages-01.png)

### <a name="what-it-means"></a>Betydelse

Det här meddelandet innebär att du behöver ändra dina iOS/iPadOS-enhetsinställningar för att kunna godkänna och installera en app som har utvecklats av ditt företag på iOS/iPadOS-enheten.

När du installerar sådana appar med hjälp av företagsportalen och startar appen, följer du stegen nedan för att godkänna appen när du har hämtat den:

1. När du startar en installerad företagsapp (verksamhetsspecifik app), visas meddelandet ”Ej betrodd företagsutvecklare”. <br>
   Tryck på **Avbryt**.
2. Gå till **Inställningar** > **Allmänt** > **Enhetshantering**.

   ![iOS-enhetens användargränssnitt – Enhetshantering](./media/end-user-company-portal-messages/end-user-company-portal-messages-02.png)

3. Välj **Hanteringsprofil** > **Företagsapp**.
4. Välj utvecklarens namn.
5. Tryck på **Betrodd_utvecklares namn_** .
6. Bekräfta appen genom att välja **Förtroende** i appinstallationens popup-meddelande.

   ![iOS-enhetens användargränssnitt – Meddelande om betrodd app](./media/end-user-company-portal-messages/end-user-company-portal-messages-03.png)

    Du ska nu kunna starta och använda företagsappen.


## <a name="see-also"></a>Se även
[Vad du ska berätta för slutanvändare om att använda Intune](end-user-educate.md)
