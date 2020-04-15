---
title: Requisiti di sistema di .NET Framework
description: Informazioni sui requisiti hardware, software e del sistema operativo per installare .NET Framework 4.5 e versioni successive.
ms.custom: updateeachrelease
ms.date: 04/18/2019
helpviewer_keywords:
- software requirements
- .NET Framework, system requirements
- system requirements
- operating systems supported
- hardware requirements
ms.assetid: 298275e2-da1d-4618-9f74-6a3567832350
ms.openlocfilehash: 571075f7d0f330cf88ac9618376876b4f72e75ed
ms.sourcegitcommit: c91110ef6ee3fedb591f3d628dc17739c4a7071e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2020
ms.locfileid: "81389480"
---
# <a name="net-framework-system-requirements"></a>Requisiti di sistema di .NET Framework

Nelle tabelle di questo articolo vengono forniti i requisiti hardware, del sistema operativo e software per le seguenti versioni di .NET Framework:

- .NET framework 4.5 e relative versioni intermedie (4.5.1 e 4.5.2).
- .NET framework 4.6 e relative versioni intermedie (4.6.1 e 4.6.2).
- .NET framework 4.7 e relative versioni intermedie (4.7.1 e 4.7.2).
- .NET Framework 4.8

Per informazioni sulle versioni di .NET Framework precedenti a .NET Framework 4.5, vedere [Versioni e dipendenze di .NET Framework](../migration-guide/versions-and-dependencies.md).

Gli ambienti di sviluppo che consentono di sviluppare app per .NET Framework hanno un set separato di requisiti.

[!INCLUDE[net-framework-4-versions](../../../includes/net-framework-4x-versions.md)]

Per informazioni su download e collegamenti, vedere [Install the .NET Framework for developers](../install/guide-for-developers.md) (Installazione di .NET Framework per sviluppatori).

Per informazioni sul ciclo di vita del supporto delle versioni di .NET Framework, vedere [Ciclo di vita del supporto Microsoft](https://support.microsoft.com/lifecycle/search?sort=PN&alpha=Microsoft%20.NET%20Framework&Filter=FilterNO).

## <a name="hardware-requirements"></a>Requisiti hardware

|                          |        |
| ------------------------ | ------ |
| **Processore**            | 1 GHz  |
| **Ram**                  | 512 MB |
| **Spazio su disco (minimo)** |        |
| 32 bit                   | 4,5 GB |
| 64 bit                   | 4,5 GB |

## <a name="installation-requirements"></a>Requisiti di installazione

.NET Framework richiede privilegi di amministratore per l'installazione. Se non si dispone dei diritti di amministratore per il computer in cui si desidera installare .NET Framework, contattare l'amministratore di rete.

## <a name="supported-client-operating-systems"></a>Sistemi operativi client supportati

| Sistema operativo | Edizioni supportate | Preinstallato con il sistema operativo | Installabile separatamente |
| ---------------- | ------------------ | ------------------------ | ---------------------- |
| Aggiornamento di Windows 10 di maggio 2019<br/> (versione 1903) | 32 bit e 64 bit | .NET Framework 4.8 | -- |
| Aggiornamento di Windows 10 (ottobre 2018)<br/> (versione 1809) | 32 bit e 64 bit | .NET Framework 4.7.2 | .NET Framework 4.8 |
| Aggiornamento di Windows 10 (aprile 2018)<br/> (versione 1803) | 32 bit e 64 bit | .NET Framework 4.7.2 |.NET Framework 4.8|
| Windows 10 Fall Creators Update<br/> (versione 1709) | 32 bit e 64 bit | .NET Framework 4.7.1 | .NET Framework 4.7.2<br/><br/>.NET Framework 4.8 |
| Windows 10 Creators Update<br/> (versione 1703) | 32 bit e 64 bit | .NET Framework 4.7 | .NET Framework 4.7.1<br/><br/>.NET Framework 4.7.2<br/><br/>.NET Framework 4.8 |
| Aggiornamento dell'anniversario di Windows 10<br/> (versione 1607) | 32 bit e 64 bit | .NET Framework 4.6.2 |.NET Framework 4.7<br/><br/>.NET Framework 4.7.1<br/><br/>.NET Framework 4.7.2<br/><br/>.NET Framework 4.8  |
| Aggiornamento di novembre di Windows 10<br/> (versione 1511) | 32 bit e 64 bit | .NET Framework 4.6.1 | .NET Framework 4.6.2 |
| Windows 10<br/> (versione 1507) | 32 bit e 64 bit | .NET Framework 4.6 | .NET Framework 4.6.1 <br/><br/> .NET Framework 4.6.2 |
| Windows 8.1 | 32 bit, 64 bit e ARM | .NET Framework 4.5.1 | .NET Framework 4.5.2<br /><br /> .NET Framework 4.6<br /><br /> .NET Framework 4.6.1<br /><br /> .NET Framework 4.6.2<br /><br />.NET Framework 4.7<br/><br/>.NET Framework 4.7.1<br/><br/>.NET Framework 4.7.2<br/><br/>.NET Framework 4.8 |
| Windows 8 | 32 bit, 64 bit e ARM | .NET Framework 4.5 | .NET Framework 4.5.1<br /><br />.NET Framework 4.5.2<br /><br /> .NET Framework 4.6<br /><br /> .NET Framework 4.6.1 |
| Windows 7 SP1|32 bit e 64 bit | -- | .NET Framework 4<br /><br /> .NET Framework 4.5<br /><br /> .NET Framework 4.5.1<br /><br /> .NET Framework 4.5.2<br /><br /> .NET Framework 4.6<br /><br /> .NET Framework 4.6.1<br /><br /> .NET Framework 4.6.2<br /><br />.NET Framework 4.7<br/><br/>.NET Framework 4.7.1<br/><br/>.NET Framework 4.7.2<br/><br/>.NET Framework 4.8 |
| Windows Vista SP2|32 bit e 64 bit | -- | .NET Framework 4<br /><br /> .NET Framework 4.5<br /><br /> .NET Framework 4.5.1<br /><br /> .NET Framework 4.5.2<br /><br /> .NET Framework 4.6 |
| Windows XP |32 bit e 64 bit | -- | .NET Framework 4 |

 **Note:**

- Nei sistemi Windows 7, .NET Framework richiede Windows 7 SP1. Se si ha Windows 7 ma non è ancora stato installato Service Pack 1, è necessario farlo prima di installare .NET Framework.

- .NET Framework 4.5 è supportato nell'Ambiente preinstallazione di Windows (Windows PE). Non tutte le funzionalità sono supportate in Windows PE.

- .NET Framework 4 supporta anche la piattaforma IA64.

- Per tutte le piattaforme, è consigliabile eseguire l'aggiornamento al Service Pack di Windows più recente e installare gli aggiornamenti critici disponibili da [Windows Update](https://support.microsoft.com/help/12373/windows-update-faq) per garantire la migliore compatibilità e sicurezza.

- Nei sistemi operativi a 64 bit, .NET Framework supporta sia WOW64 (elaborazione a 32 bit in un computer a 64 bit) che l'elaborazione nativa a 64 bit.

## <a name="supported-server-operating-systems"></a>Sistemi operativi server supportati

| Sistema operativo | Edizioni supportate | Preinstallato con il sistema operativo | Installabile separatamente |
| ---------------- | ------------------ | ------------------------ | ---------------------- |
| Windows Server 2019 | 64 bit | .NET Framework 4.7.2 | .NET Framework 4.8 |
| Windows Server, versione 1809 | 64 bit | .NET Framework 4.7.2 | .NET Framework 4.8 |
| Windows Server, versione 1803 | 64 bit | .NET Framework 4.7.2 | .NET Framework 4.8 |
| Windows Server, versione 1709 | 64 bit | .NET Framework 4.7.1 | .NET Framework 4.7.2|
| Windows Server 2016 | 64 bit | .NET Framework 4.6.2 | .NET Framework 4.7<br/><br/> .NET Framework 4.7.1<br/><br/>.NET Framework 4.7.2<br/><br/>.NET Framework 4.8 |
| Windows Server 2012 R2 | 64 bit | .NET Framework 4.5.1 | .NET Framework 4.5.2<br /><br /> .NET Framework 4.6<br /><br /> .NET Framework 4.6.1<br /><br /> .NET Framework 4.6.2<br /><br />.NET Framework 4.7<br/><br/> .NET Framework 4.7.1<br/><br/>.NET Framework 4.7.2<br/><br/>.NET Framework 4.8 |
| Windows Server 2012 (edizione a 64 bit) | 64 bit| .NET Framework 4.5 | .NET Framework 4.5.1<br /><br /> .NET Framework 4.5.2<br /><br /> .NET Framework 4.6<br /><br /> .NET Framework 4.6.1<br /><br /> .NET Framework 4.6.2<br /><br />.NET Framework 4.7<br/><br/>.NET Framework 4.7.1<br/><br/>.NET Framework 4.7.2<br/><br/>.NET Framework 4.8 |
| Windows Server 2008 R2 SP1|64 bit | -- | .NET Framework 4<br /><br /> .NET Framework 4.5<br /><br /> .NET Framework 4.5.1<br /><br /> .NET Framework 4.5.2<br /><br /> .NET Framework 4.6<br /><br /> .NET Framework 4.6.1<br /><br /> .NET Framework 4.6.2<br /><br />.NET Framework 4.7<br/><br/>.NET Framework 4.7.1<br/><br/>.NET Framework 4.7.2<br/><br/>.NET Framework 4.8 |
| Windows Server 2008 SP2|32 bit e 64 bit | -- | .NET Framework 4<br /><br /> .NET Framework 4.5<br /><br /> .NET Framework 4.5.1<br /><br /> .NET Framework 4.5.2<br /><br /> .NET Framework 4.6 |

**Note:**

- Windows Server 2012 include .NET Framework 4.5, pertanto non è necessario installarlo separatamente. Analogamente, Windows Server 2012 R2 include .NET Framework 4.5.1.

- .NET Framework ha un supporto limitato per il ruolo di base del Server con Windows Server 2008 R2 SP1 o versione successiva. Per un elenco di API non supportate, vedere [Server Core .NET Functionality](https://docs.microsoft.com/previous-versions//dd745015(v=vs.85)) (Funzionalità .NET di Server Core).

- .NET Framework non è supportato in Windows Server 2008 R2 per sistemi basati su Itanium.

- In Windows Server 2008 SP2, .NET Framework non è supportato nel ruolo Server Core.

- Per tutte le piattaforme, è consigliabile eseguire l'aggiornamento al Service Pack di Windows più recente e agli aggiornamenti critici disponibili da [Windows Update](https://support.microsoft.com/help/12373/windows-update-faq) per garantire la migliore compatibilità e sicurezza. Su alcuni sistemi operativi potrebbe essere necessaria l'installazione dell'ultimo Windows Service Pack.

- Nei sistemi operativi a 64 bit, .NET Framework supporta sia WOW64 (elaborazione a 32 bit in un computer a 64 bit) che l'elaborazione nativa a 64 bit.

## <a name="see-also"></a>Vedere anche

- [Guida all'installazione](../install/index.md)
- [Guida introduttiva](index.md)
- [Risolvere i problemi relativi alle installazioni e alle disinstallazioni bloccate di .NET Framework](../install/troubleshoot-blocked-installations-and-uninstallations.md)
