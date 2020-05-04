---
title: Planera klient distribution till Linux-och UNIX-datorer
titleSuffix: Configuration Manager
description: Planera för klient distribution till Linux-och UNIX-datorer i Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 44153689-70e8-42ad-9ae8-17ae35f6a2e3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: dfede7594224ff48af2a1e4066e69d551c3c576e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713235"
---
# <a name="planning-for-client-deployment-to-linux-and-unix-computers-in-configuration-manager"></a>Planera för klient distribution till Linux-och UNIX-datorer i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

> [!Important]  
> Från och med version 1902 stöder Configuration Manager inte Linux-eller UNIX-klienter. 
> 
> Överväg Microsoft Azure hantering för hantering av Linux-servrar. Azure-lösningar har omfattande Linux-support som i de flesta fall överskrider Configuration Manager-funktioner, inklusive slut punkt till slut punkt för korrigerings hantering för Linux.

Du kan installera Configuration Manager-klienten på datorer som kör Linux eller UNIX. Den här klienten är utformad för servrar som fungerar som en arbets grupps dator och klienten har inte stöd för interaktion med inloggade användare. När du har installerat klient program varan och klienten upprättar kommunikation med Configuration Manager-platsen hanterar du klienten med hjälp av Configuration Manager-konsolen och rapporter.  

> [!NOTE]
>  Configuration Manager-klienten för Linux-och UNIX-datorer stöder inte följande hanterings funktioner:  
> 
> - Push-installation av klient  
>   -   Distribution av operativsystem  
>   -   Programdistribution; distribuera i stället programvara med hjälp av paket och program.  
>   -   Programvaruinventering  
>   -   Programuppdateringar  
>   -   Kompatibilitetsinställningar  
>   -   Fjärrstyrning  
>   -   Energisparfunktioner  
>   -   Klientkontroll och reparation av klientstatus  
>   -   Internetbaserad klienthantering  

 Information om vilka Linux-och UNIX-distributioner som stöds och vilken maskin vara som krävs för att stödja klienten för Linux och UNIX finns i [Rekommenderad maskin vara för Configuration Manager](../../../../core/plan-design/configs/recommended-hardware.md).  

 Använd informationen i den här artikeln för att få hjälp att planera distributionen av Configuration Manager-klienten för Linux och UNIX.  

##  <a name="prerequisites-for-client-deployment-to-linux-and-unix-servers"></a><a name="BKMK_ClientDeployPrereqforLnU"></a>Krav för klient distribution till Linux-och UNIX-servrar  
 Använd följande information för att avgöra vilka krav som måste uppfyllas för installation av klienten på Linux och UNIX.  

###  <a name="dependencies-external-to-configuration-manager"></a><a name="BKMK_ClientDeployExternalforLnU"></a>Externa beroenden till Configuration Manager:  
 I följande tabeller beskrivs de UNIX- och Linux-operativsystem och paketberoenden som krävs.  

 **Red Hat Enterprise Linux Server Release 5.1 (Tikanga)**  

|Nödvändigt paket|Beskrivning|Lägsta version|  
|----------------------|-----------------|---------------------|  
|glibc|C-standardbibliotek|2.5-12|  
|Openssl|OpenSSL-bibliotek, Secure Network Communications Protocol|0.9.8b-8.3.el5|  
|PAM|Pluggable Authentication Modules|0.99.6.2-3.14.el5|  

 **Red Hat Enterprise Linux Server Release 6**  

|Nödvändigt paket|Beskrivning|Lägsta version|  
|----------------------|-----------------|---------------------|  
|glibc|C-standardbibliotek|2.12-1.7|  
|Openssl|OpenSSL-bibliotek, Secure Network Communications Protocol|1.0.0-4|  
|PAM|Pluggable Authentication Modules|1.1.1-4|  

 **Red Hat Enterprise Linux Server Release 7**  

|Nödvändigt paket|Beskrivning|Lägsta version|  
|----------------------|-----------------|---------------------|  
|glibc|C-standardbibliotek|2.17|  
|Openssl|OpenSSL-bibliotek, Secure Network Communications Protocol|1.0.1|  
|PAM|Pluggable Authentication Modules|1.1.1-4|  

 **Solaris 10 SPARC**  

|Nödvändigt paket|Beskrivning|Lägsta version|  
|----------------------|-----------------|---------------------|  
|Nödvändig operativsystemskorrigering|PAM-minnesläcka|117463-05|  
|SUNWlibC|Sun Workshop Compilers Bundled libC (sparc)|5.10, REV=2004.12.22|  
|SUNWlibms|Math & Microtasking Libraries (Usr) (sparc)|5.10, REV=2004.11.23|  
|SUNWlibmsr|Math & Microtasking Libraries (Root) (sparc)|5.10, REV=2004.11.23|  
|SUNWcslr|Core Solaris Libraries (Root) (sparc)|11.10.0, REV=2005.01.21.15.53|  
|SUNWcsl|Core Solaris Libraries (Root) (sparc)|11.10.0, REV=2005.01.21.15.53|  
|OpenSSL|SUNopenssl-librararies (Usr)<br /><br /> Sun innehåller OpenSSL-bibliotek för Solaris 10 SPARC. De ingår i operativsystemet.|11.10.0,REV=2005.01.21.15.53|  
|PAM|Pluggable Authentication Modules<br /><br /> SUNWcsr, Core Solaris, (Root) (sparc)|11.10.0, REV=2005.01.21.15.53|  

 **Solaris 10 x86**  

|Nödvändigt paket|Beskrivning|Lägsta version|  
|----------------------|-----------------|---------------------|  
|Nödvändig operativsystemskorrigering|PAM-minnesläcka|117464-04|  
|SUNWlibC|Sun Workshop Compilers Bundled libC (i386)|5.10, REV=2004.12.20|  
|SUNWlibmsr|Math & Microtasking Libraries (Root) (i386)|5.10, REV=2004.12.18|  
|SUNWcsl|Core Solaris, (Shared Libs) (i386)|11.10.0, REV=2005.01.21.16.34|  
|SUNWcslr|Core Solaris Libraries (Root) (i386)|11.10.0, REV=2005.01.21.16.34|  
|OpenSSL|SUNWopenssl-libraries; OpenSSL Libraries (Usr) (i386)|11.10.0, REV=2005.01.21.16.34|  
|PAM|Pluggable Authentication Modules<br /><br /> SUNWcsr Core Solaris, (Root)(i386)|11.10.0, REV=2005.01.21.16.34|  

 **Solaris 11 SPARC**  

|Nödvändigt paket|Beskrivning|Lägsta version|  
|----------------------|-----------------|---------------------|  
|SUNWlibC|Sun Workshop Compilers Bundled libC|5.11, REV=2011.04.11|  
|SUNWlibmsr|Math & Microtasking Libraries (Rot)|5.11, REV=2011.04.11|  
|SUNWcslr|Core Solaris Libraries (Rot)|11.11, REV=2009.11.11|  
|SUNWcsl|Core Solaris, (Shared Libs)|11.11, REV=2009.11.11|  
|SUNWcsr|Core Solaris, (Rot)|11.11, REV=2009.11.11|  
|SUNWopenssl-libraries|OpenSSL Libraries (Usr)|11.11.0, REV=2010.05.25.01.00|  

 **Solaris 11 x86**  

|Nödvändigt paket|Beskrivning|Lägsta version|  
|----------------|-----------|---------------|  
|SUNWlibC|Sun Workshop Compilers Bundled libC|5.11, REV=2011.04.11|  
|SUNWlibmsr|Math & Microtasking Libraries (Rot)|5.11, REV=2011.04.11|  
|SUNWcslr|Core Solaris Libraries (Rot)|11.11, REV=2009.11.11|  
|SUNWcsl|Core Solaris, (Shared Libs)|11.11, REV=2009.11.11|  
|SUNWcsr|Core Solaris, (Rot)|11.11, REV=2009.11.11|  
|SUNWopenssl-libraries|OpenSSL Libraries (Usr)|11.11.0, REV=2010.05.25.01.00|  


 **SUSE Linux Enterprise Server 10 SP1 (i586)**  

|Nödvändigt paket|Beskrivning|Lägsta version|  
|----------------------|-----------------|---------------------|  
|glibc-2.4-31.30|Delat C-standardbibliotek|2.4-31.30|  
|OpenSSL|OpenSSL-bibliotek, Secure Network Communications Protocol|0.90,8a-18,15|  
|PAM|Pluggable Authentication Modules|0.99.6.3-28.8|  

 **SUSE Linux Enterprise Server 11 (i586)**  

|Nödvändigt paket|Beskrivning|Lägsta version|  
|----------------------|-----------------|---------------------|  
|glibc-2.9-13.2|Delat C-standardbibliotek|2.9-13.2|  
|PAM|Pluggable Authentication Modules|pam-1.0.2-20.1|  

 **Universal Linux (Debian-paket) Debian, Ubuntu Server**  

|Nödvändigt paket|Beskrivning|Lägsta version|  
|----------------------|-----------------|---------------------|  
|libc6|Delat C-standardbibliotek|2.3.6|  
|OpenSSL|OpenSSL-bibliotek, Secure Network Communications Protocol|0.9.8 eller 1.0|  
|PAM|Pluggable Authentication Modules|0.79-3|  

 **Universal Linux (RPM-paket) CentOS, Oracle Linux**  

|Nödvändigt paket|Beskrivning|Lägsta version|  
|----------------------|-----------------|---------------------|  
|glibc|Delat C-standardbibliotek|2.5-12|  
|OpenSSL|OpenSSL-bibliotek, Secure Network Communications Protocol|0.9.8 eller 1.0|  
|PAM|Pluggable Authentication Modules|0.99.6.2-3.14|  


 **IBM AIX 6.1**  

|Nödvändigt paket|Beskrivning|Lägsta version|  
|----------------------|-----------------|---------------------|  
|OS-version|Version av operativsystemet|AIX 6,1: alla teknik nivåer och Service Pack|  
|xlC.rte|XL C/C++ Runtime|9.0.0.5|  
|OpenSSL/openssl.base|OpenSSL-bibliotek, Secure Network Communications Protocol|0.9.8.4|  

 **IBM AIX 7.1 (Power)**  

|Nödvändigt paket|Beskrivning|Lägsta version|  
|----------------------|-----------------|---------------------|  
|OS-version|Version av operativsystemet|AIX 7,1: alla teknik nivåer och Service Pack|  
|xlC.rte|XL C/C++ Runtime||  
|OpenSSL/openssl.base|OpenSSL-bibliotek, Secure Network Communications Protocol||  


 **HP-UX 11i v3 IA64**  

|Nödvändigt paket|Beskrivning|Lägsta version|  
|----------------------|-----------------|---------------------|  
|HPUX11i-OE|HP-UX Foundation Operating Environment|B.110,310,0709|  
|OS-Core.MinimumRuntime.CORE-SHLIBS|Specifika IA-utvecklingsbibliotek|B.110,31|  
|SysMgmtMin|Lägsta programdistribueringsverktyg|B.110,310,0709|  
|SysMgmtMin.openssl|OpenSSL-bibliotek, Secure Network Communications Protocol|A.00.09.08d.002|  
|PAM|Pluggable Authentication Modules|I HP-UX är PAM del av operativsystemets kärnkomponenter. Det finns inga andra beroenden.|  

 **Configuration Manager beroenden:** I följande tabell visas de plats system roller som stöder Linux-och UNIX-klienter. Mer information om dessa plats system roller finns i [bestämma plats system roller för Configuration Manager klienter](../../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md).  

|Configuration Manager plats system|Mer information|  
|---------------------------------------|----------------------|  
|Hanteringsplats|Även om det inte krävs någon hanterings plats för att installera en Configuration Manager-klient för Linux och UNIX måste du ha en hanterings plats för att överföra information mellan klient datorer och Configuration Manager-servrar. Utan hanterings plats kan du inte hantera klient datorer.|  
|Distributionsplats|Distributions platsen krävs inte för att installera en Configuration Manager-klient för Linux och UNIX. Platssystemrollen krävs dock om du distribuerar programvara till Linux- och UNIX-servrar.<br /><br /> Eftersom Configuration Manager-klienten för Linux och UNIX inte har stöd för kommunikation som använder SMB, måste de distributions platser som du använder med klienten ha stöd för HTTP-eller HTTPS-kommunikation.|  
|Status för återställningsplats|Återställnings status punkten krävs inte för att installera en Configuration Manager-klient för Linux och UNIX. Återställnings status punkten gör det dock möjligt för datorer på Configuration Manager-platsen att skicka tillstånds meddelanden när de inte kan kommunicera med en hanterings plats. Klienten kan även skicka status för installationen till återställningsstatuspunkten.|  

 **Brand Väggs krav**: se till att brand väggar inte blockerar kommunikation mellan de portar som du anger som klient begär ande portar. Klienten för Linux och UNIX kommunicerar direkt med hanteringsplatser, distributionsplatser och återställningsstatuspunkter.  

 Information om klientens kommunikation och begäran portar finns i [Konfigurera klienten för Linux och UNIX för att hitta hanteringsplatser](../../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md#BKMK_ConfigClientMP).  

##  <a name="planning-for-communication-across-forest-trusts-for-linux-and-unix-servers"></a><a name="BKMK_PlanningforCommunicationsforLnU"></a>Planera för kommunikation över skogs förtroenden för Linux-och UNIX-servrar  
 Linux-och UNIX-servrar som du hanterar med Configuration Manager fungerar som arbets grupps klienter och kräver liknande konfigurationer som Windows-baserade klienter som finns i en arbets grupp. Information om kommunikation från datorer som finns i arbets grupper finns i [kommunikation mellan Active Directory skogar](../../../plan-design/hierarchy/communications-between-endpoints.md#Plan_Com_X-Forest).  

###  <a name="service-location-by-the-client-for-linux-and-unix"></a><a name="BKMK_ServiceLocationforLnU"></a>Tjänst plats av klienten för Linux och UNIX  
 Uppgiften att hitta en platssystemserver som tillhandahåller tjänster för klienter kallas för tjänstlokalisering. Till skillnad från en Windows-baserad klient använder klienten för Linux och UNIX inte Active Directory för tjänst lokalisering. Dessutom stöder Configuration Manager-klienten för Linux och UNIX inte en klient egenskap som anger domänsuffixet för en hanterings plats. Klienten lär sig i stället om ytterligare platssystemservrar som tillhandahåller tjänster till klienter från en känd hanteringsplats som du tilldelar när du installerar klientprogrammet.  

 Mer information finns i [tjänst lokalisering och hur klienter avgör sina tilldelade hanterings platser](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location).  

##  <a name="planning-for-security-and-certificates-for-linux-and-unix-servers"></a><a name="BKMK_SecurityforLnU"></a>Planera för säkerhet och certifikat för Linux-och UNIX-servrar  
 För säker och autentiserad kommunikation med Configuration Manager-platser använder Configuration Manager-klienten för Linux och UNIX samma modell för kommunikation som Configuration Manager-klienten för Windows.  

 När du installerar Linux-och UNIX-klienten kan du tilldela klienten ett PKI-certifikat som gör det möjligt att använda HTTPS för att kommunicera med Configuration Manager-platser. Om du inte tilldelar ett PKI-certifikat skapar klienten ett självsignerat certifikat och kommunicerar endast med HTTP.  

 Klienter som tilldelas ett PKI-certifikat under installationen använder HTTPS för att kommunicera med hanteringsplatser. Om en klient inte kan hitta en hanteringsplats som har stöd för HTTPS går den tillbaka till att använda HTTP med det angivna PKI-certifikatet.  

 När en Linux-eller UNIX-klient använder ett PKI-certifikat behöver du inte godkänna dem. När en klient använder ett självsignerat certifikat granskar du inställningarna för hierarkin för klient godkännande i Configuration Manager-konsolen. Om klientgodkännandemetoden inte är **Godkänn automatiskt alla datorer (rekommenderas inte)** måste du godkänna klienten manuellt.  

 Mer information om hur du godkänner klienten manuellt finns i [Hantera klienter från noden enheter](../../manage/manage-clients.md#BKMK_ManagingClients_DevicesNode).  

 Information om hur du använder certifikat i Configuration Manager finns i [krav för PKI-certifikat](../../../plan-design/network/pki-certificate-requirements.md).  

###  <a name="about-certificates-for-use-by-linux-and-unix-servers"></a><a name="BKMK_AboutCertsforLnU"></a>Om certifikat som ska användas av Linux-och UNIX-servrar  
 Configuration Manager-klienten för Linux och UNIX använder ett självsignerat certifikat eller ett X. 509 PKI-certifikat precis som Windows-baserade klienter. Det finns inga ändringar i PKI-kraven för Configuration Manager plats system när du hanterar Linux-och UNIX-klienter.  

 De certifikat som du använder för Linux-och UNIX-klienter som kommunicerar med Configuration Manager-plats system måste vara i formatet PKCS # 12 (Public Key Certificate Standard), och lösen ordet måste vara känt så att du kan ange det för klienten när du anger PKI-certifikatet.  

 Configuration Manager-klienten för Linux och UNIX har stöd för ett enda PKI-certifikat och har inte stöd för flera certifikat. Därför gäller inte certifikat urvalskriterierna som du konfigurerar för en Configuration Manager plats.  

###  <a name="configuring-certificates-for-linux-and-unix-servers"></a><a name="BKMK_ConfigCertsforLnU"></a>Konfigurera certifikat för Linux-och UNIX-servrar  
 Om du vill konfigurera en Configuration Manager-klient för Linux-och UNIX-servrar för att använda HTTPS-kommunikation måste du konfigurera klienten så att den använder ett PKI-certifikat när du installerar klienten. Du kan inte etablera ett certifikat innan du installerar klient programmet.  

 När du installerar en klient som använder ett PKI-certifikat använder du kommando rads parametern `-UsePKICert` för att ange plats och namn för en PKCS # 12-fil som innehåller PKI-certifikatet. Dessutom måste du använda kommando rads parametern `-certpw` för att ange lösen ordet för certifikatet.  

 Om du inte anger `-UsePKICert`genererar klienten ett självsignerat certifikat och försöker kommunicera med plats system servrar genom att endast använda http.  

##  <a name="versions-that-dont-support-sha-256"></a><a name="BKMK_NoSHA-256"></a>Versioner som inte stöder SHA-256  
 Följande Linux-och UNIX-operativsystem som stöds som klienter för Configuration Manager släpptes med versioner av OpenSSL som inte stöder SHA-256:  

-   Solaris, version 10 (SPARC/x86)  


 Om du vill hantera dessa operativ system med Configuration Manager måste du installera Configuration Manager-klienten för Linux och UNIX med en kommando rads växel som instruerar klienten att hoppa över validering av SHA-256. Configuration Manager-klienter som körs på dessa versioner av operativ systemet fungerar i ett mindre säkert läge än klienter som har stöd för SHA-256. Det här mindre säkra läget fungerar på följande sätt:  

-   Klienterna verifierar inte plats serverns signatur som är associerad med principen som de begär från en hanterings plats.  

-   Klienterna validerar inte hashvärdet för paket som de hämtar från en distributions plats.  

> [!IMPORTANT]  
>  Med `ignoreSHA256validation` alternativet kan du köra klienten för Linux-och UNIX-datorer i ett mindre säkert läge. Det här är avsett att användas på äldre plattformar som inte omfattar stöd för SHA-256. Detta är en säkerhetsåsidosättning som inte rekommenderas av Microsoft, men som stöds för användning i en säker och betrodd datacentermiljö.  

 När Configuration Manager-klienten för Linux och UNIX installeras kontrollerar installations skriptet operativ systemets version. Om operativ systemets version identifieras som frigjord utan en version av OpenSSL som har stöd för SHA-256 Miss lyckas installationen av den Configuration Manager klienten.  

 Om du vill installera Configuration Manager-klienten på Linux-och UNIX-operativsystem som inte släpptes med en version av OpenSSL som har stöd för SHA-256, måste du använda kommando `ignoreSHA256validation`rads växeln install. När du använder det här kommando rads alternativet på ett tillämpligt Linux-eller UNIX-operativsystem hoppar Configuration Manager-klienten över SHA-256-validering och efter installationen använder klienten SHA-256 för att signera data som skickas till plats system med hjälp av HTTP. Information om hur du konfigurerar Linux-och UNIX-klienter för att använda certifikat finns i [Planera för säkerhet och certifikat för Linux-och UNIX-servrar](#BKMK_SecurityforLnU). Mer information om hur du kräver SHA-256 finns i [Konfigurera signering och kryptering](../../../plan-design/security/configure-security.md#BKMK_ConfigureSigningEncryption).  

> [!NOTE]  
>  Kommando rads alternativet `ignoreSHA256validation` ignoreras på datorer som kör en version av Linux och UNIX som släpps med versioner av OpenSSL som har stöd för SHA-256.  
