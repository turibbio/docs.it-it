---
title: Introduzione a C# e Visual Studio Code
description: Informazioni su come creare la prima applicazione .NET Core in C# ed eseguirne il debug tramite Visual Studio Code.
author: kendrahavens
ms.date: 12/05/2018
ms.openlocfilehash: 49a1271f2bf74224e189e70bebf0d22c49408e5d
ms.sourcegitcommit: 267d092663aba36b6b2ea853034470aea493bfae
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/21/2020
ms.locfileid: "80111062"
---
# <a name="get-started-with-c-and-visual-studio-code"></a>Introduzione a C# e Visual Studio Code

.NET Core offre una piattaforma veloce e modulare per la creazione di applicazioni eseguibili in Windows, Linux e macOS. Usare Visual Studio Code con l'estensione C# per ottenere un'efficace esperienza di programmazione con il supporto completo per IntelliSense C# (completamento intelligente del codice) e debug.

## <a name="prerequisites"></a>Prerequisiti

1. Installare [Visual Studio Code](https://code.visualstudio.com/).
2. Installare [.NET Core SDK](https://dotnet.microsoft.com/download).
3. Installare l'[estensione C#](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp) per Visual Studio Code. Per altre informazioni su come installare estensioni in Visual Studio Code, vedere [VS Code Extension Marketplace](https://code.visualstudio.com/docs/editor/extension-gallery) (Marketplace delle estensioni di Visual Studio Code).

## <a name="hello-world"></a>Hello World

Si inizia con un semplice programma "Hello World" in .NET Core:

1. Aprire un progetto:

    - Aprire Visual Studio Code.
    - Fare clic sull'icona Esplora nel menu a sinistra e quindi fare clic su **Apri cartella**.
    - Selezionare**Cartella di apertura** **file** > dal menu principale per aprire la cartella in cui si desidera inserire il progetto in C, quindi fare clic su **Seleziona cartella**. Ai fini di questo esempio, viene creata una cartella per il progetto denominato *HelloWorld*.

      ![Cartella aperta di Visual Studio Code](media/with-visual-studio-code/vs-code-open-folder.png)

2. Inizializzare un progetto C#:

    - Aprire il terminale integrato da Visual Studio Code selezionando **Visualizza** > **terminale integrato** dal menu principale.
    - Nella finestra del terminale digitare `dotnet new console`.
    - Questo comando consente di creare un file *di Program.cs* nella cartella con un semplice programma "Hello World" già scritto, insieme a un file di progetto di C, denominato *HelloWorld.csproj*.

      ![Comando new di dotnet](media/with-visual-studio-code/dotnet-new-command.png)

3. Risolvere le risorse di compilazione:

    - Per **.NET Core 1.x** digitare `dotnet restore`. L'esecuzione di `dotnet restore` consente di accedere ai pacchetti .NET Core necessari per la compilazione del progetto.

      ![Comando restore di dotnet](media/with-visual-studio-code/dotnet-restore-command.png)

      [!INCLUDE[DotNet Restore Note](~/includes/dotnet-restore-note.md)]

4. Eseguire il programma "Hello World":

    - Digitare `dotnet run`.

      ![Comando run di dotnet](media/with-visual-studio-code/dotnet-run-command.png)

Per altre informazioni sull'installazione in [Windows](https://channel9.msdn.com/Blogs/dotnet/Get-started-with-VS-Code-using-CSharp-and-NET-Core), [macOS](https://channel9.msdn.com/Blogs/dotnet/Get-started-with-VS-Code-using-CSharp-and-NET-Core-on-MacOS) o [Linux](https://channel9.msdn.com/Blogs/dotnet/Get-started-with-VS-Code-Csharp-dotnet-Core-Ubuntu), è anche possibile guardare una breve esercitazione video.

## <a name="debug"></a>Debug

1. Aprire il file *Program.cs* facendo clic su di esso. La prima volta che si apre un file C# in Visual Studio Code, [OmniSharp](https://www.omnisharp.net/) viene caricato nell'editor.

    ![Aprire il file Program.cs](media/with-visual-studio-code/open-program-cs.png)

2. Visual Studio Code dovrebbe chiedere di aggiungere le risorse mancanti per compilare l'app ed eseguirne il debug. Selezionare **Sì**.

    ![Richiesta delle risorse mancanti](media/with-visual-studio-code/missing-assets.png)

3. Per aprire la visualizzazione Debug, fare clic sull'icona Debug nel menu di sinistra.

    ![Aprire la scheda Debug in Visual Studio Code](media/with-visual-studio-code/open-debug-tab.png)

4. Individuare la freccia verde nella parte superiore del riquadro. Assicurarsi che nell'elenco a discesa accanto ad esso sia selezionato **.NET Core Launch (console).**

    ![Selezione di .NET Core in Visual Studio Code](media/with-visual-studio-code/select-net-core.png)

5. Aggiungere un punto di interruzione al progetto facendo clic sul **margine dell'editor**, ovvero lo spazio a sinistra dei numeri di riga nell'editor accanto alla riga 9, oppure spostare il cursore di testo sulla riga 9 e premere <kbd>F9</kbd>.

    ![Impostazione di un punto di interruzione](media/with-visual-studio-code/set-breakpoint-vs-code.png)

6. Per avviare il debug, premere <kbd>F5</kbd> o selezionare la freccia verde. Il debugger interrompe l'esecuzione del programma quando raggiunge il punto di interruzione impostato nel passaggio precedente.
    - Durante il debug, è possibile visualizzare le variabili locali nel riquadro in alto a sinistra o utilizzare la console di debug.

7. Selezionare la freccia blu in alto per continuare il debug oppure fare clic sul quadrato rosso per arrestarlo.

    ![Esecuzione e debug in Visual Studio Code](media/with-visual-studio-code/run-debug-vs-code.png)

> [!TIP]
> Per altre informazioni e per suggerimenti sul debug .NET Core con OmniSharp in Visual Studio Code, vedere [Instructions for setting up the .NET Core debugger](https://github.com/OmniSharp/omnisharp-vscode/blob/master/debugger.md) (Istruzioni per l'impostazione del debugger .NET Core).

## <a name="add-a-class"></a>Aggiungere una classe

1. Per aggiungere una nuova classe, fare clic con il pulsante destro del mouse in VSCode Explorer e selezionare **Nuovo file**. Verrà aggiunto un nuovo file alla cartella aperta in VSCode.
2. Assegnare un nome al file *MyClass.cs*. È necessario salvarlo con l'estensione `.cs` alla fine in modo che venga riconosciuto come file csharp.
3. Aggiungere il codice seguente per creare la prima classe. Assicurarsi di includere lo spazio dei nomi corretto in modo da potervi fare riferimento dal file *di Program.cs:*

    ``` csharp
    using System;

    namespace HelloWorld
    {
        public class MyClass
        {
            public string ReturnMessage()
            {
                return "Happy coding!";
            }
        }
    }
    ```

4. Chiamare la nuova classe dal metodo principale in Program.cs aggiungendo il codice seguente:Call your new class from your main method in *Program.cs* by adding the code below:

    ```csharp
    using System;

    namespace HelloWorld
    {
        class Program
        {
            static void Main(string[] args)
            {
                var c1 = new MyClass();
                Console.WriteLine($"Hello World! {c1.ReturnMessage()}");
            }
        }
    }
    ```

5. Salvare le modifiche ed eseguire nuovamente il programma. Verrà visualizzato il nuovo messaggio con la stringa aggiunta.

    ```dotnetcli
    dotnet run
    ```

    Si ottiene l'output seguente:

    ```console
    Hello World! Happy coding!
    ```

## <a name="faq"></a>Domande frequenti

### <a name="im-missing-required-assets-to-build-and-debug-c-in-visual-studio-code-my-debugger-says-no-configuration"></a>Non sono più disponibili gli asset necessari per compilare ed eseguire il debug di C# in Visual Studio Code. Ildebugger indica "Nessuna configurazione".

L'estensione C# di Visual Studio Code può generare gli asset necessari per compilare ed eseguire il debug. Visual Studio Code chiederà di generarli alla prima apertura di un progetto C#. Se gli asset non sono stati generati, è comunque possibile eseguire questo comando aprendo il riquadro comandi (**Visualizza > Riquadro comandi**) e digitando "> .NET: generare gli asset per la compilazione e il debug". Se si seleziona questa opzione, vengono generati i file di configurazione *.vscode*, *launch.json*e *tasks.json* necessari.

## <a name="see-also"></a>Vedere anche

- [Setting up Visual Studio Code (Impostazione di Visual Studio Code)](https://code.visualstudio.com/docs/setup/setup-overview)
- [Debugging in Visual Studio Code (Debug in Visual Studio Code)](https://code.visualstudio.com/Docs/editor/debugging)
