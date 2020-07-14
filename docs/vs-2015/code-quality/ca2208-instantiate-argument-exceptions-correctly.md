---
title: 'CA2208: instanciar exceções de argumento corretamente | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2208
- InstantiateArgumentExceptionsCorrectly
helpviewer_keywords:
- InstantiateArgumentExceptionsCorrectly
- CA2208
ms.assetid: e2a48939-d9fa-478c-b2f9-3bdbce07dff7
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 6a63ebb7f3946926864c4dd882c281b5dcd7c6c5
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85535831"
---
# <a name="ca2208-instantiate-argument-exceptions-correctly"></a>CA2208: Criar instância de exceções de argumento corretamente
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|InstantiateArgumentExceptionsCorrectly|
|CheckId|CA2208|
|Categoria|Microsoft. Usage|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 As possíveis causas incluem as seguintes situações:

- É feita uma chamada para o Construtor (sem parâmetros) padrão de um tipo de exceção que é ou deriva de [System. ArgumentException] (<!-- TODO: review code entity reference <xref:assetId:///System.ArgumentException?qualifyHint=True&amp;autoUpgrade=True>  -->).

- Um argumento de cadeia de caracteres incorreto é passado para um construtor com parâmetros de um tipo de exceção que é ou deriva de [System. ArgumentException.] (<!-- TODO: review code entity reference <xref:assetId:///System.ArgumentException.?qualifyHint=True&amp;autoUpgrade=True>  -->)

## <a name="rule-description"></a>Descrição da Regra
 Em vez de chamar o construtor padrão, chame uma das sobrecargas do construtor que permite que uma mensagem de exceção mais significativa seja fornecida. A mensagem de exceção deve ter como alvo o desenvolvedor e explicar claramente a condição de erro e como corrigir ou evitar a exceção.

 As assinaturas de um e dois construtores de cadeia de caracteres de <xref:System.ArgumentException> e seus tipos derivados não são consistentes em relação `message` aos `paramName` parâmetros e. Verifique se esses construtores são chamados com os argumentos de cadeia de caracteres corretos. As assinaturas são as seguintes:

 <xref:System.ArgumentException>(cadeia de caracteres `message` )

 <xref:System.ArgumentException>(cadeia `message` de caracteres, Cadeia de caracteres `paramName` )

 <xref:System.ArgumentNullException>(cadeia de caracteres `paramName` )

 <xref:System.ArgumentNullException>(cadeia `paramName` de caracteres, Cadeia de caracteres `message` )

 <xref:System.ArgumentOutOfRangeException>(cadeia de caracteres `paramName` )

 <xref:System.ArgumentOutOfRangeException>(cadeia `paramName` de caracteres, Cadeia de caracteres `message` )

 <xref:System.DuplicateWaitObjectException>(cadeia de caracteres `parameterName` )

 <xref:System.DuplicateWaitObjectException>(cadeia `parameterName` de caracteres, Cadeia de caracteres `message` )

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, chame um construtor que receba uma mensagem, um nome de parâmetro ou ambos, e verifique se os argumentos são adequados para o tipo de <xref:System.ArgumentException> chamada.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso dessa regra somente se um construtor com parâmetros for chamado com os argumentos de cadeia de caracteres corretos.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um construtor que instancia incorretamente uma instância do tipo ArgumentNullException.

 [!code-cpp[FxCop.Usage.InstantiateArgumentExceptionsCorrectly#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Usage.InstantiateArgumentExceptionsCorrectly/cpp/FxCop.Usage.InheritedPublic.cpp#1)]
 [!code-csharp[FxCop.Usage.InstantiateArgumentExceptionsCorrectly#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.InstantiateArgumentExceptionsCorrectly/cs/FxCop.Usage.InheritedPublic.cs#1)]
 [!code-vb[FxCop.Usage.InstantiateArgumentExceptionsCorrectly#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.InstantiateArgumentExceptionsCorrectly/vb/FxCop.Usage.InstantiateArgumentExceptionsCorrectly.vb#1)]

## <a name="example"></a>Exemplo
 O exemplo a seguir corrige a violação acima alternando os argumentos do construtor.

 [!code-cpp[FxCop.Usage.InstantiateArgumentExceptionsCorrectly#2](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Usage.InstantiateArgumentExceptionsCorrectly/cpp/FxCop.Usage.InheritedPublic.cpp#2)]
 [!code-csharp[FxCop.Usage.InstantiateArgumentExceptionsCorrectly#2](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.InstantiateArgumentExceptionsCorrectly/cs/FxCop.Usage.InheritedPublic.cs#2)]
 [!code-vb[FxCop.Usage.InstantiateArgumentExceptionsCorrectly#2](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.InstantiateArgumentExceptionsCorrectly/vb/FxCop.Usage.InstantiateArgumentExceptionsCorrectly.vb#2)]
