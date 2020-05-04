---
title: Metod tips för klient distribution
titleSuffix: Configuration Manager
description: Få metod tips för klient distribution i Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a933d69c-5feb-4b2b-84e8-56b3b64d5947
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 28f8bfb2ef012fcd4f19835190b7c042d38fd9e0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713340"
---
# <a name="best-practices-for-client-deployment-in-configuration-manager"></a>Metod tips för klient distribution i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*


## <a name="use-software-update-based-client-installation-for-active-directory-computers"></a>Använda klientinstallation baserad på programuppdatering för Active Directory-datorer  
 Den här metoden för klient distribution använder befintliga Windows-tekniker, integreras med din Active Directory-infrastruktur, kräver minst konfiguration i Configuration Manager, är det enklaste sättet att konfigurera för brand väggar och är den säkraste. Genom att använda säkerhets grupper och WMI-filtrering för grupprincip konfiguration har du också stor flexibilitet för att kontrol lera vilka datorer som installerar Configuration Manager-klienten.  

 Mer information finns i [Så här installerar du Configuration Manager-klienter med programuppdateringsbaserad installation](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientSUP).  

## <a name="extend-the-active-directory-schema-and-publish-the-site-so-that-you-can-run-ccmsetup-without-command-line-options"></a>Utöka Active Directory-schemat och publicera platsen så att du kan köra CCMSetup utan kommandoradsalternativ  
 När du utökar Active Directory-schemat för Configuration Manager och platsen publiceras till Active Directory Domain Services publiceras många klient installations egenskaper till Active Directory Domain Services. Om en dator kan hitta de här klient installations egenskaperna kan den använda dem under Configuration Manager klient distributionen. Eftersom den här informationen genereras automatiskt elimineras risken för handhavarfel vid manuell inmatning av installationsegenskaper.  

 Mer information finns i [om klient installations egenskaper som publicerats till Active Directory Domain Services](../../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

## <a name="use-a-phased-rollout-to-manage-cpu-usage"></a>Använd en stegvis distribution för att hantera CPU-användning  
 Minimera effekterna av processor bearbetnings kraven på plats servern med hjälp av en stegvis distribution av klienter. Distribuera klienter utanför kontors tid så att andra tjänster har mer tillgänglig bandbredd under dagen och användarna inte störs om deras dator saktar ned eller kräver en omstart.  

## <a name="enable-automatic-upgrade-after-your-main-client-deployment-has-finished"></a>Aktivera automatisk uppgradering när huvuddistributionen av klienter är klar.  
 [Automatiska klient uppgraderingar](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md) är användbara när du vill uppgradera ett litet antal klient datorer som kan ha missats av din huvudsakliga klient installations metod, kanske på grund av att de var offline. 

> [!NOTE]  
>  Prestanda förbättringar i Configuration Manager kan göra att du kan använda automatiska uppgraderingar som en primär klient uppgraderings metod. Prestanda kommer dock att bero på infrastrukturen i din hierarki, t.ex. antalet klienter.  


## <a name="use-smsmp-and-fsp-if-you-install-the-client-with-clientmsi-properties"></a>Använd SMSMP och FSP om du installerar klienten med client.msi-egenskaper  
 Egenskapen SMSMP anger den ursprungliga hanteringsplatsen som klienten ska kommunicera med, och eliminerar beroendet av tjänstplatslösningar som t.ex. Active Directory Domain Services, DNS och WINS.  

 Använd egenskapen FSP och installera en återställningsstatusplats så att du kan övervaka klientinstallation och tilldelning och identifiera eventuella kommunikationsproblem.  

 Mer information om de här alternativen finns i [om klient installations egenskaper](../../../../core/clients/deploy/about-client-installation-properties.md).  

## <a name="install-client-language-packs-before-you-install-the-clients"></a>Installera klient språk paket innan du installerar klienterna  
Vi rekommenderar att du installerar klient språk paketen innan du distribuerar-klienten. Om du installerar [klient språk paketen](../../../../core/servers/deploy/install/language-packs.md) (för att aktivera ytterligare språk) på en plats efter att du har installerat klienter måste du installera om klienterna innan de kan använda dessa språk. För mobila enhets klienter måste du rensa den mobila enheten och registrera den igen.  

## <a name="prepare-required-pki-certificates-in-advance"></a>Förbered nödvändiga PKI-certifikat i förväg  
 För att kunna hantera enheter på Internet, registrerade mobila enheter och Mac-datorer måste du ha PKI-certifikat på platssystem (hanterings- och distributionsplatser) och klientenheterna. I produktionsnätverk kan du behöva godkännande från förändringsledningen för att använda nya certifikat eller starta om systemservrar, och användare kan behöva logga ut och logga in igen för nya gruppmedlemskap. Dessutom kan du behöva sätta av tillräckligt med tid för replikering av säkerhetsbehörigheter och för eventuella nya certifikatmallar.  

 Mer information om de PKI-certifikat som krävs finns i [PKI-certifikat krav för Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

## <a name="before-you-install-clients-configure-any-required-client-settings-and-maintenance-windows"></a>Innan du installerar klienterna konfigurerar du eventuella klientinställningar och underhållsfönster som behövs  
 Även om du kan [Konfigurera klient inställningar](../../../../core/clients/deploy/configure-client-settings.md) och underhålls fönster före eller efter att klienterna har installerats, är det bättre att konfigurera nödvändiga inställningar innan du installerar klienterna så att de används så fort klienten är installerad. 

 Konfigurera underhålls perioder för servrar och för Windows Embedded-enheter för att säkerställa affärs kontinuitet för kritiska enheter. Underhålls fönster säkerställer att nödvändiga program uppdateringar och program mot skadlig kod inte startar om datorn under kontors tid.  

> [!IMPORTANT]  
>  För Windows 10-datorer som du vill skydda med Enhetligt skrivfilter (UWF), måste du konfigurera enheten för Enhetligt skrivfilter innan du installerar klienten. På så sätt kan Configuration Manager installera klienten med en anpassad autentiseringsprovider som låser ut användare med låg behörighet från att logga in på enheten under underhålls läge.  

## <a name="plan-your-user-enrollment-experience-for-mac-computers-and-mobile-devices"></a>Planera din användar registrerings upplevelse för Mac-datorer och mobila enheter   
 Om användarna ska registrera sina egna Mac-datorer och mobila enheter med Configuration Manager planera användar upplevelsen. Du kan till exempel skapa skript för installations-och registrerings processen genom att använda en webb sida så att användarna anger den minsta mängd information som krävs och skickar instruktioner med en länk via e-post.  

## <a name="use-file-based-write-filters-for-windows-embedded-devices"></a>Använda filbaserade Skriv filter för Windows Embedded-enheter 
 Inbäddade enheter som använder EWF (Enhanced Write Filters) upplever antagligen omsynkronisering av tillståndsmeddelanden. Om du bara har ett fåtal inbäddade enheter som använder EWF kanske du inte lägger märke till detta. Men om du har många inbäddade enheter som synkroniserar om sin information, t.ex. genom att skicka en fullständig inventering istället för en ändringsinventering, kan detta generera en märkbar ökning i nätverkspaket och högre CPU-belastning på platsservern.  

 När du har möjlighet att välja vilken typ av Skriv filter som ska aktive ras väljer du filbaserade Skriv filter och konfigurerar undantag som bevarar klient tillstånds-och inventerings data mellan omstarter av enheter för nätverks-och CPU-effektivitet på den Configuration Manager klienten. Mer information om Skriv filter finns i [Planera för klient distribution till Windows Embedded-enheter](../../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

 Mer information om det högsta antal Windows Embedded-klienter som en primär plats kan hantera finns i [Operativsystem som stöds för klienter och enheter](../../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md).  
