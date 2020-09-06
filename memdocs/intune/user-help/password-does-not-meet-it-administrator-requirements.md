---
title: Lösenordskrav för Intune-registrerade enheter | Microsoft Docs
description: Den här artikeln beskriver hur du uppfyller lösenordskraven för din organisation så att du kan komma åt nätverket.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/27/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: efb3c261-1f6c-4d39-bfa4-18661f8c59c7
searchScope:
- User help
ROBOTS: ''
ms.custom: intune-enduser, contperfq1
ms.collection: ''
ms.openlocfilehash: b9bdada31e280c7fdc8a5d7a5a0a4a7ab7d36ae3
ms.sourcegitcommit: 41e6e6b7f5c2a87aaf7f23d90d0f175dd63c0579
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/28/2020
ms.locfileid: "89057295"
---
# <a name="device-password-requirements"></a>Krav på enhetslösenord  

Du får ett meddelande från Företagsportal om ditt enhetslösenord inte uppfyller organisationens säkerhetskrav. Lösenordskraven finns för att skydda dig och organisationens data från obehörig åtkomst. Innan du skapar ett säkrare lösenord kan du hindras från att komma åt organisationens nätverk.  

Företagsportal skickar ett meddelande per lösenordskrav, så du kan få fler än ett meddelande på samma gång. Tryck på ett meddelande om du vill visa mer information (om det finns).  

Den här artikeln innehåller alla lösenordsrelaterade meddelanden som du kan få och ger ytterligare information om varje krav, per OS-plattform.     

## <a name="change-password-passcode-pin"></a>Ändra lösenord och PIN-kod  

För att komma åt lösenordsinställningarna kan du i allmänhet öppna appen Inställningar på enheten och söka efter *Låsskärm* eller *Säkerhetsinställningar*.  

I följande artiklar beskrivs hur du uppdaterar enhetslösenordet, per OS-plattform. De senaste anvisningarna för din specifika enhet finns i hjälpdokumentationen från enhetstillverkaren.  

- [Ange lösenord för Windows 10-enhet](set-or-change-your-password-windows.md)  
- [Konfigurera lösenord för iOS-enhet](set-or-change-your-passcode-ios.md)  
- [Ställ in en PIN-kod eller ett lösenord för en Android-enhet](set-your-pin-or-password-android.md)  


> [!IMPORTANT]
> Om du har ändrat ditt lösenord för att uppfylla kraven, men fortfarande får meddelanden, startar du om enheten.  

Kontakta din IT-support om du har specifika frågor om organisationens lösenordskrav.  

## <a name="windows-10-password-requirements"></a>Lösenordskrav för Windows 10

| Meddelande | Så här löser du |
|-----------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Lösenord måste anges. | Ställ in ett lösenord. Din organisation kräver att du anger ett lösenord för att låsa upp enheten. |
| Lösenordet är för enkelt. |  Kontrollera att lösenordet inte innehåller sekventiella eller upprepade siffror, till exempel 1234 eller 1111. |
| Lösenordet är för kort.| Uppdatera eller ställ in ett lösenord med fler tecken. Din organisation kräver att ditt lösenord är en viss längd. Vad de faktiskt väljer varierar, men den minsta längden som de kan kräva är 4 tecken och det högsta värdet är 16. |
| Lösenordet får endast innehålla siffror. | Ange ett lösenord som endast innehåller siffror.|
| Lösenord får bara innehålla alfanumeriska tecken. | Ange ett lösenord som innehåller en blandning av siffror och bokstäver.|
| Lösenordet måste innehålla komplexa tecken. | Lägg till komplexa tecken som siffror, versaler och symboler som `$`, `%` och `#`. Din organisation kräver en blandning av bokstäver, siffror och icke-alfanumeriska tecken för att det ska bli svårare för andra att gissa lösenordet.|  
| Lösenordet har upphört att gälla. | Ange ett nytt lösenord. Din organisation kräver att du ändrar ditt lösenord efter ett visst antal dagar. |
| Lösenordet har använts nyligen. | Välj ett lösenord som du inte har använt tidigare. Din organisation kräver att en viss tidsperiod passerar innan du återanvänder ett lösenord. |

## <a name="ios-passcode-requirements"></a>Krav för iOS-lösenord

| Meddelande | Så här löser du |
|-----------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Lösenord krävs.| Ställ in ett lösenord. Din organisation kräver att du anger ett lösenord för att låsa upp enheten. |
| Lösenordet är för enkelt. |  Kontrollera att lösenordet inte innehåller sekventiella eller upprepade siffror, till exempel 1234 eller 1111. |
| Lösenordet är för kort. | Uppdatera eller ställ in ett lösenord med fler tecken. Din organisation kräver att ditt lösenord är en viss längd. Vad de faktiskt väljer varierar, men den minsta längden som de kan kräva är 4 tecken och det högsta värdet är 14. När du ändrar ditt lösenord kan du få en uppmaning från Apple som säger att du kan ange 6 eller fler tecken. Det här meddelandet är bara en systemrekommendation för Apple. Om din organisation bara kräver ett lösenord som är 4 eller 5 tecken behöver du inte ange ett lösenord med 6 siffror.|  
| Lösenordet får endast innehålla siffror. | Ange ett lösenord som endast innehåller siffror.|
| Lösenord får bara innehålla alfanumeriska tecken.| Ange ett lösenord som innehåller en blandning av siffror och bokstäver.|
| Lösenord får bara innehålla icke-alfanumeriska tecken. | Lägg till specialtecken som `&`, `!`, `$`, `%`och `#`. Din organisation kräver en blandning av bokstäver, siffror och icke-alfanumeriska tecken för att det ska bli svårare för andra att gissa lösenordet.|
| Lösenkoden har gått ut. | Ange ett nytt lösenord. Din organisation kräver att du ändrar ditt lösenord efter ett visst antal dagar. |
| Lösenordet har använts för nyligen.| Välj ett lösenord som du inte har använt tidigare. Din organisation kräver att en viss tidsperiod passerar innan du återanvänder ett lösenord. |
|Autentisering av Touch-ID eller ansikts-ID krävs. | Ställ in Touch-ID eller ansikts-ID. Din organisation kräver att du autentiserar med någon av dessa metoder innan du använder automatisk ifyllning för lösenord eller kreditkortsinformation. | 

## <a name="macos-password-requirements"></a>Lösenordskrav för macOS
| Meddelande | Så här löser du |
|-----------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Lösenord måste anges. | Ställ in ett lösenord. Din organisation kräver att du anger ett lösenord för att låsa upp enheten. |
| Lösenordet är för enkelt.|  Kontrollera att lösenordet inte innehåller sekventiella eller upprepade siffror, till exempel 1234 eller 1111. |
| Lösenordet är för kort. | Uppdatera eller ställ in ett lösenord med fler tecken. Din organisation kräver att ditt lösenord är en viss längd.|
| Lösenordet får endast innehålla siffror. | Ange ett lösenord som endast innehåller siffror.|
| Lösenord får bara innehålla alfanumeriska tecken. | Ange ett lösenord som innehåller en blandning av siffror och bokstäver.|
| Lösenord måste innehålla icke-alfanumeriska tecken. | Lägg till specialtecken som `&`, `!`, `$`, `%`och `#`. Din organisation kräver en blandning av bokstäver, siffror och icke-alfanumeriska tecken för att det ska bli svårare för andra att gissa lösenordet.|
| Lösenordet har upphört att gälla. | Ange ett nytt lösenord. Din organisation kräver att du ändrar ditt lösenord efter ett visst antal dagar. |
| Lösenordet har använts nyligen. | Välj ett lösenord som du inte har använt tidigare. Din organisation kräver att en viss tidsperiod passerar innan du återanvänder ett lösenord. |

## <a name="android-password-requirements"></a>Lösenordskrav för Android
| Meddelande | Så här löser du |
|-----------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Lösenord måste anges. | Ställ in ett lösenord eller en PIN-kod. Din organisation kräver att du anger ett lösenord för att låsa upp enheten. |
| Lösenordet är för enkelt. |  Kontrollera att lösenordet eller PIN-koden inte innehåller sekventiella eller upprepade siffror, till exempel 1234 eller 1111. |
| Lösenordet är för kort. | Uppdatera eller ställ in ett lösenord med fler tecken. Din organisation kräver att ditt lösenord är en viss längd.|
| Lösenordet måste innehålla siffror. | Ange ett lösenord eller en PIN-kod som innehåller siffror.|
| Lösenordet måste innehålla bokstäver. | Ange ett lösenord som innehåller bokstäver från alfabetet.|
| Lösenord måste innehålla alfanumeriska tecken. | Ange ett lösenord som innehåller en blandning av siffror och bokstäver.|
| Lösenord måste innehålla alfanumeriska tecken och symboler. | Ange ett lösenord som innehåller en blandning av bokstäver, siffror och specialtecken, till exempel `&`, `!`, `$`, `%` och `#`. |
| Lösenordet måste använda biometrisk teknik.| Konfigurera enheten för att använda biometrisk autentisering, t. ex. fingeravtryck eller ansiktsigenkänning.
| Lösenordet har upphört att gälla. | Ange ett nytt lösenord. Din organisation kräver att du ändrar ditt lösenord efter ett visst antal dagar. |
| Lösenordet har använts nyligen. | Välj ett lösenord som du inte har använt tidigare. Din organisation kräver att en viss tidsperiod passerar innan du återanvänder ett lösenord. |

## <a name="next-steps"></a>Nästa steg
Om du efter att ha uppdaterat ditt lösenord fortfarande får lösenordsrelaterade meddelanden kan du prova att starta om enheten. 

Behöver du fortfarande hjälp? Kontakta IT-supporten. Titta efter IT-administratörens kontaktuppgifter på [företagsportalens webbplats](https://go.microsoft.com/fwlink/?linkid=2010980).  


