---
title: Planera klient distribution till Windows Embedded-enheter
titleSuffix: Configuration Manager
description: Planera för klient distribution till Windows Embedded-enheter i Configuration Manager.
ms.date: 06/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 038e61f9-f49d-41d1-9a9f-87bec9e00d5d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7848e3c0c38391ab61d10ad46cbb772c812539c7
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906648"
---
# <a name="planning-for-client-deployment-to-windows-embedded-devices-in-configuration-manager"></a>Planera för klient distribution till Windows Embedded-enheter i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

<a name="BKMK_DeployClientEmbedded"></a>Om din Windows Embedded-enhet inte innehåller Configuration Manager-klienten, kan du använda valfri klient installations metod om enheten uppfyller de nödvändiga beroendena. Om den inbäddade enheten har stöd för skrivfilter måste du inaktivera dessa filer innan du installerar klienten, och sedan återaktivera filtren igen när klienten har installerats och tilldelats en plats.  

 Tänk på att om du inaktiverar filtren bör du inte inaktivera filterdrivrutinerna. Dessa drivrutiner startas normalt automatiskt när datorn startas. Om drivrutinerna inaktiveras kan det antingen förhindra att klienten installeras eller så kan det störa orkestrering av skrivfilter, vilket gör att klientåtgärderna misslyckas. Det här är de tjänster som är kopplade till varje skrivfiltertyp som måste fortsätta att köras:  

|Skrivfiltertyp|Drivrutin|Typ|Beskrivning|  
|-----------------------|------------|----------|-----------------|  
|EWF|EWF|Kernel|Implementerar I/O-omdirigering på sektornivå på skyddade volymer.|  
|FBWF|FBWF|Filsystem|Implementerar I/O-omdirigering på filnivå på skyddade volymer.|  
|UWF|uwfreg|Kernel|UWF-registeromdirigerare|  
|UWF|uwfs|Filsystem|UWF-filomdirigerare|  
|UWF|uwfvol|Kernel|UWF-volymhanterare|  

 Skrivfiltren kontrollerar hur operativsystemet på den inbäddade enheten uppdateras när du gör ändringar, exempelvis när du installera programvara. Om skrivfilter är aktiverade dirigeras ändringarna om till ett tillfälligt överlägg, i stället för att ändringarna görs direkt i operativsystemet. Om ändringarna enbart skrivs till överlägget går de förlorade om den inbäddade enheten stängs av. Om skrivfilten inaktiveras tillfälligt kan ändringarna dock göras permanenta så att du inte behöver göra ändringarna igen (eller installera om programvaran) varje gång den inbäddade enheten startar om. Att tillfälligt inaktivera och sedan återaktivera skrivfilten kräver dock en eller flera omstarter. Det går att kontrollera när detta sker, genom att konfigurera underhållsfönster så att omstarterna äger rum utanför kontorstid, vilket är en praktisk lösning.  

 Du kan konfigurera alternativ för att automatiskt inaktivera och återaktivera skrivfiltren när du distribuerar programvara som applikationer, aktivitetssekvenser, programuppdateringar och Endpoint Protection-klienten. Undantaget är konfigurationsbaslinjer med konfigurationsobjekt som använder automatisk reparation. I det här scenariot sker alltid reparationen i överlägget så att den är tillgänglig först när enheten startas om. Reparationen tillämpas igen vid nästa utvärderingscykel, men enbart på överlägget, som rensas vid omstart. Om du vill tvinga Configuration Manager att genomföra reparations ändringarna kan du distribuera konfigurations bas linjen och sedan en annan program distribution som har stöd för att genomföra ändringen så snart som möjligt.  

 Om skrivfilten är inaktiverade kan du installera programvaran på Windows Embedded-enheterna med hjälp av Software Center. Men om Skriv filtren är aktiverade, Miss lyckas installationen och Configuration Manager visar ett fel meddelande om att du inte har tillräcklig behörighet för att installera programmet.  

> [!WARNING]  
>  Även om du inte väljer Configuration Manager alternativ för att genomföra ändringarna, kan ändringarna genomföras om en annan program varu installation eller ändring görs som genomför ändringar. I detta scenario sparas de ursprungliga ändringarna, förutom de nya ändringarna.  

 När Configuration Manager inaktiverar Skriv filtren för att göra ändringar permanenta, kan endast användare som har lokala administratörs rättigheter logga in och använda den inbäddade enheten. Under den här perioden blir användare med begränsade rättigheter utelåsta, och det visas ett meddelande om att datorn inte är tillgänglig eftersom underhåll utförs på den. Detta bidrar till att skydda enheten när den är i ett tillstånd där ändringar kan tillämpas permanent, och detta utelåsningsbeteende i serviceläget är ett annat skäl att konfigurera ett underhållsfönster under en tid då användarna inte kommer att logga in till dessa enheter.  

 Configuration Manager stöder hantering av följande typer av Skriv filter:  

- Filbaserat Skriv filter (FBWF) – mer information finns i [filbaserat Skriv filter](https://docs.microsoft.com/previous-versions/windows/embedded/aa940926(v=winembedded.5)).  

- Förbättrat Skriv filter (EWF) RAM – mer information finns i [förbättrat Skriv filter](https://docs.microsoft.com/previous-versions/windows/embedded/ms912906(v=winembedded.5)).  

- Enhetligt Skriv filter (UWF) – mer information finns i [enhetligt Skriv filter](https://docs.microsoft.com/windows-hardware/customize/enterprise/unified-write-filter).  

  Configuration Manager stöder inte Skriv filter åtgärder när Windows Embedded-enheten är i EWF RAM-läge.  

> [!IMPORTANT]
>  Om du har valt kan du använda filbaserade Skriv filter (FBWF) med Configuration Manager för ökad effektivitet och högre skalbarhet.
> 
> **För enheter som endast använder FBWF:** Konfigurera följande undantag för att spara klient tillstånd och inventerings data mellan omstarter av enheter:  
> 
> - CCMINSTALLDIR \\ *. SDF  
>   -   CCMINSTALLDIR\ServiceData  
>   -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\StateSystem  
> 
>   Enheter som kör Windows Embedded 8.0 och senare har inte stöd för undantag som innehåller jokertecken. På dessa enheter måste du konfigurera följande undantag enskilt:  
> 
> - Alla filer i CCMINSTALLDIR med tillägget .sdf, normalt:  
> 
>   -   UserAffinityStore.sdf  
>   -   InventoryStore.sdf  
>   -   CcmStore.sdf  
>   -   StateMessageStore.sdf  
>   -   CertEnrollmentStore.sdf  
>   -   CCMINSTALLDIR\ServiceData  
>   -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\StateSystem  
> 
> **För enheter som endast använder FBWF och UWF:** När klienter i en arbets grupp använder certifikat för autentisering till hanterings platser måste du också utesluta den privata nyckeln för att säkerställa att klienten fortsätter att kommunicera med hanterings platsen. Konfigurera följande undantag på dessa enheter:  
> 
> - c:\Windows\System32\Microsoft\Protect  
>   -   c:\ProgramData\Microsoft\Crypto  
>   -   HKEY_LOCAL_MACHINE\Software\Microsoft\SystemCertificates\SMS\Certificates  

> [!NOTE]
> Inga ytterligare undantag krävs av Configuration Manager-klienten förutom de som dokumenteras i den **viktiga** rutan ovan. Om du lägger till ytterligare Configuration Manager eller WMI (WBEM) relaterade undantag kan det leda till fel i Configuration Manager inklusive enheter som fastnar i behandlings läge eller enheter som har startats om. Undantag som inte behövs omfattar Configuration Manager-CCMcache, katalogen CCMSetup, katalogen CCMSetup, katalogen för aktivitetssekvensen, WBEM-katalogen och Configuration Manager relaterade register nycklar.

 Ett exempel scenario för att distribuera och hantera Write-filter-aktiverade Windows Embedded-enheter i Configuration Manager finns i [exempel scenario för att distribuera och hantera Configuration Manager-klienter på Windows Embedded-enheter](../../../../core/clients/deploy/example-scenario-for-deploying-and-managing-clients-on-windows-embedded-devices.md).  

 Mer information om hur du bygger avbildningar för Windows Embedded-enheter och konfigurerar skrivfilter finns i dokumentationen till Windows Embedded. Du kan även kontakta komponenttillverkaren.  

> [!NOTE]
>  Om du väljer lämpliga plattformar för programvarudistributioner och konfigurationsobjekt visar dessa Windows Embedded-familjerna i stället för de specifika versionerna. Använd följande lista för att mappa de specifika versionerna av Windows Embedded till alternativen i listrutan:  
> 
> - **Embedded-operativsystem baserade på Windows XP (32 bitar)** innehåller följande:  
> 
>   -   Windows XP Embedded  
>   -   Windows Embedded för Point of Service  
>   -   Windows Embedded Standard 2009  
>   -   Windows Embedded POSReady 2009  
>   -   **Embedded-operativsystem som bygger på Windows 7 (32 bitar)** innehåller följande:  
> 
>   -   Windows Embedded Standard 7 (32 bitar)  
>   -   Windows Embedded POSReady 7 (32 bitar)  
>   -   Windows ThinPC  
>   -   **Embedded-operativsystem som bygger på Windows 7 (64-bitars)** innehåller följande:  
> 
>   -   Windows Embedded Standard 7 (64-bitars)  
>   -   Windows Embedded POSReady 7 (64-bitars)
