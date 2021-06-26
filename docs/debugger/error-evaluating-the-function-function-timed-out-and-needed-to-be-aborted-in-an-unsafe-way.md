---
title: Avaliar a função &apos; de função &apos; tempou e precisava ser anulada de maneira não segura | Microsoft Docs
description: "Texto completo da mensagem: a avaliação da função 'função' tempou e precisava ser anulada de maneira não segura."
ms.date: 06/18/2021
ms.topic: error-reference
ms.custom: contperf-fy21q4
f1_keywords:
- vs.debug.error.unsafe_func_eval_abort
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 94c308e9ec960f744a98f0f930999df36afff475
ms.sourcegitcommit: d3658667e768d7516cbf4461ec47bf24c8fcb7e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112925001"
---
# <a name="error-evaluating-the-function-39function39-timed-out-and-needed-to-be-aborted-in-an-unsafe-way"></a>Erro: avaliar a função &#39;função&#39; o tempo foi e precisava ser anulada de maneira não segura

Texto completo da mensagem: a avaliação da função 'função' tempou e precisava ser anulada de maneira não segura. Isso pode ter corrompido o processo de destino.

Para facilitar a inspeção do estado dos objetos .NET, o depurador força automaticamente o processo depurado a executar código adicional (normalmente métodos getter de propriedade e funções ToString). Na maioria dos cenários, essas funções são concluídas rapidamente e facilitam muito a depuração. No entanto, o depurador não executará o aplicativo em uma área sandbox. Como resultado, um método getter de propriedade ou ToString que chama em uma função nativa que para de responder pode levar a longos tempos que podem não ser recuperáveis. Se você encontrar essa mensagem de erro, isso ocorreu.

Um motivo comum para esse problema é que, quando o depurador avalia uma propriedade, ele só permite que o thread que está sendo inspecionado seja executado. Portanto, se a propriedade estiver aguardando outros threads para execução dentro do aplicativo depurado e se ela estiver aguardando de uma maneira que o Runtime do .NET não seja capaz de interromper, esse problema ocorrerá.

## <a name="to-correct-this-error"></a>Para corrigir este erro

Confira as seções a seguir para ver várias soluções possíveis para esse problema.

## <a name="solution-1-prevent-the-debugger-from-calling-the-getter-property-or-tostring-method"></a>Solução #1: impedir que o depurador chama a propriedade getter ou o método ToString

A mensagem de erro dirá o nome da função que o depurador tentou chamar. Se você puder modificar essa função, poderá impedir que o depurador chamar o método getter ou ToString da propriedade. Tente um dos seguintes:

* Altere o método para algum outro tipo de código além de um getter de propriedade ou método ToString e o problema desaparecerá.
  – ou –
* (Para ToString) Defina [um atributo DebuggerDisplay](../debugger/using-the-debuggerdisplay-attribute.md) no tipo e você poderá fazer com que o depurador avalie algo diferente de ToString.
  – ou –
* (Para um getter de propriedade) Coloque o [atributo System.Diagnostics.DebuggerBrowsable(DebuggerBrowsableState.Never)](/dotnet/api/system.diagnostics.debuggerbrowsableattribute) na propriedade . Isso pode ser útil se você tiver um método que precisa permanecer uma propriedade por motivos de compatibilidade de API, mas ele realmente deve ser um método.

## <a name="solution-2-have-the-target-code-ask-the-debugger-to-abort-the-evaluation"></a>Solução #2: peça ao código de destino que peça ao depurador para anular a avaliação

A mensagem de erro dirá o nome da função que o depurador tentou chamar. Se o método getter ou ToString da propriedade às vezes não for executado corretamente, especialmente em situações em que o problema é que o código precisa de outro thread para executar código, a função de implementação pode chamar [System.Diagnostics.Debugger.NotifyOfCrossThreadDependency](/dotnet/api/system.diagnostics.debugger.notifyofcrossthreaddependency) para pedir ao depurador para anular a avaliação da função. Com essa solução, ainda é possível avaliar explicitamente essas funções, mas o comportamento padrão é que a execução é interrompida quando a chamada NotifyOfCrossThreadDependency ocorre.

## <a name="solution-3-disable-all-implicit-evaluation"></a>Solução #3: desabilitar toda a avaliação implícita

Se as soluções anteriores não corrigirem o problema, acesse Opções de Ferramentas e desmarque a configuração  >   **Depuração** Geral Habilitar avaliação de propriedade e outras chamadas  >    >  **de função implícitas**. Isso desabilitará a maioria das avaliações de função implícita e deverá resolver o problema.

## <a name="solution-4-check-compatibility-with-third-party-developer-tools"></a>Solução #4: verificar a compatibilidade com ferramentas de desenvolvedor de terceiros

Se você estiver usando o Resharper, consulte este [problema para](https://youtrack.jetbrains.com/issue/RSRP-476824) sugestões.

## <a name="solution-5-enable-managed-compatibility-mode"></a>Solução #5: habilitar o modo de compatibilidade gerenciada

Se você alternar para o mecanismo de depuração herdado, poderá eliminar esse erro. Vá para **Opções**  >  **de Ferramentas** e selecione a configuração **Depuração**  >  **Geral**  >  **Use o modo de compatibilidade gerenciada**. Para obter mais informações, consulte [Opções gerais de depuração](../debugger/general-debugging-options-dialog-box.md).
