---
title: Usar pontos de interrupção no depurador | Microsoft Docs
ms.custom: seodec18
ms.date: 10/15/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.breakpointswin
- vs.debug.disassembly.insert
- vs.debug.sourcewin.edit
- vs.debug.file
- vs.debug.breakpt.new
- vs.debug.whenbreakpointishit
- vs.debug.breakpt.choose
- vs.debug.breakpt.location.address
- vs.debug.breakpt.constraints
- vs.debug.breakpoints.delete
- vs.debug.breakpt.location.data
- vc.breakpoints
- vs.debug.breakpt.condition
- vs.debug.breakpt.location.function
- vs.debug.breakpoints
- vs.debug.menu.insert
- vs.debug.filenames
- vs.debug.breakpt.action
- vs.debug.sourcewin.insert
- vs.debug.address
- vs.debug.data
- vs.debug.func
- vs.debug.breakpt.location.file
helpviewer_keywords:
- breakpoints, about breakpoints
ms.assetid: 020b2e97-3b3e-4b2c-872d-b5c6025e120e
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 16bcb4bb12e852a8fa268998d0605b2ffc7471e5
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53068442"
---
# <a name="use-breakpoints-in-the-visual-studio-debugger"></a>Usar pontos de interrupção no depurador do Visual Studio
Pontos de interrupção são uma das técnicas de depuração mais importantes na caixa de ferramentas do seu desenvolvedor. Sempre que você deseja pausar a execução do depurador, você definir pontos de interrupção. Por exemplo, talvez você queira ver o estado das variáveis de código ou examinar a pilha de chamadas em um determinado ponto de interrupção. Se esta for sua primeira tentativa de depurar um código, leia [Como depurar para iniciantes absolutos](../debugger/debugging-absolute-beginners.md) antes continuar neste artigo.
  
##  <a name="BKMK_Overview"></a> Defina pontos de interrupção no código-fonte  
 Você pode definir um ponto de interrupção em qualquer linha de código executável. Por exemplo, no seguinte C# código, você pode definir um ponto de interrupção na declaração de variável, o `for` loop ou qualquer código dentro de `for` loop. Não é possível definir um ponto de interrupção, as declarações de namespace ou classe ou a assinatura do método.  

 Para definir um ponto de interrupção no código-fonte, clique na margem da extrema esquerda ao lado de uma linha de código. Você também pode selecionar a linha e pressione **F9**, selecione **Debug** > **alternar ponto de interrupção**, ou clique com botão direito e selecione **depontodeinterrupção**  >  **Inserir ponto de interrupção**. O ponto de interrupção aparece como um ponto vermelho na margem esquerda.  

No C# código, o ponto de interrupção e linhas de execução atual são realçadas automaticamente. Para código C++, você pode ativar realce de ponto de interrupção e linhas atuais, selecionando **ferramentas** (ou **Debug**) > **opções**  >   **Depurando** >  **realçar a linha de origem inteira para pontos de interrupção e a instrução atual (C++)**. 
  
 ![Defina um ponto de interrupção](../debugger/media/basicbreakpoint.png "básico ponto de interrupção")  
  
 Quando você depura, a execução pausa no ponto de interrupção, antes do código nessa linha é executado. O símbolo de ponto de interrupção mostra uma seta amarela. 

 O ponto de interrupção no exemplo a seguir, o valor de `testInt` ainda é 1.  
  
 ![Execução de ponto de interrupção interrompida](../debugger/media/breakpointexecution.png "execução de ponto de interrupção")  
  
 Quando o depurador é interrompido no ponto de interrupção, você pode examinar o estado atual do aplicativo, incluindo valores de variáveis e a pilha de chamadas. Para obter mais informações sobre a pilha de chamadas, consulte [como: usar a janela pilha de chamadas](../debugger/how-to-use-the-call-stack-window.md).  

- O ponto de interrupção é um controle de alternância. Você pode clicar nele, pressione **F9**, ou use **Debug** > **alternar ponto de interrupção** para excluir ou inseri-lo novamente.
  
- Para desabilitar um ponto de interrupção sem excluí-la, passe o mouse sobre ou clique duas vezes e selecione **desabilitar ponto de interrupção**. Pontos de interrupção desabilitados serão exibidos como pontos vazios na margem esquerda ou o **pontos de interrupção** janela. Para reabilitar um ponto de interrupção, passe o mouse sobre ou clique duas vezes e selecione **habilitar ponto de interrupção**. 
  
- Definir condições e ações, adicionar e editar rótulos ou exportar um ponto de interrupção direito do mouse e selecionando o comando apropriado, ou passando o mouse sobre ele e o **configurações** ícone.

##  <a name="BKMK_Set_a_breakpoint_in_a_function"></a> Definir pontos de interrupção do depurador do windows 

Você também pode definir pontos de interrupção do **pilha de chamadas** e **desmontagem** janelas do depurador.  
  
### <a name="BKMK_Set_a_breakpoint_in_the_call_stack_window"></a> Definir um ponto de interrupção na janela pilha de chamadas  

 Para interromper na instrução ou na linha de uma função de chamada retorna, você pode definir um ponto de interrupção na **pilha de chamadas** janela. 
  
**Para definir um ponto de interrupção na janela pilha de chamadas:**

1. Para abrir o **pilha de chamadas** janela, você precisa ser interrompido durante a depuração. Selecione **Debug** > **Windows** > **pilha de chamadas**, ou pressione **Ctrl** + **Alt**+**C**.  
   
2. No **pilha de chamadas** janela, a função de chamada com o botão direito e selecione **ponto de interrupção** > **Inserir ponto de interrupção**, ou pressione **F9**.  
   
   Um símbolo de ponto de interrupção aparecerá ao lado do nome da chamada de função na margem esquerda da pilha de chamadas.
   
O ponto de interrupção de pilha de chamada aparece na **pontos de interrupção** janela como um endereço, com um local de memória que corresponde à próxima instrução executável na função. 

O depurador interrompe na instrução.  

Para obter mais informações sobre a pilha de chamadas, consulte [como: usar a janela pilha de chamadas](../debugger/how-to-use-the-call-stack-window.md). 

Para visualmente rastrear pontos de interrupção durante a execução de código, consulte [mapear métodos na pilha de chamadas ao depurar](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md). 
  
### <a name="set-a-breakpoint-in-the-disassembly-window"></a>Defina um ponto de interrupção na janela de desmontagem  
   
1. Para abrir o **desmontagem** janela, você precisa ser interrompido durante a depuração. Selecione **Debug** > **Windows** > **desmontagem**, ou pressione **Alt** + **8**.  
   
2. No **desmontagem** janela, clique na margem esquerda da instrução que você deseja interromper. Você também pode selecioná-lo e pressionar **F9**, ou clique com botão direito e selecione **ponto de interrupção** > **Inserir ponto de interrupção**. 

##  <a name="BKMK_Set_a_breakpoint_in_a_source_file"></a> Defina pontos de interrupção de função  

  Você pode interromper a execução quando uma função é chamada. 

**Para definir um ponto de interrupção de função:**
  
1. Selecione **Debug** > **novo ponto de interrupção** > **ponto de interrupção de função**, ou pressione **Alt** + **F9** > **Ctrl**+**B**. 
   
   Você também pode selecionar **New** > **ponto de interrupção de função** no **pontos de interrupção** janela.
   
1. No **novo ponto de interrupção de função** caixa de diálogo, insira o nome da função a **nome da função** caixa. 

   Para restringir a especificação de função:
   
   - Use o nome da função totalmente qualificado. 
     
     Exemplo: `Namespace1.ClassX.MethodA()`
     
   - Adicione os tipos de parâmetro de uma função sobrecarregada. 
     
     Exemplo: `MethodA(int, string)`
     
   - Use o '!' símbolo para especificar o módulo.
     
     Exemplo: `App1.dll!MethodA`
     
   - Use o operador de contexto em C++ nativo.
     
     `{function, , [module]} [+<line offset from start of method>]`
     
     Exemplo: `{MethodA, , App1.dll}+2`
   
1. No **linguagem** lista suspensa, escolha o idioma da função.
   
1. Selecione **OK**.
  
### <a name="set-a-function-breakpoint-using-a-memory-address-native-c-only"></a>Defina um ponto de interrupção de função usando um endereço de memória (somente C++ nativo)  
 Você pode usar o endereço de um objeto para definir um ponto de interrupção de função em um método chamado por uma instância específica de uma classe.  Por exemplo, dado um objeto do tipo de endereçável `my_class`, você pode definir um ponto de interrupção de função no `my_method` essa instância de chamadas de método. 
  
1.  Defina um ponto de interrupção em algum lugar depois que a instância da classe é instanciada.  
    
2.  Localizar o endereço da instância (por exemplo, `0xcccccccc`). 
    
3.  Selecione **Debug** > **novo ponto de interrupção** > **ponto de interrupção de função**, ou pressione **Alt** + **F9** > **Ctrl**+**B**.  
    
4.  Adicione o seguinte para o **nome da função** caixa e selecione **C++** idioma.  
    
    ```C++  
    ((my_class *) 0xcccccccc)->my_method  
    ```  

## <a name="BKMK_set_a_data_breakpoint_native_cplusplus_only"></a>Definir pontos de interrupção de dados (somente C++ nativo) 
 
 Pontos de interrupção interromper a execução quando um valor armazenado em um alterações de endereço de memória especificado. Se o valor é lido, mas não alterado, não interrompe a execução.  
  
**Para definir um ponto de interrupção de dados:**

1.  Em um projeto do C++, iniciar a depuração e aguarde até que um ponto de interrupção seja atingido. Sobre o **Debug** menu, escolha **novo ponto de interrupção** > **ponto de interrupção de dados** 

    Você também pode selecionar **New** > **ponto de interrupção de dados** no **pontos de interrupção** janela.
  
2.  No **endereço** , digite um endereço de memória ou uma expressão que é avaliada como um endereço de memória. Por exemplo, digite `&avar` para interromper quando o conteúdo da variável `avar` alterações.  
  
3.  No **contagem de bytes** lista suspensa, selecione o número de bytes que você deseja que o depurador para observar. Por exemplo, se você selecionar **4**, o depurador examinará os quatro bytes começando em `&avar` e interromperá se qualquer um desses bytes mudar o valor.  

Pontos de interrupção não funcionam nas seguintes condições:  
-   Um processo que não estiver sendo depurado grava na localização da memória.  
-   A localização de memória é compartilhada entre dois ou mais processos.  
-   O local da memória é atualizado no kernel. Por exemplo, se a memória é passada para o Windows de 32 bits `ReadFile` função, a memória será atualizada de modo kernel, portanto, o depurador não quebre na atualização.  

>[!NOTE]
>- Pontos de interrupção de dados dependem de endereços de memória específica. O endereço de uma variável muda de uma sessão de depuração para o próximo, para que os pontos de interrupção de dados são automaticamente desabilitados no final de cada sessão de depuração.  
>  
>- Se você definir um ponto de interrupção de dados em uma variável local, o ponto de interrupção permanece habilitado quando a função terminar, mas o endereço de memória não é mais aplicável, portanto, o comportamento do ponto de interrupção é imprevisível. Se você definir um ponto de interrupção de dados em uma variável local, você deve excluir ou desabilitar o ponto de interrupção antes do fim da função.  

##  <a name="BKMK_Specify_advanced_properties_of_a_breakpoint_"></a> Gerenciar pontos de interrupção na janela de Pontos de Interrupção 

 Você pode usar o **pontos de interrupção** janela para ver e gerenciar todos os pontos de interrupção em sua solução. Esse local centralizado é especialmente útil em uma solução grande ou para cenários complexos de depuração em que os pontos de interrupção são essenciais. 

No **pontos de interrupção** janela, você pode pesquisar, classificar, filtrar, habilitar/desabilitar ou excluir pontos de interrupção. Você também pode definir condições e ações ou adicionar uma nova função ou um ponto de interrupção de dados.
  
Para abrir o **pontos de interrupção** janela, selecione **Debug** > **Windows** > **pontos de interrupção**, ou pressione  **ALT**+**F9** ou **Ctrl**+**Alt**+**B**.
  
![Janela pontos de interrupção](../debugger/media/breakpointswindow.png "janela pontos de interrupção")  
  
Para selecionar as colunas para exibir o **pontos de interrupção** janela, selecione **Mostrar colunas**. Selecione um cabeçalho de coluna para classificar a lista de pontos de interrupção com base nessa coluna. 

###  <a name="BKMK_Set_a_breakpoint_at_a_function_return_in_the_Call_Stack_window"></a> Rótulos de ponto de interrupção  
Você pode usar rótulos para classificar e filtrar a lista de pontos de interrupção a **pontos de interrupção** janela. 

1. Para adicionar um rótulo a um ponto de interrupção, clique com botão direito do ponto de interrupção no código-fonte ou o **pontos de interrupção** janela e, em seguida, selecione **editar rótulos**. Adicionar um novo rótulo ou escolha um existente e, em seguida, selecione **Okey**.
2. Classifique a lista de ponto de interrupção na **pontos de interrupção** selecionando o **rótulos**, **condições**, ou outros cabeçalhos de coluna. Você pode selecionar as colunas a ser exibida marcando **Mostrar colunas** na barra de ferramentas. 
  
### <a name="export-and-import-breakpoints"></a>Importar e exportar pontos de interrupção  
 Para salvar ou compartilhar o estado e o local dos seus pontos de interrupção, você pode exportar ou importá-los. 

- Para exportar um único ponto de interrupção em um arquivo XML, clique com botão direito do ponto de interrupção no código-fonte ou **pontos de interrupção** janela e selecione **exportar** ou **Export selecionada**. Selecione um local de exportação e, em seguida, selecione **salvar**. O local padrão é a pasta da solução. 
- Para exportar vários pontos de interrupção na **pontos de interrupção** janela, marque as caixas ao lado de pontos de interrupção, ou insira os critérios de pesquisa a **pesquisa** campo. Selecione o **exportar todos os pontos de interrupção que correspondem aos critérios de pesquisa atual** ícone e salve o arquivo. 
- Para exportar todos os pontos de interrupção, desmarque todas as caixas e deixar o **pesquisa** espaço em branco o campo. Selecione o **exportar todos os pontos de interrupção que correspondem aos critérios de pesquisa atual** ícone e salve o arquivo.  
- Para importar os pontos de interrupção, na **pontos de interrupção** janela, selecione a **importar pontos de interrupção de um arquivo** ícone, navegue até o local do arquivo XML e selecione **abrir**. 

##  <a name="breakpoint-conditions"></a>Condições de ponto de interrupção  
 Você pode controlar quando e onde um ponto de interrupção é executada, definindo condições. A condição pode ser qualquer expressão válida que reconhece o depurador. Para obter mais informações sobre expressões válidas, confira [Expressões no depurador](../debugger/expressions-in-the-debugger.md).  

**Para definir uma condição de ponto de interrupção:**

1. O símbolo de ponto de interrupção com o botão direito e selecione **condições**. Ou passe o mouse sobre o símbolo de ponto de interrupção, selecione o **as configurações** ícone e, em seguida, selecione **condições** no **configurações de ponto de interrupção** janela.  

   Você também pode definir condições **pontos de interrupção** janela clicando duas vezes um ponto de interrupção e selecionando **configurações**e, em seguida, selecionando **condições**. 
  
   ![Configurações de ponto de interrupção](../debugger/media/breakpointsettings.png "BreakpointSettings")  
  
2. No menu suspenso, selecione **expressão condicional**, **contagem de ocorrências**, ou **filtro**e definir o valor correspondente. 
  
3. Selecione **feche** ou pressione **Ctrl**+**Enter** para fechar o **configurações de ponto de interrupção** janela. Ou, do **pontos de interrupção** janela, selecione **Okey** para fechar a caixa de diálogo. 

Pontos de interrupção com o conjunto de condições são exibidos com um **+** símbolo no código-fonte e **pontos de interrupção** windows. 

<a name="BKMK_Specify_a_breakpoint_condition_using_a_code_expression"></a>
### <a name="conditional-expression"></a>Expressão Condicional

Quando você seleciona **expressão condicional**, você pode escolher entre duas condições: **Vale** ou **quando alterado**. Escolher **vale** para interromper quando a expressão for satisfeita, ou **quando alterado** para interromper quando o valor da expressão for alterado.  
  
 No exemplo a seguir, o ponto de interrupção somente quando o valor de `testInt` está **4**:  
  
 ![Condição de ponto de interrupção é verdadeira](../debugger/media/breakpointconditionistrue.png "ponto de interrupção é true")  
  
 No exemplo a seguir, o ponto de interrupção somente quando o valor de `testInt` alterações:  
  
 ![Ponto de interrupção quando alterado](../debugger/media/breakpointwhenchanged.png "ponto de interrupção quando alterado")  
  
 Se você definir uma condição de ponto de interrupção com sintaxe inválida, uma mensagem de aviso será exibida. Se você especificar uma condição de ponto de interrupção com sintaxe válida mas semântica inválida, uma mensagem de aviso aparecerá na primeira vez em que o ponto de interrupção for atingido. Em ambos os casos, o depurador interrompe quando atinge o ponto de interrupção inválido. O ponto de interrupção é ignorado somente se a condição é válida e avaliada como `false`.  
  
 >[!NOTE]
 >O comportamento do **quando alterado** campo é diferente para diferentes linguagens de programação. 
 >- Para código nativo, o depurador não considerará a primeira avaliação da condição como uma alteração, portanto, não atingir o ponto de interrupção na primeira avaliação. 
 >- Para código gerenciado, o depurador atinge o ponto de interrupção na primeira avaliação depois **quando alterado** está selecionado.  
  
### <a name="using-object-ids-in-conditional-expressions-c-and-f-only"></a>Usando IDs de objeto em expressões condicionais (C# e F# somente)  
 Há ocasiões em que você deseja observar o comportamento de um objeto específico. Por exemplo, você talvez queira saber por que um objeto foi inserido em uma coleção de mais de uma vez. No C# e F#, você pode criar IDs de objeto para instâncias específicas de [tipos de referência](/dotnet/csharp/language-reference/keywords/reference-types)e usá-los em condições de ponto de interrupção. A ID de objeto é gerada pelo common language runtime (CLR) serviços de depuração e associada ao objeto.  

**Para criar uma ID de objeto:** 
  
1. Defina um ponto de interrupção no código de algum lugar após o objeto foi criado.  
   
2. Iniciar a depuração e quando a execução pausa no ponto de interrupção, selecione **Debug** > **Windows** > **Locals** ou **Alt** + **4** para abrir o **locais** janela.
   
   Localizar o ponto de interrupção a **Locals** , clique duas vezes e selecione **criar ID de objeto**.  
   
   Você deve ver uma **$** além de um número no **locais** janela. Isso é a ID de objeto.  
   
3. Adicionar um novo ponto de interrupção no ponto em que você deseja investigar; Por exemplo, quando o objeto deve ser adicionado à coleção. Clique com o botão direito do mouse no ponto de interrupção e selecione **Condições**.  
   
4. Use a ID de objeto na **expressão condicional** campo. Por exemplo, se a variável `item` é o objeto a ser adicionado à coleção, selecione **for verdadeira** e digite **item = = $\<n >**, onde \<n > é o número de ID de objeto .  
   
   Execução será interrompida no ponto quando esse objeto deve ser adicionado à coleção.  
   
   Para excluir a ID de objeto, clique com botão direito na variável de **Locals** janela e selecione **excluir ID de objeto**.  

>[!NOTE]
>IDs de objeto criem referências fracas e não impedem que o objeto que está sendo coletado como lixo. Eles só são válidos para a sessão de depuração atual.  
  
### <a name="hit-count"></a>Contagem de acertos  
 Se você suspeitar que um loop em seu código inicia com comportamento inadequado após um determinado número de iterações, você pode definir um ponto de interrupção para interromper a execução após esse número de ocorrências, em vez de precisar pressionar repetidamente **F5** para alcançar essa iteração.  
  
 Sob **condições** na **configurações de ponto de interrupção** janela, selecione **contagem de ocorrências**e, em seguida, especifique o número de iterações. No exemplo a seguir, o ponto de interrupção é definido como atingir em cada iteração outra:  
  
 ![Contagem de ocorrências de ponto de interrupção](../debugger/media/breakpointhitcount.png "BreakpointHitCount")  
  
### <a name="filter"></a>Filtro  
Você pode restringir um ponto de interrupção seja acionado apenas nos dispositivos especificados, ou em threads e processos especificados.  
  
Sob **condições** na **configurações de ponto de interrupção** janela, selecione **filtro**e, em seguida, insira um ou mais das seguintes expressões:  
  
-   MachineName = "name"  
-   ProcessId = valor  
-   ProcessName = "name"  
-   ThreadId = valor  
-   ThreadName = "name"  

Coloque os valores de cadeia de caracteres entre aspas duplas. Você pode combinar cláusulas usando `&` (AND), `||` (OR), `!` (NOT) e parênteses.  
  
##  <a name="BKMK_Print_to_the_Output_window_with_tracepoints"></a> Ações de ponto de interrupção e Tracepoints  
 Um *tracepoint* é um ponto de interrupção que imprime uma mensagem na janela de **Saída**. Um tracepoint pode funcionar como uma declaração de rastreamento temporária na linguagem de programação.  
  
**Para definir um tracepoint:**

1. Um ponto de interrupção com o botão direito e selecione **ações**. Ou, nos **configurações de ponto de interrupção** janela, passe o mouse sobre o ponto de interrupção, selecione o **configurações** ícone e, em seguida, selecione **ações**.  
   
1. Insira uma mensagem na **registrar uma mensagem de janela de saída** campo. A mensagem pode incluir cadeias de caracteres de texto genérico, valores de variáveis ou expressões incluídas em especificadores de formato e entre chaves ([ C# ](../debugger/format-specifiers-in-csharp.md) e [C++](../debugger/format-specifiers-in-cpp.md)) para obter os valores.
   
   Você também pode usar as seguintes palavras-chave especial na mensagem:  
   
   - **$ADDRESS** -instrução atual  
   - **$CALLER** -nome da função de chamada  
   - **$CALLSTACK** -pilha de chamadas 
   - **$FUNCTION** -nome da função atual  
   - **$PID** -id do processo  
   - **$PNAME** -nome do processo  
   - **$TID** -id do thread  
   - **$TNAME** -nome do thread  
   - **$TICK** -contagem de escala (do Windows `GetTickCount`)  
   
1. Para imprimir a mensagem para o **saída** janela sem quebra, selecione o **continuar a execução** caixa de seleção. Para imprimir a execução da mensagem e quebra no tracepoint, desmarque a caixa de seleção. 

Tracepoints são exibidos como losangos vermelhos na margem esquerda do código-fonte e **pontos de interrupção** windows. 
  
## <a name="see-also"></a>Consulte também  
 [O que é depuração?](../debugger/what-is-debugging.md)  
 [Gravar melhor C# o código usando o Visual Studio](../debugger/write-better-code-with-visual-studio.md)  
 [Primeira olhada na depuração](../debugger/debugger-feature-tour.md)  
 [Solucionar problemas de pontos de interrupção no depurador do Visual Studio](../debugger/troubleshooting-breakpoints.md)  
