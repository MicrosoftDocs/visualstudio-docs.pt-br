---
title: Diretivas de modelo de texto T4
description: Saiba mais sobre as diretivas de modelo de teste do T4 e como elas fornecem instruções para o mecanismo de transformação do modelo de texto.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, import directive
- text templates, include directive
- text templates, assembly directive
- text templates, output directive
- text templates, directives
- text templates, template directive
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 0d9b7ca189ced11eea57e175a06b81161090070b
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112388731"
---
# <a name="t4-text-template-directives"></a>Diretivas de modelo de texto T4

As diretivas fornecem instruções para o mecanismo de transformação do modelo de texto.

A sintaxe das diretivas é a seguinte:

```
<#@ DirectiveName [AttributeName = "AttributeValue"] ... #>
```

Todos os valores dos atributos devem estar entre aspas duplas. Se o próprio valor contiver aspas, elas devem ser substituídas pelo caractere \.

As diretivas são normalmente os primeiros elementos de um arquivo de modelo ou de um arquivo incluído. Você não deve inseri-las em um bloco de códigos `<#...#>`, nem depois de um bloco de recursos da classe `<#+...#>`.

[Diretiva de modelo T4](../modeling/t4-template-directive.md)

```
<#@ template [language="VB"] [hostspecific="true|TrueFromBase"] [debug="true"] [inherits="templateBaseClass"] [culture="code"] [compilerOptions="options"] [visibility="internal"] [linePragmas="false"] #>
```

[Diretiva de parâmetro T4](../modeling/t4-parameter-directive.md)

```
<#@ parameter type="Full.TypeName" name="ParameterName" #>
```

[T4 Diretiva de saída](../modeling/t4-output-directive.md)

```
<#@ output extension=".fileNameExtension" [encoding="encoding"] #>
```

[Diretiva de assembly T4](../modeling/t4-assembly-directive.md)

```
<#@ assembly name="[assembly strong name|assembly file name]" #>
```

[Diretiva de importação T4](../modeling/t4-import-directive.md)

```
<#@ import namespace="namespace" #>
```

[Diretiva de inclusão T4](../modeling/t4-include-directive.md)

```
<#@ include file="filePath" #>
```

[Diretiva CleanUpBehavior T4](../modeling/t4-cleanupbehavior-directive.md)

```
<#@ CleanupBehavior processor="T4VSHost" CleanupAfterProcessingtemplate="true" #>
```

Além disso, você pode criar suas próprias diretivas. Para obter mais informações, consulte [criando processadores de diretiva de modelo de texto T4 personalizados](../modeling/creating-custom-t4-text-template-directive-processors.md). Se você usar o SDK de Visualização e Modelagem para criar uma linguagem específica do domínio (DSL), um processador de diretriz será gerado como parte da DSL.
