---
title: Aktivera Transport Layer Security (TLS) 1,2 på klienter
titleSuffix: Configuration Manager
description: Information om hur du aktiverar TLS 1,2 för Configuration Manager klienter.
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5b094a02-a425-4b67-81d3-8455e4265512
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e5b525da4a58240b34c30403db618ea0d2ca85f1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720557"
---
# <a name="how-to-enable-tls-12-on-clients"></a>Så här aktiverar du TLS 1,2 på klienter

*Gäller för: Configuration Manager (Current Branch)*

När du aktiverar TLS 1,2 för Configuration Managers miljön börjar du med att se till att klienterna är kompatibla och korrekt konfigurerade att använda TLS 1,2 innan du aktiverar TLS 1,2 och inaktiverar de äldre protokollen på plats servrarna och fjärrplatssystem. Det finns tre uppgifter för att aktivera TLS 1,2 på klienter:

- Uppdatera Windows och WinHTTP
- Se till att TLS 1,2 är aktiverat som ett protokoll för SChannel på operativ system nivå
- Uppdatera och konfigurera .NET Framework för att stödja TLS 1,2

Mer information om beroenden för vissa Configuration Manager funktioner och scenarier finns i [Aktivera TLS 1,2](enable-tls-1-2.md).

## <a name="update-windows-and-winhttp"></a><a name="bkmk_winhttp"></a>Uppdatera Windows och WinHTTP

Windows 8,1, Windows Server 2012 R2, Windows 10, Windows Server 2016 och senare versioner av Windows har inbyggt stöd för TLS 1,2 för klient-server-kommunikation över WinHTTP. 

Tidigare versioner av Windows, till exempel Windows 7 eller Windows Server 2012, aktiverar inte TLS 1,1 eller TLS 1,2 som standard för säker kommunikation med hjälp av WinHTTP. För dessa tidigare versioner av Windows installerar du [uppdatering 3140245](https://support.microsoft.com/help/3140245) för att aktivera registervärdet nedan, som kan ställas in för att lägga till TLS 1,1 och TLS 1,2 till listan över säkra protokoll för WinHTTP som är standard. När korrigeringen är installerad skapar du följande register värden:

> [!IMPORTANT]
> Aktivera de här inställningarna på alla klienter som kör tidigare versioner av Windows *innan* du aktiverar TLS 1,2 och inaktiverar de äldre protokollen på Configuration Manager servrar. Annars kan du oavsiktligt överblivna dem.

Verifiera värdet för `DefaultSecureProtocols` register inställningen, till exempel:

``` Registry
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
```

Om du ändrar det här värdet startar du om datorn.

Exemplet ovan visar värdet `0xAA0` för för WinHTTP `DefaultSecureProtocols` -inställningen. [KB 3140245: uppdatera för att aktivera tls 1,1 och tls 1,2 som standard säkra protokoll i WinHTTP i Windows](https://support.microsoft.com/help/3140245) listar det hexadecimala värdet för varje protokoll. Som standard i Windows är `0x0A0` det här värdet att aktivera SSL 3,0 och TLS 1,0 för WinHTTP. Exemplet ovan behåller dessa standardinställningar och aktiverar även TLS 1,1 och TLS 1,2 för WinHTTP. Den här konfigurationen säkerställer att ändringen inte bryter några andra program som kan vara beroende av SSL 3,0 eller TLS 1,0. Du kan använda värdet för `0xA00` för att endast aktivera TLS 1,1 och TLS 1,2. Configuration Manager stöder det säkraste protokollet som Windows förhandlar mellan båda enheterna.

 Om du vill inaktivera SSL 3,0 och TLS 1,0, använder du inställningen för inaktiverade SChannel-protokoll i Windows. Mer information finns i [så här begränsar du användningen av vissa kryptografiska algoritmer och protokoll i Schannel. dll](https://support.microsoft.com/help/245030/how-to-restrict-the-use-of-certain-cryptographic-algorithms-and-protoc).

## <a name="ensure-that-tls-12-is-enabled-as-a-protocol-for-schannel-at-the-operating-system-level"></a><a name="bkmk_protocol"></a>Se till att TLS 1,2 är aktiverat som ett protokoll för SChannel på operativ system nivå

[!INCLUDE [Enable TLS 1.2 protocol as a security provider](includes/enable-tls-1-2-protocol-security-provider.md)]

## <a name="update-and-configure-the-net-framework-to-support-tls-12"></a><a name="bkmk_net"></a>Uppdatera och konfigurera .NET Framework för att stödja TLS 1,2

[!INCLUDE [Update and configure the .NET framework to support TLS 1.2](includes/update-net-framework-to-support-tls-1-2.md)]


## <a name="next-steps"></a>Nästa steg

- [Aktivera TLS 1,2 på plats servrarna och fjärrplatsens system](enable-tls-1-2-server.md)
- [Vanliga problem vid aktivering av TLS 1.2](enable-tls-1-2-troubleshoot.md)

