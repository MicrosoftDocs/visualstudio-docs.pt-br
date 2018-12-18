---
title: 'CA2119: Métodos para lacrar que atendam a interfaces privadas | Microsoft Docs'
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
- SealMethodsThatSatisfyPrivateInterfaces
- CA2119
helpviewer_keywords:
- CA2119
- SealMethodsThatSatisfyPrivateInterfaces
ms.assetid: 483d02e1-cfaf-4754-a98f-4116df0f3509
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: c6d3e102cde1fc010f777006d629fa2d19add894
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49825374"
---
# <a name="ca2119-seal-methods-that-satisfy-private-interfaces"></a>CA2119: os métodos para lacrar que atendam a interfaces privadas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|SealMethodsThatSatisfyPrivateInterfaces|
|CheckId|CA2119|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo público herdável fornece uma implementação de método substituível de uma `internal` (`Friend` no Visual Basic) interface.

## <a name="rule-description"></a>Descrição da Regra
 Métodos de interface tem acessibilidade pública, que não pode ser alterada por tipo de implementação. Uma interface interna cria um contrato que não se destina a ser implementada fora do assembly que define a interface. Um tipo público que implementa um método de uma interface interna usando o `virtual` (`Overridable` no Visual Basic) modificador permite que o método a ser substituído por um tipo derivado que está fora do assembly. Se um segundo tipo no assembly de definição chama o método e espera que um contrato somente interno, o comportamento pode ficar comprometido quando, em vez disso, o método substituído no assembly externo é executado. Isso cria uma vulnerabilidade de segurança.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, impedir que o método que está sendo substituído fora do assembly usando um dos seguintes:

-   Verifique o tipo de declaração `sealed` (`NotInheritable` no Visual Basic).

-   Altere a acessibilidade do tipo declarativo para `internal` (`Friend` no Visual Basic).

-   Remova todos os construtores públicos do tipo de declaração.

-   Implementar o método sem usar o `virtual` modificador.

-   Implemente o método explicitamente.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso desta regra se, depois de uma análise cuidadosa, há nenhum problema de segurança que pode ser explorável se o método for substituído fora do assembly.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo, `BaseImplementation`, que viola essa regra.

 [!code-cpp[FxCop.Security.SealMethods1#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Security.SealMethods1/cpp/FxCop.Security.SealMethods1.cpp#1)]
 [!code-csharp[FxCop.Security.SealMethods1#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.SealMethods1/cs/FxCop.Security.SealMethods1.cs#1)]
 [!code-vb[FxCop.Security.SealMethods1#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Security.SealMethods1/vb/FxCop.Security.SealMethods1.vb#1)]

## <a name="example"></a>Exemplo
 O exemplo a seguir explora a implementação do método virtual do exemplo anterior.

 [!code-cpp[FxCop.Security.SealMethods2#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Security.SealMethods2/cpp/FxCop.Security.SealMethods2.cpp#1)]
 [!code-csharp[FxCop.Security.SealMethods2#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.SealMethods2/cs/FxCop.Security.SealMethods2.cs#1)]
 [!code-vb[FxCop.Security.SealMethods2#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Security.SealMethods2/vb/FxCop.Security.SealMethods2.vb#1)]

## <a name="see-also"></a>Consulte também
 [Interfaces](http://msdn.microsoft.com/library/2feda177-ce11-432d-81b4-d50f5f35fd37) [Interfaces](http://msdn.microsoft.com/library/61b06674-12c9-430b-be68-cc67ecee1f5b)



