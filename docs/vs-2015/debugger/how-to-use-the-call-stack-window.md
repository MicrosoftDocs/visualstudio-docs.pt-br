---
title: 'Como: usar a janela de pilha de chamadas | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.debug.callstack
dev_langs:
- FSharp
- VB
- CSharp
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
caps.latest.revision: 45
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c45f0a645945e68b7b3d21eefe2f981b9b4b352f
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51751021"
---
# <a name="how-to-use-the-call-stack-window"></a>Como usar a janela Pilha de Chamadas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Usando o **pilha de chamadas** janela, você pode exibir as chamadas de função ou procedimento que estão atualmente na pilha.  
  
 O **pilha de chamadas** janela exibe o nome de cada função e que ele está escrito na linguagem de programação. O nome da função ou do procedimento pode ser acompanhado de informações opcionais, como o nome do módulo, o número da linha e os nomes de parâmetro, tipos e valores. A exibição dessas informações opcionais pode ser ativada ou desativada.  
  
 Uma seta amarela identifica o quadro de pilha onde o ponteiro de execução está localizado atualmente. Por padrão, isso é o quadro cujas informações aparecem na origem, **desmontagem**, **Locals**, **Assista**, e **Autos** windows. Se você quiser alterar o contexto para outro quadro na pilha, você pode fazer isso **pilha de chamadas** janela.  
  
 Quando os símbolos de depuração não estão disponíveis para a parte de uma pilha de chamadas, o **pilha de chamadas** janela pode não ser capaz de exibir as informações corretas para essa parte da pilha de chamadas. A notação a seguir aparece:  
  
 [Os quadros abaixo podem estar incorretos e/ou ausentes, nenhum símbolo carregado para name.dll]  
  
 No código gerenciado, por padrão. o **pilha de chamadas** janela oculta informações do código de não usuário. Aparecerá as notações a seguir em vez das informações ocultas:  
  
 **[\<Código externo >]**  
  
 Um código que não seja do usuário é qualquer código que não seja "Meu Código". Você pode optar por exibir informações da pilha de chamadas para o código que não é do usuário usando o menu de atalho.  
  
 Ao usar o menu de atalho, você pode escolher se exibe chamadas entre threads.  
  
> [!NOTE]
>  As caixas de diálogo e os comandos do menu que você vê podem ser diferentes dos descritos na Ajuda, dependendo da edição ou das configurações ativas. Para alterar suas configurações, selecione **Import and Export Settings** sobre o **ferramentas** menu. Para obter mais informações, consulte [Personalizando configurações de desenvolvimento no Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### <a name="to-display-the-call-stack-window-in-break-mode-or-in-run-mode"></a>Para exibir a janela Pilha de chamadas no modo de interrupção ou no modo de execução  
  
-   Sobre o **Debug** menu, selecione **Windows** e, em seguida, clique em **pilha de chamadas**.  
  
### <a name="to-change-the-optional-information-displayed"></a>Para alterar as informações opcionais exibidas  
  
-   Clique com botão direito do **pilha de chamadas** janela e defina ou desmarque **mostram \<**  _as informações que você deseja_ **>**.  
  
### <a name="to-display-non-user-code-frames-in-the-call-stack-window"></a>Para exibir quadros de código de não usuário na janela Pilha de chamadas  
  
-   Clique com botão direito do **pilha de chamadas** janela e selecione **Mostrar código externo**.  
  
### <a name="to-switch-to-another-stack-frame"></a>Para alternar para outro registro de ativação  
  
1.  No **pilha de chamadas** janela, clique com botão direito do quadro cujos código e os dados que você deseja exibir.  
  
2.  Selecione **alternar para quadro**.  
  
     Uma seta verde com uma parte final encaracolada aparece ao lado do quadro que você selecionou. O ponteiro de execução permanece no quadro original, que ainda está marcado com a seta amarela. Se você selecionar **etapa** ou **continuar** do **depurar** menu, a execução continuará no quadro original, não no quadro selecionado.  
  
### <a name="to-display-calls-to-or-from-another-thread"></a>Para exibir chamadas para ou de outro segmento  
  
-   Clique com botão direito do **pilha de chamadas** janela e selecione **incluem chamadas para / de outros Threads**.  
  
### <a name="to-view-the-source-code-for-a-function-on-the-call-stack"></a>Para exibir o código-fonte em uma função na pilha de chamadas  
  
-   No **pilha de chamadas** janela, o botão direito do mouse na função cujo código-fonte código que você deseja ver e selecione **ir para código-fonte**.  
  
### <a name="to-visually-trace-the-call-stack"></a>Para rastrear visualmente a pilha de chamadas  
  
1.  No **pilha de chamadas** janela, abra o menu de atalho. Escolher **Mostrar pilha de chamadas no mapa de códigos**. (Teclado: **CTRL** + **SHIFT** + **`**)  
  
     Ver [mapear métodos na pilha de chamadas ao depurar](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md).  
  
### <a name="to-view-the-disassembly-code-for-a-function-on-the-call-stack"></a>Para exibir o código de desmontagem de uma função na pilha de chamadas  
  
-   No **pilha de chamadas** janela, o botão direito do mouse a função cujo código de desmontagem você deseja ver e selecione **ir para desmontagem**.  
  
### <a name="to-run-to-a-specific-function-from-the-call-stack-window"></a>Para executar em uma função específica da janela de pilha de chamadas  
  
-  No **pilha de chamadas** janela, selecione a função, clique com botão direito e escolha **executar até o Cursor**.  
  
### <a name="to-set-a-breakpoint-on-the-exit-point-of-a-function-call"></a>Para definir um ponto de interrupção no ponto de saída de uma chamada de função  
  
-   Ver [defina um ponto de interrupção em uma função de pilha de chamada](../debugger/using-breakpoints.md#BKMK_Set_a_breakpoint_in_the_call_stack_window).  
  
### <a name="to-load-symbols-for-a-module"></a>Para carregar símbolos para um módulo  
  
-   No **pilha de chamadas** janela, clique com botão direito no quadro que mostra o módulo cujos símbolos você deseja recarregar e selecione **carregar símbolos**.  
  
## <a name="loading-symbols"></a>Carregando símbolos  
 No **pilha de chamadas** janela, você pode carregar símbolos de depuração para o código que não tem símbolos carregados atualmente. Esses símbolos podem ser símbolos do .NET Framework ou do sistema baixados dos servidores públicos de símbolo da Microsoft ou de símbolos em um caminho de símbolo no computador que você está depurando.  
  
 Consulte [especificar símbolo (. PDB) e arquivos de origem](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)  
  
#### <a name="to-load-symbols"></a>Para carregar símbolos  
  
1.  No **pilha de chamadas** janela, o botão direito do mouse o quadro para o qual os símbolos não foram carregados. O quadro ficará esmaecido.  
  
2.  Aponte para **carregar símbolos de** e, em seguida, clique em **servidores de símbolo Microsoft** ou **caminho de símbolo**.  
  
#### <a name="to-set-the-symbol-path"></a>Para definir o caminho do símbolo  
  
1.  No **pilha de chamadas** janela, escolha **configurações de símbolo** no menu de atalho.  
  
     O **opções** caixa de diálogo é aberta e o **símbolos** página é exibida.  
  
2.  Clique em **configurações de símbolo**.  
  
3.  No **opções** caixa de diálogo, clique no ícone de pasta.  
  
     No **locais de arquivo (. PDB) de símbolo** caixa, será exibido um cursor.  
  
4.  Digite um nome de caminho de diretório no local do símbolo no computador que você está depurando. Para depuração local, este é o computador local. Para depuração remota, é o computador remoto.  
  
5.  Clique em **OK** para fechar a caixa de diálogo **Opções**.  
  
## <a name="see-also"></a>Consulte também  
 [Código misto e informações ausentes na janela pilha de chamadas](../debugger/mixed-code-and-missing-information-in-the-call-stack-window.md)   
 [Como: alterar o formato numérico de Windows do depurador](http://msdn.microsoft.com/library/cd593847-a625-411d-a430-b798346ef18f)   
 [Exibindo dados no depurador](../debugger/viewing-data-in-the-debugger.md)   
 [Especifique o símbolo (. PDB) e arquivos de origem](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)   
 [Usando pontos de interrupção](../debugger/using-breakpoints.md)





