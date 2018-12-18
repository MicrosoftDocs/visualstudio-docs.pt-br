---
title: 'CA1009: Declarar manipuladores de eventos corretamente | Microsoft Docs'
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
- CA1009
- DeclareEventHandlersCorrectly
helpviewer_keywords:
- CA1009
- DeclareEventHandlersCorrectly
ms.assetid: ab65c471-1449-49d2-9896-7b9af74284b4
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 7a405ebbf4cd11a695c6e93231d260d8ceae2483
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49918500"
---
# <a name="ca1009-declare-event-handlers-correctly"></a>CA1009: declarar manipuladores de eventos corretamente
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|DeclareEventHandlersCorrectly|
|CheckId|CA1009|
|Categoria|Microsoft.Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um delegado que manipula um evento público ou protegido não tem a assinatura correta, tipo de retorno, ou nomes de parâmetro.

## <a name="rule-description"></a>Descrição da Regra
 Os métodos de manipulador de eventos utilizam dois parâmetros. A primeira é do tipo <xref:System.Object?displayProperty=fullName> e é denominado 'remetente'. Este é o objeto que acionou o evento. O segundo parâmetro é do tipo <xref:System.EventArgs?displayProperty=fullName> e é chamado 'e'. Esses são os dados associados ao evento. Por exemplo, se o evento é gerado sempre que um arquivo é aberto, os dados de evento normalmente contém o nome do arquivo.

 Métodos do manipulador de eventos não devem retornar um valor. No c# linguagem de programação, isso é indicado pelo tipo de retorno `void`. Um manipulador de eventos pode chamar vários métodos em vários objetos. Se os métodos eram permitidos para retornar um valor, vários valores de retorno ocorreria para cada evento, e apenas o valor do último método que foi invocado estaria disponível.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, corrija a assinatura, tipo de retorno ou nomes de parâmetro do delegado. Para obter detalhes, consulte o exemplo a seguir.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um delegado que é adequado para manipulação de eventos. Os métodos que podem ser invocados por este manipulador de eventos está em conformidade com a assinatura que é especificada nas diretrizes de Design. `AlarmEventHandler` é o nome do tipo do delegado. `AlarmEventArgs` deriva da classe base para os dados de evento, <xref:System.EventArgs>, e mantém dados de evento do alarme.

 [!code-cpp[FxCop.Design.EventsTwoParams#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.EventsTwoParams/cpp/FxCop.Design.EventsTwoParams.cpp#1)]
 [!code-csharp[FxCop.Design.EventsTwoParams#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.EventsTwoParams/cs/FxCop.Design.EventsTwoParams.cs#1)]
 [!code-vb[FxCop.Design.EventsTwoParams#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.EventsTwoParams/vb/FxCop.Design.EventsTwoParams.vb#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA2109: examinar manipuladores de eventos visíveis](../code-quality/ca2109-review-visible-event-handlers.md)

## <a name="see-also"></a>Consulte também
 <xref:System.EventArgs?displayProperty=fullName> <xref:System.Object?displayProperty=fullName>
 [NIB: Eventos e delegados](http://msdn.microsoft.com/en-us/d98fd58b-fa4f-4598-8378-addf4355a115)



