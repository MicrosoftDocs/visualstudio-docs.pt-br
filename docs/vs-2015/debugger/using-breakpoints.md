---
title: Usando pontos de interrupção | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
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
manager: jillfra
ms.openlocfilehash: bbe2ecf89f94cc75ff9036285ae9acbf9cf3b657
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85534492"
---
# <a name="using-breakpoints"></a>Usando pontos de interrupção
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]
Você pode definir pontos de interrupção quando quiser parar a execução do depurador, talvez para ver o estado das variáveis de código ou para examinar a pilha de chamadas. Elas são uma das técnicas de depuração mais importantes na caixa de ferramentas de um desenvolvedor.
  
## <a name="setting-a-function-breakpoint-in-source-code"></a><a name="BKMK_Overview"></a>Definindo um ponto de interrupção de função no código-fonte  
 Você define um ponto de interrupção de função no código-fonte clicando na margem esquerda de um arquivo de código-fonte ou colocando o cursor em uma linha de código e pressionando F9. O ponto de interrupção aparece como vermelho na margem esquerda e a linha de código também é colorida:  
  
 ![Definir um ponto de interrupção](../debugger/media/basicbreakpoint.png "BasicBreakpoint")  
  
 Quando você executa esse código no depurador, a execução é interrompida sempre que o ponto de interrupção é atingido, antes que o código nessa linha seja executado. A linha de código-fonte é amarela colorida:  
  
 ![Execução de ponto de interrupção interrompida](../debugger/media/breakpointexecution.png "BreakpointExecution")  
  
 Neste ponto, o valor de `testInt` é ainda 1.  
  
 Você pode examinar o estado atual do aplicativo, incluindo valores de variáveis e a pilha de chamadas. Para obter mais informações sobre a pilha de chamadas, consulte [como: usar a janela pilha de chamadas](../debugger/how-to-use-the-call-stack-window.md).  
  
 Você pode definir um ponto de interrupção em qualquer linha de código executável. Por exemplo, no código C# acima, você pode definir um ponto de interrupção na declaração da variável, no `for` loop ou em qualquer código dentro do `for` loop, mas não pode definir um ponto de interrupção no namespace ou nas declarações de classe ou na assinatura do método.  
  
## <a name="setting-other-kinds-of-breakpoints"></a><a name="BKMK_Set_a_breakpoint_in_a_source_file"></a>Definindo outros tipos de pontos de interrupção  
 Você também pode definir pontos de interrupção na pilha de chamadas, na janela de desmontagem e, no código C++ nativo, em uma condição de dados ou em um endereço de memória.  
  
## <a name="setting-a-breakpoint-in-the-call-stack-window"></a><a name="BKMK_Set_a_breakpoint_in_the_call_stack_window"></a>Configurando um ponto de interrupção na janela pilha de chamadas  
 Você pode interromper a execução na instrução ou na linha que uma função de chamada retorna ao definindo um ponto de interrupção na janela **pilha de chamadas** . Para obter mais informações sobre a pilha de chamadas, consulte [como: usar a janela pilha de chamadas](../debugger/how-to-use-the-call-stack-window.md). O depurador deve ter parado de ser executado.  
  
1. Inicie a depuração do aplicativo e aguarde a execução ser interrompida (por exemplo, em um ponto de interrupção). Abra a janela **pilha de chamadas** (**depuração/Windows/pilha de chamadas**ou **Ctrl + Alt + C**).  
  
2. Clique com o botão direito do mouse na função de chamada e selecione ponto de interrupção **/Inserir ponto de quebra**ou use apenas a tecla de atalho **F9**.  
  
3. Um símbolo de ponto de interrupção aparece na margem esquerda da pilha de chamadas, ao lado do nome da chamada de função.  
  
   Na janela **pontos de interrupção** , o ponto de interrupção de pilha de chamadas aparece como um endereço com um local de memória que corresponde à próxima instrução executável na função. O depurador interrompe a execução na instrução.  
  
   Para rastrear visualmente pontos de interrupção durante a execução do código, consulte [mapear métodos na pilha de chamadas durante a depuração](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md).  
  
## <a name="setting-a-breakpoint-in-the-disassembly-window"></a>Definindo um ponto de interrupção na janela de desmontagem  
 Para definir um ponto de interrupção em uma instrução de assembly, o depurador deve estar no modo de interrupção.  
  
1. Inicie a depuração do aplicativo e aguarde a execução ser interrompida (por exemplo, em um ponto de interrupção). Abra a janela de **desmontagem** (**debug/Windows/Disassembly**ou **Ctrl + Alt + D**).  
  
2. Clique na margem esquerda na instrução que você deseja interromper ou defina o cursor na instrução e pressione **F9**.  
  
## <a name="setting-a-data-breakpoint-native-c-only"></a><a name="BKMK_set_a_data_breakpoint_native_cplusplus_only"></a>Definindo um ponto de interrupção de dados (somente C++ nativo)  
 Os pontos de interrupção de dados interrompem a execução quando um valor armazenado em um endereço de memória especificado é alterado. Se o valor for lido, mas não for alterado, a execução não será interrompida. Para definir pontos de interrupção de dados, o depurador deve estar em modo de interrupção.  
  
1. Inicie a depuração do aplicativo e aguarde até que um ponto de interrupção seja atingido. No menu **depurar** , clique em novo ponto de interrupção **/pontos de interrupção de dados** (ou abra a janela **pontos** de interrupção e escolha **novo/ponto de interrupção de dados**.  
  
2. Na caixa **endereço** , digite um endereço de memória ou uma expressão que seja avaliada como um endereço de memória. Por exemplo, digite `&avar` para quebrar quando o conteúdo da variável `avar` for alterado.  
  
3. Na lista suspensa **contagem de bytes** , selecione o número de bytes que você deseja que o depurador Assista. Por exemplo, se você selecionar **4**, o depurador observará os quatro bytes Iniciando em `&avar` e interromperá se qualquer um desses bytes alterar o valor.  
  
   Tenha em mente que os pontos de interrupção de dados dependem da aplicabilidade de endereços de memória específicos.  
  
- O endereço de uma variável é alterado de uma sessão de depuração para a próxima. Os pontos de interrupção de dados são automaticamente desabilitados no final de cada sessão de depuração.  
  
- Se você definir um ponto de interrupção de dados em uma variável local, o ponto de interrupção permanecerá habilitado quando a função terminar, mas o endereço de memória não será mais aplicável e o comportamento do ponto de interrupção será imprevisível. Se você definir um ponto de interrupção de dados em uma variável local, deverá remover ou desabilitar o ponto de interrupção antes que a função termine.  
  
  Pontos de interrupção não funcionam nestas condições:  
  
- Um processo que não está sendo depurado grava no local da memória  
  
- O local da memória é compartilhado entre dois ou mais processos  
  
- O local da memória é atualizado no kernel. Por exemplo, se a memória for passada para a função do Windows de 32 bits `ReadFile` , a memória será atualizada do modo kernel e o depurador não interromperá a gravação da memória.  
  
## <a name="setting-a-breakpoint-with-a-memory-address-native-c-only"></a>Configurando um ponto de interrupção com um endereço de memória (somente C++ nativo)  
 Você também pode usar o endereço de um objeto para definir um ponto de interrupção em um método chamado em uma instância específica de uma classe.  Aqui está um exemplo:  
  
 Por exemplo, dado um objeto do tipo `my_class` com o endereço, você pode definir um ponto de interrupção de função em um método chamado `my_method` por essa instância.  
  
1. Defina um ponto de interrupção em algum lugar depois que a instância da classe for instanciada.  
  
2. Localize o endereço da instância (vamos dizer que é `0xcccccccc` ).  
  
3. Clique no **ponto de interrupção de depuração/novo** ponto de interrupção/função (ou **ALT + F9, B**).  
  
4. Adicione o seguinte texto à caixa **nome da função** :  
  
    ```cpp  
    ((my_class *) 0xcccccccc)->my_method  
    ```  
  
## <a name="managing-breakpoints"></a><a name="BKMK_Specify_advanced_properties_of_a_breakpoint_"></a>Gerenciando pontos de interrupção  
 Você pode usar a janela **pontos de interrupção** (**depurar/Windows/pontos de interrupção**ou **Ctrl + Alt + B**) para ver todos os pontos de interrupção que você definiu em sua solução:  
  
 ![Janela pontos de interrupção](../debugger/media/breakpointswindow.png "BreakpointsWindow")  
  
 A janela **pontos de interrupção** oferece um local central para gerenciar todos os seus pontos de interrupção, o que pode ser especialmente útil em uma solução grande ou em um cenário de depuração complexo em que os pontos de interrupção são críticos. Se você precisar salvar ou compartilhar o estado e o local de um conjunto de pontos de interrupção, poderá exportar e importar pontos de interrupção somente da janela **pontos de interrupção** .  
  
## <a name="advanced-breakpoints"></a><a name="BKMK_Specify_a_breakpoint_condition_using_a_code_expression"></a>Pontos de interrupção avançados  
  
## <a name="breakpoint-conditions"></a>Condições de ponto de interrupção  
 Você pode controlar quando e onde um ponto de interrupção é executado definindo condições.  
  
1. Clique com o botão direito do mouse no ponto de interrupção ou focalize o ponto de interrupção e escolha o ícone de configurações.  
  
2. No menu de contexto, selecione **condições**. Isso abre a janela **configurações de ponto de interrupção** :  
  
   ![Configurações de ponto de interrupção](../debugger/media/breakpointsettings.png "BreakpointSettings")  
  
   Quando você marca a caixa **condições** , a janela se expande para mostrar os diferentes tipos de condições.  
  
   **Expressão condicional:** Ao selecionar a expressão condicional, você pode escolher duas condições: **é verdadeiro** e **quando alterado**. Escolha **será verdadeiro** se você quiser interromper quando a expressão for satisfeita ou se quiser se desmembrar quando o valor da expressão tiver **sido alterado.**  
  
   No exemplo a seguir, definimos o ponto de interrupção para atingir somente quando o valor de `testInt` for **4**:  
  
   ![A condição de ponto de interrupção é verdadeira](../debugger/media/breakpointconditionistrue.png "BreakpointConditionIsTrue")  
  
   No exemplo a seguir, definimos o ponto de interrupção para atingir somente quando o valor de `testInt` for alterado:  
  
   ![Ponto de interrupção quando alterado](../debugger/media/breakpointwhenchanged.png "BreakpointWhenChanged")  
  
   O comportamento do campo quando alterado é diferente para linguagens de programação diferentes. Se você escolher **quando alterado** para código nativo, o depurador não considerará a primeira avaliação da condição para ser uma alteração, portanto, o ponto de interrupção não será atingido na primeira avaliação. Se você escolher **quando alterado** para código gerenciado, o ponto de interrupção será atingido na primeira avaliação depois **que a alteração** for selecionada.  
  
   Se você definir uma condição de ponto de interrupção com sintaxe inválida, uma mensagem de aviso será exibida. Se você especificar uma condição de ponto de interrupção com sintaxe válida mas semântica inválida, uma mensagem de aviso aparecerá na primeira vez em que o ponto de interrupção for atingido. Em qualquer um dos casos, o depurador interromperá a execução quando o ponto de interrupção inválido for atingido. O ponto de interrupção será ignorado somente se a condição for válida e for avaliada como `false` .  
  
   A condição pode ser qualquer expressão válida que seja reconhecida pelo depurador. Para obter mais informações sobre expressões válidas, consulte [expressões no depurador](../debugger/expressions-in-the-debugger.md).  
  
## <a name="using-object-ids-in-breakpoint-conditions-c-and-f"></a>Usando IDs de objeto em condições de ponto de interrupção (C# e F #)  
 Há ocasiões em que você deseja observar o comportamento de um objeto específico; por exemplo, talvez você queira descobrir por que um objeto foi inserido mais de uma vez em uma coleção. Em C# e F #, você pode criar IDs de objeto para instâncias específicas de [tipos de referência](https://msdn.microsoft.com/library/801cf030-6e2d-4a0d-9daf-1431b0c31f47) e usá-las em condições de ponto de interrupção. A ID de objeto é gerada pelos serviços de depuração de Common Language Runtime (CLR) e associada ao objeto.  Para criar uma ID de objeto, faça o seguinte:  
  
1. Defina um ponto de interrupção no código uma vez após o objeto ter sido criado.  
  
2. Inicie a depuração e quando a execução for interrompida no ponto de interrupção, localize o ponto de interrupção na janela **locais** , clique com o botão direito do mouse nele e selecione **criar ID de objeto**.  
  
    Você deve ver **$** mais um número na janela **locais** . Esta é a ID do objeto.  
  
3. Adicione um novo ponto de interrupção condicional no momento que você deseja investigar, por exemplo, quando o objeto deve ser adicionado à coleção.  
  
4. Use a ID de objeto no campo expressão condicional. Por exemplo, se houver uma variável `item` referente ao objeto a ser adicionado à coleção, você colocará **Item = = $n**, em que **n** é o número de ID de objeto.  
  
    A execução será interrompida no ponto em que o objeto deve ser adicionado à coleção.  
  
   Se posteriormente você quiser excluir a ID de objeto, poderá clicar com o botão direito do mouse na variável na janela **locais** e selecionar **excluir ID de objeto**.  
  
   Observe que as IDs de objeto criam referências fracas e não impedem que o objeto seja coletado como lixo. Eles são válidos somente para a sessão de depuração atual.  
  
## <a name="hit-count"></a>Contagem de Ocorrências  
 Se você suspeitar que um loop em seu código inicia o comportamento inadequado após um determinado número de iterações, você pode definir um ponto de interrupção para interromper a execução após um número especificado de ocorrências para a linha de código associada, em vez de ser forçado a pressionar **F5** repetidamente para alcançar o nível de iteração.  
  
 Na janela **configurações de ponto de interrupção** , defina a condição como **contagem de acesso**. Em seguida, você pode especificar o número de iterações. No exemplo a seguir, definimos o ponto de interrupção para atingir todas as outras iterações:  
  
 ![Contagem de acesso de ponto de interrupção](../debugger/media/breakpointhitcount.png "BreakpointHitCount")  
  
## <a name="filter"></a>Filtrar  
 Você pode restringir um ponto de interrupção para disparar somente em dispositivos especificados ou em processos e threads especificados.  
  
 Na janela **configurações do ponto de interrupção**, defina a condição a ser **filtrada**. Insira uma ou mais das expressões a seguir.  
  
- MachineName = "nome"  
  
- ProcessId = valor  
  
- ProcessName = "nome"  
  
- ThreadId = valor  
  
- ThreadName = "nome"  
  
  Coloque os valores da cadeia de caracteres entre aspas duplas. Você pode combinar cláusulas usando `&` (and), `||` (or), `!` (não) e parênteses.  
  
## <a name="breakpoint-actions-and-tracepoints"></a><a name="BKMK_Print_to_the_Output_window_with_tracepoints"></a>Ações de ponto de interrupção e tracepoints  
 Um tracepoint é um ponto de interrupção que imprime uma mensagem na janela de Saída. Um tracepoint pode funcionar como uma declaração de rastreamento temporária na linguagem de programação.  
  
 Na janela **configurações de ponto de interrupção** , marque a caixa **ações** . Escolha **registrar uma mensagem na janela de saída** no grupo de **ações** . Você pode imprimir uma cadeia de caracteres genérica, como **este é um teste**. Para incluir o valor de uma variável ou expressão, coloque-a entre chaves.  
  
 Para interromper a execução quando o tracepoint for atingido, desmarque a caixa de seleção **continuar execução** . Quando **continuar a execução** estiver marcada, a execução não será interrompida. Nos dois casos, a mensagem é impressa.  
  
 Você pode usar as palavras-chave especiais a seguir na **mensagem**.  
  
|Palavra-chave|Descrição|  
|-|-|  
|**$ADDRESS**|Instrução atual|  
|**$CALLER**|Nome da função de chamada|  
|**$CALLSTACK**|Pilha de chamadas|  
|**$FUNCTION**|Nome da função atual|  
|**$PID**|ID do processo|  
|**$PNAME**|Nome do processo|  
|**$TID**|id do thread|  
|**$TNAME**|Nome do thread|  
|**$TICK**||  
|**$TNAME**||  
  
## <a name="breakpoint-labels"></a><a name="BKMK_Set_a_breakpoint_at_a_function_return_in_the_Call_Stack_window"></a>Rótulos de ponto de interrupção  
 Os rótulos de ponto de interrupção são usados somente na janela **pontos de interrupção** para classificar e filtrar a lista de pontos de interrupção. Para adicionar um rótulo a um ponto de interrupção, escolha a linha do ponto de interrupção e, em seguida, escolha **rótulo** no menu de contexto.  
  
## <a name="export-and-import-breakpoints"></a>Exportar e importar pontos de interrupção  
 Você pode exportar um ponto de interrupção para um arquivo XML clicando com o botão direito do mouse no ponto de interrupção e selecionando **Exportar**. O arquivo é salvo por padrão no diretório da solução. Para importar pontos de interrupção, abra a janela **pontos de interrupção** (**Ctrl + Alt + B**) e, na barra de ferramentas, clique na seta apontando para a direita (a dica de ferramenta é **importar pontos de interrupção de um arquivo**).  
  
## <a name="troubleshoot-breakpoints"></a>Solucionar problemas de pontos de interrupção  
  
### <a name="i-deleted-a-breakpoint-but-i-continue-to-hit-it-when-i-start-debugging-again"></a>Excluí um ponto de interrupção, mas continue a clicar quando eu iniciar a depuração novamente  
 Se você excluiu um ponto de interrupção durante a depuração, em alguns casos, você pode atingir o ponto de interrupção novamente na próxima vez que iniciar a depuração. Para parar de atingir esse ponto de interrupção, verifique se todas as instâncias do ponto de interrupção foram removidas da janela **pontos de interrupção** .  
  
### <a name="the-debugger-cant-locate-the-correct-version-of-the-source-file-for-a-breakpoint"></a>O depurador não pode localizar a versão correta do arquivo de origem de um ponto de interrupção  
 Se um arquivo de origem tiver sido alterado e se a fonte não corresponder mais ao código que você estiver depurando, o depurador poderá localizar o arquivo de origem que corresponda a um ponto de interrupção, mesmo se o arquivo de origem existir.  
  
1. Se você quiser que o Visual Studio exiba o código-fonte que não corresponde à versão que você está Depurando, escolha **depurar/opções e configurações**. Na página **depuração/geral** , desmarque a opção **exigir arquivos de origem que correspondem exatamente à versão original** .  
  
2. Você também pode associar o ponto de interrupção ao arquivo de origem. Selecione o ponto de interrupção e escolha **condições** no menu de contexto. Marque **permitir que o código-fonte seja diferente do original** na janela **configurações de ponto de interrupção** .  
  
### <a name="breakpoints-dont-work-in-a-dll"></a>Os pontos de interrupção não funcionam em uma DLL  
 Você não pode definir um ponto de interrupção em um arquivo de origem quando o depurador não carregou informações de depuração do módulo no qual o código está localizado. Os sintomas podem incluir mensagens como **o ponto de interrupção não serão definidos**. O glifo de ponto de interrupção Aviso aparece no local do ponto de interrupção. No entanto, esses pontos de interrupção de Aviso tornam-se pontos de interrupção reais quando o código é carregado. Para obter mais informações sobre como carregar símbolos, consulte [especificar símbolo (. pdb) e arquivos de origem](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Navegar pelo Código com o Depurador](../debugger/navigating-through-code-with-the-debugger.md)
