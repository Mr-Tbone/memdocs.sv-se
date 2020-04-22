---
title: Vilken information kan företaget se när enheten registreras?
description: Förklarar vad IT-avdelningen kan och inte kan se på den hanterade enheten.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/31/2019
ms.topic: article
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
ms.openlocfilehash: ccef2c10f4baaac9e417dd4952b1ea6d6cf47e5c
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "79346852"
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

**Vad din organisation alltid kan se:**

- Enhetsmodell som Google Pixel
- Enhetstillverkare, t.ex. Microsoft
- Operativsystem och version, t.ex. iOS 12.0.1
- Appinventering och appnamn såsom Microsoft Word. På personliga enheter kan organisationen bara se din hanterade appinventering. På företagsägda enheter kan organisationen se hela din appinventering.
- Enhetens ägare
- Enhetsnamn
- Enhetens serienummer
- IMEI

**Det här kan organisationen kanske se:**

- Telefonnummer: På företagsägda enheter kan det fullständiga telefonnumret visas. På personligt ägda enheter är endast de sista fyra siffrorna i telefonnumret synliga för organisationen. Du kan se ägarskapstypen för varje enskild enhet på enhetssidan **Enhetsinformation**.
- Lagringsutrymme för enheten: om du inte kan installera en obligatorisk app kan organisationen titta på din enhets lagringsutrymme för att ta reda på om det är för lågt.  
- Plats: din organisation kan aldrig se enhetens plats, såvida du inte behöver återställa en övervakad iOS-enhet som har försvunnit. Gå till [dokumentationen för Apple iOS](https://go.microsoft.com/fwlink/?linkid=853816) för att få mer information om övervakade enheter.  
- Information om appinventering: om organisationen använder skydd mot mobilhot kommer de att kunna se information om de appar som är på din iOS-enhet. Läs mer om [Mobile Threat Defense](you-are-prompted-to-install-mtd-ios.md). Om du har en personlig enhet kan organisationen bara se din hanterade appinventering. Om du har en företagsägd enhet kan organisationen se hela din appinventering.
- Nätverksinformation: en del information om nätverksanslutningar för Android-enheter kan vara tillgänglig för din organisationssupport. Om organisationen till exempel kräver att enheter ska finnas kvar i en viss byggnad kan din enhet identifiera det nätverk som den är ansluten till. 
