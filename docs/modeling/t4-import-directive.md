---
title: Diretiva de importação T4
ms.date: 11/04/2016
ms.topic: reference
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.openlocfilehash: 6df6b3f4677e53fd2105d616a4be42156848504b
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2019
ms.locfileid: "53842220"
---
# <a name="t4-import-directive"></a>Diretiva de importação T4

Em blocos de código de um modelo de texto T4 do Visual Studio, o `import` diretiva permite que você se referir a elementos em outro namespace sem fornecer um nome totalmente qualificado. É o equivalente de `using` em C# ou `imports` em [!INCLUDE[vb_current_short](../debugger/includes/vb_current_short_md.md)].

Para obter uma visão geral da gravação de modelos de texto T4, consulte [gravando um modelo de texto T4](../modeling/writing-a-t4-text-template.md).

## <a name="using-the-import-directive"></a>Usando a diretiva de importação

```
<#@ import namespace="namespace" #>
```

 Neste exemplo, o código do modelo pode omitir um namespace explícito para membros de System.IO:

```
<#@ import namespace="System.IO" #>
<#
   string fileContent = File.ReadAllText("C:\x.txt"); // System.IO.File
#>
The file contains: <#=  fileContent #>
```

## <a name="standard-imports"></a>Importações padrão
 O seguinte namespace é importado automaticamente, para que não seja necessário gravar uma diretiva de importação para ele:

- `System`

  Além disso, se você usar uma diretiva personalizada, o processador de diretriz pode importar alguns namespaces automaticamente.

  Por exemplo, se você gravar modelos para uma linguagem específica do domínio (DSL), você não precisa gravar diretivas de importação para os namespaces a seguir:

- `Microsoft.VisualStudio.Modeling`

- Namespace de sua DSL

## <a name="see-also"></a>Consulte também

- [Diretiva de assembly T4](../modeling/t4-assembly-directive.md)