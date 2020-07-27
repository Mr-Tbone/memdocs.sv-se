---
title: Lagra en återställningsnyckel i Intune via Företagsportal-webbplatsen
description: Ladda upp och lagra återställningsnyckeln för din enhet via Företagsportal-webbplatsen.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/17/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: annochiva
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 826515026e578cb993bb706fc61dedb4a80fb3e6
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/18/2020
ms.locfileid: "86465044"
---
# <a name="store-your-personal-filevault-key"></a>Lagra din personliga FileVault-nyckel 

Lagra en FileVault-nyckel för din personliga krypterade macOS-enhet. Förutom att uppfylla krypteringskraven kan du göra följande när du lagrar din nyckel i Intune: 

* Snabbt och enkelt hämta eller rotera nyckeln från valfri enhet. 
* Be din supportkontakt om hjälp om du behöver hämta eller rotera nyckeln och inte kan komma åt appar eller webbplatser för att göra det själv.


## <a name="retrieve-or-rotate-the-key"></a>Hämta eller rotera nyckeln

Om du blir utelåst från enheten kan du hämta nyckeln från följande platser:
   
- Företagsportalens webbplats
- Appen Företagsportal i iOS/iPadOS 
- Apen Företagsportal i Android
- Intune-appen
 
 IT-personal med administratörsbehörighet till Intune kan rotera din personliga återställningsnyckel åt dig om du blir utelåst från enheten. De kan också visa nycklar, men bara de som tillhör företagsägda enheter. IT-personalen kan inte visa återställningsnycklar som tillhör personliga enheter.   


## <a name="do-i-need-to-store-my-key"></a>Måste jag lagra min nyckel?  
IT-personalen meddelar dig om du är tvungen att ladda upp en personlig återställningsnyckel. Du kan få ett meddelande från appen Företagsportal för iOS/iPad eller Android om det är så organisationens IT-avdelning vanligtvis kommunicerar med dig. 

Vi rekommenderar att du bara laddar upp en återställningsnyckel om du tillhör någon av följande kategorier:
* Du krypterade din enhet innan du registrerade den i organisationen. 
* Du krypterade enheten manuellt via systeminställningarna i macOS.   

Beroende på organisationens policy kan du blockeras från företagets resurser på enheten tills du har laddat upp nyckeln.  

## <a name="upload-personal-recovery-key"></a>Ladda upp personlig återställningsnyckel 
Utför de här stegen för att spara den personliga FileVault-nyckeln för din krypterade Mac-enhet.  


1. Öppna [Företagsportal-webbplatsen](https://portal.manage.microsoft.com) och logga in med ditt arbets- eller skolkonto. 
2. Välj den krypterade enheten.
3. Välj **Lagra återställningsnyckel**.  
4. Ange en alfanumerisk FileVault-nyckel med 24 tecken.  
5. Ange nyckeln igen. Välj sedan **Spara**.
6. Företagsportal försöker verifiera, rotera och spara din personliga återställningsnyckel. Du behöver inte göra något mer förrän nyckeln har sparats. Om du lämnar webbplatsen innan uppladdningen är klar kan du visa statusen på sidan med enhetsinformation nästa gång du loggar in.  

Mer information om de meddelanden du kan se under processen finns i [Meddelanden i Företagsportal](store-recovery-key.md#company-portal-messages).  

## <a name="company-portal-messages"></a>Meddelanden i företagsportalen

|Meddelande  |Betydelse  |
|---------|---------|
|Nycklarna måste överensstämma. Kontrollera nycklarna och försök igen.     | Visas under **Bekräfta återställningsnyckel** så att du ser om nycklarna inte matchar. Skriv nycklarna i båda fälten på nytt och försök sedan spara igen.        |
|Det gick inte att uppdatera enhetens återställningsnyckel| Visas som popup-meddelande längst upp på skärmen så att du ser om Företagsportal inte lyckas lagra en återställningsnyckel åt dig. Välj den krypterade enheten om du vill se mer information. Läs sedan meddelandet längst upp på sidan för att se hur du kan gå vidare. |
|Det gick inte att ladda upp återställningsnyckeln. Kontrollera att du har angett rätt nyckel och försök igen. Om problemet kvarstår kan du försöka rotera nyckeln manuellt. Tryck för att läsa mer.     | Visas på enhetens informationssida och kan betyda några olika saker: Företagsportal kanske inte kunde rotera och spara din nyckel eftersom nyckeln du angav är felaktig. Kontrollera att du har angett rätt nyckel och försök igen. Den andra möjligheten är att enheten inte har checkat in i organisationen på ett tag. Om du vill synkronisera de senaste uppdateringarna från organisationen väljer du enheten > **Status** > **Kontrollera åtkomst**. Försök sedan att lagra återställningsnyckeln igen. Om problemet kvarstår kan det betyda att organisationen inte har aktiverat FileVault på sitt håll. Kontakta IT-supporten och meddela att du har synkroniserat din enhet men fortfarande inte kan lagra din FileVault-nyckel.         |
|Din återställningsnyckel har uppdaterats. Om du skulle låsas ute från din enhet och måste få tag på nyckeln loggar du in i Företagsportal och väljer **Hämta återställningsnyckel**.    | Visas på enhetens informationssida. Nyckeln du sparade har roterats och den nya personliga återställningsnyckeln har lagrats.    |



## <a name="it-pro-support"></a>IT-supportpersonal

Om du är IT-supporttekniker och vill konfigurera och hantera FileVault-kryptering för macOS-enheter i organisationen läser du [Använda FileVault-diskkryptering för macOS med Intune](https://docs.microsoft.com/mem/intune/protect/encrypt-devices-filevault).  

## <a name="next-steps"></a>Nästa steg

Du kan alltid hämta din nyckel från Företagsportal-webbplatsen, Intune-appen och appen Företagsportal för iOS och Android och använda den för att få åtkomst till din Mac-enhet. Information om hur du hämtar återställningsnyckeln finns i [Hämta återställningsnyckel](get-recovery-key-cpweb.md).

Ta reda på vad du mer kan göra på Företagsportal-webbplatsen. Du hittar en lista med åtgärder i [Använda Intune Företagsportal-webbplatsen](using-the-intune-company-portal-website.md).  

Behöver du fortfarande hjälp? Kontakta IT-supporten. Titta efter IT-administratörens kontaktuppgifter på [företagsportalens webbplats](https://go.microsoft.com/fwlink/?linkid=2010980).  
