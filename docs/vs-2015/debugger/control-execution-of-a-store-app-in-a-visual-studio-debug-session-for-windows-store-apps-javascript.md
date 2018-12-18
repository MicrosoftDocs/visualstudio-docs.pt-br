---
title: Controlar a execução de um aplicativo da Store em uma sessão de depuração do Visual Studio para aplicativos da Windows Store (JavaScript) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: 60159535-61ec-466a-a4a6-115ec72a8af5
caps.latest.revision: 19
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 8b5fbd27226db800a99423191126e91df1810411
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51810488"
---
# <a name="control-execution-of-a-store-app-in-a-visual-studio-debug-session-for-windows-store-apps-javascript"></a>Controlar a execução de um aplicativo da Store em uma sessão de depuração do Visual Studio para Aplicativos da Windows Store (JavaScript)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este início rápido demonstra como navegar no depurador do Visual Studio e como exibir o estado do programa em uma sessão.  
  
 Este guia de início rápido é para desenvolvedores que são novos na depuração com o Visual Studio e a sessão de depuração para desenvolvedores que desejam saber mais sobre como navegar em um Visual Studio. Ele não ensina a arte de depurar a si próprio. As funções no código de exemplo destinam-se somente a demonstrar os procedimentos de depuração descritos neste tópico. As funções não utilizam as práticas recomendadas de design de aplicativo ou função. Na verdade, você rapidamente descobrirá que as funções e o aplicativo em si, não fazem muita coisa alguma.  
  
 As seções deste início rápido foram projetadas para serem o mais independentes possível, portanto, você pode ignorar qualquer seção que inclui informações que você já estiver familiarizado com. Você também não precisa criar um aplicativo de exemplo. No entanto, nós recomendamos que faça isso e tornamos o processo mais fácil possível.  
  
 **Atalhos de teclado do depurador.** A navegação no depurador do Visual Studio é otimizada tanto para mouse quanto para teclado. Muitas das etapas neste tópico incluem o acelerador de teclado ou a tecla de atalho em um comentário entre parênteses. Por exemplo, (teclado: F5) indica que pressionar a tecla F5 inicia ou continua a execução do depurador.  
  
> [!NOTE]
>  **O padrão de módulo**  
>   
>  Aplicativos da Windows Store geralmente usam o JavaScript *padrão de módulo* para encapsular dados e funções em uma página. O padrão Módulo usa um fechamento único, autoexecutado e anônimo para manter a funcionalidade de página separada do namespace global. Neste tópico, chamamos essa função a *módulo*.  
  
## <a name="in-this-topic"></a>Neste tópico  
 Você pode aprender como:  
  
 [Criar o aplicativo de exemplo](#BKMK_Create_the_sample_app)  
  
 [Definir e executar até um ponto de interrupção, entrar em uma função e examinar os dados de programa](#BKMK_Set_and_run_to_a_breakpoint__step_into_a_function__and_examine_program_data)  
  
 [Entrar, sobre e sair de funções](#BKMK_Step_into__over__and_out_of_functions)  
  
 [Defina um ponto de interrupção condicional, executar até o cursor e visualizar uma variável](#BKMK_Set_a_conditional_breakpoint__run_to_the_cursor__and_visualize_a_variable)  
  
 [Exibir dados da variável na janela locais](#BKMK_View_variable_data_in_the_Locals_window)  
  
- [Exibir dados da variável e a cadeia de protótipos de um objeto](#BKMK_View_variable_data_and_the_prototype_chain_of_an_object)  
  
- [Examinar dados de cadeia de escopo](#BKMK_Examine_scope_chain_data)  
  
  [Navegue até o código usando a janela pilha de chamadas](#BKMK_Navigate_to_code_by_using_the_Call_Stack_window)  
  
##  <a name="BKMK_Create_the_sample_app"></a> Criar o aplicativo de exemplo  
 Depuração é sobre código, portanto, o aplicativo de exemplo usa a estrutura do aplicativo Windows Store apenas para criar um arquivo de origem no qual você pode ver como funciona a navegar de uma sessão de depuração e como examinar o estado do programa. Todo o código que você vai invocar é chamado por meio da função `module` do arquivo default. js. Nenhum controle é adicionado e nenhum evento é tratado.  
  
1. **Crie um aplicativo JavaScript Windows Store em branco.** Abra o Visual Studio. Na home page, escolha o **novo projeto** link. Sobre o **novo projeto** caixa de diálogo, escolha **JavaScript** no **instalado** lista e, em seguida, escolha **Windows Store**. Na lista de modelos de projeto, escolha **aplicativo em branco**. Visual Studio cria uma nova solução e projeto e exibe o arquivo default.htm no editor de códigos.  
  
    Observe os arquivos de script que são carregados para a página.  
  
   -   O `base.js` e `ui.js` criam arquivos de **biblioteca do Windows para JavaScript**. A Biblioteca do Windows para JavaScript é um conjunto de arquivos em JavaScript e CSS que tornam mais fácil criar aplicativos da Windows Store usando JavaScript. Você usá-lo junto com HTML, CSS e o tempo de execução do Windows para criar seu aplicativo.  
  
   -   O código começa `default.js` arquivo.  
  
2. **Abra o arquivo de origem default. js.** No Gerenciador de soluções, abra o **js** nó e escolha `default.js`.  
  
3. **Substitua o conteúdo da página com o código de exemplo.** Exclua todo o conteúdo do arquivo `default.js`. Siga este link: [código de exemplo de navegação (JavaScript) depurador](../debugger/debugger-navigation-sample-code-javascript.md)e, em seguida, copie o código listado na seção de JavaScript para a área de transferência. (Escolha **volta** no navegador ou Visualizador da Ajuda para retornar a esta página de início rápido.) No editor do Visual Studio, cole o código no `default.js` agora vazio. Escolher **Ctrl + S** para salvar o arquivo.  
  
   {1&gt;Agora você pode acompanhar os exemplos neste tópico.&lt;1}  
  
##  <a name="BKMK_Set_and_run_to_a_breakpoint__step_into_a_function__and_examine_program_data"></a> Definir e executar até um ponto de interrupção, entrar em uma função e examinar os dados de programa  
 A maneira mais comum para iniciar uma sessão de depuração é escolher **iniciar depuração** da **depurar** menus (teclado: F5). O aplicativo é iniciado e continua até que um ponto de interrupção é atingido, você suspenda a execução manualmente, ocorra uma exceção ou o aplicativo seja encerrado.  
  
 Quando a execução é suspensa no depurador, você pode exibir o valor de uma variável ativa em uma dica de dados pausando o mouse sobre a variável.  
  
 Depois que você suspenda a execução do aplicativo (que também é chamado de invadir o depurador), você pode controlar a maneira como o restante do código do programa é executado. Você pode continuar a linha por linha, movendo de uma chamada de função para a função em si, ou pode executar uma função chamada em uma única etapa. Esses procedimentos são chamados percorrendo o aplicativo. Você também pode retomar a execução padrão do aplicativo, executando até o próximo ponto de interrupção definido ou até a linha em que você posicionou o cursor. Você pode parar a sessão de depuração a qualquer momento. O depurador foi projetado para executar as operações de limpeza necessárias e sair da execução.  
  
###  <a name="BKMK_Example_1"></a> Exemplo 1  
 Neste exemplo, você deve definir um ponto de interrupção no corpo do `module` funcionar em `default.js` pois ele chama a primeira das nossas instruções do usuário. Em seguida, entra na função, exibir valores de variáveis em dicas de dados do depurador e parar a depuração.  
  
1. **Defina um ponto de interrupção.** Defina um ponto de interrupção na instrução `callTrack = "module function";` que ocorra logo após a chamada para `app.start()`. Escolha a linha na medianiz sombreada do editor de código fonte (teclado: Posicione o cursor na linha e escolha o **F9** chave).  
  
    ![Defina um ponto de interrupção em example1](../debugger/media/dbg-jsnav-example1-breakpoint.png "DBG_JSNAV_example1_breakpoint")  
  
    O ícone de ponto de interrupção aparece na medianiz.  
  
2. **Execute o ponto de interrupção.** Iniciar a sessão de depuração, escolhendo **iniciar depuração** sobre o **depurar** menu (teclado: F5).  
  
    O aplicativo começa a ser executado e suspende a execução imediatamente antes da instrução em que você definir o ponto de interrupção. O ícone de linha atual na medianiz identifica o local e a instrução atual é realçada.  
  
    ![Executar até o ponto de interrupção](../debugger/media/dbg-jsnav-example1-run-to-breakpoint.png "DBG_JSNAV_example1_run_to_breakpoint")  
  
    Você agora está no controle da execução do aplicativo e pode examinar o estado do programa conforme você percorre as instruções do programa.  
  
3. **{2&gt;entrar na função.** Sobre o **Debug** menu, escolha **intervir** (teclado: **F11**).  
  
    ![Etapa em uma linha de código](../debugger/media/dbg-jsnav-example1-step-into.png "DBG_JSNAV_example1_step_into")  
  
    Observe que o depurador vai para a próxima linha, que é uma chamada para o `example1` função. Escolher **intervir** novamente. O depurador vai para a primeira linha de código da função `example1`. A linha realçada não foi executada, mas a função foi carregada na pilha de chamadas e a memória para variáveis locais foi alocada.  
  
4. {1&gt;Quando você entra em uma linha de código, o depurador executa uma das seguintes ações:&lt;1}  
  
   - {1&gt;Se a próxima instrução não for uma chamada para uma função em sua solução, o depurador executará a instrução, irá para a próxima instrução e suspenderá a execução.&lt;1}  
  
   - {1&gt;Se a instrução for uma chamada para uma função em sua solução, o depurador irá para a primeira linha da função chamada e então suspenderá a execução.&lt;1}  
  
     Prossiga para entrar nas instruções de `example1` até atingir o ponto de saída. O depurador realça a chave de fechamento da função.  
  
5. **Exibir valores de variáveis em dicas de dados.** Prossiga para entrar nas instruções de `example1` até atingir o ponto de saída. O depurador realça a chave de fechamento da função. Quando você pausa o mouse sobre um nome de variável, o nome e valor da variável são exibidos em uma dica de dados.  
  
    ![Exibir valores de variáveis na dica de dados](../debugger/media/dbg-jsnav-data-tip.png "DBG_JSNAV_data_tip")  
  
6. **Adicione uma inspeção para a variável calltrack.&lt;2}.** A variável `callTrack` é usada em todo este guia rápido para mostrar as funções chamadas nos exemplos. Para facilitar a exibição do valor da variável, adicione-o uma janela Inspeção. Selecione o nome da variável no editor e, em seguida, escolha **Adicionar inspeção** no menu de atalho.  
  
    ![Assista a uma variável](../debugger/media/dbg-jsnav-watch-window.png "DBG_JSNAV_watch_window")  
  
    Você pode inspecionar diversas variáveis em uma janela inspeção. Os valores de variáveis inspecionadas, como valores em janelas de dica de dados, são atualizados sempre que a execução é suspensa. As variáveis inspecionadas são salvas nas sessões de depuração.  
  
7. **Pare a depuração.** Sobre o **Debug** menu, escolha **parar depuração** (teclado: **Shift + F5**). Isso encerra a sessão de depuração.  
  
##  <a name="BKMK_Step_into__over__and_out_of_functions"></a> Entrar, sobre e sair de funções  
 Em contraste a entrar em uma função chamada por uma função pai, passar sobre uma função executa a função filha e, em seguida, suspende a execução da função de chamada como o pai é retomada. Você pode entrar em uma função quando estiver familiarizado com a maneira como a função funciona e tiver certeza de que sua execução não afetará o problema que você está investigando.  
  
 Entrar em uma linha de código que não contém uma chamada de função executa a linha da mesma forma passo a passo para a linha.  
  
 Sair de uma função filho continua a execução da função e, em seguida, suspende a execução depois que a função retorna para sua função de chamada. Você pode sair de uma função longa quando tiver determinado que o restante da função não é significativo.  
  
 Percorrendo tanto sair de uma função de executam a função.  
  
 ![Etapa em, sobre e sair de métodos](../debugger/media/dbg-basics-stepintooverout.png "DBG_Basics_StepIntoOverOut")  
  
###  <a name="BKMK_Example_2"></a> Exemplo 2  
 {1&gt;Neste exemplo, você pode entrar, passar sobre e sair de funções. &lt;1}  
  
1.  **Chame a função example2 na função de módulo.** Editar o `module` de função e substitua a linha após `var callTrack = "module function"` com `example2();`.  
  
     ![Chamar a função example2](../debugger/media/dbg-jsnav-example2.png "DBG_JSNAV_example2")  
  
2.  **Execute o ponto de interrupção.** Iniciar a sessão de depuração, escolhendo **iniciar depuração** sobre o **depurar** menu (teclado: F5). O depurador suspende a execução no ponto de interrupção.  
  
3.  **Depurar a linha de código.** Sobre o **Debug** menu, escolha **Step Over** (teclado: F10). O depurador executa a `var callTrack = "module function"` instrução da mesma maneira como entrar na instrução.  
  
4.  **Intervenha em example2 e example2_a.** Escolha o **F11** chave Step into a `example2` função. Continue a entrar nas instruções `example2` até chegar à linha `var x = example2_a();`. Novamente, entre nessa linha para mover para o ponto de entrada de `example2_a`. Continue a entrar em cada instrução de `example2_a` até voltar à `example2`.  
  
     ![Etapa em uma função](../debugger/media/dbg-jsnav-example2-a.png "DBG_JSNAV_example2_a")  
  
5.  **Passe por uma função.** Observe que na próxima linha em `example2`, `var y = example2_a();` é basicamente igual à linha anterior. Você pode passar sobre essa linha com segurança. Escolha o **F10** tecla para mover a retomada de `example2` para essa segunda chamada para `example2_a`. Observe que o `callTrack` cadeia de caracteres indica o `example2_a` função foi executada duas vezes.  
  
6.  **Sair de uma função.** Escolha o **F11** chave Step into a `example2_b` função. Observe que `example2_b` não é muito diferente de `example2_a`. Para sair da função, escolha **depuração circular** sobre o **depurar** menus (teclado: **Shift + F11**). Observe que o `callTrack` variável indica que `example2_b` foi executado e que o depurador foi retornado para o ponto onde `example2` será retomada.  
  
7.  **Pare a depuração.** Sobre o **Debug** menu, escolha **parar depuração** (teclado: **Shift + F5**). Isso encerra a sessão de depuração.  
  
##  <a name="BKMK_Set_a_conditional_breakpoint__run_to_the_cursor__and_visualize_a_variable"></a> Defina um ponto de interrupção condicional, executar até o cursor e visualizar uma variável  
 Um ponto de interrupção condicional Especifica uma condição que faz com que o depurador suspender a execução. A condição é especificada por uma expressão de código que pode ser avaliada como true ou false. Por exemplo, você pode usar um ponto de interrupção condicional para examinar o estado do programa em uma função chamada com frequência apenas quando uma variável atinge um determinado valor.  
  
 Executar até o cursor é como configurar um único ponto de interrupção. Quando a execução for suspensa, você poderá selecionar uma linha na origem e retomar a execução até que a linha selecionada seja atingida. Por exemplo, você pode percorrer um loop em uma função e determinar que o código no loop está sendo executado corretamente. Em vez de percorrer cada iteração do loop, você pode executar até o cursor que é posicionado após o loop é executado.  
  
 Às vezes, é difícil ler um valor de variável na linha de uma dica de dados ou em outra janela de dados. O depurador pode exibir cadeias de caracteres, HTML e Xml em um visualizador de texto que apresente uma exibição formatada do valor em uma janela rolável.  
  
###  <a name="BKMK_Example_3"></a> Exemplo 3  
 Neste exemplo, você deve definir um ponto de interrupção condicional para parar em uma iteração específica de um loop e, em seguida, executar até o cursor posicionado após o loop. Você também pode exibir o valor de uma variável em um visualizador de texto.  
  
1.  **Chame a função example3 na função de módulo.** Editar o `module` de função e substitua a linha após `var callTrack = "module function";` com a linha `example3();`.  
  
     ![Chamar example3](../debugger/media/dbg-jsnav-example3.png "DBG_JSNAV_example3")  
  
2.  **Execute o ponto de interrupção.** Iniciar a sessão de depuração, escolhendo **iniciar depuração** sobre o **depurar** menu (teclado: **F5**). O depurador suspende a execução no ponto de interrupção no `module` função.  
  
3.  **Passar para a função example3.** Escolha **intervir** sobre o **depurar** menu (teclado: **F11**) para mover para o ponto de entrada do `example3` função. Continue entrando na função até ter iterado um ou dois loops do bloco `for`. Observe que ele levaria muito tempo para percorrer todas as 1.000 iterações.  
  
4.  **Defina um ponto de interrupção condicional.** Na medianiz esquerda da janela de código, clique na linha `s += i.toString() + "\n";` e, em seguida, escolha **condição** no menu de atalho.  
  
     Selecione o **condição** caixa de seleção e, em seguida, digite `i == 500;` na caixa de texto. Escolha o **vale** opção e escolha **Okey**. O ponto de interrupção permite verificar o valor à 500ª iteração do loop `for`. Você pode identificar um ícone de ponto de interrupção condicional pela sua cruz branca.  
  
     ![Ícone de ponto de interrupção condicional](../debugger/media/dbg-jsnav-breakpoint-condition-icon.png "DBG_JSNAV_Breakpoint_Condition_icon")  
  
5.  **Execute o ponto de interrupção.** Sobre o **Debug** menu, escolha **continuar** (teclado: **F5**). Pause sobre `i` para confirmar que o valor atual de `i` é 500. Observe também que a variável `s` é representada como uma linha e é muito mais do que a janela de dica de dados.  
  
6.  **Visualize uma variável de cadeia de caracteres.** Clique no ícone de lupa na dica de dados do `s`.  
  
     A janela do Visualizador de texto é exibida e o valor da cadeia de caracteres é apresentado como uma cadeia de caracteres de várias linha.  
  
     ![Depurar um visualizador de texto](../debugger/media/dbg-jsnav-text-visualizer.png "DBG_JSNAV_Text_Visualizer")  
  
7.  **Execute até o cursor.** Selecione a linha `callTrack += "->example3";` e, em seguida, escolha **executar até o Cursor** no menu de atalho (teclado: **CTRL+F10**). O depurador conclui as iterações do loop e então suspende a execução na linha.  
  
8.  **Pare a depuração.** Sobre o **Debug** menu, escolha **parar depuração** (teclado: **Shift + F5**). Isso encerra a sessão de depuração.  
  
###  <a name="BKMK_Use_Run_to_Cursor_to_return_to_your_code_and_delete_a_breakpoint"></a> Usar executar até o Cursor para retornar ao seu código e excluir um ponto de interrupção  
 Executar até o cursor pode ser muito útil quando você tiver entrado em código de biblioteca da Microsoft ou por terceiros. Embora percorrer o código de biblioteca possa ser informativo, isso geralmente pode demorar muito. E, em geral, você estará muito mais interessado em seu próprio código. Este exercício mostra como fazer isso.  
  
1.  **Defina um ponto de interrupção na chamada App.Start.&lt;2}.** No `module` de função, defina um ponto de interrupção na linha `app.start()`  
  
2.  **Executar até o ponto de interrupção e etapa para a função de biblioteca.**  
  
     Quando você entrar em `app.start()`, o editor exibirá o código em `base.js`. Intervenha em mais algumas linhas.  
  
3.  **Etapa sobre e sair de funções.** Conforme você avança em (**F10**) e sai do (**SHIFT+F11**) de código em `base.js`, você pode chegar à conclusão de que examinar a complexidade e comprimento da função inicial é não o que você deseja fazer.  
  
4.  **Defina o cursor para o seu código e execute a ele.** Volte para o arquivo `default.js` no editor de códigos. Selecione a primeira linha de código após `app.start()` (você não pode executar até um comentário ou uma linha em branco). Escolher **executar até o Cursor** no menu de atalho. O depurador continua a execução da função App.Start.&lt;2} e suspende a execução no ponto de interrupção.  
  
##  <a name="BKMK_View_variable_data_in_the_Locals_window"></a> Exibir dados da variável na janela locais  
 As janelas de variáveis locais é uma exibição de árvore dos parâmetros e variáveis da cadeia do escopo da função em execução no momento.  
  
###  <a name="BKMK_View_variable_data_and_the_prototype_chain_of_an_object"></a> Exibir dados da variável e a cadeia de protótipos de um objeto  
  
1.  **Adicione um objeto de matriz, a função do módulo.** Editar o `module` de função e substitua a linha após `var callTrack = "module function"` com `var myArray = new Array(1, 2, 3);`  
  
     ![definição de myArray](../debugger/media/dbg-jsnav-myarray.png "DBG_JSNAV_myArray")  
  
2.  **Execute o ponto de interrupção.** Iniciar a sessão de depuração, escolhendo **iniciar depuração** sobre o **depurar** menu (teclado: **F5**). O depurador suspende a execução no ponto de interrupção. Entrar para a linha.  
  
3.  **Abra a janela locais.** Sobre o **Debug** , aponte para **Windows**e, em seguida, escolha **locais**. (Teclado: Alt + 4).  
  
4.  **As variáveis locais na função de módulo** windows locais o exibe as variáveis da função em execução no momento (a `module` função) como nós de nível superior da árvore. Quando você inserir uma função, o JavaScript criará todas as variáveis e atribuirá a elas um valor de `undefined`. Funções que são definidas na função têm seu texto como um valor.  
  
     ![Janela locais](../debugger/media/dbg-jsnav-locals-window.png "DBG_JSNAV_Locals_window")  
  
5.  **Percorrer as definições de callTrack e myArray.** Encontre as variáveis callTrack e myArray na janela Locais. Depuração parcial (**F10**) as duas definições e observe que o **valor** e **tipo** campos são alterados. A janela locais realça os valores das variáveis que foram alterados desde a última interrupção.  
  
6.  **Examinar o objeto MyArray&lt;2** expandir o `myArray` variável. Cada elemento da matriz é listado o **[protótipo]** nó que contém a hierarquia de herança do `Array` objeto. Expanda esse nó.  
  
     ![Cadeia de protótipos na janela locais](../debugger/media/dbg-jsnav-locals-proto-chain.png "DBG_JSNAV_Locals_proto_chain")  
  
    -   O **métodos** nó lista todos os métodos do `Array` objeto.  
  
    -   O **[protótipo]** nó contém o protótipo da `Object` objeto do qual `Array` é derivado. **[protótipo]**  nós podem ser recursivas. Cada objeto pai em uma hierarquia de objetos é descrito na **[protótipo]** nó de seu filho.  
  
7.  **Pare a depuração.** Sobre o **Debug** menu, escolha **parar depuração** (teclado: Shift + F5). Isso encerra a sessão de depuração.  
  
##  <a name="BKMK_Examine_scope_chain_data"></a> Examinar dados de cadeia de escopo  
 O *cadeia de escopo* de uma função inclui todas as variáveis que estão ativas e pode ser acessado pela função. Variáveis globais são parte da cadeia de escopo, assim como quaisquer objetos (incluindo funções) definidos na função que define a função atualmente em execução. Por exemplo, a variável `callTrack` definida na função `module` de `default.js` pode ser acessada por qualquer função definida na função `module`. Cada escopo é listado separadamente na janela locais.  
  
- {1&gt;As variáveis da função que está em execução no momento são listadas na parte superior da janela.&lt;1}  
  
- As variáveis de cada escopo de função na cadeia de escopo são listadas em uma **[escopo]** nó para a função. As funções de escopo são listadas pela sua ordem na cadeia, da função que define a função atual para a função mais externa da cadeia.  
  
- O **[Globals]** nó lista os objetos globais definidos fora de qualquer função.  
  
  Cadeias de escopo podem ser confusas e são melhor ilustradas pelo exemplo. No exemplo a seguir, você pode ver como o `module` função cria seu próprio escopo e como você pode criar outro nível de escopo criando um fechamento.  
  
###  <a name="BKMK_Example_4"></a> Exemplo 4  
  
1.  **Chame a função example4 da função de módulo.** Editar o `module` de função e substitua a linha após `var callTrack = "module function"` com o `example4()`:  
  
     ![Chamar example4](../debugger/media/dbg-jsnav-example4.png "DBG_JSNAV_example4")  
  
2.  **Execute o ponto de interrupção.** Iniciar a sessão de depuração, escolhendo **iniciar depuração** sobre o **depurar** menu (teclado: **F5**). O depurador suspende a execução no ponto de interrupção.  
  
3.  **Abra a janela locais.** Se necessário, sobre o **depurar** , aponte para **Windows**e, em seguida, escolha **locais**. (Teclado: **Alt + 4**). Observe que a janela lista todas as variáveis e funções na `module` funcionar e também contém uma **[Globals]** nó.  
  
4.  **Examine as variáveis globais.** Expanda o **[Globals]** nó. Os objetos e as variáveis em Global foram definidos pela biblioteca do Windows para JavaScript. Você pode adicionar suas próprias variáveis ao escopo global.  
  
5.  **Intervir no example4 e examine seu local e definir o escopo de variáveis** intervir (teclado: **F11**) o `example4` função. Porque `example4` é definido em de `module` função, o `module` função torna-se o escopo pai. `example4` pode chamar qualquer uma das funções no `module` de função e acessar suas variáveis. Expanda o **[escopo]** nó na janela locais e observe que ele contém as mesmas variáveis do `module` função.  
  
     ![Escopos do método example4](../debugger/media/dbg-jsnav-locals-example4-scope.png "DBG_JSNAV_Locals_example4_scope")  
  
6.  **{2&gt;entre em example4_a e examinar seu local e definir o escopo de variáveis** prossiga para entrar nas `example4` e na chamada para `example4_a`. Observe que as variáveis locais agora são de `example4_a`e que o **[escopo]** nó continua contendo as variáveis do `module` função. Embora as variáveis do `example4` estejam ativas, eles não poderão ser alcançados pelo `example4_a` e não fazem mais parte da cadeia de escopo.  
  
7.  **{2&gt;entre em multipyByA e examinar seu local e definir o escopo de variáveis** percorra o restante dos `example4_a` na linha `var x = multilpyByA(b);`.  
  
     A variável de função `multipyByA` foi definido para o `multiplyClosure` função que é um *fechamento*. `multipyClosure` define e retorna uma função interna, `mulitplyXby`e captura (encerra) seu parâmetro e variável. Em um fechamento, a função interna retornada tem acesso aos dados da função externa e então, cria seu próprio nível de escopo.  
  
     Quando você entrar em `var x = multilpyByA(b);`, mova para o `return a * b;` de linha no `mulitplyXby` função interna.  
  
8.  Na janela locais, somente o parâmetro `b` é listada como uma variável local no `multiplyXby`, mas uma nova **[escopo]** nível foi adicionado. Expandindo esse nó, você verá que ele contém os parâmetros, as funções e as variáveis de `multiplyClosure`, incluindo a variável `a` chamada na primeira linha de `multiplyXby`. Uma verificação rápida da segunda **[escopo]** nó revela as variáveis de função do módulo, que `multiplyXby` acessa em sua próxima linha.  
  
     ![Escopos de um fechamento na janela locais](../debugger/media/dbg-jsnav-scope-mulitplyxby.png "DBG_JSNAV_scope_mulitplyXby")  
  
9. **Pare a depuração.** Sobre o **Debug** menu, escolha **parar depuração** (teclado: **Shift + F5**). Isso encerra a sessão de depuração.  
  
##  <a name="BKMK_Navigate_to_code_by_using_the_Call_Stack_window"></a> Navegue até o código usando a janela pilha de chamadas  
 A pilha de chamadas é uma estrutura de dados que contém informações sobre as funções que estão em execução no thread atual do aplicativo. Quando você atinge um ponto de interrupção, a janela Pilha de Chamadas exibe uma lista de todas as funções que estão ativas na pilha. A função que está em execução no momento está no topo da lista da janela Pilha de Chamadas. A função que inicia o thread está na parte inferior da lista. As funções entre o topo e a parte inferior mostram o demarcador da chamada da função inicial até a função atual.  
  
 Além de mostrar o caminho da chamada para a função em execução no momento, a janela pilha de chamadas pode ser usada para navegar até o código no editor de códigos. Essa funcionalidade pode ser valiosa quando você estiver trabalhando com vários arquivos e você deseja mover rapidamente para uma função específica.  
  
###  <a name="BKMK_Example_5"></a> Exemplo 5  
 {1&gt;Neste exemplo, você deve entrar em um caminho de chamada que contenha cinco funções definidas pelo usuário. &lt;1}  
  
1.  **Chame a função example5 na função de módulo.** Editar o `module` de função e substitua a linha após `var callTrack = "module function";` com a linha `example5();`.  
  
     ![Chamar example5](../debugger/media/dbg-jsnav-example5.png "DBG_JSNAV_example5")  
  
2.  **Execute o ponto de interrupção.** Iniciar a sessão de depuração, escolhendo **iniciar depuração** sobre o **depurar** menu (teclado: **F5**). O depurador suspende a execução no ponto de interrupção na função de módulo.  
  
3.  **Abra a janela pilha de chamadas.** Sobre o **Debug** menu, escolha **Windows**e, em seguida, escolha **pilha de chamadas** (teclado: Alt + 7). Observe que a janela pilha de chamadas mostra duas funções:  
  
    -   **Código global** é o ponto de entrada do `module` função na parte inferior da pilha de chamadas.  
  
    -   **Função anônima** mostra a linha no `module` função em que a execução é suspensa. Isso está no topo da pilha de chamadas.  
  
4.  **Intervir em funções para acessar a função example5_d.** Escolher **intervir** sobre o **Debug** menu (teclado: **F11**) para executar as chamadas no caminho de chamada até que o ponto de entrada da função example5_d. Observe que cada vez que uma função chama uma função, o número de linha da função de chamada é salvo e a função chamada é colocada na parte superior da pilha. O número de linha da função de chamada é o ponto em que a função de chamada suspendeu a execução. Uma seta amarela aponta para a função em execução no momento.  
  
     ![Janela pilha de chamadas](../debugger/media/dbg-jsnav-callstack-windows.png "DBG_JSNAV_CallStack_windows")  
  
5.  **Use a janela pilha de chamadas para navegar até o código example5_a e definir um ponto de interrupção.** Na janela pilha de chamadas, selecione a `example5_a` item de lista e, em seguida, escolha **ir para fonte** no menu de atalho. O editor de código define o cursor na linha de retorno da função. Defina um ponto de interrupção nessa linha. Observe que a linha de execução atual não é alterada. Somente o cursor do editor foi movido.  
  
6.  **Intervir em funções e, em seguida, execute o ponto de interrupção.** Continue entrando em `example5_d`. Observe que, quando você retorna da função, ela é retirada da pilha de chamadas. Pressione **F5** para continuar a execução do programa. Parar no ponto de interrupção criado na etapa anterior.  
  
7.  **Pare a depuração.** Sobre o **Debug** menu, escolha **parar depuração** (teclado: **Shift + F5**). Isso encerra a sessão de depuração.  
  
## <a name="see-also"></a>Consulte também  
 [Iniciar uma sessão de depuração (JavaScript)](../debugger/start-a-debugging-session-for-store-apps-in-visual-studio-javascript.md)   
 [Guia de início rápido: Navegação no depurador (JavaScript)](../debugger/control-execution-of-a-store-app-in-a-visual-studio-debug-session-for-windows-store-apps-javascript.md)   
 [Guia de início rápido: Depurar HTML e CSS](../debugger/quickstart-debug-html-and-css.md)   
 [Disparar de suspender, continuar e eventos para Windows Store em segundo plano)](../debugger/how-to-trigger-suspend-resume-and-background-events-for-windows-store-apps-in-visual-studio.md)   
 [Depurar aplicativos no Visual Studio](../debugger/debug-store-apps-in-visual-studio.md)



