---
title: Övervaka samhantering
titleSuffix: Configuration Manager
description: Använd instrument panelen för samhantering för att granska information om samhanterade enheter.
ms.date: 06/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: how-to
ms.assetid: e83a7b0d-b381-4b4a-8eca-850385abbebb
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: eab91146ec21bbee888d496012419f47bca4b599
ms.sourcegitcommit: 7b2f7918d517005850031f30e705e5a512959c3d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/15/2020
ms.locfileid: "84776981"
---
# <a name="how-to-monitor-co-management-in-configuration-manager"></a>Övervaka samhantering i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

När du har aktiverat samhantering kan du övervaka samhanterings enheter med följande metoder:

- [Instrumentpanel för samhantering](#co-management-dashboard)  

- [Distributions principer](#deployment-policies)

- [WMI-enhets data](#wmi-device-data)

## <a name="co-management-dashboard"></a>Instrumentpanel för samhantering

Den här instrument panelen hjälper dig att granska datorer som är samhanterade i din miljö. Diagrammen kan hjälpa till att identifiera enheter som kan behöva åtgärdas.<!--1356648,1358980-->

I Configuration Manager-konsolen går du till arbets ytan **övervakning** och väljer noden för **samtidig hantering** .

![Skärm bild av instrument panelen för samhantering](media/co-management-dashboard.png)

### <a name="client-os-distribution"></a>Klientens OS-distribution

Visar antalet klient enheter per operativ system efter version. Den använder följande grupperingar:  

- Windows 7 & 8. x
- Windows 10, lägre än 1709  
- Windows 10 1709 och senare  

    > [!Tip]  
    > Windows 10, version 1709 och senare, är en förutsättning för samhantering.  

Hovra över ett diagram avsnitt för att Visa procent andelen enheter i den OS-gruppen.

![Distributions panel för klient operativ system](media/co-management-dashboard/Co-management-OS-distribution-graph.PNG)

### <a name="co-management-status"></a>Status för samhantering

Ett trattdiagram som visar antalet enheter med följande tillstånd från registrerings processen:
  
- Kvalificerade enheter
- Schemalagd  
- Registrering initierad  
- Registrerad  

![Panel för samhanterings status (tratt)](media/co-management-dashboard/1358980-status-funnel.png)

### <a name="co-management-enrollment-status"></a>Registrerings status för samhantering

Visar en uppdelning av enhets status i följande kategorier:

- Lyckades, hybrid Azure AD-ansluten  
- Lyckades, Azure AD-ansluten  
- Registrering, hybrid Azure AD-ansluten  
- Haveri, hybrid Azure AD-ansluten  
- Det gick inte att ansluta till Azure AD  
- Väntande användar inloggning  

    > [!NOTE]
    > Från och med version 1906, för att minska antalet enheter i det här väntande läget, registreras en ny samhanterad enhet nu automatiskt i Microsoft Intune tjänst baserat på dess Azure AD- *enhets* -token. Användaren behöver inte vänta på att en användare loggar in på enheten för automatisk registrering för att starta. För att det ska fungera måste enheten köra Windows 10, version 1803 eller senare.
    >
    > Om enhetens token Miss lyckas går den tillbaka till föregående beteende med användartoken. Sök efter följande post i **ComanagementHandler. log** :`Enrolling device with RegisterDeviceWithManagementUsingAADDeviceCredentials`

Välj ett tillstånd i panelen om du vill gå till en lista över enheter i det aktuella läget.  

![Registrerings status panel för samhantering](media/co-management-dashboard/1358980-enrollment-status.png)

### <a name="workload-transition"></a>Arbets belastnings över gång

Visar ett stapeldiagram med antalet enheter som du har övergått till Microsoft Intune för de tillgängliga arbets belastningarna.

Listan över arbets belastningar varierar efter version av Configuration Manager. Mer information finns i [arbets belastningar som kan överföras till Intune](workloads.md).

Hovra över ett diagram avsnitt om du vill visa antalet enheter som övergår till arbets belastningen.

![Stapeldiagram över arbets belastnings över gångar](media/co-management-dashboard/Workload-Transition.PNG)

### <a name="enrollment-errors"></a>Registreringsfel

Den här tabellen är en lista över registrerings fel från enheter. Felen kan komma från MDM-komponenten i Windows, kärnan i Windows OS eller på den Configuration Manager klienten.

Det finns hundratals möjliga fel. I följande tabell visas de vanligaste felen.
<!-- SCCMDocs issue 1064, BUG 3158555 -->

| Fel | Beskrivning |
|---------|---------|
| 2147549183 (0x8000FFFF) | MDM-registreringen har inte kon figurer ATS ännu på Azure AD eller också förväntas registrerings-URL: en.<br><br>[Aktivera automatisk registrering i Windows 10](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment) |
| 2149056536 (0x80180018)<br>MENROLL_E_USERLICENSE | Licensen för användaren är i ett felaktigt tillstånd som blockerar registreringen<br><br>[Tilldela licenser till användare](https://docs.microsoft.com/intune/licenses-assign) |
| 2149056555 (0x8018002B)<br>MENROLL_E_MDM_NOT_CONFIGURED | Vid försök att automatiskt registrera till Intune, men Azure AD-konfigurationen används inte fullt ut. Det här problemet bör vara tillfälligt när enheten försöker igen efter en kort tid. |
| 2149056554 (0x 8018002A)<br>&nbsp; | Användaren avbröt åtgärden<br><br>Om MDM-registrering kräver Multi-Factor Authentication och användaren inte har loggat in med en andra faktor som stöds, visar Windows ett popup-meddelande till användaren att registrera sig. Om användaren inte svarar på popup-meddelanden uppstår det här felet. Det här problemet bör vara övergående, eftersom Configuration Manager försöker igen och uppmana användaren. Användarna bör använda Multi-Factor Authentication när de loggar in på Windows. Utbilda dem också för att förvänta detta beteende och om du uppmanas att göra det. |
| 2149056532 (0x80180014)<br>MENROLL_E_DEVICENOTSUPPORTED | Hantering av mobila enheter stöds inte. Kontrol lera enhets begränsningar. |
| 2149056533 (0x80180015)<br>MENROLL_E_NOTSUPPORTED | Hantering av mobila enheter stöds inte. Kontrol lera enhets begränsningar. |
| 2149056514 (0x80180002)<br>MENROLL_E_DEVICE_AUTHENTICATION_ERROR | Servern kunde inte autentisera användaren<br><br> Det finns ingen Azure AD-token för användaren. Se till att användaren kan autentisera till Azure AD. |
| 2147942450 (0x 80070032)<br>&nbsp; | Automatisk MDM-registrering stöds bara på Windows-RS3 och senare.<br><br>Kontrol lera att enheten uppfyller [minimi kraven](overview.md#windows-10) för samhantering. |
| 3400073293 | ADAL användar sfär konto svar okänt<br><br>Kontrol lera Azure AD-konfigurationen och se till att användarna kan autentisera sig. |
| 3399548929 | Behöver användar inloggning<br><br>Det här problemet bör vara tillfälligt. Det inträffar när användaren snabbt loggar ut innan registrerings aktiviteten sker. |
| 3400073236 | Begäran om ADAL-säkerhetstoken misslyckades.<br><br>Kontrol lera Azure AD-konfigurationen och se till att användarna kan autentisera sig. |
| 2149122477 | Allmänt HTTP-problem |
| 3400073247 | ADAL-integrerad Windows-autentisering stöds endast i federerade flöden<br><br>[Planera implementeringen av Azure Active Directory-hybridanslutning](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan) |
| 3399942148 | Servern eller proxyn hittades inte.<br><br>Det här problemet bör vara tillfälligt när klienten inte kan kommunicera med molnet. Om den kvarstår kontrollerar du att klienten har en konsekvent anslutning till Azure. | 
| 2149056532 | En speciell plattform eller version stöds inte<br><br>Kontrol lera att enheten uppfyller [minimi kraven](overview.md#windows-10) för samhantering. |
| 2147943568 | Elementet hittades inte<br><br>Det här problemet bör vara tillfälligt. Kontakta Microsoft Support om den kvarstår. |
| 2192179208 | Det finns inte tillräckligt med minnes resurser för att utföra det här kommandot.<br><br>Det här problemet bör vara övergående, det bör lösa sig självt när klienten försöker igen. |
| 3399614467 | ADAL-auktorisering misslyckades för den här kontrollen<br><br>Kontrol lera Azure AD-konfigurationen och se till att användarna kan autentisera sig. |
| 2149056517 | Allmänt fel från hanterings servern, t. ex. DB-åtkomst fel<br><br>Det här problemet bör vara tillfälligt. Kontakta Microsoft Support om den kvarstår. |
| 2149134055 | Okänt WinHTTP-namn<br><br>Klienten kan inte matcha namnet på tjänsten. Kontrol lera DNS-konfigurationen. |
| 2149134050 | Internet-timeout<br><br>Det här problemet bör vara tillfälligt när klienten inte kan kommunicera med molnet. Om den kvarstår kontrollerar du att klienten har en konsekvent anslutning till Azure. |

Mer information finns i [fel värden för MDM-registrering](https://docs.microsoft.com/windows/desktop/mdmreg/mdm-registration-constants).

## <a name="deployment-policies"></a>Distributions principer

Två principer skapas i noden **distributioner** på arbets ytan **övervakning** . En princip är för pilot gruppen och en för produktion. Dessa principer rapporterar bara antalet enheter där Configuration Manager tillämpade principen. De funderar inte på hur många enheter som är registrerade i Intune, vilket är ett krav innan enheterna kan hanteras tillsammans.

Produktions principen (CoMgmtSettingsProd) är riktad till samlingen **alla system** . Det har ett tillämpbart villkor som kontrollerar operativ systemets typ och version. Om klienten är ett server-OS eller inte Windows 10, gäller inte principen och ingen åtgärd vidtas.

## <a name="wmi-device-data"></a>WMI-enhets data

Fråga **SMS_Client_ComanagementState** WMI-klassen i namn området **root\sms\ site_ &lt; SITECODE>** på plats servern. Du kan skapa anpassade samlingar i Configuration Manager, vilket hjälper dig att fastställa statusen för din samhanterings distribution. Mer information om hur du skapar anpassade samlingar finns i [skapa samlingar](../core/clients/manage/collections/create-collections.md).

Följande fält är tillgängliga i WMI-klassen:

- **MachineId**: ett unikt enhets-ID för den Configuration Manager klienten

- **MDMEnrolled**: anger om enheten är MDM-registrerad

- **Auktoritet**: den myndighet som enheten har registrerats för

- **ComgmtPolicyPresent**: anger om den Configuration Manager principen för samtidig hantering finns på klienten. Om **MDMEnrolled** -värdet är är `0` enheten inte samhanterad, oavsett vilken princip för samtidig hantering som finns på klienten.

En enhet hanteras tillsammans när fälten **MDMEnrolled** och **ComgmtPolicyPresent** båda har värdet `1` .
