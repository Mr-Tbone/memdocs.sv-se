---
title: Integrera Windows Hello för företag med Microsoft Intune
titleSuffix: Microsoft Intune
description: Läs mer om att skapa en policy för att kontrollera användningen av Windows Hello för företag på hanterade enheter under enhetsregistreringen.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/14/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: shpate
ms.openlocfilehash: 70c0418f02bd94a957967c72045be210dad56c78
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914709"
---
# <a name="integrate-windows-hello-for-business-with-microsoft-intune"></a>Integrera Windows Hello för företag med Microsoft Intune  

Du kan integrera Windows Hello för företag (tidigare Microsoft Passport for Work) med Microsoft Intune under enhetsregistreringen.

Hello för företag är en alternativ inloggningsmetod som använder Active Directory eller ett Azure Active Directory-konto för att ersätta ett lösenord, smartkort eller virtuellt smartkort. Du kan använda en *användargest* för att logga in i stället för ett lösenord. En användargest kan vara en PIN-kod, biometrisk autentisering, t.ex. Windows Hello, eller en extern enhet, t.ex. en fingeravtrycksläsare.

Intune kan integreras med Hello för företag på två sätt:

- **Klientomfattande** (*den här artikeln)* : En Intune-princip kan skapas under *Enhetsregistrering*. Den här principen riktar in sig på hela organisationen (klienttäckande). Den har stöd för välkomstprogrammet (OOBE) i Windows AutoPilot och används när en enhet registreras.
- **Diskreta grupper**: För enheter som tidigare har registrerats med Intune använder du en [**Identitetsskydd**](../protect/identity-protection-configure.md)-profil för att konfigurera enheter för Windows Hello för företag. Identitetsskyddsprofiler kan rikta sig mot tilldelade användare eller enheter och tillämpas vid incheckning.

Dessutom stöder Intune följande typer av principer för att hantera vissa inställningar för Windows Hello för företag:

- [**Säkerhetsbaslinjer**](../protect/security-baselines.md). Följande baslinjer innehåller inställningar för Windows Hello för företag:
  - [Baslinjeinställningar för Microsoft Defender Advanced Threat Protection](../protect/security-baseline-settings-defender-atp.md#windows-hello-for-business)
  - [Inställningar för Windows MDM-säkerhetsbaslinjer](../protect/security-baseline-settings-mdm-all.md#windows-hello-for-business)
- Slutpunktssäkerhet [**Kontoskydd**](../protect/endpoint-security-account-protection-policy.md)-princip. Visa [Kontoskyddsinställningar](../protect/endpoint-security-account-protection-profile-settings.md#account-protection).

Återstoden av den här artikeln fokuserar på hur man skapar en standardprincip för Windows Hello för företag som riktar in sig på hela organisationen.

> [!IMPORTANT]
> Innan Anniversary Update kan du ange två olika PIN-koder som kan användas för autentisering mot resurser:
>
> - **PIN-koden för enheten** kunde användas för att låsa upp enheten och ansluta till molnresurser.
> - **PIN-koden för arbetsplatsen** användes för att komma åt resurser i Azure AD på användarnas personliga enheter (BYOD).
>
> I och med Anniversary Update sammanfogades dessa två PIN-koder till en enda PIN-kod för enheten.
> Alla principer för konfiguration i Intune som du anger för att styra PIN-koden för enheten och alla principer för Windows Hello för företag du konfigurerat ställer nu båda in det nya PIN-värdet.
> Om du har angett båda principtyperna för att kontrollera PIN-koden tillämpas Windows Hello för företag-principen.
> Uppdatera din princip för Windows Hello för företag så att den matchar inställningarna i konfigurationsprincipen och be dina användare att synkronisera sina enheter i företagsportalappen för att säkerställa att principkonflikter inte uppstår och att PIN-principen tillämpas korrekt.

## <a name="create-a-windows-hello-for-business-policy"></a>Skapa en princip för Windows Hello för företag

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Gå till **Enheter** >  **Registrering** > **Registrera enheter** > **Windows.-registrering** > **Windows Hello för företag**. Fönstret Windows Hello för företag öppnas.

3. Välj bland följande alternativ för **Konfigurera Windows Hello för företag**:

   - **Aktiverad**. Välj den här inställningen om du vill konfigurera inställningarna för Windows Hello för företag.  När du väljer *Aktiverad* blir ytterligare inställningar för Windows Hello synliga och du kan konfigurera dem för dina enheter.

   - **Inaktiverad**. Om du inte vill aktivera Windows Hello för företag under enhetsregistreringen väljer du det här alternativet. När den är inaktiverad kan användarna inte etablera Windows Hello för företag. Om du anger *Inaktiverad* kan du fortfarande konfigurera de efterföljande inställningarna för Windows Hello för företag, även om den här policyn inte aktiverar Windows Hello för företag.

   - **Inte konfigurerat**. Välj den här inställningen om du inte vill konfigurera inställningarna för Windows Hello för företag. Eventuella befintliga inställningar för Windows Hello för företag på Windows 10-enheter ändras inte. Alla andra inställningar i fönstret inaktiveras.

4. Om du valde **Aktiverad** i föregående steg, konfigurerar du de obligatoriska inställningar som kommer att användas på alla registrerade Windows 10-enheter. Välj **Spara** när du har konfigurerat inställningarna.

   - **Använd TPM (Trusted Platform Module)** :

     Ett TPM-chip ger ett ytterligare lager med datasäkerhet. Välj ett av följande värden:

     - **Obligatoriskt** (standard). Endast enheter med en tillgänglig TPM kan etablera Windows Hello för företag.
     - **Önskad**. Enheterna försöker först använda TPM. Om det inte är tillgängligt kan de använda programvarukryptering.

   - **Minsta PIN-kodslängd** och **Maximal PIN-kodslängd**:

     Konfigurerar enheterna så att de använder de minsta och största PIN-kodslängder du anger för att hjälpa till att säkerställa säker inloggning. Standardlängden för PIN-kod är sex tecken, men du kan ange en minsta längd på fyra tecken. Den maximala längden för PIN-kod är 127 tecken.

   - **Gemener i PIN-koden**, **Versaler i PIN-koden** och **Specialtecken i PIN-koden**.

     Du kan tillämpa en starkare PIN-kod genom att kräva att versaler, gemener och specialtecken används i PIN-koden. För var och en väljer du från:

     - **Tillåts**. Användarna kan använda teckentypen i sina PIN-koder, men det är inte obligatoriskt.

     - **Krävs**. Användarna måste inkludera minst en av teckentyperna i sina PIN-koder. Det är till exempel vanligt att man kräver minst en versal och ett specialtecken.

     - **Tillåts inte** (standard). Användarna får inte använda dessa teckentyper i sina PIN-koder. (Det är också det som gäller om inställningen inte konfigureras.)

       Specialtecken omfattar följande: **! " # $ % &amp; ' ( ) &#42; + , - . / : ; &lt; = &gt; ? @ [ \ ] ^ _ &#96; { &#124; } ~**

   - **PIN-kodens giltighetstid (dagar)** :

     Det tillhör god praxis att ange en giltighetstid för en PIN-kod och efter denna tid måste användaren ändra den. Standarden är 41 dagar.

   - **Spara PIN-kodshistorik**:

     Begränsar återanvändning av PIN-koder som har använts tidigare. Standardvärdet är att de 5 senaste PIN-koderna inte kan återanvändas.

   - **Tillåt biometrisk autentisering**:

     Aktiverar biometrisk autentisering, t.ex. ansiktsigenkänning eller fingeravtryck, som ett alternativ till PIN-koden för Windows Hello för företag. Användarna måste ändå konfigurera en PIN-kod om den biometriska autentiseringen skulle misslyckas. Välj mellan:

     - **Ja**. Windows Hello för företag tillåter biometrisk autentisering.
     - **Nej**. Windows Hello för företag förhindrar biometrisk autentisering (för alla kontotyper).

   - **Använd utökat skydd mot förfalskning när det är tillgängligt**:

     Konfigurerar om funktionerna för skydd mot förfalskning i Windows Hello ska användas på enheter som stöder detta. Till exempel att identifiera ett foto av ett ansikte, i stället för ett riktigt ansikte.

     Om detta är inställt på **Ja** kräver Windows att alla användare använder skydd mot förfalskning för ansiktsdrag när detta stöds.

   - **Tillåt telefoninloggning**:

     Om det här alternativet är inställt på **Ja** kan användarna använda ett fjärranslutet Passport som fungerar som en bärbar tillhörande enhet för autentisering på stationär dator. Den stationära datorn måste vara ansluten med Azure Active Directory och den tillhörande enheten måste vara konfigurerad med en PIN-kod för Windows Hello för företag.

## <a name="windows-holographic-for-business-support"></a>Stöd för Windows Holographic for Business

Windows Holographic for Business har stöd för följande inställningar för Windows Hello för företag:

- Använd en Trusted Platform Module (TPM)
- Minsta PIN-kodslängd
- Maximala PIN-kodslängd
- Gemener i PIN-koden
- Versaler i PIN-koden
- Specialtecken i PIN-koden
- Förfallodagar för PIN-kod (dagar)
- Kom ihåg PIN-historik

## <a name="next-steps"></a>Nästa steg

Mer information om Microsoft Hello för Företag finns i [guiden](/windows/security/identity-protection/hello-for-business/hello-identity-verification) i Windows 10-dokumentationen.