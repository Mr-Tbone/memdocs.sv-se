---
title: Så här använder du plugin-programmet för konvertering
titleSuffix: Configuration Manager
description: Använd plugin-programmet Package Conversion Manager för att anpassa analys-och konverterings processerna.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 83cf156c-36de-483f-a9e6-2e06158f3b20
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 4ca16ade5f8581cb124df39294c3cfc27627a346
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709882"
---
# <a name="how-to-use-the-package-conversion-manager-plug-in"></a>Använda Package Conversion Manager-plugin-programmet

*Gäller för: Configuration Manager (aktuell gren)*

<!--1357861-->

Package Conversion Manager-plugin-programmet hjälper dig att anpassa analys-och konverterings processerna. Om du vill använda Package Conversion Manager-plugin-programmet skriver du en körbar fil eller en skript fil som utför anpassade åtgärder. Redigera sedan konfigurations filen Microsoft. ConfigurationManagement. exe. config för att anropa den körbara filen eller skriptet. De vanligaste språken som används för att skriva skriptet är VBScript eller PowerShell.

Package Conversion Manager-plugin-programmet körs en gång för varje paket. Om du analyserar eller konverterar flera paket i taget körs Package Conversion Manager-plugin-programmet varje gång.

> [!NOTE]  
> Mer information om paket konverterings hanterarens element i Configuration Manager konfigurations filen finns i [teknisk referens för Package Conversion Manager-konfigurationen för plugin-programmet](plugin-config-xml.md).



## <a name="default-process"></a>Standard process

Paket konverterings hanteraren utför följande åtgärder som standard:

1.  Läs ett Configuration Manager-paket.  

2.  Skapa ett program från paketet och Lägg till standardattribut.  

3.  Analysera programmet och fastställa ett paket beredskaps tillstånd.  

4.  Vidta någon av följande åtgärder, beroende på åtgärds hanteraren för paket konvertering:  

    - **Analysera**: Visa paket beredskaps tillstånd i Configuration Manager-konsolen.  

    - **Convert**: Skriv programmet till Configuration Manager databasen.  


## <a name="plug-in-based-process"></a>Plug-in-based process 

När du använder plugin-programmet utförs följande åtgärder i paket konverterings hanteraren:

1.  Läs ett Configuration Manager-paket.  

2.  Skapa ett program från paketet och Lägg till standardattribut.  

3.  Konvertera programmet till XML. Spara filen på disk.  

4.  Kör plugin-skriptet för att ändra program-XML. Mer information finns i [teknisk referens för konfigurations-XML för plugin-programmet för Package Conversion Manager](plugin-config-xml.md).  

5.  Konvertera program-XML till ett Configuration Manager-program.  

6.  Analysera programmet och fastställa ett paket beredskaps tillstånd.  

7.  Vidta någon av följande åtgärder, beroende på åtgärds hanteraren för paket konvertering:  

    - **Analysera**: Visa paket beredskaps tillstånd i Configuration Manager-konsolen.  

    - **Konvertera**: Skriv programmet till Configuration Manager databas.  



## <a name="see-also"></a>Se även

[Teknisk referens för konfigurations-XML för Package Conversion Manager-plugin](plugin-config-xml.md)
