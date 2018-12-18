---
title: 'Erro: A avaliação da função &#39;função&#39; atingiu o tempo limite e precisou ser interrompida de forma não segura | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.topic: troubleshooting
f1_keywords:
- vs.debug.error.unsafe_func_eval_abort
ms.technology: vs-ide-debug
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 1f36e56b2870d5f099a3b8ed95265fe7e2d688ff
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49934438"
---
# <a name="error-evaluating-the-function-39function39-timed-out-and-needed-to-be-aborted-in-an-unsafe-way"></a>Erro: A avaliação da função &#39;função&#39; atingiu o tempo limite e precisou ser interrompida de forma não segura

Mensagem de texto completo: avaliar a função 'função' atingiu o tempo limite e precisou ser interrompida de forma não segura. Isso pode ter corrompido o processo de destino. 

Para tornar mais fácil de inspecionar o estado de objetos .NET, o depurador automaticamente forçará o processo depurado para executar código adicional (normalmente os métodos de getter de propriedade e funções de ToString). Na maioria dos cenários de todos os, essas funções concluída rapidamente e facilitar a depuração muito. No entanto, o depurador não executa o aplicativo em uma área restrita. Como resultado, um getter de propriedade ou método ToString que chama uma função nativa que trava pode levar a tempos limite longo que talvez não sejam recuperável. Se você encontrar esta mensagem de erro, isso ocorreu.
 
Uma razão comum para esse problema é que quando o depurador avalia uma propriedade, ele só permite que o thread que está sendo inspecionado para executar. Portanto, se a propriedade estiver aguardando outros threads sejam executados dentro do aplicativo depurado e está aguardando de forma que o tempo de execução do .NET não é capaz de interrupção, esse problema ocorrerá.
 
## <a name="to-correct-this-error"></a>Para corrigir este erro
 
Há três soluções possíveis para esse problema.
 
### <a name="solution-1-prevent-the-debugger-from-calling-the-getter-property-or-tostring-method"></a>Solução #1: Impedir que o depurador chamar a propriedade getter ou o método ToString
 
A mensagem de erro informará o nome da função que o depurador tentou chamar. Se você pode modificar essa função, você pode impedir que o depurador chamar o getter de propriedade ou método ToString. Tente um destes procedimentos:
 
* Alterar o método para algum outro tipo de código, além de um getter de propriedade ou método ToString e o problema desaparecerá.
    -ou-
* (Para ToString) Definir um atributo DebuggerDisplay no tipo e você pode fazer com que o depurador avaliar algo diferente de ToString.
    -ou-
* (Para um getter de propriedade) Coloque o `[System.Diagnostics.DebuggerBrowsable(DebuggerBrowsableState.Never)]` atributo na propriedade. Isso pode ser útil se você tiver um método que deve manter uma propriedade por razões de compatibilidade de API, mas na verdade, ele deve ser um método.
 
### <a name="solution-2-have-the-target-code-ask-the-debugger-to-abort-the-evaluation"></a>Solução #2: Tem o código de destino pergunte o depurador para anular a avaliação
 
A mensagem de erro informará o nome da função que o depurador tentou chamar. Se o getter de propriedade ou método ToString, às vezes, não seja executada corretamente, especialmente em situações em que o problema é que o código precisa outro thread para executar o código e a função de implementação pode chamar `System.Diagnostics.Debugger.NotifyOfCrossThreadDependency` pedir o depurador para a função abort avaliação. Com essa solução, ainda é possível avaliar a essas funções explicitamente, mas o comportamento padrão é que a execução é interrompida quando ocorre a chamada NotifyOfCrossThreadDependency.
 
### <a name="solution-3-disable-all-implicit-evaluation"></a>Solução #3: Desabilitar todas as avaliação implícita
 
Se as soluções anteriores não resolverem o problema, vá para *ferramentas* > *opções*e desmarque a configuração *depuração*  >   *Gerais* > *habilitar avaliação de propriedade e outras chamadas de função implícitas*. Isso desabilitará a maioria das avaliações de função implícitas e deve resolver o problema.



  
