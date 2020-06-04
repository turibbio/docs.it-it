---
title: -doc
ms.date: 03/10/2018
helpviewer_keywords:
- doc compiler option [Visual Basic]
- -doc compiler option [Visual Basic]
- /doc compiler option [Visual Basic]
ms.assetid: 5fc32ec9-a149-4648-994c-a8d0cccd0a65
ms.openlocfilehash: 57a81983278c26090c62995f4da55c5cbfd66047
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84408673"
---
# <a name="-doc"></a>-doc
Elabora commenti sulla documentazione in un file XML.  
  
## <a name="syntax"></a>Sintassi  
  
```console  
-doc[+ | -]  
```

Oppure  

```console
-doc:file  
```  
  
## <a name="arguments"></a>Argomenti  
  
|Termine|Definizione|  
|---|---|  
|`+` &#124; `-`|Facoltativa. Se si specifica +, o semplicemente `-doc`, il compilatore genera informazioni di documentazione e le inserisce in un file XML. La specifica di `-` equivale a non specificare `-doc`, quindi non vengono create informazione di documentazione.|  
|`file`|Richiesto se è usato `-doc:`. Specifica il file di output XML, popolato con i commenti dai file del codice sorgente della compilazione. Se il nome del file contiene uno spazio, racchiudere il nome tra virgolette doppie (" ").|  
  
## <a name="remarks"></a>Commenti  
 L'opzione `-doc` controlla se il compilatore genera un file XML contenente i commenti della documentazione. Se si usa la sintassi `-doc:file`, il parametro `file` specifica il nome del file XML. Se si usa `-doc` o `-doc+`, il compilatore ottiene il nome del file XML dal file eseguibile o dalla libreria che il compilatore sta creando. Se si usa `-doc-` o non si specifica l'opzione `-doc`, il compilatore non crea un file XML.  
  
 Nei file di codice sorgente, i commenti della documentazione possono precedere le definizioni seguenti:  
  
- Tipi definiti dall'utente, ad esempio una [classe](../../language-reference/statements/class-statement.md) o [interfaccia](../../language-reference/statements/interface-statement.md)  
  
- Membri, ad esempio un campo, un [evento](../../language-reference/statements/event-statement.md), una [proprietà](../../language-reference/statements/property-statement.md), una [funzione](../../language-reference/statements/function-statement.md) oppure una [subroutine](../../language-reference/statements/sub-statement.md).  
  
 Per usare il file XML generato con la funzionalità [IntelliSense](/visualstudio/ide/using-intellisense) di Visual Studio, usare un nome per il file XML uguale al nome dell'assembly che si vuole supportare. Assicurarsi che il file XML sia nella stessa directory dell'assembly, in modo che quando si fa riferimento all'assembly nel progetto di Visual Studio, venga trovato anche il file XML. I file di documentazione XML non sono necessari per il funzionamento di IntelliSense per il codice all'interno di un progetto o all'interno di progetti a cui viene fatto riferimento da un progetto.  
  
 A meno che non si esegua la compilazione con `-target:module`, il file XML contiene i tag `<assembly></assembly>`. Questi tag specificano il nome del file contenente il manifesto dell'assembly per il file di output della compilazione.  
  
 Vedere [Tag XML consigliati per i commenti relativi alla documentazione](../../language-reference/xmldoc/index.md) per informazioni su come generare documentazione dai commenti nel codice.  
  
|Per impostare -doc nell'ambiente di sviluppo integrato di Visual Studio|  
|---|  
|1. è stato selezionato un progetto in **Esplora soluzioni**. Scegliere **Proprietà** dal menu **Progetto**. <br />2. fare clic sulla scheda **Compila** .<br />3. impostare il valore nella casella **genera file di documentazione XML** .|  
  
## <a name="example"></a>Esempio  
 Vedere [Documentazione del codice tramite XML](../../programming-guide/program-structure/documenting-your-code-with-xml.md) per un esempio.  
  
## <a name="see-also"></a>Vedere anche

- [Compilatore della riga di comando di Visual Basic](index.md)
- [Documentazione del codice tramite XML](../../programming-guide/program-structure/documenting-your-code-with-xml.md)
