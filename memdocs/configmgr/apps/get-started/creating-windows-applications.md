---
title: Skapa Windows-program
titleSuffix: Configuration Manager
description: Mer information om hur du skapar och distribuerar Windows-program i Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 9181c84e-d74f-44ea-9bb9-f7805eb465fc
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 77fee5931046bc706f965a9a5d738f5a7e2223f4
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/25/2020
ms.locfileid: "88819634"
---
# <a name="create-windows-applications-in-configuration-manager"></a>Skapa Windows-program i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Förutom de andra Configuration Manager krav och procedurer för att [skapa ett program](../deploy-use/create-applications.md)bör du också ta hänsyn till följande när du skapar och distribuerar program för Windows-enheter.  

## <a name="general-considerations"></a><a name="bkmk_general"></a> Allmänna överväganden  

Configuration Manager stöder distribution av Windows-appaket (. appx) och app bunt-format (. appxbundle) för Windows 8,1-och Windows 10-enheter.

När du skapar ett program i Configuration Manager-konsolen väljer du installations fil **typen** för programmet som **Windows-appaket ( \* . appx, \* . appxbundle, \* . msix, \* . msixbundle)**. Mer information om hur du skapar appar i allmänhet finns i [skapa program](../deploy-use/create-applications.md). Mer information om MSIX-formatet finns i [stöd för MSIX-format](#bkmk_msix).

> [!Note]  
> Om du vill dra nytta av nya Configuration Manager funktioner måste du först uppdatera klienter till den senaste versionen. När nya funktioner visas i Configuration Manager-konsolen när du uppdaterar platsen och konsolen, fungerar inte det fullständiga scenariot förrän klient versionen också är den senaste.<!--SCCMDocs issue 646-->  

## <a name="provision-windows-app-packages-for-all-users-on-a-device"></a><a name="bkmk_provision"></a> Etablera Windows-appaket för alla användare på en enhet
<!--1358310-->
Etablera ett program med ett Windows app-paket för alla användare på enheten. Ett vanligt exempel på det här scenariot är etablering av en app från Microsoft Store för företag och utbildning, till exempel Minecraft: Education Edition, för alla enheter som används av studenter i en skola. Tidigare Configuration Manager endast installera programmen per användare. När du har loggat in på en ny enhet skulle en student behöva vänta på att få åtkomst till en app. Nu när appen är etablerad till enheten för alla användare kan de vara produktivare snabbare.

> [!Important]  
> Var försiktig med att installera, konfigurera och uppdatera olika versioner av samma Windows app-paket på en enhet, vilket kan orsaka oväntade resultat. Det här problemet kan uppstå när du använder Configuration Manager för att etablera appen, men sedan tillåta att användare uppdaterar appen från Microsoft Store. Mer information finns i nästa steg-vägledning när du [hanterar appar från Microsoft Store för företag](../deploy-use/manage-apps-from-the-windows-store-for-business.md#next-steps).  

När du distribuerar offline-appar till Windows 10-enheter med Configuration Manager-klienten tillåter du inte att användare uppdaterar program som är externa för att Configuration Manager distributioner. Kontroll av uppdateringar till offline-appar är särskilt viktigt i miljöer med flera användare, till exempel klass rum. Mer information finns i [Hantera appar från Microsoft Store för företag och utbildning med Configuration Manager](../deploy-use/manage-apps-from-the-windows-store-for-business.md#next-steps).<!-- MEMDocs#316 -->

Configuration Manager stöder app-etablering i alla versioner av Windows 10 som stöds.<!--SCCMDocs-pr issue 2762-->

<!--
- Install action: Windows 10, version 1607 and later
- Uninstall action: Windows 10, version 1703 and later
-->

Om du vill konfigurera en distributions typ för Windows-appen för den här funktionen aktiverar du alternativet för att **etablera det här programmet för alla användare på enheten**. Mer information finns i [skapa program](../deploy-use/create-applications.md).

> [!Note]  
> Om du behöver avinstallera ett etablerad program från enheter som användarna redan har loggat in på, måste du skapa två avinstallations distributioner. Rikta den första avinstallations distributionen till en enhets samling som innehåller enheterna. Rikta den andra avinstallations distributionen till en användar samling som innehåller de användare som redan har loggat in på enheter med det etablerade programmet. När du avinstallerar en etablerad app på en enhet avinstallerar Windows för närvarande inte appen för användare även.

## <a name="support-for-msix-format"></a><a name="bkmk_msix"></a> Stöd för MSIX-format
<!--1357427-->

Configuration Manager stöder formaten Windows 10-appaket (. msix) och app-paket (. msixbundle). Windows 10 version 1809 eller senare har stöd för dessa format.

- En översikt över MSIX finns i [en närmare titt på MSIX](/archive/blogs/sgern/a-closer-look-at-msix).  

- Information om hur du skapar en ny MSIX-app finns [i stöd för MSIX som introducerades i Insider Build 17682](https://techcommunity.microsoft.com/t5/MSIX-Blog/MSIX-support-introduced-in-Insider-Build-17682/ba-p/202376).  

### <a name="convert-applications-to-msix"></a>Konvertera program till MSIX
<!--3607729, fka 1359029-->

Konvertera befintliga Windows Installer-program (. msi) till MSIX-format.

#### <a name="prerequisites-for-msix"></a>Krav för MSIX

- En referens enhet som kör Windows 10 version 1809 eller senare  

- Logga in på Windows på den här enheten som en användare med lokal administratörs behörighet  

- Installera följande appar på den här enheten:  

  - Configuration Manager-konsolen  

  - Installera [MSIX packning Tool](https://www.microsoft.com/store/productId/9N5LW3JBCXKF) från Microsoft Store  

  - Installera [MSIX packnings verktyg driv rutin](/windows/msix/packaging-tool/tool-known-issues#frameworks-and-drivers)<!--SCCMDocs-pr issue #3091-->  

Installera inte andra appar eller tjänster på den här enheten. Det är ditt referens system.

#### <a name="process-to-convert-applications-to-msix-format"></a>Process för att konvertera program till MSIX-format

1. Höj Configuration Manager-konsolen, gå till arbets ytan **program bibliotek** , expandera **program hantering**och välj noden **program** .  

2. Välj ett program som har distributions typen Windows Installer (. msi).  

    > [!Note]  
    > Du måste kunna komma åt programmets käll innehåll från referens enheten.  
    >
    > Programmets namn får inte innehålla specialtecken. Configuration Manager använder appens namn som namn på utdatafilen.  
    >
    > Installera inte det här programmet på referens enheten i förväg.  

3. Välj **konvertera till. MSIX** i menyfliksområdet.

När guiden har slutförts skapar MSIX packnings verktyget en MSIX-fil på den plats som du angav i guiden. Under den här processen installerar Configuration Manager tyst programmet på referens enheten.

Om processen Miss lyckas pekar sammanfattnings sidan på logg filen med mer information. Om det uppstår ett fel när du fångar in användar tillstånd loggar du ut från Windows. Det här problemet kan lösas om du loggar in igen.

Om du vill använda den här MSIX-appen måste du först signera den så att klienterna litar på den. Mer information om den här processen finns i följande artiklar:

- [MSIX – MSIX packnings verktyg – signera MSIX-paketet](/archive/blogs/sgern/msix-the-msix-packaging-tool-signing-the-msix-package)
- [Signera ett appaket med SignTool](/windows/desktop/appxpkg/how-to-sign-a-package-using-signtool)

När du har signerat appen skapar du en ny distributions typ i programmet i Configuration Manager. Mer information finns i [skapa distributions typer för programmet](../deploy-use/create-applications.md#bkmk_create-dt).

## <a name="task-sequence-deployment-type"></a><a name="bkmk_tsdt"></a> Distributions typ för aktivitetssekvens

<!--3555953-->

> [!Note]  
> I den här versionen av Configuration Manager är distributions typen för aktivitetssekvens en för hands versions funktion. För att aktivera den, se [för hands versions funktioner](../../core/servers/manage/pre-release-features.md).  

Från och med version 2002 kan du installera komplexa program med hjälp av aktivitetssekvenser via program modellen. Lägg till en distributions typ för aktivitetssekvens i en app för att installera eller avinstallera appen. Den här distributions typen innehåller följande beteenden:

<!-- - Deploy an app task sequence to a user collection -->

- Visa aktivitetssekvensen för appar med en ikon i Software Center. En ikon gör det enklare för användarna att hitta och identifiera programaktivitetssekvens.

- Definiera ytterligare metadata för aktivitetssekvensen, inklusive lokaliserad information

Du kan bara lägga till en aktivitetssekvens som distributions typ för en app. Det finns inte stöd för aktivitetssekvenser med hög effekt, OS-distribution eller operativ system uppgradering. <!--A user-targeted deployment still runs in the user context of the local System account.-->

När du lägger till den här distributions typen i en app konfigurerar du dess egenskaper på sidan **aktivitetssekvens** . Mer information finns i [alternativ för distributions typen **aktivitetssekvens** ](../deploy-use/create-applications.md#bkmk_dt-ts).

Från och med version 2006 använder du följande Windows PowerShell-cmdlets för att lägga till och konfigurera en aktivitetssekvensdistribution:

- [Add-CMTaskSequenceDeploymentType](/powershell/module/configurationmanager/add-cmtasksequencedeploymenttype?view=sccm-ps)
- [Set-CMTaskSequenceDeploymentType](/powershell/module/configurationmanager/set-cmtasksequencedeploymenttype?view=sccm-ps)

### <a name="prerequisites-for-a-task-sequence-deployment-type"></a>Krav för en aktivitetssekvensdistribution

Skapa en anpassad aktivitetssekvens:

- Använd endast distributions steg som inte är operativ system, till exempel: **installera paket**, **Kör kommando rad**eller **kör PowerShell-skript**. Mer information och en fullständig lista över de steg som stöds finns i [skapa en aktivitetssekvens för distributioner som inte är operativ system](../../osd/deploy-use/create-a-task-sequence-for-non-operating-system-deployments.md).

- På **fliken Egenskaper** för aktivitetssekvens väljer du inte alternativet för en aktivitetssekvens med hög effekt.

<!-- - If you use the **Install Application** step in the task sequence, don't add an app to that step that has a task sequence deployment type. -->

När du skapar ett program för att lägga till en aktivitetssekvensdistribution måste ditt användar konto ha behörighet att läsa aktivitetssekvenser.<!-- 6348976 --> Använd något av följande alternativ för att konfigurera dessa behörigheter:

- Lägg till appens administratörs användar konto i den inbyggda rollen för **skrivskyddad analys** . Med den här rollen kan du Visa alla Configuration Manager objekt.

- Kopiera den inbyggda rollen **program administratör** för att skapa en anpassad roll. Lägg till behörigheten **läsa** för **objektet aktivitetssekvens** .

### <a name="known-issues-for-a-task-sequence-deployment-type"></a>Kända problem för en aktivitetssekvensdistribution

- Du kan inte distribuera en app-aktivitetssekvens till en användar samling ännu

- Använd inte steget **installera program** i den här aktivitetssekvensen. Använd steget [installera paket](../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage) för att installera appar.

## <a name="support-for-universal-windows-platform-uwp-apps"></a><a name="bkmk_uwp"></a> Stöd för Universell Windows-plattform-appar (UWP)  

Windows 10-enheter kräver inte en nyckel för separat inläsning för att installera branschspecifika appar. Om du vill aktivera separat inläsning i Windows måste register nyckeln `HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Appx\AllowAllTrustedApps` ha värdet **1**.  

Om du inte konfigurerar den här register nyckeln anger Configuration Manager automatiskt värdet till **1** första gången du distribuerar en app till enheten. Om du har angett värdet till **0**kan Configuration Manager inte automatiskt ändra värdet och distributionen av branschspecifika appar Miss lyckas.  

Signera UWP-appar digitalt. Använd ett certifikat för kod signering som är betrott på varje enhet som du distribuerar appen till. Använd certifikat från din organisations PKI eller köp ett certifikat från en tredjeparts-Provider vars offentliga rot certifikat redan är betrott av Windows.  

Använd följande tabell för att ta reda på vilken typ av kod signerings certifikat som ska användas för att signera paket för mobilappar:

| Paket  | Symantec  | Ej Symantec  |
|---------|---------|---------|
| Universella **. appx** -paket på Windows 10 Mobile-enheter | Ja | Ja |
| **. xap** -paket | Ja | Inga |
| **. appx** -paket som skapats för Windows Phone 8,1 för installation på Windows 10 Mobile-enheter | Ja | Inga |

## <a name="deploy-windows-installer-apps-to-mdm-enrolled-windows-10-devices"></a><a name="bkmk_mdm-msi"></a> Distribuera Windows Installer appar till MDM-registrerade Windows 10-enheter  

Med distributions typen **Windows Installer via MDM ( \* . msi)** kan du skapa och distribuera Windows Installer-baserade appar till MDM-registrerade enheter som kör Windows 10.  

Tänk på följande när du använder den här distributions typen:

- Ladda bara upp en enda fil med MSI-tillägget.  

- Configuration Manager använder filens produkt kod och produkt version för identifiering av appar.  

- Windows använder appens standard beteende för omstart. Configuration Manager styr inte beteendet för att starta om appen.  

- MSI-paket per användare installeras för en enskild användare.  

- MSI-paket per dator installeras för alla användare av enheten.  

- Configuration Manager stöder uppdateringar av appar. Produkt koden för MSI för varje version måste vara densamma.