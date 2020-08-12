---
title: Självstudie&#58; aktivera samhantering för befintliga klienter
titleSuffix: Configuration Manager
description: Konfigurera samhantering med Microsoft Intune när du redan hanterar Windows 10-enheter med Configuration Manager.
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: tutorial
ms.assetid: 140c522f-d09a-40b6-a4b0-e0d14742834a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9cb8097fbdd57184e5cd0e229cf96dcb317cf1e5
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127349"
---
# <a name="tutorial-enable-co-management-for-existing-configuration-manager-clients"></a>Självstudie: Aktivera samhantering för befintliga Configuration Manager-klienter

Med samhantering kan du hålla väletablerade processer för att använda Configuration Manager för att hantera datorer i din organisation. Samtidigt ska du investera i molnet genom att använda Intune för säkerhet och modern etablering.  

I den här självstudien ställer du in samhantering av dina Windows 10-enheter som redan har registrerats i Configuration Manager. Den här självstudien börjar med den plats där du redan använder Configuration Manager för att hantera dina Windows 10-enheter.

Använd den här självstudien när:  

- Du har en lokal Active Directory som du kan ansluta till Azure Active Directory (Azure AD) i en hybrid Azure AD-konfiguration.

  Om du inte kan distribuera en hybrid Azure Active Directory (AD) som ansluter till din lokala AD med Azure AD, rekommenderar vi att du följer vår medföljande vägledning, [aktiverar samhantering för nya Internet-baserade Windows 10-enheter](tutorial-co-manage-new-devices.md).
- Du har befintliga Configuration Manager-klienter som du vill lägga till i molnet.

**I den här självstudien kommer du att:**  
> [!div class="checklist"]
> * Granska krav för Azure och din lokala miljö
> * Konfigurera Hybrid Azure AD  
> * Konfigurera Configuration Manager klient agenter som ska registreras med Azure AD  
> * Konfigurera Intune för att automatiskt registrera enheter  
> * Aktivera samhantering i Configuration Manager  

## <a name="prerequisites"></a>Förutsättningar  

### <a name="azure-services-and-environment"></a>Azure-tjänster och-miljö

- Azure-prenumeration ([kostnads fri utvärderings version](https://azure.microsoft.com/free))
- Azure Active Directory Premium
- Microsoft Intune-prenumeration
  > [!TIP]  
  > En Enterprise Mobility + Security-prenumeration (EMS) inkluderar både Azure Active Directory Premium och Microsoft Intune. EMS-prenumeration ([kostnads fri utvärderings version](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-trial)).  

Om du inte redan finns i din miljö kan du under den här självstudien:

- Konfigurera [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-install-select-installation) mellan din lokala Active Directory och din Azure Active Directory-klient (AD).

> [!TIP]
> Du behöver inte längre köpa och tilldela enskilda Intune-eller EMS-licenser till dina användare. Mer information finns i [vanliga frågor och svar om produkt och licensiering](../core/understand/product-and-licensing-faq.md#bkmk_mem).

### <a name="on-premises-infrastructure"></a>Lokal infrastruktur

- En [version](../core/servers/manage/updates.md#supported-versions) av Configuration Manager aktuella grenen som stöds
- Hanterings auktoriteten för mobila enheter (MDM) måste anges till Intune.  

### <a name="permissions"></a>Behörigheter

I den här självstudien använder du följande behörigheter för att slutföra aktiviteter:

- Ett konto som är en *domän administratör* i din lokala infrastruktur  
- Ett konto som är en *Fullständig administratör* för *alla* scope i Configuration Manager
- Ett konto som är en *Global administratör* i Azure Active Directory (Azure AD)
   - Se till att du har tilldelat en Intune-licens till det konto som du använder för att logga in på din klient organisation. Annars Miss lyckas inloggningen med fel meddelandet "användaren känns inte igen". <!--mem issue 169-->

## <a name="set-up-hybrid-azure-ad"></a>Konfigurera Hybrid Azure AD

När du konfigurerar en hybrid Azure AD konfigurerar du verkligen integrering av en lokal AD med Azure AD med hjälp av Azure AD Connect och Active Directory federerade tjänster (ADFS). Med lyckad konfiguration kan dina arbetare sömlöst logga in på externa system med sina lokala AD-autentiseringsuppgifter.

> [!IMPORTANT]  
> I den här självstudien lär du dig hur du konfigurerar hybrid Azure AD för en hanterad domän. Vi rekommenderar att du är bekant med processen och inte förlitar dig på den här självstudien som vägledning för att förstå och distribuera hybrid Azure AD.
>
> Om du vill ha mer information om hybrid Azure AD börjar du med följande artiklar i Azure Active Directory-dokumentationen:
>
> - [Planera implementeringen av Azure AD-anslutningen](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)
> - [Planera implementering av Azure AD-anslutningshybriden](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)
> - [Kontrollera Azure AD-anslutningshybriden för dina enheter](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-control)
> - [Konfigurera Azure AD-anslutningshybrid för federerade domäner](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-federated-domains)  

### <a name="set-up-azure-ad-connect"></a>Konfigurera Azure AD Connect

För Azure AD krävs konfiguration av Azure AD Connect för att se till att dator konton i din lokala Active Directory (AD) och enhetsobjektet i Azure AD synkroniseras.

Från och med version 1.1.819.0 tillhandahåller Azure AD Connect en guide för konfiguration av Hybrid Azure AD-anslutning. Genom att använda den här guiden under lättas konfigurations processen.  

Om du vill konfigurera Azure AD Connect behöver du autentiseringsuppgifterna för en global administratör för Azure AD.  

> [!TIP]  
> Följande procedur bör inte betraktas som auktoritativ för installation av Azure AD Connect, men tillhandahålls här för att effektivisera konfigurationen av samhantering mellan Intune och Configuration Manager. Information om det auktoritativa innehållet på denna och relaterade procedurer för konfiguration av Azure AD finns i [Konfigurera hybrid Azure AD-anslutning för hanterade domäner](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains) i Azure AD-dokumentationen.  

#### <a name="configure-a-hybrid-azure-ad-join-using-azure-ad-connect"></a>Konfigurera en hybrid Azure AD-anslutning med hjälp av Azure AD Connect

1. Hämta och installera den [senaste versionen av Azure AD Connect](https://www.microsoft.com/download/details.aspx?id=47594) (1.1.819.0 eller högre).  
2. Starta Azure AD Connect och välj sedan **Konfigurera**.
3. På sidan **Ytterligare aktiviteter** väljer du **Konfigurera enhets alternativ**och väljer sedan **Nästa**.
4. På sidan **Översikt** väljer du **Nästa**.
5. På sidan **Anslut till Azure AD** anger du autentiseringsuppgifterna för en global administratör för Azure AD.
6. På sidan **enhets alternativ** väljer du **Konfigurera hybrid Azure AD-anslutning**och väljer sedan **Nästa**.
7. På sidan **enhets operativ system** väljer du de operativ system som används av enheter i Active Directorys miljön och väljer sedan **Nästa**.  

   Du kan välja alternativet för att stöda domänanslutna Windows-enheter med äldre versioner, men tänk på att samhantering av enheter bara stöds för Windows 10.
8. På sidan **SCP** , för varje lokal skog som du vill Azure AD Connect konfigurera tjänst anslutnings punkten (SCP), utför följande steg och välj sedan **Nästa**:  
   1. Välj skogen.  
   2. Välj autentiseringstjänst.  Om du har en federerad domän väljer du AD FS server om inte din organisation har enbart Windows 10-klienter och du har konfigurerat synkronisering av dator/enhet eller om din organisation använder [SeamlessSSO](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso).  
   3. Klicka på **Lägg till** för att ange autentiseringsuppgifter för företagsadministratör.  
9. Hoppa över det här steget om du har en hanterad domän.  

   På sidan **Federations konfiguration** anger du autentiseringsuppgifterna för AD FS administratör och väljer sedan **Nästa**.
10. På sidan **klar att konfigurera** väljer du **Konfigurera**.
11. På sidan **konfigurationen har slutförts** väljer du **Avsluta**.

Om du får problem med att slutföra hybrid Azure AD-anslutning för domänanslutna Windows-enheter läser du [Felsöka hybrid Azure AD-anslutning för aktuella Windows-enheter](https://docs.microsoft.com/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current).

## <a name="configure-client-settings-to-direct-clients-to-register-with-azure-ad"></a>Konfigurera klient inställningar för att dirigera klienter att registrera med Azure AD

Använd klient inställningar för att konfigurera Configuration Manager klienterna automatiskt ska registreras med Azure AD.  

1. Öppna klient inställningarna för administration av **Configuration Manager konsol**  >  **Administration**  >  **Overview**  >  **Client Settings**och redigera sedan **standard klient inställningarna**.  

2. Välj **Cloud Services**.  

3. På sidan **standardinställningar** ställer du in **automatisk registrering av nya Windows 10-domänanslutna enheter med Azure Active Directory** till = **Ja**.  

4. Spara konfigurationen genom att välja **OK**.  

## <a name="configure-auto-enrollment-of-devices-to-intune"></a>Konfigurera automatisk registrering av enheter till Intune

Nu ska vi konfigurera automatisk registrering av enheter med Intune. Med automatisk registrering kan enheter som du hanterar med Configuration Manager registreras automatiskt med Intune.

Med automatisk registrering kan användarna registrera sina Windows 10-enheter till Intune. Enheter registreras när en användare lägger till sitt arbets konto till sin personligt ägda enhet eller när en företagsägda enhet är ansluten till Azure Active Directory.  

1. Logga in på [Azure Portal](https://portal.azure.com/) och välj **Azure Active Directory**  >  **Mobility (MDM och MAM)**  >  **Microsoft Intune**.  

2. Konfigurera **användar omfång i MDM**. Ange något av följande för att konfigurera vilka användares enheter som hanteras av Microsoft Intune och acceptera standardvärdena för URL-värden.  

   - **Några**: Välj de **grupper** som automatiskt kan registrera sina Windows 10-enheter  

   - **Alla**: alla användare kan registrera sina Windows 10-enheter automatiskt

   - **Ingen**: inaktivera automatisk registrering i MDM

   > [!IMPORTANT]  
   > Om både **MAM-användaromfattning** och automatisk MDM-registrering (**MDM-användaromfattning**) är aktiverat för en grupp så är endast MAM aktiverat. Endast hantering av mobil program (MAM) läggs till för användare i gruppen när de ansluter till en personlig enhet. Enheterna är inte automatiskt MDM-registrerade.  

3. Välj **Spara** för att slutföra konfigurationen av automatisk registrering.  

4. Gå tillbaka till **Mobility (MDM och MAM)** och välj sedan **Microsoft Intune registrering**.  

    > [!NOTE]
    > Vissa klienter kanske inte har dessa alternativ för att konfigurera.<!-- SCCMDocs#1230 -->
    >
    > **Microsoft Intune** hur du konfigurerar MDM-appen för Azure AD. **Microsoft Intune registreringen** är en särskild Azure AD-app som skapas när du tillämpar Multi-Factor Authentication-principer för iOS-och Android-registrering. Mer information finns i [Kräv Multi-Factor Authentication för enhets registrering i Intune](https://docs.microsoft.com/intune/enrollment/multi-factor-authentication).

5. För MDM-användar omfång väljer du **alla**och sedan **Spara**.  

## <a name="enable-co-management-in-configuration-manager"></a>Aktivera samhantering i Configuration Manager

Med hybrid Azure AD-konfiguration och Configuration Manager-klientkonfigurationer på plats är du redo att vända växeln och aktivera samhantering av dina Windows 10-enheter.  

> [!TIP]
> - När du aktiverar samhantering tilldelar du en samling som en *pilot grupp*. Det här är en grupp som innehåller ett litet antal klienter för att testa konfigurationerna för samhantering. Vi rekommenderar att du skapar en lämplig samling innan du påbörjar proceduren. Sedan kan du välja samlingen utan att avsluta proceduren.
> - Från och med Configuration Manager version 1906 kan du behöva flera samlingar eftersom du kan tilldela en annan *pilot grupp* för varje arbets belastning.

### <a name="enable-co-management-starting-in-version-1906"></a>Aktivera samtidig hantering från och med version 1906

[!INCLUDE [Enable Co-management in version 1906 and later](includes/enable-co-management-1906-and-higher.md)]

### <a name="enable-co-management-in-version-1902-and-earlier"></a>Aktivera samhantering i version 1902 och tidigare

[!INCLUDE [Enable Co-management in version 1902 and earlier](includes/enable-co-management-1902-and-earlier.md)]

## <a name="next-steps"></a>Nästa steg

- Granska statusen för samhanterade enheter med [instrument panelen för samhantering](how-to-monitor.md)
- Börja få [omedelbar värde](quickstarts.md#immediate-value) från samhantering
- Använd [villkorlig åtkomst](quickstart-conditional-access.md) och Intune-efterlevnadsprinciper för att hantera användar åtkomst till företags resurser
