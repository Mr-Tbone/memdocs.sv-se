---
title: Använda PXE för OSD över nätverket
titleSuffix: Configuration Manager
description: Använd PXE-initierade operativ Systems distributioner för att uppdatera en dators operativ system eller för att installera en ny version av Windows på en ny dator.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: da5f8b61-2386-4530-ad54-1a5c51911f07
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7d2d467a053689edad1dcf62fa9bb140d5f259d9
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124626"
---
# <a name="use-pxe-to-deploy-windows-over-the-network-with-configuration-manager"></a>Använd PXE för att distribuera Windows via nätverket med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

PXE-initierade operativ Systems distributioner i Configuration Manager låta klienterna begära och distribuera operativ system över nätverket. För den här distributions metoden skickar du OS-avbildningen och start avbildningarna till en PXE-aktiverad distributions plats.

> [!NOTE]
> När du skapar en OS-distribution som bara riktar sig till x64 BIOS-datorer måste både x64-startavbildningen och x86-startavbildningen vara tillgängliga på distributions platsen.

Du kan använda PXE-initierade operativ Systems distributioner i följande scenarier:

- [Uppdatera en befintlig dator med en ny version av Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [Installera en ny version av Windows på en ny dator (utan operativsystem)](install-new-windows-version-new-computer-bare-metal.md)

Slutför stegen i ett av scenarierna för operativ Systems distribution och Använd sedan avsnitten i den här artikeln för att förbereda för PXE-initierade distributioner.

> [!WARNING]
> Om du använder PXE-distributioner och konfigurerar enhets maskin vara med nätverkskortet som den första startenheten kan de här enheterna automatiskt starta en aktivitetssekvens för operativ system distribution utan användar interaktion. [Distributions verifiering](../../core/servers/manage/settings-to-manage-high-risk-deployments.md) hanterar inte den här konfigurationen. Även om den här konfigurationen kan förenkla processen och minska användar interaktionen, medför enheten större risk för oavsiktlig återavbildning.

Från och med version 2006 kan PXE-baserade aktivitetssekvenser Ladda ned molnbaserad innehåll. Den PXE-aktiverade distributions platsen kräver fortfarande start avbildningen och enheten behöver en intranät anslutning till hanterings platsen. Den kan sedan hämta ytterligare innehåll från en innehålls aktive rad Cloud Management Gateway (CMG) eller en moln distributions plats.<!--6209223--> Mer information finns i [stöd för molnbaserad innehåll](use-bootable-media-to-deploy-windows-over-the-network.md#support-for-cloud-based-content).

## <a name="configure-distribution-points-for-pxe"></a><a name="BKMK_Configure"></a>Konfigurera distributions platser för PXE

Om du vill distribuera operativ system till Configuration Manager klienter som gör PXE-startbegäranden konfigurerar du en eller flera distributions platser så att PXE-begäranden accepteras. Distributions platsen svarar sedan på PXE-startbegäranden och anger lämplig distributions åtgärd. Mer information finns i [Install or modify a distribution point](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).

> [!NOTE]
> När du konfigurerar en enda PXE-aktiverad distributions plats för att stödja flera undernät, stöds det inte för att använda DHCP-alternativ. Om du vill tillåta att nätverket vidarebefordrar klient-PXE-begäranden till PXE-aktiverade distributions platser konfigurerar du IP-hjälp på routrarna.

I version 1810 stöds inte PXE-svarare utan WDS på servrar som också kör en DHCP-server.

Från och med version 1902 kan den nu finnas på samma server som DHCP-tjänsten när du aktiverar en PXE-svarare på en distributions plats utan Windows Deployment-tjänst.<!--3734270, SCCMDocs-pr #3416--> Lägg till följande inställningar för att stödja den här konfigurationen:

- Ange DWord-värdet **DoNotListenOnDhcpPort** till `1` i följande register nyckel: `HKLM\Software\Microsoft\SMS\DP` .
- Ange DHCP-alternativet 60 till `PXEClient` .
- Starta om SCCMPXE-och DHCP-tjänsterna på servern.

## <a name="prepare-a-pxe-enabled-boot-image"></a>Förbereda en PXE-aktiverad startavbildning

Om du vill använda PXE för att distribuera ett operativ system distribuerar du både x86 och x64 PXE-aktiverade start avbildningar till en eller flera PXE-aktiverade distributions platser.

- Om du vill aktivera PXE på en start avbildning väljer du **distribuera den här start avbildningen från den PXE-aktiverade distributions platsen** på fliken **data källa** i egenskaperna för start avbildningen.

- När du ändrar egenskaperna för start avbildningen uppdaterar du och distribuerar om start avbildningen till distributions platser. Mer information finns i avsnittet [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

## <a name="manage-duplicate-hardware-identifiers"></a>Hantera dubbletter av maskin varu identifierare

Configuration Manager kan identifiera flera datorer som samma enhet om de har dubbla SMBIOS-attribut eller om du använder ett delat nätverkskort. Minska problemen genom att hantera dubbla maskin varu identifierare i inställningarna för hierarkin. Mer information finns i [Hantera dubbletter av maskin varu identifierare](../../core/clients/manage/manage-clients.md#manage-duplicate-hardware-identifiers).

## <a name="create-an-exclusion-list-for-pxe-deployments"></a><a name="BKMK_PXEExclusionList"></a> Skapa en undantagslista för PXE-distributioner

> [!NOTE]
> I vissa fall kan processen för att [hantera dubbla maskin varu identifierare](../../core/clients/manage/manage-clients.md#manage-duplicate-hardware-identifiers) vara enklare.<!-- SCCMDocs issue 802 -->
>
> Beteendena för var och en kan orsaka olika resultat i vissa scenarier. Undantags listan startar aldrig en klient med den angivna MAC-adressen, oavsett vad.
>
> Listan med dubbla ID: n använder inte MAC-adressen för att hitta aktivitetssekvensen för en klient. Om den matchar SMBIOS-ID: t, eller om det finns en aktivitetssekvens för okända datorer, startar klienten fortfarande.

När du distribuerar operativ system med PXE kan du skapa en undantags lista på varje distributions plats. Lägg till MAC-adresserna i undantags listan för de datorer som du vill att distributions platsen ska ignorera. Datorer som listas tar inte emot de aktivitetssekvensdistributioner som Configuration Manager används för PXE-distribution.

1. Skapa en textfil på den PXE-aktiverade distributions platsen. Namnge till exempel filen **pxeExceptions.txt**.

1. Använd en vanlig text redigerare, till exempel anteckningar, för att redigera filen. Lägg till MAC-adresserna för de datorer som den PXE-aktiverade distributions platsen ska ignorera. Separera MAC-adressvärdena med kolon och ange varje adress på en separat rad. Exempel: `01:23:45:67:89:ab`

1. Spara text filen på den PXE-aktiverade distributions platsen. Du kan spara den på valfri plats på servern.

1. Redigera registret på den PXE-aktiverade distributions platsen. Bläddra till följande register Sök väg: `HKLM\Software\Microsoft\SMS\DP` . Skapa ett **MACIgnoreListFile** -sträng värde. Lägg till den fullständiga sökvägen till text filen på den PXE-aktiverade distributions platsen.

    > [!WARNING]
    > Om du använder Registereditorn på ett felaktigt sätt kan det orsaka allvarliga problem som kan kräva att du installerar om Windows. Microsoft kan inte garantera att du kan lösa problem som orsakas av felaktig användning av Registereditorn. Du använder Registereditorn på egen risk.

1. När du har gjort den här register ändringen startar du om WDS-tjänsten eller PXE responder-tjänsten. Du behöver inte starta om servern.<!--512129-->

## <a name="ramdisk-tftp-block-size-and-window-size"></a><a name="BKMK_RamDiskTFTP"></a>Storlek på RamDisk TFTP-block storlek och fönster storlek

Du kan anpassa RamDisk TFTP-block och fönster storlekar för PXE-aktiverade distributions platser. Om du har anpassat nätverket kan en stor block-eller fönster storlek medföra att hämtningen av start avbildningen inte kan slutföras med ett timeout-fel. Med anpassningarna av RamDisk TFTP-block och fönster storlek kan du optimera TFTP-trafik när du använder PXE för att uppfylla dina särskilda nätverks krav. Testa de anpassade inställningarna i din miljö för att avgöra vilken konfiguration som är mest effektiv. Mer information finns i [Anpassa storlek på RAMDISK TFTP-block storlek och fönster storlek på PXE-aktiverade distributions platser](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP).

## <a name="configure-deployment-settings"></a>Konfigurera distributionsinställningar

Om du vill använda en PXE-initierad operativ Systems distribution konfigurerar du distributionen för att göra operativ systemet tillgängligt för PXE-startbegäranden. Konfigurera tillgängliga operativ system på fliken **distributions inställningar** i distributions egenskaperna. Välj något av följande alternativ för inställningen **gör tillgängligt för följande** :

- Configuration Manager klienter, media och PXE

- Endast media och PXE

- Endast media och PXE (dolt)

## <a name="option-82-during-pxe-dhcp-handshake"></a>Alternativ 82 under PXE DHCP-handskakning

Från och med version 1906 stöder Configuration Manager alternativ 82 under PXE DHCP-handskakningen med PXE-svarare utan WDS. Om du behöver alternativet 82, se till att använda PXE-svarare utan WDS. Configuration Manager stöder inte alternativ 82 med WDS.

## <a name="deploy-the-task-sequence"></a><a name="BKMK_Deploy"></a> Distribuera aktivitetssekvensen

Distribuera operativ systemet till en mål samling. Mer information finns i [Distribuera en aktivitetssekvens](deploy-a-task-sequence.md). När du distribuerar operativsystem med PXE kan du konfigurera om distributionen är obligatorisk eller tillgänglig.

- **Nödvändig distribution**: nödvändiga distributioner använder PXE utan att användaren behöver göra något. Användaren kan inte kringgå PXE-starten. Men om användaren avbryter PXE-starten innan distributions platsen svarar, distribueras inte operativ systemet.

- **Tillgänglig distribution**: tillgängliga distributioner kräver att användaren finns på mål datorn. En användare måste trycka på **F12** -tangenten för att fortsätta PXE-startprocessen. Om en användare inte är närvarande för att trycka på **F12**startar datorn med det aktuella operativ systemet eller från nästa tillgängliga startenhet.

Du kan distribuera om en nödvändig PXE-distribution genom att rensa statusen för den senaste PXE-distributionen som tilldelats till en Configuration Manager samling eller en dator. Mer information om åtgärden **Rensa nödvändiga PXE-distributioner** finns i [Hantera klienter](../../core/clients/manage/manage-clients.md#BKMK_ManagingClients_DevicesNode) eller [hantera samlingar](../../core/clients/manage/collections/manage-collections.md#bkmk_device). Med den här åtgärden återställs statusen för distributionen och de senaste nödvändiga distributionerna installeras om.

> [!IMPORTANT]
> PXE-protokollet är inte säkert. Se till att PXE-servern och PXE-klienten finns i ett fysiskt säkert nätverk, till exempel i ett Data Center, för att förhindra obehörig åtkomst till webbplatsen.

## <a name="how-the-boot-image-is-selected-for-pxe"></a>Hur start avbildningen väljs för PXE

När en klient startar med PXE tillhandahåller Configuration Manager klienten med en start avbildning att använda. Configuration Manager använder en start avbildning med en exakt arkitektur matchning. Om en start avbildning med den exakta arkitekturen inte är tillgänglig använder Configuration Manager en start avbildning med en kompatibel arkitektur.

Följande lista innehåller information om hur en start avbildning väljs för klienter som startas med PXE:  

1. Configuration Manager söker i plats databasen efter den system post som matchar MAC-adressen eller SMBIOS för den klient som försöker starta.  

    > [!NOTE]  
    > Om en dator som har tilldelats en plats startar till PXE för en annan plats, är principerna inte synliga för datorn. Om en klient till exempel redan är tilldelad till plats A, kan hanterings platsen och distributions platsen för plats B inte komma åt principerna från plats A. Klienten har inte PXE-start.  

2. Configuration Manager letar efter aktivitetssekvenser som har distribuerats till system posten som finns i steg 1.  

3. I listan med aktivitetssekvenser som påträffades i steg 2 söker Configuration Manager efter en start avbildning som matchar arkitekturen hos klienten som försöker starta. Om en start avbildning hittas med samma arkitektur används den Start avbildningen.  

    Om det finns fler än en start avbildning använder den det *högsta* eller senaste distributions-ID: t för aktivitetssekvens. Om det finns en hierarki med flera platser prioriteras den *högre* bokstavs platsen i den sträng jämförelsen. Om de båda båda stämmer överens kan en årets gamla distribution från plats ZZZ väljas över igår-distributionen från plats AAA.<!-- SCCMDocs issue 877 -->  

4. Om det inte går att hitta en start avbildning med samma arkitektur Configuration Manager söker efter en start avbildning som är kompatibel med klientens arkitektur. Det ser ut i listan med aktivitetssekvenser som finns i steg 2. Till exempel är en 64-bitars BIOS/MBR-klient kompatibel med 32-bitars-och 64-bitars start avbildningar. En 32-bitars BIOS/MBR-klient är kompatibel med endast 32-bitars start avbildningar. UEFI-klienter är bara kompatibla med matchande arkitektur. En 64-bitars UEFI-klient är kompatibel med endast 64-bitars start avbildningar och en 32-bitars UEFI-klient är kompatibel med endast 32-bitars start avbildningar.

## <a name="next-steps"></a>Nästa steg

[Användarupplevelser för distribution av operativsystem](../understand/user-experience.md#pxe)
