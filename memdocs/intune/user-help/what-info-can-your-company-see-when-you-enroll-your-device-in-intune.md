---
title: Vilken information kan företaget se när enheten registreras?
description: Förklarar vad IT-avdelningen kan och inte kan se på den hanterade enheten.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 06/11/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 12655728-a1af-4d89-97bc-925fe36c0dc4
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.collection: ''
ms.openlocfilehash: bc3ff7b10d3b0ae5779db26fae711bc335c8ec62
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/18/2020
ms.locfileid: "86461682"
---
# <a name="what-information-can-my-organization-see-when-i-enroll-my-device"></a>Vilken information min organisation se när jag registrerar min enhet?

Organisationen kan inte se din personliga information när du registrerar en enhet med Microsoft Intune. När du registrerar en enhet ger du organisationen behörighet att visa vissa typer av information på din enhet, till exempel enhetsmodell och serienummer. Organisationen använder den här informationen för att skydda företagsdata på enheten.

**Vad din organisation aldrig kan se:**

- Historik för samtal och surfning
- E-post och textmeddelanden
- Kontakter
- Kalender
- Lösenord
- Bilder (inte heller de som ingår i appen Foton eller i Kamerabilder)
- Filer
- För företagsägda enheter med en arbetsprofil, program och data i din personliga profil. 

**Vad din organisation alltid kan se:**

- Enhetsmodell som Google Pixel
- Enhetstillverkare, t.ex. Microsoft
- Operativsystem och version, t.ex. iOS 12.0.1
- Appinventering och appnamn såsom Microsoft Word. På personliga enheter kan organisationen bara se din hanterade appinventering. På företagsägda fullständigt hanterade enheter och dedikerade enheter kan organisationen se alla dina appar. För företagsägda enheter med en arbetsprofil kan din organisation bara se appinventeringen i din arbetsprofil.
- Enhetens ägare
- Enhetsnamn
- Enhetens serienummer
- IMEI

 > [!NOTE]
 > För fullständigt hanterade och dedikerade enheter för Android Enterprise kan du inte se alla appar.
 
 > [!NOTE]
 > En app anses vara en **hanterad app** när den installeras på något av följande sätt:
 > 1. En användare installerar den från appen Företagsportal efter att en Intune-administratör publicerat den som **tillgänglig**.
 > 2. Appen publiceras som **obligatorisk** av en Intune-administratör och installeras på enheten. 
 >
 > Om du är IT-administratör eller supportmedarbetare i organisationen och vill ha mer information om hantering av appar i Intune kan du läsa [Förstå funktionerna för ohanterade appar, hanterade appar och MAM-appar](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/understanding-the-capabilities-of-unmanaged-apps-managed-apps/ba-p/249164).
    
**Det här kan organisationen kanske se:**

- Telefonnummer: För företagsägda enheter kan det fullständiga telefonnumret visas. På personligt ägda enheter är endast de sista fyra siffrorna i telefonnumret synliga för organisationen. Du kan se ägarskapstypen för varje enskild enhet på enhetssidan **Enhetsinformation**.
- Enhetens lagringsutrymme: Om du inte kan installera en obligatorisk app kan organisationen se om du har för lite lagringsutrymme på din enhet.  
- Plats: På företagsägda enheter kan organisationen se var en förlorad enhet befinner sig. Din organisation ser inte var personliga enheter befinner sig, såvida de inte försöker hitta en övervakad iOS-enhet som förlorats. Gå till [dokumentationen för Apple iOS](https://go.microsoft.com/fwlink/?linkid=853816) för att få mer information om övervakade enheter.  
- Information om appinventering: Om organisationen använder skydd mot mobilhot kommer de att kunna se information om apparna som finns på din iOS-enhet. Läs mer om [Mobile Threat Defense](set-up-mobile-threat-defense.md). På personliga enheter kan organisationen annars bara se dina hanterade appar. På företagsägda enheter kan organisationen se alla dina appar.
- Nätverksinformation: En del information om nätverksanslutningar för Android-enheter kan vara tillgänglig för din organisationssupport. Om organisationen till exempel kräver att enheter ska finnas kvar i en viss byggnad kan din enhet identifiera det nätverk som den är ansluten till. 
