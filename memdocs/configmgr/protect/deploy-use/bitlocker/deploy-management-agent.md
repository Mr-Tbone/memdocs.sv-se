---
title: Distribuera BitLocker-hantering
titleSuffix: Configuration Manager
description: Distribuera hanterings agenten för BitLocker till Configuration Manager klienter och återställnings tjänsten till hanterings platser
ms.date: 07/27/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 39aa0558-742c-4171-81bc-9b1e6707f4ea
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ba72e9accb7cbc5a7dc1149c6c9d947cb3e0692b
ms.sourcegitcommit: 7e34b561d43aa086fc07ab4edf2230d09c04f05b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/03/2020
ms.locfileid: "87526091"
---
# <a name="deploy-bitlocker-management"></a>Distribuera BitLocker-hantering

*Gäller för: Configuration Manager (aktuell gren)*

<!--3601034-->

BitLocker-hanteringen i Configuration Manager innehåller följande komponenter:

- **BitLocker-hanterings agent**: Configuration Manager aktiverar den här agenten på en enhet när du [skapar en princip](#create-a-policy) och [distribuerar den till en samling](#deploy-a-policy).

- **Återställnings tjänst**: Server komponenten som tar emot BitLocker-återställningsinformation från klienter. Mer information finns i [återställnings tjänsten](#recovery-service).

Innan du skapar och distribuerar principer för hantering av BitLocker:

- Granska [kraven](../../plan-design/bitlocker-management.md#prerequisites)

- Om det behövs [krypterar du återställnings nycklar](encrypt-recovery-data.md) i plats databasen

## <a name="create-a-policy"></a>Skapa en princip

När du skapar och distribuerar den här principen aktiverar Configuration Manager klienten BitLocker-hanteringsservern på enheten.

> [!NOTE]
> Om du vill skapa en princip för BitLocker-hantering behöver du rollen **Fullständig administratör** i Configuration Manager.

1. Gå till arbets ytan **till gångar och efterlevnad** i Configuration Manager-konsolen, expandera **Endpoint Protection**och välj noden **BitLocker-hantering** .

1. I menyfliksområdet väljer du **Skapa princip för BitLocker-hanterings kontroll**.

1. På sidan **Allmänt** anger du ett namn och en valfri beskrivning. Välj de komponenter som ska aktive ras på klienter med den här principen:  

    - **Operativ system enhet**: hantera om operativ system enheten är krypterad

    - **Fast enhet**: hantera kryptering för ytterligare data enheter i en enhet

    - **Flyttbar enhet**: hantera kryptering för enheter som du kan ta bort från en enhet, till exempel en USB-nyckel

    - **Klient hantering**: hantera säkerhets kopiering av nyckel återställnings tjänsten för BitLocker-diskkryptering återställnings information  

1. På sidan **installation** konfigurerar du följande globala inställningar för BitLocker-diskkryptering:

    > [!NOTE]
    > Configuration Manager tillämpar dessa inställningar när du aktiverar BitLocker. Om enheten redan är krypterad eller pågår ändras inte enhetens kryptering på enheten.
    >
    > Om du inaktiverar eller inte konfigurerar de här inställningarna använder BitLocker standard krypterings metoden (AES 128-bit).

    - För Windows 8,1-enheter aktiverar du alternativet för **enhets krypterings metod och krypterings styrka**. Välj sedan krypterings metod.

    - För Windows 10-enheter aktiverar du alternativet för **enhets krypterings metod och krypterings styrka (Windows 10)**. Välj en separat krypterings metod för OS-enheter, fasta data enheter och flyttbara data enheter.

    Mer information om dessa och andra inställningar på den här sidan finns i [Inställningar referens-konfiguration](../../tech-ref/bitlocker/settings.md#setup).

1. På sidan **operativ system enhet** anger du följande inställningar:  

    - **Krypterings inställningar för operativ system enhet**: om du aktiverar den här inställningen måste användaren skydda operativ system enheten och BitLocker krypterar enheten. Om du inaktiverar den kan användaren inte skydda enheten.  

    På enheter med en kompatibel TPM kan två typer av autentiseringsmetoder användas vid start för att ge extra skydd för krypterade data. När datorn startas kan den endast använda TPM: en för autentisering, eller så kan du också kräva att en PIN-kod tas med på en personlig kod. Konfigurera följande inställningar:

    - **Välj skydd för operativ system enhet**: Konfigurera den att använda en TPM och PIN-kod eller bara TPM.

    - **Konfigurera minimilängd för PIN-kod för start**: om du behöver en PIN-kod är det här värdet den kortaste längd som användaren kan ange. Användaren anger denna PIN-kod när datorn startar för att låsa upp enheten. Som standard är minimilängd för PIN-kod `4` .

    Mer information om dessa och andra inställningar på den här sidan finns i [Inställningar referens-OS-enhet](../../tech-ref/bitlocker/settings.md#os-drive).

1. På sidan **fast enhet** anger du följande inställningar:

    - **Kryptering av fast data enhet**: om du aktiverar den här inställningen kräver BitLocker att användare lägger till alla fasta data enheter under skyddet. Sedan krypteras data enheterna. När du aktiverar den här principen aktiverar du antingen automatisk upplåsning eller inställningarna för **lösen ords princip för fast data enhet**.

    - **Konfigurera automatisk upplåsning för fast data enhet**: Tillåt eller Kräv att BitLocker automatiskt låser upp en krypterad data enhet. Om du vill använda automatisk upplåsning måste du också använda BitLocker för att kryptera operativ system enheten.

    Mer information om dessa och andra inställningar på den här sidan finns i [Settings Reference-Fixed Drive](../../tech-ref/bitlocker/settings.md#fixed-drive).

1. På sidan **flyttbar enhet** anger du följande inställningar:

    - **Kryptering av flyttbara data enheter**: när du aktiverar den här inställningen och tillåter att användare använder BitLocker-skyddet sparar Configuration Manager klienten återställnings information om flyttbara enheter till återställnings tjänsten på hanterings platsen. Med det här beteendet kan användare återställa enheten om de glömmer bort eller förlorar skydds inställningen (lösen ordet).

    - **Tillåt att användare använder BitLocker-skydd på flyttbara data enheter**: användare kan aktivera BitLocker-skyddet för en flyttbar enhet.

    - **Lösen ords princip för flyttbara data enheter**: Använd de här inställningarna för att ange begränsningar för lösen ord för att låsa upp BitLocker-skyddade flyttbara enheter.

    Mer information om dessa och andra inställningar på den här sidan finns i [Inställningar referens-flyttbar enhet](../../tech-ref/bitlocker/settings.md#removable-drive).

1. På sidan **klient hantering** anger du följande inställningar:

    > [!IMPORTANT]
    > Konfigurera inte den här inställningen om du inte har en hanterings plats med en HTTPS-aktiverad webbplats. Mer information finns i [återställnings tjänsten](#recovery-service).

    - **Konfigurera BitLocker-hanterings tjänster**: när du aktiverar den här inställningen Configuration Manager automatiskt och säkerhetskopiera nyckel återställnings information i plats databasen. Om du inaktiverar eller inte konfigurerar den här inställningen sparar Configuration Manager inte nyckel återställnings information.

        - **Välj BitLocker-återställningsinformation som ska lagras**: Konfigurera den att använda ett återställnings lösen ord och nyckel paket, eller bara ett återställnings lösen ord.

        - **Tillåt att återställnings information lagras i oformaterad text**: utan ett BitLocker-Management-krypterings certifikat, Configuration Manager lagra nyckel återställnings informationen i oformaterad text. Mer information finns i [kryptera återställnings data](encrypt-recovery-data.md).

    Mer information om dessa och andra inställningar på den här sidan finns i [Inställningar referens-klient hantering](../../tech-ref/bitlocker/settings.md#client-management).

1. Slutför guiden.

Om du vill ändra inställningarna för en befintlig princip väljer du den i listan och väljer **Egenskaper**.

När du skapar fler än en princip kan du konfigurera deras relativa prioritet. Om du distribuerar flera principer till en klient använder den prioritet svärdet för att fastställa dess inställningar.

## <a name="deploy-a-policy"></a>Distribuera en princip

1. Välj en befintlig princip i noden **BitLocker-hantering** . I menyfliksområdet väljer du **distribuera**.

1. Välj en enhets samling som mål för distributionen.

1. Om du vill att enheten ska kunna kryptera eller dekryptera sina enheter när som helst väljer du alternativet för att **tillåta reparation utanför underhålls fönstret**. Om samlingen har ett underhålls fönster repare ras den här BitLocker-principen.

1. Konfigurera ett **enkelt** eller **anpassat** schema. Klienten utvärderar sitt kompatibilitet baserat på de inställningar som anges i schemat.

1. Välj **OK** för att distribuera principen.

Du kan skapa flera distributioner av samma princip. Om du vill visa mer information om varje distribution väljer du principen i noden **BitLocker-hantering** och växlar sedan till fliken **distributioner** i informations fönstret.

> [!IMPORTANT]
> MBAM-klienten startar inte BitLocker-diskkryptering åtgärder om en anslutning till fjärr skrivbords protokoll är aktiv. Alla anslutningar till fjärr konsolen måste vara stängda och en användare måste vara inloggad på en fysisk konsolsession innan BitLocker-diskkryptering börjar.


## <a name="monitor"></a>Övervaka

Visa grundläggande Kompatibilitetsrapport om princip distributionen i informations fönstret för noden **BitLocker-hantering** :

- Antal kompatibla
- Antal haverier
- Antal ej kompatibla

Växla till fliken **distributioner** om du vill se kompatibiliteten i procent och Rekommenderad åtgärd. Välj distributionen och välj sedan **Visa status**i menyfliksområdet. Den här åtgärden växlar vyn till arbets ytan **övervakning** , noden **distributioner** . Precis som distributionen av andra distributioner av konfigurations principer kan du se mer detaljerad kompatibilitetsstatus i den här vyn.

Information om varför klienter rapporterar att de inte är kompatibla med principen för BitLocker-hantering finns i [koder för inkompatibilitet](../../tech-ref/bitlocker/non-compliance-codes.md).

Mer felsöknings information finns i [Felsöka BitLocker](../../tech-ref/bitlocker/troubleshoot.md).

Använd följande loggar för att övervaka och felsöka:

### <a name="client-logs"></a>Klient loggar

- MBAM-händelse logg: i Windows Loggboken bläddrar du till program och tjänster > Microsoft > Windows > MBAM.  Mer information finns i [om händelse](../../tech-ref/bitlocker/about-event-logs.md) loggar för BitLocker och [klient händelse loggar](../../tech-ref/bitlocker/client-event-logs.md).

- **BitlockerMangementHandler. log** i klient loggar Sök väg, `%WINDIR%\CCM\Logs` som standard

### <a name="management-point-logs-recovery-service"></a>Hanterings plats loggar (återställnings tjänst)

- Händelse logg för återställnings tjänst: i Windows Loggboken bläddrar du till program och tjänster > Microsoft > Windows > MBAM-Web. Mer information finns i [om händelse](../../tech-ref/bitlocker/about-event-logs.md) loggar för BitLocker och [Server händelse loggar](../../tech-ref/bitlocker/server-event-logs.md).

- Spårnings loggar för återställnings tjänsten:`<Default IIS Web Root>\Microsoft BitLocker Management Solution\Logs\Recovery And Hardware Service\trace*.etl`

## <a name="recovery-service"></a>Återställnings tjänst

BitLocker-återställningsnyckeln är en Server komponent som tar emot BitLocker-återställningsinformation från Configuration Manager klienter. Platsen distribuerar återställnings tjänsten när du skapar en princip för BitLocker-hantering. Configuration Manager installerar återställnings tjänsten automatiskt på varje hanterings plats med en HTTPS-aktiverad webbplats.

Configuration Manager lagrar återställnings informationen i plats databasen. Utan ett BitLocker Management Encryption-certifikat, Configuration Manager lagra nyckel återställnings informationen i oformaterad text.

Mer information finns i [kryptera återställnings data](encrypt-recovery-data.md).

## <a name="migration-considerations"></a>Överväganden vid migrering

Om du för närvarande använder Microsoft BitLocker administration och övervakning (MBAM) kan du sömlöst migrera hanteringen till Configuration Manager. När du distribuerar BitLocker-hanterings principer i Configuration Manager laddar klienterna automatiskt upp återställnings nycklar och paket till Configuration Manager återställnings tjänsten.

> [!IMPORTANT]
> När du migrerar från fristående MBAM till Configuration Manager BitLocker-hantering, om du behöver befintliga funktioner i fristående MBAM, återanvänder du inte fristående MBAM-servrar eller-komponenter med Configuration Manager BitLocker-hantering. Om du återanvänder dessa servrar slutar fristående MBAM att fungera när Configuration Manager BitLocker-hanteringen installerar dess komponenter på dessa servrar. Kör inte MBAMWebSiteInstaller.ps1-skriptet för att konfigurera BitLocker-portalerna på fristående MBAM-servrar. När du konfigurerar Configuration Manager BitLocker-hantering använder du separata servrar.

### <a name="group-policy"></a>Grup princip

- Inställningarna för BitLocker-hantering är helt kompatibla med MBAM grup princip inställningar. Om enheterna tar emot både grup princip inställningar och Configuration Manager principer konfigurerar du dem att matcha.

  > [!NOTE]
  > Om det finns en grup princip inställning för fristående MBAM, kommer den att åsidosätta motsvarande inställning som görs av Configuration Manager. Fristående MBAM använder domän grup principer, medan Configuration Manager anger lokala principer för BitLocker-hantering. Domän principer åsidosätter de lokala Configuration Manager hanterings principerna för BitLocker. Om den fristående MBAM domän grup principen inte matchar den Configuration Manager principen kommer Configuration Manager BitLocker-hanteringen att Miss Missing. Om en domän grup princip till exempel anger den fristående MBAM-servern för nyckel återställnings tjänster kan Configuration Manager BitLocker-hanteringen inte ange samma inställning för hanterings platsen. Det här beteendet gör att klienter inte rapporterar sina återställnings nycklar till Configuration Manager BitLocker Management Key Recovery-tjänsten på hanterings platsen.

- Configuration Manager implementerar inte alla grup princip inställningar för MBAM. Om du konfigurerar ytterligare inställningar i en grup princip, kommer BitLocker-hanteringsservern på Configuration Manager klienter att respektera dessa inställningar.

  > [!IMPORTANT]
  > Ange inte en grup princip för en inställning som Configuration Manager BitLocker-hanteringen redan anger. Ange bara grup principer för inställningar som för närvarande inte finns i Configuration Manager BitLocker-hantering. Configuration Manager version 2002 har funktions paritet med fristående MBAM. I de flesta fall bör det inte finnas någon anledning att ange domän grup principer för att konfigurera BitLocker-principer med Configuration Manager version 2002 och senare. Undvik att använda grup principer för BitLocker för att förhindra konflikter och problem. Konfigurera alla inställningar genom att Configuration Manager BitLocker-hanterings principer.

### <a name="tpm-password-hash"></a>Hash för TPM-lösenord

- Tidigare MBAM-klienter överför inte TPM-lösenords-hash till Configuration Manager. Klienten överför bara TPM: ens hash-lösenord en gång.

- Om du behöver migrera den här informationen till Configuration Manager återställnings tjänsten rensar du TPM på enheten. När den har startats om överförs den nya hashen för TPM-lösenord till återställnings tjänsten.

### <a name="re-encryption"></a>Ny kryptering

Configuration Manager krypterar inte enheter som redan är skyddade med BitLocker-diskkryptering. Om du distribuerar en princip för BitLocker-hantering som inte matchar enhetens nuvarande skydd rapporteras den som icke-kompatibel. Enheten är fortfarande skyddad.

Du använde till exempel MBAM för att kryptera enheten med krypteringsalgoritmen AES-XTS 128, men Configuration Manager principen kräver AES-XTS 256. Enheten är inte kompatibel med principen, även om enheten är krypterad.

Undvik det här problemet genom att först inaktivera BitLocker på enheten. Distribuera sedan en ny princip med de nya inställningarna.

## <a name="co-management-and-intune"></a>Samhantering och Intune

<!-- SCCMDocs#2321 -->

Configuration Manager klient hanterare för BitLocker är medveten om samhantering. Om enheten är samhanterad och du växlar [Endpoint Protection arbets belastning](../../../comanage/workloads.md#endpoint-protection) till Intune, ignorerar Configuration Manager klienten dess BitLocker-princip. Enheten hämtar Windows-krypterings princip från Intune.

När du växlar krypterings hanterings utfärdare och önskad krypteringsalgoritm också ändras, måste du planera för [omkryptering](#re-encryption) .

Mer information om hur du hanterar BitLocker med Intune finns i följande artiklar:

- [Använda enhets kryptering med Intune](../../../../intune/protect/encrypt-devices.md)
- [Felsöka BitLocker-principer i Microsoft Intune](../../../../intune/protect/troubleshoot-bitlocker-policies.md)

## <a name="next-steps"></a>Nästa steg

[Konfigurera BitLocker-rapporter och portaler](setup-websites.md)
