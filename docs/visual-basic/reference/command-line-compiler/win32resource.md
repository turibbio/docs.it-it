---
title: -win32resource
ms.date: 03/13/2018
f1_keywords:
- -win32resource
- win32resource
helpviewer_keywords:
- /win32resource compiler option [Visual Basic]
- -win32resource compiler option [Visual Basic]
- win32resource compiler option [Visual Basic]
ms.assetid: e226946d-19ce-4cc9-91f5-aed24f77aa2b
ms.openlocfilehash: bcbc690690993a094bc5360d0c13bddebf8cd615
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84414246"
---
# <a name="-win32resource"></a>-win32resource
Inserisce un file di risorse Win32 nel file di output.  
  
## <a name="syntax"></a>Sintassi  
  
```console  
-win32resource:filename  
```  
  
## <a name="arguments"></a>Argomenti  
 `filename`  
 Nome del file di risorse da aggiungere al file di output. Racchiudere il nome file tra virgolette ("") se contiene uno spazio.  
  
## <a name="remarks"></a>Commenti  
 È possibile creare un file di risorse Win32 con il compilatore di risorse di Microsoft Windows (RC).  
  
 Una risorsa Win32 può contenere informazioni sulla versione o sulla bitmap (icona) che consentono di identificare l'applicazione in **Esplora file**. Se non si specifica `-win32resource` , il compilatore genera le informazioni sulla versione in base alla versione dell'assembly. Le opzioni `-win32resource` e `-win32icon` si escludono reciprocamente.  
  
 Vedere [-linkresource ((Visual Basic)](linkresource.md) per fare riferimento a un file di risorse .NET Framework o [-Resource (Visual Basic)](resource.md) per alleghire un file di risorse .NET Framework.  
  
> [!NOTE]
> L' `-win32resource` opzione non è disponibile nell'ambiente di sviluppo di Visual Studio. è disponibile solo quando si esegue la compilazione dalla riga di comando.  
  
## <a name="example"></a>Esempio  
 Il codice seguente compila `In.vb` e connette un file di risorse Win32 `Rf.res` :  
  
```console  
vbc -win32resource:rf.res in.vb  
```  
  
## <a name="see-also"></a>Vedere anche

- [Compilatore della riga di comando di Visual Basic](index.md)
- [Esempi di righe di comando di compilazione](sample-compilation-command-lines.md)
