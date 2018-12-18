---
title: Compartilhar o retorno de log do Unity com o VSTU | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2018
ms.technology: vs-unity-tools
ms.topic: conceptual
ms.assetid: 5d71f906-6e50-4399-b59b-d38c6dfef7ee
author: conceptdev
ms.author: crdun
manager: crdun
ms.workload:
- unity
ms.openlocfilehash: 3bf25ed2764078f2d3e0424ab34f4e4a8e470ff5
ms.sourcegitcommit: e6ef03cc415ca67f75fd1f26e0e7b8846857166d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/27/2018
ms.locfileid: "39310014"
---
# <a name="share-the-unity-log-callback-with-vstu"></a>Compartilhar o retorno de log do Unity com o VSTU
As Ferramentas do Visual Studio para Unity registram um retorno de chamada de log do Unity para transmitir seu console para o Visual Studio. Se os scripts do seu editor também registram um retorno de chamada de log do Unity, o retorno de chamada VSTU pode interferir em seu retorno de chamada. Para evitar essa possibilidade, use o evento `VisualStudioIntegration.LogCallback` para cooperar com VSTU.

## <a name="demonstrates"></a>Demonstra
 Como compartilhar o retorno de chamada de log do Unity criado pelas Ferramentas do Visual Studio para Unity.

## <a name="example"></a>Exemplo

```csharp
#if ENABLE_VSTU
using System;

using UnityEngine;
using UnityEditor;

using SyntaxTree.VisualStudio.Unity.Bridge;

[InitializeOnLoad]
public class LogCallbackHook
{
    static LogCallbackHook()
    {
        VisualStudioIntegration.LogCallback += (string condition, string trace, LogType type) =>
        {
            // place code that implements your log callback here
        };
    }
}
#endif
```

## <a name="see-also"></a>Consulte também
 [Exemplo: geração de arquivo de projeto](../cross-platform/customize-project-files-created-by-vstu.md)
