---
title: Voltar para a função que chamou MFC em caso de interrupção | Microsoft Docs
ms.custom: seodec18
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
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
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: c746fc287435ea6219e0f6052bc9372fc2ae5d25
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53048562"
---
# <a name="how-to-get-back-to-the-function-that-called-mfc-if-halted"></a>Como: Retornar à função que chamou o MFC em caso de interrupção

> [!NOTE]
> As caixas de diálogo e os comandos de menu que você vê podem ser diferentes dos descritos na Ajuda, dependendo da sua edição ou das configurações ativas. Para alterar as configurações, escolha **Importar e Exportar Configurações** no menu **Ferramentas**. Para obter mais informações, confira [Redefinir as configurações](../ide/environment-settings.md#reset-settings).

Se você usou o comando **Interromper** no menu **Depurar** para interromper o programa e terminou no MFC e se você tiver certeza de que o problema está no código, use a janela Pilha de Chamadas para retornar à função. Confira mais informações em [Como: Usar a janela Pilha de Chamadas](../debugger/how-to-use-the-call-stack-window.md).

Às vezes seu código pode ser interrompido na bomba da mensagem. Nesse caso, não há nenhum código de usuário na pilha de chamadas. Para evitar esse problema, use pontos de interrupção (possivelmente com condições e contagens de ocorrências) em vez do comando **Interromper**. Para obter mais informações, consulte [pontos de interrupção e Tracepoints](https://msdn.microsoft.com/library/fe4eedc1-71aa-4928-962f-0912c334d583).

## <a name="navigate-to-the-function-from-which-mfc-was-called"></a>Navegue até a função da qual o MFC foi chamado

-   Use a janela **Pilha de Chamadas**.

## <a name="see-also"></a>Consulte também

- [Perguntas frequentes de depuração de código nativo](../debugger/debugging-native-code-faqs.md)
- [Depurando código nativo](../debugger/debugging-native-code.md)