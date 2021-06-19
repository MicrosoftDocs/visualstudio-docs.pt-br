---
title: Diretiva de importação T4
description: Saiba que, em um Visual Studio de texto T4, a diretiva de importação permite que você consulte elementos em outro namespace sem fornecer um nome totalmente qualificado.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: d0d441ec5a62dfa5266a17a06ac8fe33941136c6
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112386313"
---
# <a name="t4-import-directive"></a>Diretiva de importação T4

Nos blocos de código de um modelo de texto Visual Studio T4, a diretiva permite que você consulte elementos em outro namespace sem fornecer um nome `import` totalmente qualificado. É o equivalente de `using` em C# ou `imports` em [!INCLUDE[vb_current_short](../debugger/includes/vb_current_short_md.md)].

Para uma visão geral da escrita de modelos de texto T4, consulte [Escrevendo um modelo de texto T4](../modeling/writing-a-t4-text-template.md).

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

- Namespace da DSL

## <a name="see-also"></a>Confira também

- [Diretiva de assembly T4](../modeling/t4-assembly-directive.md)
