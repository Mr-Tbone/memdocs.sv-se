---
title: Tilldela licenser för Microsoft Intune
description: Tilldela licenser till användare så att de kan registrera sig i Intune
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 12/12/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: bb4314ea-88b5-44d3-92ce-4c6aff0587a4
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: d770ee040044cdaee9e4a717e9ee3045874952b2
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88906913"
---
# <a name="assign-licenses-to-users-so-they-can-enroll-devices-in-intune"></a>Tilldela licenser till användare så att de kan registrera enheter i Intune

Oavsett om du lägger till användare manuellt eller synkroniserar från din lokala Active Directory, så måste du först tilldela varje användare en Intune-licens innan de kan registrera sina enheter i Intune. En lista över licenser finns i [Licenser som inkluderar Intune](licenses.md).

> [!NOTE]
> Användare som har tilldelats en Intune-appskyddsprincip och inte registrerar sina enheter i Microsoft Intune måste också ha en Intune-licens för att ta emot principer.

## <a name="assign-an-intune-license-microsoft-endpoint-manager-admin-center"></a>Tilldela en Intune-licens i administrationscentret för Microsoft Endpoint Manager

Du kan använda [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) för att manuellt lägga till molnbaserade användare och tilldela licenser till både molnbaserade användarkonton och konton som synkroniseras från din lokala Active Directory till Azure AD.

1. I [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) väljer du **Användare** > **Alla användare** > välj användaren > **Licenser** > **Tilldelningar**.

2. Markera kryssrutan för **Intune** > **Spara**. Om du vill använda Enterprise Mobility + Security E5 eller någon annan licens markerar du den rutan i stället.

   ![Skärmbild av Administrationscenter för Microsoft 365, avsnittet Produktlicenser.](./media/licenses-assign/mem-assign-license.png)

3. Användarkontot har nu de behörigheter som krävs för att använda tjänsten och registrera enheter för hantering.

> [!NOTE]
> Användarna visas bara i den klassiska Intune-portalen efter att de har registrerat en enhet med hjälp av Intune PC-klienten. Du kan också välja en grupp användare som redigeras samtidigt, genom att välja att lägga till eller ersätta en licens för alla markerade användare.

## <a name="assign-an-intune-license-by-using-azure-active-directory"></a>Tilldela en Intune-licens genom att använda Azure Active Directory

Du kan också tilldela Intune-licenser till användare med hjälp av Azure Active Directory. Mer information finns i [artikeln Licensiera användare i Azure Active Directory](/azure/active-directory/active-directory-licensing-group-assignment-azure-portal). 

## <a name="use-school-data-sync-to-assign-licenses-to-users-in-intune-for-education"></a>Använd synkronisering av skolinformation för att tilldela användare licenser till Intune for Education

Om du representerar en utbildningsorganisation kan du använda synkronisering av skolinformation (SDS) för att tilldela Intune for Education-licenser till synkroniserade användare. Markera bara kryssrutan Intune for Education när du konfigurerar din SDS-profil.  

![Skärmbild av SDS-profilinställningen](./media/licenses-assign/i4e-sds-profile-setup-setting.png)

Kontrollera att Intune A Direct-licensen också tilldelas när du tilldelar en Intune for Education-licens.

![Skärmbild av konfiguration av produktlicens](./media/licenses-assign/i4e-set-licenses.png)

Se den här [översikten över synkronisering av skolinformation](https://support.office.com/article/Overview-of-School-Data-Sync-and-Classroom-f3d1147b-4ade-4905-8518-508e729f2e91) om du vill veta mer om SDS.

## <a name="how-user-and-device-licenses-affect-access-to-services"></a>Hur användar- och enhetslicenser påverkar åtkomsten till tjänster

* Varje **användare** du tilldelar en användarprogramlicens till har åtkomst till och kan använda onlinetjänsterna och tillhörande programvara (inklusive System Center-program) för att hantera program och upp till 15 MDM-enheter. Intune PC-agenten tillåter 5 fysiska och 1 virtuell dator per användarlicens.
* Du kan köpa licenser för enheter separat från användarlicenser. Enhetslicenser behöver inte tilldelas till enheterna. Varje enhet som har åtkomst till och använder onlinetjänster och relaterad programvara (som System Center-program) måste ha en enhetslicens.
* Om en enhet används av mer än en användare så krävs det en programvarulicens för var och en, eller så krävs det en programlicens för varje användare.

## <a name="understanding-the-type-of-licenses-you-have-purchased"></a>Förstå vilken typ av licenser som du har köpt

Hur du har köpt Intune avgör vilken prenumerationsinformation som visas:

- Om du har köpt Intune med ett Enterprise-avtal, hittar du din prenumerationsinformation i volymlicensportalen under **Prenumerationer**.
- Kontakta din återförsäljare om du har köpt Intune från en leverantör av molnlösningar.
- Om du har köpt Intune med en CC# eller faktura är dina licenser användarbaserade.

## <a name="use-powershell-to-selectively-manage-ems-user-licenses"></a>Använda PowerShell för att hantera EMS-användarlicenser selektivt
Organisationer som använder Microsoft Enterprise Mobility + Security (tidigare Enterprise Mobility Suite) kanske har användare som bara behöver Azure Active Directory Premium eller Intune-tjänster i EMS-paketet. Du kan tilldela en tjänst eller en delmängd tjänster med hjälp av [Azure Active Directory PowerShell-cmdlets](/previous-versions/azure/jj151815(v=azure.100)).

Om du vill tilldela användarlicenser för EMS-tjänster öppnar du PowerShell som administratör på en dator där [Azure Active Directory-modulen för Windows PowerShell](/previous-versions/azure/jj151815(v=azure.100)#bkmk_installmodule) är installerad. Du kan installera PowerShell på en lokal dator eller på en AD FS-server.

Du måste skapa en ny definition av licens-SKU:n som bara gäller önskade tjänstplaner. Det gör du genom att inaktivera planer som du inte vill använda. Du kan till exempel skapa en definition av licens-SKU:n som inte tilldelar en Intune-licens. Om du vill visa en lista över tjänster som är tillgängliga skriver du:

```powershell
(Get-MsolAccountSku | Where {$_.SkuPartNumber -eq "EMS"}).ServiceStatus
```

Du kan köra följande kommando om du vill undanta Intune-tjänstplanen. Du kan använda samma metod om du vill utöka till en hel säkerhetsgrupp eller använda mer detaljerade filter.

**Exempel 1**<br>
Skapa en ny användare på kommandoraden och tilldela en EMS-licens utan att aktivera Intune-delen av licensen:

```powershell
Connect-MsolService

New-MsolUser -DisplayName "Test User" -FirstName FName -LastName LName -UserPrincipalName user@<TenantName>.onmicrosoft.com –Department DName -UsageLocation US

$CustomEMS = New-MsolLicenseOptions -AccountSkuId "<TenantName>:EMS" -DisabledPlans INTUNE_A
Set-MsolUserLicense -UserPrincipalName user@<TenantName>.onmicrosoft.com -AddLicenses <TenantName>:EMS -LicenseOptions $CustomEMS
```

Kontrollera med:

```powershell
(Get-MsolUser -UserPrincipalName "user@<TenantName>.onmicrosoft.com").Licenses.ServiceStatus
```

**Exempel 2**<br>
Inaktivera Intune-delen av EMS-licensen för en användare som redan har tilldelats en licens:

```powershell
Connect-MsolService

$CustomEMS = New-MsolLicenseOptions -AccountSkuId "<TenantName>:EMS" -DisabledPlans INTUNE_A
Set-MsolUserLicense -UserPrincipalName user@<TenantName>.onmicrosoft.com -LicenseOptions $CustomEMS
```

Kontrollera med:

```powershell
(Get-MsolUser -UserPrincipalName "user@<TenantName>.onmicrosoft.com").Licenses.ServiceStatus
```

![PoSH-AddLic-Verify](./media/licenses-assign/posh-addlic-verify.png)