---
title: Webbplatsen för administration och övervakning av BitLocker
titleSuffix: Configuration Manager
description: Så här använder du webbplatsen för administration och övervakning av BitLocker (supportavdelningen) i Configuration Manager
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: how-to
ms.assetid: 81f03922-90f6-4e8f-be65-da64ccb21cf2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bf9301e4fcb279b7d79a6f6c3d0a90ab3d15e277
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697321"
---
# <a name="bitlocker-administration-and-monitoring-website"></a>Webbplatsen för administration och övervakning av BitLocker

*Gäller för: Configuration Manager (aktuell gren)*

<!--3601034-->

Webbplatsen för administration och övervakning av BitLocker är ett administrativt gränssnitt för BitLocker-diskkryptering. Det kallas även support portalen. Använd den här webbplatsen för att granska rapporter, återställa användares enheter och hantera TPM-enheter.

[![Skärm bild av standard webbplatsen för BitLocker-administration och övervakning](media/bitlocker-helpdesk-website.png)](media/bitlocker-helpdesk-website.png#lightbox)

Installera den här komponenten på en webb server innan du kan använda den. Mer information finns i [Konfigurera BitLocker-rapporter och portaler](setup-websites.md).

Gå till webbplatsen för administration och övervakning via följande URL: `https://webserver.contoso.com/HelpDesk`

> [!NOTE]
> Du kan visa **rapporten för återställnings granskning** på webbplatsen för administration och övervakning. Du lägger till andra BitLocker Management-rapporter till repor ting Services-platsen. Mer information finns i [Visa BitLocker-rapporter](view-reports.md).

## <a name="groups"></a>Grupper

För att få åtkomst till vissa områden på webbplatsen för administration och övervakning måste ditt användar konto vara i någon av följande grupper. Skapa de här grupperna i Active Directory med ett namn som du vill använda. När du installerar den här webbplatsen anger du dessa grupp namn. Mer information finns i [Konfigurera BitLocker-rapporter och portaler](setup-websites.md).

|Grupp|Beskrivning|
|--- |--- |
|BitLocker-administratörer för supportavdelningen|Ger åtkomst till alla områden på webbplatsen för administration och övervakning. När du hjälper en användare att återställa sina enheter anger du bara återställnings nyckeln och inte domänen och användar namnet. Om en användare är medlem i både den här gruppen och användar gruppen för BitLocker-supportavdelningen, åsidosätter administratörs grupp behörigheten användar gruppens behörigheter.|
|Användare av BitLocker-supportavdelningen|Ger åtkomst till områdena **hantera TPM** och **enhets återställning** på webbplatsen för administration och övervakning. När du använder något av områdena måste du fylla i alla fält inklusive användarens domän och konto namn. Om en användare är medlem i både den här gruppen och administratörs gruppen för BitLocker-supportavdelningen åsidosätter administratörs grupp behörigheten användar gruppens behörigheter.|
|BitLocker-rapportens användare|Ger åtkomst till avsnittet **rapporter** på webbplatsen Administration och övervakning.|

## <a name="manage-tpm"></a>Hantera TPM

Om en användare anger en felaktig PIN-kod för många gånger kan de låsa TPM: en. Antalet gånger som en användare kan ange en felaktig PIN-kod innan TPM: ens låser sig mellan tillverkare och tillverkare. Från webbplatsen **hantera TPM** på webbplatsen för administration och övervakning får du åtkomst till det centrala nyckel återställnings data systemet.

Mer information om TPM-ägarskap finns i [Configure MBAM to depositions The TPM and Store OwnerAuth passwords](/microsoft-desktop-optimization-pack/mbam-v25/mbam-25-security-considerations#bkmk-tpm).

> [!NOTE]
> Från och med Windows 10, version 1607, behåller Windows inte TPM-ägarens lösen ord vid etablering av TPM.

1. Gå till webbplatsen för administration och övervakning i webbläsaren, till exempel `https://webserver.contoso.com/HelpDesk` .

1. I det vänstra fönstret väljer du **hantera TPM** -ytan.

    ![Sidan för administration och övervakning av BitLocker-webbplats hantera TPM](media/bitlocker-admin-manage-tpm.png)

1. Ange det fullständigt kvalificerade domän namnet för datorn och dator namnet.

1. Om det behövs anger du användarens domän och användar namn för att hämta lösen ords filen för TPM-ägaren.

1. Välj ett av följande alternativ för **orsaken till att du begär lösen ords filen för TPM-ägare**:

    - Återställ PIN-utelåsning
    - Aktivera TPM
    - Inaktivera TPM
    - Ändra TPM-lösenord
    - Rensa TPM
    - Annat

    När du har **skickat** formuläret returnerar webbplatsen något av följande svar:

    - Om det inte går att hitta en matchande TPM-ägares lösen ords fil returneras ett fel meddelande.

    - Lösen ords filen för TPM-ägare för den överförda datorn

    När du har hämtat lösen ords filen för TPM-ägaren visas ägar lösen ordet på webbplatsen.

1. Om du vill spara lösen ordet till en fil väljer du **Spara**.

1. I avsnittet **hantera TPM** väljer du alternativet **Återställ TPM-utelåsning** och anger lösen ords filen för TPM-ägaren.

    TPM-utelåsning återställs. BitLocker återställer användarens åtkomst till enheten.

    > [!IMPORTANT]
    > Dela inte TPM-hashvärdet eller lösen ords filen för TPM-ägare.

## <a name="drive-recovery"></a>Enhets återställning

### <a name="recover-a-drive-in-recovery-mode"></a><a name="bkmk_recovery"></a> Återställa en enhet i återställnings läge

Enheter går in i återställnings läge i följande scenarier:

- Användaren tappar bort eller glömmer bort sin PIN-kod eller lösen ord
- TPM (Trusted module Platform) identifierar ändringar i BIOS-eller startfiler på datorn

Om du vill få ett återställnings lösen ord använder du avsnittet **enhets återställning** på webbplatsen Administration och övervakning.

> [!IMPORTANT]
> Återställnings lösen ord upphör att gälla efter ett och samma tillfälle. På OS-enheter och fasta data enheter gäller regeln för enkel användning automatiskt. På flyttbara enheter gäller den när du tar bort och sätter på enheten igen.

1. Gå till webbplatsen för administration och övervakning i webbläsaren, till exempel `https://webserver.contoso.com/HelpDesk` .

1. I det vänstra fönstret väljer du **enhets återställnings** ytan.

    ![Sidan BitLocker-administration och övervakning av driv rutin för webbplats driv rutin](media/bitlocker-admin-drive-recovery.png)

1. Om det behövs anger du användarens domän och användar namn för att Visa återställnings information.

1. Om du vill se en lista över möjliga matchande återställnings nycklar anger du de första åtta siffrorna i återställnings nyckelns ID. Om du vill hämta den exakta återställnings nyckeln anger du hela återställnings nyckel-ID.

1. Välj något av följande alternativ som **orsak för upplåsning av enhet**:

    - Operativ systemets start ordning har ändrats
    - BIOS har ändrats
    - Ändrade operativsystemfiler
    - Förlorad start nyckel
    - Förlorad PIN-kod
    - Återställning av TPM
    - Förlorad lösen fras
    - Förlorat smartkort
    - Annat

    När du har **skickat** formuläret returnerar webbplatsen något av följande svar:

    - Om användaren har flera matchande återställnings lösen ord returneras flera möjliga matchningar.

    - Återställnings lösen ordet och återställnings paketet för den inskickade användaren.

        > [!NOTE]
        > Om du återställer en skadad enhet ger alternativet återställnings paket BitLocker med viktig information som krävs för att återställa enheten.

    - Om det inte går att hitta ett matchande återställnings lösen ord returneras ett fel meddelande.

    När du har hämtat återställnings lösen ordet och återställnings paketet visas återställnings lösen ordet på webbplatsen.

1. Kopiera lösen ordet genom att välja **Kopiera nyckel**. Om du vill spara återställnings lösen ordet till en fil väljer du **Spara**.

För att låsa upp enheten, ange återställnings lösen ordet eller Använd återställnings paketet.

### <a name="recover-a-moved-drive"></a><a name="bkmk_moved"></a> Återställa en flyttad enhet

När du flyttar en enhet till en ny dator, eftersom TPM: en är annorlunda, accepterar BitLocker inte den tidigare PIN-koden. För att återställa den flyttade enheten hämtar du återställnings nyckel-ID: t för att hämta återställnings lösen ordet.

Om du vill återställa en flyttad enhet använder du **enhets återställnings** avsnittet på webbplatsen för administration och övervakning.

1. Starta datorn i läget Windows återställnings miljö (WinRE) på datorn med den flyttade enheten.

1. I WinRE behandlar BitLocker den flyttade OS-enheten som en fast data enhet. BitLocker visar enhetens återställnings lösen ord-ID och fråga om återställnings lösen ord.

    > [!NOTE]
    > I vissa fall kan du under start processen välja **att jag har glömt PIN-koden** om alternativet är tillgängligt. Ange sedan återställnings läge för att Visa återställnings nyckel-ID.

1. Använd återställnings nyckel-ID: t för att hämta återställnings lösen ordet från webbplatsen för administration och övervakning. Mer information finns i [återställa en enhet i återställnings läge](#bkmk_recovery).

Om du konfigurerade den flyttade enheten för att använda ett TPM-chip på den ursprungliga datorn utför du följande steg. Annars slutförs återställnings processen.

1. När du har låst upp enheten startar du datorn i WinRE-läge. Öppna en kommando tolk i WinRE och Använd `manage-bde` kommandot för att dekryptera enheten. Det här verktyget är det enda sättet att ta bort **TPM + PIN-** skyddet utan det ursprungliga TPM-kretsen. Mer information om det här kommandot finns i [manage-bde](/windows/security/information-protection/bitlocker/bitlocker-use-bitlocker-drive-encryption-tools-to-manage-bitlocker#bkmk-managebde).

1. När den är klar startar du datorn på vanligt sätt. Configuration Manager tvingar BitLocker-principen att kryptera enheten med den nya datorns TPM och PIN-kod.

### <a name="recover-a-corrupted-drive"></a><a name="bkmk_corrupted"></a> Återställa en skadad enhet

Använd återställnings nyckel-ID: t för att hämta ett återställnings nyckel paket från webbplatsen för administration och övervakning. Mer information finns i [återställa en enhet i återställnings läge](#bkmk_recovery).

1. Spara **återställnings nyckel paketet** på datorn och kopiera det sedan till datorn med den skadade enheten.

1. Öppna en kommando tolk som administratör och skriv följande kommando:

    `repair-bde <corrupted drive> <fixed drive> -kp <key package> -rp <recovery password>`

    Ersätt följande värden:

    - `<corrupted drive>`: Enhets beteckningen för den skadade enheten, till exempel `D:`
    - `<fixed drive>`: Enhets beteckningen för en tillgänglig hård disk med samma eller större storlek än den skadade enheten. BitLocker återställer och flyttar data på den skadade enheten till den angivna enheten. Alla data på den här enheten skrivs över.
    - `<key package>`: Platsen för återställnings nyckel paketet
    - `<recovery password>`: Det associerade återställnings lösen ordet

    Exempel:

    `repair-bde C: D: -kp F:\RecoveryKeyPackage -rp 111111-222222-333333-444444-555555-666666-777777-888888`

Mer information om det här kommandot finns i [Repair-BDE](/windows/security/information-protection/bitlocker/bitlocker-use-bitlocker-drive-encryption-tools-to-manage-bitlocker#bkmk-repairbde).

## <a name="reports"></a>Rapporter

Webbplatsen för administration och övervakning innehåller **rapporten återställnings granskning**. Andra rapporter är tillgängliga från Configuration Manager repor ting Services-platsen. Mer information finns i [Visa BitLocker-rapporter](view-reports.md).

1. Gå till webbplatsen för administration och övervakning i webbläsaren, till exempel `https://webserver.contoso.com/HelpDesk` .

1. I det vänstra fönstret väljer du **rapport** områden.

1. Välj **rapporten återställnings granskning**på den översta meny raden.

Mer information om den här rapporten finns i [rapporten återställnings granskning](view-reports.md#bkmk-audit)

> [!TIP]
> Om du vill spara rapport resultaten väljer du **Exportera** i meny raden **rapporter** .