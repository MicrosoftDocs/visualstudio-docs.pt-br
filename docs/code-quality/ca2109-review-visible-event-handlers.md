---
title: 'CA2109: revisar manipuladores de eventos visíveis'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2109
- ReviewVisibleEventHandlers
helpviewer_keywords:
- ReviewVisibleEventHandlers
- CA2109
ms.assetid: 8f8fa0ee-e94e-400e-b516-24d8727725d7
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 4df271f5427d005ef94c4c09d6c0a1eb05c850b0
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45548849"
---
# <a name="ca2109-review-visible-event-handlers"></a>CA2109: revisar manipuladores de eventos visíveis

|||
|-|-|
|NomeDoTipo|ReviewVisibleEventHandlers|
|CheckId|CA2109|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um método público ou protegido de tratamento de eventos foi detectado.

## <a name="rule-description"></a>Descrição da regra
 Um método de manipulação de eventos visível externamente apresenta um problema de segurança que exige a revisão.

Não expor os métodos de manipulação de eventos, a menos que absolutamente necessário. Um manipulador de eventos, um tipo de delegado que invoca o método exposto pode ser adicionado a qualquer evento, desde que as assinaturas de evento e o manipulador coincidam. Eventos potencialmente podem ser gerados por qualquer código e com frequência são gerados pelo código de sistema altamente confiável em resposta às ações do usuário, como clicar em um botão. Adicionar uma verificação de segurança para um método de manipulação de eventos não impedir que um código ao registrar um manipulador de eventos que chama o método.

 Uma demanda de forma confiável não pode proteger um método invocado por um manipulador de eventos. Demandas de segurança ajuda proteger o código, examinando os chamadores na pilha de chamadas de chamadores não confiáveis. Código que adiciona um manipulador de eventos a um evento não é necessariamente presente na pilha de chamadas quando executar métodos do manipulador de eventos. Portanto, a pilha de chamadas pode ter apenas altamente confiável os chamadores quando o método de manipulador de eventos é invocado. Isso faz com que as demandas feitas pelo método de manipulador de eventos seja bem-sucedida. Além disso, a permissão exigida pode ser confirmada quando o método é invocado. Por esses motivos, o risco de não corrigir uma violação dessa regra pode ser avaliado somente depois de examinar o método de manipulação de eventos. Ao examinar seu código, considere as seguintes questões:

- O seu manipulador de eventos executa todas as operações que são perigosas ou podem ser exploradas como declarar permissões ou suprimir a permissão de código não gerenciado?

- Quais são as ameaças de segurança para e do seu código, porque ele pode ser executado a qualquer momento com apenas altamente confiáveis que os chamadores na pilha?

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, examine o método e avaliar o seguinte:

- Você pode tornar o método de manipulação de eventos não público?

- Você pode mover toda a funcionalidade perigosa fora do manipulador de eventos?

- Se uma exigência de segurança é imposta, isso pode ser feito de alguma outra maneira?

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Suprima um aviso nessa regra somente após uma análise atenta da segurança para certificar-se de que seu código não representem uma ameaça de segurança.

## <a name="example"></a>Exemplo
 O código a seguir mostra um método de manipulação de eventos que pode ser usado indevidamente por códigos mal-intencionados.

 [!code-csharp[FxCop.Security.EventSecLib#1](../code-quality/codesnippet/CSharp/ca2109-review-visible-event-handlers_1.cs)]

## <a name="see-also"></a>Consulte também

- <xref:System.Security.CodeAccessPermission.Demand%2A?displayProperty=fullName>
- <xref:System.EventArgs?displayProperty=fullName>