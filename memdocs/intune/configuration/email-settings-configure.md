---
title: Konfigurera e-postinställningar i Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Skapa en e-postprofil i Microsoft Intune och distribuera profilen till Android-enhetsadministratör-, Android Enterprise-, iOS-, iPadOS- och Windows-enheter. Använd e-postprofiler för att konfigurera vanliga e-postinställningar, inklusive en e-postserver och autentiseringsmetoder för att ansluta till företagets e-post på enheter som du hanterar.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 07/20/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5bb01770909192b17f0e72b852e4094ff7ad3a04
ms.sourcegitcommit: d3992eda0b89bf239cea4ec699ed4711c1fb9e15
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/21/2020
ms.locfileid: "86565656"
---
# <a name="add-email-settings-to-devices-using-intune"></a>Lägg till e-postinställningar på enheter med Intune

Microsoft Intune innehåller olika e-postinställningar som du kan distribuera till enheter i din organisation. En IT-administratör skapar e-postprofiler med specifika inställningar för att ansluta till en e-postserver, till exempel Office 365 och Gmail. Slutanvändare kan sedan ansluta, autentisera och synkronisera sina e-postkonton för organisationen på sina mobila enheter. Genom att skapa och distribuera en e-postprofil kan du bekräfta att inställningarna är gemensamma för många enheter. Och minska antalet supportsamtal från slutanvändare som inte vet de rätta e-postinställningarna.

Du kan använda e-postprofiler för att konfigurera de inbyggda e-postinställningarna för följande enheter:

- Android-enhetsadministratör på Samsung Knox Standard 5.0 och senare
- Android enterprise
- iOS 11.0 och senare
- iPadOS 13.0 och senare
- Windows Phone 8.1 och senare
- Windows 10 Desktop och Windows 10 Mobile

Den här artikeln visar hur du skapar en e-postprofil i Microsoft Intune. Den innehåller också länkar till de olika plattformarna för mer specifika inställningar.

## <a name="create-the-profile"></a>Skapa profilen

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj **Enheter** > **Konfigurationsprofiler** > **Skapa profil**.
3. Ange följande egenskaper:

    - **Plattform**: Välj plattform för dina enheter. Alternativen är:  

        - **Android-enhetsadministratör**(endast Samsung Android Knox Standard)
        - **Android enterprise**
        - **iOS/iPadOS**
        - **Windows 10 och senare**
        - **Windows Phone 8.1**

    - **Profil**: Välj **E-post**.

4. Välj **Skapa**.
5. Ange följande egenskaper i **Grundinställningar**:

    - **Namn**: Ange ett beskrivande namn på principen. Namnge dina principer så att du enkelt kan identifiera dem senare. Exempel på ett bra principnamn: **Windows 10: E-postinställningar för alla Windows 10-enheter**.
    - **Beskrivning**: Ange en beskrivning av principen. Denna inställning är valfri, men rekommenderas.

6. Välj **Nästa**.

7. Under **Konfigurationsinställningar**  visas olika inställningar som du kan konfigurera beroende på vilken plattform du väljer. Välj din plattform för detaljerade inställningar:

    - [Android-enhetsadministratör (Samsung Knox Standard)](email-settings-android.md)
    - [Android enterprise](email-settings-android-enterprise.md)
    - [iOS/iPadOS](email-settings-ios.md)
    - [Windows 10](email-settings-windows-10.md)
    - [Windows Phone 8.1](email-settings-windows-phone-8-1.md)

8. Välj **Nästa**.
9. Under **Omfångstaggar** (valfritt), tilldelar du en tagg för att filtrera profilen till specifika IT-grupper, till exempel `US-NC IT Team` eller `JohnGlenn_ITDepartment`. Mer information om omfångstaggar finns i [Använda RBAC och omfångstaggar för distribuerad IT](../fundamentals/scope-tags.md).

    Välj **Nästa**.

10. Under **Tilldelningar** väljer du de användare eller enhetsgrupper som ska få profilen. Mer information om hur du tilldelar profiler finns [Vad du behöver veta](#what-you-need-to-know) (i den här artikeln). I [Tilldela användar- och enhetsprofiler](device-profile-assign.md) finns också information.

    Välj **Nästa**.

11. Granska inställningarna under **Granska + skapa**. När du väljer **Skapa** sparas dina ändringar och profilen tilldelas. Principen visas också i profillistan.

## <a name="what-you-need-to-know"></a>Vad du behöver veta

- E-postprofiler distribueras för den användare som har registrerat enheten. För att konfigurera e-postprofilen använder Intune egenskaperna Azure Active Directory (AD) i användarens e-postprofil under registreringen.

- Microsoft Outlook för iOS-/iPad- och Android-enheter stöder inte e-postprofiler. Distribuera i stället en konfigurationsprincip för appar. Mer information finns i [Konfigurationsinställning för Outlook](../apps/app-configuration-policies-outlook.md).

  På Android Enterprise-enheter distribuerar du Gmail eller Nine for Work med hjälp av Google Play Butik. [Lägg till hanterade Google Play-appar](../apps/apps-add-android-for-work.md) anger stegen.

- E-postmeddelandet baseras på identitets- och användarinställningar. E-postprofiler tilldelas vanligtvis till användargrupper och inte enhetsgrupper. Några saker att tänka på:

  - Om e-postprofilen innehåller användarcertifikat måste du tilldela e-postprofilen till användargrupper. Du kan ha flera användarcertifikatprofiler tilldelade. Flera profiler skapar en kedja av profildistributioner. Distribuera profilkedjan till användargrupper.

    Om en profil i den här kedjan distribueras till en enhetsgrupp kan användarna alltid uppmanas att ange sina lösenord.

  - Enhetsgrupper används vanligtvis när det inte finns någon primär användare eller om du inte vet vem användaren kommer att vara. E-postprofiler som är riktade till enhetsgrupper (inte användargrupper) kan inte levereras till enheten.

    Om din e-postprofil till exempel är riktad mot alla iOS/iPad-enhetsgrupper måste du se till att alla dessa enheter har en användare. Om en enhet inte har någon användare kan e-postprofilen inte distribueras. Sedan begränsar du profilen och kan missa vissa enheter. Om enheten har en primär användare bör det fungera att distribuera till enhetsgrupper.

    Mer information om möjliga problem med att använda enhetsgrupper finns [Common issues with email profiles](troubleshoot-email-profiles-in-microsoft-intune.md) (Vanliga problem med e-postprofiler).

## <a name="remove-an-email-profile"></a>Ta bort en e-postprofil

Du kan ta bort en e-postprofil från en enhet på olika sätt, även om det bara finns en e-postprofil på enheten:

- **Alternativ 1**: Öppna e-postprofilen (**Enheter** > **Konfigurationsprofiler** > välj din profil) och välj **Tilldelningar**. Fliken **Inkludera** visar de grupper som har tilldelats profilen. Högerklicka på gruppen > **Ta bort**. **Spara** dina ändringar.

- **Alternativ 2**: [Rensa eller dra tillbaka enheten](../remote-actions/devices-wipe.md). Du kan använda de här åtgärderna för att selektivt eller helt ta bort data och inställningar.

## <a name="secure-email-access"></a>Säkra åtkomst till e-post

Du kan skydda e-postprofiler med hjälp av följande alternativ:

- **Certifikat**: När du skapar en e-postprofil väljer du en certifikatprofil som tidigare skapats i Intune. Certifikatet kallas för identitetscertifikat. Det autentiserar mot en betrodd certifikatprofil eller ett rotcertifikat för att bekräfta att en användares enhet får ansluta. Det betrodda certifikatet tilldelas datorn som verifierar e-postanslutningen. Den här datorn är vanligtvis den interna e-postservern.

  Om du använder certifikatbaserad autentisering för din e-postprofil distribuerar du e-postprofilen, certifikatprofilen och profilen för betrodd rot till samma grupper. Den här distributionen gör att alla enheter kan identifiera certifikatutfärdarens legitimitet.

  Mer information om hur du skapar och använder certifikatprofiler i Intune finns i [Konfigurera certifikat i Intune](../protect/certificates-configure.md).

- **Användarnamn och lösenord**: Slutanvändaren autentiseras mot den interna e-postservern genom att ange ett användarnamn och lösenord. Lösenordet finns inte i e-postprofilen. Slutanvändaren måste därför ange lösenordet när hen ansluter till e-post.

## <a name="how-intune-handles-existing-email-accounts"></a>Hur Intune hanterar befintliga e-postkonton

Om användaren redan konfigurerat ett e-postkonto, tilldelas e-postprofilen på olika sätt, beroende på plattformen.

- **iOS/iPadOS**: En befintlig duplicerad e-postprofil identifieras utifrån värdnamn och e-postadress. E-postprofildubbletten blockerar tilldelningen av en Intune-profil. I det här fallet meddelar företagsportalen användaren om att denne inte uppfyller kraven och uppmanar slutanvändaren att ta bort den manuellt konfigurerade profilen. Om du vill förhindra det här sceneriet bör du be slutanvändarna registrera sig *innan* de installerar någon e-postprofil, så att Intune kan konfigurera profilen.

- **Windows:** En befintlig duplicerad e-postprofil identifieras utifrån värdnamn och e-postadress. Intune skriver över den befintliga e-postprofilen som skapats av slutanvändaren.

- **Android Samsung Knox Standard**: En befintlig duplicerad e-postprofil identifieras utifrån e-postadressen, och den skrivs över med Intune-profilen. Android använder inte värdnamn för att identifiera profilen. Skapa inte flera e-postprofiler på samma e-postadress på olika värdar. Profilerna skriver över varandra.

- **Android-arbetsprofiler**: Intune har två e-postprofiler för arbete för Android, en för Gmail-appen och en för Nine Work-appen. De här apparna är tillgängliga i Google Play Butik och installeras i enhetens arbetsprofil. De här apparna skapar inte dubblettprofiler. Båda apparna stöder anslutningar till Exchange. Om du vill använda e-postanslutningen, distribuerar du en av dessa e-postappar till användarnas enheter. Skapa och distribuera sedan e-postprofilen. Du kan använda e-postkonfigurationsprinciper för Gmail och Nine som fungerar för registreringstyperna arbetsprofil, dedikerad och företagsägd arbetsprofil. Detta innefattar användning av certifikatprofiler på båda e-postkonfigurationstyperna. Alla principer för Gmail eller Nine som du skapar i enhetskonfigurationen för arbetsprofiler fortsätter att gälla för enheten. Du behöver inte flytta dem till konfigurationsprinciper för appar. E-postappar som Nine Work kanske inte är kostnadsfria. Granska appens licensieringsinformation eller kontakta företaget som skapat appen om du har frågor.

## <a name="changes-to-assigned-email-profiles"></a>Ändringar av tilldelade e-postprofiler

Om du gör ändringar i en e-postprofil som du tidigare tilldelat, kan användarna få ett meddelande som ber dem godkänna omkonfigurationen av deras e-postinställningar.

## <a name="next-steps"></a>Nästa steg

När profilen har skapats gör den ingenting ännu. [Tilldela profilen](device-profile-assign.md) och [övervaka dess status](device-profile-monitor.md).
