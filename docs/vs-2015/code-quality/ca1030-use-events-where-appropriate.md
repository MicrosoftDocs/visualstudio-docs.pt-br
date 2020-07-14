---
title: 'CA1030: usar eventos quando apropriado | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- UseEventsWhereAppropriate
- CA1030
helpviewer_keywords:
- CA1030
- UseEventsWhereAppropriate
ms.assetid: ea051367-deeb-40f9-9b65-eb818f1e133a
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 1313c5ee79a7a13d3eb937a3431b13ea393857d1
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544515"
---
# <a name="ca1030-use-events-where-appropriate"></a>CA1030: Usar eventos quando apropriado
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|UseEventsWhereAppropriate|
|CheckId|CA1030|
|Categoria|Microsoft. Design|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um nome de método público, protegido ou privado começa com um dos seguintes:

- Complemento

- RemoveOn

- Fire

- Gera

## <a name="rule-description"></a>Descrição da Regra
 Essa regra detecta métodos que têm nomes que seriam usados normalmente em eventos. Eventos seguem o observador ou o padrão de design de publicação/assinatura; Eles são usados quando uma alteração de estado em um objeto deve ser comunicada a outros objetos. Se um método é chamado em resposta a uma alteração de estado claramente definida, o método deve ser invocado por um manipulador de eventos. Os objetos que chamam o método devem acionar eventos, em vez de chamar o método diretamente.

 Alguns exemplos comuns de eventos são encontrados em aplicativos de interface do usuário em que uma ação do usuário, como clicar em um botão, faz com que um segmento de código seja executado. O [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] modelo de evento não está limitado às interfaces do usuário; ele deve ser usado em qualquer lugar que você deva comunicar alterações de estado em um ou mais objetos.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Se o método for chamado quando o estado de um objeto for alterado, considere alterar o design para usar o [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] modelo de evento.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Suprimir um aviso dessa regra se o método não funcionar com o [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] modelo de evento.
