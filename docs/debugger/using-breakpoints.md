---
title: Usar pontos de interrupção no depurador | Microsoft Docs
ms.custom: ''
ms.date: 06/30/2020
ms.topic: how-to
f1_keywords:
- vs.debug.breakpointswin
- vs.debug.disassembly.insert
- vs.debug.sourcewin.edit
- vs.debug.file
- vs.debug.breakpt.new
- vs.debug.whenbreakpointishit
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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 57b2ea6a0c69387043057bc07957a757ed351f99
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85769404"
---
# <a name="use-breakpoints-in-the-visual-studio-debugger"></a>Usar pontos de interrupção no depurador do Visual Studio

Os pontos de interrupção são uma das técnicas de depuração mais importantes na caixa de ferramentas do desenvolvedor. Você define pontos de interrupção onde quiser pausar a execução do depurador. Por exemplo, talvez você queira ver o estado das variáveis de código ou examinar a pilha de chamadas em um determinado ponto de interrupção.  Se você estiver tentando resolver um aviso ou problema ao usar pontos de interrupção, consulte [solucionar problemas de pontos de interrupção no depurador do Visual Studio](../debugger/troubleshooting-breakpoints.md).

> [!NOTE]
> Se você souber a tarefa ou o problema que está tentando resolver, mas precisar saber qual tipo de ponto de interrupção usar, consulte [localizar sua tarefa de depuração](../debugger/find-your-debugging-task.md#pause-running-code).

## <a name="set-breakpoints-in-source-code"></a><a name="BKMK_Overview"></a>Definir pontos de interrupção no código-fonte

Você pode definir um ponto de interrupção em qualquer linha de código executável. Por exemplo, no código C# a seguir, você pode definir um ponto de interrupção na linha de código com a atribuição de variável ( `int testInt = 1` ), o `for` loop ou qualquer código dentro do `for` loop. Você não pode definir um ponto de interrupção em assinaturas de método, declarações para um namespace ou classe, ou declarações de variável, se não houver nenhuma atribuição e nenhum getter/setter.

Para definir um ponto de interrupção no código-fonte, clique na margem da extrema esquerda ao lado de uma linha de código. Você também pode selecionar a linha e pressionar **F9**, selecionar **Debug**  >  **ponto de interrupção de alternância**de depuração, ou clicar com o botão direito do mouse e selecionar **ponto de**interrupção  >  **Inserir ponto**de interrupção. O ponto de interrupção aparece como vermelho na margem esquerda.

Para a maioria das linguagens, incluindo C#, pontos de interrupção e linhas de execução atuais são realçados automaticamente. Para o código C++, você pode ativar o realce do ponto de interrupção e das linhas atuais selecionando **ferramentas** (ou **depurar**) > **Opções**de  >  **depuração**  >   **realçar toda a linha de origem para pontos de interrupção e a instrução atual (somente C++)**.

![Definir um ponto de interrupção](../debugger/media/basicbreakpoint.png "Ponto de interrupção básico")

Quando você depura, a execução pausa no ponto de interrupção, antes que o código nessa linha seja executado. O símbolo de ponto de interrupção mostra uma seta amarela.

No ponto de interrupção no exemplo a seguir, o valor de `testInt` é ainda 1. Portanto, o valor não foi alterado desde que a variável foi inicializada (definida como um valor de 1) porque a instrução em amarelo ainda não foi executada.

![Execução de ponto de interrupção interrompida](../debugger/media/breakpointexecution.png "Execução de ponto de interrupção")

Quando o depurador para o ponto de interrupção, você pode examinar o estado atual do aplicativo, incluindo [valores de variáveis](../debugger/debugger-feature-tour.md#inspect-variables-with-data-tips) e a [pilha de chamadas](../debugger/how-to-use-the-call-stack-window.md).

Aqui estão algumas instruções gerais para trabalhar com pontos de interrupção.

- O ponto de interrupção é uma alternância. Você pode clicar nele, pressionar **F9**ou usar o **Debug**  >  **ponto de interrupção de alternância** de depuração para excluí-lo ou reinseri-lo.

- Para desabilitar um ponto de interrupção sem excluí-lo, focalize ou clique com o botão direito do mouse nele e selecione **desabilitar ponto de interrupção**. Os pontos de interrupção desabilitados aparecem como pontos vazios na margem esquerda ou na janela **pontos de interrupção** . Para reabilitar um ponto de interrupção, focalize ou clique com o botão direito do mouse nele e selecione **habilitar ponto de interrupção**.

- Defina condições e ações, adicione e edite rótulos ou exporte um ponto de interrupção clicando com o botão direito do mouse nele e selecionando o comando apropriado, ou passando o cursor sobre ele e selecionando o ícone de **configurações** .

## <a name="breakpoint-actions-and-tracepoints"></a><a name="BKMK_Print_to_the_Output_window_with_tracepoints"></a>Ações de ponto de interrupção e tracepoints

Um *tracepoint* é um ponto de interrupção que imprime uma mensagem na janela de **Saída**. Um tracepoint pode agir como uma instrução de rastreamento temporária na linguagem de programação e não pausa a execução do código. Você cria um tracepoint definindo uma ação especial na janela **configurações de ponto de interrupção** . Para obter instruções detalhadas, consulte [usar tracepoints no depurador do Visual Studio](../debugger/using-tracepoints.md).

## <a name="breakpoint-conditions"></a>Condições de ponto de interrupção

Você pode controlar quando e onde um ponto de interrupção é executado definindo condições. A condição pode ser qualquer expressão válida que o depurador reconheça. Para obter mais informações sobre expressões válidas, confira [Expressões no depurador](../debugger/expressions-in-the-debugger.md).

**Para definir uma condição de ponto de interrupção:**

1. Clique com o botão direito do mouse no símbolo do ponto de interrupção e selecione **condições**. Ou passe o mouse sobre o símbolo de ponto de interrupção, selecione o ícone **configurações** e, em seguida, selecione **condições** na janela **configurações de ponto de interrupção** .

   Você também pode definir condições na janela **pontos de interrupção** clicando com o botão direito do mouse em um ponto de interrupção e selecionando **configurações**e, em seguida, selecionando **condições**.

   ![Configurações de ponto de interrupção](../debugger/media/breakpointsettings.png "BreakpointSettings")

2. Na lista suspensa, selecione **expressão condicional**, **contagem de acesso**ou **filtro**e defina o valor de acordo.

3. Selecione **fechar** ou pressione **Ctrl** + **Enter** para fechar a janela **configurações de ponto de interrupção** . Ou, na janela **pontos de interrupção** , selecione **OK** para fechar a caixa de diálogo.

Os pontos de interrupção com condições definidas aparecem com um **+** símbolo nas janelas código-fonte e **pontos de interrupção** .

<a name="BKMK_Specify_a_breakpoint_condition_using_a_code_expression"></a>
### <a name="create-a-conditional-expression"></a>Criar uma expressão condicional

Quando você seleciona **expressão condicional**, pode escolher entre duas condições: **é verdadeiro** ou **quando alterado**. Escolha **é true** para quebrar quando a expressão for satisfeita ou **quando for alterada** para quebra quando o valor da expressão for alterado.

No exemplo a seguir, o ponto de interrupção é atingido somente quando o valor de `testInt` é **4**:

![A condição de ponto de interrupção é verdadeira](../debugger/media/breakpointconditionistrue.png "Ponto de interrupção é verdadeiro")

No exemplo a seguir, o ponto de interrupção é atingido somente quando o valor de é `testInt` alterado:

![Ponto de interrupção quando alterado](../debugger/media/breakpointwhenchanged.png "Ponto de interrupção quando alterado")

Se você definir uma condição de ponto de interrupção com sintaxe inválida, uma mensagem de aviso será exibida. Se você especificar uma condição de ponto de interrupção com sintaxe válida mas semântica inválida, uma mensagem de aviso aparecerá na primeira vez em que o ponto de interrupção for atingido. Em ambos os casos, o depurador é interrompido quando atinge o ponto de interrupção inválido. O ponto de interrupção será ignorado somente se a condição for válida e for avaliada como `false` .

>[!NOTE]
>O comportamento do campo **quando alterado** é diferente para linguagens de programação diferentes.
>- Para código nativo, o depurador não considera a primeira avaliação da condição como uma alteração, portanto, não atinge o ponto de interrupção na primeira avaliação.
>- Para código gerenciado, o depurador atinge o ponto de interrupção na primeira avaliação depois **que a alteração** é selecionada.

<a name="using-object-ids-in-breakpoint-conditions-c-and-f"></a>
### <a name="use-object-ids-in-conditional-expressions-c-and-f-only"></a>Usar IDs de objeto em expressões condicionais (somente C# e F #)

 Há ocasiões em que você deseja observar o comportamento de um objeto específico. Por exemplo, talvez você queira descobrir por que um objeto foi inserido em uma coleção mais de uma vez. Em C# e F #, você pode criar IDs de objeto para instâncias específicas de [tipos de referência](/dotnet/csharp/language-reference/keywords/reference-types)e usá-las em condições de ponto de interrupção. A ID de objeto é gerada pelos serviços de depuração de Common Language Runtime (CLR) e associada ao objeto.

**Para criar uma ID de objeto:**

1. Defina um ponto de interrupção no código em algum lugar depois que o objeto tiver sido criado.

2. Inicie a depuração e, quando a execução pausa no ponto de interrupção, selecione **depurar**  >  **Windows**  >  **locais** do Windows ou **ALT** + **4** para abrir a janela **locais** .

   Localize a instância de objeto específica na janela **locais** , clique com o botão direito do mouse nela e selecione **criar ID de objeto**.

   Você deve ver **$** mais um número na janela **locais** . Esta é a ID do objeto.

3. Adicione um novo ponto de interrupção no momento que você deseja investigar; por exemplo, quando o objeto deve ser adicionado à coleção. Clique com o botão direito do mouse no ponto de interrupção e selecione **Condições**.

4. Use a ID de objeto no campo **expressão condicional** . Por exemplo, se a variável `item` for o objeto a ser adicionado à coleção, selecione **é verdadeiro** e digite **item = = $ \<n> **, em que \<n> é o número de ID de objeto.

   A execução será interrompida no ponto em que o objeto deve ser adicionado à coleção.

   Para excluir a ID de objeto, clique com o botão direito do mouse na variável na janela **locais** e selecione **excluir ID de objeto**.

> [!NOTE]
> As IDs de objeto criam referências fracas e não impedem que o objeto seja coletado como lixo. Eles são válidos somente para a sessão de depuração atual.

### <a name="set-a-hit-count-condition"></a>Definir uma condição de contagem de acesso

Se você suspeitar que um loop em seu código inicia o comportamento inadequado após um determinado número de iterações, você pode definir um ponto de interrupção para parar a execução após esse número de ocorrências, em vez de ter que pressionar **F5** repetidamente para alcançar essa iteração.

Em **condições** na janela **configurações de ponto de interrupção** , selecione **contagem de acesso**e, em seguida, especifique o número de iterações. No exemplo a seguir, o ponto de interrupção é definido para atingir todas as outras iterações:

![Contagem de acesso de ponto de interrupção](../debugger/media/breakpointhitcount.png "BreakpointHitCount")

### <a name="set-a-filter-condition"></a>Definir uma condição de filtro

Você pode restringir um ponto de interrupção para disparar somente em dispositivos especificados ou em processos e threads especificados.

Em **condições** na janela **configurações de ponto de interrupção** , selecione **Filtrar**e, em seguida, insira uma ou mais das seguintes expressões:

- MachineName = "nome"
- ProcessId = valor
- ProcessName = "nome"
- ThreadId = valor
- ThreadName = "nome"

Coloque os valores da cadeia de caracteres entre aspas duplas. Você pode combinar cláusulas usando `&` (and), `||` (or), `!` (não) e parênteses.

## <a name="set-function-breakpoints"></a><a name="BKMK_Set_a_breakpoint_in_a_source_file"></a>Definir pontos de interrupção de função

Você pode interromper a execução quando uma função é chamada. Isso é útil, por exemplo, quando você sabe o nome da função, mas não sua localização. Ele também será útil se você tiver funções com o mesmo nome e quiser interromper todas elas (como funções ou funções sobrecarregadas em projetos diferentes).

**Para definir um ponto de interrupção de função:**

1. Selecione **depurar**  >  **novo**ponto de interrupção da  >  **função**de ponto de interrupção ou pressione **ALT** + **F9**  >  **Ctrl** + **B**.

   Você também pode selecionar **novo**  >  **ponto de interrupção de função** na janela **pontos de interrupção** .

1. No diálogo **novo ponto de interrupção de função** , digite o nome da função na caixa **nome da função** .

   Para restringir a especificação de função:

   - Use o nome da função totalmente qualificada.

     Exemplo: `Namespace1.ClassX.MethodA()`

   - Adicione os tipos de parâmetro de uma função sobrecarregada.

     Exemplo: `MethodA(int, string)`

   - Use o símbolo '! ' para especificar o módulo.

     Exemplo: `App1.dll!MethodA`

   - Use o operador de contexto em C++ nativo.

     `{function, , [module]} [+<line offset from start of method>]`

     Exemplo: `{MethodA, , App1.dll}+2`

1. Na lista suspensa **idioma** , escolha o idioma da função.

1. Selecione **OK**.

### <a name="set-a-function-breakpoint-using-a-memory-address-native-c-only"></a>Definir um ponto de interrupção de função usando um endereço de memória (somente C++ nativo)
 Você pode usar o endereço de um objeto para definir um ponto de interrupção de função em um método chamado por uma instância específica de uma classe.  Por exemplo, dado um objeto endereçável do tipo `my_class` , você pode definir um ponto de interrupção de função no `my_method` método que a instância chama.

1. Defina um ponto de interrupção em algum lugar depois que a instância da classe for instanciada.

2. Localize o endereço da instância (por exemplo, `0xcccccccc` ).

3. Selecione **depurar**  >  **novo**ponto de interrupção da  >  **função**de ponto de interrupção ou pressione **ALT** + **F9**  >  **Ctrl** + **B**.

4. Adicione o seguinte à caixa **nome da função** e selecione linguagem **C++** .

   ```cpp
   ((my_class *) 0xcccccccc)->my_method
   ```

::: moniker range=">= vs-2019"

## <a name="set-data-breakpoints-net-core-30-or-higher"></a><a name="BKMK_set_a_data_breakpoint_managed"></a>Definir pontos de interrupção de dados (.NET Core 3,0 ou superior)

Os pontos de interrupção de dados interrompem a execução quando uma propriedade de um objeto específico é alterada.

**Para definir um ponto de interrupção de dados**

1. Em um projeto do .NET Core, inicie a depuração e aguarde até que um ponto de interrupção seja atingido.

2. Na janela **automáticos**, **inspecionar**ou **locais** , clique com o botão direito do mouse em uma propriedade e selecione **interromper quando o valor for alterado** no menu de contexto.

    ![Ponto de interrupção de dados gerenciados](../debugger/media/managed-data-breakpoint.png "Ponto de interrupção de dados gerenciados")

Os pontos de interrupção de dados no .NET Core não funcionarão para:

- Propriedades que não são expansíveis na dica de ferramenta, locais, automáticos ou janela Inspeção
- Variáveis estáticas
- Classes com o atributo DebuggerTypeProxy
- Campos dentro de structs

::: moniker-end

## <a name="set-data-breakpoints-native-c-only"></a><a name="BKMK_set_a_data_breakpoint_native_cplusplus"></a>Definir pontos de interrupção de dados (somente C++ nativo)

 Os pontos de interrupção de dados interrompem a execução quando um valor armazenado em um endereço de memória especificado é alterado. Se o valor for lido, mas não for alterado, a execução não será interrompida.

**Para definir um ponto de interrupção de dados:**

1. Em um projeto C++, inicie a depuração e aguarde até que um ponto de interrupção seja atingido. No menu **depurar** , escolha **novo**ponto de interrupção de ponto de interrupção de  >  **dados**

    Você também pode selecionar **novo**  >  **ponto de interrupção de dados** na janela **pontos de interrupção** ou clicar com o botão direito do mouse em um item na janela **automáticos**, **inspecionar**ou **locais** e selecionar **interromper quando o valor for alterado** no menu de contexto.

2. Na caixa **endereço** , digite um endereço de memória ou uma expressão que seja avaliada como um endereço de memória. Por exemplo, digite `&avar` para quebrar quando o conteúdo da variável `avar` for alterado.

3. Na lista suspensa **contagem de bytes** , selecione o número de bytes que você deseja que o depurador Assista. Por exemplo, se você selecionar **4**, o depurador observará os quatro bytes Iniciando em `&avar` e interromperá se qualquer um desses bytes alterar o valor.

Os pontos de interrupção de dados não funcionam sob as seguintes condições:
- Um processo que não estiver sendo depurado grava na localização da memória.
- A localização de memória é compartilhada entre dois ou mais processos.
- O local da memória é atualizado no kernel. Por exemplo, se a memória for passada para a função do Windows de 32 bits `ReadFile` , a memória será atualizada do modo kernel, portanto, o depurador não interromperá a atualização.
- Em que a expressão Watch tem mais de 4 bytes no hardware de 32 bits e 8 bytes no hardware de 64 bits. Essa é uma limitação da arquitetura x86.

> [!NOTE]
> - Os pontos de interrupção de dados dependem de endereços de memória específicos. O endereço de uma variável é alterado de uma sessão de depuração para a próxima, de modo que os pontos de interrupção de dados sejam automaticamente desabilitados no final de cada sessão de depuração.
>
> - Se você definir um ponto de interrupção de dados em uma variável local, o ponto de interrupção permanecerá habilitado quando a função terminar, mas o endereço de memória não será mais aplicável, portanto, o comportamento do ponto de interrupção será imprevisível. Se você definir um ponto de interrupção de dados em uma variável local, deverá excluir ou desabilitar o ponto de interrupção antes que a função termine.

## <a name="manage-breakpoints-in-the-breakpoints-window"></a><a name="BKMK_Specify_advanced_properties_of_a_breakpoint_"></a> Gerenciar pontos de interrupção na janela de Pontos de Interrupção

 Você pode usar a janela **pontos de interrupção** para ver e gerenciar todos os pontos de interrupção em sua solução. Esse local centralizado é especialmente útil em uma solução grande, ou para cenários de depuração complexos em que os pontos de interrupção são críticos.

Na janela **pontos de interrupção** , você pode pesquisar, classificar, filtrar, habilitar/desabilitar ou excluir pontos de interrupção. Você também pode definir condições e ações ou adicionar um novo ponto de interrupção de função ou de dados.

Para abrir a janela **pontos de interrupção** , selecione **depurar**  >  **Windows**  >  **pontos de interrupção**do Windows ou pressione **ALT** + **F9** ou **Ctrl** + **ALT** + **B**.

![Janela pontos de interrupção](../debugger/media/breakpointswindow.png "Janela Pontos de Interrupção")

Para selecionar as colunas a serem exibidas na janela **pontos de interrupção** , selecione **Mostrar colunas**. Selecione um cabeçalho de coluna para classificar a lista de pontos de interrupção por essa coluna.

### <a name="breakpoint-labels"></a><a name="BKMK_Set_a_breakpoint_at_a_function_return_in_the_Call_Stack_window"></a>Rótulos de ponto de interrupção
Você pode usar rótulos para classificar e filtrar a lista de pontos de interrupção na janela **pontos de interrupção** .

1. Para adicionar um rótulo a um ponto de interrupção, clique com o botão direito do mouse no ponto de interrupção no código-fonte ou na janela **pontos de interrupção** e, em seguida, selecione **Editar rótulos**. Adicione um novo rótulo ou escolha um existente e, em seguida, selecione **OK**.
2. Classifique a lista de pontos de interrupção na janela **pontos de interrupção** selecionando os **Rótulos**, **condições**ou outros cabeçalhos de coluna. Você pode selecionar as colunas a serem exibidas selecionando **Mostrar colunas** na barra de ferramentas.

### <a name="export-and-import-breakpoints"></a>Importar e exportar pontos de interrupção
 Para salvar ou compartilhar o estado e o local dos pontos de interrupção, você pode exportá-los ou importá-los.

- Para exportar um único ponto de interrupção para um arquivo XML, clique com o botão direito do mouse no ponto de interrupção na janela código-fonte ou **pontos de interrupção** e selecione **Exportar** ou **Exportar selecionado**. Selecione um local de exportação e, em seguida, selecione **salvar**. O local padrão é a pasta da solução.
- Para exportar vários pontos de interrupção, na janela **pontos de interrupção** , selecione as caixas ao lado dos pontos de interrupção ou insira os critérios de pesquisa no campo de **pesquisa** . Selecione o ícone **exportar todos os pontos de interrupção correspondentes aos critérios de pesquisa atuais** e salve o arquivo.
- Para exportar todos os pontos de interrupção, desmarque todas as caixas e deixe o campo de **pesquisa** em branco. Selecione o ícone **exportar todos os pontos de interrupção correspondentes aos critérios de pesquisa atuais** e salve o arquivo.
- Para importar pontos de interrupção, na janela **pontos de interrupção** , selecione o ícone **importar pontos de interrupção de um arquivo** , navegue até o local do arquivo XML e selecione **abrir**.

## <a name="set-breakpoints-from-debugger-windows"></a><a name="BKMK_Set_a_breakpoint_from_debugger_windows"></a>Definir pontos de interrupção de janelas do depurador

Você também pode definir pontos de interrupção da **pilha de chamadas** e janelas do depurador de **desmontagem** .

### <a name="set-a-breakpoint-in-the-call-stack-window"></a>Definir um ponto de interrupção na janela pilha de chamadas

 Para interromper a instrução ou a linha para a qual uma função de chamada retorna, você pode definir um ponto de interrupção na janela **pilha de chamadas** .

**Para definir um ponto de interrupção na janela pilha de chamadas:**

1. Para abrir a janela **pilha de chamadas** , você deve estar em pausa durante a depuração. Selecione **depurar**  >  **Windows**  >  **pilha de chamadas**do Windows ou pressione **Ctrl** + **ALT** + **C**.

2. Na janela **pilha de chamadas** , clique com o botão direito do mouse na função de chamada, selecione ponto de interrupção de inserção de **ponto de interrupção**  >  **Insert Breakpoint**ou pressione **F9**.

   Um símbolo de ponto de interrupção aparece ao lado do nome de chamada de função na margem esquerda da pilha de chamadas.

O ponto de interrupção da pilha de chamadas aparece na janela **pontos de interrupção** como um endereço, com um local de memória que corresponde à próxima instrução executável na função.

O depurador é interrompido na instrução.

Para obter mais informações sobre a pilha de chamadas, consulte [como: Use a janela Pilha de Chamadas](../debugger/how-to-use-the-call-stack-window.md).

Para rastrear visualmente pontos de interrupção durante a execução do código, consulte [mapear métodos na pilha de chamadas durante a depuração](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md).

### <a name="set-a-breakpoint-in-the-disassembly-window"></a>Definir um ponto de interrupção na janela de desmontagem

1. Para abrir a janela de **desmontagem** , você deve estar em pausa durante a depuração. Selecione **depurar**  >  **Windows**  >  **desmontagem**do Windows ou pressione **ALT** + **8**.

2. Na janela **desmontagem** , clique na margem esquerda da instrução que você deseja interromper. Você também pode selecioná-lo e pressionar **F9**, ou clicar com o botão direito do mouse **e selecionar ponto**de interrupção de inserção de pontos de interrupção  >  **Insert Breakpoint**.

## <a name="see-also"></a>Confira também

- [O que é depuração?](../debugger/what-is-debugging.md)
- [Escreva um código C# melhor usando o Visual Studio](../debugger/write-better-code-with-visual-studio.md)
- [Primeira olhada na depuração](../debugger/debugger-feature-tour.md)
- [Solucionar problemas de pontos de interrupção no depurador do Visual Studio](../debugger/troubleshooting-breakpoints.md)
