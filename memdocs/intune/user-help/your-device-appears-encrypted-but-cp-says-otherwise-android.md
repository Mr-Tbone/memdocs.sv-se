---
title: Det verkar som om din Android-enhet är krypterad | Microsoft Docs
description: Lösa krypteringsstatus i Företagsportal och Microsoft Intune-appen
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/14/2019
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ba593c08-1a78-4013-8525-b45a948772ec
searchScope:
- User help
ROBOTS: ''
ms.reviewer: arnab
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: a7ce95d5c28b1b85f27fdd0aee74e3148abfb554
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83882260"
---
# <a name="device-encrypted-but-apps-say-otherwise"></a>Enheten är krypterad men appar känner inte igen det

Om det står i Företagsportal eller Microsoft Intune-appen att enheten inte är krypterad, men du är säker på att den är det, kan du prova stegen i den här artikeln.  

## <a name="add-a-startup-pin"></a>Lägga till en start PIN-kod

På vissa Android-enheter måste du skapa en start-PIN-kod för att se till att enheten är skyddad. Den här inställningen finns i enhetens **Inställningar**-app. Namnet och platsen för inställningen kan variera. På till exempel Samsung Galaxy S7 kallas inställningen **Secure Startup** (Säker start). Om du vill aktivera det och skapa ett lösenord går du till **Settings** > **Lock Screen and Security** > **Secure Startup** (Inställningar, Låsskärm och säkerhet, Säker start).  

## <a name="encrypt-the-entire-device"></a>Kryptera hela enheten

Det här avsnittet gäller endast företagsportalappen. Med vissa enheter kan du välja mellan att kryptera hela enheten eller bara det använda utrymmet. Välj alternativet att kryptera hela enheten. Om du valde att bara kryptera det använda utrymmet:

1. [Ta bort den här enheten från företagsportalen](unenroll-your-device-from-intune-android.md).
2. Dekryptera använt utrymme.  
3. Kryptera hela enheten.  
4. Omregistrera enheten.  

## <a name="downgrade-your-version-of-android"></a>Nedgradera din version av Android

Det här avsnittet gäller endast företagsportalappen. Om enheten ger dig alternativet att nedgradera till Android 6.0 och senare gör du det. Det finns en risk för dataförlust om du nedgraderar din enhet. I annat fall rekommenderar vi att du kontaktar företagets support för att lösa problemet. Leta upp kontaktuppgifter till företagets support på [företagsportalwebbplatsen](https://go.microsoft.com/fwlink/?linkid=2010980).  

## <a name="specific-manufacturer-issues"></a>Problem med vissa tillverkare

På vissa Android-enheter med version 7.0 och senare krypteras data på ett sätt som strider mot vissa standarder för Android-plattformen. Dessa krypteringsmetoder utsätter enhetsinformation för risker. Därför stöds inte dessa enheter.

En ofullständig lista över Android-enheter som stöds finns i artikeln [Operativsystem och webbläsare som stöds i Intune](https://docs.microsoft.com/intune/fundamentals/supported-devices-browsers#supported-samsung-knox-standard-devices). Om din enhet inte finns med i listan hör du med enhetstillverkaren eller kontaktar en supporttekniker.

> [!Note]
> Microsoft arbetar med tillverkare för att åtgärda eventuella problem som vi påträffar under testning eller som användarna rapporterar till oss. Vi uppdaterar den här artikeln när ny information är tillgänglig.

## <a name="update-devices"></a>Uppdatera enheter

Om du inte har uppdaterat enheten till den senaste versionen av Android går du till enhetens **inställnings** app och väljer **Uppdatera**.  

## <a name="next-steps"></a>Nästa steg

Behöver du fortfarande hjälp? Kontakta företagets support (du hittar kontaktinformation på [företagsportalwebbplatsen](https://go.microsoft.com/fwlink/?linkid=2010980)) eller skriv till <a href="mailto:wintunedroidfbk@microsoft.com?subject=I'm having trouble with enrolling my Android device&body=Describe the issue you're experiencing here.">Microsoft Android-teamet</a>.  
