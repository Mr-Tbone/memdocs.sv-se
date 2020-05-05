---
title: Funktioner i Technical Preview 1610
titleSuffix: Configuration Manager
description: Lär dig mer om funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1610.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8b31fd3e-875a-4a31-9498-5b050aadce32
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 6402205ae694d719845492b1af37000a0b9335c5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721474"
---
# <a name="capabilities-in-technical-preview-1610-for-configuration-manager"></a>Funktioner i Technical Preview 1610 för Configuration Manager

*Gäller för: Configuration Manager (Technical Preview Branch)*



Den här artikeln beskriver de funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1610. Du kan installera den här versionen för att uppdatera och lägga till nya funktioner till din Configuration Manager Technical Preview-webbplats.      Innan du installerar den här versionen av Technical Preview kan du läsa introduktions avsnittet, [teknisk för hands version för Configuration Manager](../../core/get-started/technical-preview.md), för att bekanta dig med allmänna krav och begränsningar för att använda en teknisk för hands version, hur du uppdaterar mellan versioner och hur du ger feedback om funktionerna i en teknisk för hands version.    


**Följande är nya funktioner som du kan prova med den här versionen.**  
## <a name="filter-by-content-size-in-automatic-deployment-rules"></a>Filtrera efter innehålls storlek i regler för automatisk distribution
Nu kan du filtrera efter innehålls storleken för program uppdateringar i regler för automatisk distribution. Du kan till exempel ange filtret för **innehålls storlek (KB)** till **< 2048** för att endast hämta program uppdateringar som är mindre än 2 MB. Med det här filtret förhindrar du att stora program uppdateringar laddas ned automatiskt för att ge bättre stöd för förenklad Windows-etablering när nätverks bandbredden är begränsad. Mer information finns i [Configuration Manager och förenklad Windows-underhåll på äldre operativ system](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/).

#### <a name="to-configure-the-content-size-field"></a>Så här konfigurerar du fältet innehålls storlek
Om du vill konfigurera fältet **innehålls storlek (KB)** går du till sidan **program uppdateringar** i guiden Skapa regel för automatisk distribution när du skapar en ADR eller går till fliken **program uppdateringar** i egenskaperna för en befintlig ADR.

![Fält för innehålls storlek](media/contentsizefield.png)

## <a name="improved-functionality-for-required-software-dialogs"></a>Förbättrade funktioner för nödvändiga program varu dialog rutor
När en användare får nödvändig program vara, från inställningen **vilo läge och Påminn mig:** kan du välja i följande listruta med värden:
- Senare: anger att meddelanden ska schemaläggas baserat på de meddelande inställningar som kon figurer ATS i klient agent inställningarna.
- Fast tid: anger att meddelandet ska visas igen efter den valda tiden. Om en användare exempelvis väljer 30 minuter visas meddelandet igen om 30 minuter.

![Sidan dator agent i inställningar för klient agent](media/computeragentsettings.png)

Den maximala tiden för vilo läge baseras alltid på de meddelande värden som kon figurer ATS i inställningarna för klient agenten vid varje tidpunkt längs drifts tids linjen. Om **distributions tids gränsen är större än 24 timmar, är inställningen Påminn användare var (timme)** på sidan dator agent konfigurerad i 10 timmar och det är mer än 24 timmar innan tids gränsen har startats visas användaren med en uppsättning alternativ för vilo läge, upp till men aldrig längre än 10 timmar. När tids gränsen närmar sig kommer dialog rutan att visa färre alternativ, konsekvent med relevanta klient agent inställningar för varje komponent i distributions tids linjen.

För en distribution med hög risk, till exempel en aktivitetssekvens som distribuerar ett operativ system, är aviseringen för slutanvändare nu mer påträngande. I stället för ett tillfälligt meddelande i aktivitets fältet, varje gång användaren meddelas att kritiskt program varu underhåll krävs, visas en dialog ruta som nedan på användarens dator:

![Dialog rutan nödvändig program vara](media/requiredsoftwaredialog.png)


Mer information:
- [Inställningar för att hantera högrisk distributioner](../servers/manage/settings-to-manage-high-risk-deployments.md)
- [Konfigurera klientinställningar](../clients/deploy/configure-client-settings.md)

## <a name="deny-previously-approved-application-requests"></a>Neka tidigare godkända program begär Anden

Som administratör kan du nu neka en tidigare godkänd programbegäran. När programmet har nekats måste du skicka en begäran igen för att installera det här programmet. Neka avinstallation av programmet. i stället tvingas godkännandet av alla nya begär Anden för programmet från den användaren. Tidigare var avslag endast tillgängligt för program begär Anden som inte hade godkänts.

#### <a name="try-it-out"></a>Prova nu
Så här nekar du ett program som godkänns förfrågan:

1. [Skapa och distribuera ett program](../../apps/deploy-use/create-applications.md) som kräver godkännande i Configuration Manager-konsolen.
2. Öppna Software Center på en klient dator och skicka en begäran om programmet.
3. Godkänn programbegäran i Configuration Manager-konsolen.
4. Neka den godkända programbegäran: i Configuration Manager-konsolen går du till översikt över program **varu bibliotek** > **Översikt över** > **program hanterings** > **begär Anden** och väljer den programbegäran som du vill neka.  Klicka på **neka**i menyfliksområdet.

## <a name="exclude-clients-from-automatic-upgrade"></a>Undanta klienter från automatisk uppgradering
Technical Preview 1610 introducerar en ny inställning som du kan använda för att undanta en samling klienter från att automatiskt installera uppdaterade klient versioner.  Detta gäller för automatisk uppgradering samt andra metoder, till exempel program uppdatering baserad uppgradering, inloggnings skript och grup princip. Detta kan användas för en samling datorer som behöver bättre försiktighet vid uppgradering av-klienten. En klient som ingår i en undantagen samling ignorerar begär Anden om att installera uppdaterad klient program vara.

### <a name="configure-exclusion-from-automatic-upgrade"></a>Konfigurera undantag från automatisk uppgradering
Så här konfigurerar du undantag för automatiska uppgraderingar:
1. I Configuration Manager-konsolen öppnar du **Inställningar för hierarki** under **Administration > plats konfiguration > platser**och väljer sedan fliken **klient uppgradering** .
2. Markera kryss rutan för **undanta angivna klienter från uppgradering**och välj den samling som du vill undanta för **exkluderings samling**. Du kan bara välja en samling som ska undantas.
3. Klicka på **OK** för att stänga och spara konfigurationen. Efter att klienterna uppdaterar principen kommer klienter i den undantagna samlingen inte längre att automatiskt installera uppdateringar av klient programmet.

   ![Inställningar för undantag för automatisk uppgradering](media/automatic_upgrade_exclusion.png)

> [!NOTE]
> Även om användar gränssnittet anger att klienterna inte ska uppgraderas via någon metod, finns det två metoder som du kan använda för att åsidosätta inställningarna. Push-installation av klienter och en manuell klient installation kan användas för att åsidosätta den här konfigurationen. Mer information finns i följande avsnitt.

### <a name="how-to-upgrade-a-client-that-is-in-an-excluded-collection"></a>Så här uppgraderar du en klient som ingår i en undantagen samling
Så länge som en samling har kon figurer ATS för att undantas, kan medlemmar i samlingen endast ha sin klient program vara uppgraderad av en av två metoder, vilket åsidosätter undantaget:
- **Push-installation av klient** – du kan använda push-installation av klienter för att uppgradera en klient som finns i en undantagen samling. Detta är tillåtet eftersom det anses vara administratörens avsikt och gör att du kan uppgradera klienter utan att ta bort hela samlingen från undantag.       
- **Manuell klient installation** – du kan uppgradera klienter som finns i en undantagen samling manuellt när du använder följande kommando rads växel med CCMSetup: ***/ignoreskipupgrade***

  Om du försöker uppgradera en klient som är medlem i den undantagna samlingen och inte använder den här växeln, kommer klienten inte att installera den nya klient program varan. Mer information finns i [så här installerar du Configuration Manager klienter manuellt](../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual).

Mer information om klient installations metoder finns i [Distribuera klienter till Windows-datorer](../clients/deploy/deploy-clients-to-windows-computers.md).

## <a name="windows-defender-configuration-settings"></a>Konfigurations inställningar för Windows Defender

Nu kan du konfigurera inställningar för Windows Defender-klienten på Intune-registrerade Windows 10-datorer med hjälp av konfigurations objekt i Configuration Manager-konsolen.

Mer specifikt kan du konfigurera följande inställningar för Windows Defender:
- Tillåt realtidsövervakning
- Tillåt beteendeövervakning
- Aktivera system för nätverksinspektion
- Skanna alla hämtningar
- Tillåt skriptgenomsökning
- Övervaka fil- och programaktivitet
  - Filer som övervakas
- Dagar som löst skadlig kod ska spåras
- Tillåt användargränssnittåtkomst för klient
- Schemalägg en systemsökning
  - Schemalagd dag
  - Schemalagd tid
- Schemalägg en snabb daglig genomgång
  - Schemalagd tid
- Begränsa CPU-användning% under en skannings genomsökning arkivera filer
- Skanna e-postmeddelanden
- Skanna flyttbara enheter
- Genomsök mappade enheter
- Genomsök filer som öppnats från net-resurser
- Intervall för signaturuppdatering
- Tillåt molnskydd
- Uppmana användarna att ange exempel
- Identifiering av potentiellt oönskade program
- Exkluderade filer/mappar
- Undantagna fil namns tillägg
- Undantagna processer

> [!NOTE]
> De här inställningarna kan bara konfigureras på klient datorer som kör Windows 10 november Update (1511) och senare.

### <a name="try-it-out"></a>prova!

1. I Configuration Manager-konsolen går du **till till gångar och efterlevnad** > **Översikt över** > **Compliance Settings** > kompatibilitetsinställningar**konfigurations objekt**och skapar ett nytt **konfigurations objekt**.
2. Ange ett namn och välj sedan **Windows 8,1 och Windows 10** under **Inställningar för enheter som hanteras utan den Configuration Manager klienten** och klicka på **Nästa**.
3. Se till att **alla Windows 10 (64-bitars)** och **alla windows 10 (32-bitars)** har marker ATS på sidan **plattformar som stöds** och klicka sedan på **Nästa**.
4. Välj gruppen **Windows Defender** -inställningar och klicka sedan på **Nästa**.
5. Konfigurera önskade inställningar på den här sidan och klicka sedan på **Nästa**.
6. Slutför guiden.
7. Lägg till detta konfigurations objekt i en konfigurations bas linje och distribuera den här bas linjen till datorer som kör Windows 10 november Update (1511) eller senare.

> [!NOTE]
> Kom ihåg att markera kryss rutan **Reparera inkompatibla inställningar** när du distribuerar konfigurations bas linjen.

## <a name="request-policy-sync-from-administrator-console"></a>Begär princip synkronisering från administratörs konsolen

Du kan nu begära en princip synkronisering för en mobil enhet från Configuration Manager-konsolen, i stället för att behöva begära en synkronisering från själva enheten. Information om synkroniseringsstatus för begäran är tillgänglig som en ny kolumn i enhets visningar som kallas **fjärrsynkroniseringsstatus**. Tillstånd visas också i avsnittet **identifierings data** i dialog rutan **Egenskaper** för varje mobil enhet.

### <a name="try-it-out"></a>prova!

1. I Configuration Manager-konsolen går du **till till gångar och efterlevnad** > **– Översikt** > enheter.
2. Välj **Skicka synkroniseringsbegäran**i menyn **åtgärder för fjärrenhet** .

Synkroniseringen kan ta fem till tio minuter. Alla ändringar i principen synkroniseras till enheten. Du kan spåra statusen för synkroniseringsbegäran i kolumnen **fjärrsynkroniseringsstatus** i vyn **enheter** eller i enhetens **egenskaps** dialog ruta.

## <a name="additional-security-role-support"></a>Ytterligare säkerhets Rolls stöd

Förutom fullständig administratör har följande inbyggda säkerhets roller nu fullständig åtkomst till objekt i noden **alla företagsägda enheter** , inklusive **fördeklarerade enheter**, **registrerings profiler för iOS**och **Windows registrerings profiler**:
- **Tillgångsansvarig**
- **Åtkomst hanterare för företags resurs**

Skrivskyddad åtkomst till dessa områden i Configuration Manager-konsolen beviljas fortfarande rollen som **skrivskyddad analys** .

## <a name="conditional-access-for-windows-10-vpn-profiles"></a>Villkorlig åtkomst för VPN-profiler i Windows 10

Du kan nu kräva att Windows 10-enheter som har registrerats i Azure Active Directory ska vara kompatibla för att få VPN-åtkomst via Windows 10 VPN-profiler som skapats i Configuration Manager-konsolen. Detta är möjligt med kryss rutan ny **Aktivera villkorlig åtkomst för den här VPN-anslutningen** på sidan **autentiseringsmetod** i guiden VPN-profil och egenskaper för VPN-profil för Windows 10 VPN-profiler. Du kan också ange ett separat certifikat för autentisering med enkel inloggning om du aktiverar villkorlig åtkomst för profilen.

## <a name="see-also"></a>Se även
[Teknisk för hands version för Configuration Manager](../../core/get-started/technical-preview.md)
