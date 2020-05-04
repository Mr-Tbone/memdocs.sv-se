---
title: Hantera Linux-och UNIX-klienter
titleSuffix: Configuration Manager
description: Hantera klienter på Linux-och UNIX-servrar i Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 948664f2-239d-47a8-92fc-f8efeebd5796
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 716441bd146e9172b3f183c497fcaa4036ad0084
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710645"
---
# <a name="how-to-manage-clients-for-linux-and-unix-servers-in-configuration-manager"></a>Hantera klienter för Linux-och UNIX-servrar i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

> [!Important]  
> Från och med version 1902 stöder Configuration Manager inte Linux-eller UNIX-klienter. 
> 
> Överväg Microsoft Azure hantering för hantering av Linux-servrar. Azure-lösningar har omfattande Linux-support som i de flesta fall överskrider Configuration Manager-funktioner, inklusive slut punkt till slut punkt för korrigerings hantering för Linux.

När du hanterar Linux-och UNIX-servrar med Configuration Manager kan du konfigurera samlingar, underhålls perioder och klient inställningar som hjälper dig att hantera servrarna. Även om Configuration Manager-klienten för Linux och UNIX inte har något användar gränssnitt kan du tvinga klienten att söka efter klient principen manuellt.

##  <a name="collections-of-linux-and-unix-servers"></a><a name="BKMK_CollectionsforLnU"></a> Collections of Linux and UNIX servers  
 Använd samlingar för att hantera grupper av Linux-och UNIX-servrar på samma sätt som du använder samlingar för att hantera andra klient typer. Samlingar kan vara direkta medlemskaps samlingar eller frågebaserade samlingar. Frågebaserade samlingar identifierar klient operativ system, maskinvarukonfigurationer eller annan information om klienten som lagras i plats databasen. Du kan till exempel använda samlingar som innehåller Linux-och UNIX-servrar för att hantera följande inställningar:  

- Klientinställningar  

- Programdistributioner  

- Framtvinga underhållsperioder  

  Innan du kan identifiera en Linux-eller UNIX-klient med dess operativ system eller distribution måste du samla in [maskin varu inventering](../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md) från klienten.  

  Standard klient inställningarna för maskin varu inventering innehåller information om en klient dators operativ system. Du kan använda egenskapen **Beskrivning** för klassen **Operativsystem** för att identifiera operativsystemet på en Linux- eller UNIX-server.  

  Du kan visa information om datorer som kör Configuration Manager-klienten för Linux och UNIX i noden **enheter** i arbets ytan **till gångar och efterlevnad** i Configuration Manager-konsolen. På arbets ytan **till gångar och efterlevnad** i Configuration Manager-konsolen kan du se namnet på varje dators operativ system i kolumnen **operativ system** .  

  Som standard är Linux- och UNIX-servrar medlemmar i samlingen **Alla system** . Vi rekommenderar att du skapar anpassade samlingar som bara innehåller Linux-och UNIX-servrar eller en delmängd av dem. Med anpassade samlingar kan du hantera åtgärder som att distribuera program vara eller tilldela klient inställningar till grupper av liknande datorer, så att du korrekt kan mäta framgången för en distribution.   

  Lägg till frågor för medlemskapsregler som innehåller attributet Beskrivning för attributet Operativsystem när du skapar en anpassad samling för Linux- och UNIX-servrar. Information om hur du skapar samlingar finns i [skapa samlingar](../../../core/clients/manage/collections/create-collections.md).  

##  <a name="maintenance-windows-for-linux-and-unix-servers"></a><a name="BKMK_MaintenanceWindowsforLnU"></a> Maintenance windows for Linux and UNIX servers  
 Configuration Manager-klienten för Linux-och UNIX-servrar har stöd för användning av [underhålls fönster](../../../core/clients/manage/collections/use-maintenance-windows.md). Detta stöd är oförändrat från Windows-baserade klienter.  

##  <a name="client-settings-for-linux-and-unix-servers"></a><a name="BKMK_ClientSettingsforLnU"></a> Client settings for Linux and UNIX servers  
 Du kan [Konfigurera klient inställningar](../../../core/clients/deploy/configure-client-settings.md) som gäller för Linux-och UNIX-servrar på samma sätt som du konfigurerar inställningar för andra klienter.  

 **Standardinställning för klientagent** tillämpas på Linux- och UNIX-servrar som standard. Du kan också skapa anpassade klient inställningar och distribuera dem till samlingar med vissa klienter.  

 Det finns inga ytterligare inställningar som endast gäller för Linux- och UNIX-klienter. Det finns dock standard klient inställningar som inte gäller för Linux-och UNIX-klienter. Klienten för Linux och UNIX använder bara inställningar för funktioner som stöds.  

 Till exempel ignoreras en anpassad klienten hets inställning som aktiverar och konfigurerar inställningar för fjärr styrning av Linux-och UNIX-servrar, eftersom klienten för Linux och UNIX inte stöder fjärr styrning.  

##  <a name="computer-policy-for-linux-and-unix-servers"></a><a name="BKMK_PolicyforLnU"></a>Dator princip för Linux-och UNIX-servrar  
 Klienten för Linux-och UNIX-servrar avsöker regelbundet sin plats efter dator principer för att lära sig om begärda konfigurationer och för att söka efter distributioner.  

 Du kan också tvinga klienten på en Linux- eller UNIX-server att genast söka efter datorprinciper. Det gör du genom att använda autentiseringsuppgifter för **roten** på-servern för att köra följande kommando: **/opt/microsoft/configmgr/bin/ccmexec-RS-princip**  

 Information om sökningen efter datorprinciper registreras i den delade klientloggfilen, **scxcm.log**.  

> [!NOTE]  
>  Configuration Manager-klienten för Linux och UNIX begär eller bearbetar aldrig användar principer.  

##  <a name="how-to-manage-certificates-on-the-client-for-linux-and-unix"></a><a name="BKMK_ManageLinuxCerts"></a>Hantera certifikat på klienten för Linux och UNIX  
 När du har installerat klienten för Linux och UNIX kan du använda verktyget **certutil** för att uppdatera klienten med ett nytt PKI-certifikat och för att importera en ny lista över återkallade certifikat (CRL). När du installerar-klienten för Linux och UNIX placeras det här verktyget i `/opt/microsoft/configmgr/bin/certutil`. 

 Om du vill hantera certifikat kör du certutil på varje klient med något av följande alternativ:  

|Alternativ|Mer information|  
|------------|----------------------|  
|`importPFX`|Använd det här alternativet om du vill ange ett certifikat som ska ersätta det certifikat som för närvarande används av en klient.<br /><br /> När du använder `-importPFX`måste du också använda `-password` kommando rads parametern för att ange lösen ordet som är kopplat till PKCS # 12-filen.<br /><br /> Använd `-rootcerts` för att ange ytterligare krav för rot certifikat.<br /><br /> Exempel: `certutil -importPFX <path to the PKCS#12 certificate> -password <certificate password> [-rootcerts <comma-separated list of certificates>]`|  
|`importsitecert`|Använd det här alternativet om du vill uppdatera platsserverns signeringscertifikat som finns på hanteringsservern.<br /><br /> Exempel: `certutil -importsitecert <path to the DER certificate>`|  
|`importcrl`|Använd det här alternativet om du vill uppdatera listan över återkallade certifikat (CRL) på klienten med en eller flera CRL-filsökvägar.<br /><br /> Exempel: `certutil -importcrl <comma separated CRL file paths>`|  
