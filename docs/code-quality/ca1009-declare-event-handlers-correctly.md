---
title: 'CA1009: declarar manipuladores de eventos corretamente'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1009
- DeclareEventHandlersCorrectly
helpviewer_keywords:
- CA1009
- DeclareEventHandlersCorrectly
ms.assetid: ab65c471-1449-49d2-9896-7b9af74284b4
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 7697b394396f729133b7cb6a7f3c0501c5c45202
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45547390"
---
# <a name="ca1009-declare-event-handlers-correctly"></a>CA1009: declarar manipuladores de eventos corretamente

|||
|-|-|
|NomeDoTipo|DeclareEventHandlersCorrectly|
|CheckId|CA1009|
|Categoria|Microsoft.Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um delegado que manipula um evento público ou protegido não tem a assinatura correta, tipo de retorno, ou nomes de parâmetro.

## <a name="rule-description"></a>Descrição da regra
 Os métodos de manipulador de eventos utilizam dois parâmetros. A primeira é do tipo <xref:System.Object?displayProperty=fullName> e é denominado 'remetente'. Este é o objeto que acionou o evento. O segundo parâmetro é do tipo <xref:System.EventArgs?displayProperty=fullName> e é chamado 'e'. Esses são os dados associados ao evento. Por exemplo, se o evento é gerado sempre que um arquivo é aberto, os dados de evento normalmente contém o nome do arquivo.

 Métodos do manipulador de eventos não devem retornar um valor. No c# linguagem de programação, isso é indicado pelo tipo de retorno `void`. Um manipulador de eventos pode chamar vários métodos em vários objetos. Se os métodos eram permitidos para retornar um valor, vários valores de retorno ocorreria para cada evento, e apenas o valor do último método que foi invocado estaria disponível.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, corrija a assinatura, tipo de retorno ou nomes de parâmetro do delegado. Para obter detalhes, consulte o exemplo a seguir.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um delegado que é adequado para manipulação de eventos. Os métodos que podem ser invocados por este manipulador de eventos está em conformidade com a assinatura que é especificada nas diretrizes de Design. `AlarmEventHandler` é o nome do tipo do delegado. `AlarmEventArgs` deriva da classe base para os dados de evento, <xref:System.EventArgs>, e mantém dados de evento do alarme.

 [!code-cpp[FxCop.Design.EventsTwoParams#1](../code-quality/codesnippet/CPP/ca1009-declare-event-handlers-correctly_1.cpp)]
 [!code-csharp[FxCop.Design.EventsTwoParams#1](../code-quality/codesnippet/CSharp/ca1009-declare-event-handlers-correctly_1.cs)]
 [!code-vb[FxCop.Design.EventsTwoParams#1](../code-quality/codesnippet/VisualBasic/ca1009-declare-event-handlers-correctly_1.vb)]

## <a name="related-rules"></a>Regras relacionadas
 [CA2109: examinar manipuladores de eventos visíveis](../code-quality/ca2109-review-visible-event-handlers.md)

## <a name="see-also"></a>Consulte também

- <xref:System.EventArgs?displayProperty=fullName>
- <xref:System.Object?displayProperty=fullName>
- [Manipulando e acionando eventos](/dotnet/standard/events/index)