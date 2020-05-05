---
title: Installera roller för lokal MDM
titleSuffix: Configuration Manager
description: Installera de plats system roller som krävs för lokal hantering av mobila enheter (MDM) i Configuration Manager.
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: c3cf9f64-c2b9-4ace-9527-2aba6d4eef04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f47d78eeafb745732d4917dd7abd80f752f4dd20
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721859"
---
# <a name="install-site-system-roles-for-on-premises-mdm-in-configuration-manager"></a>Installera plats system roller för lokal MDM i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Manager lokal hantering av mobila enheter (MDM) kräver följande plats system roller på din Configuration Manager plats:

- Registreringsplats

- Registreringsproxyplats

- Distributionsplats

- Enhets hanterings plats, som är en hanterings plats som du kan använda för mobila enheter

## <a name="requirements-and-limitations"></a>Krav och begränsningar

- Lokal MDM kräver att du aktiverar plats system roller för HTTPS-kommunikation. Mer information finns i [Konfigurera certifikat för betrodd kommunikation i lokal MDM](set-up-certificates-on-premises-mdm.md).

- Den aktuella grenen av Configuration Manager stöder endast *intranät* anslutningar från enheter till distributions platser och enhets hanterings platser för lokal MDM. Men om du även hanterar macOS-datorer kräver dessa klienter *Internet* anslutningar till samma roller. När du konfigurerar distributions platsen och enhets hanterings platsen använder du alternativet för att **tillåta intranät-och Internet anslutningar**.

- Distributions platser som du konfigurerar för intranät anslutningar kräver att du konfigurerar plats gränser för dem. Configuration Manager stöder endast IPv4-intervall gränser för lokal MDM. Mer information finns i [definiera plats gränser och gräns grupper](../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md).

- Om du använder [databas repliker](../../core/servers/deploy/configure/database-replicas-for-management-points.md) med enhets hanterings platsen kommer nyligen registrerade enheter inte att kunna ansluta. Det här anslutnings felet uppstår eftersom databas repliken inte har informationen om den nyligen registrerade enheten som krävs för en lyckad anslutning. Repliker synkroniseras var femte minut. Enheterna kommer inte att kunna ansluta för de första fem minuterna efter registreringen, vilket vanligt vis är två anslutnings försök. Kommer enheterna att ansluta.

## <a name="add-roles"></a>Lägga till roller

Om du lägger till lokal MDM på en plats som har de flesta enheter som hanteras med Configuration Manager-klienten, kanske du redan har några av de här rollerna installerade på platsen. Distributions platsen är till exempel en gemensam roll och enhets hanterings platsen krävs för att hantera macOS-enheter.

Mer information om hur du lägger till roller på din plats finns i [lägga till plats system roller](../../core/servers/deploy/configure/install-site-system-roles.md).

## <a name="configure-roles"></a>Konfigurera roller

Konfigurera nya eller befintliga roller för att hantera mobila enheter. Följ stegen nedan för att konfigurera distributions platsen och enhets hanterings platsen så att den fungerar korrekt för lokal MDM:

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**och välj noden **servrar och plats system roller** .

1. Välj plats system servern med den distributions plats eller enhets hanterings plats som du vill konfigurera. Välj servern i listan och välj sedan **plats system** rollen i informations fönstret plats system roller. I menyfliksområdet på fliken **plats roll** väljer du **Egenskaper**.

    > [!TIP]
    > På en stor webbplats kan du begränsa vyn till att endast Visa servrar med vissa roller. När du väljer noden **servrar och plats system roller** i menyfliksområdet väljer du **servrar med roll**på Start-taggen. Välj sedan den roll som du vill använda från listan över roller som är tillgängliga på platsen.

    På fliken **Allmänt** i egenskaperna för **plats systemet**ser du till att **namnet** är ett fullständigt kvalificerat domän namn (FQDN). Stäng egenskaperna.

1. I konsol listan väljer du en server med en lokal distributions plats roll. Välj **distributions plats** rollen i informations fönstret plats system roller. I menyfliksområdet på fliken **plats roll** väljer du **Egenskaper**. På fliken **kommunikation** i egenskaperna för **distributions platsen**:

    1. Välj **https**och välj **Tillåt endast anslutningar för intranät**.

        > [!IMPORTANT]
        > Om du också hanterar macOS-datorer med Configuration Manager-klienten använder du **Tillåt intranät-och Internet anslutningar** i stället.

    1. Aktivera alternativet för att **tillåta att mobila enheter ansluter till den här distributions platsen**och stäng sedan egenskaperna.

1. Öppna egenskaper för **hanterings** platsens plats system roll.

    1. På fliken **Allmänt** väljer du **https**och väljer **Tillåt endast anslutningar för intranät**.

        > [!IMPORTANT]
        > Om du också hanterar macOS-datorer med Configuration Manager-klienten använder du **Tillåt intranät-och Internet anslutningar** i stället.

    1. Aktivera alternativet att **tillåta att mobila enheter och Mac-datorer använder den här hanterings platsen**och stäng sedan egenskaperna.

        > [!NOTE]
        > Med det här alternativet aktive ras hanterings platsen i en *enhets* hanterings plats.  

## <a name="next-step"></a>Nästa steg

När du har lagt till och konfigurerat roller för hantering av mobila enheter konfigurerar du servrarna som betrodda slut punkter. Detta förtroende gör att rollerna kan kommunicera med och registrera hanterade enheter.

> [!div class="nextstepaction"]
> [Konfigurera certifikat för betrodd kommunikation](set-up-certificates-on-premises-mdm.md)
