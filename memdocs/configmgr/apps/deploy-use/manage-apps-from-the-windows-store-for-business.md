---
title: Microsoft Store-appar
titleSuffix: Configuration Manager
description: Hantera och distribuera appar från Microsoft Store för företag och utbildning med Configuration Manager.
ms.date: 12/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 8cdb22a6-72d7-41f5-9bed-c098b1bcf675
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7d6a61324f8c777ba5ed09dd26816152d6f17af9
ms.sourcegitcommit: 2aa97d1b6409575d731c706faa2bc093c2b298c4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82643206"
---
# <a name="manage-apps-from-the-microsoft-store-for-business-and-education-with-configuration-manager"></a>Hantera appar från Microsoft Store för företag och utbildning med Configuration Manager

[Microsoft Store för företag och utbildning](https://docs.microsoft.com/microsoft-store/) är där du hittar och skaffar Windows-appar för din organisation. När du ansluter butiken till Configuration Manager, synkroniserar du listan med appar som du har köpt. Visa de här apparna i Configuration Manager-konsolen och distribuera dem på samma sätt som du distribuerar andra appar.

## <a name="online-and-offline-apps"></a><a name="bkmk_apps"></a>Online-och offline-appar

Microsoft Store för företag och utbildning stöder två typer av appar:

- **Online**: den här licens typen kräver att användare och enheter ansluter till Store för att få en app och dess licens. Windows 10-enheter måste vara Azure Active Directory (Azure AD) eller hybrid Azure AD-ansluten.  

- **Offline**: med den här typen kan du cachelagra appar och licenser för att distribuera direkt i ditt lokala nätverk. Enheterna behöver inte ansluta till butiken eller ha en anslutning till Internet.

Mer information finns i [Översikt över Microsoft Store för företag och utbildning](https://docs.microsoft.com/microsoft-store/microsoft-store-for-business-overview).

### <a name="summary-of-capabilities"></a>Sammanfattning av funktioner

Configuration Manager stöder hantering av Microsoft Store för affärs-och utbildnings appar på både Windows 10-enheter med Configuration Manager-klienten och även Windows 10-enheter som har registrerats med Microsoft Intune. Configuration Manager erbjuder följande funktioner för online-och offline-appar:

|Funktion|Offline-appar|Online-appar|
|------------|------------|------------|
|Synkronisera AppData till Configuration Manager<br>(synkronisering sker var 24: e timme)|Ja|Ja|
|Skapa Configuration Manager program från Store-appar|Ja|Ja|
|Stöd för kostnads fria appar från Store|Ja|Ja|
|Stöd för betalda appar från Store|Inga|Ja,<sup>[Anmärkning 1](#bkmk_note1)</sup>|
|Stöd för distributioner som krävs för användar-eller enhets samlingar|Ja|Ja|
|Stöd för tillgängliga distributioner till användar-eller enhets samlingar|Ja|Ja|
|Stöd för branschspecifika appar från Store|Ja|Ja|
|Tillhandahåll en Store-app för alla användare på en enhets<sup>[anteckning 2](#bkmk_note2)</sup><!--1358310-->|Ja|Ja|

#### <a name="note-1-online-licensed-apps-version-requirement"></a><a name="bkmk_note1"></a>Anmärkning 1: versions krav för licensierade appar online

För att distribuera online-licensierade appar till Windows 10-enheter med Configuration Manager-klienten, måste de köra Windows 10, version 1703 eller senare.  

#### <a name="note-2-configuration-manager-minimum-version"></a><a name="bkmk_note2"></a>Anmärkning 2: Configuration Manager lägsta version

Från och med version 1806. Mer information finns i [skapa Windows-program](../get-started/creating-windows-applications.md#bkmk_provision).  

### <a name="deploying-online-apps-using-the-microsoft-store-for-business-and-education-to-devices-that-run-the-configuration-manager-client"></a>Distribuera online-appar med Microsoft Store för företag och utbildning till enheter som kör Configuration Manager-klienten

Innan du distribuerar Microsoft Store för affärs-och utbildnings appar till enheter som kör den fullständiga Configuration Manager klienten bör du tänka på följande:

- För alla funktioner måste enheterna köra Windows 10, version 1703 eller senare.  

- Registrera eller Anslut enheter till samma Azure AD-klient där du registrerade Microsoft Store för företag och utbildning som ett hanterings verktyg.  

- När det lokala administratörs kontot loggar in på enheten kan det inte komma åt Microsoft Store för affärs-och utbildnings appar.  

- Enheter måste ha en Live Internet-anslutning till Microsoft Store för företag och utbildning. Mer information, inklusive proxykonfiguration, finns i [krav](https://docs.microsoft.com/microsoft-store/prerequisites-microsoft-store-for-business).  

### <a name="notes-for-devices-running-earlier-versions-of-windows-10"></a>Information om enheter som kör tidigare versioner av Windows 10

På enheter med Configuration Manager-klienten och kör Windows 10 version 1607 eller tidigare gäller följande funktioner:  

När du tillämpar installationen av appen på enheten med någon av följande metoder:  

- Användaren installerar appen  

- Distributionen når installationens tids gräns

- Omvärdering efter installation för nödvändiga distributioner  

Följande beteenden inträffar:  

- Configuration Manager klienten framtvingar appen genom att starta Microsoft Store-appen  

- Användaren måste slutföra installationen från Store  

- I Configuration Manager-konsolen rapporterar appens distributions status fel med följande fel: "Microsoft Store-appen öppnades på klient datorn och väntar på att användaren ska slutföra installationen."  

Vid nästa program utvärderings cykel:  

- Om användaren installerade programmet från Store rapporterar programmet statusen **slutfört**  

- Om användaren inte försöker installera appen från Store:  

  - För nödvändiga distributioner försöker Configuration Manager klienten starta Store-appen igen  

  - Configuration Manager tillämpar inte tillgängliga distributioner igen

#### <a name="devices-running-earlier-versions-of-windows-10"></a>Enheter som kör tidigare versioner av Windows 10

- Du kan inte distribuera branschspecifika appar från Microsoft Store för företag och utbildning

- När du distribuerar betalda appar från Store måste användarna logga in i butiken och hämta själva appen  

- Om du distribuerar en grup princip för att inaktivera åtkomst till konsument versionen av Microsoft Store fungerar inte distributioner från Microsoft Store för företag och utbildning. Detta händer även om du aktiverar Microsoft Store för företag och utbildning.  

## <a name="set-up-synchronization"></a><a name="bkmk_setup"></a>Konfigurera synkronisering

När du synkroniserar listan med Microsoft Store för affärs-och utbildnings appar som din organisation har köpt, kan du se dessa appar i Configuration Manager-konsolen.

Anslut Configuration Manager-platsen till Azure AD och Microsoft Store för företag och utbildning. Mer information och information om den här processen finns i [Konfigurera Azure-tjänster](../../core/servers/deploy/configure/azure-services-wizard.md). Skapa en anslutning till **Microsoft Store for Business** -tjänsten.

Kontrol lera att tjänst anslutnings punkten och mål enheterna har åtkomst till moln tjänsten. Mer information finns i [krav för Microsoft Store för företags-och utbildnings-proxy-konfiguration](https://docs.microsoft.com/microsoft-store/prerequisites-microsoft-store-for-business#proxy-configuration).

### <a name="supplemental-information-and-configuration"></a><a name="bkmk_config"></a>Kompletterande information och konfiguration

På sidan **app** i guiden Azure-tjänster konfigurerar du först Azure- **miljön** och **webbappen**. Läs sedan avsnittet **Mer information** längst ned på sidan. Den här informationen omfattar följande ytterligare åtgärder på portalen Microsoft Store for Business och Education:  

- Konfigurera Configuration Manager som lagrings hanterings verktyg. Mer information finns i [Konfigurera hanterings leverantör](https://docs.microsoft.com/microsoft-store/configure-mdm-provider-microsoft-store-for-business).  

- Aktivera stöd för licensierade appar offline. Mer information finns i [distribuera offline-appar](https://docs.microsoft.com/microsoft-store/distribute-offline-apps).  

- Hämta minst en app. Mer information finns i [hitta och hämta appar](https://docs.microsoft.com/microsoft-store/find-and-acquire-apps-overview).  

Ange följande information på sidan **konfigurationer** i guiden Azure-tjänster:  

- **Sökväg till Microsoft Store för lagring av Business app-innehåll**: Ange en delad nätverks Sök väg, inklusive en mapp. Till exempel `\\server\share\folder`. När plats servern synkroniserar med Store cachelagras innehållet på den här platsen. När du skapar ett program i Configuration Manager kopierar plats servern appens innehåll från den här lokala cachen till platsens innehålls bibliotek.  

- **Valda språk**: Välj de språk som ska synkroniseras från butiken och visas för användare i Software Center. Om användaren till exempel konfigurerar Windows för tyska visar Software Center tyska strängar för Store-appen. Det här beteendet kräver att språket synkroniseras och att det finns för det specifika programmet.

- **Standard språk**: om användarens språk inte är tillgängligt väljer du ett standard språk som ska användas.  

> [!NOTE]
> Configuration Manager synkroniserar inte appens ikon från Store. Om du behöver en ikon som ska visas för den här appen i Software Center, lägger du till den manuellt i appens egenskaper. Mer information finns i [Ange programinformation manuellt](create-applications.md#bkmk_manual-app).<!-- 2837053 -->

## <a name="create-and-deploy-the-app"></a><a name="bkmk_deploy"></a>Skapa och distribuera appen

Efter synkroniseringen skapar och distribuerar du Microsoft Store for Business-och Education-appar som liknar andra Configuration Manager program.

1. I arbets ytan **program varu bibliotek** i Configuration Manager-konsolen expanderar du **program hantering**och väljer sedan **licens information för Store Apps** -noden.  

2. Välj den app som du vill distribuera och välj sedan **skapa program** i menyfliksområdet.  

Webbplatsen skapar ett Configuration Manager-program som innehåller appen Microsoft Store for Business och Education.

Distribuera och övervaka sedan det här programmet precis som med andra Configuration Manager program. Mer information finns i följande artiklar:  

- [Distribuera program](deploy-applications.md)
- [Övervaka program från konsolen](monitor-applications-from-the-console.md)

## <a name="next-steps"></a>Nästa steg

I arbets ytan **program bibliotek** expanderar du **program hantering**och väljer sedan **licens information för Store Apps** -noden.

För varje Store-app som du hanterar kan du se följande information om appen:

- Appnamn
- App-plattform
- Antalet licenser för den app som du äger
- Antalet tillgängliga licenser

När du har distribuerat online-appar kommer alla uppdateringar av appen att komma direkt från Microsoft Store. Dessutom kontrollerar Configuration Manager inte versions kompatibilitet för online-appar, precis som Windows rapporterar appen som installerad.  

När du distribuerar offline-appar till Windows 10-enheter med Configuration Manager-klienten tillåter du inte att användare uppdaterar program som är externa för att Configuration Manager distributioner. Kontroll av uppdateringar till offline-appar är särskilt viktigt i miljöer med flera användare, till exempel klass rum. Ett alternativ för att inaktivera Microsoft Store är med hjälp av en [grup princip](https://docs.microsoft.com/windows/configuration/stop-employees-from-using-microsoft-store#block-microsoft-store-using-group-policy).

När Microsoft Store för företag och utbildnings administratör hämtar en offline-app, ska du inte publicera appen till användare via Store. Den här konfigurationen säkerställer att användare inte kan installera eller uppdatera online. Användare får bara ta emot uppdateringar av offline-appar via Configuration Manager.

## <a name="see-also"></a>Se även

[Felsök Microsoft Store för affärs-och utbildnings integrering med Configuration Manager](troubleshoot-microsoft-store-for-business-integration.md)
