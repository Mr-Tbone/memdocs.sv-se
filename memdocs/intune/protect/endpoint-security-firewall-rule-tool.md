---
title: Verktyget för migrering av Endpoint Security-brandväggsregler i Microsoft Intune – Azure | Microsoft Docs
description: Lär dig hur du använder verktyget för migrering av Endpoint Security-brandväggsregler i Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/14/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
mr.reviewer: mattsha
ms.openlocfilehash: 7dd6d3a01d18e4d8b334bdeee3f72eeaeed67c0a
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/18/2020
ms.locfileid: "86465035"
---
# <a name="endpoint-security-firewall-rule-migration-tool-overview"></a>Översikt över verktyget för migrering av Endpoint Security-brandväggsregler

Många organisationer vill nu flytta sin säkerhetskonfiguration till Microsoft Endpoint Manager för att få tillgång till en mer modern och molnbaserad hantering.

Endpoint Security i Endpoint Manager har omfattande hanteringsfunktioner för konfigurering av Windows-brandväggen och detaljerad hantering av brandväggsregler.

Många organisationer använder redan gruppolicyer till att hantera brandväggsregler i Windows. Det kan vara svårt att flytta till en modern hantering eftersom det är mödosamt att skapa hundratals brandväggsregler manuellt.

För att hjälpa kunderna att flytta sina brandväggsregler till policyer för slutpunktssäkerhet i Endpoint Manager så har vi utvecklat **verktyget för migrering av Endpoint Security-brandväggsregler**.

Kunder kan köra **verktyget för migrering av Endpoint Security-brandväggsregler** på en referensenhet/förkonfigurerad Windows 10-klient och automatiskt skapa policyer för Endpoint Security-brandväggsregler i Endpoint Manager. När de har skapats kan administratörer rikta in de här reglerna mot Azure AD-grupper för att konfigurera MDM och samhanterade klienter.

Ladda ned [verktyget för migrering av Endpoint Security-brandväggsregler](https://aka.ms/EndpointSecurityFWRuleMigrationTool):<br>
<a href="https://aka.ms/EndpointSecurityFWRuleMigrationTool"><img alt="Download the tool" src="./media/endpoint-security-firewall-rule-tool/downloadtool.png" width="170"></a>

## <a name="tool-usage"></a>Använda verktyget

Verktyget körs på en referensdator och migrerar den aktuella konfigurationen av Windows-brandväggsregler. När du kör verktyget exporteras alla aktiva brandväggsregler på enheten. Nya Intune-policyer med de insamlade reglerna skapas automatiskt.

1. Logga in på referensdatorn med lokal administratörsbehörighet.
2. Ladda ned och zippa upp filen `Export-FirewallRules.zip`. <br>
   Zip-filen innehåller skriptfilen `Export-FirewallRules.ps1`. 
3. Kör skriptet `Export-FirewallRules.ps1` på datorn. <br>
   Skriptet laddar ned alla komponenter som krävs för att köra verktyget. Ange autentiseringsuppgifter som Intune-administratören när du uppmanas till det. Mer information om vilken behörighet som krävs finns i [Nödvändiga behörigheter](#required-permissions).
4. Ange ett policynamn när du uppmanas till det. <br>
   Den här policyn visas i [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) i fönstret **Endpoint Security** > **Brandvägg**. 

    > [!IMPORTANT]
    > Policynamnet måste vara unikt för klientorganisationen.

    Om fler än 150 brandväggsregler hittas skapas flera policyer.

    > [!NOTE]
    > Som standard migreras bara aktiva brandväggsregler som skapats via GPO. Det finns växlar för att ändra standardvärdena. Mer information finns i [Växlar](#switches).
    >
    > Beroende på hur många brandväggsregler som hittas kan det ta en stund att köra verktyget.

5. När du är färdig matar verktyget ut antalet brandväggsregler som inte gick att migrera automatiskt. Mer information finns i [Konfiguration som inte stöds](#unsupported-configuration).

## <a name="switches"></a>Växlar

Du kan använda följande reglage (parametrar) till att ändra verktygets standardfunktion.

- `IncludeLocalRules` – Om du använder den här växeln tas alla regler som skapats lokalt och alla standardregler i Windows med i exporten. Observera att den här växeln kan göra att många regler migreras. 
- `IncludedDisabledRules` – Om du använder den här växeln tas alla aktiva och inaktiva Windows-brandväggsregler med i exporten. Observera att den här växeln kan göra att många regler migreras.

## <a name="unsupported-configuration"></a>Konfiguration som inte stöds

Följande registerbaserade inställningar stöds inte eftersom det saknas MDM-stöd i Windows. De här inställningarna är ovanliga, men om du behöver använda dem ska du logga behovet via dina vanliga supportkanaler.

|     GPO-fält    |     Orsak    |
|-|-|
|      TYPE-VALUE =/ "Security=" IFSECURE-VAL    |     IPSec-relaterad inställning som inte stöds i Windows MDM    |
|      TYPE-VALUE =/ "Security2_9=" IFSECURE2-9-VAL    |     IPSec-relaterad inställning som inte stöds i Windows MDM    |
|      TYPE-VALUE =/ "Security2=" IFSECURE2-10-VAL     |     IPSec-relaterad inställning som inte stöds i Windows MDM    |
|      TYPE-VALUE =/ "IF=" IF-VAL    |     Det går inte att hantera gränssnitts-ID:t (LUID)    |
|      TYPE-VALUE =/ "Defer=" DEFER-VAL    |     Relaterade till inkommande NAT-traversering exponeras inte via grupprincip eller Windows MDM    |
|      TYPE-VALUE =/ "LSM=" BOOL-VAL    |     Lös källmappning exponeras inte via grupprincip eller Windows MDM    |
|      TYPE-VALUE =/ "Platform=" PLATFORM-VAL    |     OS-versionshantering exponeras inte via grupprincip eller Windows MDM    |
|      TYPE-VALUE =/ "RMauth=" STR-VAL    |     IPSec-relaterad inställning som inte stöds i Windows MDM    |
|      TYPE-VALUE =/ "RUAuth=" STR-VAL    |     IPSec-relaterad inställning som inte stöds i Windows MDM    |
|      TYPE-VALUE =/ "AuthByPassOut=" BOOL-VAL    |     IPSec-relaterad inställning som inte stöds i Windows MDM    |
|      TYPE-VALUE =/ "LOM=" BOOL-VAL    |     Endast lokal mappning exponeras inte via grupprincip eller Windows MDM    |
|      TYPE-VALUE =/ "Platform2=" PLATFORM-OP-VAL    |     Redundant inställning exponeras inte via grupprincip eller Windows MDM    |
|      TYPE-VALUE =/ "PCross=" BOOL-VAL    |     Tillåt profilöverlappning exponeras inte via grupprincip eller Windows MDM    |
|      TYPE-VALUE =/ "LUOwn=" STR-VAL    |     Ägar-SID för lokal användare kan inte tillämpas i MDM    |
|      TYPE-VALUE =/ "TTK=" TRUST-TUPLE-KEYWORD-VAL    |     Matcha trafik med betrott tupelnyckelord exponeras inte via grupprincip eller Windows MDM    |
|      TYPE-VALUE =/ “TTK2_22=” TRUST-TUPLE-KEYWORD-VAL2-22    |     Matcha trafik med betrott tupelnyckelord exponeras inte via grupprincip eller Windows MDM    |
|      TYPE-VALUE =/ “TTK2_27=” TRUST-TUPLE-KEYWORD-VAL2-27    |     Matcha trafik med betrott tupelnyckelord exponeras inte via grupprincip eller Windows MDM    |
|      TYPE-VALUE =/ “TTK2_28=” TRUST-TUPLE-KEYWORD-VAL2-28    |     Matcha trafik med betrott tupelnyckelord exponeras inte via grupprincip eller Windows MDM    |
|      TYPE-VALUE =/ "NNm=" STR-ENC-VAL    |     IPSec-relaterad inställning som inte stöds i Windows MDM    |
|      TYPE-VALUE =/ "SecurityRealmId=" STR-VAL    |     IPSec-relaterad inställning som inte stöds i Windows MDM    |

## <a name="unsupported-setting-values"></a>Inställningsvärden som inte stöds
Följande inställningsvärden stöds inte för migrering:

**Portar**
- `PlayToDiscovery` stöds inte som lokalt eller fjärranslutet portintervall.

**Adressintervall**
- `LocalSubnet6` stöds inte som lokalt eller fjärranslutet adressintervall. 
- `LocalSubnet4` stöds inte som lokalt eller fjärranslutet adressintervall.
- `PlatToDevice` stöds inte som lokalt eller fjärranslutet adressintervall.

När du har kört verktyget genereras en rapport med de regler som inte migrerades. Du kan se de här reglerna i `RulesError.csv` som finns i `C:\<folder needed>`. 

## <a name="required-permissions"></a>Behörigheter som krävs
Endpoint Security Manager-, Intune Service Admin- och Global Admin-användare kan migrera Windows-brandväggsregler till Endpoint Security-policyer. Du kan också använda en anpassad roll med behörigheterna **Ta bort**, **Läsa**, **Tilldela**, **Skapa** och **Uppdatera**. Mer information finns i [Tilldela administratörsbehörighet för Intune](../fundamentals/users-add.md#grant-admin-permissions).

## <a name="next-steps"></a>Nästa steg

- Tilldela regler till Azure AD-grupper för att konfigurera MDM-klienter och samhanterade klienter. Mer information finns i [Lägga till grupper för att organisera användare och enheter](../fundamentals/groups-add.md).
