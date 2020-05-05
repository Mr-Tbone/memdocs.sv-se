---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/13/2019
ms.openlocfilehash: b21365d0c355adab6819e13537c1b25316583ec2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720543"
---
<!-- ## Update and configure the .NET Framework to support TLS 1.2 Note: the heading in in the 2 articles (enable-tls-1-2-client & enable-tls-1-2-server) to better facilitate linking. -->

### <a name="determine-net-version"></a>Fastställ .NET-version

Börja med att fastställa de installerade .NET-versionerna. Mer information finns i [How to avgöra vilka versioner och Service Pack nivåer i Microsoft .NET Framework som är installerade](https://support.microsoft.com/help/318785/how-to-determine-which-versions-and-service-pack-levels-of-the-microso).

### <a name="install-net-updates"></a>Installera .NET-uppdateringar

Installera .NET-uppdateringar så att du kan aktivera stark kryptografi. Vissa versioner av .NET Framework kan kräva att uppdateringar möjliggör stark kryptering. Använd följande rikt linjer:

- NET Framework-4.6.2 och senare har stöd för TLS 1,1 och TLS 1,2. Bekräfta register inställningarna, men inga ytterligare ändringar krävs.

- Uppdatera NET Framework 4,6 och tidigare versioner för att stödja TLS 1,1 och TLS 1,2. Mer information finns i [.NET Framework versioner och beroenden](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies).

- Om du använder .NET Framework 4.5.1 eller 4.5.2 på Windows 8,1 eller Windows Server 2012 är relevanta uppdateringar och information även tillgängliga från [Download Center](https://www.microsoft.com/download/details.aspx?id=42883).


### <a name="configure-for-strong-cryptography"></a>Konfigurera för stark kryptografi

Konfigurera .NET Framework för att stödja stark kryptografi. Ange `SchUseStrongCrypto` register inställningen till `DWORD:00000001`. Det här värdet inaktiverar chiffrering av RC4-Stream och kräver en omstart. Mer information om den här inställningen finns i [Microsoft Security Advisory 296038](https://docs.microsoft.com/security-updates/SecurityAdvisories/2015/2960358).

Se till att ange följande register nycklar på alla datorer som kommunicerar i nätverket med ett TLS 1,2-aktiverat system. Till exempel, Configuration Manager klienter, fjärrplatsens system roller som inte är installerade på plats servern och själva plats servern.

Uppdatera följande under nyckel värden för 32-bitars program som körs på 32-bitars OSs och för 64-bitars program som körs på 64-bitars OSs:

``` Registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v2.0.50727]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
```

Uppdatera följande under nyckel värden för 32-bitars program som körs på 64-bitars OSs:

``` Registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v2.0.50727]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
```

> [!Note]  
> `SchUseStrongCrypto` Inställningen tillåter att .net använder TLS 1,1 och TLS 1,2. `SystemDefaultTlsVersions` Inställningen gör att .net kan använda operativ systemets konfiguration. Mer information finns i [metod tips för TLS med .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls).
