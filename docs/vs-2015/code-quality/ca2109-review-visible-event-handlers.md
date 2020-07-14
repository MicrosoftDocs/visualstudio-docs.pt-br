---
title: 'CA2109: examinar os manipuladores de eventos visíveis | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2109
- ReviewVisibleEventHandlers
helpviewer_keywords:
- ReviewVisibleEventHandlers
- CA2109
ms.assetid: 8f8fa0ee-e94e-400e-b516-24d8727725d7
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 3ddcab6e0f416837bcd7b01521a6d77ddce691b9
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85520972"
---
# <a name="ca2109-review-visible-event-handlers"></a>CA2109: Examinar manipuladores de eventos visíveis
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|ReviewVisibleEventHandlers|
|CheckId|CA2109|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um método público ou protegido de tratamento de eventos foi detectado.

## <a name="rule-description"></a>Descrição da Regra
 Um método de manipulação de eventos visível externamente apresenta um problema de segurança que requer revisão.

 Os métodos de tratamento de eventos não devem ser expostos, a menos que seja absolutamente necessário. Um manipulador de eventos, um tipo delegado, que invoca o método exposto, pode ser adicionado a qualquer evento, desde que o manipulador e as assinaturas de eventos correspondam. Os eventos podem potencialmente ser gerados por qualquer código e são gerados com frequência por código de sistema altamente confiável em resposta a ações do usuário, como clicar em um botão. Adicionar uma verificação de segurança a um método de manipulação de eventos não impede que o código registre um manipulador de eventos que invoque o método.

 Uma demanda não pode proteger de maneira confiável um método invocado por um manipulador de eventos. As demandas de segurança ajudam a proteger o código de chamadores não confiáveis examinando os chamadores na pilha de chamadas. O código que adiciona um manipulador de eventos a um evento não está necessariamente presente na pilha de chamadas quando os métodos do manipulador de eventos são executados. Portanto, a pilha de chamadas pode ter apenas chamadores altamente confiáveis quando o método do manipulador de eventos é invocado. Isso faz com que as demandas feitas pelo método manipulador de eventos tenham sucesso. Além disso, a permissão exigida pode ser declarada quando o método é invocado. Por esses motivos, o risco de não corrigir uma violação dessa regra só pode ser avaliado após a revisão do método de manipulação de eventos. Ao examinar seu código, considere os seguintes problemas:

- O manipulador de eventos executa qualquer operação que seja perigosa ou explorável, como a declaração de permissões ou a supressão de permissão de código não gerenciado?

- Quais são as ameaças de segurança de e para seu código, pois podem ser executadas a qualquer momento com chamadores altamente confiáveis na pilha?

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, examine o método e avalie o seguinte:

- Você pode tornar o método de manipulação de eventos não público?

- Você pode mover toda a funcionalidade perigosa do manipulador de eventos?

- Se uma demanda de segurança for imposta, isso poderá ser feito de alguma outra maneira?

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Suprimir um aviso desta regra somente após uma revisão de segurança cuidadosa para certificar-se de que seu código não representa uma ameaça de segurança.

## <a name="example"></a>Exemplo
 O código a seguir mostra um método de manipulação de eventos que pode ser usado por código mal-intencionado.

 [!code-csharp[FxCop.Security.EventSecLib#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.EventSecLib/cs/FxCop.Security.EventSecLib.cs#1)]

## <a name="see-also"></a>Consulte Também
 <xref:System.Security.CodeAccessPermission.Demand%2A?displayProperty=fullName> <xref:System.EventArgs?displayProperty=fullName>
 [Demandas de segurança](https://msdn.microsoft.com/324c14f8-54ff-494d-9fd1-bfd20962c8ba)
