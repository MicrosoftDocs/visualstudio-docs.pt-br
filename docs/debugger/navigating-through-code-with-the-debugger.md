---
title: Navegar pelo código com o depurador | Microsoft Docs
ms.custom: seodec18
ms.date: 11/12/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.execution
helpviewer_keywords:
- stepping
- debugging [Visual Studio], execution control
- execution, controlling in debugger
ms.assetid: 759072ba-4aaa-447e-8e51-0dd1456fe896
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: f951732704b178c2726d60f20fc4fedcbd4cde90
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53068267"
---
# <a name="navigate-through-code-with-the-visual-studio-debugger"></a>Navegar pelo código com o depurador do Visual Studio

O depurador do Visual Studio pode ajudá-lo a navegar pelo código para inspecionar o estado de um aplicativo e mostrar o fluxo de execução. Você pode usar atalhos de teclado, comandos de depuração, os pontos de interrupção e outros recursos para obter rapidamente o código que você deseja examinar. Familiaridade com comandos de navegação do depurador e atalhos torna mais rápido e mais fácil localizar e resolver problemas do aplicativo.  Se essa for a primeira vez que você tentou depurar o código, você talvez queira ler [corrigir bugs, escrevendo melhor C# código](../debugger/write-better-code-with-visual-studio.md) e [depuração para iniciantes absolutos](../debugger/debugging-absolute-beginners.md) antes de prosseguir com este artigo.
  
## <a name="basic-debugging"></a>Depuração básica  

Para iniciar seu aplicativo com o depurador anexado, pressione **F5**, selecione **Debug** > **iniciar depuração**, ou selecione a seta verde na barra de ferramentas do Visual Studio.  
  
 ![DBG&#95;Noções básicas&#95;iniciar&#95;depuração](../debugger/media/dbg_basics_start_debugging.png "DBG_Basics_Start_Debugging")  
  
Enquanto você estiver depurando, um realce amarelo mostra a linha de código que executará a próxima.  
  
 ![DBG&#95;Noções básicas&#95;interromper&#95;modo](../debugger/media/dbg_basics_break_mode.png "modo de interrupção")  
  
Mais o depurador de janelas, como o **módulos** e **inspeção** windows, estão disponíveis apenas enquanto o depurador está em execução. Alguns recursos do depurador, como exibir valores de variável na **Locals** janela ou avaliar expressões na **inspeção** janela, estão disponíveis apenas enquanto o depurador está em pausa no ponto de interrupção, também chamado de *modo de interrupção*. 

No modo de interrupção, a execução do aplicativo é suspensa durante a funções, variáveis, e os objetos permanecem na memória. Você pode examinar as posições dos elementos e estados para procurar violações ou bugs. Para alguns tipos de projeto, você também pode fazer ajustes no aplicativo no modo de interrupção. Para obter um vídeo mostrando esses recursos, consulte [Introdução ao depurador](https://www.youtube.com/watch?v=FtGCi5j30YU&list=PLReL099Y5nRfw6VNvzMkv0sabT2crbSpK&index=6).

Se você interromper no código que não tem a origem ou símbolo (*. PDB*) arquivos carregados, o depurador exibe um **arquivos de origem não encontrado** ou **símbolos não encontrados** página que pode ajudá-lo Localizar e carregar os arquivos. Confira [Especificar arquivos de símbolo (.pdb) e de origem](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md). Se você não pode carregar os arquivos de símbolo ou de origem, você ainda poderá depurar as instruções de assembly a **desmontagem** janela. 

Você não precisa sempre iniciar a depuração iniciar um aplicativo no início. Você também pode pressionar **F11** à [intervir no código](#BKMK_Step_into__over__or_out_of_the_code), pressione **F10** para [step over no código](#BKMK_Step_over_Step_out), ou [executados em um local específico ou função](#BKMK_Break_into_code_by_using_breakpoints_or_Break_All).    

##  <a name="step-through-code"></a>Percorrer o código

Os comandos de etapa do depurador ajudam você a inspecionar o estado do aplicativo ou Saiba mais sobre seu fluxo de execução. 

Se você precisar localizar o ponto de entrada em seu aplicativo, comece com **F10** ou **F11**.  

### <a name="BKMK_Step_into__over__or_out_of_the_code"></a> Intervir no código linha por linha  

Para interromper em cada linha de código ou instrução durante a depuração, use **Debug** > **intervir**, ou pressione **F11**.  

O depurador percorre a instruções de código, as linhas não físicas. Por exemplo, uma cláusula `if` pode ser escrita em uma linha:  
  
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

No entanto, quando você entra nessa linha, o depurador trata a condição como uma etapa e a consequência como outra. No exemplo anterior, a condição for verdadeira.  
  
Em uma chamada de função aninhada, a **Depuração Completa** intervém na função aninhada mais profunda. Por exemplo, se você usar **intervir** em uma chamada como `Func1(Func2())`, o depurador vai para a função `Func2`.  

>[!TIP]
>Conforme você executa cada linha de código, você pode passar o mouse sobre as variáveis para ver seus valores, ou usar o [Locals](autos-and-locals-windows.md) e [inspeção](watch-and-quickwatch-windows.md) windows para observar os valores a alterar. Você pode também visualmente a pilha de chamadas ao entrar em funções. Ver [mapear métodos na pilha de chamadas ao depurar](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md). 

###  <a name="BKMK_Step_over_Step_out"></a> Percorrer o código e ignorar algumas funções  

Você pode não se importa uma função durante a depuração ou você sabe que ele funciona, como o código da biblioteca bem testado. Você pode usar os comandos a seguir para ignorar por meio de código. As funções ainda executar, mas o depurador ignora sobre eles.  
  
|Comando de teclado|Comando do menu Depurar|Descrição|  
|----------------------|------------------|-----------------|  
|**F10**|**Depuração Parcial**|Se a linha atual contiver uma chamada de função **Step Over** executa o código e, em seguida, suspende a execução na primeira linha de código após a função chamada retorna.|  
|**Shift**+**F11**|**Depuração Circular**|**Depuração circular** continua a execução de código e suspende a execução quando a função atual é retornado. O depurador ignora por meio da função atual.|  
  
##  <a name="BKMK_Break_into_code_by_using_breakpoints_or_Break_All"></a> Executar até um local específico ou uma função  

Talvez você prefira executar diretamente para um local específico ou uma função quando você sabe exatamente o código que você deseja inspecionar ou, você sabe onde você deseja iniciar a depuração.  
  
### <a name="run-to-a-breakpoint-in-code"></a>Executar um ponto de interrupção no código  
  
Para definir um ponto de interrupção simple em seu código, clique na margem da extrema esquerda ao lado da linha de código onde você deseja suspender a execução. Você também pode selecionar a linha e pressione **F9**, selecione **Debug** > **alternar ponto de interrupção**, ou clique com botão direito e selecione **depontodeinterrupção**  >  **Inserir ponto de interrupção**. O ponto de interrupção aparece como um ponto vermelho na margem esquerda ao lado da linha de código. O depurador suspende a execução imediatamente antes que a linha é executada.
  
![Definir um ponto de interrupção](../debugger/media/dbg_basics_setbreakpoint.png "Definir um ponto de interrupção")  
  
Os pontos de interrupção no Visual Studio fornecem um conjunto rico de funcionalidades adicionais, como pontos de interrupção e pontos de monitoramento condicionais. Para obter detalhes, consulte [usando pontos de interrupção](../debugger/using-breakpoints.md).  
  
### <a name="run-to-a-function-breakpoint"></a>Executar um ponto de interrupção de função  

Você pode instruir o depurador para executar até alcançar uma função especificada. É possível especificar a função por nome ou escolhê-la na pilha de chamadas.  
  
**Para especificar um ponto de interrupção de função por nome**

1. Selecione **Debug** > **novo ponto de interrupção** > **ponto de interrupção de função**
   
1. No **novo ponto de interrupção de função** caixa de diálogo, digite o nome da função e selecione seu idioma.
   
   ![Caixa de diálogo Novo ponto de interrupção de função](../debugger/media/dbg_execution_newbreakpoint.png "novo ponto de interrupção de função")  
   
1. Selecione **OK**. 

Se a função estiver sobrecarregada ou em mais de um namespace, você pode escolher o item desejado na **pontos de interrupção** janela.  

![Sobrecarregado de pontos de interrupção de função](../debugger/media/dbg_execution_overloadedbreakpoints.png "sobrecarregado pontos de interrupção de função")  
  
**Para selecionar um ponto de interrupção de função da pilha de chamadas** 
  
1. Durante a depuração, abra o **pilha de chamadas** janela selecionando **Debug** > **Windows** > **pilha de chamadas**. 
   
1. No **pilha de chamadas** janela, uma função com o botão direito e selecione **executar até o Cursor**, ou pressione **Ctrl**+**F10**.  

Para rastrear visualmente a pilha de chamadas, consulte [mapear métodos na pilha de chamadas ao depurar](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md).  
  
### <a name="run-to-a-cursor-location"></a>Executar em um local do cursor  

Para executar até o local do cursor, no código-fonte ou o **pilha de chamadas** janela, selecione a linha que você deseja interromper em, clique com botão direito e selecione **executar até o Cursor**, ou pressione **Ctrl** + **F10**. Selecionando **executar até o Cursor** é como configurar um ponto de interrupção temporário.

### <a name="run-to-click"></a>Executar com um Clique 

Enquanto está em pausa no depurador, você pode passar o mouse sobre uma instrução no código-fonte ou o **desmontagem** janela e selecione o **executar para este lugar** ícone de seta verde. Usando o **executar com um clique** elimina a necessidade de definir um ponto de interrupção temporário.

![Executar com um Clique](../debugger/media/dbg-run-to-click.png "Executar com um Clique") 

> [!NOTE]
> **Executar com um clique** há de novo no [!include[vs_dev15](../misc/includes/vs_dev15_md.md)].
  
### <a name="manually-break-into-code"></a>Interromper manualmente o código  
  
Para interromper na próxima linha de código em um aplicativo em execução disponível, selecione **Debug** > **interromper tudo**, ou pressione **Ctrl**+**Alt**  + **Interromper**. 
  
##  <a name="BKMK_Set_the_next_statement_to_execute"></a> Mova o ponteiro para alterar o fluxo de execução  

Enquanto o depurador está em pausa, uma seta amarela na margem do código-fonte ou **desmontagem** janela marca o local da próxima instrução a ser executada. Você pode alterar a próxima instrução a executar movendo essa seta. Você pode ignorar uma parte do código ou retornar a uma linha anterior. Movendo o ponteiro é útil para situações como ignorar uma seção de código que contém um bug conhecido.  

 ![Mova o ponteiro](../debugger/media/dbg_basics_example3.gif "mova o ponteiro")
  
Para alterar a próxima instrução a ser executada, o depurador deve estar no modo de interrupção. No código-fonte ou **desmontagem** janela, arraste a seta amarela para uma linha diferente, ou clique na linha que você deseja executar depois e selecione **definir próxima instrução**. 

O contador do programa saltará diretamente para o novo local e instruções entre a execução de nova e antiga pontos não são executados. No entanto, se você mover o ponto de execução com versões anteriores, as instruções intervenientes não são desfeitas.  

>[!CAUTION]
>- Mover a instrução seguinte para outra função ou escopo normalmente resulta em danos à pilha de chamadas, causando um erro em tempo de execução ou uma exceção. Se você tentar mover a instrução seguinte para outro escopo, o depurador abrirá uma caixa de diálogo com um aviso e dará uma chance de cancelar a operação. 
>- No Visual Basic, você não pode mover a instrução seguinte para outro escopo ou função.  
>- No C++ nativo, se você tiver as verificações de tempo de execução ativadas, definir a instrução seguinte poderá fazer com que uma exceção seja gerada quando a execução chegar ao final do método.  
>- Quando a opção Editar e Continuar está habilitada, **Definir Próxima Instrução** falha caso você tenha feito edições que Editar e Continuar não pode remapear imediatamente. Isso pode ocorrer, por exemplo, se você editou o código dentro de um bloco catch. Quando isso acontece, uma mensagem de erro informa que a operação não é suportada.  
>- No código gerenciado, você não pode mover a próxima instrução se:  
>   - A instrução a seguir é um método diferente do que a instrução atual.  
>   - Depuração foi iniciada pelo Just-In-Time de depuração.  
>   - Um desenrolamento de pilha de chamada está em andamento.  
>   - Uma exceção System.StackOverflowException ou System.Threading.ThreadAbortException foi lançada.  
  
## <a name="BKMK_Restrict_stepping_to_Just_My_Code"></a>Depurar o código de não usuário  

Por padrão, o depurador tenta depurar somente o código do aplicativo, permitindo uma configuração chamada *Just My Code*. Para obter mais detalhes sobre como esse recurso funciona para diferentes tipos de projetos e idiomas e como personalizá-lo, consulte [Just My Code](../debugger/just-my-code.md). 

Para examinar o código de estrutura, código da biblioteca de terceiros ou chamadas do sistema durante a depuração, você pode desabilitar apenas meu código. Na **ferramentas** (ou **Debug**) > **opções** > **depuração**, limpe o **habilitar apenas meu código** caixa de seleção. Quando apenas meu código está desabilitado, o código de não usuário é exibido nas janelas do depurador e o depurador pode intervir no código não-usuário.  

> [!NOTE]
> Apenas Meu Código não é suportada para projetos de dispositivo.  
  
### <a name="debug-system-code"></a>Depurar o código do sistema

Se você tiver carregado símbolos de depuração para o código de sistema da Microsoft e apenas meu código, você pode entrar em uma chamada do sistema assim como qualquer outra chamada.  
  
Para carregar símbolos da Microsoft, consulte [configurar locais de símbolos e opções de carregamento](specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md#configure-symbol-locations-and-loading-options).  
  
**Para carregar símbolos para um componente do sistema específicos:**

1. Enquanto você estiver depurando, abra o **módulos** janela selecionando **Debug** > **Windows** > **módulos**, ou pressionando **Ctrl**+**Alt**+**U**.  
  
1. No **módulos** janela, você pode informar quais módulos possuem símbolos carregados na **Status do símbolo** coluna. Com o módulo que você deseja carregar símbolos para e, em seguida, selecione o botão direito **carregar símbolos**.  
  
##  <a name="BKMK_Step_into_properties_and_operators_in_managed_code"></a> Intervir em propriedades e operadores no código gerenciado  
 O depurador considera propriedades e operadores no código gerenciado por padrão. Na maioria dos casos, isso proporciona uma melhor experiência de depuração. Para habilitar a depuração em propriedades ou operadores, escolha **Debug** > **opções**. Sobre o **Debugging** > **geral** página, desmarque o **depurar parcialmente propriedades e operadores (somente gerenciado)** caixa de seleção.

## <a name="see-also"></a>Consulte também
 [O que é depuração?](../debugger/what-is-debugging.md)  
 [Corrigir bugs escrevendo um melhor código C#](../debugger/write-better-code-with-visual-studio.md)  
 [Primeira olhada na depuração](../debugger/debugger-feature-tour.md) 
