---
title: 'CA2109: Revisar manipuladores de eventos visíveis | Microsoft Docs'
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
- CA2109
- ReviewVisibleEventHandlers
helpviewer_keywords:
- ReviewVisibleEventHandlers
- CA2109
ms.assetid: 8f8fa0ee-e94e-400e-b516-24d8727725d7
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 328df28441fa5c96fee40baed11a54c3044542b8
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49880371"
---
# <a name="ca2109-review-visible-event-handlers"></a>CA2109: revisar manipuladores de eventos visíveis
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|ReviewVisibleEventHandlers|
|CheckId|CA2109|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um método público ou protegido de tratamento de eventos foi detectado.

## <a name="rule-description"></a>Descrição da Regra
 Um método de manipulação de eventos visível externamente apresenta um problema de segurança que exige a revisão.

 Os métodos de tratamento de eventos não devem ser expostos, a menos que seja absolutamente necessário. Um manipulador de eventos, um tipo de delegado que invoca o método exposto pode ser adicionado a qualquer evento, desde que as assinaturas de evento e o manipulador coincidam. Eventos potencialmente podem ser gerados por qualquer código e com frequência são gerados pelo código de sistema altamente confiável em resposta às ações do usuário, como clicar em um botão. Adicionar uma verificação de segurança para um método de manipulação de eventos não impedir que um código ao registrar um manipulador de eventos que chama o método.

 Uma demanda de forma confiável não pode proteger um método invocado por um manipulador de eventos. Demandas de segurança ajuda proteger o código, examinando os chamadores na pilha de chamadas de chamadores não confiáveis. Código que adiciona um manipulador de eventos a um evento não é necessariamente presente na pilha de chamadas quando executar métodos do manipulador de eventos. Portanto, a pilha de chamadas pode ter apenas altamente confiável os chamadores quando o método de manipulador de eventos é invocado. Isso faz com que as demandas feitas pelo método de manipulador de eventos seja bem-sucedida. Além disso, a permissão exigida pode ser confirmada quando o método é invocado. Por esses motivos, o risco de não corrigir uma violação dessa regra pode ser avaliado somente depois de examinar o método de manipulação de eventos. Ao examinar seu código, considere as seguintes questões:

-   O seu manipulador de eventos executa todas as operações que são perigosas ou podem ser exploradas como declarar permissões ou suprimir a permissão de código não gerenciado?

-   Quais são as ameaças de segurança para e do seu código, porque ele pode ser executado a qualquer momento com apenas altamente confiáveis que os chamadores na pilha?

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, examine o método e avaliar o seguinte:

-   Você pode tornar o método de manipulação de eventos não público?

-   Você pode mover toda a funcionalidade perigosa fora do manipulador de eventos?

-   Se uma exigência de segurança é imposta, isso pode ser feito de alguma outra maneira?

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Suprima um aviso nessa regra somente após uma análise atenta da segurança para certificar-se de que seu código não representem uma ameaça de segurança.

## <a name="example"></a>Exemplo
 O código a seguir mostra um método de manipulação de eventos que pode ser usado indevidamente por códigos mal-intencionados.

 [!code-csharp[FxCop.Security.EventSecLib#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.EventSecLib/cs/FxCop.Security.EventSecLib.cs#1)]

## <a name="see-also"></a>Consulte também
 <xref:System.Security.CodeAccessPermission.Demand%2A?displayProperty=fullName> <xref:System.EventArgs?displayProperty=fullName>
 [Demandas de segurança](http://msdn.microsoft.com/en-us/324c14f8-54ff-494d-9fd1-bfd20962c8ba)



