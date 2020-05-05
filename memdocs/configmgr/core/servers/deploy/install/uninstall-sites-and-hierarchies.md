---
title: Avinstallera platser
titleSuffix: Configuration Manager
description: En guide för att ta bort roller och avinstallera platser och hierarkier
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d466edd2-97f0-44c1-a73e-d71abbdbf4a8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a90d6f34370b8c3167272bce1a0a673cc5074094
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718051"
---
# <a name="uninstall-roles-sites-and-hierarchies-in-configuration-manager"></a>Avinstallera roller, platser och hierarkier i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Använd den här artikeln som en guide för att avinstallera en Configuration Manager plats system roll, plats eller hierarki.

Från och med version 2002 kan du också ta bort den centrala administrations platsen (CAS) från en hierarki, men behålla den primära platsen.

## <a name="site-system-role"></a><a name="bkmk_role"></a>Plats system roll

Du kanske vill ta bort en roll från en plats system Server av följande anledningar:

- Större infrastruktur förändringar, till exempel nätverks-eller fysiska platser
- Inaktivera den underliggande servern
- Konsolidera roller för att minska kostnaderna och komplexiteten
- Konfigurera om eller ändra design på plats rollerna
- Avbryt användningen av funktionen som rollen stöder

När du bestämmer dig för att ta bort en roll måste du först tänka på dina svar på följande frågor:

- Behöver du fortfarande rollen på platsen? I så fall, har ett annat plats system redan rollen?

- Har andra plats system med den här rollen rätt storlek för att stödja företagets behov av prestanda och tillgänglighet?

- Har alla klienter redan kon figurer ATS om att använda en annan roll? Kommer du att förlita dig på standard klient beteenden för att komma tillbaka eller identifiera en annan server?

### <a name="procedure-to-remove-a-site-system-role"></a>Procedur för att ta bort en plats system roll

Använd följande procedur för att ta bort en roll:

1. Gå till arbets ytan **Administration** i **Configuration Manager** -konsolen. Expandera **plats konfiguration**och välj noden **servrar och plats system roller** .

1. Välj den plats system server med rollen som ska tas bort. I informations fönstret **plats system roller** väljer du mål rollen.

1. I menyfliksområdet på fliken **plats roll** i gruppen **plats roll** väljer du **ta bort roll**. Bekräfta att du vill ta bort rollen.

### <a name="additional-information-for-specific-roles"></a>Ytterligare information för vissa roller

Vissa roller kan ha ytterligare steg och överväganden.

#### <a name="software-update-point"></a>Programuppdateringsplats

När du har tagit bort program uppdaterings platsen uppdaterar Configuration Manager klient principen för att ta bort program uppdaterings platsen från listan. När du tar bort den senaste program uppdaterings platsen på platsen innehåller listan över program uppdaterings platser inga program uppdaterings platser. Om det inte finns några tillgängliga roller är hantering av program uppdateringar i princip inaktiverat på platsen.

Om du har fler än en program uppdaterings plats på en primär plats och du tar bort program uppdaterings platsen som är synkroniseringens källa väljer du en annan plats för program uppdatering på platsen som ska vara den nya synkroniserings källan.

## <a name="secondary-site"></a><a name="bkmk_secondary"></a>Sekundär plats  

Förutom när du [inaktiverar en-hierarki](#bkmk_hierarchy)beror det huvudsakliga skälet till att ta bort en sekundär plats på grund av en bredare infrastruktur ändring, till exempel nätverk eller fysiska platser. Granska även skälen till att [välja en sekundär plats](../../../plan-design/hierarchy/design-a-hierarchy-of-sites.md#BKMK_ChooseSecondary).

När du bestämmer dig för att ta bort en sekundär plats måste du först tänka på dina svar på följande frågor:

- Har du tagit bort alla plats system roller från plats servern?

- Är alla gränser eller gräns grupper kopplade till den sekundära platsen? Konfigurera om gränser innan du tar bort platsen.

- Finns det kvar några klienter på platsen?

- Har du konfigurerat andra alternativ för innehålls hantering som [peer-cachelagring](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#peer-caching-technologies)?

### <a name="options-to-delete-secondary-sites"></a>Alternativ för att ta bort sekundära platser

Det går inte att flytta eller omtilldela en sekundär plats till en annan primär plats. När du tar bort en sekundär plats från dess direkta överordnade plats väljer du om du vill avinstallera eller ta bort den.

#### <a name="uninstall-the-secondary-site"></a>Avinstallera den sekundära platsen

Använd det här alternativet om du vill ta bort en fungerande sekundär plats som är tillgänglig från nätverket. Med det här alternativet avinstalleras Configuration Manager från den sekundära plats servern. Sedan tas all information om platsen och dess resurser bort från Configuration Manager-platsen.

Om Configuration Manager installerade SQL Server Express för den sekundära platsen Configuration Manager avinstallerar även SQL Express. Om du har installerat SQL Server Express innan du installerade den sekundära platsen Configuration Manager avinstallera inte SQL Server Express.

#### <a name="delete-the-secondary-site"></a>Ta bort den sekundära platsen

Använd det här alternativet i följande situationer:

- Det gick inte att installera

- När du har avinstallerat det visar Configuration Manager-konsolen fortfarande den sekundära platsen

    Med det här alternativet raderas all information om platsen och dess resurser från Configuration Manager-hierarkin, men inga ändringar görs på plats servern.

    > [!TIP]
    >  Du kan också använda verktyget underhåll av hierarki med alternativet **/DELSITE** för att ta bort en sekundär plats. Mer information finns i [verktyget underhåll av hierarki (Preinst. exe)](../../manage/hierarchy-maintenance-tool-preinst.exe.md).

### <a name="prerequisites-to-delete-a-secondary-site"></a>Krav för att ta bort en sekundär plats

Den administrativa användare som kör Configuration Manager-installationen behöver följande säkerhets behörigheter:

- Lokal **Administratörs** behörighet på den sekundära plats servern

- Om den primära platsens databas server är fjärran sluten från den primära plats servern, är lokal **Administratörs** behörighet på fjärrplatsens databas server för den primära platsen.

- **Infrastruktur administratör** eller säkerhets rollen **Fullständig administratör** på den överordnade primära platsen

- **Sysadmin** -behörighet på den sekundära platsens databas

### <a name="procedure-to-delete-a-secondary-site"></a>Procedur för att ta bort en sekundär plats

Använd följande procedur för att avinstallera eller ta bort en sekundär plats:

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**och välj noden **platser** .

1. Välj den sekundära plats server som du vill ta bort. I menyfliksområdet på fliken **Start** i gruppen **plats** väljer du **ta bort**.

1. På sidan **Allmänt** väljer du om du vill avinstallera eller ta bort den sekundära platsen.

1.  Slutför guiden.

## <a name="primary-site"></a><a name="bkmk_primary"></a>Primär plats  

Du kanske vill avinstallera en primär plats från hierarkin av följande skäl:

- Konsolidera platser för att minska kostnaderna och komplexiteten
- Konfigurera om eller designa om platser i hierarkin

Innan du avinstallerar en underordnad primär plats som använder [distribuerade vyer](../../../plan-design/hierarchy/database-replication.md#bkmk_distviews) för dess replikeringslänk till certifikat utfärdarna ska du först stänga av distribuerade vyer i hierarkin. Mer information finns under [Avinstallera en primär plats som är konfigurerad med distribuerade vyer](#bkmk_distviews).

### <a name="plan-to-uninstall-a-primary-site"></a><a name="bkmk_pri-plan"></a>Planera att avinstallera en primär plats

Innan du avinstallerar en primär plats bör du gå igenom följande uppgifter:

- Granska gränser, gräns grupper och återställnings relationer. Om du tilldelar klienter till en ny plats, men inte ändrar gränserna, kan de betraktas som nätverks växling. Mer information finns i [definiera plats gränser och gräns grupper](../configure/define-site-boundaries-and-boundary-groups.md).

- Se till att alla aktiva klienter omtilldelas till en annan primär plats i hierarkin. Annars kommer klienterna att bli ohanterade när du har avinstallerat platsen. Mer information finns i [tilldela klienter till en plats](../../../clients/deploy/assign-clients-to-a-site.md).

  - Granska listan över plats roller för att se till att den nya platsen tillhandahåller samma tjänste nivå.

  - Kontrol lera att du har angett rätt storlek på de andra plats systemen med den här rollen på den andra platsen. De behöver stöd för dina verksamhets krav för prestanda och tillgänglighet med ytterligare klienter.

  - Om den här platsen har många klienter tilldelar du om dem i steg. Övervaka databasreplikering när klienter uppdaterar fullständig inventering och andra sitespecifika data. Om du hanterar program uppdateringar tilldelas klienter till en ny program uppdaterings plats. Detta medför en fullständig genomsökning av kompatibiliteten för uppdateringar.

  - Omtilldelning av klienter kan påverka rapporter och frågor som förlitar sig på inventerings data och tillstånds beroende efterlevnad. Överväg att tillfälligt justera alla klienters cykler under över gången.

  - Granska alla klient tilldelnings metoder för att se till att ingen refererar till den här primära platsen.

- Kontrol lera om alla aktivt använda objekt i hierarkin har statiska referenser till plats koden. Till exempel samlings frågor, aktivitetssekvenser eller administrativa skript.

- Om hierarkin använder en [återställnings plats](../configure/boundary-group-procedures.md#bkmk_site-fallback) för automatisk platstilldelning kontrollerar du att den inte refererar till den primära platsen.

- Konfigurera om alla [klient installations metoder](../../../clients/deploy/plan/client-installation-methods.md) som kan referera till en statisk platskod.

- Om den primära platsen har några platsspecifika molnbaserade moln tjänster, se till att ta bort dem. Om du fortfarande behöver moln resurserna flyttar du dem till en annan primär plats i hierarkin. Ta bort dem från den primära platsen som du ska avinstallera och Lägg till dem till en annan primär plats.

- Om den primära platsen har [identifierings metoder](../configure/run-discovery.md) för hierarkin flyttar du dem till en annan plats.

- Dra tillbaka alla platsbaserade [operativ Systems distributions medier](../../../../osd/deploy-use/create-task-sequence-media.md).

- Avinstallera alla plats system roller från platsen och plats servern. Mer information finns i [Avinstallera plats system roller](#bkmk_role). Även om det här förberedelse steget inte krävs, hjälper det att identifiera eventuella ytterligare beroenden innan du avinstallerar platsen.

- Avinstallera alla sekundära platser under den här primära platsen. Mer information finns i avsnittet [sekundär plats](#bkmk_secondary) .

### <a name="prerequisites-to-uninstall-a-primary-site"></a><a name="bkmk_pri-prereq"></a>Krav för att avinstallera en primär plats

Den administrativa användare som kör Configuration Manager-installationen behöver följande säkerhets behörigheter:

- Lokal **Administratörs** behörighet på CAS-servern

- Om CAS-databasservern är fjärr från plats servern, lokal **Administratörs** behörighet på fjärrplatsens databas server för CAS.

- **Sysadmin** -behörighet på CAS-platsdatabasen

- Lokal **Administratörs** behörighet på den primära plats servern

- Om den primära platsens databas server är fjärran sluten från den primära plats servern, är lokal **Administratörs** behörighet på fjärrplatsens databas server för den primära platsen.

- **Infrastruktur administratör** eller säkerhets rollen **Fullständig administratör** på CAS

### <a name="procedure-to-uninstall-a-primary-site"></a><a name="bkmk_pri-process"></a>Procedur för att avinstallera en primär plats

Du kör Configuration Manager installations programmet för att avinstallera en primär plats som inte har en associerad sekundär plats. Använd följande procedur för att avinstallera en primär plats:

> [!TIP]
> Om den primära plats servern inte längre är tillgänglig använder du verktyget underhåll av hierarki på certifikat utfärdaren för att ta bort den primära platsen från plats databasen. Mer information finns i [verktyget underhåll av hierarki (Preinst. exe)](../../manage/hierarchy-maintenance-tool-preinst.exe.md).

1. Starta Configuration Manager-installationen på den primära plats servern med någon av följande metoder:

    - På **Start** -menyn väljer du **Configuration Manager installationen**.

    - I katalogen för *installations mediet*för Configuration Manager öppnar `\SMSSETUP\BIN\X64\setup.exe`du. Kontrol lera att den här versionen är samma som plats versionen.

    - I katalogen där Configuration Manager har *installerats*öppnar `\BIN\X64\setup.exe`du.

1. Granska informationen på sidan **innan du börjar** .

1. På sidan **komma igång** väljer du **Avinstallera en Configuration Manager plats**.

    > [!IMPORTANT]  
    >  Om en sekundär plats är kopplad till den primära platsen måste du ta bort den sekundära platsen innan du kan avinstallera den primära platsen.  

1. På sidan **avinstallera Configuration Manager webbplats** är båda följande alternativ aktiverade som standard:

    - Ta bort plats databasen från den primära plats servern
    - Ta bort Configuration Manager-konsolen

1. Välj **Ja** för att bekräfta avinstallationen av Configuration Manager primära platsen.

### <a name="uninstall-a-primary-site-that-uses-distributed-views"></a><a name="bkmk_distviews"></a>Avinstallera en primär plats som använder distribuerade vyer

1. Innan du avinstallerar en underordnad primär plats inaktiverar du distribuerade vyer på varje länk i hierarkin mellan certifikat utfärdarna och en primär plats.

1. När du har stängt av distribuerade vyer på varje länk bekräftar du att data från den primära platsen har slutförts genom att initiera på certifikat utfärdaren. Information om hur du övervakar data initiering finns i [övervaka replikering](../../manage/monitor-replication.md).

1. När data har initierats med certifikat utfärdarna kan du [avinstallera den primära platsen](#bkmk_pri-process).

1. När den primära platsen har avinstallerats kan du konfigurera om distribuerade vyer på länkar från certifikat utfärdarna till andra primära platser.

    > [!IMPORTANT]
    > Om du avinstallerar den primära platsen innan du inaktiverar distribuerade vyer på varje plats, eller innan data från den primära platsen har initierats på certifikat utfärdarna, kan datareplikeringen Miss lyckas.

## <a name="decommission-a-hierarchy"></a><a name="bkmk_hierarchy"></a>Ta en hierarki ur drift

Vissa organisationer har flera hierarkier på grund av sammanslagningar, förvärv, test miljöer eller andra affärs behov. Om du konsoliderar hantering till en enda hierarki kan den här åtgärden hjälpa till att minska kostnaderna och komplexiteten. Ett annat skäl till att inaktivera hierarkin är att du migrerar till en molnbaserad hanterings tjänst, till exempel Microsoft Intune, och är redo att ta bort den lokala infrastrukturen.

Om du vill inaktivera en hierarki med flera platser är borttagnings ordningen viktig. Börja med att avinstallera platserna längst ned i hierarkin och flytta sedan uppåt:

1. Ta bort sekundära platser som är kopplade till primära platser.
2. Avinstallera primära platser.
3. När du har avinstallerat alla primära platser kan du avinstallera certifikat utfärdarna.

Mer information finns i följande avsnitt:

- [Ta bort en sekundär plats](#bkmk_secondary)
- [Avinstallera en primär plats](#bkmk_primary)
- [Avinstallera CAS](#bkmk_uninstall-cas)

### <a name="uninstall-the-cas"></a><a name="bkmk_uninstall-cas"></a>Avinstallera CAS

Det sista steget för att inaktivera en hierarki är att avinstallera CAS. Kör Configuration Manager installations programmet för att avinstallera de certifikat utfärdare som inte har underordnade primära platser.

#### <a name="prerequisites-to-uninstall-the-cas"></a>Krav för att avinstallera CAS

Den administrativa användaren som kör Configuration Manager-installationen behöver följande säkerhets behörigheter:

- Lokal **Administratörs** behörighet på CAS-servern

- Om CAS-databasservern är fjärr från plats servern, lokal **Administratörs** behörighet på fjärrplatsens databas server för CAS.

#### <a name="procedure-to-uninstall-the-cas"></a>Procedur för att avinstallera CAS

1. Starta Configuration Manager-installationen på CAS-servern med någon av följande metoder:

    - På **Start** -menyn väljer du **Configuration Manager installationen**.

    - I katalogen för *installations mediet*för Configuration Manager öppnar `\SMSSETUP\BIN\X64\setup.exe`du. Kontrol lera att den här versionen är samma som plats versionen.

    - I katalogen där Configuration Manager har *installerats*öppnar `\BIN\X64\setup.exe`du.

1. Granska informationen på sidan **innan du börjar** .

1. På sidan **komma igång** väljer du **Avinstallera en Configuration Manager plats**.

    > [!IMPORTANT]  
    >  Ta bort alla underordnade primära platser innan du kan avinstallera certifikat utfärdarna.  

1. På sidan **avinstallera Configuration Manager webbplats** är båda följande alternativ aktiverade som standard:

    - Ta bort plats databasen från CAS-servern
    - Ta bort Configuration Manager-konsolen

1. Välj **Ja** för att bekräfta avinstallationen av Configuration Manager centrala administrations platsen (CAS).

## <a name="remove-the-cas"></a><a name="bkmk_remove-cas"></a>Ta bort CAS

<!-- 3607277 -->

Från och med version 2002, om hierarkin består av certifikat utfärdare och en enda underordnad primär plats, kan du ta bort certifikat utfärdarna. Den här åtgärden fören klar din Configuration Manager-infrastruktur till en enda fristående primär plats. Den tar bort de komplexa funktionerna för plats-till-plats-replikering och fokuserar dina hanterings uppgifter på den enskilda platsen.

Mer information finns i [ta bort CAS](remove-central-administration-site.md).
