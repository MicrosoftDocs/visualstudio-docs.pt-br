---
title: 'CA1053: tipos de detentor estáticos não devem ter construtores | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- StaticHolderTypesShouldNotHaveConstructors
- CA1053
helpviewer_keywords:
- CA1053
- StaticHolderTypesShouldNotHaveConstructors
ms.assetid: 10302b9a-fa5e-4935-a06a-513d9600f613
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 29cc322dd59dc0de66af8f92a46524d15b0022c7
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85539575"
---
# <a name="ca1053-static-holder-types-should-not-have-constructors"></a>CA1053: Tipos de suporte estático não devem ter construtores
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|StaticHolderTypesShouldNotHaveConstructors|
|CheckId|CA1053|
|Categoria|Microsoft. Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo público ou público aninhado declara apenas membros estáticos e tem um construtor padrão público ou protegido.

## <a name="rule-description"></a>Descrição da Regra
 O construtor é desnecessário porque chamar membros estáticos não exige uma instância do tipo. Além disso, como o tipo não tem membros não estáticos, a criação de uma instância não fornece acesso a nenhum dos membros do tipo.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, remova o construtor padrão ou torne-o privado.

> [!NOTE]
> Alguns compiladores criam automaticamente um construtor padrão público se o tipo não define nenhum construtor. Se esse for o caso com o tipo, adicione um construtor padrão privado para eliminar a violação.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra. A presença do Construtor sugere que o tipo não é um tipo estático.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo que viola essa regra. Observe que não há nenhum construtor padrão no código-fonte. Quando esse código é compilado em um assembly, o compilador C# insere um construtor padrão, que violará essa regra. Para corrigir isso, declare um Construtor privado.

 [!code-csharp[FxCop.Design.StaticTypes#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.StaticTypes/cs/FxCop.Design.StaticTypes.cs#1)]
