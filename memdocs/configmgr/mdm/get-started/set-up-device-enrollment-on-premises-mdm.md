---
title: Konfigurera registrering för lokal MDM
titleSuffix: Configuration Manager
description: Ge användare behörighet att registrera sina enheter för lokal hantering av mobila enheter (MDM) i Configuration Manager.
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 9ffaea91-1379-4b86-9953-b25e152f56a9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5c8213fac603d69e0f2afd31631e61ad301090f6
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721845"
---
# <a name="set-up-device-enrollment-for-on-premises-mdm-in-configuration-manager"></a>Konfigurera enhets registrering för lokal MDM i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Det sista steget för att konfigurera lokal hantering av mobila enheter (MDM) är att göra det möjligt för användare att registrera sina enheter. Använd Configuration Manager klient inställningar för att ge användare behörighet att registrera enheter i lokal MDM.

## <a name="create-an-enrollment-profile"></a><a name="bkmk_createProf"></a> Skapa en registreringsprofil

Om du vill skicka de inställningar som krävs för att tillåta användare att registrera mobila enheter lägger du till en ny registrerings profil i standard klient inställningarna. Den här profilen gäller sedan för alla användare på Configuration Managers platsen.

> [!NOTE]
> Den här processen använder **standard klient inställningarna**, som automatiskt kommer att gälla för alla enheter och användare. Du kan också skapa anpassade klient inställningar och sedan distribuera till samlingar som du väljer. Den här alternativa metoden kräver minst två anpassade klient inställningar, en för *enhets* inställningar och en för *användar* inställningar. Mer information finns i [så här konfigurerar du klient inställningar](../../core/clients/deploy/configure-client-settings.md).

1. I Configuration Manager-konsolen går du till arbets ytan **Administration** och väljer noden **klient inställningar** . Öppna **standard klient inställningar** och välj **registrerings** gruppen.

1. Under enhets inställningar anger du **avsöknings intervallet för moderna enheter (minuter)**. Som standard är det här intervallet 60 minuter.

1. Under användar inställningar aktiverar du alternativet för att **tillåta användare att registrera moderna enheter**.

1. För **profil för modern enhets registrering**väljer du **Ange profil**. I fönstret registrerings profil väljer du **skapa**.

1. I fönstret Skapa registrerings profil anger du följande information:

    - Ett unikt och beskrivande **namn** för registrerings profilen.

    - En valfri **Beskrivning** som ger ytterligare information om profilen.

    - Välj den **hanterings plats kod** som innehåller enhets hanterings platsen. Välj **OK** för att spara och stänga.

## <a name="configure-additional-client-settings"></a><a name="bkmk_addClient"></a>Konfigurera ytterligare klient inställningar

Det finns ytterligare klient inställningar för att konfigurera enheter när de har registrerats. Mer allmän information finns i [Konfigurera klient inställningar](../../core/clients/deploy/configure-client-settings.md).

Configuration Manager stöder följande klient inställningar för lokal MDM:

- **Klient princip**: de här inställningarna anger hur ofta klient principen ska laddas ned till enheten. Du kan också aktivera inställningar för användar principer. Mer information finns i [om klient inställningar-klient princip](../../core/clients/deploy/about-client-settings.md#client-policy).

- **Program varu distribution**: Ange intervallet för utvärdering av program varu distributioner. Mer information finns i [om klient inställningar-program varu distribution](../../core/clients/deploy/about-client-settings.md#software-deployment).

    > [!NOTE]
    > För lokal MDM kan inställningar för program varu distribution bara användas som standard klient inställningar.

## <a name="discover-users"></a><a name="bkmk_enableUsers"></a>Identifiera användare

För att användare ska kunna ta emot klient inställningarna med registrerings profilen för lokal MDM, identifierar platsen sitt användar konto i Active Directory. Om du vill se till att alla som behöver registreringsprofilen får den kör du identifiering av Active Directory-användare. Mer information finns i [Active Directory User Discovery](../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser).

## <a name="install-the-trusted-root-certificate"></a><a name="bkmk_storeCert"></a>Installera det betrodda rot certifikatet

Domänanslutna enheter hämtar förtroende rot certifikatet för betrodd kommunikation med servrarna som är värdar för plats system rollerna. Active Directory Certificate Services distribuerar automatiskt det betrodda rot certifikatet. Icke-domänanslutna datorer och mobila enheter behöver det här certifikatet installerat via andra sätt för att tillåta registrering.

> [!NOTE]
> Om webb server certifikat utfärdas av en offentlig certifikat utfärdare, är de flesta enheter redan betrodda dessa certifikat utfärdare. Om din design inkluderar användning av någon av dessa offentliga ca: er, behöver du inte göra det här steget.

När du har [exporterat det betrodda rot certifikatet](set-up-certificates-on-premises-mdm.md#bkmk_exportCert)måste du installera det på enheter som behöver det för att kunna registrera sig. Till exempel enheter som inte är anslutna till domänen och som inte kan hämtas automatiskt från Active Directory. Vilken process du ska använda beror på följande faktorer:

- Vissa enhets typer och tekniska funktioner
- OS-version
- Krav för din verksamhet, säkerhet och användar upplevelse

Följande lista innehåller några exempel metoder för att leverera och installera det betrodda rot certifikatet på enheter:

- Filresurs

- E-postbilaga

- Minneskort

- Enhet med Internetdelning

- Lagring i molnet (till exempel OneDrive)

- NFC-anslutning (Near field communication)

- Streckkodsläsare

- OOBE-etableringspaket (Out of box experience)

### <a name="manually-install-the-trusted-root-certificate-in-windows"></a>Installera det betrodda rot certifikatet manuellt i Windows

1. På enheten som ska registreras bläddrar du i Utforskaren till den betrodda rot certifikat filen (. cer) och **öppnar** den.

1. I fönstret certifikat väljer du **Installera certifikat**.

1. I guiden Importera certifikat väljer du **lokal dator**och väljer sedan **Nästa** för att fortsätta som administratör.

1. På sidan certifikat Arkiv väljer du **Placera alla certifikat i följande Arkiv**och väljer sedan **Bläddra**.

1. I fönstret Välj certifikat Arkiv väljer du **betrodda rot certifikat utfärdare**och väljer **OK**.

1. Slutför och guiden.

## <a name="next-step"></a>Nästa steg

> [!div class="nextstepaction"]
> [Registrera enheter](../deploy-use/enroll-devices-on-premises-mdm.md)
