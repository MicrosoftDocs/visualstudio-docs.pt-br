---
title: 'CA1032: Implementar construtores de exceção padrão | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- CA1032
- ImplementStandardExceptionConstructors
helpviewer_keywords:
- CA1032
- ImplementStandardExceptionConstructors
ms.assetid: a8623c56-273a-4c95-8d83-95911a042be7
caps.latest.revision: 18
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: efef441e84c4f1d51c633e3fdcb2da8d1ba3e963
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49868606"
---
# <a name="ca1032-implement-standard-exception-constructors"></a>CA1032: implementar construtores de exceção padrão
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|ImplementStandardExceptionConstructors|
|CheckId|CA1032|
|Categoria|Microsoft.Design|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa
 Estende um tipo <xref:System.Exception?displayProperty=fullName> e não declare construtores necessários.

## <a name="rule-description"></a>Descrição da Regra
 Tipos de exceção devem implementar os seguintes construtores:

- NewException() pública

- NewException(string) pública

- público NewException exceção (string)

- NewException protegida ou privada (SerializationInfo, StreamingContext)

  Deixar de fornecer o conjunto completo de construtores pode dificultar o tratamento correto das exceções. Por exemplo, o construtor que tem a assinatura `NewException(string, Exception)` é usado para criar as exceções causadas por outras exceções. Sem esse construtor não é possível criar e lançar uma instância de sua exceção personalizada que contém a exceção interna (aninhada), que é o que o código gerenciado deve fazer nessa situação. Os construtores de três exceção primeiros são públicos por convenção. O quarto construtor é protegido em classes não seladas e privado em classes sealed. Para obter mais informações, consulte [CA2229: implementar construtores de serialização](../code-quality/ca2229-implement-serialization-constructors.md)

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, adicionar os construtores ausentes para a exceção e certifique-se de que eles têm a acessibilidade correta.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso nessa regra, quando a violação é causada pelo uso de um nível de acesso diferentes para os construtores públicos.

## <a name="example"></a>Exemplo
 O exemplo a seguir contém um tipo de exceção que viola essa regra e um tipo de exceção que é implementado corretamente.

 [!code-csharp[FxCop.Design.ExceptionMultipleCtors#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.ExceptionMultipleCtors/cs/FxCop.Design.ExceptionMultipleCtors.cs#1)]



