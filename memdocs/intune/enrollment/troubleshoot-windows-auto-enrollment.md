---
title: Felsöka automatisk registrering av Windows 10-enheter i Intune
titleSuffix: Microsoft Intune
description: Lär dig hur du felsöker automatisk enhetsregistrering.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 8/3/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: jchombe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6aff5dfe62c1c44ec22f56c287220b59b98a7536
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915491"
---
# <a name="troubleshoot-windows-10-group-policy-based-auto-enrollment-in-intune"></a>Felsöka automatisk registrering baserad på grupprinciper av Windows 10-enheter i Intune

Du kan använda en grupprincip till att utlösa automatisk registrering till MDM för enheter kopplade till en AD-domän (Active Directory). Mer information om den här funktionen finns i [Registrera en Windows 10-enhet automatiskt med hjälp av en grupprincip](/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy).

## <a name="verify-the-configuration"></a>Verifiera konfigurationen

Innan du börjar felsöka bör du kontrollera att allt är konfigurerat på rätt sätt. Om problemet inte kan åtgärdas under verifieringen kan du felsöka ytterligare genom att kontrollera viktiga loggfiler.

- Kontrollera att en giltig Intune-licens är tilldelad till användaren som försöker registrera enheten.

   ![Kontrollera Intune-licensen](./media/troubleshoot-windows-auto-enrollment/intune-license.png)

- Kontrollera att automatisk registrering är aktiverad för alla användare som ska registrera enheter i Intune. Mer information finns i [Azure AD och Microsoft Intune: Automatisk MDM-registrering i den nya portalen](/windows/client-management/mdm/azure-ad-and-microsoft-intune-automatic-mdm-enrollment-in-the-new-portal).

   ![Kontrollera automatisk registrering](./media/troubleshoot-windows-auto-enrollment/verify-auto-enrollment.png)

   - Kontrollera att **MDM-användaromfång** har angetts till **Alla** så att alla användare ska kunna registrera en enhet i Intune.
   - Kontrollera att **MDM-användaromfång** har angetts till **Inga**. Annars har den här inställningen företräde framför MDM-omfånget vilket orsakar problem.
   - Kontrollera att **Webbadress till MDM-identifiering** har angetts till **https://enrollment.manage.microsoft.com/enrollmentserver/discovery** .

- Kontrollera att enheten kör Windows 10 version 1709 eller senare.

- Kontrollera att enheterna är inställda som  **Azure AD-hybridanslutna**. Det innebär att enheterna både är domänanslutna och Azure AD-anslutna.

   Du kontrollerar inställningarna genom att köra **dsregcmd /status** på kommandoraden. Kontrollera sedan följande statusvärden i utdata:

   - Device State (enhetstillstånd)
 
     ```asciidoc
     AzureAdJoined: YES
     DomainJoined: YES
     ```

   - SSO State (SSO-tillstånd)

     ```asciidoc
     AzureAdPrt: YES
     ```

   Du hittar samma information i listan med Azure AD-anslutna enheter:

   ![Lista med Azure AD-anslutna enheter](./media/troubleshoot-windows-auto-enrollment/ad-joined-devices.png)

- Både **Microsoft Intune** och **Microsoft Intune Enrollment** kan visas under **Mobility (MDM och MAM)**  på Azure AD-bladet. Om båda visas måste du konfigurera inställningarna för automatisk registrering under **Microsoft Intune**.

- Kontrollera att följande grupprincipinställning har distribuerats till alla enheter som ska registreras i Intune:

   **Datorkonfiguration** > **Policyer** > **Administrativa mallar** > **Windows-komponenter** > **MDM** > **Aktivera automatisk MDM-registrering med standardautentiseringsuppgifter för Azure AD**

   Du kan kontakta domänadministratörerna för att kontrollera att grupprincipinställningen har distribuerats.

- Kontrollera att enheten inte har registrerats i Intune med den klassiska PC-agenten.
- Kontrollera följande inställningar i Azure AD och Intune:

   **I inställningarna för Azure AD-enheter:**

   ![Inställningar för Azure AD-enheter](./media/troubleshoot-windows-auto-enrollment/device-setting.png)

   - Inställningen **Användare kan ansluta enheter till Azure AD** har angetts till **Alla**.
   - Antalet enheter som en användare har i Azure AD får inte överskrida kvoten **Maximalt antal enheter per användare**.
   
   **I begränsningar för Intune-registrering:**

   - Registrering av Windows-enheter tillåts.

     ![Tillåten registrering av Windows-enheter](./media/troubleshoot-windows-auto-enrollment/restrictions.png)

## <a name="troubleshooting"></a>Felsökning

Om problemet kvarstår granskar du MDM-loggarna på enheten på följande plats i Loggboken:

**Program- och tjänstloggar** > **Microsoft** > **Windows** > **DeviceManagement-Enterprise-Diagnostic-Provider** > **Administratör**

Sök efter Event ID 75 (meddelandet ”Auto MDM Enroll: Succeeded” (händelse-ID 75, automatisk MRM-registrering lyckades)). Den här händelsen anger att den automatiska registreringen har utförts.

Händelse-ID 75 loggas inte i följande situationer:

- Registreringen misslyckas.

  Du kan kontrollera det här felet genom att leta efter Event ID 76 (meddelande: Automatisk MDM-registrering: Misslyckades (okänd Win32-felkod: 0x8018002b)). Den här händelsen indikerar en misslyckad automatisk registrering.

  Du kan läsa om en möjlig lösning på problemet i [Felsöka problem med registrering av Windows-enheter i Microsoft Intune](/intune/troubleshoot-windows-enrollment-errors).

- Registreringen utlöstes inte alls. I det här fallet loggas inte händelse-ID 75 eller 76.
  
  Den automatiska registreringsprocessen utlöses av uppgiften **Schemat som skapats av registreringsklienten för automatisk registrering i MDM från AAD** som finns under **Microsoft** > **Windows** > **EnterpriseMgmt**.

  ![Registreringen utlöstes inte](./media/troubleshoot-windows-auto-enrollment/trigger.png)

  Den här uppgiften skapas när grupprincipinställningen **Aktivera automatisk MDM-registrering med standardautentiseringsuppgifter för Azure AD** har distribuerats till målenheten. Aktiviteten är schemalagd att köras var 5:e minut under en dag.

  Kontrollera att aktiviteten har startats genom att granska händelseloggarna för schemaläggaren på följande plats i Loggboken:

  **Program- och tjänstloggar > Microsoft > Windows > Schemaläggaren > Drift**

  När aktiviteten utlöses i schemaläggaren loggas händelse-ID 107.

  Händelse-ID 102 loggas när uppgiften har slutförts. Händelsen loggas oavsett om den automatiska registreringen utförs eller inte.

  > [!NOTE]
  > Du kan använda loggen för schemaläggaren till att kontrollera om den automatiska registreringen utlöses. Du kan dock inte använda loggen till att avgöra om den automatiska registreringen har utförts.

  Följande situation kan leda till att schemat som skapas av registreringsklienten för uppgiften med automatisk registrering i MDM från AAD inte startas:

  - Enheten är redan registrerad i en annan MDM-lösning. I det här fallet loggas händelse-ID 7016 tillsammans med felkoden 2149056522 i händelseloggen **Program- och tjänstloggar** > **Microsoft** > **Windows** > **Schemaläggaren** > **Drift**.

    Lös problemet genom att avregistrera enheten från MDM.

  - Det är problem med grupprincipen. I det här fallet kan du framtvinga en uppdatering av grupprincipinställningarna genom att köra följande kommando:

    **gpupdate /force**

    Om problemet kvarstår utför du ytterligare felsökning i Active Directory.

## <a name="next-steps"></a>Nästa steg
[Felsöka registrering av Windows-enheter](troubleshoot-windows-enrollment-errors.md)