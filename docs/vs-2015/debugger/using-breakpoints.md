---
title: Usando pontos de interrupção | Microsoft Docs
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
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
helpviewer_keywords:
- breakpoints, about breakpoints
ms.assetid: 020b2e97-3b3e-4b2c-872d-b5c6025e120e
caps.latest.revision: 63
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: d980fd2367545eb5c824bacc507d9ced9aa2d723
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51765952"
---
# <a name="using-breakpoints"></a>Usando pontos de interrupção
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]
Você pode definir pontos de interrupção quando você deseja interromper a execução do depurador, talvez para ver o estado das variáveis de código ou para examinar a pilha de chamadas. Eles são uma das técnicas de depuração mais importantes na caixa de ferramentas do desenvolvedor.
  
##  <a name="BKMK_Overview"></a> Definindo um ponto de interrupção de função no código-fonte  
 Você pode definir um ponto de interrupção de função no código-fonte clicando na margem esquerda de um arquivo de código-fonte ou colocando o cursor em uma linha de código e pressionando F9. O ponto de interrupção aparece como um ponto vermelho na margem esquerda, e a linha de código é colorida também:  
  
 ![Defina um ponto de interrupção](../debugger/media/basicbreakpoint.png "BasicBreakpoint")  
  
 Quando você executa esse código no depurador, a execução é interrompida sempre que o ponto de interrupção for atingido antes que o código nessa linha é executado. A linha de código-fonte é colorida de amarela:  
  
 ![Execução de ponto de interrupção interrompida](../debugger/media/breakpointexecution.png "BreakpointExecution")  
  
 Neste ponto, o valor de `testInt` ainda é 1.  
  
 Você pode examinar o estado atual do aplicativo, incluindo valores de variáveis e a pilha de chamadas. Para obter mais informações sobre a pilha de chamadas, consulte [como: usar a janela pilha de chamadas](../debugger/how-to-use-the-call-stack-window.md).  
  
 Você pode definir um ponto de interrupção em qualquer linha de código executável. Por exemplo, no c# o código acima, você pode definir um ponto de interrupção na declaração de variável, o `for` loop ou qualquer código dentro de `for` loop, mas você não pode definir um ponto de interrupção nas declarações de namespace ou classe ou a assinatura do método.  
  
##  <a name="BKMK_Set_a_breakpoint_in_a_source_file"></a> Configuração de outros tipos de pontos de interrupção  
 Você também pode definir pontos de interrupção na pilha de chamadas, na janela de desmontagem e, em código C++ nativo, em uma condição de dados ou um endereço de memória.  
  
## <a name="BKMK_Set_a_breakpoint_in_the_call_stack_window"></a> Definindo um ponto de interrupção na janela de pilha de chamadas  
 Você pode interromper a execução na instrução ou na linha de uma função de chamada retorna, definindo um ponto de interrupção **pilha de chamadas** janela. Para obter mais informações sobre a pilha de chamadas, consulte [como: usar a janela pilha de chamadas](../debugger/how-to-use-the-call-stack-window.md). O depurador deve ter parado de executar.  
  
1. Iniciar a depuração do aplicativo e execução de espera é interrompida (por exemplo, em um ponto de interrupção). Abra o **pilha de chamadas** janela (**depurar / Windows / pilha de chamadas**, ou **CTRL + ALT + C**).  
  
2. A função de chamada com o botão direito e, em seguida, selecione **ponto de interrupção / Inserir ponto de interrupção**, ou simplesmente usar a tecla de atalho **F9**.  
  
3. Um símbolo de ponto de interrupção aparece na margem esquerda da pilha de chamadas, ao lado do nome da função de chamada.  
  
   No **pontos de interrupção** janela, o ponto de interrupção de pilha de chamadas é exibida como um endereço com um local de memória que corresponde à próxima instrução executável na função. O depurador interrompe a execução na instrução.  
  
   Para visualmente rastrear pontos de interrupção durante a execução de código, consulte [mapear métodos na pilha de chamadas ao depurar](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md).  
  
## <a name="setting-a-breakpoint-in-the-disassembly-window"></a>Definindo um ponto de interrupção na janela de desmontagem  
 Para definir um ponto de interrupção em uma instrução de assembly, o depurador deve estar no modo de interrupção.  
  
1.  Iniciar a depuração do aplicativo e execução de espera é interrompida (por exemplo, em um ponto de interrupção). Abra o **desmontagem** janela (**depurar / Windows / desmontagem**, ou **Ctrl + Alt + D**).  
  
2.  Clique na margem esquerda na instrução que você deseja interromper em, ou defina o cursor na instrução e pressione **F9**.  
  
## <a name="BKMK_set_a_data_breakpoint_native_cplusplus_only"></a> Definindo um ponto de interrupção de dados (somente C++ nativo)  
 Pontos de interrupção interromper a execução quando um valor que é armazenado em um alterações de endereço de memória especificado. Se o valor é lido, mas não alterado, não interrompe a execução. Para definir pontos de interrupção de dados, o depurador deve estar em modo de interrupção.  
  
1. Iniciar a depuração do aplicativo e aguarde até que um ponto de interrupção seja atingido. No **Debug** menu, escolha **novo ponto de interrupção / ponto de interrupção de dados** (ou abrir o **pontos de interrupção** janela e escolha **novo / ponto de interrupção de dados**.  
  
2. No **endereço** , digite um endereço de memória ou uma expressão que é avaliada para um endereço de memória. Por exemplo, digite `&avar` para interromper quando o conteúdo da variável `avar` alterações.  
  
3. No **contagem de bytes** lista suspensa, selecione o número de bytes que você deseja que o depurador para observar. Por exemplo, se você selecionar **4**, o depurador examinará os quatro bytes começando em `&avar` e interromperá se qualquer um desses bytes mudar o valor.  
  
   Tenha em mente que pontos de interrupção de dados dependem da aplicabilidade de endereços específicos de memória.  
  
- O endereço de uma variável muda de uma sessão de depuração para o próximo. Pontos de interrupção de dados serão desabilitados automaticamente no final de cada sessão de depuração.  
  
- Se você definir um ponto de interrupção de dados em uma variável local, o permanece de ponto de interrupção habilitado quando a função terminar, mas o endereço de memória não é mais aplicável, e o comportamento do ponto de interrupção é imprevisível. Se você definir um ponto de interrupção de dados em uma variável local, você deve remover ou desabilitar o ponto de interrupção antes do fim da função.  
  
  Pontos de interrupção não funcionam nestas condições:  
  
- Um processo que está sendo depurado não grava no local de memória  
  
- O local da memória é compartilhado entre dois ou mais processos  
  
- O local da memória é atualizado no kernel. Por exemplo, se a memória é passada para o Windows de 32 bits `ReadFile` função, a memória será atualizada de modo kernel e o depurador não interromperá a gravação na memória.  
  
## <a name="setting-a-breakpoint-with-a-memory-address-native-c-only"></a>Definindo um ponto de interrupção com um endereço de memória (somente C++ nativo)  
 Você também pode usar o endereço de um objeto para definir um ponto de interrupção em um método chamado em uma instância específica de uma classe.  Veja um exemplo:  
  
 Por exemplo, dado um objeto do tipo `my_class` com o endereço, você pode definir um ponto de interrupção de função em um método chamado `my_method` chamado a partir dessa instância.  
  
1.  Defina um ponto de interrupção em algum lugar depois que essa instância da classe é instanciada.  
  
2.  Localizar o endereço da instância (vamos dizer tem `0xcccccccc`).  
  
3.  Clique em **Debug / novo ponto de interrupção de função ponto de interrupção** (ou **ALT + F9, B**).  
  
4.  Adicione o seguinte texto para o **nome da função** caixa:  
  
    ```cpp  
    ((my_class *) 0xcccccccc)->my_method  
    ```  
  
##  <a name="BKMK_Specify_advanced_properties_of_a_breakpoint_"></a> Gerenciando pontos de interrupção  
 Você pode usar o **pontos de interrupção** janela (**depurar / Windows / pontos de interrupção**, ou **CTRL + ALT + B**) para ver todos os pontos de interrupção que você tiver definido em sua solução:  
  
 ![Janela pontos de interrupção](../debugger/media/breakpointswindow.png "BreakpointsWindow")  
  
 O **pontos de interrupção** janela fornece um local central para gerenciar todos os seus pontos de interrupção, que pode ser especialmente úteis em uma solução grande ou um cenário complexo de depuração em que os pontos de interrupção são essenciais. Se você precisar salvar ou compartilhar o estado e o local de um conjunto de pontos de interrupção, você pode exportar e importar pontos de interrupção somente a partir de **pontos de interrupção** janela.  
  
##  <a name="BKMK_Specify_a_breakpoint_condition_using_a_code_expression"></a> Pontos de interrupção avançados  
  
## <a name="breakpoint-conditions"></a>Condições de ponto de interrupção  
 Você pode controlar quando e onde um ponto de interrupção é executada, definindo condições.  
  
1. Clique com botão direito no ponto de interrupção, ou passe o mouse sobre o ponto de interrupção e escolha o ícone de configurações.  
  
2. No menu de contexto, selecione **condições**. Isso abre o **configurações de ponto de interrupção** janela:  
  
   ![Configurações de ponto de interrupção](../debugger/media/breakpointsettings.png "BreakpointSettings")  
  
   Quando você verificar a **condições** caixa, a janela expande para mostrar os diferentes tipos de condições.  
  
   **Expressão condicional:** quando você seleciona a expressão condicional, você pode escolher duas condições: **vale** e **quando alterado**. Escolher **vale** se você quiser interromper quando a expressão for satisfeita ou escolha **quando alterado** se você quiser interromper quando o valor da expressão for alterado.  
  
   No exemplo a seguir, definimos o ponto de interrupção atingido somente quando o valor de `testInt` está **4**:  
  
   ![Condição de ponto de interrupção é verdadeira](../debugger/media/breakpointconditionistrue.png "BreakpointConditionIsTrue")  
  
   No exemplo a seguir, definimos o ponto de interrupção atingido somente quando o valor de `testInt` alterações:  
  
   ![Ponto de interrupção quando alterado](../debugger/media/breakpointwhenchanged.png "BreakpointWhenChanged")  
  
   O comportamento de quando o campo alterado é diferente para diferentes linguagens de programação. Se você escolher **quando alterado** para código nativo, o depurador não considerará a primeira avaliação da condição como uma alteração, portanto, o ponto de interrupção não será atingido na primeira avaliação. Se você escolher **quando alterado** para código gerenciado, o ponto de interrupção será atingido na primeira avaliação depois **quando alterado** está selecionado.  
  
   Se você definir uma condição de ponto de interrupção com sintaxe inválida, uma mensagem de aviso será exibida. Se você especificar uma condição de ponto de interrupção com sintaxe válida mas semântica inválida, uma mensagem de aviso aparecerá na primeira vez em que o ponto de interrupção for atingido. Nos dois casos, o depurador interrompe a execução quando o ponto de interrupção inválido é atingido. O ponto de interrupção é ignorado somente se a condição é válida e avaliada como `false`.  
  
   A condição pode ser qualquer expressão válida que seja reconhecida pelo depurador. Para obter mais informações sobre expressões válidas, consulte [expressões no depurador](../debugger/expressions-in-the-debugger.md).  
  
## <a name="using-object-ids-in-breakpoint-conditions-c-and-f"></a>Usando IDs de objeto em condições de ponto de interrupção (C# e F#)  
 Há vezes quando você deseja observar o comportamento de um objeto específico; Por exemplo, você talvez queira saber por que um objeto foi inserido mais de uma vez em uma coleção. No C# e F#, você pode criar IDs de objeto para instâncias específicas de [tipos de referência](http://msdn.microsoft.com/library/801cf030-6e2d-4a0d-9daf-1431b0c31f47) e usá-los em condições de ponto de interrupção. A ID de objeto é gerada pelo common language runtime (CLR) serviços de depuração e associada ao objeto.  Para criar uma ID de objeto, faça o seguinte:  
  
1. Defina um ponto de interrupção no código de algum tempo depois que o objeto foi criado.  
  
2. Iniciar a depuração e quando a execução é interrompida no ponto de interrupção, localizar o ponto de interrupção a **Locals** , clique duas vezes e selecione **criar ID de objeto**.  
  
    Você deve ver uma **$** além de um número no **locais** janela. Isso é a ID de objeto.  
  
3. Adicione um novo ponto de interrupção condicional no ponto em que você deseja investigar, por exemplo quando o objeto deve ser adicionado à coleção.  
  
4. Use a ID de objeto no campo expressão condicional. Por exemplo, se houver uma variável `item` referindo-se ao objeto a ser adicionado à coleção, você colocaria **item = = $n**, onde **n** é o número de ID de objeto.  
  
    Execução será interrompida no ponto quando esse objeto deve ser adicionado à coleção.  
  
   Se você quiser excluir a ID de objeto mais tarde, você pode clique com botão direito a variável na **Locals** janela e selecione **excluir ID de objeto**.  
  
   Observe que as IDs de objeto criar referências fracas e não impedem que o objeto que está sendo coletado como lixo. Eles só são válidos para a sessão de depuração atual.  
  
## <a name="hit-count"></a>Contagem de acertos  
 Se você suspeitar que um loop em seu código inicia com comportamento inadequado após um determinado número de iterações, você pode definir um ponto de interrupção para interromper a execução após um determinado número de ocorrências para o para a linha de código associada, em vez de ser forçado a repetidamente pressione  **F5** para atingir o nível de iteração.  
  
 No **configurações de ponto de interrupção** janela, defina a condição como **contagem de ocorrências**. Em seguida, você pode especificar o número de iterações. No exemplo a seguir, definimos o ponto de interrupção atingido em cada iteração outra:  
  
 ![Contagem de ocorrências de ponto de interrupção](../debugger/media/breakpointhitcount.png "BreakpointHitCount")  
  
## <a name="filter"></a>Filtro  
 Você pode restringir um ponto de interrupção seja acionado apenas nos dispositivos especificados, ou em threads e processos especificados.  
  
 No **configuração de ponto de interrupção**janela s, defina a condição como **filtro**. Insira um ou mais das seguintes expressões.  
  
- MachineName = "name"  
  
- ProcessId = valor  
  
- ProcessName = "name"  
  
- ThreadId = valor  
  
- ThreadName = "name"  
  
  Coloque os valores de cadeia de caracteres entre aspas duplas. Você pode combinar cláusulas usando `&` (AND), `||` (OR), `!` (NOT) e parênteses.  
  
##  <a name="BKMK_Print_to_the_Output_window_with_tracepoints"></a> Ações de ponto de interrupção e Tracepoints  
 Um tracepoint é um ponto de interrupção que imprime uma mensagem na janela Saída. Um tracepoint pode funcionar como uma declaração de rastreamento temporária na linguagem de programação.  
  
 No **configurações de ponto de interrupção** janela, verifique o **ações** caixa. Escolher **registrar uma mensagem de janela de saída** na **ação** grupo. Você pode imprimir uma cadeia de caracteres genérica, como **este é um teste**. Para incluir o valor de uma variável ou expressão, coloque-as entre chaves.  
  
 Para interromper a execução quando o tracepoint for atingido, desmarque a **continuar a execução** caixa de seleção. Quando **continuar a execução** estiver marcada, não a execução é interrompida. Nos dois casos, a mensagem é impressa.  
  
 Você pode usar as seguintes palavras-chave especial na **mensagem**.  
  
|||  
|-|-|  
|**$ADDRESS**|Instrução atual|  
|**$CALLER**|Nome da função de chamada|  
|**$CALLSTACK**|Pilha de chamadas|  
|**$FUNCTION**|Nome da função atual|  
|**$PID**|Id do processo|  
|**$PNAME**|Nome do processo|  
|**$TID**|Id do thread|  
|**$TNAME**|Nome do thread|  
|**$TICK**||  
|**$TNAME**||  
  
##  <a name="BKMK_Set_a_breakpoint_at_a_function_return_in_the_Call_Stack_window"></a> Rótulos de ponto de interrupção  
 Rótulos de ponto de interrupção são usados somente na **pontos de interrupção** janela para classificar e filtrar a lista de pontos de interrupção. Para adicionar um rótulo a um ponto de interrupção, escolha a linha do ponto de interrupção e, em seguida, escolha **rótulo** no menu de contexto.  
  
## <a name="export-and-import-breakpoints"></a>Pontos de interrupção de importação e exportação  
 Você pode exportar um ponto de interrupção em um arquivo XML clicando duas vezes no ponto de interrupção e selecionando **exportar**. O arquivo é salvo por padrão no diretório da solução. Para importar os pontos de interrupção, abra o **pontos de interrupção** janela (**CTRL + ALT + B**) e na barra de ferramentas, clique na seta que aponta para a direita (a dica de ferramenta é **importar pontos de interrupção de um arquivo**) .  
  
## <a name="troubleshoot-breakpoints"></a>Solucionar problemas de pontos de interrupção  
  
### <a name="i-deleted-a-breakpoint-but-i-continue-to-hit-it-when-i-start-debugging-again"></a>Exclui um ponto de interrupção, mas continuar a ele durante a iniciar a depuração novamente  
 Se você excluir um ponto de interrupção durante a depuração, em alguns casos você pode atingir o ponto de interrupção novamente na próxima vez que você iniciar a depuração. Para interromper a atingir esse ponto de interrupção, verifique se todas as instâncias do ponto de interrupção são removidas do **pontos de interrupção** janela.  
  
### <a name="the-debugger-cant-locate-the-correct-version-of-the-source-file-for-a-breakpoint"></a>O depurador não pode localizar a versão correta do arquivo de origem de um ponto de interrupção  
 Se um arquivo de origem tiver sido alterado e se a fonte não corresponder mais ao código que você estiver depurando, o depurador poderá localizar o arquivo de origem que corresponda a um ponto de interrupção, mesmo se o arquivo de origem existir.  
  
1.  Se você quiser que o Visual Studio para exibir o código-fonte que não corresponde à versão você está depurando, escolha **depurar / opções e configurações**. Sobre o **depuração/geral** página, desmarque a **exigem arquivos de origem que correspondam exatamente à versão original** opção.  
  
2.  Você também pode associar o ponto de interrupção ao arquivo de origem. Selecione o ponto de interrupção e escolha **condições** no menu de contexto. Verifique **permitir que o código-fonte seja diferente da original** na **configurações de ponto de interrupção** janela.  
  
### <a name="breakpoints-dont-work-in-a-dll"></a>Os pontos de interrupção não funcionam em uma DLL  
 Você não pode definir um ponto de interrupção em um arquivo de origem quando o depurador não carregou informações de depuração do módulo no qual o código está localizado. Os sintomas podem incluir mensagens, como **não será possível definir o ponto de interrupção**. O glifo de ponto de interrupção Aviso aparece no local do ponto de interrupção. No entanto, esses pontos de interrupção de Aviso tornam-se pontos de interrupção reais quando o código é carregado. Para obter mais informações sobre o carregamento de símbolos, consulte [especificar arquivos de símbolo (. PDB) e código-fonte](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md).  
  
## <a name="see-also"></a>Consulte também  
 [Navegar pelo Código com o Depurador](../debugger/navigating-through-code-with-the-debugger.md)



