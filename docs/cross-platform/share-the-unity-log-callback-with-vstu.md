---
title: Compartilhar o retorno de log do Unity com o VSTU | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2018
ms.technology: vs-unity-tools
ms.topic: conceptual
ms.assetid: 5d71f906-6e50-4399-b59b-d38c6dfef7ee
author: therealjohn
ms.author: johmil
manager: crdun
ms.workload:
- unity
ms.openlocfilehash: aa8a4a229102a6a9439ffb36582cd03e322a086b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62815659"
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
 [Exemplo: Geração de arquivo de projeto](../cross-platform/customize-project-files-created-by-vstu.md)
