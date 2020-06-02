---
title: Sicurezza e input dell'utente
description: Il codice potrebbe passare i dati immessi dall'utente come parametri ad altro codice, che può influire sulla sicurezza. È possibile eseguire il controllo degli intervalli per rifiutare l'input problematico.
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- security [.NET Framework], user input
- user input, security
- secure coding, user input
- code security, user input
ms.assetid: 9141076a-96c9-4b01-93de-366bb1d858bc
ms.openlocfilehash: 995af30385790a88718193e7abad1db7bc4b56c3
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84275945"
---
# <a name="security-and-user-input"></a>Sicurezza e input dell'utente

I dati utente, ovvero tutti i tipi di input, ad esempio i dati di una richiesta Web o di un URL, gli input in controlli di un'applicazione Microsoft Windows Forms e così via, possono avere effetti negativi sul codice in quanto questi dati sono spesso utilizzati direttamente come parametri per chiamare altro codice. Questa situazione è analoga a quella della chiamata del codice da parte di codice dannoso con parametri insoliti ed è necessario adottare le stesse precauzioni. La sicurezza dell'input dell'utente è un'operazione difficile in quanto non è disponibile alcuno stack frame per registrare la presenza dei dati potenzialmente inattendibili.

Questi ultimi rappresentano i bug più difficili da rilevare in quanto, sebbene possano essere presenti in codice apparentemente non collegato alla sicurezza, costituiscono una porta tramite cui i dati dannosi possono essere passati ad altro codice. Per ricercare bug di questo tipo, prendere in considerazione i vari tipi di dati di input, immaginare l'intervallo dei valori possibili e determinare se il codice relativo a questi dati è in grado di gestire tutti i casi. Questi bug possono essere corretti tramite la verifica dell'intervallo e il rifiuto dell'input che non è possibile gestire tramite codice.

Tra gli aspetti importanti dei dati utente sono inclusi i seguenti:

- I dati utente in una risposta server sono eseguiti nel contesto del sito del server sul client. Se il server Web accetta dati utente e li inserisce nella pagina Web restituita, potrebbe, ad esempio, includere un **\<script>** tag ed eseguirlo come se fosse dal server.

- Tenere presente che il client può richiedere qualsiasi URL.

- Prendere in considerazione i percorsi complessi o non validi:

  - ..\ , percorsi estremamente lunghi.

  - Utilizzo di caratteri jolly (*).

  - Espansione del token (% token%).

  - Forme insolite di percorsi con significati speciali.

  - Nomi di flusso del file system alternativi come filename: `filename::$DATA`.

  - Versioni abbreviate dei nomi file come `longfi~1` per `longfilename`.

- Ricordare che Eval(userdata) consente di eseguire qualsiasi operazione.

- Tenere conto dell'associazione tardiva a un nome che include dati utente.

- Se si utilizzano dati Web, prendere in considerazione le varie forme di escape consentite, inclusi:

  - Escape esadecimali escape (%nn).

  - Escape Unicode (%nnn).

  - Escape lunghi UTF-8 (%nn%nn).

  - Escape doppi (%nn diviene %mmnn, dove %mm è il carattere di escape per '%').

- Prestare attenzione ai nomi utente che possono avere più di un formato canonico. Ad esempio, è spesso possibile utilizzare la forma MYDOMAIN\\*nomeutente* o la forma *nomeutente@mydomain.example.com*@mydomain.example.com.

## <a name="see-also"></a>Vedere anche

- [Linee guida per la generazione di codice sicuro](secure-coding-guidelines.md)
