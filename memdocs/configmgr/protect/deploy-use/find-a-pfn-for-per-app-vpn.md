---
title: Hitta ett paketfamiljenamn (PFN) för per app-VPN
titleSuffix: Configuration Manager
description: Lär dig mer om de två sätten att hitta ett paket familje namn så att du kan konfigurera en per app-VPN.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 47118499-3d26-4c25-bfde-b129de7eaa59
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f109e4ea4bee4a1de767508d62bc3f080d24f625
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715608"
---
# <a name="find-a-package-family-name-pfn-for-per-app-vpn"></a>Hitta ett paketfamiljenamn (PFN) för per app-VPN

*Gäller för: Configuration Manager (aktuell gren)*


Det finns två sätt att hitta ett PFN så att du kan konfigurera en per app-VPN.

## <a name="find-a-pfn-for-an-app-thats-installed-on-a-windows-10-computer"></a>Hitta ett PFN för en app som är installerad på en Windows 10-dator

Om den app som du arbetar med redan är installerad på en Windows 10-dator kan du hämta PFN med hjälp av PowerShell-cmdleten [Get-AppxPackage](https://technet.microsoft.com/library/hh856044.aspx).

Syntaxen för Get-AppxPackage är:

``` Syntax
Get-AppxPackage [[-Name] <String> ] [[-Publisher] <String> ] [-AllUsers] [-User <String> ] [ <CommonParameters>]
```

> [!NOTE]
> Du kan behöva köra PowerShell som administratör för att kunna hämta PFN

Om du exempelvis vill få information om alla universella appar som är installerade på datorn använder du `Get-AppxPackage`.

Använd `Get-AppxPackage *<app_name>` om du vill få information om en app som du känner till namnet eller en del av namnet på. Observera användning av jokertecken, vilket är särskilt användbart om du inte är säker på appens fullständiga namn. Använd till exempel `Get-AppxPackage *OneNote` om du vill hämta info för OneNote.


Här är den information som har hämtats för OneNote:

`Name                   : Microsoft.Office.OneNote`

`Publisher              : CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US`

`Architecture           : X64`

`ResourceId             :`

`Version                : 17.6769.57631.0`

`PackageFullName        : Microsoft.Office.OneNote_17.6769.57631.0_x64__8wekyb3d8bbwe`

`InstallLocation        : C:\Program Files\WindowsApps`

`\Microsoft.Office.OneNote_17.6769.57631.0_x64__8wekyb3d8bbwe`

`IsFramework            : False`

**`PackageFamilyName      : Microsoft.Office.OneNote_8wekyb3d8bbwe`**

`PublisherId            : 8wekyb3d8bbwe`



## <a name="find-a-pfn-if-the-app-is-not-installed-on-a-computer"></a>Hitta en PFN om appen inte har installerats på en dator

1. Gå till https://www.microsoft.com/store/apps
2. Ange namnet på appen i sökfältet. I vårt exempel söker du efter OneNote.
3. Klicka på länken till appen. Observera att den URL som du har åtkomst till har en serie bokstäver i slutet. I vårt exempel ser URL: en ut så här:`https://www.microsoft.com/store/apps/onenote/9wzdncrfhvjl`
4. På en annan flik klistrar du in följande URL `https://bspmts.mp.microsoft.com/v1/public/catalog/Retail/Products/<app id>/applockerdata`, och `<app id>` ersätter med det app-ID som https://www.microsoft.com/store/apps du fick från – serien med bokstäver i slutet av URL: en i steg 3. I vårt exempel med OneNote skulle du klistra in: `https://bspmts.mp.microsoft.com/v1/public/catalog/Retail/Products/9wzdncrfhvjl/applockerdata`.

Den information du vill visa visas i Microsoft Edge; i Internet Explorer klickar du på **Öppna** om du vill se informationen. PFN-värdet anges på första raden. Så här ser resultatet ut i vårt exempel:

``` JSON
{
  "packageFamilyName": "Microsoft.Office.OneNote_8wekyb3d8bbwe",
  "packageIdentityName": "Microsoft.Office.OneNote",
  "windowsPhoneLegacyId": "ca05b3ab-f157-450c-8c49-a1f127f5e71d",
  "publisherCertificateName": "CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US"
}
```
