---
title: Integrera Windows Update för företag
titleSuffix: Configuration Manager
description: Använd Windows Update for Business (WUfB) för att hålla Windows 10 uppdaterat för enheter som är anslutna till Windows Update-tjänsten.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/07/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 183315fe-27bd-456f-b2c5-e8d25e05229b
ms.openlocfilehash: 8ea95a04977038514c00f0199df42c8070e813c3
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127662"
---
# <a name="integrate-with-windows-update-for-business"></a>Integrera med Windows Update för företag

*Gäller för: Configuration Manager (aktuell gren)*

Windows Update for Business (WUfB) gör att du kan hålla Windows 10-baserade enheter i din organisation alltid uppdaterade med de senaste säkerhets försvars-och Windows-funktionerna när dessa enheter ansluter direkt till tjänsten Windows Update (WU). Configuration Manager kan skilja mellan Windows 10-datorer som använder WUfB och WSUS för att hämta program uppdateringar.  

> [!WARNING]
> Om du använder samhantering för dina enheter och du har flyttat [Windows Update-principerna](../../comanage/workloads.md#windows-update-policies) till Intune, kommer dina enheter att få sina [Windows Update för affärs principer från Intune](https://docs.microsoft.com/intune/windows-update-for-business-configure).
> - Om Configuration Manager-klienten fortfarande är installerad på den samhanterade enheten, hanteras inställningarna för kumulativa uppdateringar och funktions uppdateringar av Intune. Uppdatering av tredje part, om aktive rad i [**klient inställningar**](../../core/clients/deploy/about-client-settings.md#enable-third-party-software-updates), hanteras dock fortfarande av Configuration Manager.  

 Vissa Configuration Manager-funktioner är inte längre tillgängliga när Configuration Manager-klienter har kon figurer ATS för att ta emot uppdateringar från WU, som omfattar WUfB eller Windows Insiders:  

- Efterlevnadsrapportering för Windows Update:  
  - Configuration Manager kommer inte att vara medveten om uppdateringarna som publiceras på WU. De Configuration Manager-klienter som kon figurer ATS för att ta emot uppdateringar från WU kommer att visa **okända** för de här uppdateringarna i Configuration Manager-konsolen.  

  - Fel sökning av övergripande kompatibilitetsstatus är svårt eftersom **okänd** status endast var för klienter som inte hade rapporterade genomsöknings statusen tillbaka från WSUS. Nu omfattar det även Configuration Manager-klienter som tar emot uppdateringar från WU.  

  - Kompatibilitet för definitions uppdateringar är en del av den övergripande uppdateringen av kompatibilitet och fungerar inte som förväntat.

- Övergripande Endpoint Protection rapportering för Defender baserat på uppdateringens kompatibilitetsstatus returnerar inte korrekta resultat på grund av de data som saknas.  

- Configuration Manager kan inte distribuera Microsoft-uppdateringar, till exempel Microsoft 365 appar, IE och Visual Studio till klienter som är anslutna till WUfB för att ta emot uppdateringar.  

- Configuration Manager kan fortfarande distribuera uppdateringar från tredje part som publiceras i WSUS och hanteras via Configuration Manager till klienter som är anslutna till WUfB för att ta emot uppdateringar. Om du inte vill att uppdateringar från tredje part ska installeras på klienter som ansluter till WUfB inaktiverar du klient inställningen [Aktivera program uppdateringar på klienter](../../core/clients/deploy/about-client-settings.md#software-updates).

- Configuration Manager fullständig klient distribution som använder infrastrukturen för program uppdateringar fungerar inte för klienter som är anslutna till WUfB för att ta emot uppdateringar.  

## <a name="identify-clients-that-use-wufb-for-windows-10-updates"></a>Identifiera klienter som använder WUfB för Windows 10-uppdateringar

Använd följande procedur för att identifiera klienter som använder WUfB för att hämta uppdateringar och uppgraderingar för Windows 10. Konfigurera sedan dessa klienter att sluta använda WSUS för att hämta uppdateringar och distribuera en klient agent inställning för att inaktivera arbets flödet för program uppdateringar för dessa klienter.  

### <a name="prerequisites-for-wufb"></a>Krav för WUfB

- Klienter som kör Windows 10 Desktop Pro eller Windows 10 Enterprise Edition version 1511 eller senare

- [Windows Update för företag](https://docs.microsoft.com/windows/deployment/update/waas-manage-updates-wufb) har distribuerats och klienterna använder WUfB för att hämta Windows 10-uppdateringar och -uppgraderingar.  

### <a name="to-identify-clients-that-use-wufb"></a>Identifiera klienter som använder WUfB  

1. Se till att Windows Updates agent inte genomsöker mot WSUS, om den tidigare har Aktiver ATS. Följande register nyckel kan användas för att ange om datorn ska genomsökas mot WSUS eller Windows Update. Om register nyckeln inte finns genomsöks den inte mot WSUS.
    - **HKEY_LOCAL_MACHINE \SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\UseWUServer**
1. Det finns ett nytt attribut, **UseWUServer**, under noden **Windows Update** i Configuration Manager Resursläsaren.
1. Skapa en samling som bygger på attributet **UseWUServer** för alla datorer som är anslutna via WUfB för uppdateringar och uppgraderingar. Du kan skapa en samling baserat på en fråga som liknar den som visas nedan:  

    ```wql
    Select sr.* from SMS_R_System as sr join SMS_G_System_WINDOWSUPDATE as su on sr.ResourceID=su.ResourceID where su.UseWUServer is null
    ```

1. Skapa en klient agent inställning för att inaktivera arbets flödet för program uppdatering. Distribuera inställningen till den samling datorer som är anslutna direkt till WUfB.
1. De datorer som hanteras via WUfB visas som **okända** i kompatibilitetsstatus och räknas inte som en del av den övergripande kompatibiliteten i procent.  

## <a name="configure-windows-update-for-business-deferral-policies"></a>Konfigurera Windows Update för principer för avstängning av företag
<!-- 1290890 -->
Från och med Configuration Manager version 1706 kan du konfigurera uppskjutnings principer för Windows 10-funktions uppdateringar eller kvalitets uppdateringar för Windows 10-enheter som hanteras direkt av Windows Update för företag. Du kan hantera uppskjutnings principerna i noden nya **Windows Update för affärs principer** under **program varu bibliotek**  >  **Windows 10-Underhåll**.

> [!NOTE]
> Från och med Configuration Manager version 1802 kan du ange regler för avstängning för Windows Insider. <!--507201-->  
Mer information om Windows Insider program finns i [komma igång med Windows Insider program för företag](https://docs.microsoft.com/windows/deployment/update/waas-windows-insider-for-business).

### <a name="prerequisites-for-deferral-policies"></a>Krav för regler för avstängning

- Windows 10 version 1703 eller senare
- Windows 10-enheter som hanteras av Windows Update för företag måste ha Internet anslutning

#### <a name="to-create-a-windows-update-for-business-deferral-policy"></a>Så här skapar du en princip för avstängning av Windows Update för företag

1. I **program varu biblioteket**  >  **Windows 10 Servicing**  >  **Windows Update for Business policies**
1. På fliken **Start** går du till gruppen **skapa** och väljer **skapa Windows Update för företag** för att öppna guiden skapa Windows Update för företag-princip.
1. På sidan **Allmänt** anger du ett namn och en beskrivning för principen.
1. På sidan **regler för avstängning** anger du om du vill skjuta upp eller pausa funktions uppdateringar. Funktionsuppdateringarna är för det mesta nya funktioner i Windows. När du har konfigurerat inställningen **gren beredskaps nivå** kan du definiera om, och hur länge, du vill skjuta upp att ta emot funktions uppdateringar efter deras tillgänglighet från Microsoft.
    - **Gren beredskaps nivå**: Ange den gren för vilken enheten ska ta emot Windows-uppdateringar. Välj antingen halvårs kanal (riktad), halvårs kanal eller en Windows Insider-version.

        > [!NOTE]
        > Distribuera principer för **halvårs kanal (riktad)** till Windows 10, *version 1903 eller senare*. Distribuera principer för **halvårs kanal** till Windows 10, *version 1809 eller tidigare*.
        >
        > Om du distribuerar en princip för **halvårs kanal** till Windows 10, version 1903 eller senare, Miss lyckas distributionen med fel **0x8004100c**.<!-- 5593139 -->

    - Uppskjutnings **period (dagar)**: Ange antalet dagar som funktions uppdateringar ska skjutas upp. Du kan skjuta upp att ta emot dessa funktions uppdateringar i upp till 365 dagar från deras version.
    - **Pausa funktioner uppdateringar startar**: Välj om du vill pausa enheter från att ta emot funktions uppdateringar i upp till 35 dagar från den tidpunkt då du pausar uppdateringarna. Efter det att det maximala antalet pausdagar har passerat upphör funktionen automatiskt och enheten söker efter tillämpliga uppdateringar på Windows Update. Efter den här sökningen kan du pausa uppdateringarna igen. Du kan avbryta pausen av funktions uppdateringar genom att avmarkera kryss rutan.
1. Välj om du vill skjuta upp eller pausa kvalitets uppdateringar. Kvalitetsuppdateringar utgörs vanligtvis av korrigeringar och förbättringar av befintliga Windows-funktioner, och publiceras vanligtvis den första tisdagen varje månad, men Microsoft kan publicera dem när som helst. Du kan ange om, och hur länge, du vill skjuta upp mottagandet av kvalitetsuppdateringar från det att de har gjorts tillgängliga.
    - Uppskjutnings **period (dagar)**: Ange antalet dagar som kvalitets uppdateringar ska skjutas upp. Du kan skjuta upp att ta emot dessa kvalitets uppdateringar i upp till 30 dagar från lanseringen.
    - **Pausa kvalitets uppdateringar**från: Välj om du vill pausa enheter från att ta emot kvalitets uppdateringar i upp till 35 dagar från den tidpunkt då du pausar uppdateringarna. Efter det att det maximala antalet pausdagar har passerat upphör funktionen automatiskt och enheten söker efter tillämpliga uppdateringar på Windows Update. Efter den här sökningen kan du pausa uppdateringarna igen. Du kan avbryta kvalitets uppdateringar genom att avmarkera kryss rutan.
1. Välj **Installera uppdateringar från andra Microsoft-produkter** för att aktivera grup princip inställningen som gör uppskjutnings inställningar tillämpliga på Microsoft Update, samt Windows-uppdateringar.
1. Välj **Inkludera driv rutiner med Windows Update** för att automatiskt uppdatera driv rutiner från Windows-uppdateringar. Om du avmarkerar den här inställningen laddas inte driv rutins uppdateringar ned från Windows-uppdateringar.
1. Slutför guiden för att skapa den nya avstängnings principen.

#### <a name="to-deploy-a-windows-update-for-business-deferral-policy"></a>Så här distribuerar du en princip för avstängning av Windows Update för företag

1. I **program varu biblioteket**  >  **Windows 10 Servicing**  >  **Windows Update for Business policies**
1. På fliken **Start** går du till gruppen **distribution** och väljer **distribuera Windows Update for Business-princip**.
1. Konfigurera följande inställningar:
    - **Konfigurations princip som ska distribueras**: välj den Windows Update för företags princip som du vill distribuera.
    - **Samling**: Klicka på **Bläddra** och välj den samling där du vill distribuera principen.
    - **Tillåt reparation utanför underhålls fönstret**: om en underhålls period har kon figurer ATS för den samling som du distribuerar principen till aktiverar du det här alternativet för att låta princip inställningar reparera värdet utanför underhålls perioden. Mer information om underhålls perioder finns i [använda underhålls](../../core/clients/manage/collections/use-maintenance-windows.md)perioder.
    - **Schema**: Ange det schema för utvärdering av kompatibilitet som den distribuerade principen utvärderas på klient datorer. Schemat kan vara ett enkelt eller ett anpassat schema.
1. Distribuera principen genom att slutföra guiden.
