---
title: 'Erro: O processo de destino foi encerrado com o código de &#39;código&#39; ao avaliar a função &#39;função&#39; | Microsoft Docs'
ms.custom: ''
ms.date: 4/06/2018
ms.topic: troubleshooting
f1_keywords:
- vs.debug.error.process_exit_during_func_eval
ms.technology: vs-ide-debug
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 98923757912d1f4619cc79c8f946aabaa531ac05
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49936258"
---
# <a name="error-the-target-process-exited-with-code-39code39-while-evaluating-the-function-39function39"></a>Erro: O processo de destino foi encerrado com o código de &#39;código&#39; ao avaliar a função &#39;função&#39;

Mensagem de texto completo: O processo de destino foi encerrado com o código 'code' durante a avaliação da função 'function'.

Para tornar mais fácil de inspecionar o estado de objetos .NET, o depurador automaticamente forçará o processo depurado para executar código adicional (normalmente os métodos de getter de propriedade e `ToString` funções). Na maioria dos cenários, essas funções concluída com êxito ou lancem exceções que podem ser capturadas pelo depurador. No entanto, há algumas circunstâncias em que as exceções não podem ser detectadas porque cruzar os limites do kernel, exigem o bombeamento de mensagens do usuário ou são irrecuperáveis. Como resultado, um getter de propriedade ou método ToString que executa o código que encerra o processo explicitamente (por exemplo, chamadas `ExitProcess()`) ou gera uma exceção sem tratamento que não pode ser detectada (por exemplo, `StackOverflowException`) encerrará o processo depurado e encerre a sessão de depuração. Se você encontrar esta mensagem de erro, isso ocorreu.
 
Uma razão comum para esse problema é que, quando o depurador avalia uma propriedade que chama a mesmo, isso pode resultar em uma exceção de estouro de pilha. A exceção de estouro de pilha não pode ser recuperada e o processo de destino será encerrado.
 
## <a name="to-correct-this-error"></a>Para corrigir este erro
 
Há duas soluções possíveis para esse problema.
 
### <a name="solution-1-prevent-the-debugger-from-calling-the-getter-property-or-tostring-method"></a>Solução #1: Impedir que o depurador chamar a propriedade getter ou o método ToString 

A mensagem de erro informará o nome da função que o depurador tentou chamar. Com o nome da função, você pode tentar reavaliar essa função do **imediato** janela Depurar a avaliação. É possível depurar ao avaliar a partir de **imediato** janela porque, diferentemente de avaliações implícitas do **Autos/locais/inspeção** windows, o depurador é interrompido em exceções sem tratamento.

Se você pode modificar essa função, você pode impedir que o depurador de chamar o getter de propriedade ou `ToString` método. Tente um destes procedimentos:
 
* Alterar o método para algum outro tipo de código, além de um getter de propriedade ou método ToString e o problema desaparecerá.
    -ou-
* (Para `ToString`) definir um `DebuggerDisplay` atributo no tipo e você pode ter o depurador avaliar algo diferente de `ToString`.
    -ou-
* (Para um getter de propriedade) Coloque o `[System.Diagnostics.DebuggerBrowsable(DebuggerBrowsableState.Never)]` atributo na propriedade. Isso pode ser útil se você tiver um método que deve permanecer a uma propriedade por razões de compatibilidade de API, mas na verdade, ele deve ser um método.

Se você não pode modificar esse método, você poderá interromper o processo de destino em uma instrução de alternativa e tente novamente a avaliação.
 
### <a name="solution-2-disable-all-implicit-evaluation"></a>Solução #2: Desabilitar todas as avaliação implícita
 
Se as soluções anteriores não resolverem o problema, vá para **ferramentas** > **opções**e desmarque a configuração **depuração**  >   **Gerais** > **habilitar avaliação de propriedade e outras chamadas de função implícitas**. Isso desabilitará a maioria das avaliações de função implícitas e deve resolver o problema.



  
