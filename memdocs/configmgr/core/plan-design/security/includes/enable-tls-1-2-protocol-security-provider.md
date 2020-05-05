---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/13/2019
ms.openlocfilehash: 08cebf6ef844e1854daa9444462f4c4470319186
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720536"
---
<!--## Enable Transport layer security (TLS) 1.2 protocol as a security provider Note: the heading in in the 2 articles (enable-tls-1-2-client & enable-tls-1-2-server) to better facilitate linking. -->

TLS 1,2 är aktiverat som standard. Därför behövs ingen ändring av dessa nycklar för att aktivera den. Du kan göra ändringar under `Protocols` för att inaktivera TLS 1,0 och TLS 1,1 när du har följt resten av vägledningen i de här artiklarna och du har verifierat att miljön fungerar när endast TLS 1,2 har Aktiver ATS.

Kontrol lera `\SecurityProviders\SCHANNEL\Protocols` inställningen för register under nyckeln, som du ser i [metod tips för TLS (Transport Layer security) med .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry).

