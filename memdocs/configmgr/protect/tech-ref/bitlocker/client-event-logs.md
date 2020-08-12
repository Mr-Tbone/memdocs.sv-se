---
title: Klienthändelseloggar
titleSuffix: Configuration Manager
description: En teknisk referens för möjliga BitLocker (MBAM)-klient poster i händelse loggen i Windows
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: reference
ms.assetid: c38b6963-cb1f-40ed-a888-e19d401ec3fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d108f56032b1ca3cf4a41a836a7e9096afe41d0d
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127975"
---
# <a name="client-event-logs"></a>Klienthändelseloggar

*Gäller för: Configuration Manager (aktuell gren)*

<!--3601034-->

På en Configuration Manager-klient som du distribuerar en hanterings princip för BitLocker till använder du Windows Loggboken för att visa händelse loggar för BitLocker-klienten. Gå till **program-och tjänst loggar**, **Microsoft**, **Windows**, **MBAM** för både [Administratörs](#admin) -och [drift](#operational) händelse loggar.

## <a name="admin"></a>Administratör

### <a name="2-volumeenactmentfailed"></a>2: VolumeEnactmentFailed

Ett fel uppstod när MBAM-principer skulle tillämpas.

#### <a name="error-code--2144272219"></a>Felkod:-2144272219

Information: BitLocker-diskkryptering endast stöder kryptering med enbart använt utrymme i tunt allokerat lagrings utrymme.

Det här felet uppstår om du försöker använda BitLocker för att kryptera en virtuell dator som kör Windows 10 version 1803 eller tidigare. Tidigare versioner av Windows 10 stöder inte fullständig disk kryptering. Hanterings principer för BitLocker tvingar fullständig disk kryptering.

#### <a name="error-code--2147024774"></a>Felkod:-2147024774

Information: data fältet som överfördes till ett system anrop är för litet.

Lös problemet genom att starta om datorn.

### <a name="4-transferstatusdatafailed"></a>4: TransferStatusDataFailed

Ett fel inträffade när krypterings status data skickades.

### <a name="8-systemvolumenotfound"></a>8: SystemVolumeNotFound

System volymen saknas. SystemVolume krävs för att kryptera operativ system enheten.

### <a name="9-tpmnotfound"></a>9: TPMNotFound

TPM-maskinvaran saknas. TPM krävs för att kryptera operativ system enheten med valfritt TPM-skydd.

### <a name="10-machinehwexempted"></a>10: MachineHWExempted

Datorn är undantagen från kryptering. Datorns maskin varu status: undantagen

### <a name="11-machinehwunknown"></a>11: MachineHWUnknown

Datorn är undantagen från kryptering. Datorns maskin varu status: okänd

### <a name="12-hwcheckfailed"></a>12: HWCheckFailed

Kontroll av maskin varu undantag misslyckades.

### <a name="13-userisexempted"></a>13: UserIsExempted

Användaren är undantagen från kryptering.

### <a name="14-useriswaiting"></a>14: UserIsWaiting

Användaren begärde ett undantag.

### <a name="15-userexemptioncheckfailed"></a>15: UserExemptionCheckFailed

Användar undantags kontrollen misslyckades.

### <a name="16-userpostponed"></a>16: UserPostponed

Användaren skjuter upp krypterings processen.

### <a name="17-tpminitializationfailed"></a>17: TPMInitializationFailed

TPM-initieringen misslyckades. Användaren avvisade BIOS-ändringarna.

### <a name="18-coreservicedown"></a>18: CoreServiceDown

Det går inte att ansluta till MBAM-återställnings-och maskin varu tjänsten.

#### <a name="error-code--2147024809"></a>Felkod:-2147024809

Information: parametern är felaktig.

Felet uppstår om webbplatsen inte är HTTPS eller om klienten inte har något PKI-certifikat.

### <a name="20-policymismatch"></a>20: PolicyMismatch

Hanterings principen för BitLocker är i konflikt eller skadad.

### <a name="21-conflictingosvolumepolicies"></a>21: ConflictingOSVolumePolicies

Konflikt mellan identifierade operativ system volym krypterings principer. Kontrol lera de BitLocker-principer som är relaterade till skydd av OS-enheter.

### <a name="22-conflictingfddvolumepolicies"></a>22: ConflictingFDDVolumePolicies

En konflikt mellan volym krypterings principer för fasta data enheter upptäcktes. Kontrol lera de BitLocker-principer som är relaterade till fasta data enhets enhets skydd.

### <a name="27-encryptionfailednodra"></a>27: EncryptionFailedNoDra

Ett fel uppstod vid kryptering. En data återställnings agent (DRA) skydd krävs i FIPS-läge för datorer med äldre versioner än Windows 8,1.

### <a name="34-tpmlockoutresetfailed"></a>34: TpmLockOutResetFailed

Det gick inte att återställa TPM-utelåsning.

### <a name="36-tpmownerauthretrievalfailed"></a>36: TpmOwnerAuthRetrievalFailed

Det gick inte att hämta TPM-OwnerAuth från MBAM-tjänsterna.

### <a name="37-wmiproviderdllsearchpathupdatefailed"></a>37: WmiProviderDllSearchPathUpdateFailed

Det gick inte att uppdatera Sök vägen för DLL-filen för WMI-providern.

### <a name="38-timedoutwaitingforwmiprovider"></a>38: TimedOutWaitingForWmiProvider

Agenten stoppas. Tids gränsen nåddes i väntan på instansen av MBAM WMI-providern.

## <a name="operational"></a>Operativ

### <a name="1-volumeenactmentsuccessful"></a>1: VolumeEnactmentSuccessful

Hanterings principerna för BitLocker har tillämpats.

### <a name="3-transferstatusdatasuccessful"></a>3: TransferStatusDataSuccessful

Krypterings status data har skickats.

### <a name="19-coreserviceup"></a>19: CoreServiceUp

Har anslutit till MBAM-återställnings-och maskin varu tjänsten.

### <a name="28-tpmownerauthescrowed"></a>28: TpmOwnerAuthEscrowed

TPM-OwnerAuth har deponerats.

### <a name="29-recoverykeyescrowed"></a>29: RecoveryKeyEscrowed

Återställnings nyckeln för BitLocker för volymen har deponerats.

### <a name="30-recoverykeyreset"></a>30: RecoveryKeyReset

Återställnings nyckeln för BitLocker för volymen har uppdaterats.

### <a name="31-enforcepolicydateset"></a>31: EnforcePolicyDateSet

Använd princip datum... har angetts för volymen

### <a name="32-enforcepolicydatecleared"></a>32: EnforcePolicyDateCleared

Använd princip datum... har rensats för volymen.

### <a name="33-tpmlockoutresetsucceeded"></a>33: TpmLockOutResetSucceeded

TPM-utelåsning har återställts.

### <a name="35-tpmownerauthretrievalsucceeded"></a>35: TpmOwnerAuthRetrievalSucceeded

TPM-OwnerAuth har hämtats från MBAM-tjänsterna.

### <a name="39-removabledrivemounted"></a>39: RemovableDriveMounted

Den flyttbara enheten monterades.

### <a name="40-removabledrivedismounted"></a>40: RemovableDriveDismounted

Den flyttbara enheten har demonterats.

### <a name="41-failedtoenactendpointunreachable"></a>41: FailedToEnactEndpointUnreachable

Det gick inte att ansluta till MBAM-återställnings-och maskin varu tjänsten eftersom det inte gick att tillämpa hanterings principer för BitLocker på volymen.

### <a name="42-failedtoenactlockedvolume"></a>42: FailedToEnactLockedVolume

Det gick inte att använda BitLocker-hanterings principer för volymen på grund av låst volym tillstånd.

### <a name="43-transferstatusdatafailedendpointunreachable"></a>43: TransferStatusDataFailedEndpointUnreachable

Om du inte kan ansluta till MBAM-tjänsten för efterlevnad och status förhindrades överföring av krypterings status data.

## <a name="see-also"></a>Se även

Mer information om hur du använder dessa loggar finns i [händelse loggar för BitLocker](about-event-logs.md).

Mer felsöknings information finns i [Felsöka BitLocker](troubleshoot.md).
