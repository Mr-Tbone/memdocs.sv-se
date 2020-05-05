---
title: Översikt över CNG-certifikat
titleSuffix: Configuration Manager
description: Läs mer om stöd för CNG-certifikat (Cryptography Next Generation) för Configuration Manager-klienter och-servrar.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: dba904ae-7c44-46db-ae63-999b9821cb46
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4574b7ae97e8200da248a0b798677eacadb6229f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719836"
---
# <a name="cng-certificates-overview"></a>Översikt över CNG-certifikat
<!-- 1356191 --> 

Configuration Manager har begränsat stöd för kryptografi: CNG-certifikat (Next Generation). Configuration Manager klienter kan använda certifikat för PKI-klientautentisering med privat nyckel i CNG Key Storage Provider (KSP). Med KSP-stöd har Configuration Manager-klienter stöd för maskinvarubaserad privat nyckel, t. ex. TPM-KSP för certifikat för PKI-klientautentisering.

## <a name="supported-scenarios"></a>Scenarier som stöds
Du kan använda [Cryptography-API: t. ex. CNG-](https://msdn.microsoft.com/library/windows/desktop/bb204775.aspx) certifikatmallar för följande scenarier:

- Klient registrering och kommunikation med en HTTPS-hanterings plats   
- Program distribution och program distribution med en HTTPS-distributions plats   
- Distribution av operativsystem  
- SDK för klient meddelanden (med senaste uppdatering) och ISV-proxy   
- Cloud Management Gateway konfiguration  

Från och med version 1802 använder du CNG-certifikat för följande HTTPS-aktiverade Server roller: <!-- 1357314 -->   
- Hanteringsplats
- Distributionsplats
- Programuppdateringsplats
- Plats för tillståndsmigrering     

Från och med version 1806 använder du CNG-certifikat för följande HTTPS-aktiverade Server roller:

- Certifikat registrerings plats, inklusive NDES-servern med modulen Configuration Manager-princip <!--1357314-->

> [!NOTE]
> CNG är bakåtkompatibel med krypto-API (CAPI). CAPI-certifikat fortsätter att stödja även när CNG-stöd är aktiverat på klienten.

## <a name="unsupported-scenarios"></a>Scenarier som inte stöds

Följande scenarier stöds inte för närvarande:

- Följande Server roller fungerar inte när de installeras i HTTPS-läge med ett CNG-certifikat som är kopplat till webbplatsen i Internet Information Services (IIS): 
    - Webb tjänst för program katalog
    - Webbplats för program katalog
    - Registreringsplats  
    - Registreringsproxyplats  

- Software Center visar inte program och paket som är tillgängliga som distribueras till användar-eller användar grupp samlingar.

- Använd CNG-certifikat för att skapa en moln distributions plats.

- Om NDES-principmodulen använder ett CNG-certifikat för klientautentisering Miss lyckas kommunikationen till certifikat registrerings platsen. 
    - Detta stöds från och med Configuration Manager version 1806.

- Om du anger ett CNG-certifikat när du skapar media för aktivitetssekvenser kan guiden inte skapa startbara media.
    - Detta stöds från och med Configuration Manager version 1806.

## <a name="to-use-cng-certificates"></a>Använda CNG-certifikat

Om du vill använda CNG-certifikat måste din certifikat utfärdare (CA) tillhandahålla mallar för CNG-certifikat för mål datorer. Mal Lav bildinformationen varierar beroende på scenariot. följande egenskaper krävs dock:

- Fliken **kompatibilitet**

    - **Certifikat utfärdaren** måste vara Windows Server 2008 eller senare. (Windows Server 2012 rekommenderas.)

    - **Certifikat mottagaren** måste vara Windows Vista/Server 2008 eller senare. (Windows 8/Windows Server 2012 rekommenderas.)

- Fliken **kryptografi**

    - **Leverantörs kategori** måste vara **nyckel lagrings leverantör**. kunna
    - **Begäran måste använda någon av följande providers:** måste vara **Microsoft Software Key Storage-Provider**. 

> [!NOTE]
> Kraven för din miljö eller organisation kan vara olika. Kontakta din PKI-expert. Den viktiga punkten att tänka på är att en certifikatmall måste använda en nyckel lagrings leverantör för att dra nytta av CNG.

För bästa resultat rekommenderar vi att du skapar ämnes namnet från Active Directory information. Använd DNS-namnet för **ämnes namnets format** och inkludera DNS-namnet i det alternativa ämnes namnet. Annars måste du ange den här informationen när enheten registreras i certifikat profilen.
