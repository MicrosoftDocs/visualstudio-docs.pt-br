---
title: Voltar à função que chamou o MFC, se for interrompido | Microsoft Docs
description: Entenda como retornar à função que chamou o MFC se a execução for interrompida no depurador do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.debug.mfc
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- functions [C++], debugging
- function calls, returning to calling function
- debugging [MFC], returning to calling function
- debugging [MFC], functions
- Break command
- programs, halting
- functions [debugger]
ms.assetid: d254a5a9-afbd-4923-9d7a-7422d824cabf
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 31bbb064aad5a43738b2f345cf31a20767c55e69
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112384675"
---
# <a name="how-to-get-back-to-the-function-that-called-mfc-if-halted"></a>Como retornar à função que chamou MFC em caso de parada

> [!NOTE]
> As caixas de diálogo e os comandos de menu encontrados podem diferir daqueles descritos na Ajuda, dependendo das configurações ativas ou edição. Para alterar suas configurações, selecione **Importar e Exportar Configurações** no menu **Ferramentas** . Para obter mais informações, confira [Redefinir as configurações](../ide/environment-settings.md#reset-settings).

Se você usou o comando **Interromper** no menu **Depurar** para interromper o programa e terminou no MFC e se você tiver certeza de que o problema está no código, use a janela Pilha de Chamadas para retornar à função. Para obter mais informações, consulte [como: usar a janela pilha de chamadas](../debugger/how-to-use-the-call-stack-window.md).

Às vezes seu código pode ser interrompido na bomba da mensagem. Nesse caso, não há nenhum código de usuário na pilha de chamadas. Para evitar esse problema, use pontos de interrupção (possivelmente com condições e contagens de ocorrências) em vez do comando **Interromper**. Para obter mais informações, consulte [pontos de interrupção e tracepoints](/previous-versions/ktf38f66(v=vs.100)).

## <a name="navigate-to-the-function-from-which-mfc-was-called"></a>Navegue até a função da qual o MFC foi chamado

- Use a janela **pilha de chamadas** .

## <a name="see-also"></a>Confira também

- [Perguntas frequentes sobre depuração de código nativo](../debugger/debugging-native-code-faqs.md)
- [Depurando código nativo](../debugger/debugging-native-code.md)