---
title: 'CA1009: declarar manipuladores de eventos corretamente | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1009
- DeclareEventHandlersCorrectly
helpviewer_keywords:
- CA1009
- DeclareEventHandlersCorrectly
ms.assetid: ab65c471-1449-49d2-9896-7b9af74284b4
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 6a4a4e2e6990772b50568043c4d18ff29248571d
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547882"
---
# <a name="ca1009-declare-event-handlers-correctly"></a>CA1009: Declarar manipuladores de eventos corretamente
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|DeclareEventHandlersCorrectly|
|CheckId|CA1009|
|Categoria|Microsoft. Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um delegado que manipula um evento público ou protegido não tem a assinatura, o tipo de retorno ou os nomes de parâmetro corretos.

## <a name="rule-description"></a>Descrição da Regra
 Os métodos de manipulador de eventos utilizam dois parâmetros. O primeiro é do tipo <xref:System.Object?displayProperty=fullName> e é chamado de ' Remetente '. Este é o objeto que acionou o evento. O segundo parâmetro é do tipo <xref:System.EventArgs?displayProperty=fullName> e é denominado ' e '. Esses são os dados associados ao evento. Por exemplo, se o evento for gerado sempre que um arquivo for aberto, os dados do evento normalmente conterá o nome do arquivo.

 Os métodos do manipulador de eventos não devem retornar um valor. Na linguagem de programação C#, isso é indicado pelo tipo de retorno `void` . Um manipulador de eventos pode invocar vários métodos em vários objetos. Se os métodos tivessem permissão para retornar um valor, vários valores de retorno ocorreriam para cada evento, e somente o valor do último método que foi invocado estaria disponível.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, corrija a assinatura, o tipo de retorno ou os nomes de parâmetro do delegado. Para obter detalhes, consulte o exemplo a seguir.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um delegado que é adequado para manipular eventos. Os métodos que podem ser invocados por esse manipulador de eventos estão em conformidade com a assinatura especificada nas diretrizes de design. `AlarmEventHandler`é o nome do tipo do delegado. `AlarmEventArgs`deriva da classe base para dados de evento, <xref:System.EventArgs> e mantém dados de evento de alarme.

 [!code-cpp[FxCop.Design.EventsTwoParams#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.EventsTwoParams/cpp/FxCop.Design.EventsTwoParams.cpp#1)]
 [!code-csharp[FxCop.Design.EventsTwoParams#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.EventsTwoParams/cs/FxCop.Design.EventsTwoParams.cs#1)]
 [!code-vb[FxCop.Design.EventsTwoParams#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.EventsTwoParams/vb/FxCop.Design.EventsTwoParams.vb#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA2109: Examinar manipuladores de eventos visíveis](../code-quality/ca2109-review-visible-event-handlers.md)

## <a name="see-also"></a>Consulte Também
 <xref:System.EventArgs?displayProperty=fullName> <xref:System.Object?displayProperty=fullName>
 [NIB: eventos e delegados](https://msdn.microsoft.com/d98fd58b-fa4f-4598-8378-addf4355a115)
