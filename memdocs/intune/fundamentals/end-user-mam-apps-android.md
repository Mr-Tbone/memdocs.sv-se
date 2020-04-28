---
title: Android-appar med appskyddsprinciper
description: Det här avsnittet beskriver vad som händer när din app hanteras av appskyddsprinciper.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 02/15/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 53c8e2ad-f627-425b-9adc-39ca69dbb460
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: b712b0365505ce4dab6162640cc8440799f2948b
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82079458"
---
# <a name="what-to-expect-when-your-android-app-is-managed-by-app-protection-policies"></a>Vad som händer när din Android-app hanteras av appskyddsprinciper

Den här artikeln beskriver användarupplevelsen för appar med appskyddsprinciper. Appskyddsprinciper tillämpas endast när appar används i arbetssammanhang: Till exempel när användaren har åtkomst till appar med ett arbetskonto eller har åtkomst till filer som lagras på en plats för OneDrive för företag.

## <a name="access-apps"></a>Åtkomstappar

Företagsportalappen krävs för alla appar som är kopplade till appskyddsprinciper på Android-enheter.

För enheter som inte har registrerats i Intune måste företagsportalappen installeras på enheten. Användaren behöver dock inte starta eller logga in i företagsportalappen innan de kan använda appar som hanteras av appskyddsprinciper.

Företagsportalappen är ett sätt för Intune att dela data på en säker plats. Därför är företagsportalappen ett krav för alla appar som är associerade med appskyddsprinciper, även om enheten inte har registrerats i Intune.

## <a name="use-apps-with-multi-identity-support"></a>Använda appar med stöd för flera identiteter

Appskyddsprinciper tillämpas bara i arbetssammanhang. Därför kan appen fungerar på olika sätt beroende på om sammanhanget är arbete eller personligt.

Användaren uppmanas till exempel att ange en PIN-kod för att kunna komma åt arbetsdata. För **Outlook-appen**, uppmanas användaren att ange en PIN-kod när hen startar appen. För **OneDrive-appen**, uppmanas användaren att ange PIN-koden när hen skriver i arbetskontot. För Microsoft **Word**, **PowerPoint** och **Excel**, uppmanas användaren att ange PIN-koden när hen har åtkomst till dokument som lagras i företagets OneDrive för företag.

## <a name="manage-user-accounts-on-the-device"></a>Hantera användarkonton på enheten

Med program med stöd för flera identiteter är det möjligt för användare att lägga till flera konton.  Intune APP har endast stöd för ett hanterat konto.  Intune APP begränsar inte antalet ohanterade konton.

När ett hanterat konto finns i ett program:

* Om en användare försöker lägga till ett andra hanterat konto uppmanas användaren att välja vilket av de hanterade kontona som ska användas.  Det andra kontot tas bort.
* Om IT-administratören lägger till en princip till ett andra befintligt konto uppmanas användaren att välja vilket av de hanterade kontona som ska användas.  Det andra kontot tas bort.

Läs följande exempel för att få en bättre förståelse för hur flera användarkonton behandlas.

Användare A arbetar för två företag – **Företag X** och **Företag Y**. Användare A har ett arbetskonto för varje företag och båda använder Intune för att distribuera appskyddsprinciper. **Företag X** distribuerar appskyddsprinciper **före** **Företag Y**. Det konto som är kopplat till **Företag X** får appskyddsprincipen, men inte kontot som är kopplat till Företag Y. Om du vill att användarkontot som är kopplat till Företag Y ska hanteras av appskyddsprinciperna måste du ta bort användarkontot som är kopplat till Företag X och lägga till kontot som är kopplat till Företag Y.

### <a name="add-a-second-account"></a>Lägg till ett andra konto

#### <a name="android"></a>Android

Om du använder en Android-enhet kan ett blockeringsmeddelande visas med instruktioner för att ta bort det befintliga kontot och lägga till ett nytt.  Om du vill ta bort det befintliga kontot går du till **Inställningar &gt;Allmänt &gt; Programhanterare &gt;Företagsportal.** Välj sedan **Rensa data**.

![Skärmbild av felmeddelande och anvisningar för att ta bort kontot](./media/end-user-mam-apps-android/Android_SwitchUser.png)

## <a name="view-media-files-with-the-azure-information-protection-app"></a>Visa mediefiler med Azure Information Protection-appen

Du kan visa företagets AV-, PDF- och bildfiler på Android-enheter i [Azure Information Protection-app](https://play.google.com/store/apps/details?id=com.microsoft.ipviewer) (tidigare kallad Rights Management Sharing-app).

Hämta den här appen från Google Play Store.  

Följande filtyper stöds:

* **Ljud:** AAC LC, HE-AACv1 (AAC+), HE-AACv2 (förbättrad AAC+), AAC ELD (Enhanced Low Delay AAC), AMR-NB, AMR-WB, FLAC, MP3, MIDI, Ogg Vorbis, PCM/WAVE
* **Video:** H.263, H.264 AVC, MPEG-4 SP, VP8
* **Bild:** .jpg, .pjpg, .png, .ppng, .bmp, .pbmp, .gif, .pgif, .jpeg, .pjpeg
* **Dokument:** PDF, PPDF

|**pfile**|
|----|
|Pfile är ett allmänt ”wrapper”-format för skyddade filer som kapslar in det krypterade innehållet och Azure Information Protection-licenserna. Det kan användas för att skydda alla filtyper.|

## <a name="next-steps"></a>Nästa steg
[Vad som händer när din iOS-/iPadOS-app hanteras av appskyddsprinciper](end-user-mam-apps-ios.md)
