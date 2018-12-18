---
title: Navegar pelo código com o depurador | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- vs.debug.execution
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
helpviewer_keywords:
- stepping
- debugging [Visual Studio], execution control
- execution, controlling in debugger
ms.assetid: 759072ba-4aaa-447e-8e51-0dd1456fe896
caps.latest.revision: 47
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 43155bbd4236ea34d67058443e8814f7ccf00b1f
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51750572"
---
# <a name="navigating-through-code-with-the-debugger"></a>Navegar pelo Código com o Depurador
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Familiarize-se com comandos e atalhos para navegar pelo código no depurador e o que torna mais rápido e fácil encontrar e resolver problemas em seu aplicativo. Enquanto você navegar pelo código no depurador, você poderá [inspecionar o estado do seu aplicativo](https://msdn.microsoft.com/library/mt243867.aspx#BKMK_Inspect_Variables) ou Saiba mais sobre seu fluxo de execução.  
  
## <a name="start-debugging"></a>Iniciar a depuração  
 Muitas vezes, você inicia uma sessão de depuração usando **F5** (**Debug** / **iniciar depuração**). Esse comando inicia o aplicativo com o depurador anexado.  
  
 A seta verde também inicia o depurador (mesmo que **F5**).  
  
 ![DBG&#95;Basics&#95;Start&#95;Debugging](../debugger/media/dbg-basics-start-debugging.png "DBG_Basics_Start_Debugging")  
  
 Algumas outras maneiras que você pode iniciar o aplicativo com o depurador anexado incluem **F11** ([intervir no código](#BKMK_Step_into__over__or_out_of_the_code)), **F10** ([step over no código](#BKMK_Step_over_Step_out)), ou por usando o **executar até o Cursor**.  Consulte as outras seções neste tópico para obter informações sobre o que fazem essas opções.  
  
 Quando você depura, a linha amarela mostra o código que executará a seguir.  
  
 ![DBG&#95;Noções básicas&#95;interromper&#95;modo](../debugger/media/dbg-basics-break-mode.png "DBG_Basics_Break_Mode")  
  
 Durante a depuração, você pode alternar entre os comandos **F5**, **F11** e usar outros recursos descritos neste tópico (como pontos de interrupção) para obter rapidamente o código que você deseja examinar.  
  
 A maioria dos recursos do depurador, como exibir valores de variáveis na janela locais ou avaliar expressões na janela de inspeção, estão disponíveis apenas enquanto o depurador estiver pausado (também chamado de *modo de interrupção*). Quando o depurador estiver pausado, o estado do aplicativo é suspenso durante a funções, variáveis, e os objetos permanecem na memória. No modo de interrupção, você pode examinar as posições dos elementos e estados para procurar violações ou bugs. Para alguns tipos de projeto, você também pode fazer ajustes no aplicativo no modo de interrupção.  
  
##  <a name="BKMK_Step_into__over__or_out_of_the_code"></a> Intervir no código, linha por linha  
 Para interromper em cada linha de código (cada instrução) durante a depuração, use o **F11** atalho de teclado (ou **Debug** / **intervir** no menu).  
  
> [!TIP]
>  Conforme você executa cada linha de código, você pode passar o mouse sobre as variáveis para ver seus valores, ou usar o [Locals](../debugger/autos-and-locals-windows.md) e [inspeção](../debugger/autos-and-locals-windows.md) windows para observar os valores a alterar.  
  
 Aqui estão alguns detalhes sobre o comportamento do **intervir**:  
  
- Em uma chamada de função aninhada **intervir** etapas para a função aninhada mais profundamente. Se você usar **intervir** em uma chamada como `Func1(Func2())`, o depurador vai para a função `Func2`.  
  
- O depurador avança realmente com as instruções de código em vez de linhas físicas. Por exemplo, uma cláusula `if` pode ser gravada em uma linha:  
  
  ```csharp  
  int x = 42;  
  string s = "Not answered";  
  if( int x == 42) s = "Answered!";  
  ```  
  
  ```vb  
  Dim x As Integer = 42  
  Dim s As String = "Not answered"  
  If x = 42 Then s = "Answered!"  
  ```  
  
   Quando você entra nessa linha, o depurador trata a condição como uma etapa e a consequência como outra (nesse exemplo, a condição é verdadeira.)  
  
  Para rastrear visualmente a pilha de chamadas ao entrar em funções, consulte [mapear métodos na pilha de chamadas ao depurar](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md).  
  
##  <a name="BKMK_Step_over_Step_out"></a> Percorrer o código, ignorando a funções  
 Ao executar o código no depurador, muitas vezes você vai perceber que você não precisa ver o que acontece em uma função específica (não se preocupa-lo ou se você souber que ele funciona, como o código da biblioteca bem testado). Use estes comandos para ignorar por meio de código (as funções ainda forem executados, claro, mas o depurador ignora-los).  
  
|Comando de teclado|Menu Comando|Descrição|  
|----------------------|------------------|-----------------|  
|**F10**|**Depuração Parcial**|Se a linha atual contiver uma chamada de função **Step Over** executa o código e em seguida, suspende a execução na primeira linha de código após a função chamada retorna.|  
|**Shift+F11**|**Depuração Circular**|**Depuração circular** continua a execução de código e suspende a execução quando a função atual (a depurador ignora por meio da função atual) é retornado.|  
  
> [!TIP]
>  Se você precisar localizar o ponto de entrada em seu aplicativo, comece com **F10** ou **F11**. Esses comandos geralmente são úteis quando você inspecionar o estado do aplicativo ou tentar encontrar mais informações sobre seu fluxo de execução.  
  
##  <a name="BKMK_Break_into_code_by_using_breakpoints_or_Break_All"></a> Executar até um local específico ou uma função  
 Geralmente o método preferencial de depuração de código, esses métodos são úteis quando você sabe exatamente o código que você deseja inspecionar ou ao menos sabe onde você deseja iniciar a depuração.  
  
-   **Defina pontos de interrupção no código**  
  
     Para definir um ponto de interrupção simples em seu código, abra o arquivo de origem no editor do Visual Studio. Defina o cursor na linha de código onde você deseja suspender a execução e, em seguida, com o botão direito na janela de código para ver o menu de contexto e escolha **ponto de interrupção / Inserir ponto de interrupção** (ou pressione **F9**). O depurador suspende o direito de execução antes da linha é executada.  
  
     ![Defina um ponto de interrupção](../debugger/media/dbg-basics-setbreakpoint.png "DBG_Basics_SetBreakpoint")  
  
     Os pontos de interrupção no Visual Studio fornecem um conjunto rico de funcionalidades adicionais, como pontos de interrupção e pontos de monitoramento condicionais. Ver [usando pontos de interrupção](../debugger/using-breakpoints.md).  
  
-   **Executar até o local do cursor**  
  
     Para executar a localização do cursos, coloque o cursor em uma linha executável do código em uma janela de origem. No menu de contexto do editor (clique com botão direito no editor), escolha **executar até o Cursor**. Isso é como configurar um ponto de interrupção temporário.  
  
-   **Interromper manualmente o código**  
  
     Para interromper a próxima linha de código em um aplicativo executando disponível, escolha **Debug**, **interromper tudo** (teclado: **Ctrl + Alt + Break**).  
  
     Se você interromper a execução de código sem origem correspondente ou símbolo arquivos (. PDB)), o depurador exibe uma **arquivos de origem não encontrado** ou um **símbolos não encontrados** página que pode ajudá-lo a encontrar o apropriada arquivos. Confira [Especificar arquivos de símbolo (.pdb) e de origem no Depurador do Visual Studio](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md). Se não for possível acessar os arquivos de suporte, você ainda poderá depurar as instruções de assembly na janela de desmontagem.  
  
-   **Executar uma função na pilha de chamadas**  
  
     No **pilha de chamadas** janela (disponível durante a depuração), selecione a função, clique com botão direito e escolha **executar até o Cursor**. Para rastrear visualmente a pilha de chamadas, consulte [mapear métodos na pilha de chamadas ao depurar](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md).  
  
-   **Executar uma função especificada por nome**  
  
     Você pode instruir o depurador para executar o aplicativo até atingir uma função especificada. É possível especificar a função por nome ou escolhê-la da pilha de chamadas.  
  
     Para especificar uma função por nome, escolha **Debug**, **novo ponto de interrupção**, **interromper na função**, em seguida, insira o nome da função e outras informações de identificação.  
  
     ![Caixa de diálogo Novo ponto de interrupção](../debugger/media/dbg-execution-newbreakpoint.png "DBG_Execution_NewBreakpoint")  
  
     Se a função estiver sobrecarregada ou estiver em vários namespaces, você pode escolher as funções que você deseja na **escolher pontos de interrupção** caixa de diálogo.  
  
     ![Escolha a caixa de diálogo de pontos de interrupção](../debugger/media/dbg-execution-overloadedbreakpoints.png "DBG_Execution_OverloadedBreakpoints")  
  
##  <a name="BKMK_Set_the_next_statement_to_execute"></a> Mova o ponteiro para alterar o fluxo de execução  
 Enquanto o depurador estiver pausado, você pode mover o ponteiro de instrução para definir a próxima instrução de código a ser executada. Uma seta amarela na margem de uma fonte ou janela de desmontagem marca o local da próxima instrução a ser executada. Movendo essa seta, você pode ignorar uma parte do código ou retornar a uma linha executada anteriormente. É possível usar esse procedimento para situações como ignorar uma seção de código que contém um bug conhecido.  
  
 ![Example2](../debugger/media/dbg-basics-example2.png "DBG_Basics_Example2")  
  
 Para definir a próxima instrução a ser executada, use um destes procedimentos:  
  
-   Em uma janela de origem, arraste a seta amarela para um local onde você deseja definir a instrução seguinte no mesmo arquivo de origem  
  
-   Em uma janela de origem, coloque o cursor na linha que você deseja executar em seguida, clique com botão direito e escolha **definir próxima instrução**.  
  
-   Na janela de desmontagem, coloque o cursor na instrução de montagem que você deseja executar em seguida, clique com botão direito um e escolha **definir próxima instrução**.  
  
> [!CAUTION]
>  Definir a instrução a seguir faz com que o contador do programa pule diretamente para a nova localização. Use este comando com cuidado:  
> 
> - As instruções entre os pontos de execução antigos e novos não são executadas.  
>   -   Se você mover o ponto de execução para trás, as instruções intervenientes não serão desfeitas.  
>   -   Mover a instrução seguinte para outra função ou escopo normalmente resulta em danos à pilha de chamadas, causando um erro em tempo de execução ou uma exceção. Se você tentar mover a instrução seguinte para outro escopo, o depurador abrirá uma caixa de diálogo com um aviso e dará uma chance de cancelar a operação. No Visual Basic, você não pode mover a instrução seguinte para outro escopo ou função.  
>   -   No C++ nativo, se você tiver as verificações de tempo de execução ativadas, definir a instrução seguinte poderá fazer com que uma exceção seja gerada quando a execução chegar ao final do método.  
>   -   Quando editar e continuar está ativada, **definir próxima instrução** falhar caso você tenha feito edições que editar e continuar não pode remapear imediatamente. Isso pode ocorrer, por exemplo, se você editou o código dentro de um bloco catch. Quando isso acontece, você verá uma mensagem de erro que indica que a operação não é suportada.  
> 
> [!NOTE]
>  No código gerenciado, você não pode mover a instrução seguinte nas seguintes circunstâncias:  
> 
> - A instrução a seguir é um método diferente do que a instrução atual.  
>   -   A depuração foi iniciada com a depuração Just-In-Time.  
>   -   Um desenrolamento de pilha de chamada está em andamento.  
>   -   Uma exceção System.StackOverflowException ou System.Threading.ThreadAbortException foi lançada.  
  
 Não é possível definir a próxima instrução durante a execução ativa do seu aplicativo. Para definir a próxima instrução, o depurador deve estar no modo de interrupção.  
  
## <a name="step-into-non-user-code"></a>Intervir no código de não usuário  
 Por padrão, o depurador tenta mostram somente o código do aplicativo durante a depuração, que é determinado por um depurador chamada *Just My Code*. (Consulte [Just My Code](../debugger/just-my-code.md) para ver como isso funciona para diferentes tipos de projetos e idiomas e como você pode personalizar o comportamento.) No entanto, às vezes, enquanto você estiver depurando, convém examinar o código do framework, o código da biblioteca de terceiros ou chamadas para o sistema operacional (chamadas do sistema).  
  
 Você pode desativar o Just My Code acessando **ferramentas** / **opções** / **depuração** e desmarque o **habilitar apenas meu código** caixa de seleção.  
  
 Quando apenas meu código está desabilitado, o depurador pode intervir no código de não usuário e código de não usuário é exibido nas janelas do depurador.  
  
> [!NOTE]
>  Apenas Meu Código não é suportada para projetos de dispositivo.  
  
 **Entrar em chamadas do sistema**  
  
 Se você tiver carregado símbolos de depuração para código do sistema e apenas meu código não está habilitado, você poderá intervir uma chamada do sistema assim como qualquer outra chamada.  
  
 Para acessar arquivos de símbolo Microsoft, consulte [usar servidores de símbolo para localizar arquivos de símbolo não em seu computador local](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md#BKMK_Use_symbol_servers_to_find_symbol_files_not_on_your_local_machine) na [especificar arquivos de símbolo (. PDB) e código-fonte](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md) tópico.  
  
 Para carregar símbolos para um componente do sistema específico enquanto você depura:  
  
1.  Abra a janela de módulos (teclado: **Ctrl + Alt + U**).  
  
2.  Selecione o módulo para os quais você deseja carregar os símbolos.  
  
     Você pode informar quais módulos possuem símbolos carregados, observando os **Status do símbolo** coluna.  
  
3.  Escolher **carregar símbolos** no menu de contexto.  
  
##  <a name="BKMK_Step_into_properties_and_operators_in_managed_code"></a> Depurar propriedades e operadores no código gerenciado  
 O depurador considera propriedades e operadores no código gerenciado por padrão. Na maioria dos casos, isso proporciona uma melhor experiência de depuração. Para habilitar a depuração em propriedades ou operadores, escolha **Debug** / **opções**. Sobre o **Debugging** / **geral** página, desmarque o **depurar parcialmente propriedades e operadores (somente gerenciado)** caixa de seleção





