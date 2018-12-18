---
title: 'CA2208: instanciar exceções de argumento corretamente'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2208
- InstantiateArgumentExceptionsCorrectly
helpviewer_keywords:
- InstantiateArgumentExceptionsCorrectly
- CA2208
ms.assetid: e2a48939-d9fa-478c-b2f9-3bdbce07dff7
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: f7a10d126d5432a80b146fe2086c01064d83006e
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45547429"
---
# <a name="ca2208-instantiate-argument-exceptions-correctly"></a>CA2208: instanciar exceções de argumento corretamente

|||
|-|-|
|NomeDoTipo|InstantiateArgumentExceptionsCorrectly|
|CheckId|CA2208|
|Categoria|Microsoft.Usage|
|Alteração Significativa|Não separável|

## <a name="cause"></a>Causa

Possíveis causas incluem as seguintes situações:

- É feita uma chamada ao construtor (sem parâmetros) padrão de um tipo de exceção que seja ou derive de <xref:System.ArgumentException>.

- Um argumento de cadeia de caracteres incorreto é passado para um construtor com parâmetros de um tipo de exceção que seja ou derive de <xref:System.ArgumentException>.

## <a name="rule-description"></a>Descrição da regra

Em vez de chamar o construtor padrão, chame uma das sobrecargas de construtor que permite que uma mensagem de exceção mais significativa a ser fornecido. A mensagem de exceção deve direcionar o desenvolvedor e explicam claramente a condição de erro e como corrigir ou evitar a exceção.

As assinaturas dos construtores de cadeia de caracteres de uma e duas de <xref:System.ArgumentException> e seus tipos derivados não são consistentes com relação ao `message` e `paramName` parâmetros. Verifique se que esses construtores são chamados com os argumentos de cadeia de caracteres correta. As assinaturas são da seguinte maneira:

 <xref:System.ArgumentException>(cadeia de caracteres `message`)

 <xref:System.ArgumentException>(cadeia de caracteres `message`, cadeia de caracteres `paramName`)

 <xref:System.ArgumentNullException>(cadeia de caracteres `paramName`)

 <xref:System.ArgumentNullException>(cadeia de caracteres `paramName`, cadeia de caracteres `message`)

 <xref:System.ArgumentOutOfRangeException>(cadeia de caracteres `paramName`)

 <xref:System.ArgumentOutOfRangeException>(cadeia de caracteres `paramName`, cadeia de caracteres `message`)

 <xref:System.DuplicateWaitObjectException>(cadeia de caracteres `parameterName`)

 <xref:System.DuplicateWaitObjectException>(cadeia de caracteres `parameterName`, cadeia de caracteres `message`)

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, chamar um construtor que aceita uma mensagem, um nome de parâmetro ou ambos e verifique se os argumentos são apropriados para o tipo de <xref:System.ArgumentException> que está sendo chamado.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 É seguro suprimir um aviso nessa regra somente se um construtor parametrizado é chamado com os argumentos de cadeia de caracteres correta.

## <a name="example-1"></a>Exemplo 1
 O exemplo a seguir mostra um construtor que instancia incorretamente uma instância do tipo ArgumentNullException.

 [!code-cpp[FxCop.Usage.InstantiateArgumentExceptionsCorrectly#1](../code-quality/codesnippet/CPP/ca2208-instantiate-argument-exceptions-correctly_1.cpp)]
 [!code-csharp[FxCop.Usage.InstantiateArgumentExceptionsCorrectly#1](../code-quality/codesnippet/CSharp/ca2208-instantiate-argument-exceptions-correctly_1.cs)]
 [!code-vb[FxCop.Usage.InstantiateArgumentExceptionsCorrectly#1](../code-quality/codesnippet/VisualBasic/ca2208-instantiate-argument-exceptions-correctly_1.vb)]

## <a name="example-2"></a>Exemplo 2
 O exemplo a seguir corrige a violação acima alternando os argumentos de construtor.

 [!code-cpp[FxCop.Usage.InstantiateArgumentExceptionsCorrectly#2](../code-quality/codesnippet/CPP/ca2208-instantiate-argument-exceptions-correctly_2.cpp)]
 [!code-csharp[FxCop.Usage.InstantiateArgumentExceptionsCorrectly#2](../code-quality/codesnippet/CSharp/ca2208-instantiate-argument-exceptions-correctly_2.cs)]
 [!code-vb[FxCop.Usage.InstantiateArgumentExceptionsCorrectly#2](../code-quality/codesnippet/VisualBasic/ca2208-instantiate-argument-exceptions-correctly_2.vb)]