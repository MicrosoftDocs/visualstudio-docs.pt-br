---
title: 'CA1801: Revisar parâmetros não utilizados | Microsoft Docs'
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
- AvoidUnusedParameters
- CA1801
- ReviewUnusedParameters
helpviewer_keywords:
- CA1801
- ReviewUnusedParameters
ms.assetid: 5d73545c-e153-4b7c-a7b2-be6bf5aca5be
caps.latest.revision: 31
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: b0946e315aef0c333207d49eb14820d287a9b361
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49269666"
---
# <a name="ca1801-review-unused-parameters"></a>CA1801: revisar parâmetros não usados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Para obter a documentação mais recente do Visual Studio 2017, consulte [CA1801: revisar parâmetros não utilizados](https://docs.microsoft.com/visualstudio/code-quality/ca1801-review-unused-parameters) em docs.microsoft.com.  
  
|||  
|-|-|  
|NomeDoTipo|ReviewUnusedParameters|  
|CheckId|CA1801|  
|Categoria|Microsoft.Usage|  
|Alteração Significativa|Não separável - se o membro não é visível fora do assembly, independentemente da alteração feita.<br /><br /> Não separável - se você alterar o membro para usar o parâmetro em seu corpo.<br /><br /> Quebrando - se você remover o parâmetro e é visível fora do assembly.|  
  
## <a name="cause"></a>Causa  
 Uma assinatura de método inclui um parâmetro que não é usado no corpo do método. Essa regra não examina os métodos a seguir:  
  
-   Métodos referenciados por um delegado.  
  
-   Métodos usados como manipuladores de eventos.  
  
-   Os métodos declarados com o `abstract` (`MustOverride` no Visual Basic) modificador.  
  
-   Os métodos declarados com o `virtual` (`Overridable` no Visual Basic) modificador.  
  
-   Os métodos declarados com o `override` (`Overrides` no Visual Basic) modificador.  
  
-   Os métodos declarados com o `extern` (`Declare` instrução no Visual Basic) modificador.  
  
## <a name="rule-description"></a>Descrição da Regra  
 Revise os parâmetros em métodos não virtuais que não são usados no corpo do método para verificar se que nenhuma correção existe em torno de falha para acessá-los. Parâmetros não utilizados incorrem em custos de manutenção e desempenho.  
  
 Às vezes, uma violação dessa regra pode apontar para um bug de implementação no método. Por exemplo, o parâmetro deve ter sido usado no corpo do método. Suprima avisos desta regra se o parâmetro precisar existir devido à compatibilidade com versões anteriores.  
  
## <a name="how-to-fix-violations"></a>Como Corrigir Violações  
 Para corrigir uma violação dessa regra, remova o parâmetro não utilizado (uma alteração significativa) ou use o parâmetro no corpo do método (uma alteração sem interrupção).  
  
## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos  
 É seguro suprimir um aviso nessa regra para o código fornecido anteriormente para o qual a correção seria uma alteração significativa.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra dois métodos. Um método viola a regra e o outro método satisfaz a regra.  
  
 [!code-csharp[FxCop.Usage.ReviewUnusedParameters#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.ReviewUnusedParameters/cs/FxCop.Usage.ReviewUnusedPerameters.cs#1)]  
  
## <a name="related-rules"></a>Regras relacionadas  
 [CA1811: evitar código privado não chamado](../code-quality/ca1811-avoid-uncalled-private-code.md)  
  
 [CA1812: evitar classes internas sem instâncias](../code-quality/ca1812-avoid-uninstantiated-internal-classes.md)  
  
 [CA1804: remover locais não usados](../code-quality/ca1804-remove-unused-locals.md)

