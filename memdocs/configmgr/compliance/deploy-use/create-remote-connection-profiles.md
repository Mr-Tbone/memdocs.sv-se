---
title: Skapa fjärranslutningsprofiler
titleSuffix: Configuration Manager
description: Använd Configuration Manager fjärr anslutnings profiler så att användarna kan fjärrans luta till arbets datorer.
ms.date: 01/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 8c6eabc4-5dda-4682-b03e-3a450e6ef65a
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 1434d7802eb1ed68cb0a575778bdae1e5e99c9ec
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694754"
---
# <a name="remote-connection-profiles-in-configuration-manager"></a>Fjärr anslutnings profiler i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Använd Configuration Manager fjärr anslutnings profiler så att användarna kan fjärrans luta till arbets datorer. Med de här profilerna kan du distribuera Anslutning till fjärrskrivbord inställningar till användare i hierarkin. Användare kan komma åt sina primära arbets datorer via fjärr skrivbord via en VPN-anslutning.  

> [!IMPORTANT]  
> När du anger inställningar för fjärr anslutnings profil med Configuration Manager, lagrar klienten inställningarna i den lokala Windows-principen. De här inställningarna kan åsidosätta inställningar för fjärr skrivbord som du konfigurerar med ett annat program. Om du använder Windows grupprincip för att konfigurera inställningar för fjärr skrivbord åsidosätter de inställningar som anges i grupprincip Configuration Manager inställningar.

Configuration Manager skapar en säkerhets grupp på klienter, **fjärran sluten dator**. När du distribuerar en fjärr anslutnings profil lägger klienten till de primära användarna av datorn i den här gruppen. En lokal administratör kan manuellt lägga till eller ta bort användare i den här gruppen, men Configuration Manager uppdaterar medlemskapet nästa gång den utvärderar profilen.

> [!IMPORTANT]  
> Om tillhörighets förhållandet mellan en användare och en enhet ändras i Configuration Manager inaktive ras fjärr anslutnings profilen och Windows-brandväggens inställningar för att förhindra anslutningar till datorn.

## <a name="prerequisites"></a>Förutsättningar  

### <a name="external-dependencies"></a>Externa beroenden  

- Om du vill att användarna ska kunna ansluta från Internet installerar och konfigurerar du en server för fjärrskrivbordsgateway. Mer information om hur du installerar och konfigurerar en server för Fjärrskrivbordsgateway finns i [Fjärrskrivbordstjänster – åtkomst från var som helst](/windows-server/remote/remote-desktop-services/rds-plan-access-from-anywhere).

- Om klienter kör en värdbaserad brand vägg måste den Aktivera mstsc.exe programmet. När du konfigurerar en fjärr anslutnings profil aktiverar du inställningen för att **tillåta undantag i Windows-brandväggen för anslutningar i Windows-domäner och i privata nätverk**. Med den här inställningen kan Configuration Manager automatiskt konfigurera Windows-brandväggen.

    > [!TIP]
    > Inställningar för grupprincip som konfigurerar Windows-brandväggen kan åsidosätta den konfiguration du anger i Configuration Manager. Om du använder grupprincip för att konfigurera Windows-brandväggen kontrollerar du att grupprincip inställningarna inte blockerar mstsc.exe.

    Om klienterna kör en annan värdbaserad brand vägg konfigurerar du det här brand Väggs beroendet manuellt.  

### <a name="configuration-manager-dependencies"></a>Beroenden i Configuration Manager  

- För att en användare ska kunna ansluta till en arbets dator måste datorn vara en primär enhet för användaren. Mer information finns i [Länka användare och enheter med mappning mellan användare och enhet](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

- För att hantera fjärr anslutnings profiler måste ditt användar konto ha vissa behörigheter i Configuration Manager. Den inbyggda rollen **Compliance Settings Manager** innehåller de behörigheter som krävs för att hantera dessa profiler. Mer information finns i [Konfigurera rollbaserad administration](../../core/servers/deploy/configure/configure-role-based-administration.md).

## <a name="security-and-privacy-considerations"></a>Säkerhets-och sekretess överväganden

### <a name="security-considerations"></a>Säkerhetsöverväganden  

- Definiera mappning mellan användare och enhet manuellt i stället för att tillåta att användarna identifierar sina primära enheter. Aktivera inte användnings-baserad konfiguration.

  - Innan du kan distribuera en fjärr anslutnings profil måste du aktivera alternativet för att tillåta att **alla primära användare av arbets datorn fjärransluter**. Med den här konfigurationen ska du alltid ange mappning mellan användare och enhet manuellt. Överväg inte den information som Configuration Manager samlar in från användare eller från enheten som ska vara auktoritativ. Om du distribuerar en profil och en betrodd administrativ användare inte anger mappning mellan användare och enhet, kan obehöriga användare få utökade privilegier och fjärrans luta till datorer.

  - Configuration Manager samlar in användnings-baserad information via tillstånds meddelanden, vilket är en snabb men osäker kommunikations kanal. För att minimera det här hotet använder du signering med SMB (Server Message Block) eller IPsec (Internet Protocol security) mellan klientdatorer och hanteringsplatsen.

- Begränsa lokala administrativa rättigheter på platsserverdatorn. En lokal administratör på plats servern kan manuellt lägga till medlemmar till den säkerhets grupp för **fjärr PC Connect** som Configuration Manager skapar och underhåller automatiskt. Den här åtgärden kan orsaka en höjning av privilegier eftersom medlemmar får behörigheten fjärr skrivbord.

### <a name="privacy-considerations"></a>Överväganden för sekretess  

När en användare ansluter till en arbets dator via fjärr anslutning, laddar de ned en. wsrdp-fil. Den här filen innehåller enhets namnet och namnet på servern för fjärrskrivbordsgateway. Dessa värden krävs för att skapa fjärrskrivbordssessionen. .wsrdp-filen laddas ned och sparas automatiskt lokalt. Filen skrivs över nästa gång användaren kör en fjärrskrivbordssession.  

## <a name="create-a-profile"></a>Skapa en profil

1. Gå till arbets ytan **till gångar och efterlevnad** i Configuration Manager-konsolen **, expandera kompatibilitetsinställningar och välj** **fjärr anslutnings profiler**.  

1. Välj **skapa fjärr anslutnings profil**i gruppen **skapa** på fliken **Start** i menyfliksområdet.  

1. På sidan **Allmänt** i **guiden skapa fjärr anslutnings profil**anger du ett namn och en valfri beskrivning för profilen. Båda värdena har en övre gräns på 256 tecken.  

1. På sidan **profil inställningar** anger du följande inställningar:  

    - **Fullständigt namn och port för servern för fjärrskrivbordsgateway (valfritt)**: Ange namnet på den server för fjärrskrivbordsgateway som ska användas för anslutningar. Det här värdet har följande krav:

        - Server namnet får inte vara längre än 256 tecken.
        - Det kan innehålla versaler, gemener och numeriska tecken.
        - Förutom punkter ( `.` ) mellan segment och ett kolon ( `:` ) före porten, är de enda specialtecknen ( `–` ) och under streck ( `_` ).
        - Configuration Manager stöder inte användning av ett internationellt domän namn för det här värdet.

    - **Tillåt bara anslutningar från datorer som kör fjärr skrivbord med autentisering på nätverksnivå**: aktiverat som standard lägger den här inställningen till ytterligare en säkerhets nivå för anslutningen. Mer information finns i [bevilja åtkomst till fjärr skrivbord](/windows-server/remote/remote-desktop-services/clients/remote-desktop-allow-access#why-allow-connections-only-with-network-level-authentication).

    - Aktivera följande anslutnings inställningar:

        - **Tillåt fjärranslutningar till arbetsdatorer**

        - **Tillåt att alla primära användare av arbetsdatorer fjärransluter**

        - **Tillåt undantag i Windows-brandväggen för anslutningar i Windows-domäner och i privata nätverk**

        > [!IMPORTANT]  
        > Alla tre inställningarna måste vara desamma innan du kan fortsätta.

        Inaktivera bara de här inställningarna när du distribuerar en profil för att stänga av fjärr anslutningar.

1. Slutför guiden.

Den nya profilen visas i noden **fjärr anslutnings profiler** på arbets ytan **till gångar och efterlevnad** .  

## <a name="deploy"></a>Distribuera

1. Gå till arbets ytan **till gångar och efterlevnad** i Configuration Manager-konsolen **, expandera kompatibilitetsinställningar och välj** **fjärr anslutnings profiler**.

1. I listan **fjärr anslutnings profiler** väljer du den profil som du vill distribuera. På fliken **Start** i menyfliksområdet väljer du **distribuera**i gruppen **distribution** .  

1. I fönstret **distribuera fjärr anslutnings profil** anger du följande information:

    - **Samling**: Bläddra och välj den enhets samling där du vill distribuera profilen.

    - **Reparera inkompatibla regler när stöd**finns: Aktivera den här inställningen om du vill reparera profil inställningarna automatiskt när de inte är kompatibla på en enhet. Profilen kan vara icke-kompatibel när den inte finns.

    - **Tillåt reparation utanför underhålls fönstret**: om du konfigurerar en underhålls period för den samling som du distribuerar profilen till aktiverar du det här alternativet för att låta Configuration Manager åtgärda det utanför underhålls fönstret. Mer information finns i [använda underhålls](../../core/clients/manage/collections/use-maintenance-windows.md)perioder.

    - **Generera en varning**: aktivera det här alternativet om du vill konfigurera en avisering om efterlevnad.

    - **Ange schema för utvärdering av kompatibilitet för denna konfigurations bas linje**: Ange ett enkelt eller anpassat schema som klienten utvärderar profilen i.

1. Välj **OK** för att stänga fönstret och skapa distributionen.

### <a name="client-evaluation"></a>Klient utvärdering

Klienten utvärderar profilen när en användare loggar in.

Om en enhet lämnar en samling som du distribuerar en fjärr anslutnings profil från, inaktiverar Configuration Manager inställningarna på enheten. För att den här processen ska ske korrekt ska du redan ha distribuerat minst ett konfigurationsobjekt eller en konfigurationsbaslinje som innehåller ett konfigurationsobjekt från din webbplats.

### <a name="conflict-resolution"></a>Konfliktlösning

Distribuera inte fler än en fjärr anslutnings profil med motstridiga inställningar till samma enhet. Du kan till exempel distribuera två profiler med olika inställningar till samma samling. Du konfigurerar bara en profil distribution för att **Reparera inkompatibla regler när detta stöds**. Den här distributionen kan åsidosätta inställningarna i den andra profilen. Configuration Manager stöder inte den här typen av distribution av fjärr anslutnings profiler.

## <a name="monitor"></a>Övervaka

I Configuration Manager-konsolen går du till arbets ytan **övervakning** och väljer **distributioner**. I listan **distributioner** väljer du distributionen av fjärr anslutnings profilen.

Översiktlig kompatibilitetsinformation om fjärranslutningsprofilens distribution visas på huvudsidan. Välj profil distributionen om du vill visa mer detaljerad information. Välj sedan **Visa status**i gruppen **distribution** på fliken **Start** i menyfliksområdet. Den här åtgärden öppnar sidan **distributions status** .  

På sidan **Distributionsstatus** finns följande flikar:  

- **Kompatibel**: visar fjärr anslutnings profilens kompatibilitet baserat på antalet till gångar som påverkas.

    > [!IMPORTANT]  
    > Klienten utvärderar inte en fjärr anslutnings profil om den inte är tillämplig. Men rapporterar fortfarande kompatibel.

- **Fel**: visar en lista över alla fel för den valda fjärr anslutnings profil distributionen baserat på antalet till gångar som påverkas.

- **Icke-kompatibel**: visar en lista över alla inkompatibla regler i fjärr anslutnings profilen baserat på antalet till gångar som påverkas.

- **Okänd**: visar en lista över alla enheter som inte rapporterades som kompatibla för den valda fjärr anslutnings profil distributionen, tillsammans med enheternas aktuella klient status.

På någon flik öppnar du en regel för att skapa en tillfällig undernoden under noden **användare** i arbets ytan **till gångar och efterlevnad** . Den här undernoden innehåller alla enheter med kompatibilitetstillstånd för den valda fliken.

I fönstret **till gångs Detaljer** visas enheterna med det valda kompatibilitetstillstånd för den här profilen. Öppna en enhet i listan om du vill visa mer information.

## <a name="reports"></a>Rapporter

Configuration Manager innehåller inbyggda rapporter som du kan använda för att övervaka information om fjärr anslutnings profiler. De här rapporterna tillhör rapportkategorin **Hantering av efterlevnad och inställningar**.  

> [!IMPORTANT]  
> Använd jokertecknet ( `%` ) när du använder parametrarna **enhets filter** och **användar filter** i rapporterna för kompatibilitetsinställningar.  

Mer information om hur du konfigurerar rapportering i Configuration Manager finns i [Introduktion till rapportering](../../core/servers/manage/introduction-to-reporting.md).