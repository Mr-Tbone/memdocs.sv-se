---
title: Konfigurera Endpoint Protection på en fristående klient
titleSuffix: Configuration Manager
description: Lär dig hur du konfigurerar Endpoint Protection på en fristående klient.
ms.date: 07/22/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f8d116879b0a85f3276d848b01c69d575b8b69fd
ms.sourcegitcommit: 41b2b50d5870dc127a8848a6657d56112f92515a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/04/2020
ms.locfileid: "87758320"
---
# <a name="configure-endpoint-protection-on-a-standalone-client"></a>Konfigurera Endpoint Protection på en fristående klient

*Gäller för: Configuration Manager (aktuell gren)*

Din organisation kan ha ett antal fristående klienter som du inte kan hantera eller skydda med Microsoft Endpoint Configuration Manager. Utan någon slut punkts skydd på plats är dessa fristående klienter utsatta för potentiella attacker mot skadlig kod. För att skydda sådana fristående klienter kan du konfigurera dem manuellt med Endpoint Protection, enligt beskrivningen i det här avsnittet.

Så här konfigurerar du Endpoint Protection på en fristående klient manuellt:

- [Skapa en princip för program mot skadlig kod för den fristående klienten](#create-an-antimalware-policy-for-the-standalone-client)
- [Överföra Endpoint Protection klient installations paket till den fristående klienten](#transfer-endpoint-protection-client-installation-package-to-the-standalone-client)
- [Installera Endpoint Protection på den fristående klienten](#install-endpoint-protection-on-the-standalone-client)

## <a name="prerequisites"></a>Förutsättningar

Följande är förutsättningarna för att konfigurera Endpoint Protection på en fristående klient:

- Du måste ha åtkomst till Endpoint Protection klient installations paketet **scepinstall.exe**. Du hittar det här paketet i mappen **C:\Program\Microsoft Configuration Manager\Client** . 
- Se till att [plattforms uppdateringen för program mot skadlig kod i januari 2017 för Endpoint Protection-klienter](https://support.microsoft.com/help/3209361/january-2017-anti-malware-platform-update-for-endpoint-protection-clie) är installerad. 

## <a name="create-an-antimalware-policy-for-the-standalone-client"></a>Skapa en princip för program mot skadlig kod för den fristående klienten

I det här steget skapar du en anpassad princip för program mot skadlig kod i Configuration Manager-konsolen och överför den sedan till den fristående klienten.

När du skapar principen för program mot skadlig kod måste du konfigurera definitions uppdaterings källan så att princip definitionerna hålls uppdaterade på den fristående klienten. Du kan konfigurera definitions uppdaterings källan som [Microsoft Update](endpoint-definitions-microsoft-updates.md) och [Microsoft Malware Protection Center](endpoint-definitions-protection-center.md), om den fristående klienten är ansluten till Internet. Du kan också välja [nätverks resurs](endpoint-definitions-network.md) som definitions distributions källa och uppdatera den regelbundet med det senaste definitions uppdaterings paketet. 

Så här skapar du en princip för program mot skadlig kod för den fristående klienten:

1. Klicka på **till gångar och efterlevnad**i **Configuration Manager** -konsolen.
2. I arbetsytan **Tillgångar och efterlevnad** expanderar du **Endpoint Protection**och klickar på **Antiskadlig kod-principer**.
3. På fliken **Start** i gruppen **Skapa** klickar du på **Skapa princip för program mot skadlig kod**.
4. I avsnittet **Allmänt** i dialogrutan **Skapa princip för program mot skadlig kod** anger du ett namn och en beskrivning för principen.
5. I dialogrutan **princip för program mot skadlig kod** konfigurerar du de inställningar som krävs för denna princip för program mot skadlig kod och klickar sedan på **OK**. En lista över inställningar som du kan konfigurera finns i [lista över princip inställningar för program mot skadlig kod](endpoint-antimalware-policies.md#list-of-antimalware-policy-settings).
    > [!NOTE]
    > För inställningen **definitions uppdateringar** väljer du **uppdateringar som distribuerats från Microsoft Update** och uppdateringar som är **distribuerade från Microsoft Malware Protection Center** om den fristående klienten är ansluten till Internet.  
    > Du kan också välja **uppdateringar från UNC-filresurser** för att distribuera princip definitionerna via nätverks resursen. Lägg sedan till en eller flera UNC-sökvägar till platsen för definitions uppdateringarnas filer på en nätverks resurs.

6. Exportera den nyligen skapade principen som en XML:
    1. I listan **principer för program mot skadlig kod** högerklickar du på principen.
    1. Välj **Exportera**.
    1. Spara principen som en XML, till exempel **standalone.xml**.
7. Överför den nya XML-koden för program mot skadlig kod till den fristående mål klient som du vill konfigurera Endpoint Protection på.

## <a name="transfer-endpoint-protection-client-installation-package-to-the-standalone-client"></a>Överföra Endpoint Protection klient installations paket till den fristående klienten

I det här steget kopierar du Endpoint Protection klient installations paket (**scepinstall.exe**) från Configuration Manager-servern och överför det till den fristående klienten.

1. Logga in på Configuration Manager servern.
2. Navigera till mappen **klient** i Configuration Manager-installationsmappen (**c:\Program\Microsoft Configuration Manager\Client**).
3. Kopiera **scepinstall.exe**.
4. Överför **scepinstall.exe** till den fristående mål klient som du vill installera Endpoint Protection klient program varan på.

## <a name="install-endpoint-protection-on-the-standalone-client"></a>Installera Endpoint Protection på den fristående klienten
I det här steget ska du köra installations paketet (**scepinstall.exe**) och principen för program mot skadlig kod (som tidigare har överförts från Configuration Manager-servern) från kommando tolken på den fristående klienten.

Så här installerar du Endpoint Protection på den fristående klienten:

1. Öppna en kommando tolk som administratör på den fristående klienten.
2. Ändra katalogen till den mapp där du sparade installations filen för **scepinstall.exe** .
3. Ange följande kommando för att köra **scepinstall.exe** med principen för program mot skadlig kod:

    ```cmd
    scepinstall.exe /policy <full path>\<policy file>
    ```

    Ersätt `full path` med sökvägen där du sparade XML-filen med program mot skadlig kod och `policy file` med princip fil namnet för program mot skadlig kod.
 
    Installations programmet extraheras och installations guiden startas.

4. Slutför klient installationen genom att följa anvisningarna på skärmen.

    På den sista skärmen i installations guiden är alternativet för att söka igenom datorn efter potentiella hot efter att de senaste uppdateringarna är markerat som standard. Du kan avmarkera kryss rutan om du vill hoppa över sökningen.

## <a name="change-antimalware-policy-settings-on-a-standalone-endpoint-protection-client"></a>Ändra princip inställningar för program mot skadlig kod på en fristående Endpoint Protection-klient

Ändra eller uppdatera principen för program mot skadlig kod på den fristående Endpoint Protection klienten: 

1. [Skapa en princip för program mot skadlig kod för den fristående klienten](#create-an-antimalware-policy-for-the-standalone-client).
2. Kör följande kommando på den fristående klienten:

```cmd
C:\Program Files\Microsoft Security Client\ConfigSecurityPolicy.exe <full path>\<policy file>
```

Ersätt `full path` med sökvägen där du sparade den nya XML-filen för program mot skadlig kod och `policy file` med princip fil namnet för program mot skadlig kod.

## <a name="next-steps"></a>Nästa steg

Information om hur du använder Endpoint Protection för att hantera säkerhet och skadlig kod på Configuration Manager klient datorer finns i [konfigurera Endpoint Protection](endpoint-protection-configure.md).