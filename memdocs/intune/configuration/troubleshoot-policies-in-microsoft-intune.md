---
title: Felsöka principer i Microsoft Intune – Azure | Microsoft Docs
description: Se hur du använder den inbyggd felsökningsfunktion och läs om vanliga problem eller frågor och lösningar på dem när du använder efterlevnadsprinciper och konfigurationsprofiler i Microsoft Intune
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/18/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 99fb6db6-21c5-46cd-980d-50f063ab8ab8
ROBOTS: ''
ms.reviewer: tscott
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: f3aaf2bf895082f3647f0a1ad6b9997a5e97baee
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79364129"
---
# <a name="troubleshoot-policies-and-profiles-and-in-intune"></a>Felsökning av principer och profiler i Intune

Microsoft Intune har några inbyggda felsökningsprinciper. Med hjälp av dessa funktioner kan du felsöka efterlevnadsprinciper och konfigurationsprofiler i din miljö.

I den här artikeln beskrivs några vanliga felsökningsmetoder och några problem du kan stöta på.

## <a name="check-tenant-status"></a>Kontrollera klientorganisationens status

Kontrollera [Klientorganisationens status](../fundamentals/tenant-status.md) och bekräfta att prenumerationen är aktiv. Du kan också visa information om aktiva incidenter och rekommendationer som kan påverka din princip eller profildistribution.

## <a name="use-built-in-troubleshooting"></a>Använda inbyggd felsökning

1. Välj **Felsökning och support** i [Administrationscenter för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431):

    ![Gå till Hjälp och support i Intune och välj Felsök](./media/troubleshoot-policies-in-microsoft-intune/help-and-support-troubleshoot.png)

2. Välj **Välj användare** > välj användaren som har ett problem > **Välj**.
3. Bekräfta att **Intune-licens** och **Kontostatus** har gröna bockmarkeringar:

    ![I Intune väljer du användaren och bekräftar att Kontostatus och Intune-licens har gröna bockmarkeringar för statusen](./media/troubleshoot-policies-in-microsoft-intune/account-status-intune-license-show-green.png)

    **Användbara länkar**:

    - [Tilldela licenser så att användare kan registrera enheter](../fundamentals/licenses-assign.md)
    - [Lägga till användare i Intune](../fundamentals/users-add.md)

4. Under **Enheter** letar du reda på enheten som har problem. Granska de olika kolumnerna:

    - **Hanterad**: För att en enhet ska kunna ta emot efterlevnads- eller konfigurationsprinciper måste värdet för egenskapen vara **MDM** eller **EAS/MDM**.

        - Om **Hanterad** inte är inställt på **MDM** eller **EAS/MDM** är enheten inte registrerad. Den tar inte emot efterlevnads- eller konfigurationsprinciper förrän den har registrerats.

        - Skyddsprinciper för appar (hantering av mobilprogram) kräver inte att enheter är registrerade. Mer information finns i [Skapa och tilldela skyddsprinciper för appar](../apps/app-protection-policies.md).

    - **Azure AD-anslutningstyp**: Ska vara inställt på **Arbetsplats** eller **AzureAD**.
 
        - Om kolumnen är **Inte registrerad** kan det finnas ett problem med registreringen. Normalt löser du problemet genom att avregistrera och registrera på nytt.

    - **Intune-kompatibel**: Ska vara **Ja**. Om **Nej** visas kan det finnas ett problem med efterlevnadsprinciperna, eller så ansluts inte enheten till Intune-tjänsten. Till exempel kan enheten ha stängts av eller sakna nätverksanslutning. Till slut blir enheten icke-kompatibel, möjligen efter 30 dagar.

        Mer information finns i [Komma igång med efterlevnadsprinciper för enheter i Intune](../protect/device-compliance-get-started.md).

    - **Azure AD-kompatibel**: Ska vara **Ja**. Om **Nej** visas kan det finnas ett problem med efterlevnadsprinciperna, eller så ansluts inte enheten till Intune-tjänsten. Till exempel kan enheten ha stängts av eller sakna nätverksanslutning. Till slut blir enheten icke-kompatibel, möjligen efter 30 dagar.

        Mer information finns i [Komma igång med efterlevnadsprinciper för enheter i Intune](../protect/device-compliance-get-started.md).

    - **Senaste incheckning**: Ska vara en nylig tid och ett nyligt datum. Som standard checkar Intune-enheter in var 8:e timme.

        - Om **Senaste incheckning** är mer än 24 timmar sedan kan det vara problem med enheten. En enhet som inte kan checka in tar inte emot dina principer från Intune.

        - Framtvinga incheckning:
            - På Android-enheten öppnar du appen Företagsportal > **Enheter** > välj enheten i listan > **Kontrollera enhetsinställningarna**.
            - Gå till iOS/iPadOS-enheten, öppna appen Företagsportal > **Enheter** > välj enheten i listan > **Kontrollera inställningar**.

        - På en Windows-enhet öppnar du **Inställningar** > **Konton** > **Åtkomst till arbete eller skola** > välj kontot eller MDM-registreringen > **Info** > **Synkronisera**.

    - Välj enhet för att se principspecifik information.

        **Enhetsefterlevnad** visar statusar för efterlevnadsprinciper som tilldelats till enheten.

        **Enhetskonfiguration** visar statusar för konfigurationsprinciper som tilldelats till enheten.

        Om de förväntade principerna inte visas under **Enhetsefterlevnad** eller **Enhetskonfiguration** är principerna inte rätt riktade. Öppna principen och tilldela principen till den här användaren eller enheten.

        **Principtillstånd**:

        - **Inte tillämpligt**: Principen stöds inte på den här plattformen. iOS/iPadOS-principer fungerar t.ex. inte på Android. Samsung KNOX-principer fungerar inte på Windows-enheter.
        - **Konflikt**: Det finns en befintlig inställning på enheten som Intune inte kan åsidosätta. Eller så har du distribuerat två principer med samma inställning med olika värden.
        - **Väntar**: Enheten har inte checkats in i Intune för att få principen. Eller så har enheten tagit emot principen men har inte rapporterat statusen till Intune.
        - **Fel**: Du hittar fel och möjliga lösningar i [Felsöka åtkomstproblem för företagsresurser](../fundamentals/troubleshoot-company-resource-access-problems.md).

        **Användbara länkar**: 

        - [Sätt att distribuera policyer för efterlevnad för enheter](../protect/device-compliance-get-started.md#ways-to-deploy-device-compliance-policies)
        - [Övervaka principer för enhetsefterlevnad](../protect/compliance-policy-monitor.md)

## <a name="youre-unsure-if-a-profile-is-correctly-applied"></a>Du är osäker på om en profil tillämpas korrekt

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj **Enheter** > **Alla enheter** > välj enheten > **Enhetskonfiguration**. 

    Profilerna för varje enhet listas. Varje profil har en **Status**. Statusen gäller när alla tilldelade profiler, inklusive begränsningar och krav på maskinvara och operativsystem, bedöms tillsammans. Möjliga statusar:

    - **Överensstämmer**: Enheten har tagit emot profilen och rapporterar till Intune att den överensstämmer med inställningen.

    - **Ej tillämpligt**: Profilinställningen är inte tillämplig. E-postinställningar för iOS/iPadOS-enheter är t.ex. inte tillämpliga för Android-enheter.

    - **Väntar**: Profilen har skickats till enheten men har inte rapporterat statusen till Intune. Till exempel kräver kryptering på Android användaraktivering, vilket kan leda till att krypteringen väntar.

**Användbar länk**: [Övervaka enhetsprofiler för konfiguration](../configuration/device-profile-monitor.md)

> [!NOTE]
> Om två principer med olika begränsningsnivåer tillämpas på samma enhet eller användare, tillämpas den mer restriktiva principen.

## <a name="policy-troubleshooting-resources"></a>Felsökningsresurser för principer

- [Felsöka iOS/iPadOS- eller Android-principer som inte tillämpas på enheter](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-tip-Troubleshooting-iOS-or-Android-policies-not-applying/ba-p/280154) (öppnar en annan Microsoft-webbplats)
- [Felsöka Windows 10 Intune-principfel](https://blogs.technet.microsoft.com/configmgrdogs/2018/08/09/troubleshooting-windows-10-intune-policy-failures/) (öppnar en blogg)
- [Felsök anpassade CSP-inställningar för Windows 10](https://support.microsoft.com/en-us/help/4055338/troubleshoot-csp-setting-windows-10-computer-intune) (öppnar en annan Microsoft-webbplats)
- [Windows 10-grupprincipen jämfört med Intunes MDM-princip](https://blogs.technet.microsoft.com/cbernier/2018/04/02/windows-10-group-policy-vs-intune-mdm-policy-who-wins/) (öppnar en annan Microsoft-webbplats)

## <a name="alert-saving-of-access-rules-to-exchange-has-failed"></a>Avisering: Det gick inte att spara åtkomstregler i Exchange

**Problem**: Du får aviseringen **Det gick inte att spara åtkomstregler i Exchange** i administrationskonsolen.

Om du har skapat principer på arbetsytan Exchange On-premises-princip (administrationskonsolen) men använder Office 365, tillämpas inte de konfigurerade principinställningarna av Intune. Observera principkällan i aviseringen. Ta bort de gamla reglerna under arbetsytan Exchange On-premises-princip. De gamla reglerna är globala Exchange-regler i Intune för lokal Exchange och är inte relevanta för Office 365. Skapa sedan en ny princip för Office 365.

[Felsöka lokal Intune Exchange-anslutning](../protect/troubleshoot-exchange-connector.md) kan ge bra resultat.

## <a name="cant-change-security-policies-for-enrolled-devices"></a>Det går inte att säkerhetsprinciper för registrerade enheter

Windows Phone-enheter tillåter inte att säkerheten minskas för säkerhetsprinciper som har ställts in med hjälp av MDM eller EAS när de väl har ställts in. Som om du exempelvis ställer in **minsta antalet tecken för lösenord** till 8 och sedan försöker att minska det till 4. Den mer restriktiva principen tillämpas för enheten.

Windows 10-enheter kan inte ta bort säkerhetsprinciper när du tar bort principtilldelningen (stoppar distributionen). Du kan behöva lämna den tilldelade principen och sedan ändra tillbaka säkerhetsinställningarna till standardvärdena.

Du kan, beroende på enhetsplattform, vara tvungen att återställa säkerhetsprinciperna om du vill ändra principen till ett mindre säkert värde.

I Windows 8.1 sveper du till exempel från höger på skrivbordet för att öppna menyraden för **Snabbknappar**. Choose **Inställningar** > **Kontrollpanelen** > **Användarkonton**. Till vänster väljer du länken **Återställ säkerhetsprinciper** och sedan **Återställ principer**.

Andra plattformar, som Android, iOS/iPadOS och Windows Phone 8.1, kan behöva tas ur bruk och sedan registreras på nytt om en mindre begränsande profil ska kunna tillämpas.

[Felsöka enhetsregistrering](../enrollment/troubleshoot-device-enrollment-in-intune.md) kan vara en bra resurs.

## <a name="pcs-using-the-intune-software-client---classic-portal"></a>Datorer använder Intune-programklienten – klassisk portal

> [!NOTE]
> Det här avsnittet gäller för den klassiska portalen. 

### <a name="microsoft-intune-policy-related-errors-in-policyplatformlog"></a>Principrelaterade Microsoft Intune-fel i policyplatform.log

För Windows-datorer som hanteras med Intune-programklienten kan principfel i filen `policyplatform.log` bero på att andra inställningar än standardinställningarna används i Windows User Account Control (UAC) på enheten. Andra inställningar än UAC-standardinställningarna kan påverka Microsoft Intune-klientinstallationer och principkörning.

#### <a name="resolve-uac-issues"></a>Lösa problem med UAC

1. Ta datorn ur bruk. Se [Ta bort enheter](../remote-actions/devices-wipe.md).

2. Vänta 20 minuter tills klientprogrammet har tagits bort.

    > [!NOTE]
    > Försök inte att ta bort klienten från Program och funktioner.

3. Skriv **UAC** på startmenyn för att öppna inställningarna för User Account Control.

4. Dra meddelandereglaget till standardinställningen.

### <a name="error-cannot-obtain-the-value-from-the-computer-0x80041013"></a>FEL: Det går inte att hämta värdet från datorn, 0x80041013

Inträffar om tiden på det lokala systemet är felsynkroniserat med fem minuter eller mer. Om tiden på den lokala datorn inte är rätt synkroniserad misslyckas säkra transaktioner eftersom tidsstämplarna blir ogiltiga.

Du kan lösa problemet genom att ange den lokala systemtiden så nära Internettiden som möjligt. Eller ange samma tid som för domänkontrollanterna på nätverket.

## <a name="next-steps"></a>Nästa steg

[Vanliga problem och lösningar med e-postprofiler](../configuration/troubleshoot-email-profiles-in-microsoft-intune.md)

Få [support från Microsoft](../fundamentals/get-support.md) eller använd [community-forumen](https://social.technet.microsoft.com/Forums/en-US/home?category=microsoftintune).
