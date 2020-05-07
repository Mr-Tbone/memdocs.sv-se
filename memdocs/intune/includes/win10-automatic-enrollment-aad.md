## <a name="enable-windows-10-automatic-enrollment"></a>Aktivera automatisk registrering i Windows 10

Med automatisk registrering kan användarna registrera sina Windows 10-enheter i Intune. Användarna registrerar genom att lägga till sina arbetskonton till sina personligt ägda enheter eller genom att ansluta sina företagsägda enheter till Azure Active Directory. Enheten registreras och ansluts till Azure Active Directory i bakgrunden. När enheten har registrerats hanteras den med Intune.

**Förutsättningar**

- Azure Active Directory Premium-prenumeration ([provprenumeration](https://go.microsoft.com/fwlink/?LinkID=816845))
- Microsoft Intune-prenumeration

### <a name="configure-automatic-mdm-enrollment"></a>Konfigurera automatisk MDM-registrering

1. Logga in på [Azure Portal](https://portal.azure.com) och välj **Azure Active Directory**.

   ![Skärmbild av Azure-portalen](../enrollment/media/windows-enroll/auto-enroll-azure-main.png)

2. Välj **Mobility (MDM och MAM)** .

   ![Skärmbild av Azure-portalen](../enrollment/media/windows-enroll/auto-enroll-mdm.png)

3. Välj **Microsoft Intune**.

   ![Skärmbild av Azure-portalen](../enrollment/media/windows-enroll/auto-enroll-intune.png)

4. Konfigurera **MDM-användaromfattning**. Ange vilka användares enheter som ska hanteras av Microsoft Intune. Dessa Windows 10-enheter kan registreras automatiskt för hantering med Microsoft Intune.

   - **Ingen** – Automatisk registrering av MDM är inaktiverad
   - **Vissa** – Välj de **grupper** som automatiskt kan registrera sina Windows 10-enheter
   - **Alla** – Alla användare kan automatiskt registrera sina Windows 10-enheter

      > [!IMPORTANT]
      > För Windows BYOD-enheter har MAM-användaromfånget företräde om både MAM- och MDM-användaromfånget (automatisk MDM-registrering) har aktiverats för alla användare (eller samma grupper av användare). Enheten MDM-registreras inte och Windows Information Protection-principer (WIP) tillämpas om du har konfigurerat dem.
      >
      > Om avsikten är att aktivera automatisk registrering för Windows BYOD-enheter till en MDM: Konfigurera MDM-användaromfånget till **Alla** (eller **Vissa** och ange en grupp) och MAM-användaromfånget till **Ingen** (eller **Vissa** och ange en grupp; se till att användarna inte är medlemmar i en grupp som omfattas av både MDM- och MAM-användaromfång).
      >
      >För [företagsenheter](../enrollment/enrollment-restrictions-set.md#blocking-personal-windows-devices) får MDM-användaromfånget företräde om både MDM- och MAM-användaromfång är aktiverade. Enheten registreras automatiskt i den konfigurerade MDM:en.

   > [!NOTE]
   > MDM-användaromfånget måste vara inställt på en Azure AD-grupp som innehåller användarobjekt.

   ![Skärmbild av Azure-portalen](../enrollment/media/windows-enroll/auto-enroll-scope.png)

5. Använd standardvärdena för följande URL:er:
    - **Webbadress till MDM-användarvillkor**
    - **Webbadress till MDM-identifiering**
    - **Webbadress till MDM-kompatibilitet**

6. Välj **Spara**.

Som standard är inte tvåfaktorautentisering aktiverat för tjänsten. Tvåfaktorautentisering rekommenderas dock när du registrerar en enhet. För att aktivera tvåfaktorautentisering konfigurerar du en provider för tvåfaktorautentisering i Azure AD och konfigurerar dina användarkonton för multifaktorautentisering. Se [Komma igång med Azure Multi-Factor Authentication-servern](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-cloud).
