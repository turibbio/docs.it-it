---
ms.openlocfilehash: beb869208e8d48d762d94b5989a558fa2f1aaf29
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85622011"
---
### <a name="data-binding-improvement-for-keyedcollection"></a>Miglioramento del data binding per KeyedCollection

#### <a name="details"></a>Dettagli

Correzione <xref:System.Windows.Data.Binding> dell'uso errato dell'indicizzatore IList quando l'oggetto di origine dichiara un indicizzatore personalizzato con la stessa firma, ad esempio KeyedCollection &lt; int, TItem &gt; .

#### <a name="suggestion"></a>Suggerimento

Per fare in modo che un'applicazione destinata a una versione precedente tragga vantaggio da questa modifica, deve essere eseguita nel .NET Framework 4,8 o versione successiva e deve acconsentire esplicitamente alla modifica aggiungendo l' [opzione AppContext](https://docs.microsoft.com/dotnet/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element) seguente alla <code>&lt;runtime&gt;</code> sezione del file di configurazione dell'app e impostandolo su <code>false</code> :<pre><code class="lang-xml">&lt;?xml version=&quot;1.0&quot; encoding=&quot;utf-8&quot;?&gt;&#13;&#10;&lt;configuration&gt;&#13;&#10;&lt;startup&gt;&#13;&#10;&lt;supportedRuntime version=&quot;v4.0&quot; sku=&quot;.NETFramework,Version=v4.7&quot;/&gt;&#13;&#10;&lt;/startup&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;!-- AppContextSwitchOverrides value attribute is in the form of &#39;key1=true/false;key2=true/false  --&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Windows.Data.Binding.IListIndexerHidesCustomIndexer=false&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>

| Nome    | Valore       |
|:--------|:------------|
| Scope   |Principale|
|Version|4.8|
|Type|Runtime|
