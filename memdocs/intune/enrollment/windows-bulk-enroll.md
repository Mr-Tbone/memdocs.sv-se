---
title: Massregistrering för Windows 10
titleSuffix: Microsoft Intune
description: Skapa ett massregistreringspaket för Microsoft Intune
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 5/21/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 1f39c02a-8d8a-4911-b4e1-e8d014dbce95
ms.reviewer: spshumwa
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: eabdae9fcc8bdc3b6c93d5b735a5b9fbf4dcf69a
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078931"
---
# <a name="bulk-enrollment-for-windows-devices"></a>Massregistrering för Windows-enheter

Som administratör kan du ansluta ett stort antal nya Windows-enheter till Azure Active Directory och Intune. Du massregistrerar enheter för Azure AD-klienten genom att skapa ett konfigurationspaket med hjälp av appen Windows Configuration Designer (WCD). När du tillämpar konfigurationspaketet på företagsägda enheter ansluts de till Azure AD-klienten och registreras för Intune-hantering. När paketet har tillämpats kan dina Azure AD-användare logga in.

Azure AD-användare är standardanvändare på enheterna och kan ta emot de tilldelade Intune-principer och appar som krävs. Windows-enheter som registreras i Intune med hjälp av massregistrering kan använda företagsportalappen för att installera tillgängliga appar. 

## <a name="prerequisites-for-windows-devices-bulk-enrollment"></a>Krav för massregistrering av Windows-enheter

- Enheter som kör Windows 10 Creator Update (version 1703) eller senare
- [Automatisk registrering i Windows](windows-enroll.md#enable-windows-10-automatic-enrollment)

## <a name="create-a-provisioning-package"></a>Skapa ett konfigurationspaket

1. Hämta [Windows Configuration Designer (WCD)](https://www.microsoft.com/store/apps/9nblggh4tx22) från Microsoft Store.
   ![Skärmbild av Store med Windows Configuration Designer-appen](./media/windows-bulk-enroll/bulk-enroll-store.png)

2. Öppna appen **Windows Configuration Designer** och välj **Konfigurera skrivbordsenheter**.
   ![Skärmbild över att välja Konfigurera skrivbordsenheter i Windows Configuration Designer-appen](./media/windows-bulk-enroll/bulk-enroll-select.png)

3. Fönstret **Nytt projekt** öppnas, där du anger följande information:
   - **Namn** – Namnet på ditt projekt
   - **Projektmapp** – Lagringsplatsen för projektet
   - **Beskrivning** – En valfri beskrivning av projektet ![Skärmbild över att ange namn, projektmapp och beskrivning i Windows Configuration Designer-appen](./media/windows-bulk-enroll/bulk-enroll-name.png)

4. Ange ett unikt namn för dina enheter. Namnen kan innehålla ett serienummer (%SERIAL%) eller en slumpmässig uppsättning tecken. Du kan också ange en produktnyckel om du uppgraderar Windows, konfigurerar enheten för delad användning och tar bort det tidigare installerade programmet.
   
   ![Skärmbild över att ange namn och produktnyckel i Windows Configuration Designer-appen](./media/windows-bulk-enroll/bulk-enroll-device.png)

5. Du kan också konfigurera de Wi-Fi-nätverksenheter som ska anslutas när de startar första gången.  Om nätverksenheterna inte är konfigurerade, krävs en anslutning till ett kabelanslutet nätverk när enheten startas första gången.
   ![Skärmbild över att aktivera Wi-Fi, inklusive nätverks-SSID och nätverkstyper i Windows Configuration Designer-appen](./media/windows-bulk-enroll/bulk-enroll-network.png)

6. Välj **Registrera i Azure AD**, ange ett datum i **Förfallodatum för masstoken** och välj sedan **Hämta masstoken**.
   ![Skärmbild över kontohantering i Windows Configuration Designer-appen](./media/windows-bulk-enroll/bulk-enroll-account.png)

7. Ange dina Azure AD-autentiseringsuppgifter för att kunna hämta en masstoken.
   ![Skärmbild över att logga in i Windows Configuration Designer-appen](./media/windows-bulk-enroll/bulk-enroll-cred.png)

8. I **Använd det här kontot överallt på den här enheten** väljer du **Endast den här appen**.

9. Klicka på **Nästa** när **Masstoken** har hämtats.

10. Du kan också **Lägga till program** och **Lägga till certifikat**. Dessa appar och certifikat är konfigurerade på enheten.

11. Du kan också lösenordsskydda ditt konfigurationspaket.  Klicka på **Skapa**.
    ![Skärmbild över paketskydd i Windows Configuration Designer-appen](./media/windows-bulk-enroll/bulk-enroll-create.png)

## <a name="provision-devices"></a>Konfigurera enheter

1. Få åtkomst till konfigurationspaketet på den plats som anges i **Projektmapp** i appen.

2. Välj hur du ska tillämpa konfigurationspaketet på enheten.  Ett konfigurationspaket kan tillämpas på en enhet på följande sätt:
   - Placera konfigurationspaketet på en USB-enhet, sätt i USB-enheten i den enhet som du vill massregistrera och tillämpa den under den första installationen
   - Placera konfigurationspaketet i en nätverksmapp och infoga den efter den första installationen

   Stegvisa anvisningar för att använda ett konfigurationspaket finns i [Tillämpa ett konfigurationspaket](https://technet.microsoft.com/itpro/windows/configure/provisioning-apply-package).

3. När du har tillämpat paketet startas enheten automatiskt om efter en minut.
   ![Skärmbild över att ange namn, projektmapp och beskrivning i Windows Configuration Designer-appen](./media/windows-bulk-enroll/bulk-enroll-add.png)

4. När enheten startas om, ansluter den till Azure Active Directory och registreras i Microsoft Intune.

## <a name="troubleshooting-windows-bulk-enrollment"></a>Felsökning av massregistrering i Windows

### <a name="provisioning-issues"></a>Konfigurationsproblem
Konfigurationen är avsedd att användas på nya Windows-enheter. Konfigurationsfel kan kräva en rensning av enheten eller en enhetsåterställning från en startavbildning. I nedanstående exempel beskrivs några orsaker till konfigurationsfel:

- Ett konfigurationspaket som försöker ansluta till en Active Directory-domän eller Azure Active Directory-klient som inte skapar ett lokalt konto, kan innebära att enheten inte kan nås om domänanslutningen misslyckas på grund av bristande nätverksanslutning.
- Skript som körs av etableringspaketet körs i systemets kontext. Skripten kan göra godtyckliga ändringar till enhetens filsystem och konfigurationer. Ett skadligt eller felaktigt skript kan placera enheten i ett tillstånd som bara kan återställas av en återställning av avbildningen eller en rensning av enheten.

Du kan kontrollera lyckad/misslyckad status för inställningarna i ditt paket i adminloggen **Provisioning-Diagnostic-Provider** (etablering-diagnostik-provider) i Loggboken.

### <a name="bulk-enrollment-with-wi-fi"></a>Massregistrering med Wi-Fi 

Om du inte använder ett öppet nätverk måste du använda [certifikat på enhetsnivå](../protect/certificates-configure.md) för att kunna initiera anslutningar. Massregistrerade enheter kan inte använda användarriktade certifikat för nätverksåtkomst. 

### <a name="conditional-access"></a>Villkorlig åtkomst
Villkorlig åtkomst är inte tillgänglig för Windows-enheter som registreras med massregistrering.
