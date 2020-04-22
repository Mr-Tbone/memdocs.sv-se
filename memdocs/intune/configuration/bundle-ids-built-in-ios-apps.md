---
title: Samlings-ID:n för iOS/iPadOS för inbyggda appar i Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Visa en lista över samlings-ID:n för inbyggda iOS och iPadOS-appar. Med dessa samlings-ID:n kan du explicit tillåta appar i profiler och principer för enhetskonfiguration i Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: ''
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c7de0b978c24f28988c62854a249505a0598db95
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "80084086"
---
# <a name="bundle-ids-for-built-in-ios-and-ipados-apps-you-can-use-in-intune"></a>Samlings-ID:n för inbyggda iOS- och iPadOS-appar som du kan använda i Intune

När du konfigurerar funktioner i iOS/iPadOS-enheter kan du också lägga till de inbyggda apparna i iOS/iPadOS-enheter. I den här artikeln visas samlings-ID:n för några vanliga inbyggda iOS/iPadOS-appar. Kontakta programvaruleverantören för att hitta appsamlings-ID:n för andra appar. Se Apples lista över [iOS/iPadOS-paket-ID:n](https://support.apple.com/guide/mdm/ios-bundle-ids-mdm90f60c1ce/web) (öppnar Apples webbplats).

## <a name="bundle-ids"></a>Samlings-ID:n

| Samlings-ID                   | Appnamn     | Publisher |
|-----------------------------|--------------|-----------|
| com.apple.AppStore          | Appbutik    | Apple     |
| com.apple.store.Jolly       | Apple Store  | Apple     |
| com.apple.calculator        | Kalkylator   | Apple     |
| com.apple.mobilecal         | Kalender     | Apple     |
| com.apple.camera            | Kamera       | Apple     |
| com.apple.mobiletimer       | Klocka        | Apple     |
| com.apple.clips             | Klipp        | Apple     |
| com.apple.compass           | Kompass      | Apple     |
| com.apple.MobileAddressBook | Kontakter     | Apple     |
| com.apple.facetime          | FaceTime     | Apple     |
| com.apple.DocumentsApp      | Filer        | Apple     |
| com.apple.mobileme.fmf1     | Hitta vänner | Apple     |
| com.apple.mobileme.fmip1    | Hitta iPhone  | Apple     |
| com.apple.gamecenter        | Spelcenter  | Apple     |
| com.apple.mobilegarageband  | GarageBand   | Apple     |
| com.apple.Health            | Hälsa       | Apple     |
| com.apple.Home              | Hem         | Apple     |
| com.apple.iBooks            | iBooks       | Apple     |
| com.apple.iMovie            | iMovie       | Apple     |
| com.apple.itunesconnect.mobile | iTunes Connect | Apple |
| com.apple.MobileStore       | iTunes Store | Apple     |
| com.apple.itunesu           | iTunes U     | Apple     |
| com.apple.Keynote           | Keynote      | Apple     |
| com.apple.mobilemail        | E-post         | Apple     |
| com.apple.Maps              | Kartor         | Apple     |
| com.apple.measure           | Åtgärd      | Apple     |
| com.apple.MobileSMS         | Meddelanden     | Apple     |
| com.apple.Music             | Musik        | Apple     |
| com.apple.news              | Nyheter         | Apple     |
| com.apple.mobilenotes       | Obs!        | Apple     |
| com.apple.Numbers           | Siffror      | Apple     |
| com.apple.Pages             | Sidor        | Apple     |
| com.apple.mobilephone       | Telefon        | Apple     |
| com.apple.Photo-Booth       | Photo Booth  | Apple     |
| com.apple.mobileslideshow   | Foton       | Apple     |
| com.apple.podcasts          | Poddsändningar     | Apple     |
| com.apple.reminders         | Påminnelser    | Apple     |
| com.apple.mobilesafari      | Safari       | Apple     |
| com.apple.Preferences       | Inställningar     | Apple     |
| com.apple.shortcuts         | Genvägar    | Apple     |
| com.apple.SiriViewService   | Siri         | Apple     |
| com.apple.stocks            | Aktier       | Apple     |
| com.apple.tips              | Tips         | Apple     |
| com.apple.tv                | TV           | Apple     |
| com.apple.videos            | Videor       | Apple     |
| com.apple.VoiceMemos        | VoiceMemos   | Apple     |
| com.apple.Passbook          | Plånbok       | Apple     |
| com.apple.Bridge            | Titta på        | Apple     |
| com.apple.weather           | Väder      | Apple     |

## <a name="next-steps"></a>Nästa steg

Med dessa bunt-ID:n kan du konfigurera [enhetsfunktioner](ios-device-features-settings.md) och [tillåta eller begränsa vissa inställningar](device-restrictions-ios.md) på iOS/iPadOS-enheter.
