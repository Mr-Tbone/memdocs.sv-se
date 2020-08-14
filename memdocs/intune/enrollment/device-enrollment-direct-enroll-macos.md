---
title: Använda direktregistrering för macOS-enheter
titleSuffix: Microsoft Intune
description: Lär dig hur du registrerar macOS-enheter med hjälp av direktregistrering.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/04/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: scottbreenmsft
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1f12b90dd49dc9a9783a39fb78d74c40c6838b1e
ms.sourcegitcommit: c1afc8abd0d7da48815bd2b0e45147774c72c2df
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/05/2020
ms.locfileid: "87819978"
---
# <a name="use-direct-enrollment-for-macos-devices"></a>Använda direktregistrering för macOS-enheter

Intune stöder registrering av macOS-enheter med hjälp av direktregistrering (DE, Direct Enrollment) för företagsenheter. Direktregistrering rensar inte enheten. Den registrerar enheten via macOS-inställningar. Den här metoden har endast stöd för enheter **utan användartillhörighet**.

## <a name="prerequisites"></a>Förutsättningar

- Fysisk åtkomst till macOS-enheter
- [Ange MDM-utfärdare](../fundamentals/mdm-authority-set.md)
- [Ett Apple MDM-pushcertifikat](apple-mdm-push-certificate-get.md)
 - Administratörsbehörigheter på de macOS-enheter som du registrerar

## <a name="create-an-apple-configurator-profile-for-devices"></a>Skapa en Apple Configurator-profil för enheter

En enhetsregistreringsprofil definierar inställningarna som tillämpas under registreringen. Dessa inställningar tillämpas bara en gång. Följ dessa steg om du vill skapa en registreringsprofil för att registrera macOS-enheter med direktregistrering.

1. I [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) väljer du **Enheter** > **Registrera enheter** > **Apple-registrering** > **Apple Configurator**.

2. Välj **Profiler** > **Skapa**.

3. Under **Skapa registreringsprofil**, skriver du in ett **Namn** och en **Beskrivning** av profilen för administrativa ändamål. Användarna kan inte se den här informationen. Du kan använda fältet Namn för att skapa en dynamisk grupp i Azure Active Directory. Använd profilnamnet för att definiera parametern enrollmentProfileName för att tilldela registreringsprofilen till enheter. Läs mer om dynamiska Azure Active Directory-grupper.

4. För **Användartillhörighet** väljer du **Registrera utan användartillhörighet** – välj det här alternativet för enheter som inte tillhör en enskild användare. Använd det här för enheter som utför uppgifter utan att komma åt lokala användardata. Appar som kräver användartillhörighet (inklusive företagsportalappen som används för installation av verksamhetsspecifika appar) fungerar inte. Krävs för direktregistrering.

     > [!NOTE]
     > **Registrera med användartillhörighet** stöds inte i macOS vid användning av direktregistrering. För enheter som behöver användartillhörighet använder du Automatisk enhetsregistrering.

6. Spara profilen genom att välja **Skapa**.

## <a name="direct-enrollment"></a>Direktregistrering
Eftersom direktregistrering endast stöder registrering utan användartillhörighet kan företagsportalen inte användas för installation av tillgängliga program.

### <a name="export-the-profile-and-install-on-macos-devices"></a>Exportera profilen och installera på macOS-enheter

1. I [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) väljer du **Enheter** > **Registrera enheter** > **Apple-registrering** > **Apple Configurator** > **Profiler** > välj den profil som ska exporteras > **Exportera profil**.
2. Under **Direktregistrering**, väljer du **Hämta profil** och sparar filen. 

     > [!NOTE]
     > En nedladdad registreringsprofil är giltig i två veckor efter nedladdningen. Du kan ladda ned så många registreringsprofiler du behöver med hjälp av den här länken. Nedladdning av en ny profil gör inte att den tidigare blir ogiltig, men den förlänger inte heller den tidigare nedladdade filens förfallotid.
         
3. Överför filen till en macOS-dator för att installera den direkt.
4. Dubbelklicka på den sparade **.mobileconfig** för att öppna filen i Profiler.
5. När du uppmanas att installera hanteringsprofilen väljer du **Installera**.
6. Bekräfta vid nästa fråga att du vill installera hanteringsprofilen genom att välja **Installera**.
7. Ange autentiseringsuppgifterna för ett administratörskonto på macOS-enheten och klicka på **OK**.
8. macOS-enheten har nu registrerats i Intune och hanteras. Riktade profiler börjar laddas ned.

## <a name="next-steps"></a>Nästa steg

När du har registrerat macOS-enheter kan du börja [hantera dem](../remote-actions/device-management.md).