---
title: Så här skapar du Wi-Fi-profiler
titleSuffix: Configuration Manager
description: Lär dig hur du använder Wi-Fi-profiler i Configuration Manager för att distribuera trådlösa nätverks inställningar till användare i din organisation.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 321b19b2-a093-4b8f-995f-41f74b886eb5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 21dffd1201b04846a9fffcdc7cc917465daa5905
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710771"
---
# <a name="create-wi-fi-profiles"></a>Skapa Wi-Fi-profiler

*Gäller för: Configuration Manager (aktuell gren)*

Använd Wi-Fi-profiler i Configuration Manager för att distribuera trådlösa nätverks inställningar till användare i din organisation. Genom att distribuera de här inställningarna gör du det enklare för användarna att ansluta till Wi-Fi.  

Du kan till exempel ha ett Wi-Fi-nätverk som du vill aktivera alla Windows-datorer för att ansluta till. Skapa en Wi-Fi-profil som innehåller de inställningar som krävs för att ansluta till det trådlösa nätverket. Distribuera sedan profilen till alla användare som har Windows-datorer i hierarkin. Användare av de här enheterna ser ditt nätverk i listan över trådlösa nätverk och kan enkelt ansluta till det här nätverket.  

Du kan konfigurera Wi-Fi-profiler för följande OS-versioner:

- Windows 8,1 32-bitars eller 64-bitars

- Windows RT 8.1

- Windows 10 eller Windows 10 Mobile

Du kan också använda Configuration Manager för att distribuera trådlösa nätverks inställningar till mobila enheter med lokal hantering av mobila enheter (MDM). Mer allmän information finns i [Vad är lokal MDM](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).

När du skapar en Wi-Fi-profil kan du inkludera ett brett spektrum av säkerhetsinställningar. Inställningarna omfattar certifikat för Server verifiering och klientautentisering som har överförts med hjälp av Configuration Manager certifikat profiler. Mer information om certifikat profiler finns i [certifikat profiler](introduction-to-certificate-profiles.md).

## <a name="create-a-wi-fi-profile"></a>Skapa en Wi-Fi-profil

1. Gå till arbets ytan **till gångar och efterlevnad** i Configuration Manager-konsolen **, expandera kompatibilitetsinställningar, expandera** **åtkomst till företags resurser**och välj noden **Wi-Fi-profiler** .

1. På fliken **Start** går du till gruppen **skapa** och väljer **Skapa Wi-Fi-profil**.

1. Ange följande information på sidan **Allmänt** i guiden Skapa Wi-Fi-profil:

    - **Namn**: Ange ett unikt namn för att identifiera profilen i-konsolen.

    - **Beskrivning**: du kan också lägga till en beskrivning för att ange ytterligare information om Wi-Fi-profilen.

    - **Importera ett befintligt Wi-Fi-profil objekt från en fil**: Välj det här alternativet om du vill använda inställningarna från en annan Wi-Fi-profil. När du väljer det här alternativet fören klar de återstående sidorna i guiden till två sidor: **Importera Wi-Fi-profil** och **plattformar som stöds**.

        > [!IMPORTANT]
        > Kontrol lera att den Wi-Fi-profil som du importerar innehåller giltig XML för en Wi-Fi-profil. När du importerar filen verifierar Configuration Manager inte profilen.

    - **Allvarlighets grad för inkompatibilitet för rapporter**: Välj någon av följande allvarlighets grader som enheten rapporterar om den utvärderar Wi-Fi-profilen till att vara inkompatibel. Om installationen av profilen till exempel Miss lyckas, är den inkompatibel.

        - **Ingen**: datorer som inte uppfyller den här regeln rapporterar inte allvarlighets grad för Configuration Manager rapporter.

        - **Information**

        - **Honom**

        - **Kritisk**

        - **Kritisk med händelse**: datorer som inte uppfyller den här regeln rapporterar allvarlighets graden **kritisk** för Configuration Manager rapporter. Enheterna loggar också inkompatibla tillstånd som en Windows-händelse i program händelse loggen.

1. På sidan **Wi-Fi-profil** i guiden anger du följande information:

    - **Nätverks namn**: Ange det namn som enheterna ska visa som nätverks namn.

        > [!IMPORTANT]
        > Configuration Manager stöder inte apostrofer (`'`) eller kommatecken (`,`) i nätverks namnet.

    - **SSID**: Ange det Skift läges känsliga ID: t för det trådlösa nätverket.

    - **Anslut automatiskt när det här nätverket är inom räckhåll**
    - **Sök efter andra trådlösa nätverk medan du är ansluten till det här nätverket**
    - **Anslut när nätverket inte sänder sitt namn (SSID):**

1. På sidan **säkerhets konfiguration** anger du följande information:

    > [!IMPORTANT]
    > Om du skapar en Wi-Fi-profil för [lokal MDM](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md), stöder den aktuella grenen av Configuration Manager endast följande Wi-Fi-säkerhetskonfigurationer:  
    >
    > - Säkerhetstyper: **WPA2 Enterprise** eller **WPA2 Personal**  
    > - Krypteringstyper: **AES** eller **TKIP**  
    > - EAP-typer: **Smartkort eller annat certifikat** eller **PEAP**  

    - **Säkerhets typ**: Välj det säkerhets protokoll som används i det trådlösa nätverket, eller Välj **Ingen autentisering (öppen)** om nätverket är oskyddat.

    - **Kryptering**: om säkerhets typen stöder det kan du ange krypterings metod för det trådlösa nätverket.

    - **EAP-typ**: Välj autentiseringsprotokollet för den valda krypterings metoden.

        > [!NOTE]
        > Endast för Windows Phone enheter: det går inte att avsätta EAP-typerna **kliv** och **EAP-fast** .

        Välj **Konfigurera** för att ange egenskaper för den valda EAP-typen. Det här alternativet är inte tillgängligt för vissa valda EAP-typer.

        > [!IMPORTANT]
        > Konfigurations fönstret för EAP-typ är från Windows. Kontrol lera att du kör Configuration Manager-konsolen på en dator som har stöd för den valda EAP-typen.

    - **Spara autentiseringsuppgifterna för varje inloggning**: Välj det här alternativet om du vill lagra autentiseringsuppgifter så att användarna inte behöver ange autentiseringsuppgifter för trådlöst nätverk varje gången de loggar in på Windows.

1. På sidan **Avancerade inställningar** i guiden anger du ytterligare inställningar för Wi-Fi-profilen. De avancerade inställningarna kanske inte är tillgängliga eller kan variera beroende på vilka alternativ du väljer på sidan **säkerhets konfiguration** i guiden. Till exempel autentiserings läge eller alternativ för enkel inloggning.

1. Om det trådlösa nätverket använder en proxyserver på sidan **proxyinställningar** väljer du alternativet för att **Konfigurera proxyinställningar för den här Wi-Fi-profilen**. Ange sedan konfigurations informationen för proxyservern.

1. På sidan **plattformar som stöds** väljer du de OS-versioner där Wi-Fi-profilen är tillämplig.

1. Slutför guiden.

## <a name="next-step"></a>Nästa steg

> [!div class="nextstepaction"]
> [Så här distribuerar du Wi-Fi-profiler](deploy-wifi-vpn-email-cert-profiles.md)
