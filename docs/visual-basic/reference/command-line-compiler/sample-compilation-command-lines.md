---
title: Esempi di righe di comando di compilazione
ms.date: 03/13/2018
helpviewer_keywords:
- command line [Visual Basic], compilers
- compilation [Visual Basic], command-line
- command-line compilers
- compiling source code [Visual Basic], from command line
- Visual Basic compiler, sample command lines
ms.assetid: 5bfbb487-5f47-4267-969a-39dfb917beeb
ms.openlocfilehash: 496627d3b77b0382ae7d15c8225a6fbd41f1db73
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84403122"
---
# <a name="sample-compilation-command-lines-visual-basic"></a>Righe di comando di compilazione di esempio (Visual Basic)

In alternativa alla compilazione di Visual Basic programmi da Visual Studio, è possibile eseguire la compilazione dalla riga di comando per produrre file eseguibili (exe) o file dll (Dynamic-Link Library).

Il Visual Basic compilatore della riga di comando supporta un set completo di opzioni che controllano i file di input e di output, gli assembly e le opzioni di debug e preprocessore. Ogni opzione è disponibile in due forme intercambiabili: `-option` e `/option` . Questa documentazione Mostra solo il `-option` modulo.

La tabella seguente elenca alcune righe di comando di esempio che è possibile modificare per uso personale.

|A|Uso|
|--------|---------|
|Compilare file. vb e creare file. exe|`vbc -reference:Microsoft.VisualBasic.dll File.vb`|
|Compilare file. vb e creare file. dll|`vbc -target:library File.vb`|
|Compilare file. vb e creare My. exe|`vbc -out:My.exe File.vb`|
|Compilare file. vb e creare una libreria e un assembly di riferimento denominato file. dll|`vbc -target:library -ref:.\debug\bin\ref\file.dll File.vb`|
|Compila tutti i file Visual Basic nella directory corrente, con le ottimizzazioni su e il `DEBUG` simbolo definito, producendo file2. exe|`vbc -define:DEBUG=1 -optimize -out:File2.exe *.vb`|
|Compila tutti i file di Visual Basic nella directory corrente, producendo una versione di debug di file2. dll senza visualizzare il logo o gli avvisi|`vbc -target:library -out:File2.dll -nowarn -nologo -debug *.vb`|
|Compila tutti i file di Visual Basic della directory corrente in something. dll|`vbc -target:library -out:Something.dll *.vb`|

> [!TIP]
> Quando si compila un progetto usando l'IDE di Visual Studio, è possibile visualizzare informazioni sul comando **vbc** associato con le relative opzioni del compilatore nella finestra output. Per visualizzare queste informazioni, aprire la finestra di [dialogo Opzioni, progetti e soluzioni, compila ed Esegui](/visualstudio/ide/reference/options-dialog-box-projects-and-solutions-build-and-run), quindi impostare il livello di **dettaglio dell'output di compilazione del progetto MSBuild** su **normale** o su un livello di dettaglio superiore.

## <a name="see-also"></a>Vedere anche

- [Compilatore della riga di comando di Visual Basic](index.md)
- [Compilazione condizionale](../../programming-guide/program-structure/conditional-compilation.md)
