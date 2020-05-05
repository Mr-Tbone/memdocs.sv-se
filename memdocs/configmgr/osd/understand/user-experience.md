---
title: Användarupplevelser för distribution av operativsystem
titleSuffix: Configuration Manager
description: Lär dig mer om användar upplevelser som förlopp för aktivitetssekvenser och medie guiden för operativ Systems distribution i Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 58849e40-30d5-4153-84b3-ca4af3a4f09d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5f92e76047a70f6d86406b1a364603163d902e62
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719934"
---
# <a name="user-experiences-for-os-deployment"></a>Användarupplevelser för distribution av operativsystem

*Gäller för: Configuration Manager (aktuell gren)*

När du har [distribuerat en aktivitetssekvens](../deploy-use/deploy-a-task-sequence.md), beroende på scenariot, finns det olika sätt för användare att interagera med distributionen. Den här artikeln visar de huvudsakliga användar upplevelsen med OS-distributioner och hur du kan konfigurera dem:

- Användar meddelande i Software Center för en distribution med hög effekt
- Ett exempel på en PXE-start
- Guiden aktivitetssekvens från media
- Förlopps fönstret när aktivitetssekvensen körs
- Fel fönster när aktivitetssekvensen Miss lyckas

## <a name="software-center"></a>Software Center

För en distribution med hög effekt kan du anpassa det meddelande som visas i Software Center. När användaren öppnar operativ Systems distributionen i Software Center visas ett meddelande som liknar följande fönster:

![Anpassat meddelande om aktivitetssekvenser till slutanvändaren från Software Center](../media/user-notification-enduser.png)

Mer information om hur du anpassar meddelandet i det här fönstret finns i [skapa ett anpassat meddelande för distributioner med hög risk](../deploy-use/manage-task-sequences-to-automate-tasks.md#create-a-custom-notification-for-high-risk-deployments).

Du kan också anpassa organisationens namn längst upp i fönstret. (Exemplet ovan visar standardvärdet `IT Organization`). Ändra klient inställningen för **organisations namn** i **dator agent** gruppen. Mer information finns i [om klient inställningar](../../core/clients/deploy/about-client-settings.md#computer-agent).

<!--
optional vs required
**Allow user to interact** on required deployment?
-->

Mer information finns i [använda Software Center för att distribuera Windows via nätverket](../deploy-use/use-software-center-to-deploy-windows-over-the-network.md).

## <a name="pxe"></a>PXE

Olika maskin varu modeller har olika upplevelser för PXE. För att starta i nätverket använder UEFI-baserade enheter normalt `Enter` nyckeln och BIOS-baserade enheter använder `F12` nyckeln.

I följande exempel visas PXE-upplevelsen för Hyper-V-gen1 (BIOS):

![Exempel på en BIOS PXE-skärm från en virtuell Hyper-V-dator](media/hyperv-pxe.png)

När enheten har startats via PXE fungerar den på samma sätt som startbara media. Mer information finns i nästa avsnitt i [guiden aktivitetssekvens](#task-sequence-wizard).

Mer information finns i [använda PXE för att distribuera Windows via nätverket](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).

> [!WARNING]
> Om du använder PXE-distributioner och konfigurerar enhets maskin vara med nätverkskortet som den första startenheten kan de här enheterna automatiskt starta en aktivitetssekvens för operativ system distribution utan användar interaktion. Distributions verifiering hanterar inte den här konfigurationen. Även om den här konfigurationen kan förenkla processen och minska användar interaktionen, medför enheten större risk för oavsiktlig återavbildning.

## <a name="task-sequence-wizard"></a>Guiden aktivitetssekvens

När du använder [medier för aktivitetssekvenser](../deploy-use/create-task-sequence-media.md)körs guiden aktivitetssekvens för att vägleda processen.

### <a name="welcome-to-the-task-sequence-wizard"></a>Välkommen till guiden aktivitetssekvens

![Skärm bild av den huvudsakliga sidan i guiden aktivitetssekvens](media/welcome-task-sequence-wizard.png)

- Om du skyddar mediet med lösen ord måste användaren ange lösen ordet på Välkomst sidan.

- Välj **Konfigurera nätverks inställningar** om du vill ange en statisk IP-adress eller andra anpassade nätverks inställningar. Annars använder enheten DHCP som standard.

- Om ditt nätverk kräver en proxyserver väljer du **Konfigurera proxyinställningar**.

### <a name="select-a-task-sequence-to-run"></a>Välj en aktivitetssekvens som ska köras

Om du distribuerar fler än en aktivitetssekvens till enheten visas den här sidan för att välja en aktivitetssekvens. Se till att använda ett namn och en beskrivning av aktivitetssekvensen som användarna kan förstå.

![Skärm bild av sidan för val av aktivitetssekvens i guiden aktivitetssekvens](media/task-sequence-wizard-select.png)

### <a name="edit-task-sequence-variables"></a>Redigera variabler för aktivitetssekvens

Om några variabler för aktivitetssekvensen har tomma värden, visar guiden en sida där du kan redigera variabel värden.

![Skärm bild av sidan Redigera variabler för aktivitetssekvens i guiden aktivitetssekvens](media/task-sequence-wizard-variables.png)

## <a name="prestart-commands"></a>För inläsnings kommandon

Du kan anpassa media för aktivitetssekvenser eller start avbildningar för att köra ett för inläsnings kommando. Ett för inläsnings kommando körs innan aktivitetssekvensen startar. Följande åtgärder är några av de vanligaste:

- Uppmana användaren att ange dynamiska värden, t. ex. dator namnet
- Ange Nätverks konfiguration
- Ange mappning mellan användare och enhet

För inläsnings kommandot är en kommando rad som du anger med ett skript eller ett program. Användar upplevelsen är unik för det skriptet eller programmet.

Mer information finns i följande artiklar:

- [Förinläsningskommandon för aktivitetssekvensmedier](prestart-commands-for-task-sequence-media.md)
- [Hantera startavbildningar](../get-started/manage-boot-images.md#customization)
- [Media för aktivitetssekvens](../deploy-use/create-task-sequence-media.md)

## <a name="task-sequence-progress"></a>Förlopp för aktivitetssekvens

När aktivitetssekvensen körs visas fönstret **installations förlopp** :

![Exempel på förlopps fönstret för aktivitetssekvens](media/task-sequence-progress.png)

- Det här fönstret är alltid överst. Du kan flytta den, men du kan inte stänga eller minimera den.

- Du kan anpassa organisationens namn längst upp i fönstret. (Exemplet ovan visar standardvärdet `IT Organization`). Ändra klient inställningen för **organisations namn** i **dator agent** gruppen. Mer information finns i [om klient inställningar](../../core/clients/deploy/about-client-settings.md#computer-agent).

    > [!TIP]
    > Aktivitetssekvensen lagrar det här värdet i den skrivskyddade variabeln [_SMSTSOrgName](task-sequence-variables.md#SMSTSOrgName).

- Du kan anpassa under rubriken. (Exemplet ovan visar standardvärdet, `Running: <task sequence name>`.) I egenskaperna för aktivitetssekvensen väljer du alternativet för att **använda anpassad text** för förlopps meddelande texten. Det får innehålla högst 255 tecken.

- **Kör åtgärd**: den första raden visar namnet på det aktuella steget i aktivitetssekvensen. Förlopps indikatorn nedan visar den övergripande slut för ande av aktivitetssekvensen.

- Den andra raden visas bara för vissa steg som ger mer detaljerad förloppet.

- Använd variabeln [TSDisableProgressUI](task-sequence-variables.md#TSDisableProgressUI) för att styra när aktivitetssekvensen visar förloppet.

    Om du vill inaktivera förlopps fönstret fullständigt inaktiverar du alternativet för att **Visa förloppet för aktivitetssekvensen** på sidan **användar upplevelse** i distributionen av aktivitetssekvensen.

Från och med version 2002 innehåller förlopps fönstret för aktivitetssekvensen följande förbättringar:<!--5932692-->

- Visar aktuellt steg nummer, totalt antal steg och procent färdigt

- Ökat fönstrets bredd så att du får mer utrymme för att bättre Visa organisationens namn på en enda rad

![Exempel på förlopps fönster för aktivitetssekvens](media/2356386-task-sequence-progress.png)

Som standard används den befintliga texten i fönstret förlopp för aktivitetssekvens. Om du inte gör några ändringar fortsätter den att fungera på samma sätt som i version 1910 och tidigare. Om du vill visa den nya förloppet anger du variabeln aktivitetssekvens, [TSProgressInfoLevel](task-sequence-variables.md#TSProgressInfoLevel).

Antalet och procent andelen slutfört är endast avsedda för allmänna råd. Dessa värden baseras på det totala antalet steg i aktivitetssekvensen. För en mer komplex aktivitetssekvens med steg som kör villkorligt baserat på aktivitetssekvens, kan förloppet vara icke-linjärt.

Det totala antalet steg omfattar inte följande objekt i aktivitetssekvensen:

- Användargrupp. Det här objektet är en behållare för andra steg, inte ett själva steg.

- Instanser av steget **Kör aktivitetssekvens** . Det här steget är en behållare för andra steg.

- Steg som du inaktiverar. Ett inaktiverat steg körs inte under aktivitetssekvensen.

    > [!NOTE]
    > Aktiverade steg i en inaktive rad grupp ingår fortfarande i det totala antalet.

## <a name="task-sequence-error"></a>Fel i aktivitetssekvens

Om aktivitetssekvensen Miss lyckas visas fel fönstret i **aktivitetssekvensen** .

![Exempel fönster för aktivitetssekvenser](media/task-sequence-error.png)

- Du anpassar huvud informationen på samma sätt som förlopps fönstret för aktivitetssekvensen.

- Den visar namnet på aktivitetssekvensen, en felkod och ett allmänt meddelande för användare. Exempelvis: `Task sequence: Upgrade to Windows 10 Enterprise has failed with the error code (0x80004005). For more information, contact your system administrator or helpdesk operator.`

- Fönstret stängs automatiskt efter en tids gräns. Som standard är denna timeout 15 minuter. Du kan anpassa det här värdet med variabeln [SMSTSErrorDialogTimeout](task-sequence-variables.md#SMSTSErrorDialogTimeout)i aktivitetssekvensen.
