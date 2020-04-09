---
title: Kryptera Android-enhet för Intune | Microsoft Docs
description: Steg för att aktivera Android-enhetskryptering när det krävs i Intune
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 03/31/2020
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: d4430e92-04cc-48e9-a77a-81b95a90b6b3
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: d9e074def368927504c3f3c1761ec21b3ab62d22
ms.sourcegitcommit: e17fc618d4c56c38a65c489b73ba27baa133ee7b
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/06/2020
ms.locfileid: "80696269"
---
# <a name="encrypting-your-android-device"></a>Kryptera din Android-enhet

Med enhetskryptering skyddas dina filer och mappar från obehörig åtkomst om enheten tappats bort eller stulits. Den medför att dina data på enheten varken blir tillgängliga för, eller kan läsas av, personer utan lösenord. 

Innan du kan komma åt skol- eller arbetsresurser kan din organisation kräva att du ska göra följande:

* [Kryptera din enhet](#encrypt-device)
* [Aktivera Säker Start](#enable-secure-startup)
* [Konfigurera ett lösenord för start, PIN-kod eller annan autentiseringsmetod](#set-startup-passcode)  

> [!Note]
> Vissa Android-enheter från Huawei, Vivo och OPPO kan inte krypteras. Mer information finns i [Enheten är krypterad men appar känner inte igen det](your-device-appears-encrypted-but-cp-says-otherwise-android.md).  

## <a name="encrypt-device"></a>Kryptera enheten

Följ de här stegen för att kryptera enheten. Enheten kan starta om flera gånger. 

Krypteringsalternativets namn och plats varierar beroende på enhetens tillverkare och Android-version. 

1. Öppna appen **Inställningar**.
2. Skriv **säkerhet** eller **kryptera** i appens sökfält för att hitta relaterade inställningar.
3. Tryck på alternativet för att kryptera enheten. Följ anvisningarna på skärmen.  
4. Konfigurera ett lösenord för låsning av skärmen, en PIN-kod eller en annan autentiseringsmetod (om så tillåts av din organisation) när du uppmanas till detta. 
5. Öppna företagsportals- eller Microsoft Intune-appen.
    * Användare av företagsportalen: Välj din enhet och tryck på **Kontrollera enhetsinställningar**. 
    * Microsoft Intune-användare: Du måste vänta tills sidan har uppdaterats, men då ska krypteringsstatusen ändras till kompatibel. 

## <a name="enable-secure-startup"></a>Aktivera Säker Start

Din organisation kan kräva att du aktiverar Säker start som en del av sin krypteringspolicy. Den här funktionen skyddar din enhet ytterligare genom att kräva att ett lösenord eller en PIN-kod anges innan telefonen startas. Du kan erbjudas ytterligare autentiseringsalternativ, men det varierar beroende på vad din organisation tillåter. 

Säker Start-alternativets namn och plats varierar beroende på enhetens tillverkare och Android-version. På vissa enheter kan den här inställningen kallas **Starkt skydd**. 

1. Öppna appen **Inställningar**.
2. Skriv **Säker start** i appens sökfält.
3. Välj **Säker start** > **Kräv PIN-kod när enheten slås på**.
4. Ange PIN-koden för enheten när du uppmanas till det.   
5. Öppna företagsportals- eller Microsoft Intune-appen.
    * Användare av företagsportalen: Välj din enhet och tryck på **Kontrollera enhetsinställningar**. 
    * Microsoft Intune-användare: Du måste vänta tills sidan har uppdaterats, men då ska krypteringsstatusen ändras till kompatibel.  


## <a name="set-startup-passcode"></a>Konfigurera lösenord för start   
När du [krypterar enheten](#encrypt-device) och [aktiverar Säker start](#enable-secure-startup), blir du uppmanad att konfigurera en PIN-kod för enheten, lösenord eller annan autentiseringsmetod (om så tillåts av din organisation). Inga ytterligare steg krävs. 

För att välja eller ändra låsskärmstyp:

1. Öppna appen **Inställningar**.
2. Skriv **skärmlås** i appens sökfält.
3. Tryck på **Skärmlåstyp**.
4. Tryck på den skärmlåstyp som du vill använda och bekräfta genom att följa anvisningarna på skärmen.  

## <a name="troubleshoot"></a>Felsöka    
**Problem**: Krypteringsknappen är inaktiverad.   

**Försök följande**: 
* Kontrollera att enheten är fulladdad och inkopplad. Krypteringen kan ta en stund och kräver ett fullt batteri.   

**Problem**: Du ser ett meddelande om att du fortfarande behöver kryptera enheten.  

**Saker du kan prova**:
   *  [Konfigurera en låsskärm](#set-startup-passcode) på enheten. 
   * [Aktivera Säker Start](#enable-secure-startup).

Behöver du fortfarande hjälp? Kontakta företagets support (du hittar kontaktinformation på [företagsportalwebbplatsen](https://go.microsoft.com/fwlink/?linkid=2010980)) eller skriv till <a href="mailto:wintunedroidfbk@microsoft.com?subject=I'm having trouble with encryption on my Android device&body=Describe the issue you're experiencing here.">Microsoft Android-teamet</a>.  
