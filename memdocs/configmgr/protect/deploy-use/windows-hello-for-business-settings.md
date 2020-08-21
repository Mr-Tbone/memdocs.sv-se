---
title: Windows Hello för företag-inställningar
titleSuffix: Configuration Manager
description: Lär dig att integrera Windows Hello för företag med Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a95bc292-af10-4beb-ab56-2a815fc69304
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4c8029cdda80d327cbed2a4c60c71ff1811e4723
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88698705"
---
# <a name="windows-hello-for-business-settings-in-configuration-manager"></a>Inställningar för Windows Hello för företag i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

<!--1245704-->
Configuration Manager integreras med Windows Hello för företag. (Den här funktionen kallades tidigare Microsoft Passport for Work.) Windows Hello för företag är en alternativ inloggnings metod för Windows 10-enheter. Det använder Active Directory eller ett Azure Active Directory (Azure AD)-konto för att ersätta ett lösen ord, smartkort eller virtuellt smartkort. Med Hello för företag kan du använda en *användar-gest* för att logga in i stället för ett lösen ord. En användar-gest kan vara en PIN-kod, bio metrisk autentisering eller en extern enhet, till exempel en finger avtrycks läsare.

> [!Important]  
> Från och med version 1910 stöds inte certifikatbaserad autentisering med Windows Hello för företag-inställningar i Configuration Manager. Mer information finns i [föråldrade funktioner](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md). Nyckelbaserad autentisering är fortfarande giltigt.
>
> Distribution av Active Directory Federation Services (AD FS) registrerings utfärdare (ADFS RA) är enklare, ger en bättre användar upplevelse och har en mer deterministisk certifikat registrerings upplevelse. Använd ADFS RA för certifikatbaserad autentisering med Windows Hello för företag.
>
> Överväg att flytta [arbets belastningen för **resurs åtkomst principer** ](../../comanage/workloads.md#resource-access-policies) till Intune för samhanterade enheter. Använd sedan Intune-principer för att hantera dessa certifikat. Mer information finns i [så här växlar du arbets belastningar](../../comanage/how-to-switch-workloads.md).

Mer information finns i [Windows Hello för företag](/windows/security/identity-protection/hello-for-business/hello-identity-verification).

> [!Note]  
> Configuration Manager aktiverar inte den här valfria funktionen som standard. Du måste aktivera den här funktionen innan du använder den. Mer information finns i avsnittet [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

Configuration Manager integreras med Windows Hello för företag på följande sätt:  

- Styr vilka gester användare kan och inte kan använda för att logga in.  

- Lagra certifikat för autentisering i Windows Hello för Business Key Storage-providern (KSP). Mer information finns i [certifikat profiler](introduction-to-certificate-profiles.md).  

- Skapa och distribuera en Windows Hello för företag-profil för att kontrol lera inställningarna på domänanslutna Windows 10-enheter som kör Configuration Manager-klienten. Från och med version 1910 kan du inte använda certifikatbaserad autentisering. När du använder nyckelbaserad autentisering behöver du inte distribuera en certifikat profil.

## <a name="configure-a-profile"></a>Konfigurera en profil  

1. Gå till arbets ytan **till gångar och efterlevnad** i Configuration Manager-konsolen. Expandera **kompatibilitetsinställningar, expandera** **åtkomst till företags resurser**och välj noden **Windows Hello för företag-profiler** .

1. I menyfliksområdet väljer du **skapa Windows Hello för företag-profil** för att starta profil guiden.

1. På sidan **Allmänt** anger du ett namn och en valfri beskrivning för profilen.

1. På sidan **plattformar som stöds** väljer du de OS-versioner som profilen ska tillämpas på.

1. Konfigurera följande inställningar på sidan **Inställningar** :

    - **Konfigurera Windows Hello för företag**: Ange om den här profilen aktiverar, inaktiverar eller inte konfigurerar Hello för företag.

    - **Använda en Trusted Platform Module (TPM)**: en TPM ger ytterligare ett lager med data säkerhet. Välj ett av följande värden:  

      - **Obligatoriskt**: endast enheter med en tillgänglig TPM kan etablera Windows Hello för företag.  

      - **Föredra**: enheterna försöker först använda TPM. Om den inte är tillgänglig kan de använda program varu kryptering.

    - **Autentiseringsmetod**: Ange det här alternativet som **inte konfigurerat** eller **nyckelbaserad**.

        > [!NOTE]
        > Från och med version 1910 stöds inte certifikatbaserad autentisering med Windows Hello för företag-inställningar i Configuration Manager.

    - **Konfigurera minsta längd på PIN-kod**: om du vill kräva en minimilängd för användarens PIN-kod aktiverar du det här alternativet och anger ett värde. När det är aktiverat är standardvärdet `4` .

    - **Konfigurera maximal längd för PIN-kod**: om du vill kräva en maximal längd för användarens PIN-kod aktiverar du det här alternativet och anger ett värde. När aktive rad är standardvärdet `127` .

    - **Kräv förfallo datum för PIN-kod (dagar)**: anger antalet dagar innan användaren måste ändra PIN-koden för enheten.

    - **Förhindra åter användning av tidigare PIN-märken**: Tillåt inte att användare använder PIN-filerna som de tidigare har använt.

    - **Kräv versaler i PIN-kod**: anger om användarna måste inkludera versaler i PIN-koden för Windows Hello för företag. Välj mellan:  

      - **Tillåts**: användare kan använda versaler i sina PIN-koder, men behöver inte.

      - **Krävs**: användarna måste inkludera minst en versal i sina PIN-koder.  

      - **Tillåts inte**: användarna får inte använda versaler i sina PIN-koder.  

    - **Kräv gemener i PIN-kod**: anger om användarna måste innehålla gemener i PIN-koden för Windows Hello för företag. Välj mellan:  

      - **Tillåts**: användare kan använda gemener i sina PIN-koder, men behöver inte.

      - **Krävs**: användarna måste inkludera minst en gemen i sina PIN-koder.  

      - **Tillåts inte**: användarna får inte använda gemener i sina PIN-koder.  

    - **Konfigurera specialtecken**: anger användningen av specialtecken i PIN-koden. Välj mellan:  

        > [!NOTE]
        > Specialtecken innehåller följande uppsättning:
        >
        > ``` characters
        > ! " # $ % & ' ( ) * + , - . / : ; < = > ? @ [ \ ] ^ _ ` { | } ~
        > ```

      - **Tillåts**: användare kan använda specialtecken i sina PIN-koder, men behöver inte.  

      - **Krävs**: användarna måste inkludera minst ett specialtecken i sina PIN-koder.  

      - **Tillåts inte**: användarna får inte använda specialtecken i sina PIN-koder. Det här beteendet är även om inställningen **inte har kon figurer ATS**.  

    - **Konfigurera användning av siffror i PIN-kod**: anger användningen av siffror i PIN-koden. Välj mellan:

      - **Tillåts**: användare kan använda siffror i sina PIN-koder, men behöver inte.  

      - **Krävs**: användarna måste inkludera minst ett nummer i sina PIN-koder.  

      - **Tillåts inte**: användarna kan inte använda siffror i sina PIN-koder.

    - **Aktivera bio metriska gester**: Använd bio metrisk autentisering, t. ex. ansikts igenkänning eller finger avtryck. Dessa lägen är ett alternativ till en PIN-kod för Windows Hello för företag. Användare kan fortfarande konfigurera en PIN-kod i händelse av att bio metrisk autentisering Miss lyckas.  

      Om värdet är **Ja**tillåter Windows Hello för företag bio metrisk autentisering. Om värdet är **Nej**förhindrar Windows Hello för företag bio metrisk autentisering för alla konto typer.  

    - **Använd utökat skydd mot förfalskning**: konfigurerar utökat skydd mot förfalskning på enheter som har stöd för det. Om det är inställt på **Ja**, där det finns stöd för, kräver Windows att alla användare använder skydd mot förfalskning för ansikts funktioner.  

    - **Använd telefonin loggning**: konfigurerar tvåfaktorautentisering med en mobil telefon.

1. Slutför guiden.

Följande skärm bild är ett exempel på profil inställningar för Windows Hello för företag:  

![Guiden Windows Hello för företag-princip som visar listan över tillgängliga inställningar](../media/hello-for-business-settings.png)

## <a name="configure-permissions"></a>Konfigurera behörigheter

1. Som domän administratör eller motsvarande autentiseringsuppgifter loggar du in på en säker, administrativ arbets station som har följande valfria funktion installerad: RSAT: Active Directory Domain Services och Lightweight Directory Services-verktyg.

1. Öppna konsolen **Active Directory användare och datorer** .

1. Välj domän, gå till menyn **åtgärd** och välj **Egenskaper**.

1. Växla till fliken **säkerhet** och välj **Avancerat**.

    > [!TIP]
    > Om du inte ser fliken **säkerhet** stänger du fönstret Egenskaper. Gå till **Visa** -menyn och välj **avancerade funktioner**.

1. Välj **Lägg till**.

1. Välj **Välj ett huvud konto** och ange `Key Admins` .

1. I listan **gäller för väljer du** **underordnade användar objekt**.

1. Välj **Rensa alla**längst ned på sidan.

1. I avsnittet **Egenskaper** väljer du **Read msDS-KeyCredentialLink**.

1. Välj **OK** för att spara ändringarna och stänga alla fönster.

## <a name="next-steps"></a>Nästa steg

[Certifikatprofiler](introduction-to-certificate-profiles.md)