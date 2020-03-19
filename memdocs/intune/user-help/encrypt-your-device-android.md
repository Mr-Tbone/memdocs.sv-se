---
title: Kryptera Android-enhet för Intune | Microsoft Docs
description: Steg för att aktivera Android-enhetskryptering när det krävs i Intune
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/19/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: d4430e92-04cc-48e9-a77a-81b95a90b6b3
searchScope:
- User help
ROBOTS: ''
ms.reviewer: arnab
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: ee2d220e308b406251f049e1c17422f89ee36534
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79348789"
---
# <a name="encrypting-your-android-device"></a>Kryptera din Android-enhet

Med enhetskryptering skyddas dina filer och mappar från obehörig åtkomst om enheten tappats bort eller stulits. När du har aktiverat enhetskryptering kan endast personer med rätt lösenord eller PIN-kod logga in på enheten. 

Innan du kan komma åt skol- eller arbetsresurser kan din organisation kräva att du krypterar Android-enheten. Vissa nyare Android-enheter är krypterade som standard.  

## <a name="turn-on-encryption"></a>Aktivera kryptering

Om du ombes kryptera enheten i appen Företagsportal eller Microsoft Intune slutför du följande steg. 

> [!Note]
> Vissa Android-enheter från Huawei, Vivo och OPPO kan inte krypteras. Läs mer [här](your-device-appears-encrypted-but-cp-says-otherwise-android.md).  

1. Ange ett skärmlås för enheten.  
    a. Gå till **Inställningar** > **Låsskärm och säkerhet** > **Skärmlåstyp**.  
    b. Välj antingen **PIN-kod**, **Lösenord** eller **Mönster**.  
    c. Konfigurera skärmlåset genom att följa anvisningarna på skärmen.  

2. Gå tillbaka till **Låsskärm och säkerhet** och välj **Säker start**.
3. Välj **Kräv PIN-kod när enheten slås på** > **OK**.
4. Ange din PIN-kod för att bekräfta och kryptera enheten.
5. Öppna appen Företagsportal eller Microsoft Intune.
    * Användare av företagsportalen: Välj din enhet och tryck på **Kontrollera enhetsinställningar**. 
    * Microsoft Intune-användare: Du måste vänta tills sidan har uppdaterats, men då ska krypteringsstatusen ändras till kompatibel.  

På enheter som kör Android 4.4 och tidigare kanske inte alternativet **Säker start** finns. I så fall kan du slutföra följande steg för att kryptera enheten.

1. Gå till **Inställningar** > **Säkerhet** > **Kryptera enhet**. Texten som visas på skärmen varierar mellan Android-enheter. Om du inte ser alternativet **Kryptera enhet** kan du kontrollera:
    * **Lagring** > **Lagringskryptering**
    * **Lagring** > **Låsskärm och säkerhet** > **Andra säkerhetsinställningar** 

2. Följ anvisningarna på skärmen. Enheten kan starta om flera gånger under krypteringen.
3. Öppna appen Företagsportal eller Microsoft Intune.
    * Användare av företagsportalen: Välj din enhet och tryck på **Kontrollera enhetsinställningar**.  
    * Microsoft Intune-användare: Du måste vänta tills sidan har uppdaterats, men då ska krypteringsstatusen ändras till kompatibel.

## <a name="troubleshoot"></a>Felsöka  
**Problem**: Du har redan krypterat enheten.

- Krypteringsknappen är inaktiverad.
- Du ser ett meddelande om att du fortfarande behöver kryptera enheten.
- Fel uppstår när du försöker använda appen Företagsportal eller Microsoft Intune.

**Saker du kan prova**

- Kontrollera att enheten är laddad och inkopplad.  
- Kontrollera att du har ställt in en PIN-kod eller ett lösenord på enheten.  

Behöver du fortfarande hjälp? Kontakta företagets support (du hittar kontaktinformation på [företagsportalwebbplatsen](https://go.microsoft.com/fwlink/?linkid=2010980)) eller skriv till <a href="mailto:wintunedroidfbk@microsoft.com?subject=I'm having trouble with encryption on my Android device&body=Describe the issue you're experiencing here.">Microsoft Android-teamet</a>.  
