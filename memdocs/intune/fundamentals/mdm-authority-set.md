---
title: Konfigurera utfärdare för hantering av mobila enheter
titleSuffix: Microsoft Intune
description: Ange utfärdare för hantering av mobila enheter i Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/16/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 8deff871-5dff-4767-9484-647428998d82
ms.reviewer: damionw
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 380e39406dcc0b5bd286605804e3aa3c52750dd1
ms.sourcegitcommit: 62b451396eae660f2d5289ae3666b19ed1cc666d
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/19/2020
ms.locfileid: "88614729"
---
# <a name="set-the-mobile-device-management-authority"></a>Konfigurera utfärdare för hantering av mobila enheter

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Inställningen av hantering av mobil enhet bestämmer hur du ska hantera dina enheter. Som IT-administratör måste du ange en utfärdare för hantering av mobila enheter innan användarna kan registrera enheter för hantering.

Möjliga konfigurationerna är:

- **Fristående Intune** – Endast molnbaserad hantering, som du konfigurerar med hjälp av Azure-portalen. Innehåller den fullständiga uppsättning funktioner som Intune erbjuder. [Ange utfärdare för hantering av mobila enheter i Intune-konsolen](#set-mdm-authority-to-intune).

- **Intune-samhantering** – Integration av Intunes molnlösning med Configuration Manager för Windows 10-enheter. Du kan konfigurera Intune med hjälp av Configuration Manager-konsolen. [Konfigurera automatisk registrering av enheter i Intune](https://docs.microsoft.com/configmgr/comanage/tutorial-co-manage-clients#configure-auto-enrollment-of-devices-to-intune). 

- **Basic Mobility and Security for Office 365** – Om du har aktiverat den här konfigurationen visas MDM-utfärdaren som ”Office 365”. Om du vill börja använda Intune så måste du köpa Intune-licenser.

- **Basic Mobility and Security for Office 365-[samexistens](#coexistence)** – Du kan lägga till Intune i din klientorganisation om du redan använder Basic Mobility and Security for Office 365 och konfigurera hanteringsbehörigheten till antingen Intune eller Basic Mobility and Security for Office 365 så att varje användare får bestämma vilken tjänst som ska användas för att hantera deras MDM-registrerade enheter. Varje användares hanteringsbehörighet definieras utifrån den licens som tilldelats till användaren: Om användaren bara har licens för Microsoft 365 Basic eller Standard hanteras användarens enheter av Basic Mobility and Security for Office 365. Om användaren har en licens som berättigar till Intune hanteras enheterna av Intune. Om du lägger till en licens som berättigar till Intune för en användare som tidigare hanterades av Basic Mobility and Security for Office 365, växlar hanteringen av enheterna till Intune. Se till att Intune-konfigurationer som tilldelats till användare ersätter Basic Mobility and Security for Office 365 innan användarna byts till Intune, annars förlorar enheterna Basic Mobility and Security for Office 365-konfigurationen och får ingen annan konfiguration från Intune.

## <a name="set-mdm-authority-to-intune"></a>Ange Intune som utfärdare för hantering av mobila enheter

För klienter som använder tjänstversion 1911 och senare anges MDM-utfärdaren automatiskt till Intune.

För klienter med en tjänstversion tidigare än 1911 följer du stegen nedan om du inte har angett MDM-utfärdare än.

1. I [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) väljer du den orangefärgade banderollen för att öppna inställningen **Utfärdare av Hantering av mobila enheter**. Den orangefärgade banderollen visas bara om du inte har angett MDM-utfärdaren än.
2. Under **Utfärdare av Hantering av mobila enheter** väljer du en utfärdare bland följande alternativ:
  - **Intune-utfärdare av mobilenhetshantering**
  - **Inga**

  ![Skärmbild av Intune-skärmen Ange utfärdare för hantering av mobila enheter](./media/mdm-authority-set/set-mdm-auth.png)

  Ett meddelande indikerar att du har angett MDM-utfärdare till Intune.

### <a name="workflow-of-intune-administration-ui"></a>Arbetsflöde i användargränssnitt för Intune-administration
När Android- eller Apple-enhetshantering är aktiverat skickar Intune enhets- och användarinformation för att kunna integrera med dessa tredjepartstjänster och hantera deras respektive enheter.

Scenarier som kräver ett medgivande om att dela data ingår vid följande tillfällen:
- Du aktiverar Android-arbetsprofiler.
- Du aktiverar och laddar upp Apple MDM-pushcertifikat.
- Du aktiverar någon av Apples tjänster som t.ex. programmet för enhetsregistrering, School Manager och volyminköpsprogrammet.

I båda fallen är medgivandet strikt relaterat till att köra en tjänst för hantering av mobilenheter. Till exempel att bekräfta att en IT-administratör har godkänt att Google- eller Apple-enheter får registreras. Dokumentation som visar vilken information som delas när de nya arbetsflödena publiceras finns på följande platser:
- [Data som Intune skickar till Google](https://aka.ms/Data-intune-sends-to-google)
- [Data som Intune skickar till Apple](https://aka.ms/data-intune-sends-to-apple)

## <a name="key-considerations"></a>Viktigt att tänka på
När du har bytt till den nya MDM-utfärdaren kan det ta upp till åtta timmar innan enheten ansluter till och synkroniserar med tjänsten. Du måste konfigurera inställningar i den nya MDM-utfärdaren så att registrerade enheter fortsätter att hanteras och skyddas efter ändringen. 
- Enheter måste ansluta till tjänsten efter ändringen så att inställningarna från den nya MDM-utfärdaren (fristående Intune) ersätter de befintliga inställningarna på enheten.
- När du har ändrat MDM-utfärdaren finns några av de grundläggande inställningarna (t.ex. profiler) från den tidigare MDM-utfärdaren kvar på enheten i upp till sju dagar, eller tills enheten ansluter till tjänsten för första gången. Vi rekommenderar att du konfigurerar appar och inställningar (t.ex. principer, profiler och appar) i den nya MDM-utfärdaren så snart som möjligt och distribuerar inställningen till användargrupperna för användare som har befintliga registrerade enheter. Så fort en enhet ansluter till tjänsten efter ändringen av MDM-utfärdare tar den emot de nya inställningarna från den nya MDM-utfärdaren, vilket förhindrar avbrott i hanteringen och skyddet av enheten.
- Enheter som inte har associerade användare (vanligt om du har iOS/iPadOS-programmet för enhetsregistrering eller vid massregistreringsscenarier) migreras inte till den nya MDM-utfärdaren. För dessa enheter måste du ringa supporten och få hjälp med att flytta dem till den nya MDM-utfärdaren.

## <a name="coexistence"></a>Samexistens

Genom att aktivera samexistens kan du använda Intune för en ny uppsättning användare och fortsätta att använda Basic Mobility and Security för de befintliga användarna. Du styr vilka enheter som hanteras av Intune via användaren. Om en användare har tilldelats en Intune-licens eller använder Intune-samhantering med Configuration Manager, kommer alla användarens registrerade enheter att hanteras av Intune. Annars hanteras användaren av Basic Mobility and Security.

Tre viktiga steg krävs för att aktivera samexistens:
1. Förberedelse
2. Lägga till Intune-utfärdare av mobilenhetshantering
3. Användar- och enhetsmigrering (valfritt)

### <a name="preparation"></a>Förberedelse

Innan du aktiverar samexistens med Basic Mobility and Security bör du tänka på följande:
- Se till att du har tillräckligt många [Intune-licenser](licenses.md) för de användare som ska hanteras via Intune.
- Kontrollera vilka användare som har tilldelats Intune-licenser. När du har aktiverat samexistens kommer enheter som hör till användare som redan har tilldelats en Intune-licens att gå över till Intune. För att undvika oväntade enhetsflyttningar rekommenderar vi att du väntar med att tilldela Intune-licenser tills du har aktiverat samexistens.
- Skapa och distribuera Intune-principer för att ersätta enhetssäkerhetsprinciper som ursprungligen distribuerades via säkerhets- och efterlevnadsportalen för Office 365. Gör detta för alla användare som ska flyttas från Basic Mobility and Security till Intune. Om dessa användare inte tilldelas några Intune-principer kan deras Basic Mobility and Security-inställningar gå förlorade när du aktiverar samexistens. Om du inte ersätter principerna, t.ex. hanterade e-postprofiler, går dessa inställningar förlorade. Även när du ersätter enhetssäkerhetsprinciper med Intune-principer kan användare uppmanas att autentisera sina e-postprofiler igen när enheten har flyttats till Intune-hantering.

### <a name="add-intune-mdm-authority"></a>Lägga till Intune-utfärdare av mobilenhetshantering

För att kunna aktivera samexistens måste du lägga till Intune som MDM-utfärdare för din miljö:

1. Logga in på endpoint.microsoft.com med behörighet som global Azure AD-administratör eller Intune-tjänstadministratör.
2. Gå till **Enheter**.
3. Bladet **Lägg till utfärdare av mobilenhetshantering** visas.
4. Om du vill byta MDM-utfärdare från *Office 365* till *Intune* och aktivera samexistens väljer du **Intune-utfärdare för mobilenhetshantering** > **Lägg till**.
  ![Skärmbild av skärmen Lägg till utfärdare av mobilenhetshantering](./media/mdm-authority-set/add-mdm-authority.png)

### <a name="migrate-users-and-devices-optional"></a>Migrera användare och enheter (valfritt)

När du har aktiverat Intune som MDM-utfärdare aktiveras samexistens och du kan börja hantera användare via Intune. Optionally, if you want to move devices previously managed by Basic Mobility and Security to be managed by Intune, assign those users an Intune license. Användarnas enheter kommer att flyttas till Intune vid nästa MDM-incheckning. Inställningar som tillämpas på dessa enheter via Basic Mobility and Security kommer inte längre att tillämpas och kommer att tas bort från enheterna.

## <a name="mobile-device-cleanup-after-mdm-certificate-expiration"></a>Rensa mobila enheter efter att MDM-certifikatet upphört att gälla

MDM-certifikatet förnyas automatiskt när mobila enheter kommunicerar med Intune-tjänsten. Om mobila enheter raderas eller om de inte kan kommunicera med Intune-tjänsten under en viss tidsperiod, kommer MDM-certifikatet inte att förnyas. Enheten tas bort från Azure-portalen 180 dagar efter att MDM-certifikatet har upphört att gälla.

## <a name="remove-mdm-authority"></a>Ta bort MDM-utfärdare

MDM-utfärdaren kan inte ändras tillbaka till Okänd. MDM-utfärdaren används av tjänsten för att avgöra vilken portal som registrerade enheter rapporterar till (Microsoft Intune eller Basic Mobility and Security for Office 365).

## <a name="what-to-expect-after-changing-the-mdm-authority"></a>Vad som händer MDM-utfärdaren har ändrats

- När Intune-tjänsten upptäcker att en klients MDM-utfärdare har ändrats, skickar den ett aviseringsmeddelande till alla registrerade enheter och uppmanar dem att ansluta till samt synkronisera med tjänsten (detta sker utanför den normala schemalagda kontrollen). När MDM-utfärdaren för klienten har ändrats från fristående Intune kommer därför alla enheter som är påslagna och online att ansluta till tjänsten, ta emot inställningarna från den nya MDM-utfärdaren och börja hanteras av den nya MDM-utfärdaren. Det sker inget avbrott i hanteringen och skyddet av dessa enheter.
- Även för enheter som är påslagna och online under (eller strax efter) ändringen av MDM-utfärdaren uppstår det en fördröjning på upp till åtta timmar (beroende på tidpunkten för nästa schemalagda regelbundna incheckning) innan enheterna registreras med tjänsten med den nya MDM-utfärdaren.  

 > [!IMPORTANT]  
 > Under perioden från det att du ändrar MDM-utfärdaren tills det förnyade APNs-certifikatet laddas upp till den nya utfärdaren kommer nya enhetsregistreringar och enhetskontroller på iOS/iPadOS-enheter att misslyckas. Därför är det viktigt att du granskar och laddar upp APNs-certifikatet till den nya utfärdaren så snart som möjligt efter ändringen av MDM-utfärdare.

- Användarna kan snabbt gå över till den nya MDM-utfärdaren genom att manuellt starta en incheckning från enheten till tjänsten. Användarna kan enkelt göra denna ändring genom att initiera en enhetskompatibilitetskontroll från företagsportalappen.
- Du kan kontrollera att allt fungerar korrekt efter det att enheterna har anslutit till och synkroniserat med tjänsten efter ändringen av MDM-utfärdare, genom att söka efter enheterna i den nya MDM-utfärdaren.
- Det uppstår en övergångsperiod om en enhet är frånkopplad under ändringen av MDM-utfärdaren tills dess enheten ansluter till tjänsten. För att säkerställa att enheten fortfarande är skyddad och fungerar under den här övergångsperioden finns följande profiler kvar på enheten i upp till sju dagar (eller tills enheten ansluter till den nya MDM-utfärdaren och tar emot nya inställningar som skriver över de befintliga):
   - E-postprofil
   - VPN-profil
   - Certifikatprofil
   - Wi-Fi-profil
   - Konfigurationsprofiler
- När du har bytt till den nya MDM-utfärdaren kan det ta upp till en vecka innan kompatibilitetsinformationen i Microsoft Intune-administrationskonsolen visar korrekta data. Kompatibilitetsstatusen i Azure Active Directory och på enheten är dock korrekt, så enheten är fortfarande skyddad.
- Kontrollera att de nya inställningarna som ska skriva över befintliga inställningar har samma namn som de tidigare inställningarna för att säkerställa att de gamla inställningarna skrivs över. Annars är risken att de gamla profilerna och principerna ligger kvar på enheterna.  

 > [!TIP]  
 > Vi rekommenderar att du skapar alla hanteringsinställningar och konfigurationer, samt även distributionerna, så snart som möjligt efter ändringen av MDM-utfärdaren. På så sätt kan du vara säker på att enheterna skyddas och hanteras aktivt under övergångsperioden.

- Bekräfta att de nya enheterna registreras korrekt med den nya utfärdaren genom att utföra följande steg när du har ändrat MDM-utfärdaren:  
 - Registrera en ny enhet.
 - Kontrollera att den nyregistrerade enheten visas i den nya MDM-utfärdaren.
 - Utför en åtgärd på enheten, t.ex. fjärrlåsning, från administrationskonsolen. Om åtgärden lyckas betyder det att enheten hanteras av den nya MDM-utfärdaren.
- Om du har problem med specifika enheter kan du avregistrera och registrera om enheterna så att de börjar använda den nya utfärdaren och hanteras så snart som möjligt.

## <a name="next-steps"></a>Nästa steg

När MDM-utfärdaren har angetts kan du börja [registrera enheter](../enrollment/device-enrollment.md).
