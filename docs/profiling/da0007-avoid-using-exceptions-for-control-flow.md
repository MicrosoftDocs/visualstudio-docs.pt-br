---
title: DA0007-Evite usar exceções para o fluxo de controle | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.performance.rules.DAExceptionsThrown
- vs.performance.7
- vs.performance.rules.DA0007
- vs.performance.DA0007
ms.assetid: ee8ba8b5-2313-46c9-b129-3f3a2a232898
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: a33d5b8d18f18fb6bf7a2420603d994d845ce8f2
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85520790"
---
# <a name="da0007-avoid-using-exceptions-for-control-flow"></a>DA0007: Evitar usar exceções no fluxo de controle

|Item|Valor|
|-|-|
|ID de regra|DA0007|
|Categoria|Uso do .NET Framework|
|Métodos de criação de perfil|Todos|
|Mensagem|Um número elevado de exceções está sendo gerado de forma consistente. Considere a redução do uso de exceções na lógica do programa.|
|Tipo de mensagem|Aviso|

 Ao criar o perfil usando a amostragem, a memória do .NET ou métodos de contenção de recursos, é necessário coletar pelo menos 25 amostras para disparar essa regra.

## <a name="cause"></a>Causa
 Uma alta taxa de manipuladores de exceção do .NET Framework foram chamados nos dados de criação de perfil. Considere o uso de outra lógica de fluxo de controle para reduzir o número de exceções geradas.

## <a name="rule-description"></a>Descrição da regra
 Embora o uso de manipuladores de exceção para capturar erros e outros eventos que interrompem a execução do programa seja uma boa prática, o uso do manipulador de exceção como parte da lógica regular de execução do programa pode ser caro e deve ser evitado. Na maioria dos casos, as exceções devem ser usadas somente em circunstâncias que ocorrem com pouca frequência e que não são esperadas. Exceções não devem ser usadas para retornar valores como parte do fluxo típico do programa. Em muitos casos, é possível evitar acionar exceções validando valores e usando a lógica condicional para interromper a execução de instruções que causam o problema.

 Para obter mais informações, consulte a seção [Gerenciamento de exceções](/previous-versions/msp-n-p/ff647790(v=pandp.10)#exception-management) do **capítulo 5 — melhorando o desempenho do código gerenciado** no volume **aprimorando o desempenho e a escalabilidade do aplicativo .net** da biblioteca de **padrões e práticas da Microsoft** no msdn.

## <a name="how-to-investigate-a-warning"></a>Como investigar um aviso
 Clique duas vezes na mensagem da janela Lista de Erros para navegar para a exibição Marcas. Localize a coluna que contém as medidas **.NET CLR Exceptions ( @ProcessInstance ) \\ n º de excels lançados/s** . Determine se há fases específicas da execução do programa em que o tratamento de exceção é mais frequente do que em outras. Usando um perfil de amostragem, tente identificar instruções throw e blocos try/catch que geram exceções frequentes. Se necessário, adicione lógica para capturar blocos para ajudá-lo a entender quais exceções são tratadas com mais frequência. Sempre que possível, substitua instruções throw ou blocos catch frequentemente executados por uma lógica de controle de fluxo simples ou um código de validação.

 Por exemplo, se você descobrir que seu aplicativo está tratando exceções DivideByZeroException frequentes, a adição de lógica ao programa para verificar se há denominadores com valores zero melhorará o desempenho do aplicativo.
