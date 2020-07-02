---
ms.openlocfilehash: 86169b5c9a20678647153c951550e590a5bce588
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85622251"
---
### <a name="resizing-a-grid-can-hang"></a>Possibile blocco durante il ridimensionamento di una griglia

#### <a name="details"></a>Dettagli

Durante il layout di <code>T:System.Windows.Controls.Grid</code> può verificarsi un ciclo infinito nelle circostanze seguenti:<ul><li>Le definizioni di riga contengono due \* righe, che dichiarano entrambe un MinHeight e un MaxHeight.</li><li>Il contenuto di \* -Rows non supera il MaxHeight corrispondente</li><li>L'altezza disponibile della griglia viene superata dal primo valore MinHeight (più qualsiasi altra riga automatica o fissa)</li><li>L'app è destinata a .NET Framework 4.7 o acconsente esplicitamente all'algoritmo di allocazione della versione 4.7 impostando <code>Switch.System.Windows.Controls.Grid.StarDefinitionsCanExceedAvailableSpace=false</code></li></ul>Il ciclo si verificherà anche con più di due righe o nel caso analogo per le colonne. Il problema è stato corretto in .NET Framework 4.7.1.

#### <a name="suggestion"></a>Suggerimento

Effettuare l'aggiornamento a .NET Framework 4.7.1.  In alternativa, se non è necessario l'algoritmo di allocazione della versione 4.7 è possibile usare l'impostazione di configurazione seguente:<pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Windows.Controls.Grid.StarDefinitionsCanExceedAvailableSpace=true&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>

| Nome    | Valore       |
|:--------|:------------|
| Scope   |Microsoft Edge|
|Version|4.7|
|Type|Runtime|
