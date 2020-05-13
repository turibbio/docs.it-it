---
title: Contenuto degli assembly
description: Questo articolo descrive il contenuto di un assembly .NET, che può includere metadati dell'assembly, metadati del tipo, codice MSIL e risorse.
ms.date: 08/20/2019
helpviewer_keywords:
- assemblies [.NET Framework]
- assemblies [.NET Core]
- single-file assemblies
ms.assetid: 28116714-da77-45f7-826d-fa035d121948
ms.openlocfilehash: 94df452162ed7290fab7fa267d2624e6d844a587
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/13/2020
ms.locfileid: "83378564"
---
# <a name="assembly-contents"></a>Contenuto degli assembly

Per grandi linee, un assembly statico è costituito da quattro elementi:

- Il [manifesto dell'assembly](manifest.md) che contiene i metadati dell'assembly.

- I metadati dei tipi.  

- Il codice Microsoft Intermediate Language (MSIL) che implementa i tipi. Viene generato dal compilatore da uno o più file di codice sorgente.

- Set di [risorse](../../framework/resources/index.md).  

Il manifesto dell'assembly è il solo elemento obbligatorio, ma il corretto funzionamento dell'assembly dipende anche dalla presenza di tipi o risorse.

Nella figura seguente vengono illustrati questi elementi raggruppati in un singolo file fisico:

![Assembly A file singolo denominato myAssembly. dll](./media/contents/single-file-assembly.gif)

Quando si progetta il codice sorgente, si prendono decisioni esplicite su come partizionare le funzionalità dell'applicazione in uno o più file. Quando si progetta il codice .NET, è possibile prendere decisioni simili su come partizionare le funzionalità in uno o più assembly.

## <a name="see-also"></a>Vedere anche

- [Assembly in .NET](index.md)
- [Manifesto dell'assembly](manifest.md)
- [Considerazioni sulla sicurezza degli assembly](security-considerations.md)
