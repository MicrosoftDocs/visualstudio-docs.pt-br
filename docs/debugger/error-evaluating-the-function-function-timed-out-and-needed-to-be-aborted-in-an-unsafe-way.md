---
title: Erro-a avaliação da função &#39;função&#39; atingiu o tempo limite e precisava ser anulada de forma não segura | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
f1_keywords:
- vs.debug.error.unsafe_func_eval_abort
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f687672de4bc3511fa0c9198f7ad4145b26dcd11
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85460792"
---
# <a name="error-evaluating-the-function-39function39-timed-out-and-needed-to-be-aborted-in-an-unsafe-way"></a>Erro: avaliar a função &#39;função&#39; atingiu o tempo limite e precisava ser anulado de forma não segura

Texto completo da mensagem: avaliar a função ' function ' atingiu o tempo limite e precisava ser anulado de forma não segura. Isso pode ter corrompido o processo de destino.

Para facilitar a inspeção do estado dos objetos .NET, o depurador forçará automaticamente o processo depurado a executar código adicional (normalmente, métodos getter de propriedade e funções ToString). Na maioria dos cenários, essas funções são concluídas rapidamente e tornam a depuração muito mais fácil. No entanto, o depurador não executa o aplicativo em uma área restrita. Como resultado, um método getter ou ToString de propriedade que chama uma função nativa que trava pode levar a tempos limite longos que podem não ser recuperáveis. Se você encontrar essa mensagem de erro, isso ocorreu.

Um motivo comum para esse problema é que quando o depurador avalia uma propriedade, ele só permite que o thread seja inspecionado para execução. Portanto, se a propriedade estiver aguardando que outros threads sejam executados dentro do aplicativo depurado e, se estiver esperando de uma maneira que o tempo de execução do .NET não possa ser interrompido, esse problema ocorrerá.

## <a name="to-correct-this-error"></a>Para corrigir este erro

Há várias soluções possíveis para esse problema.

### <a name="solution-1-prevent-the-debugger-from-calling-the-getter-property-or-tostring-method"></a>#1 da solução: impedir que o depurador chame a propriedade getter ou o método ToString

A mensagem de erro informará o nome da função que o depurador tentou chamar. Se você puder modificar essa função, poderá impedir que o depurador chame o método getter ou ToString de propriedade. Tente uma das seguintes opções:

* Altere o método para algum outro tipo de código além de um método getter ou ToString de propriedade e o problema irá desaparecer.
    -ou-
* (Para ToString) Defina um atributo DebuggerDisplay no tipo e você pode fazer com que o depurador avalie algo diferente de ToString.
    -ou-
* (Para um getter de propriedade) Coloque o `[System.Diagnostics.DebuggerBrowsable(DebuggerBrowsableState.Never)]` atributo na propriedade. Isso pode ser útil se você tiver um método que precisa permanecer como uma propriedade para motivos de compatibilidade de API, mas deve ser realmente um método.

### <a name="solution-2-have-the-target-code-ask-the-debugger-to-abort-the-evaluation"></a>#2 da solução: faça com que o código de destino peça ao depurador para anular a avaliação

A mensagem de erro informará o nome da função que o depurador tentou chamar. Se o método getter ou ToString de propriedade às vezes não for executado corretamente, especialmente em situações em que o problema é que o código precisa de outro thread para executar o código, a função de implementação pode chamar `System.Diagnostics.Debugger.NotifyOfCrossThreadDependency` para solicitar que o depurador anule a avaliação da função. Com essa solução, ainda é possível avaliar explicitamente essas funções, mas o comportamento padrão é que a execução é interrompida quando a chamada NotifyOfCrossThreadDependency ocorre.

### <a name="solution-3-disable-all-implicit-evaluation"></a>#3 da solução: desabilitar toda a avaliação implícita

Se as soluções anteriores não corrigirem o problema, vá para **ferramentas**  >  **Opções**e desmarque a opção **depuração**  >  **geral**  >  **habilitar avaliação de propriedade e outras chamadas de função implícitas**. Isso desabilitará a maioria das avaliações de função implícitas e deverá resolver o problema.

### <a name="solution-4-enable-managed-compatibility-mode"></a>#4 de solução: habilitar o modo de compatibilidade gerenciado

Se você alternar para o mecanismo de depuração herdado, talvez seja possível eliminar esse erro. Vá para **ferramentas**  >  **Opções**e selecione a definição configuração **Debugging**  >  **geral**  >  **usar modo de compatibilidade gerenciada**. Para obter mais informações, consulte [Opções gerais de depuração](../debugger/general-debugging-options-dialog-box.md).
