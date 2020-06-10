---
title: Ta bort certifikat utfärdare
titleSuffix: Configuration Manager
description: Ta bort den centrala administrations platsen (CAS) för att förenkla din Configuration Manager-infrastruktur till en enda fristående primär plats.
ms.date: 06/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 16975644-8dfa-4f22-b45a-c54a9250dbd2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 237c326c4420aec13ad6c9ca9b07d9f5304b6945
ms.sourcegitcommit: 52dd59bdbad07b414db9e4209da0f4c957cf5d6e
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2020
ms.locfileid: "84613979"
---
# <a name="remove-the-central-administration-site"></a>Ta bort den centrala administrations platsen

*Gäller för: Configuration Manager (aktuell gren)*

<!-- 3607277 -->

Från och med version 2002, om hierarkin består av den centrala administrations platsen (CAS) och en enda underordnad primär plats, kan du ta bort certifikat utfärdarna. Den här åtgärden fören klar din Configuration Manager-infrastruktur till en enda fristående primär plats. Den tar bort de komplexa funktionerna för plats-till-plats-replikering och fokuserar dina hanterings uppgifter på den enskilda platsen.

> [!IMPORTANT]
> I den här versionen av Configuration Manager är den här funktionen för hands version och är inte aktive rad som standard. Den är för närvarande tillgänglig för Microsoft Premier-kunder.
>
> Om du vill aktivera den här funktionen kontaktar du teknisk konto ansvarig för att få hjälp:
>
> - Din TAM öppnar ett råd givande ärende, som kommer att använda dina Microsoft Premier-timmar.
> - Du kan inte ändra ärendets allvarlighets grad.
> - Microsoft Support hjälper de här råd givande fallen under normal, vardags arbets tid.

## <a name="plan"></a>Planera

- Hierarkin måste bestå av certifikat utfärdare och en enda underordnad primär plats. Den primära platsen kan ha sekundära platser. Om du vill ta bort andra underordnade primära platser från hierarkin granskar du planerings stegen och kraven för att [Avinstallera en primär plats](uninstall-sites-and-hierarchies.md#bkmk_primary).

- Kontrol lera att den underordnade primära platsen uppfyller storleks-och skalnings kraven för en [fristående primär plats](../../../plan-design/configs/size-and-scale-numbers.md#bkmk_pri).

- Flytta eller återkalla alla plats roller på certifikat utfärdarna, förutom tjänst anslutnings punkten och program uppdaterings platsen. Configuration Manager-installationen hanterar dessa två roller när du tar bort certifikat utfärdarna.

  Följande roller är de vanligaste på certifikat utfärdarna, som du måste ta ur bruk eller flytta till den primära platsen:

  - Tillgångsinformation plats för synkronisering
  - Plats för slutpunktsskydd
  - Rapporteringstjänstpunkt
  - Informations lager service punkt
  - Cloud Management Gateway (CMG)

    > [!NOTE]
    > Om du har aktiverat CMG för innehåll, bör du planera att distribuera om innehållet när du har återskapat CMG på den primära platsen.<!-- 6608659 -->

- Inaktivera distribuerade vyer

- Configuration Manager hanterar automatiskt paket käll platser för inbyggda paket, t. ex. Configuration Manager-klienten. Granska alla andra platser för innehålls källor för att se till att de inte använder en resurs på certifikat utfärdarna.

- Stoppa eventuella aktiva migreringsjobb och ta bort alla konfigurationer för migrering. Mer information finns i [stoppa aktiv migrering från en annan hierarki](prerequisites-for-installing-sites.md#stop-active-migration-from-another-hierarchy).

- Om du använder regler för automatisk distribution för program uppdateringar måste du återskapa dem på den underordnade primära platsen.

- Om du använder Configuration Manager eller System Center Updates Publisher för att hantera [program uppdateringar från tredje part](../../../../sum/deploy-use/third-party-software-updates.md)exporterar du WSUS-signeringscertifikat från program uppdaterings platsen på CAS.

  - Innan du tar bort certifikat utfärdarna väntar du tills tids gränsen för alla nödvändiga distributioner av program uppdateringar från tredje part. Klienter förladda ned innehåll för nödvändiga distributioner och när du ändrar program uppdaterings platsen ändras innehålls-hashen med *lokal publicering* av program uppdateringar. (Det här beteendet påverkar inte andra innehålls typer, endast lokal publicering av program uppdateringar från tredje part.) Om du tar bort certifikat utfärdarna med de nödvändiga distributionerna som pågår, kommer de inte att kunna köras på klienter med ett hash-matchnings fel.

- Granska program vara från tredje part som kan ha ett beroende på ca: erna.

## <a name="prerequisites"></a>Krav

- Den administrativa användare som kör Configuration Manager-installationen behöver följande säkerhets behörigheter:

  - Lokal **Administratörs** behörighet på CAS-servern

  - Om CAS-databasservern är fjärr från plats servern, lokal **Administratörs** behörighet på fjärrplatsens databas server för CAS.

  - **Sysadmin** -behörighet på CAS-platsdatabasen

  - Lokal **Administratörs** behörighet på den primära plats servern

  - Om den primära platsens databas server är fjärran sluten från den primära plats servern, är lokal **Administratörs** behörighet på fjärrplatsens databas server för den primära platsen.

  - **Sysadmin** -behörighet på den primära plats databasen

  - **Infrastruktur administratör** eller **fullständig administratörs** säkerhets roll på CAS och primär plats

- Endast en underordnad primär plats i hierarkin. Mer information finns i [Avinstallera en primär plats](uninstall-sites-and-hierarchies.md#bkmk_primary).

## <a name="process"></a>Process

1. Starta Configuration Manager-installationen på CAS-servern med någon av följande metoder:

    - På **Start** -menyn väljer du **Configuration Manager installationen**.

    - I katalogen för *installations mediet*för Configuration Manager öppnar du `\SMSSETUP\BIN\X64\setup.exe` . Kontrol lera att den här versionen är samma som plats versionen.

    - I katalogen där Configuration Manager har *installerats*öppnar du `\BIN\X64\setup.exe` .

1. Granska informationen på sidan **innan du börjar** .

1. På sidan **komma igång** väljer du **utför plats underhåll eller Återställ den här platsen**.

1. På sidan **plats underhåll** väljer du **ta bort Central administrations webbplats**. <!-- or is it still "delete"? -->

1. På sidan **Konfigurera om befintliga plats system roller** :

    - **Tjänst anslutnings punkt**: Ange det fullständigt kvalificerade domän namnet för plats systemet på den primära platsen som ska vara värd för den nödvändiga rollen. Mer information finns i [om tjänst anslutnings punkten](../configure/about-the-service-connection-point.md).

    - **Program uppdaterings plats**: Välj en befintlig program uppdaterings plats på den primära platsen. Installations programmet konfigurerar den här program uppdaterings platsen för synkronisering av samma som CAS-konfigurationen.

    Installations programmet kontrollerar att de angivna servrarna uppfyller kraven. Välj **påbörja installation** när du är redo att fortsätta.

Om installations programmet kommer över ett problem kan du använda guiden för att försöka utföra processen igen.

När installationen är klar återställs den primära platsen. Mer information finns i [köra en plats återställning](../../manage/modify-your-infrastructure.md#bkmk_reset).

## <a name="monitor-and-verify"></a>Övervaka och verifiera

Granska följande loggar under installationen:

- `C:\ConfigMgrSetup.log`på CAS-servern

- **hman. log** i katalogen Configuration Manager loggar på den primära plats servern

Använd noden **platshierarki på arbets** ytan **övervakning** för att visualisera ändringarna i hierarkin. Följande bild visar till exempel före och efter-jämförelsen av **vågade** -CAS, **Haw** -primära platsen och **VWT** sekundära plats:

| Före  | Efter   |
|---------|---------|
|![Exempel på platshierarki för en CAS, en primär plats och en sekundär plats](media/3607277-cas-primary-secondary.png)|![Exempel på platshierarki för en primär plats och en sekundär plats](media/3607277-primary-secondary.png)|

## <a name="post-setup-tasks"></a>Uppgifter efter installationen

När du har tagit bort certifikat utfärdarna går du igenom följande steg som gäller för din miljö.

- Ta bort CAS-serverns dator konto manuellt från lokala grupper för primära platser.

- Den betrodda rot nyckeln har ändrats, vilket kan kräva ytterligare åtgärder:

  - Uppdatera start avbildningar för operativ Systems distribution för att inkludera de senaste Configuration Manager binärfilerna.

  - Återskapa [mediet för operativ Systems distribution](../../../../osd/deploy-use/create-task-sequence-media.md).

- Om du ansluter Configuration Manager med [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm?context=configmgr/core/context/core-context)måste du återställa anslutningen. Det första steget för att lösa eventuella problem är att [förnya den hemliga nyckeln](../configure/azure-services-wizard.md#bkmk_renew). Om det inte löser problemet återskapar du anslutningen.<!-- 5584635 -->

- Om du aktiverar synkronisering av Surface-drivrutiner i version 2002 konfigurerar du om den här funktionen när du har tagit bort certifikat utfärdarna. Mer information finns i [uppdateringar för Microsoft-Surface-drivrutiner och inbyggd program vara](../../../../sum/deploy-use/surface-drivers.md).<!-- 5728727 -->

- Om du hanterar program uppdateringar från tredje part:

  1. Exportera WSUS-signeringscertifikat från program uppdaterings platsen på CAS, om du inte redan gjort det.

  1. Innan du skapar nya distributioner tar du bort uppdateringen från befintliga distributioner och program uppdaterings paket.

  1. Om du vill återställa program uppdateringens metadata till ett användbart tillstånd omsynkroniserar du de prenumererade katalogerna. Du kan också vänta på att Configuration Manager omsynkroniseras automatiskt.

  1. Starta eller vänta på att en normal synkronisering av program uppdaterings processen uppdaterar Configuration Manager med aktuell status från WSUS. Du kan också använda SCUP-eller WSUS PowerShell-cmdletar för att ta bort och läsa uppdateringar.

  1. Publicera om innehåll för uppdateringar som du behöver distribuera.
