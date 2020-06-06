---
title: Samhantera Internet-baserade enheter
titleSuffix: Configuration Manager
description: Lär dig hur du förbereder dina Windows 10 Internet-baserade enheter för samhantering.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 05/14/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.assetid: 101de2ba-9b4d-4890-b087-5d518a4aa624
ms.openlocfilehash: 66e6156466d0432aaa8b3b162263f8207bdc9d78
ms.sourcegitcommit: 0b30c8eb2f5ec2d60661a5e6055fdca8705b4e36
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/05/2020
ms.locfileid: "84455114"
---
# <a name="how-to-prepare-internet-based-devices-for-co-management"></a>Förbereda Internet-baserade enheter för samhantering

Den här artikeln fokuserar på den andra sökvägen till samhantering, för nya Internetbaserade enheter. Det här scenariot är när du har nya Windows 10-enheter som ansluter till Azure AD och automatiskt registreras i Intune. Du installerar Configuration Manager klienten för att uppnå ett samhanterings tillstånd.  

## <a name="windows-autopilot"></a>Windows Autopilot

För nya Windows 10-enheter kan du använda autopilot-tjänsten för att konfigurera OOBE (out of Box Experience). Den här processen omfattar att ansluta enheten till Azure AD och registrera enheten i Intune.  

Mer information finns i [Översikt över Windows autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot).

Om du vill konfigurera enheterna så att de registreras automatiskt i Intune när de ansluter till Azure AD, se [registrera Windows-enheter för Microsoft Intune](https://docs.microsoft.com/intune/windows-enroll).  

### <a name="gather-information-from-configuration-manager"></a>Samla in information från Configuration Manager

Använd Configuration Manager för att samla in och rapportera enhets informationen som krävs av Intune. Den här informationen omfattar enhetens serie nummer, Windows produkt identifierare och en maskin varu identifierare. Den används för att registrera enheten i Intune för att stödja Windows autopilot.

1. I Configuration Manager-konsolen går du till arbets ytan **övervakning** , expanderar noden **rapportering** , expanderar **rapporter**och väljer **maskin vara-allmänt-** noden.  

2. Kör rapporten, **Windows autopilot-enhets information**och visa resultatet.  

3. I rapport visnings programmet väljer du **export** ikonen och väljer alternativet **CSV (kommaavgränsad)** .  

4. När du har sparat filen laddar du upp data till Intune.  

Mer information finns i [lägga till enheter i Intune](https://docs.microsoft.com/intune/enrollment-autopilot#add-devices).

### <a name="autopilot-for-existing-devices"></a>Autopilot för befintliga enheter
<!--1358333-->

[Windows autopilot för befintliga enheter](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) är tillgängligt i Windows 10, version 1809 eller senare. Med den här funktionen kan du återställa avbildningen och etablera en Windows 7-enhet för [Windows autopilot-](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) användarläge med hjälp av en enda, inbyggd Configuration Manager-aktivitetssekvens.

Mer information finns i [aktivitetssekvens för Windows autopilot för befintliga enheter](../osd/deploy-use/windows-autopilot-for-existing-devices.md).

## <a name="install-the-configuration-manager-client"></a>Installera Configuration Manager-klienten

För Internetbaserade enheter i den andra sökvägen måste du skapa en app i Intune. Distribuera den här appen till Windows 10-enheter som inte redan Configuration Manager-klienter.

> [!NOTE]
> Innan du tilldelar den här appen till enheter i Intune måste du kontrol lera att enheterna litar på CMG för certifikat för serverautentisering. Mer information finns i [CMG-betrott rot certifikat till klienter](../core/clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_cmgroot). Om en enhet inte har förtroende för certifikatet för CMG, visas ett WINHTTP_CALLBACK_STATUS_FLAG_INVALID_CA fel i CCMSetup. log på klienten.

### <a name="get-the-command-line-from-configuration-manager"></a>Hämta kommando raden från Configuration Manager

1. I Configuration Manager-konsolen går du till arbets ytan **Administration** , expanderar **Cloud Services**och väljer noden för **samtidig hantering** .  

2. Välj objektet för samtidig hantering och välj sedan **Egenskaper** i menyfliksområdet.  

3. På fliken **aktivering** kopierar du kommando raden. Klistra in den i anteckningar och spara den för nästa process.  

Följande kommando rad är ett exempel:`CCMSETUPCMD="CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500 SMSSITECODE=ABC"`

<!--1358215-->
Bestäm vilka kommando rads egenskaper du behöver för din miljö:  

- Följande kommando rads egenskaper krävs i alla scenarier:  
  - CCMHOSTNAME  
  - SMSSITECODE  

- Följande egenskaper krävs när du använder Azure AD för klientautentisering i stället för PKI-baserade certifikat för klientautentisering:  
  - AADCLIENTAPPID  
  - AADRESOURCEURI  

- Om klienten växlar tillbaka till intranätet använder du följande egenskap:
  - SMSMP  

- Om du använder ett eget PKI-certifikat och din CRL inte har publicerats på Internet, krävs följande parameter:  
  - /noCRLCheck  

    Mer information finns i [Planera för CRL: er](../core/plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs).

- Från och med version 2002 använder du följande egenskap för att starta en aktivitetssekvens direkt efter klient registrering:
  - ETABLERINGar

    Mer information finns i [om klient installations egenskaper – etableringar](../core/clients/deploy/about-client-installation-properties.md#provisionts).

Platsen publicerar ytterligare Azure AD-information till Cloud Management Gateway (CMG). En Azure AD-ansluten klient hämtar den här informationen från CMG under CCMSetup-processen och använder samma klient organisation som den är ansluten till. Det här beteendet fören klar registreringen av enheter till samhantering i en miljö med fler än en Azure AD-klient. De enda två obligatoriska CCMSetup-egenskaperna är **CCMHOSTNAME** och **SMSSITECODE**.<!--3607731-->

> [!NOTE]
> Om du redan distribuerar Configuration Manager-klienten från Intune uppdaterar du Intune-appen med en ny kommando rad och en ny MSI. <!-- SCCMDocs-pr issue 3084 -->

Följande exempel innehåller alla dessa egenskaper:

`CCMSETUPCMD="CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSITECODE=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com PROVISIONTS=PRI20001"`

Mer information finns i [Egenskaper för klient installation](../core/clients/deploy/about-client-installation-properties.md).

### <a name="create-the-app-in-intune"></a>Skapa appen i Intune

1. Gå till [administrations Center för Microsoft Endpoint Manager](https://endpoint.microsoft.com)och expandera sedan det vänstra navigerings fönstret.  

2. Välj **appar**  >  **alla appar**  >  **Lägg till**.  

3. Under **annan**väljer du **branschspecifika appar**.  

4. Ladda upp filen **CCMSetup. msi** -appaket. Hitta filen i följande mapp på Configuration Manager plats Server: `<ConfigMgr installation directory>\bin\i386` .  

    > [!Tip]  
    > När du uppdaterar platsen, se till att du även uppdaterar den här appen i Intune.  

5. När appen har uppdaterats konfigurerar du appens information med kommando raden som du kopierade från Configuration Manager.  

> [!IMPORTANT]
> Om du anpassar den här kommando raden, se till att det inte är mer än 1024 tecken långt. När kommando rad längden är större än 1024 tecken Miss lyckas klient installationen.
