---
title: Como personalizar os arquivos de projeto criados por VSTU | Microsoft Docs
description: Saiba como personalizar arquivos de projeto criados pelo Ferramentas do Visual Studio para Unity (VSTU). Examine um exemplo de código C#.
ms.custom: ''
ms.date: 04/19/2021
ms.technology: vs-unity-tools
ms.prod: visual-studio-dev16
ms.topic: conceptual
ms.assetid: 60b8cc1d-cacc-404d-b768-77e81bc354f8
author: conceptdev
ms.author: crdun
manager: crdun
ms.workload:
- unity
ms.openlocfilehash: a4a5973863877db2d071f9be8d4689928b21a689
ms.sourcegitcommit: 3e1ff87fba290f9e60fb4049d011bb8661255d58
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107879311"
---
# <a name="customize-project-files-created-by-vstu"></a>Personalizar arquivos de projeto criados pelo VSTU
O Unity fornece retornos de chamada durante a geração de arquivos de projeto. Implemente `OnGeneratedSlnSolution` e `OnGeneratedCSProject` métodos usando um [`AssetPostprocessor`](https://docs.unity3d.com/ScriptReference/AssetPostprocessor.html) para modificar o projeto ou o arquivo de solução sempre que ele for regenerado.

## <a name="demonstrates"></a>Demonstra
Como personalizar os arquivos de projeto do Visual Studio gerados pelas Ferramentas do Visual Studio para Unity.

## <a name="example"></a>Exemplo

```csharp
using System;
using UnityEditor;
using UnityEngine;

public class ProjectFilePostprocessor : AssetPostprocessor
{
  public static string OnGeneratedSlnSolution(string path, string content)
  {
    // TODO: process solution content
    return content;
  }

  public static string OnGeneratedCSProject(string path, string content)
  {
    // TODO: process project content
    return content;
  }
}
```
