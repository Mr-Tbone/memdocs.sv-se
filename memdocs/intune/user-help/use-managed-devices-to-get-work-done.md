---
title: Vad är enhetsregistrering? | Microsoft Docs
description: Förstå vad det innebär att registrera din enhet i appen Företagsportal och Microsoft Intune.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 09/13/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 523caa6b-d792-4bb6-bddb-24b2479932d8
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 95f9677b95dc9dde4b12e60e3006b4cee5081471
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "80233421"
---
# <a name="what-is-device-enrollment"></a>Vad är enhetsregistrering?
Om du vill få åtkomst till arbets- eller skolresurser från din enhet måste du registrera din enhet med appen Intune Företagsportal eller appen Microsoft Intune. 

Under enhetsregistrering:

* Din enhet registreras hos din organisation. Det här steget garanterar att du har behörighet att komma åt din organisations e-post, appar och Wi-Fi. 
* Organisationens principer för enhetshantering tillämpas på din enhet. Principer kan innehålla krav på saker såsom enhetslösenord och -kryptering. Syftet med dessa krav är att hålla enheten och din organisations data säkra från obehörig åtkomst.

När du har uppdaterat enhetsinställningarna så att de uppfyller organisationens krav har registreringen slutförts. Du kan på ett säkert sätt logga in på ditt arbets- eller skolkonto i stort sett var som helst.  

I den här artikeln beskrivs andra aspekter av registreringen, till exempel hur du hämtar apparna, vilka enheter som stöds och hur du tar bort eller återställer enheten.  

## <a name="company-portal-and-microsoft-intune-app"></a>Appen Företagsportal and Microsoft Intune

Apparna Företagsportal och Microsoft Intune uppmärksammar dig på ändringar av principer eller inställningar, så att du kan vidta åtgärder utan att förlora åtkomsten till arbete eller skola. 

Med appen Företagsportal hålls din personliga och arbetsrelaterade information åtskild, så att du kan vara produktiv och fokuserad. Den gör även arbets- och skolappar tillgängliga för dig, så att du kan hitta och installera sådana som är relevanta för ditt arbete.  

### <a name="get-company-portal"></a>Skaffa företagsportalappen

I vissa fall kommer din organisation att installera appen Företagsportal på din enhet åt dig. Appen är även tillgänglig för installation från appbutiker som Microsoft Store, App Store och Google Play Butik. Logga in på [webbplatsen Företagsportal](https://go.microsoft.com/fwlink/?linkid=2010980) med ditt arbets- eller skolkonto om du vill komma åt appen från en webbläsare.  

### <a name="get-microsoft-intune-app"></a>Skaffa Microsoft Intune-appen

Om du måste använda appen Microsoft Intune kommer din organisation att installera den på din enhet åt dig.  

## <a name="whats-the-difference-between-the-apps-and-the-website"></a>Vad är skillnaden mellan apparna och webbplatsen?
Appen Företagsportal är tillgänglig för Windows 10-, iOS-, macOS- och Android-enheter. Den integreras smidigt med respektive enhets plattform. Webbplatsversionen är tillgänglig på valfri enhet och du får samma, universella miljö oavsett vilken enhet du använder. 

Appen Microsoft Intune är avsedd för företagsägda Android-enheter och har inte någon webbplats.  

## <a name="what-kind-of-devices-can-you-enroll-with-company-portal"></a>Vilken typ av enheter kan du registrera med Företagsportal?
Du kan registrera följande enheter med Företagsportal:  

- Windows-enheter
  - Windows 10 Mobil
  - Windows 10 Desktop
  - Windows Phone 8.1
  - Windows 8.1
- Apple-enheter
    - iOS
    - macOS
- Android-enheter:


## <a name="what-kind-of-devices-can-you-enroll-with-the-microsoft-intune-app"></a>Vilken typ av enheter kan du registrera med appen Microsoft Intune?  
Du kan registrera företagsägda Android-enheter som din organisation har konfigurerat för användning med appen. Appen stöder för närvarande Android 6.0 och senare. 

## <a name="can-you-remove-a-device-from-the-company-portal"></a>Går det att ta bort en enhet från företagsportalappen?
Du kan ta bort eller återställa en enhet från Företagsportal. Det är skillnad mellan att **ta bort** och att **återställa**.

När enheten tas bort avregistreras enheten i Företagsportal. Enheten förlorar åtkomst till Företagsportal. Arbets- eller skoldata kan också tas bort. 

Under en enhetsåterställning försöker företagsportalappen återställa datorn eller enheten till tillverkarens standardinställningar. Alla arbets- eller skoldata och alla personliga data tas bort från enheten. En återställning är användbar om du till exempel tappar bort enheten. Du kan fjärråterställa den från webbplatsen Företagsportal.  

## <a name="can-you-remove-a-device-from-the-microsoft-intune-app"></a>Går det att ta bort en enhet från appen Microsoft Intune?
Nej, du kan inte ta bort en företagsägd enhet från appen Microsoft Intune.  

## <a name="what-if-i-cant-see-my-device-in-the-company-portal-or-microsoft-intune-app"></a>Vad händer om jag kan inte se min enhet i appen Företagsportal eller Microsoft Intune?
Om du vill se en enhet i Företagsportal måste den först registreras. Om du efter registreringen fortfarande inte ser alla dina enheter kan du prova att synkronisera eller kontrollera åtkomst via Företagsportal. Enheter som ägs och hanteras av ditt företag visas inte.

I appen Microsoft Intune ser du bara den enhet som du använder just nu. Andra registrerade enheter visas inte i appen.  

## <a name="where-else-can-i-go-for-help"></a>Var finns ytterligare hjälp?  
Information om hur du felsöker vanliga problem finns i de här plattformsspecifika dokumenten:  

- [Åtgärda vanliga problem med din Android-enhet](check-compliance-on-your-device-android.md)  
- [Åtgärda vanliga problem med din iOS-enhet](troubleshoot-your-device-ios.md)
- [Åtgärda vanliga problem med din macOS-enhet](troubleshoot-your-device-macos.md)
- [Åtgärda vanliga problem med din Windows-enhet](troubleshoot-your-device-windows.md)

Du kan även kontakta din IT-support. Appen Företagsportal och Microsoft Intune erbjuder hjälp- och supportsidor med kontaktinformation och metoder för att anmäla problem. Kontaktinformation är även tillgänglig på [webbplatsen Företagsportal](https://go.microsoft.com/fwlink/?linkid=2010980) för din organisation.  

## <a name="next-steps"></a>Nästa steg  

Om du är redo att komma åt ditt arbets- eller skolkonto följer du organisationens instruktioner för att registrera din enhet. Du kan även hitta stegvis vägledning för registrering i följande artiklar.

* [Registrera din Windows 10-enhet](enroll-windows-10-device.md)
* [Registrera Android-enheten](enroll-device-android-company-portal.md)
* [Registrera med Android-arbetsprofilen](enroll-device-android-work-profile.md)
* [Registrera med Microsoft Intune-appen](enroll-device-android-microsoft-intune-app.md)
* [Registrera din iOS-enhet](enroll-your-device-in-intune-ios.md)
* [Registrera din iOS-enhet som tillhandahålls av organisationen](enroll-your-device-dep-ios.md)
* [Registrera din macOS-enhet](enroll-your-device-in-intune-macos-cp.md)
* [Registrera din macOS-enhet som tillhandahålls av organisationen](enroll-company-device-macos.md)
