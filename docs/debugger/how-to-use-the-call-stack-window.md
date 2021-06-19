---
title: Exibir a pilha de chamada no depurador | Microsoft Docs
description: Use a janela Pilha de Chamadas para exibir as chamadas de função ou procedimento que estão atualmente na pilha em Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 10/29/2018
ms.topic: how-to
f1_keywords:
- vs.debug.callstack
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
- SQL
- aspx
helpviewer_keywords:
- threading [Visual Studio], displaying calls to or from
- functions [debugger], viewing code on call stack
- disassembly code
- breakpoints, Call Stack window
- debugging [Visual Studio], switching to another stack frame
- debugging [Visual Studio], Call Stack window
- Call Stack window, viewing source code for functions on the call stack
- stack, switching stack frames
- Call Stack window, viewing disassembly code for functions on the call stack
ms.assetid: 5154a2a1-4729-4dbb-b675-db611a72a731
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 5e905a509443cd5fd30e860a887dd895c5ee21a6
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112387470"
---
# <a name="view-the-call-stack-and-use-the-call-stack-window-in-the-debugger"></a>Exibir a pilha de chamada e usar a janela Pilha de Chamada no depurador

Ao usar a janela **Pilha de Chamadas**, você pode exibir chamadas de função ou procedimento que estão na pilha atualmente. A janela **Pilha de Chamadas** mostra a ordem em que os métodos e as funções são chamados. A pilha de chamadas é uma boa maneira de examinar e entender o fluxo de execução de um aplicativo.

Quando [os símbolos](#bkmk_symbols) de depuração não estão disponíveis  para parte de uma pilha de chamada, a janela Pilha de Chamada pode não ser capaz de exibir informações corretas para essa parte da pilha de chamada, exibindo em vez disso:

`[Frames below may be incorrect and/or missing, no symbols loaded for name.dll]`

> [!NOTE]
> A janela **Pilha de Chamadas** é semelhante à perspectiva de Depuração em alguns IDEs, como o Eclipse.

> [!NOTE]
> As caixas de diálogo e os comandos de menu vistos podem ser diferentes daqueles descritos aqui, dependendo da edição ou das configurações ativas. Para alterar as configurações, selecione **Importar e Exportar Configurações** no menu **Ferramentas**.  Consulte [Redefinir configurações](../ide/environment-settings.md#reset-settings).

## <a name="view-the-call-stack-while-in-the-debugger"></a>Exibir a pilha de chamada enquanto estiver no depurador

- Durante a depuração, no menu **Depurar,** selecione **Windows > Pilha de Chamada**.

  ![Janela Pilha de Chamadas](../debugger/media/dbg_basics_callstack_window.png "CallStackWindow")

Uma seta amarela identifica o quadro de pilha onde o ponteiro de execução está localizado atualmente. Por padrão, as informações desse quadro de pilha aparecem nas **janelas** de origem, Locais, **Autos,** **Observar** e **Desmontagem.** Para alterar o contexto do depurador para outro quadro na pilha, [alternar para outro quadro de pilha.](#bkmk_switch)

## <a name="display-non-user-code-in-the-call-stack-window"></a>Exibir código não usuário na janela Pilha de Chamada

- Clique com o botão direito do mouse na janela **Pilha de Chamadas** e selecione **Mostrar Código Externo**.

Código não usuário é qualquer código que não é mostrado [quando](../debugger/just-my-code.md) Apenas Meu Código está habilitado. No código gerenciado, os quadros de código que não são do usuário ficam ocultos por padrão. A seguinte notação aparece no lugar dos quadros de código que não são do usuário:

`[<External Code>]`

## <a name="switch-to-another-stack-frame-change-the-debugger-context"></a><a name="bkmk_switch"></a> Alternar para outro quadro de pilha (alterar o contexto do depurador)

1. Na janela **Pilha de Chamada,** clique com o botão direito do mouse no quadro de pilha cujos códigos e dados você deseja exibir.

    Ou você pode clicar duas vezes em um quadro na janela **Pilha de** Chamada para alternar para esse quadro.

2. Selecione **Alternar para Quadro**.

     Uma seta verde com uma cauda curva é exibida ao lado do quadro de pilha selecionado. O ponteiro de execução permanece no quadro original, que ainda está marcado com a seta amarela. Se você selecionar **Etapa** ou **Continuar** no menu **Depurar**, a execução continuará no quadro original, não no quadro selecionado.

## <a name="view-the-source-code-for-a-function-on-the-call-stack"></a>Exibir o código-fonte de uma função na pilha de chamada

- Na janela **Pilha de Chamadas**, clique com o botão direito do mouse na função cujo código-fonte você deseja ver e selecione **Ir para Código-Fonte**.

## <a name="run-to-a-specific-function-from-the-call-stack-window"></a>Executar para uma função específica na janela Pilha de Chamada

- Na janela **Pilha de Chamada,** selecione a função , clique com o botão direito do mouse e, em seguida, **escolha Executar para o Cursor**.

## <a name="set-a-breakpoint-on-the-exit-point-of-a-function-call"></a>Definir um ponto de interrupção no ponto de saída de uma chamada de função

- Consulte [Definir um ponto de interrupção em uma função de pilha de chamada](../debugger/using-breakpoints.md#BKMK_Set_a_breakpoint_from_debugger_windows).

## <a name="display-calls-to-or-from-another-thread"></a>Exibir chamadas para ou de outro thread

- Clique com o botão direito do mouse na janela **Pilha de Chamadas** e selecione **Incluir chamadas para/de outros threads**.

## <a name="visually-trace-the-call-stack"></a>Rastrear visualmente a pilha de chamada

No Visual Studio Enterprise (somente), você pode exibir mapas de código para a pilha de chamada durante a depuração.

- Na janela **Pilha de Chamadas**, abra o menu de atalho. Escolha **Mostrar Pilha de Chamada no Mapa de Código** (**Ctrl**  +  **Shift**  +  **`** ).

    Para obter mais informações, consulte [Mapear métodos na pilha de chamada durante a depuração](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md).

![Mostrar pilha de chamada no mapa de código](../debugger/media/dbg_basics_show_call_stack_on_code_map.gif "ShowCallStackOnCodeMap")

## <a name="view-the-disassembly-code-for-a-function-on-the-call-stack-c-c-visual-basic-f"></a>Exibir o código de desmontagem de uma função na pilha de chamada (C#, C++, Visual Basic, F#)

- Na janela **Pilha de Chamadas**, clique com o botão direito do mouse na função cujo código de desmontagem você deseja ver e selecione **Ir para Desmontagem**.

## <a name="change-the-optional-information-displayed"></a>Alterar as informações opcionais exibidas

- Clique com o botão direito do mouse **na janela Pilha de** Chamada e depure ou desempure **Mostrar \<**_the information that you want_**>**.

## <a name="load-symbols-for-a-module-c-c-visual-basic-f"></a><a name="bkmk_symbols"></a> Carregar símbolos para um módulo (C#, C++, Visual Basic, F#)

Na janela **Pilha de Chamadas**, você pode carregar símbolos de depuração para o código que atualmente não tem símbolos carregados. Esses símbolos podem ser símbolos do .NET ou do sistema baixados dos servidores de símbolos públicos da Microsoft ou símbolos em um caminho de símbolo no computador que você está depurando.

Consulte [Especificar arquivos de símbolo (.pdb) e de origem.](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)

### <a name="to-load-symbols"></a>Para carregar símbolos

1. Na janela **Pilha de Chamada,** clique com o botão direito do mouse no quadro de pilha para o qual os símbolos não são carregados. O quadro ficará esmaecido.

2. Aponte para **Carregar Símbolos** e selecione **Servidores de Símbolos da Microsoft** (se disponível) ou navegue até o caminho do símbolo.

### <a name="to-set-the-symbol-path"></a>Para definir o caminho do símbolo

1. Na janela **Pilha de Chamadas**, escolha **Configurações de Símbolo** no menu de atalho.

     A caixa de diálogo **Opções** abre e a página **Símbolos** é exibida.

2. Selecione **Configurações de Símbolo**.

3. Na caixa de diálogo **Opções**, clique no ícone da Pasta.

     Na caixa **Locais do arquivo de símbolo (.pdb)**, um cursor será exibido.

4. Insira um nome de caminho de diretório para o local do símbolo no computador que você está depurando. Para depuração local e remota, esse é um caminho no computador local.

5. Selecione **OK** para fechar a **caixa de diálogo** Opções.

## <a name="see-also"></a>Confira também

- [Código misto e informações ausentes na janela pilha de chamadas](../debugger/mixed-code-and-missing-information-in-the-call-stack-window.md)
- [Exibindo dados no depurador](../debugger/viewing-data-in-the-debugger.md)
- [Especificar arquivos de símbolo (.pdb) e de origem](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)
- [Usar pontos de interrupção](../debugger/using-breakpoints.md)