---
title: Felsök Endpoint Protection
titleSuffix: Configuration Manager
description: Lär dig hur du felsöker problem med Windows Defender och Endpoint Protection.
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: d837253e-fcc2-422a-9e2c-c78b938dfd8c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: efd31eaee987a7e28557cf0601608ca97c914999
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724491"
---
# <a name="troubleshoot-windows-defender-or-endpoint-protection-client"></a>Felsöka Windows Defender eller Endpoint Protection-klienten

*Gäller för: Configuration Manager (aktuell gren)*

Om du stöter på problem med Windows Defender eller Endpoint Protection kan du använda den här artikeln för att felsöka följande problem:  

- [Uppdatera Windows Defender eller Endpoint Protection](#update-windows-defender-or-endpoint-protection)  
- [Uppdatera tjänsten Windows Defender eller Endpoint Protection](#starting-windows-defender-or-endpoint-protection-service)  
- [Problem med Internetanslutning](#internet-connection-issues)  
- [Identifierat hot kan inte åtgärdas](#detected-threat-cant-be-remediated)  

## <a name="update-windows-defender-or-endpoint-protection"></a> Uppdatera Windows Defender eller Endpoint Protection

### <a name="symptoms"></a>Symtom

Windows Defender eller Endpoint Protection fungerar automatiskt med Microsoft Update för att kontrol lera att virus-och spionprograms definitionerna hålls uppdaterade.  

Det här avsnittet behandlar vanliga problem med automatiska uppdateringar, inklusive följande situationer:  

- Du får felmeddelanden som anger att uppdateringar har misslyckats.  

- När du söker efter uppdateringar visas ett fel meddelande om att uppdateringar av virus-och spionprograms definitioner inte kan kontrol leras, hämtas eller installeras.  

- Trots att enheten är ansluten till Internet, fungerar inte uppdateringarna.  

- Uppdateringar installeras inte automatiskt enligt schemat.  

### <a name="causes"></a>Orsaker

De vanligaste orsakerna till uppdaterings problem är problem med Internet anslutningen. Om du vet att enheten är ansluten till Internet eftersom du kan bläddra till andra webbplatser, kan problemet orsakas av konflikter med Internet inställningarna i Windows.  

### <a name="options-to-resolve"></a>Alternativ för att lösa

#### <a name="step-1-reset-your-internet-settings"></a>Steg 1: Återställ Internet inställningar  

1. Avsluta alla öppna program, inklusive webbläsaren.  

    > [!NOTE]  
    > När du återställer de här Internet inställningarna kan du ta bort webbläsaren temporära filer, cookies, webb historik och lösen ord online. Favoriter tas inte bort.  

2. Gå till **Start** -menyn och öppna `inetcpl.cpl`.  

3. Växla till fliken **Avancerat** .  

4. I avsnittet för att **återställa Internet Explorer-inställningar**väljer du **Återställ**och sedan **Återställ** igen för att bekräfta.  

5. Välj **OK** när inställningarna återställs.

6. Försök att uppdatera Windows Defender igen.

Fortsätt till nästa steg om problemet kvarstår.  

#### <a name="step-2-make-sure-that-the-date-and-time-are-set-correctly-on-your-computer"></a>Steg 2: kontrol lera att datum och tid är korrekt inställda på din dator  

Om fel meddelandet innehåller koden 0x80072f8f beror, orsakas problemet troligen av ett felaktigt datum-eller tids inställning på datorn. Gå till **Start** -menyn, Välj **Inställningar**, Välj **tid & språk**och välj **datum & tid**.

#### <a name="step-3-rename-the-software-distribution-folder-on-your-computer"></a>Steg 3: Byt namn på mappen program varu distribution på din dator  

1. Stoppa tjänsten **Windows Update** .  

    1. Gå till **Start**och öppna **Services. msc**.  

    2. Välj tjänsten **Windows Update** . Gå till **åtgärd** -menyn och välj **stoppa**.

2. Byt namn på **SoftwareDistribution** -katalogen.  

    1. Öppna en kommandotolk som administratör.  

    2. Ange följande kommandon:

        ```cmd
        cd %windir%
        ren SoftwareDistribution SDTemp
        exit
        ```

3. Starta om tjänsten **Windows Update** .

    1. Gå tillbaka till fönstret **tjänster** .  

    2. Välj tjänsten **Windows Update** . Gå till **åtgärd** -menyn och välj **Starta**.

    3. Stäng tjänster-fönstret.  

#### <a name="step-4-reset-the-microsoft-antivirus-update-engine-on-your-computer"></a>Steg 4: återställa Microsoft Antivirus Update-motorn på datorn  

1. Öppna en kommandotolk som administratör.

2. Ange följande kommandon:

    ```cmd
    cd \

    cd program files\windows defender

    MpCmdRun -RemoveDefinitions -all

    exit
    ```

3. Starta om datorn.  

4. Försök att uppdatera Windows Defender igen.

Fortsätt till nästa steg om problemet kvarstår.  

#### <a name="step-5-manually-install-the-definition-updates"></a>Steg 5: installera definitions uppdateringarna manuellt  

[Hämta de senaste uppdateringarna manuellt](https://www.microsoft.com/en-us/wdsi/defenderupdates).  

#### <a name="step-6-contact-microsoft-support"></a>Steg 6: kontakta Microsoft-supporten  

Kontakta Microsoft-supporten om de här stegen inte löste problemet. Mer information finns i [Support alternativ och grupp resurser](../../core/understand/find-help.md#BKMK_SupportOptions).  

## <a name="starting-windows-defender-or-endpoint-protection-service"></a>Uppdatera tjänsten Windows Defender eller Endpoint Protection

### <a name="symptom"></a>Symptom

Du får ett meddelande som meddelar dig att **Windows Defender eller Endpoint Protection inte övervakar datorn, eftersom programmets tjänst har stoppats. Du bör starta om den nu.**

### <a name="solution"></a>Lösning

#### <a name="step-1-restart-your-computer"></a>Steg 1: starta om datorn

Stäng alla program och starta om datorn.  

#### <a name="step-2-check-the-windows-service"></a>Steg 2: kontrol lera Windows-tjänsten

1. Gå till **Start**och öppna **Services. msc**.  

2. Välj **tjänsten Windows Defender Antivirus**.  

3. Kontrol lera att **Start typen** är inställd på **Automatisk**.

4. Gå till **åtgärd** -menyn och välj **Starta**.

    1. Om den här åtgärden inte är tillgänglig väljer du **stoppa**. Vänta tills tjänsten har stoppats och välj sedan **Start** åtgärd för att starta om tjänsten.  

Observera eventuella fel som kan uppstå under den här processen. [Kontakta Microsoft Support](../../core/understand/find-help.md#BKMK_SupportOptions) och ange fel information.  

#### <a name="step-3-remove-any-third-party-security-programs"></a>Steg 3: ta bort alla säkerhets program från tredje part  

> [!NOTE]  
> Vissa säkerhets program avinstalleras inte helt. Du kan behöva hämta och köra ett rensnings verktyg för ditt tidigare säkerhets program för att helt ta bort det.  

1. Gå till **Start** och öppna **appwiz. cpl**.  

2. I listan över installerade program avinstallerar du eventuella säkerhets program från tredje part.

3. Starta om datorn.  

> [!CAUTION]  
> När du tar bort säkerhets program kan datorn vara oskyddad. Om du har problem med att installera Windows Defender efter att du har tagit bort befintliga säkerhets program kontaktar du [Microsoft Support](https://support.microsoft.com/supportforbusiness/productselection). Välj produkt familjen för **säkerhet** och sedan **Windows Defender** -produkten.

## <a name="internet-connection-issues"></a>Problem med Internetanslutning

För att datorn ska kunna ta emot de senaste uppdateringarna från Windows Update ansluter du den till Internet.  

1. Gå till **Start** och öppna **ncpa. cpl**.  

2. Öppna anslutnings namnet för att Visa anslutnings **status**.  

3. Om datorn är ansluten är status för **IPv4-anslutning** och/eller **IPv6-anslutning** **Internet**.  

4. Om datorn inte verkar vara ansluten väljer du anslutnings namnet och väljer **diagnostisera den här anslutningen**.

Stäng eventuella öppna program och starta om datorn.  

## <a name="detected-threat-cant-be-remediated"></a> Det identifierade hotet kan inte åtgärdas

När Windows Defender eller Endpoint Protection identifierar ett potentiellt hot försöker det att minimera hotet genom att sätta eller ta bort hotet. Dessa hot kan döljas i ett komprimerat`.zip`arkiv () eller på en nätverks resurs.

### <a name="remove-or-scan-the-file"></a>Ta bort eller genomsök filen  

- Om det identifierade hotet fanns i en komprimerad arkivfil bläddrar du till filen. Ta bort filen eller Genomsök den manuellt. Högerklicka på filen och välj **Genomsök med Windows Defender**. Om Windows Defender identifierar ytterligare hot i filen, meddelas du. Sedan kan du välja en lämplig åtgärd.  

- Om det identifierade hotet låg i en nätverks resurs, öppnar du resursen och genomsöker den manuellt. Högerklicka på filen och välj **Genomsök med Windows Defender**. Om Windows Defender identifierar ytterligare hot i nätverks resursen, meddelas du. Sedan kan du välja en lämplig åtgärd.  

- Om du inte är säker på filens ursprung kan du köra en fullständig genomsökning på datorn. En fullständig genomsökning kan ta lite tid att slutföra.  

## <a name="see-also"></a>Se även

[Vanliga frågor och svar om Endpoint Protection klient](endpoint-protection-client-faq.md)

[Klienthjälp för Endpoint Protection](endpoint-protection-client-help.md)
