---
title: Krypteringsrapport för krypterade enheter i Microsoft Intune
titleSuffix: Microsoft Intune
description: Visa en rapport över krypteringsstatusen för iOS/iPadOS- eller Windows-enheter och få åtkomst till FileVault- och BitLocker-återställningsnycklar från Microsoft Intune-portalen.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/18/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: shpate
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.openlocfilehash: 1199c6db96325a103394cfb53a4ca70092cd3767
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989659"
---
# <a name="monitor-device-encryption-with-intune"></a>Övervaka enhetskryptering med Intune

Krypteringsrapporten i Microsoft Intune är en central plats där du kan visa information om en enhets krypteringsstatus och se alternativ för hantering av enhetsåterställningsnycklar. Vilka alternativ för återställningsnycklar som är tillgängliga beror på vilken typ av enhet du visar.

Logga in på [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) om du vill leta reda på rapporten. Välj **Enheter** > **Övervaka** och välj **Krypteringsrapport** under *Konfiguration*.

## <a name="view-encryption-details"></a>Visa krypteringsinformation

Krypteringsrapporten innehåller allmän information för de hanterade enheter som stöds. I följande avsnitt finns information om vilken information som Intune visar i rapporten.

### <a name="prerequisites"></a>Krav

Krypteringsrapporten stöder rapportering på enheter som kör följande operativsystemversioner:

- macOS 10.13 eller senare
- Windows version 1607 eller senare

### <a name="report-details"></a>Rapportinformation

Fönstret Krypteringsrapport innehåller en lista över de enheter som du hanterar med översiktlig information om enheterna. Du kan välja en enhet i listan om du vill granska och visa mer information i fönstret [Enhetens krypteringsstatus.](#device-encryption-status)

- **Enhetsnamn** – Namnet på enheten.
- **Operativsystem** – Enhets plattform, till exempel Windows eller macOS.
- **Operativsystemversion** – Versionen av Windows eller macOS på enheten.
- **TPM-version** *(gäller endast Windows 10)* – Versionen av TPM-kretsen (Trusted Platform Module) på Windows 10-enheten.
- **Krypteringsberedskap** – En utvärdering av enheternas beredskap för en viss krypteringsteknik, t.ex. BitLocker- eller FileVault-kryptering. Enheter identifieras som:
  - **Redo**: Enheten kan krypteras med MDM-principen, som kräver att enheten uppfyller följande krav:

    **För macOS-enheter**:
    - MacOS version 10.13 eller senare

    **För Windows 10-enheter**:
    - Version 1709 eller senare av *Business*, *Enterprise* eller *Education*, eller version 1809 eller senare av *Pro*
    - Enheten måste ha en TPM-krets

    Mer information finns i [BitLocker-CSP](https://docs.microsoft.com/windows/client-management/mdm/bitlocker-csp) i Windows-dokumentationen.

  - **Ej redo**: Enheten har inte fullständiga krypteringsfunktioner, men har fortfarande stöd för kryptering. Exempelvis kan en Windows-enhet krypteras manuellt av en användare, eller via en grupprincip som kan konfigureras att tillåta kryptering utan en TPM.
  - **Ej tillämpligt**: Det finns inte tillräckligt med information för att klassificera den här enheten.

- **Krypteringsstatus** – avser huruvida OS-enheten är krypterad.

- **Namn på användarprincip** – Enhetens primära användare.

### <a name="device-encryption-status"></a>Enhetskrypteringsstatus

När du väljer en enhet från krypteringsrapporten visas fönstret **Enhetens krypteringsstatus** i Intune. Det här fönstret innehåller följande information:

- **Enhetsnamn** – namnet på den enhet som du visar.

- **Krypteringsberedskap** – En utvärdering av enheternas beredskap för kryptering via MDM-principen.

  Exempel: När en Windows 10-enhet har beredskapen *Inte klar* kan den fortfarande ha stöd för kryptering. För att Windows 10-enheten ska ha statusen *Klar* måste den ha en TPM-krets. TPM-kretsar krävs inte för att det ska gå att kryptera. (Mer information finns i *Krypteringsberedskap* i föregående avsnitt.)

- **Krypteringsstatus** – avser huruvida OS-enheten är krypterad. Det kan ta upp till 24 timmar innan Intune rapporterar om enhetens krypteringsstatus eller en statusändring. Tiden omfattar tiden då operativsystemet ska krypteras plus den tid då enheten ska rapportera tillbaka till Intune.

  Om du vill påskynda rapporteringen av FileVault-krypteringsstatus innan enhetsincheckningen normalt sker låter du användarna synkronisera sina enheter när krypteringen har slutförts.

- **Profiler** – En lista över *enhetskonfigurationsprofilerna* som gäller för den här enheten och som är konfigurerade med följande värden:

  - macOS:
    - Profiltyp = *Slutpunktsskydd*
    - Inställningar > FileVault > FileVault = *Aktivera*

  - Windows 10:
    - Profiltyp = *Slutpunktsskydd*
    - Inställningar > Windows-kryptering > Kryptera enheter = *Kräv*

  Du kan använda listan över profiler för att identifiera enskilda principer för granskning om *Sammanfattning av profilstatus* indikerar problem.

- **Sammanfattning av profiltillstånd** – en sammanfattning av de profiler som gäller för den här enheten. Sammanfattningen representerar det minst fördelaktiga tillståndet bland de tillämpliga profilerna. Om till exempel bara en av flera tillämpliga profiler resulterar i ett fel visar *Sammanfattning av profilstatus* *Fel*.

  Om du vill se mer information för en status går du till **Intune** > **Enhetskonfiguration** > **Profiler** och väljer profilen. Du kan också välja **Enhetsstatus** och sedan välja en enhet.

- **Statusinformation** – avancerad information om enhetens krypteringstillstånd.

  > [!IMPORTANT]
  > För Windows 10-enheter visar Intune endast *statusinformation* för enheter som kör *Windows-uppdateringen från 10 april 2019* eller senare.

  Det här fältet visar information för varje tillämpligt fel som kan identifieras. Du kan använda den här informationen för att förstå varför en enhet kanske inte är redo för kryptering.

  Följande är några exempel på den statusinformation som Intune kan rapportera:

  **macOS**:
  - Återställningsnyckeln har inte hämtats och lagrats ännu. Förmodligen har enheten inte låsts upp, eller så har den inte checkat in.

    *Tänk på att: Det här resultatet inte nödvändigtvis är ett feltillstånd, utan ett tillfälligt tillstånd som kan bero på en tidsinställning på enheten där återställningsnycklarnas deponering måste konfigureras innan krypteringsbegäran skickas till enheten. Denna status kan även indikera att enheten är låst eller inte har checkat in med Intune nyligen. Eftersom FileVault-kryptering inte startar förrän en enhet är ansluten (laddas) är det möjligt för en användare att ta emot en återställningsnyckel för en enhet som ännu inte har krypterats*.

  - Användaren skjuter upp krypteringen eller håller för närvarande på med krypteringsprocessen.

    *Tänk på att: Antingen har användaren inte loggat ut än efter att ha tagit emot krypteringsbegäran, vilket är nödvändigt innan FileVault kan kryptera enheten, eller så har användaren dekrypterat enheten manuellt. Intune kan inte hindra en användare från att dekryptera sin enhet.*

  - Enheten är redan krypterad. Enhetsanvändaren måste dekryptera enheten för att kunna fortsätta.

    *Tänk på att: Intune kan inte konfigurera FileVault på en enhet som redan är krypterad. I stället måste användaren dekryptera enheten manuellt innan den kan hanteras av en enhetskonfigurationsprincip och Intune*.

  - FileVault kräver att användaren godkänner sin hanteringsprofil i macOS Catalina och senare.

    *Tänk på att: Från och med macOS version 10.15 (Catalina) kan användargodkända registreringsinställningar resultera i kravet att användare godkänner FileVault-kryptering manuellt. Mer information finns i avsnittet [om användargodkänd registrering](../enrollment/macos-enroll.md) i Intune-dokumentationen*.

  - Okänt.

    *Tänk på att: En möjlig orsak till okänd status är att enheten är låst och att Intune inte kan starta depositions- eller krypteringsprocessen. När enheten har låsts upp kan förloppet fortsätta*.

  **Windows 10**:
  - BitLocker-principen kräver användarens medgivande för att starta guiden för BitLocker-diskkryptering för att starta kryptering av OS-volymen, men användare gav inte sitt medgivande.

  - OS-volymens krypteringsmetod matchar inte BitLocker-principen.

  - BitLocker-principen kräver ett TPM-skydd för att skydda OS-volymen, men TPM används inte.

  - BitLocker-principen kräver ett skydd som endast använder TPM för OS-volymen, men TPM-skydd används inte.

  - BitLocker-principen kräver skydd med TPM och PIN-kod för OS-volymen, men skydd med TPM och PIN-kod används inte.

  - BitLocker-principen kräver skydd med TPM och startnyckel för OS-volymen, men skydd med TPM och startnyckel används inte.

  - BitLocker-principen kräver skydd med TPM, PIN-kod och startnyckel för OS-volymen, men skydd med TPM, PIN-kod och startnyckel används inte.

  - OS-volymen är inte skyddad.

  - Säkerhetskopiering av återställningsnyckel misslyckades.

  - En fast enhet är oskyddad.

  - Den fasta enhetens krypteringsmetod matchar inte BitLocker-principen.

  - För att kryptera enheter kräver BitLocker-principen antingen att användaren loggar in som administratör eller, om enheterna är ansluten till Azure AD, att principen AllowStandardUserEncryption anges till 1.

  - Windows Recovery Environment (WinRE) är inte konfigurerat.

  - Ingen TPM är tillgänglig för BitLocker, antingen eftersom den inte finns eller har gjorts otillgänglig i registret, eller på grund av att operativsystemet finns på en flyttbar enhet.

  - TPM:en är inte redo för BitLocker.

  - Nätverket är inte tillgängligt, vilket krävs för säkerhetskopiering av återställningsnyckel.

## <a name="export-report-details"></a>Exportera rapportinformation

När du visar fönstret Krypteringsrapport kan du välja **Exportera** för att ladda ned en *CSV*-fil med rapportinformation. Den här rapporten innehåller översiktlig information från fönstret *Krypteringsrapport* och *Enhetens krypteringsstatus* för varje enhet som du hanterar.

![Exportera information](./media/encryption-monitor/export.png)

Den här rapporten kan användas för att identifiera problem för grupper av enheter. Du kan till exempel använda rapporten för att identifiera en lista med macOS-enheter som alla rapporterar *FileVault har redan aktiverats av användaren*, vilket indikerar enheter som måste dekrypteras manuellt innan Intune kan hantera deras FileVault-inställningar.

## <a name="manage-recovery-keys"></a>Hantera återställningsnycklar

Mer information om att hantera återställningsnycklar finns i följande avsnitt i Intune-dokumentationen:

macOS FileVault:
- [Hämta privat återställningsnyckel](../protect/encrypt-devices-filevault.md#retrieve-personal-recovery-key)
- [Rotera återställningsnycklar](../protect/encrypt-devices-filevault.md#rotate-recovery-keys)
- [Återställa återställningsnycklar](../protect/encrypt-devices-filevault.md#recover-recovery-keys)

Windows 10 BitLocker:
- [Rotera återställningsnycklar för BitLocker](../protect/encrypt-devices.md#rotate-bitlocker-recovery-keys)

## <a name="next-steps"></a>Nästa steg

[Hantera policy för BitLocker](../protect/encrypt-devices.md)

[Hantera policy för FileVault](encrypt-devices-filevault.md)
