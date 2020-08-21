---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/13/2019
ms.openlocfilehash: f14713431c71c1f3625d13ea4be1d919b072e273
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88703994"
---
<!--## Enable Transport layer security (TLS) 1.2 protocol as a security provider Note: the heading in in the 2 articles (enable-tls-1-2-client & enable-tls-1-2-server) to better facilitate linking. -->

TLS 1,2 är aktiverat som standard. Därför behövs ingen ändring av dessa nycklar för att aktivera den. Du kan göra ändringar under `Protocols` för att inaktivera tls 1,0 och tls 1,1 när du har följt resten av vägledningen i de här artiklarna och du har verifierat att miljön fungerar när endast TLS 1,2 har Aktiver ATS.

Kontrol lera `\SecurityProviders\SCHANNEL\Protocols` inställningen för register under nyckeln, som du ser i [metod tips för TLS (Transport Layer Security) med .NET Framework](/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry).