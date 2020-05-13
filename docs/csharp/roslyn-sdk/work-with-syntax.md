---
title: Usare il modello di sintassi di .NET Compiler Platform SDK
description: Questa panoramica consente di conoscere i tipi usati per comprendere e modificare i nodi di sintassi.
ms.date: 10/15/2017
ms.custom: mvc
ms.openlocfilehash: fdb13095c2b91e54d58988a51a51b05652e57ea6
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/12/2020
ms.locfileid: "83208395"
---
# <a name="work-with-syntax"></a>Utilizzare la sintassi

L'*albero della sintassi* è una struttura dei dati fondamentale esposta dalle API del compilatore. Questi alberi rappresentano la struttura lessicale e sintattica del codice sorgente e svolgono due funzioni importanti:

- Per consentire agli strumenti, ad esempio un IDE, componenti aggiuntivi, strumenti di analisi del codice e refactoring, di visualizzare ed elaborare la struttura sintattica del codice sorgente nel progetto di un utente.
- Per abilitare strumenti, ad esempio refactoring e IDE, per creare, modificare e ridisporre il codice sorgente in modo naturale senza dover usare modifiche di testo diretto. Mediante la creazione e modifica degli alberi, gli strumenti possono facilmente creare e modificare il codice sorgente.

## <a name="syntax-trees"></a>Alberi della sintassi

Gli alberi della sintassi sono la struttura primaria usata per compilazione, analisi codice, binding, refactoring, funzionalità dell'IDE e generazione di codice. Nessuna parte del codice sorgente può essere compresa senza prima essere identificata e categorizzata in uno dei numerosi elementi di linguaggio strutturali noti.

Per gli alberi della sintassi esistono tre attributi chiave. Il primo attributo è che gli alberi della sintassi contengono tutte le informazioni di origine con la massima fedeltà. Per fedeltà completa si intende che l'albero della sintassi contiene tutte le informazioni contenute nel testo di origine, ogni costrutto grammaticale, ogni token lessicale e tutti gli altri elementi tra, inclusi spazi vuoti, commenti e direttive per il preprocessore. Ad esempio, ogni valore letterale nell'origine viene rappresentato esattamente nel modo in cui è stato digitato. Gli alberi della sintassi acquisiscono anche errori nel codice sorgente quando il programma è incompleto o non corretto, rappresentando i token ignorati o mancanti.

Il secondo attributo degli alberi della sintassi è che possono produrre il testo esatto da cui sono stati analizzati. Da qualsiasi nodo di sintassi è possibile ottenere la rappresentazione testuale del sottoalbero radice in quel nodo. Questa possibilità significa che è possibile usare gli alberi della sintassi come modo per costruire e modificare il testo di origine. Creando una struttura ad albero, in modo implicito, è stato creato il testo equivalente e modificando un albero della sintassi, rendendo un nuovo albero da modifiche a un albero esistente, il testo è stato modificato.

Il terzo attributo degli alberi della sintassi è che sono thread-safe e non modificabili. Una volta ottenuto un albero, è uno snapshot dello stato corrente del codice e non viene mai modificato. In questo modo, più utenti possono interagire con lo stesso albero della sintassi contemporaneamente in thread diversi, senza causare blocchi o duplicazioni. Dato che gli alberi non sono modificabili e non è possibile apportare modifiche direttamente a un albero, i metodi factory sono utili per creare e modificare gli alberi della sintassi mediante la creazione di snapshot aggiuntivi dell'albero. L'efficienza degli alberi sta nel modo in cui vengono riutilizzati i nodi sottostanti, che consente di ricompilare una nuova versione velocemente e con una quantità limitata di memoria aggiuntiva.

Un albero della sintassi è letteralmente una struttura dei dati ad albero, in cui gli elementi strutturali non terminali fungono da padre per altri elementi. Ogni albero della sintassi è composto da nodi, token ed elementi semplici.

## <a name="syntax-nodes"></a>Nodi di sintassi

I nodi di sintassi sono tra gli elementi principali degli alberi della sintassi. Questi nodi rappresentano costrutti sintattici, ad esempio dichiarazioni, istruzioni, clausole ed espressioni. Ogni categoria di nodi di sintassi è rappresentata da una classe separata derivata da <xref:Microsoft.CodeAnalysis.SyntaxNode?displayProperty=nameWithType>. Il set di classi dei nodi non è estendibile.

Tutti i nodi di sintassi sono i nodi non terminali nell'albero della sintassi, ovvero hanno sempre altri nodi e token come elementi figlio. In quanto elemento figlio di un altro nodo, ogni nodo ha un nodo padre accessibile tramite la proprietà <xref:Microsoft.CodeAnalysis.SyntaxNode.Parent?displayProperty=nameWithType>. Dato che i nodi e gli alberi non sono modificabili, l'elemento padre di un nodo non cambia mai. La radice dell'albero ha un padre null.

Ogni nodo ha un metodo <xref:Microsoft.CodeAnalysis.SyntaxNode.ChildNodes?displayProperty=nameWithType>, che restituisce un elenco di nodi figlio in ordine sequenziale in base alla posizione nel testo di origine. L'elenco non contiene token. Ogni nodo dispone anche di metodi per esaminare i discendenti, ad esempio <xref:Microsoft.CodeAnalysis.SyntaxNode.DescendantNodes%2A> , <xref:Microsoft.CodeAnalysis.SyntaxNode.DescendantTokens%2A> o, <xref:Microsoft.CodeAnalysis.SyntaxNode.DescendantTrivia%2A> che rappresentano un elenco di tutti i nodi, i token o le banalità presenti nel sottoalbero radice da tale nodo.

Inoltre, ogni sottoclasse di nodo della sintassi espone gli stessi elementi figlio tramite proprietà fortemente tipizzate. Ad esempio, una classe di nodo <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax> include tre proprietà aggiuntive specifiche per gli operatori binari: <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.Left>, <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.OperatorToken> e <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.Right>. Il tipo di <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.Left> e <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.Right> è <xref:Microsoft.CodeAnalysis.CSharp.Syntax.ExpressionSyntax> e il tipo di <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.OperatorToken> è <xref:Microsoft.CodeAnalysis.SyntaxToken>.

Alcuni nodi di sintassi hanno elementi figlio facoltativi. Ad esempio, per un elemento <xref:Microsoft.CodeAnalysis.CSharp.Syntax.IfStatementSyntax> è disponibile un elemento <xref:Microsoft.CodeAnalysis.CSharp.Syntax.ElseClauseSyntax> facoltativo. Se l'elemento figlio non è presente, la proprietà restituisce null.

## <a name="syntax-tokens"></a>Token di sintassi

I token di sintassi sono i terminali della grammatica del linguaggio, che rappresentano i frammenti sintattici più piccoli del codice. Questi elementi non fungono mai da padre per altri nodi o token. I token di sintassi sono costituiti da parole chiave, identificatori, valori letterali e punteggiatura.

Per motivi di efficienza, il tipo <xref:Microsoft.CodeAnalysis.SyntaxToken> è un tipo valore CLR. Pertanto, a differenza dei nodi di sintassi, è presente una sola struttura per tutti i tipi di token con una combinazione di proprietà che hanno un significato in base al tipo di token rappresentato.

Ad esempio, un token letterale integer rappresenta un valore numerico. Oltre al testo di origine non elaborato rappresentato dal token, il token letterale ha una proprietà <xref:Microsoft.CodeAnalysis.SyntaxToken.Value> che indica l'esatto valore integer decodificato. Questa proprietà è tipizzata come <xref:System.Object> perché può essere uno di molti tipi primitivi.

La proprietà <xref:Microsoft.CodeAnalysis.SyntaxToken.ValueText> offre le stesse informazioni della proprietà <xref:Microsoft.CodeAnalysis.SyntaxToken.Value>, tuttavia questa proprietà è sempre tipizzata come <xref:System.String>. Un identificatore nel testo di origine C# può includere caratteri di escape Unicode, ma la sintassi della sequenza di escape stessa non viene considerata parte del nome dell'identificatore. In tal caso, anche se il testo non elaborato a cui fa riferimento il token include la sequenza di escape, la proprietà <xref:Microsoft.CodeAnalysis.SyntaxToken.ValueText> non la include e include invece i caratteri Unicode identificati dal carattere di escape. Ad esempio, se il testo di origine contiene un identificatore scritto come `\u03C0`, la proprietà <xref:Microsoft.CodeAnalysis.SyntaxToken.ValueText> per questo token restituirà `π`.

## <a name="syntax-trivia"></a>Elementi semplici della sintassi

Gli elementi semplici della sintassi rappresentano le parti del testo di origine in gran parte poco significative per la normale comprensione del codice, ad esempio spazi vuoti, commenti e direttive del preprocessore. Come i token di sintassi, gli elementi semplici sono tipi valore. Il singolo tipo <xref:Microsoft.CodeAnalysis.SyntaxTrivia?displayProperty=nameWithType> viene usato per descrivere tutti i tipi di elementi semplici.

Dato che gli elementi semplici non fanno parte della sintassi del linguaggio normale e possono trovarsi ovunque tra due token, non vengono inclusi nell'albero della sintassi come elemento figlio di un nodo. Tuttavia, dato che sono importanti quando si implementa una funzionalità come il refactoring e per mantenere la massima fedeltà con il testo di origine, esistono come parte dell'albero della sintassi.

È possibile accedere a Trivia controllando le raccolte o di un token <xref:Microsoft.CodeAnalysis.SyntaxToken.LeadingTrivia?displayProperty=nameWithType> <xref:Microsoft.CodeAnalysis.SyntaxToken.TrailingTrivia?displayProperty=nameWithType> . Quando viene analizzato il testo di origine, le sequenze di elementi semplici vengono associate ai token. In generale, un token possiede tutti gli elementi semplici dopo di esso sulla stessa riga fino al token successivo. Tutti gli elementi semplici dopo tale riga vengono associati al token seguente. Il primo token nel file di origine ottiene tutti gli elementi semplici iniziali e l'ultima sequenza degli elementi semplici nel file viene associata al token di fine del file, che in caso contrario ha larghezza zero.

A differenza dei nodi e dei token di sintassi, per gli elementi semplici della sintassi non vi sono elementi padre. Tuttavia, dato che fanno parte dell'albero e ognuno è associato a un singolo token, è possibile accedere al token associato tramite la proprietà <xref:Microsoft.CodeAnalysis.SyntaxTrivia.Token?displayProperty=nameWithType>.

## <a name="spans"></a>Intervalli

Ogni nodo, token o elemento semplice conosce la propria posizione all'interno del testo di origine e il numero di caratteri di cui è costituito. Una posizione del testo è rappresentata come intero a 32 bit, ovvero un indice `char` in base zero. Un oggetto <xref:Microsoft.CodeAnalysis.Text.TextSpan> rappresenta la posizione di inizio e il conteggio di caratteri, entrambi rappresentati come valori integer. Se <xref:Microsoft.CodeAnalysis.Text.TextSpan> ha lunghezza zero, fa riferimento a una posizione tra due caratteri.

Ogni nodo ha due proprietà <xref:Microsoft.CodeAnalysis.Text.TextSpan>: <xref:Microsoft.CodeAnalysis.SyntaxNode.Span%2A> e <xref:Microsoft.CodeAnalysis.SyntaxNode.FullSpan%2A>.

La <xref:Microsoft.CodeAnalysis.SyntaxNode.Span%2A> proprietà è l'intervallo di testo dall'inizio del primo token nel sottoalbero del nodo alla fine dell'ultimo token. Questo intervallo non include alcun elemento semplice iniziale o finale.

La <xref:Microsoft.CodeAnalysis.SyntaxNode.FullSpan%2A> proprietà è l'intervallo di testo che include l'intervallo normale del nodo, più l'intervallo di eventuali Trivia iniziali o finali.

Ad esempio:

``` csharp
      if (x > 3)
      {
||        // this is bad
          |throw new Exception("Not right.");|  // better exception?||
      }
```

Il nodo dell'istruzione all'interno del blocco ha un intervallo indicato da singole barre verticali (|) e include i caratteri `throw new Exception("Not right.");`. L'intervallo completo è indicato dalla doppia barra verticale (||) e include gli stessi caratteri dell'intervallo, oltre ai caratteri associati agli elementi semplici iniziali e finali.

## <a name="kinds"></a>Tipi

Ogni nodo, token o elemento semplice ha una proprietà <xref:Microsoft.CodeAnalysis.SyntaxNode.RawKind?displayProperty=nameWithType> di tipo <xref:System.Int32?displayProperty=nameWithType>, che identifica l'elemento di sintassi esatto rappresentato. È possibile eseguire il cast di questo valore in un'enumerazione specifica del linguaggio. Ogni linguaggio, C# o Visual Basic, ha una sola `SyntaxKind` enumerazione ( <xref:Microsoft.CodeAnalysis.CSharp.SyntaxKind?displayProperty=nameWithType> e <xref:Microsoft.CodeAnalysis.VisualBasic.SyntaxKind?displayProperty=nameWithType> rispettivamente) che elenca tutti i possibili nodi, token ed elementi Trivia nella grammatica. Questa conversione può essere eseguita automaticamente mediante l'accesso ai metodi di estensione <xref:Microsoft.CodeAnalysis.CSharp.CSharpExtensions.Kind%2A?displayProperty=nameWithType> o <xref:Microsoft.CodeAnalysis.VisualBasic.VisualBasicExtensions.Kind%2A?displayProperty=nameWithType>.

La proprietà <xref:Microsoft.CodeAnalysis.SyntaxToken.RawKind> consente di risolvere facilmente eventuali ambiguità per i tipi di nodi della sintassi che condividono la stessa classe di nodo. Per i token e gli elementi semplici, questa proprietà è l'unico modo per distinguere un tipo di elemento da un alto.

Ad esempio, una singola classe <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax> include gli elementi figlio <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.Left>, <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.OperatorToken> e <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.Right>. La proprietà <xref:Microsoft.CodeAnalysis.CSharp.CSharpExtensions.Kind%2A> consente di stabilire se si tratta di un nodo di sintassi di tipo <xref:Microsoft.CodeAnalysis.CSharp.SyntaxKind.AddExpression>, <xref:Microsoft.CodeAnalysis.CSharp.SyntaxKind.SubtractExpression> o <xref:Microsoft.CodeAnalysis.CSharp.SyntaxKind.MultiplyExpression>.

## <a name="errors"></a>Errori

Anche quando il testo di origine contiene errori di sintassi, viene esposto un albero della sintassi completo riconducibile tramite round-trip all'origine. Quando il parser rileva codice non conforme alla sintassi definita del linguaggio, usa una delle due tecniche per creare un albero della sintassi:

- Se il parser prevede un tipo specifico di token ma non lo trova, può inserire un token mancante nell'albero della sintassi nella posizione in cui era previsto il token. Un token mancante rappresenta il token effettivo previsto, ma con intervallo vuoto e la relativa proprietà <xref:Microsoft.CodeAnalysis.SyntaxNode.IsMissing?displayProperty=nameWithType> restituisce `true`.

- Il parser può ignorare i token finché non ne trova uno che può continuare l'analisi. In questo caso, i token ignorati vengono associati come nodo di elementi semplici con il tipo <xref:Microsoft.CodeAnalysis.CSharp.SyntaxKind.SkippedTokensTrivia>.
