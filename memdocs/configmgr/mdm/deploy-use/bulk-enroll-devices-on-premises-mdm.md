---
title: Så här registrerar du enheter
titleSuffix: Configuration Manager
description: Mass registrering av enheter på ett automatiserat sätt med lokal hantering av mobila enheter (MDM) i Configuration Manager.
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: b36f5e4a-2b57-4d18-83f6-197081ac2a0a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bfe2d395187f8af86e2d09156a45f7398a5bc670
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720683"
---
# <a name="how-to-bulk-enroll-devices-with-on-premises-mdm-in-configuration-manager"></a>Så här registrerar du enheter med lokal MDM i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Mass registrering i Configuration Manager lokal hantering av mobila enheter (MDM) är en automatiserad metod för att registrera enheter. Den andra metoden är Användar registrering, som kräver att användarna anger sina autentiseringsuppgifter för att registrera enheten. Massregistrering använder ett registreringspaket för att autentisera enheten under registreringen. Paketet är en. ppkg-fil som även kan innehålla certifikat-och Wi-Fi-profiler som stöder registrering.

## <a name="create-a-certificate-profile"></a><a name="bkmk_createCert"></a> Skapa en certifikatprofil

Inkludera en certifikat profil för att automatiskt installera ett betrott rot certifikat på enheten. Det här rot certifikatet krävs för betrodd kommunikation mellan enheterna och de plats system roller som krävs för lokal MDM.

När du förbereder platsen för lokal MDM exporterar du det betrodda rot certifikatet. Använd det här certifikatet i registrerings paketets certifikat profil. Mer information om hur du hämtar det betrodda rot certifikatet finns i [exportera det betrodda rot certifikatet](../get-started/set-up-certificates-on-premises-mdm.md#bkmk_exportCert).

Använd det exporterade certifikatet för att skapa en certifikat profil. Mer information finns i [så här skapar du certifikat profiler](../../protect/deploy-use/create-certificate-profiles.md).

## <a name="create-a-wi-fi-profile"></a><a name="CreateWifi"></a>Skapa en Wi-Fi-profil

En annan komponent i Mass registrerings paketet är en Wi-Fi-profil. Den här profilen kan se till att enheten har nätverks anslutningen som stöd för registrering.

Mer information om hur du skapar en Wi-Fi-profil i Configuration Manager finns i [så här skapar du Wi-Fi-profiler](../../protect/deploy-use/create-wifi-profiles.md).

### <a name="wi-fi-profile-limitations"></a>Begränsningar för Wi-Fi-profil

När du skapar en Wi-Fi-profil för lokal MDM-registrering i MDM bör du läsa följande begränsningar.

#### <a name="wi-fi-security-configurations-for-on-premises-mdm"></a>Wi-Fi-säkerhetskonfigurationer för lokal MDM

Den aktuella grenen av Configuration Manager har endast stöd för följande Wi-Fi-säkerhetskonfigurationer för lokal MDM:

- Säkerhetstyper: **WPA2 Enterprise** eller **WPA2 Personal**

- Krypteringstyper: **AES** eller **TKIP**

- EAP-typer: **Smartkort eller annat certifikat** eller **PEAP**

#### <a name="proxy-server"></a>Proxyserver

Även om Configuration Manager har en inställning för information om proxyserver i Wi-Fi-profilen, så konfigurerar den inte proxyn när enheten registreras. Om du behöver konfigurera en proxyserver på en grupp med registrerade enheter:

- Distribuera inställningarna med konfigurations objekt när enheterna registreras.

- Skapa ett andra paket med Windows-avbildningen och Configuration designer (ICD) och distribuera det sedan tillsammans med Mass registrerings paketet.

## <a name="create-an-enrollment-profile"></a><a name="bkmk_createEnroll"></a> Skapa en registreringsprofil

Med registrerings profilen kan du ange inställningar som krävs för enhets registrering. Inställningarna omfattar en [certifikat profil](#bkmk_createCert) och en [Wi-Fi-profil](#CreateWifi).

1. I Configuration Manager-konsolen går du till arbets ytan **till gångar och efterlevnad** , expanderar **alla företagsägda enheter**, expanderar **Windows**och väljer noden **registrerings profiler** .

1. I menyfliksområdet väljer du **skapa registrerings profil**.

1. Ange följande information på sidan **Allmänt** i guiden skapa registrerings profil:

    - **Namn**: ett unikt namn som identifierar profilen

    - **Beskrivning**: ett valfritt fält för att beskriva profilen närmare.

    - **Hanterings utfärdare**: Välj endast **lokalt**

1. På sidan **platstilldelning** väljer du **hanterings plats koden** med en enhets hanterings plats.

1. På sidan **Välj proxy för registrerings plats** väljer du **endast intranät**och väljer sedan en eller flera proxy-platser för registrering. Enheten kommer att använda dessa servrar för att starta registrerings processen.

1. På sidan **Välj betrott rot certifikat** väljer du den certifikat profil som innehåller det betrodda rot certifikatet.

1. På sidan **Wi-Fi-profiler** väljer du den Wi-Fi-profil som innehåller de nätverks inställningar som krävs för att ansluta enheter.

    > [!TIP]
    > Om du inte använder en Wi-Fi-profil för registrerings paketet kan du hoppa över det här steget.

1. Slutför guiden.

## <a name="create-an-enrollment-package"></a><a name="bkmk_createPpkg"></a>Skapa ett registrerings paket

Registrerings paketet (ppkg) är den fil som du använder för att registrera enheter för lokal MDM. Skapa den här filen med Configuration Manager. Även om du kan skapa liknande typer av paket med Windows-ICD kan endast paket som du skapar i Configuration Manager användas för att registrera enheter för lokal MDM. Ett paket som du skapar med Windows-ICD kan bara tillhandahålla den User Principal Name (UPN) som krävs för registreringen, det kan inte starta den faktiska registrerings processen.

Processen för att skapa registreringspaketet kräver Windows Assessment and Deployment Toolkit (ADK) för Windows 10. På den dator som kör Configuration Manager-konsolen installerar du den senaste versionen av Windows ADK. Välj **Imaging and Configuration designer (ICD)-** funktionen och eventuella beroenden. (Den här versionen behöver inte matcha den version som används för operativ Systems distribution av Configuration Manager-platsen.) Mer information finns i [Ladda ned Windows ADK för Windows 10](https://docs.microsoft.com/windows-hardware/get-started/adk-install).

1. I Configuration Manager-konsolen går du till arbets ytan **till gångar och efterlevnad** , expanderar **alla företagsägda enheter**, expanderar **Windows**och väljer noden **registrerings profiler** .

1. Välj en befintlig registrerings profil. I menyfliksområdet väljer du **Exportera**.

1. I fönstret Exportera registrerings paket anger du följande information:

    - **Giltighets period (dagar)**: Configuration Manager anger att registrerings paketet ska förfalla i två veckor (14 dagar) som standard. Du kan inte använda paketet för enhets registrering när giltighets perioden har upphört att gälla. Ange ett heltal mellan 1 och 30.

    - **Paketfil**: Ange en lokal sökväg eller en nätverks fil Sök väg och namn för. ppkg-filen.

    - **Kryptera paket**: aktivera det här alternativet om du vill skydda paketet med ett lösen ord. När du har exporterat paketet visar Configuration Manager det genererade lösen ordet. Kopiera och spara lösen ordet på en säker plats. Du kan inte använda det exporterade registrerings paketet utan lösen ordet.

        > [!IMPORTANT]
        > Configuration Manager sparar inte lösen ordet och du kan inte anpassa eller ändra det. När du stänger fönstret som visar lösen ordet finns det inget sätt att hämta lösen ordet.

1. Välj **Exportera**. Configuration Manager använder Windows ADK för att skapa registrerings paketet.

Configuration Manager håller reda på giltiga registrerings paket. I-konsolen expanderar du noden **registrerings profil** och väljer **exporterade paket**.

> [!TIP]
> Om du tar bort ett registrerings paket från Configuration Manager-konsolen kan du inte använda det för att registrera enheter. Använd den här metoden för att hantera registrerings paket som du inte vill att andra ska använda för Mass registrering.

## <a name="bulk-enroll-a-device"></a><a name="bkmk_getPpkg"></a>Mass registrering av en enhet

Du kan använda ett paket för att registrera enheter före eller efter enhetens OOBE-process (out-of-Box Experience). Registrerings paketet kan också ingå som en del av ett OEM-etablerings paket (Original Equipment Manufacturer).

Om du vill använda paketet för Mass registrering måste du leverera det fysiskt till enheten. Det finns olika metoder beroende på dina behov, till exempel:

- Kopiera från fil systemet

- Bifoga till ett e-postmeddelande

- Kopiera över en anslutning för nära fält kommunikation (NFC)

- Kopiera från ett minnes kort

- Skanna en streckkod

- Kopiera från en delad enhet

- Ta med i ett OEM-etablerings paket

### <a name="enroll-a-device-with-bulk-enrollment-package"></a>Registrera en enhet med ett Mass registrerings paket

1. Öppna filen. ppkg på en enhet. Kör som administratör vid behov.

1. Windows frågar om paketet kommer från en betrodd källa väljer du **Ja**.

Registrerings processen startar.

## <a name="verify-enrollment"></a><a name="bkmk_verifyEnroll"></a>Verifiera registrering

### <a name="verify-bulk-enrollment-on-the-device"></a>Verifiera Mass registrering på enheten

1. Öppna **Inställningar**på enheten.

1. Välj **konton**och välj **åtkomst till arbete eller skola**. När registreringen lyckas visas ett konto under **CompanyApps**.

1. Välj kontot och välj sedan **Synkronisera**. Den här åtgärden startar hanteringen med Configuration Manager.

### <a name="verify-enrollment-in-the-console"></a>Verifiera registrering i-konsolen

Använd Configuration Manager-konsolen för att verifiera att enheterna har registrerats. Gå till arbets ytan **till gångar och efterlevnad** i Configuration Manager-konsolen och välj **enheter**. Bläddra eller Sök efter den registrerade enheten i listan med enheter.
