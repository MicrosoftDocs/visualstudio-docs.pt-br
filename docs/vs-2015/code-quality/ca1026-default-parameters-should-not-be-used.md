---
title: 'CA1026: Parâmetros padrão não devem ser usados | Microsoft Docs'
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
- CA1026
- DefaultParametersShouldNotBeUsed
helpviewer_keywords:
- CA1026
- DefaultParametersShouldNotBeUsed
ms.assetid: 09643415-36ef-4d0f-9411-5721e14e2512
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 5ab5fd842363c39f23981bdec93635974e2b2582
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49894359"
---
# <a name="ca1026-default-parameters-should-not-be-used"></a>CA1026: parâmetros padrão não devem ser usados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|DefaultParametersShouldNotBeUsed|
|CheckId|CA1026|
|Categoria|Microsoft.Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo visível externamente contém um método visível externamente que usa um parâmetro padrão.

## <a name="rule-description"></a>Descrição da Regra
 Métodos que usam parâmetros padrão são permitidos sob o Common Language Specification (CLS); No entanto, a CLS permite que os compiladores para ignorar os valores que são atribuídos a esses parâmetros. Código que é escrito para os compiladores que ignoram valores de parâmetro padrão deve fornecer explicitamente os argumentos para cada parâmetro padrão. Para manter o comportamento desejado em todas as linguagens de programação, os métodos que usam parâmetros padrão devem ser substituídos com sobrecargas de método que forneçam os parâmetros padrão.

 O compilador ignora os valores de parâmetros padrão para a extensão gerenciadas para C++ quando acessa o código gerenciado. O compilador do Visual Basic dá suporte a métodos com parâmetros padrão que usam o [opcional](http://msdn.microsoft.com/library/4571ce88-a539-4115-b230-54eb277c6aa7) palavra-chave.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, substitua o método que usa os parâmetros padrão com sobrecargas de método que fornecem os parâmetros padrão.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um método que usa os parâmetros padrão e os métodos sobrecarregados que fornecem uma funcionalidade equivalente.

 [!code-vb[FxCop.Design.DefaultParameters#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.DefaultParameters/vb/FxCop.Design.DefaultParameters.vb#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1025: substituir argumentos repetitivos por matriz de parâmetros](../code-quality/ca1025-replace-repetitive-arguments-with-params-array.md)

## <a name="see-also"></a>Consulte também
 [Componentes de independência de linguagem e componentes independentes da linguagem](http://msdn.microsoft.com/library/4f0b77d0-4844-464f-af73-6e06bedeafc6)



