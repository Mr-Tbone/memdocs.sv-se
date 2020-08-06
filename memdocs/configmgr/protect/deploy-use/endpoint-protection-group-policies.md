---
title: Hantera Endpoint Protection med grup principer
titleSuffix: Configuration Manager
description: Lär dig hur du hanterar Endpoint Protection med hjälp av grup principer.
ms.date: 08/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 6c43ca9e1007c62835015a8c26a478af7da34ebb
ms.sourcegitcommit: c1afc8abd0d7da48815bd2b0e45147774c72c2df
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/05/2020
ms.locfileid: "87820013"
---
# <a name="use-group-policy-settings-to-manage-endpoint-protection-in-previous-versions-of-windows"></a>Använd grupprincip inställningar för att hantera Endpoint Protection i tidigare versioner av Windows

**Gäller för:**

- [Microsoft Defender Avancerat skydd (Microsoft Defender ATP)](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE2O8jv)
- System Center-Endpoint Protection på följande enheter på den äldre nivån:
    - Windows Server 2012 R2
    - Windows 8,1
    - Windows Server 2012
    - Windows 8
    - Windows Server 2008 R2 SP1
    - Windows 7 SP1
    - Windows Server 2008 SP2
    - Windows Vista

Du kan ha ett antal äldre Windows-enheter som är aktiverade med Endpoint Protection, men som ligger utanför Configuration Manager hierarkin. Till exempel enheter i en demilitariserad-zon eller enheter som är integrerade genom sammanslagning och förvärv. 

Du kan hantera Endpoint Protection på sådana enheter med grupprincip inställningar, enligt följande:

- [Kopiera Endpoint Protection princip definitioner](#copy-endpoint-protection-policy-definitions)
- Läs in Endpoint Protection princip definitioner på någon av följande platser:
    - [Central lagring på en domänkontrollant (rekommenderas)](#load-endpoint-protection-group-policy-settings-into-a-central-store-on-a-domain-controller)
    - [Lokal enhet](#load-endpoint-protection-group-policy-settings-into-your-local-device)

> [!NOTE]
> Information om hur du använder grupprincip inställningar för att hantera Microsoft Defender Antivirus i Windows 10, Windows Server 2019 och Windows Server 2016 finns i [använda grupprincip inställningar för att konfigurera och hantera Microsoft Defender Antivirus](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-antivirus/use-group-policy-microsoft-defender-antivirus).

## <a name="copy-endpoint-protection-policy-definitions"></a>Kopiera Endpoint Protection princip definitioner

På en Windows-enhet med äldre versioner som hanteras av Endpoint Protection kopierar du Endpoint Protection princip definitions filerna.

1. Gå till **C:\Program\Microsoft Security Client\Admx**. 

2. Komprimera följande filer till en zip-fil, till exempel **SCEP_admx.zip**:
    - **EndPointProtection.adml**
    - **EndPointProtection. admx**
3. Kopiera zip-filen till en tillfällig mapp. Till exempel, **c:\ temp_SCEP_GPO_admx**.
4. Extrahera filen. 

> [!NOTE]
> Register nycklarna för att konfigurera Endpoint Protection princip inställningar finns i **HKEY_LOCAL_MACHINE \software\policies\microsoft\microsoft program mot skadlig kod**.

## <a name="load-endpoint-protection-group-policy-settings-into-a-central-store-on-a-domain-controller"></a>Läs in Endpoint Protection grupprincip inställningar i en central lagrings plats på en domänkontrollant

Om du använder en [Central lagrings plats för grupprincip administrativa mallar](https://support.microsoft.com/help/3087759/how-to-create-and-manage-the-central-store-for-group-policy-administra)utför du följande steg för att läsa in och konfigurera inställningar för Endpoint Protection grup principer. Detta är den rekommenderade metoden.

1. Gå till mappen där du extraherade Endpoint Protection princip definitions filerna.
2. Kopiera filerna. admx och. adml till mappen **PolicyDefinitions** på domänkontrollanten:
    1. Kopiera **EndPointProtection. admx** till ** \\ \\ \<forest.root\> \\ SYSVOL- \\ \<domain\> \\ principer \\ PolicyDefinitions**. 
    2. Kopiera **EndPointProtection. adml** till ** \\ \\ \<forest.root\> \\ SYSVOL \\ \<domain\> \\ policys \\ PolicyDefinitions \\ en-US**.  

    Exempel:
    
    - Kopiera **EndPointProtection. admx** till ** \\ DC\SYSVOL\contoso.com\Policies\PolicyDefinitions**.
    - Kopiera **EndPointProtection. adml** till ** \\ DC\SYSVOL\contoso.com\Policies\PolicyDefinitions\en-US**.
    
    där **domänkontrollant** är namnet på domänkontrollanten och **contoso.com** är din domän.

3. Öppna [konsolen Grupprinciphantering](https://docs.microsoft.com/internet-explorer/ie11-deploy-guide/group-policy-and-group-policy-mgmt-console-ie11) och skapa ett nytt Grupprincip objekt (GPO) i din domän, till exempel **Endpoint Protection**.
4. Högerklicka på GRUPPRINCIPOBJEKTet för Endpoint Protection och klicka på **Redigera**.
5. I redigeraren Grupprinciphantering går du till **dator konfiguration**  >  **principer**  >  **administrativa mallar: princip definitioner**  >  **Windows-komponenter**  >  **Endpoint Protection**.

   Listan med Endpoint Protection grup principer visas.

6. Expandera avsnittet som innehåller den inställning som du vill konfigurera, dubbelklicka på inställningen för att öppna den och göra konfigurations ändringar.

## <a name="load-endpoint-protection-group-policy-settings-into-your-local-device"></a>Läs in Endpoint Protection grupprincip inställningar på den lokala enheten

I stället för att använda en central lagrings plats för att läsa in Endpoint Protection princip definitioner kan du lagra dem lokalt i enheten.

1. Gå till mappen där du extraherade Endpoint Protection princip definitions filerna.
2. Kopiera filerna. admx och. adml till din lokala PolicyDefinitions-mapp.
    1. Kopiera **EndPointProtection. admx** till **% systemroot%/PolicyDefinitions**. 
    2. Kopiera **EndPointProtection. adml** till **% systemroot%/PolicyDefinitions/en-US**.
    
    Exempel:

    - Kopiera **EndPointProtection. admx** till **C:\Windows\PolicyDefinitions**.
    - Kopiera **EndPointProtection. adml** till **C:\Windows\PolicyDefinitions\en-US**.
    
3. Öppna redigerare för lokalt grupprincipobjekt.
4. Gå till **dator konfiguration**  >  **administrativa mallar**  >  **Windows-komponenter**  >  **Endpoint Protection**.

    Listan med Endpoint Protection grup principer visas.

5. Expandera avsnittet som innehåller den inställning som du vill konfigurera, dubbelklicka på inställningen för att öppna den och göra konfigurations ändringar.

## <a name="next-steps"></a>Nästa steg
- En översikt över Endpoint Protection finns [Endpoint Protection](endpoint-protection.md).
- Information om hur du konfigurerar Endpoint Protection på en fristående klient finns manuellt i [konfigurera Endpoint Protection på en fristående klient](endpoint-protection-configure-standalone-client.md).
