---
title: Erro-o processo de destino saiu com código &#39;código&#39; ao avaliar a função &#39;função&#39; | Microsoft Docs
ms.date: 4/06/2018
ms.topic: error-reference
f1_keywords:
- vs.debug.error.process_exit_during_func_eval
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d1721196becf1f746d81fa7e3d4ff5f0371e3f57
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85460772"
---
# <a name="error-the-target-process-exited-with-code-39code39-while-evaluating-the-function-39function39"></a>Erro: o processo de destino saiu com o código &#39;código&#39; ao avaliar a função &#39;function&#39;

Texto completo da mensagem: o processo de destino saiu com o código ' code ' ao avaliar a função ' function '.

Para facilitar a inspeção do estado dos objetos .NET, o depurador forçará automaticamente o processo depurado a executar código adicional (normalmente, métodos e funções getter da propriedade `ToString` ). Na maioria dos cenários, essas funções são concluídas com êxito ou geram exceções que podem ser detectadas pelo depurador. No entanto, há algumas circunstâncias em que as exceções não podem ser detectadas porque elas cruzam limites de kernel, exigem bombeamento de mensagens do usuário ou são irrecuperáveis. Como resultado, um método getter ou ToString de propriedade que executa o código que encerra explicitamente o processo (por exemplo, chamadas `ExitProcess()` ) ou gera uma exceção sem tratamento que não pode ser detectada (por exemplo, `StackOverflowException` ) encerrará o processo depurado e encerrará a sessão de depuração. Se você encontrar essa mensagem de erro, isso ocorreu.

Um motivo comum para esse problema é que quando o depurador avalia uma propriedade que chama a si mesmo, isso pode resultar em uma exceção de estouro de pilha. A exceção de estouro de pilha não pode ser recuperada e o processo de destino será encerrado.

## <a name="to-correct-this-error"></a>Para corrigir este erro

Há duas soluções possíveis para esse problema.

### <a name="solution-1-prevent-the-debugger-from-calling-the-getter-property-or-tostring-method"></a>#1 da solução: impedir que o depurador chame a propriedade getter ou o método ToString 

A mensagem de erro informará o nome da função que o depurador tentou chamar. Com o nome da função, você pode tentar avaliar novamente essa função na janela **imediata** para depurar a avaliação. A depuração é possível ao avaliar a partir da janela **imediata** porque, ao contrário das avaliações implícitas das janelas **auto-/-local/Watch** , o depurador interrompe as exceções sem tratamento.

Se você puder modificar essa função, poderá impedir que o depurador chame o método ou getter da propriedade `ToString` . Tente uma das seguintes opções:

* Altere o método para algum outro tipo de código além de um método getter ou ToString de propriedade e o problema irá desaparecer.
    -ou-
* (Para `ToString` ) Defina um `DebuggerDisplay` atributo no tipo e você pode fazer com que o depurador avalie algo diferente de `ToString` .
    -ou-
* (Para um getter de propriedade) Coloque o `[System.Diagnostics.DebuggerBrowsable(DebuggerBrowsableState.Never)]` atributo na propriedade. Isso pode ser útil se você tiver um método que precisa permanecer como uma propriedade para motivos de compatibilidade com a API, mas deve realmente ser um método.

Se você não puder modificar esse método, poderá interromper o processo de destino em uma instrução alternativa e tentar novamente a avaliação.

### <a name="solution-2-disable-all-implicit-evaluation"></a>#2 da solução: desabilitar toda a avaliação implícita

Se as soluções anteriores não corrigirem o problema, vá para **ferramentas**  >  **Opções**e desmarque a opção **depuração**  >  **geral**  >  **habilitar avaliação de propriedade e outras chamadas de função implícitas**. Isso desabilitará a maioria das avaliações de função implícitas e deverá resolver o problema.
