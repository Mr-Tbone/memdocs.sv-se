---
title: Maskinvaruinventering för Linux och UNIX
titleSuffix: Configuration Manager
description: Lär dig hur du använder maskin varu inventering för Linux och UNIX i Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1026d616-2a20-4fb2-8604-d331763937f8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 84f4b822475111352c5dcf23f4868a1fa43ec3a7
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906270"
---
# <a name="hardware-inventory-for-linux-and-unix-in-configuration-manager"></a>Maskin varu inventering för Linux och UNIX i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

> [!Important]  
> Från och med version 1902 stöder Configuration Manager inte Linux-eller UNIX-klienter. 
> 
> Överväg Microsoft Azure hantering för hantering av Linux-servrar. Azure-lösningar har omfattande Linux-support som i de flesta fall överskrider Configuration Manager-funktioner, inklusive slut punkt till slut punkt för korrigerings hantering för Linux.

Configuration Manager-klienten för Linux och UNIX har stöd för maskin varu inventering. När du har samlat in maskin varu inventering kan du köra Visa inventering i resurs läsaren eller Configuration Manager rapporter och använda den här informationen för att skapa frågor och samlingar som möjliggör följande åtgärder:  

- Programvarudistribution  

- Framtvinga underhållsperioder  

- Distribuera anpassade klientinställningar  

Maskin varu inventering för Linux-och UNIX-servrar använder en standardbaserad Common Information Model-Server (CIM). CIM-servern körs som en programvarutjänst (eller daemon) och ger en hanteringsinfrastruktur som bygger på DMTF-standarder (Distributed Management Task Force). CIM-servern ger funktioner som liknar de möjligheter i Windows Management Infrastructure (WMI) CIM som är tillgängliga på Windows-baserade datorer.  

Från och med Cumulative Update 1 använder klienten för Linux och UNIX **omiserver** -1.0.6 med öppen källkod från den **Öppna gruppen**. (Före Cumulative Update 1 använde klienten **nanowbem** som CIM-server).  

CIM-servern installeras som en del av klienten för Linux och UNIX. Klienten för Linux och UNIX kommunicerar direkt med CIM-servern och använder inte WS-MAN-gränssnittet på CIM-servern. WS-MAN-porten på CIM-servern inaktiveras när klienten installeras. Microsoft har utvecklat CIM-servern som nu finns tillgänglig som öppen källkod via projektet Open Management Infrastructure (OMI). Mer information om projektet Open Management Infrastructure finns på webbplatsen för [The Open Group](https://www.opengroup.org/) .  

Maskinvaruinventering på Linux- och UNIX-servrar fungerar genom att mappa befintliga Win32 WMI-klasser och -egenskaper till motsvarande klasser och egenskaper för Linux- och UNIX-servrar. Den här mappningen av klasser och egenskaper gör att maskin varu inventeringen Linux och UNIX kan integreras med Configuration Manager. Inventerings data från Linux-och UNIX-servrar visas tillsammans med inventering från Windows-baserade datorer i Configuration Manager-konsolen och rapporter. Det här beteendet ger en konsekvent heterogen hanterings upplevelse.  

> [!TIP]  
>  Du kan använda värdet **Beskrivning** för klassen **Operativsystem** för att identifiera Linux- och UNIX-operativsystem i frågor och samlingar.  

##  <a name="configuring-hardware-inventory-for-linux-and-unix-servers"></a><a name="BKMK_ConfigHardwareforLnU"></a> Konfigurera maskinvaruinventering för Linux- och UNIX-servrar  
 Du kan använda klientens standardinställningar eller skapa anpassade klientenhetsinställningar för att konfigurera maskinvaruinventering. När du använder anpassade klienten hets inställningar kan du konfigurera de klasser och egenskaper som du bara vill samla in från dina Linux-och UNIX-servrar. Du kan även ange anpassade scheman för när fullständiga inventeringar och förändringsinventeringar ska hämtas från Linux- och UNIX-servrar.  

 Klienten för Linux och UNIX har stöd för följande maskinvaruinventeringsklasser som är tillgängliga på Linux- och UNIX-servrar:  

- Win32_BIOS  

- Win32_ComputerSystem  

- Win32_DiskDrive  

- Win32_DiskPartition  

- Win32_NetworkAdapter  

- Win32_NetworkAdapterConfiguration  

- Win32_OperatingSystem  

- Win32_Process  

- Win32_Service  

- Win32Reg_AddRemovePrograms  

- SMS_LogicalDisk  

- SMS_Processor  

Alla egenskaper för dessa inventerings klasser är inte aktiverade för Linux-och UNIX-datorer i Configuration Manager.  

##  <a name="operations-for-hardware-inventory"></a><a name="BKMK_OperationsforHardwareforLnU"></a> Åtgärder för maskinvaruinventering  
 När du har hämtat maskinvaruinventering från Linux- och UNIX-servrar kan du visa och använda denna information på samma sätt som du visar inventeringar som hämtas från andra datorer:  

- Använd Resursläsaren om du vill visa detaljerad information om maskinvaruinventering från Linux- och UNIX-servrar  

- Skapa frågor baserat på specifika maskinvarukonfigurationer  

- Skapa frågebaserade samlingar som baseras på specifika maskinvarukonfigurationer  

- Kör rapporter som visar specifik information om maskinvarukonfigurationer  

Maskinvaruinventering på en Linux- eller UNIX-server körs enligt det schema du konfigurerar i klientinställningarna. Som standard är det här schemat var sjunde dag. Klienten för Linux och UNIX har stöd för både fullständig inventering och förändringsinventering.  

Du kan också tvinga klienten på en Linux- eller UNIX-server att genast köra maskinvaruinventering. Om du vill köra maskin varu inventering använder du autentiseringsuppgifter för **rot** på en klient för att köra följande kommando för att starta en maskin varu inventerings cykel:`/opt/microsoft/configmgr/bin/ccmexec -rs hinv`  

Åtgärder för maskinvaruinventering registreras i klientloggfilen **scxcm.log**.  

##  <a name="how-to-use-open-management-infrastructure-to-create-custom-hardware-inventory"></a><a name="BKMK_CustomHINVforLinux"></a> Så här använder du Open Management Infrastructure för att skapa anpassad maskinvaruinventering  
 Klienten för Linux och UNIX har stöd för anpassad maskinvaruinventering som du kan skapa med hjälp av Open Management Infrastructure (OMI). Det gör du genom att följa stegen nedan:  

1.  Skapa en anpassad inventeringsprovider med hjälp av OMI-källan  

2.  Konfigurera datorer för att använda den nya providern för att rapportera inventering  

3.  Aktivera Configuration Manager för att stödja den nya providern  

###  <a name="create-a-custom-hardware-inventory-provider-for-linux-and-unix-computers"></a><a name="BKMK_LinuxProvider"></a> Skapa en anpassad maskinvaruinventeringsprovider för Linux- och UNIX-datorer:  
 Om du vill skapa en anpassad Provider för maskin varu inventering för Configuration Manager-klienten för Linux och UNIX, använder du **OMI Source-v. 1.0.6** och följer instruktionerna från OMI komma igång-guiden. Den här processen omfattar att skapa en MOF-fil (Managed Object Format) som definierar schemat för den nya providern. Senare importerar du MOF-filen till Configuration Manager för att aktivera stöd för den nya anpassade inventerings klassen.  

 Både OMI Source - v.1.0.6 och Kom igång-guiden för OMI kan hämtas från webbplatsen för [The Open Group](https://github.com/microsoft/omi/blob/master/README.md) . Du hittar dessa hämtningsbara filer på fliken **Documents** (Dokument) på följande webbsida på webbplatsen OpenGroup.org: [Open Management Infrastructure (OMI)](https://collaboration.opengroup.org/omi/).  

###  <a name="configure-each-computer-that-runs-linux-or-unix-with-the-custom-hardware-inventory-provider"></a><a name="BKMK_AddProvidertoLinux"></a> Konfigurera varje dator som kör Linux eller UNIX med den anpassade maskinvaruinventeringsprovidern:  
 När du har skapat en anpassad inventeringsprovider måste du kopiera och sedan registrera providerns biblioteksfil på varje dator som har inventering som du vill hämta.  

1.  Kopiera providerbiblioteket till varje Linux- och UNIX-dator där du vill hämta inventering. Namnet på providerns bibliotek liknar följande namn: **XYZ_MyProvider. så**  

2.  Härnäst registrerar du providerbiblioteket med OMI-servern på varje Linux- och UNIX-dator. OMI-servern installeras på datorn när du installerar Configuration Manager-klienten för Linux och UNIX, men du måste registrera anpassade providrar manuellt. Använd följande kommando rad för att registrera providern:`/opt/microsoft/omi/bin/omireg XYZ_MyProvider.so`  

3.  När du har registrerat den nya providern testar du providern med hjälp av **omicli** -verktyget. **Omicli** -verktyget installeras på varje Linux-och UNIX-dator när du installerar Configuration Manager-klienten för Linux och UNIX. Där **XYZ_MyProvider** är namnet på den provider du har skapat kör du till exempel följande kommando på datorn: **/opt/microsoft/omi/bin/omicli ei root/cimv2 XYZ_MyProvider**  

     Information om **omicli** och test av anpassade providrar finns i Kom igång-guiden för OMI.  

> [!TIP]  
>  Använd programvarudistribution för att distribuera anpassade providrar och registrera anpassade providrar på varje Linux- och UNIX-klientdator.  

###  <a name="enable-the-new-inventory-class-in-configuration-manager"></a><a name="BKMK_AddLinuxProvidertoCM"></a> Aktivera den nya inventeringsklassen i Configuration Manager:  
 Innan Configuration Manager kan rapportera om inventering som rapporteras av den nya providern på Linux-och UNIX-datorer måste du importera Managed Object Format-filen (MOF) som definierar schemat för den anpassade providern.  

 Information om hur du importerar en anpassad MOF-fil till Configuration Manager finns i [så här konfigurerar du maskin varu inventering](../../../../core/clients/manage/inventory/configure-hardware-inventory.md).  
