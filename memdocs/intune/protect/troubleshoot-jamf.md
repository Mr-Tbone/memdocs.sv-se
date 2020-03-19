---
title: Felsöka Jamf Pro-integrering med Microsoft Intune
titleSuffix: Microsoft Intune
description: Förslag på felsökning av några av de vanligaste problemen när du integrerar Jamf Pro för Mac-enheter med Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/02/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 335841a8642429e36c277673fd8a238d486366c9
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79350622"
---
# <a name="troubleshoot-integration-of-jamf-pro-with-microsoft-intune"></a>Felsöka integrering av Jamf Pro med Microsoft Intune

Den här artikeln hjälper Intune-administratörer att förstå och felsöka problem med integrering av Jamf Pro för macOS med Intune.

> [!TIP]  
> Mycket av informationen i den här artikeln publicerades ursprungligen i artikeln [Troubleshoot problems when you integrate Jamf with Microsoft Intune](https://support.microsoft.com/help/4519171/troubleshoot-problems-when-integrating-jamf-with-microsoft-intune) (Felsöka problem när du integrerar Jamf med Microsoft Intune) på support.microsoft.com.

## <a name="prerequisites"></a>Krav

Innan du påbörjar felsökningen bör du samla in viss grundläggande information som klargör problemet och minskar tiden för att hitta en lösning. Om du till exempel stöter på ett problem som rör integrering av Jamf med Intune ska du alltid kontrollera att alla krav har uppfyllts. Läs igenom följande överväganden innan du påbörjar felsökningen:

- Läs kraven från [Integrera Jamf Pro med Intune](conditional-access-integrate-jamf.md#prerequisites).
- Alla användare måste ha licenser för Microsoft Intune och Microsoft AAD Premium P1 
- Du måste ha ett användarkonto som har Microsoft Intune-integreringsbehörighet i Jamf Pro-konsolen.
- Du måste ha ett användarkonto som behörighet för global administratör i Azure.


Överväg följande information när du undersöker Jamf Pro-integrering med Intune: 
- Vilket är det exakta felmeddelandet?
- Var finns felmeddelandet?
- När började problemet?  Har Jamf Pro-integrering med Intune någonsin fungerat?
- Hur många användare påverkas? Påverkas alla användare eller bara vissa av dem?
- Hur många enheter påverkas? Påverkas alla enheter eller bara vissa av dem?
 

## <a name="common-problems"></a>Vanliga problem 

Följande information kan hjälpa dig att identifiera och lösa vanliga problem för enheter när du har konfigurerat integreringen mellan Intune och Jamf Pro.  

| Problem   | Mer information                  |
|-----------------|--------------------------|
| **Enheter markeras som icke-kommunikativa i Jamf Pro**  | [Enheter misslyckas med att checka in med Jamf Pro eller Azure AD](#devices-are-marked-as-unresponsive-in-jamf-pro) |
| **Mac-enheter frågar efter inloggning med nyckelring när du öppnar en app Enheter misslyckas med registrering**  | [Användarna uppmanas att ange sitt lösenord för att tillåta att appar registreras med Azure AD](#mac-devices-prompt-for-keychain-sign-in-when-you-open-an-app). |
| **Enheter misslyckas med registrering**  | Följande orsaker kan vara aktuella: <br> **-** [***Orsak 1*** – Jamf Pro-appen i Azure har fel behörigheter](#cause-1) <br> **-** [***Orsak 2*** – det finns ett problem med det *inbyggda Jamf-anslutningsprogrammet för macOS* i Azure AD](#cause-2) <br> **-** [***Orsak 3*** – användaren har ingen giltig Intune- eller Jamf-licens](#cause-3) <br> **-** [***Orsak 4*** – användaren använde inte Jamf Self Service för att starta företagsportalappen](#cause-4) <br> **-** [***Orsak 5*** – Intune-integreringen är inaktiverad](#cause-5) <br> **-** [***Orsak 6*** – enheten var tidigare registrerad i Intune, eller så har användaren försökt registrera enheten flera gånger](#cause-6) <br> **-** [***Orsak 7*** – JamfAAD begär åtkomst till en "Microsoft Workplace Join Key" (anslutningsnyckel för Microsoft Workplace) från användarnas nyckelring](#cause-7) |
|  **Mac-enheten visar att den följer standard i Intune men inte följer standard i Azure** | [Problem med enhetsregistreringen](#mac-device-shows-compliant-in-intune-but-noncompliant-in-azure) |
| **Dubbla poster visas i Intune-konsolen för Mac-enheter som registrerats med hjälp av Jamf** | [Flera registreringar från samma enhet](#duplicate-entries-appear-in-the-intune-console-for-mac-devices-enrolled-by-using-jamf) |
| **Efterlevnadsprincipen kan inte utvärdera enheten** | [Principen riktar in sig på enhetsgrupper](#compliance-policy-fails-to-evaluate-the-device) |
| **Det gick inte att hämta åtkomsttoken för Microsoft Graph API** | Följande orsaker kan vara aktuella: <br> -[Behörigheter för Jamf Pro-appen i Azure](#theres-a-permission-issue-with-the-jamf-pro-application-in-azure) <br> - [Utgången licens för Jamf eller Intune](#a-license-required-for-jamf-intune-integration-has-expired) <br> **-** [Portarna är inte öppna](#the-required-ports-arent-open-on-your-network)|
 

### <a name="devices-are-marked-as-unresponsive-in-jamf-pro"></a>Enheter markeras som icke-kommunikativa i Jamf Pro  

**Orsak**: Följande är vanliga orsaker till att enheter markeras som *icke-kommunikativa* av Jamf Pro:

- Enheten misslyckas med att checka in med Jamf Pro.  
  Jamf Pro förväntar sig att enheter ska checka in var 15:e minut. Enheter markeras som icke-kommunikativa av Jamf när de misslyckas med att checka in under en period på 24 timmar.  

- Enheten misslyckas med att checka in med Azure AD.  
  Med en lyckad registrering till Azure AD får macOS-enheter en Azure-token:
  - Denna token uppdateras var 12:e timme.   
  - När tokenuppdateringen misslyckas i 24 timmar eller mer markerar Jamf Pro enheten som icke-kommunikativ.  
  - Om Azure-token upphör att gälla uppmanas användarna att logga in på Azure för att få en ny token. En uppdateringstoken för Azure-åtkomst genereras var sjunde dag.

**Lösning**  
När en enhet har markerats som *icke-kommunikativ* av Jamf Pro måste enhetens registrerade användare logga in för att korrigera det icke-kommunikativa tillståndet. Det måste vara den användare som anslöt kontot via arbetet, eftersom den användaren har identiteten från Intune i sin nyckelring för inloggning.



### <a name="mac-devices-prompt-for-keychain-sign-in-when-you-open-an-app"></a>Mac-enheter frågar efter inloggning med nyckelring när du öppnar en app  

När du har konfigurerat integrering mellan Intune och Jamf Pro och distribuerat principer för villkorsstyrd åtkomst får användare av enheter som hanteras med Jamf Pro ett meddelande om lösenord när de öppnar Microsoft Office 365-program, till exempel Teams, Outlook och andra appar som kräver Azure AD-autentisering. 

Till exempel visas ett meddelande med text som liknar följande exempel när Microsoft Teams öppnas:

``` 
  Microsoft Teams wants to sign using key “Microsoft Workplace Join Key” in your keychain.  
  To allow this, enter the “login” keychain password 
```

**Orsak**: Dessa meddelanden genereras av Jamf Pro för varje tillämplig app som kräver Azure AD-registrering. 

**Lösning**   
I meddelandet måste användaren ange enhetens lösenord för att logga in på Azure AD. Alternativen är:
- **Neka** – logga inte in och använd inte appen.
- **Tillåt** – en engångsinloggning. Nästa gång appen öppnas uppmanar den om inloggning igen.
- **Tillåt alltid** – inloggningsinformationen cachelagras för programmet. Nästa gång appen öppnas uppmanar den inte om inloggning.  

Om du väljer *Tillåt alltid* för en app godkänns bara den appen för framtida inloggning. Ytterligare appar frågar efter autentisering tills de också anges till *Tillåt alltid*. Cachelagrade autentiseringsuppgifter för en app kan inte användas av en annan app.  

### <a name="devices-fail-to-register"></a>Enheter misslyckas med registrering  

Det finns flera vanliga orsaker till att Mac-enheter inte lyckas registrera.  

#### <a name="cause-1"></a>Orsak 1  

**Jamf Pro-företagsprogrammet i Azure har fel behörighet eller har fler än en behörighet**  

  När du skapar appen i Azure måste du ta bort alla standardmässiga API-behörigheter och sedan tilldela Intune en enda behörighet för *update_device_attributes*. 

  **Lösning**  
  Gå igenom och korrigera vid behov behörigheterna för den Jamf-app som du skapade i Azure AD. Se proceduren för att [skapa ett program för Jamf i Azure AD](conditional-access-integrate-jamf.md#create-an-application-in-azure-active-directory). 

#### <a name="cause-2"></a>Orsak 2  

**Det **inbyggda Jamf-anslutningsprogrammet för macOS** skapades inte i din Azure AD-klientorganisation, eller så signerades medgivandet för anslutningsprogrammet av ett konto som inte har behörigheter som global administratör**  

  **Lösning**  
  Se avsnittet *Configuring macOS Intune Integration* (Konfigurera macOS-Intine-integrering) i [Integrating with Microsoft Intune](https://docs.jamf.com/10.13.0/jamf-pro/administrator-guide/Integrating_with_Microsoft_Intune.html) (Integrera med Microsoft Intune) på docs.jamf.com. 

#### <a name="cause-3"></a>Orsak 3

**Användaren har ingen giltig Intune- eller Jamf-licens**  

  Om det saknas en giltig licens kan följande fel uppstå, vilket anger att Jamf-licensen har upphört:  
  ```
    Unable to connect to Microsoft Intune.  
    
    Check your Microsoft Intune Integration configuration.
  ```  

  **Lösning**
  - Jamf-licens: Kontakta Jamf för att få hjälp med att skaffa en ny licens för Jamf.  
  - Intune-licens: Tilldela användaren en giltig licens eller kontakta Microsoft eller din partner för att få information om hur du skaffar en aktuell licens.

#### <a name="cause-4"></a>Orsak 4  

**Användaren använde inte *Jamf Self Service* för att starta företagsportalappen**

För att en enhet ska kunna registreras med Intune via Jamf måste användaren använda Jamf Self service för att öppna Intune-företagsportalen. Om användaren öppnar företagsportalen manuellt registreras enheten utan anslutningen till Jamf.  

Du avgör vilken tjänst enheten använde för att registrera genom att titta i företagsportalappen på enheten. När den har registrerats via Jamf bör du få ett meddelande om att öppna Self-Service-appen och göra ändringar.

I företagsportalappen ser användaren kanske **`Not registered`** , och en post som liknar följande exempel visas kanske i Företagsportal-loggarna:  

```
   Line 7783: <DATE> <IP ADDRESS> INFO com.microsoft.ssp.application TID=1  
 
   WelcomeViewController.swift: 253 (startLogin()) Portal launched without WPJ only arg while account is under partner management
```

**Lösning**  
Så här ändrar du registreringskällan från Intune till Jamf:
1. [Avregistrera din macOS-enhet från Intune](https://docs.microsoft.com/user-help/unenroll-your-device-from-intune-macos). Undvik fler komplikationer för enheter som inte har tagits bort helt från Intune genom att läsa [*Orsak 6*](#cause-6) i den här listan över orsaker.  

2. På enheten använder du Jamf Self service för att öppna företagsportalappen och registrerar sedan enheten med Intune. Den här uppgiften kräver att du har [använt Jamf för att distribuera företagsportalappen för macOS](conditional-access-assign-jamf.md#deploy-the-company-portal-app-for-macos-in-jamf-pro) och har [skapat en princip i Jamf Pro som registrerar användarnas enheter med Azure AD](conditional-access-assign-jamf.md#create-a-policy-in-jamf-pro-to-have-users-register-their-devices-with-azure-active-directory).  

3. När portalen öppnas uppmanas du på den första skärmen att logga in. Använda ditt arbets- eller skolkonto  

4. Företagsportalen bekräftar kontoinformationen och visar statusen för Enhetsregistrering och Enhetsefterlevnad. Gula trianglar markerar de åtgärder du måste utföra för att skydda din macOS-enhet för skolan eller arbetet. Klicka på Börja för att starta registreringen.  

5. Om du uppmanas att göra det anger du datorns inloggningsinformation.  
     
Det kan ta några minuter att registrera enheten i hantering. Du kan göra andra saker på enheten under tiden. Du får ett meddelande när du har slutfört konfigurationen av företagsåtkomst så att du vet att du är färdig.

#### <a name="cause-5"></a>Orsak 5  

**Intune-integreringen är inaktiverad**

Om Intune-integreringen är inaktiverad får användarna ett popup-fönster i företagsportalen med följande meddelande när de försöker registrera en enhet:  

```
   Invalid command line input
   
   Registration-only command line flag (-r) can only be used when partner management is enabled in Intune. Please contact your IT admin.
```  

Jamf Pro-servern skickar en puls till Intune-servrarna när integreringen är avstängd, som talar om för Intune att integrationen är inaktiverad. 

**Lösning**  
Återaktivera Intune-integrering i Jamf Pro. Se [Konfigurera Microsoft Intune-integrering i Jamf Pro](conditional-access-integrate-jamf.md#enable-intune-to-integrate-with-jamf-pro).


#### <a name="cause-6"></a>Orsak 6  

**Enheten var tidigare registrerad i Intune, eller så har användaren försökt registrera enheten flera gånger**

Om en enhet avregistreras från Jamf men inte tas bort korrekt från Intune, eller om flera registreringsförsök görs, ser du kanske flera instanser av samma enhet i portalen. Detta gör att Jamf-registreringen misslyckas.

**Lösning**  
1. På Mac-enheten startar du **Terminal**.
2. Kör **sudo JAMF removemdmprofile**.
3. Kör **sudo JAMF removeFramework**.
4. På JAMF Pro-servern tar du bort datorns inventeringspost.
5. Ta bort enheten från Azure AD.
6. Ta bort följande filer på enheten om de finns:
   - /Library/Application Support/com.microsoft.CompanyPortal.usercontext.info
   - /Library/Application Support/com.microsoft.CompanyPortal
   - /Library/Application Support/com.jamfsoftware.selfservice.mac
   - /Library/Saved Application
   - State/com.jamfsoftware.selfservice.mac.savedState
   - /Library/Saved Application State/com.microsoft.CompanyPortal.savedState
   - /Library/Preferences/com.microsoft.CompanyPortal.plist
   - /Library/Preferences/com.jamfsoftware.selfservice.mac.plist
   - /Library/Preferences/com.jamfsoftware.management.jamfAAD.plist
   - /Users/<username>/Library/Cookies/com.microsoft.CompanyPortal.binarycookies
   - /Users/<username>/Library/Cookies/com.jamf.management.jamfAAD.binarycookies
   - com.microsoft.CompanyPortal
   - com.microsoft.CompanyPortal.HockeySDK
   - enterpriseregistration.windows.net
   - https://device.login.microsoftonline.com
   - https://device.login.microsoftonline.com/
   - Transportnyckel för Microsoft-session (offentliga OCH privata nycklar)
   - Microsoft Workplace Join-nyckel (offentliga OCH privata nycklar)
7. Ta bort allt från nyckelringen på den enhet som refererar till *Microsoft*, *Intune* eller *Företagsportal*, inklusive certifikat för DeviceLogin.microsoft.com. Ta bort *JAMF*-referenser förutom offentliga och privata JAMF-nycklar. 
   > [!IMPORTANT]  
   > Om du tar bort den offentliga och den privata nyckeln slutar enhetsregistreringen att fungera.

8. Ta bort alla av följande poster som du hittar:  
   - Variant: Programlösenord; Konto: com.microsoft.workplacejoin.thumbprint
   - Variant: Programlösenord; Konto: com.microsoft.workplacejoin.registeredUserPrincipalName
   - Variant: Certifikat; Utfärdat av: MS-Organization-Access
   - Variant: Identitetspreferens ; Namn (ADFS STS URL om sådan finns): https://adfs\<DNSName>.com/adfs/ls
   - Variant: Identitetspreferens ; Namn: https://enterpriseregistration.windows.net
   - Variant: Identitetspreferens ; Namn: https://enterpriseregistration.windows.net/  
9. Starta om Mac-enheten.
10. Avinstallera Företagsportal från enheten.
11. Gå till portal.manage.microsoft.com och ta bort alla instanser av Mac-enheten. Vänta minst 30 minuter innan du går vidare till nästa steg.
12. Omregistrera enheten i JAMF Pro.
13. Öppna Self Service igen och starta Registreringsprincip.


#### <a name="cause-7"></a>Orsak 7  

**JamfAAD begär åtkomst till en "Microsoft Workplace Join Key" (anslutningsnyckel för Microsoft Workplace) från användarnas nyckelring**

Under registreringen får användaren av en macOS-enhet följande fråga om att ge JamfAAD åtkomst till en nyckel från nyckelringen: 

```
   JamfAAD wants to access key “Microsoft Workplace Join Key" in your keychain. 
    
   To allow this, enter the “login” keychain password
```

**Lösning**  
För att enheten ska kunna registreras med Azure AD kräver Jamf att användaren anger sitt kontolösenord och väljer **Tillåt**.

Den här begäran liknar begäran för [Mac-enheter frågar efter inloggning med nyckelring när du öppnar en app](#mac-devices-prompt-for-keychain-sign-in-when-you-open-an-app) tidigare i den här artikeln.  

 
### <a name="mac-device-shows-compliant-in-intune-but-noncompliant-in-azure"></a>Mac-enheten visar att den följer standard i Intune men inte följer standard i Azure  

**Orsak**: Följande faktorer kan göra att en enhet visar att den följer standard i Intune men inte i Azure:  
- Enheten är inte korrekt registrerad.  
- Enheten registrerades flera gånger utan nödvändig rensning.

**Lösning**  
Lös problemet genom att följa lösningen för [*Orsak 6*](#cause-6) för *Enheter misslyckas med registrering* tidigare i den här artikeln. 


### <a name="duplicate-entries-appear-in-the-intune-console-for-mac-devices-enrolled-by-using-jamf"></a>Dubbla poster visas i Intune-konsolen för Mac-enheter som registrerats med hjälp av Jamf  
 
**Orsak**: En enhet registreras med Intune flera gånger och omregistreras vanligtvis när den har tagits bort från Intune.  

När en enhet tas bort från Intune- och Jamf Pro-integrering kan vissa data lämnas kvar, vilket kan göra att efterföljande registreringar skapar dubblettposter.  

**Lösning**  
Lös problemet genom att följa lösningen för [*Orsak 6*](#cause-6) för *Enheter misslyckas med registrering* tidigare i den här artikeln. 

### <a name="compliance-policy-fails-to-evaluate-the-device"></a>Efterlevnadsprincipen kan inte utvärdera enheten  

**Orsak**: Jamf-integreringen med Intune stöder inte efterlevnadsprinciper som tillämpas på enhetsgrupper. 

**Lösning**  
Ändra efterlevnadsprincip för macOS-enheter som ska tilldelas till användargrupper. 


### <a name="could-not-retrieve-the-access-token-for-microsoft-graph-api"></a>Det gick inte att hämta åtkomsttoken för Microsoft Graph API

Du får följande fel:

```
   Could not retrieve the access token for Microsoft Graph API. Check the configuration for Microsoft Intune Integration.
```   

Källan till det här felet kan vara en av följande orsaker: 

#### <a name="theres-a-permission-issue-with-the-jamf-pro-application-in-azure"></a>Det finns ett behörighetsproblem med Jamf Pro-programmet i Azure

När Jamf Pro-appen registreras i Azure skedde något av följande:  
- Appen mottog fler än en behörighet.
- Alternativet **Bevilja administratörsgodkännande för *\<ditt företag>*** valdes inte.  

**Lösning**  
Se lösningen på Orsak 1 för [Enheter misslyckas med registrering](#devices-fail-to-register) tidigare i den här artikeln.

#### <a name="a-license-required-for-jamf-intune-integration-has-expired"></a>En licens som krävs för Jamf-Intune-integrering har upphört

**Lösning**: Se lösningen på Orsak 3 för [Enheter misslyckas med registrering](#devices-fail-to-register). 

#### <a name="the-required-ports-arent-open-on-your-network"></a>De portar som krävs är inte öppna i ditt nätverk

**Lösning**: Läs informationen om nätverksportar i [Krav](conditional-access-integrate-jamf.md#prerequisites) för integrering av Jamf Pro med Intune.


## <a name="next-steps"></a>Nästa steg
Läs mer om hur du [integrerar Jamf Pro med Intune](conditional-access-integrate-jamf.md)