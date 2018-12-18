---
title: Navegar por uma sessão de depuração no Visual Studio (Xaml e c#) | Microsoft Docs
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
ms.assetid: 1da33203-333f-4a05-b4e2-8d407c497233
caps.latest.revision: 21
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 00ca08eae8d1ed9a9c1f75eff9a6d3a0642e5a79
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51741153"
---
# <a name="navigate-a-debugging-session-in-visual-studio-xaml-and-c"></a>Navegar por uma sessão de depuração no Visual Studio (XAML e C#)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este início rápido demonstra como navegar de sessões de depuração do Visual Studio e como exibir e alterar o estado do programa em uma sessão.  
  
 Este guia de início rápido é para desenvolvedores que são novos na depuração com o Visual Studio e a sessão de depuração para desenvolvedores que desejam saber mais sobre como navegar em um Visual Studio. Ele não ensina a arte de depurar a si próprio. Os métodos no código de exemplo destinam-se somente para demonstrar os procedimentos de depuração descritos neste tópico. Os métodos não utilizam as práticas recomendadas de design de aplicativo ou função. Na verdade, você rapidamente descobrirá que os métodos e o aplicativo em si, não fazem muita coisa alguma.  
  
 As seções deste início rápido foram projetadas para serem o mais independentes possível, portanto, você pode ignorar qualquer seção que inclui informações que você já estiver familiarizado com. Você também não é necessárias para criar um aplicativo de exemplo; No entanto, nós recomendamos que faça isso e tornamos o processo mais fácil possível.  
  
 **Atalhos de teclado do depurador.** A navegação pelo depurador Visual Studio é otimizada para o mouse e teclado. Muitas das etapas neste tópico incluem o acelerador de teclado ou a tecla de atalho em um comentário entre parênteses. Por exemplo, (teclado: F5) indica que pressionar a tecla F5 inicia ou continua a execução do depurador.  
  
## <a name="in-this-topic"></a>Neste tópico  
 Você pode aprender como:  
  
-   [Criar o aplicativo de exemplo](#BKMK_CreateTheApplication)  
  
-   [Definir e executar até um ponto de interrupção, etapa em um método e examinar os dados de programa](#BKMK_StepInto)  
  
-   [Para failover e fora de métodos](#BKMK_StepIntoOverOut)  
  
-   [Defina um ponto de interrupção condicional, executar até o cursor e visualizar uma variável](#BKMK_ConditionCursorVisualize)  
  
-   [Editar e continuar, se recuperar de uma exceção](#BKMK_EditContinueRecoverExceptions)  
  
##  <a name="BKMK_CreateTheApplication"></a> Criar o aplicativo de exemplo  
 Depuração é sobre código, portanto, o aplicativo de exemplo usa a estrutura do aplicativo Windows Store apenas para criar um arquivo de origem no qual você pode ver como funciona a navegar de uma sessão de depuração e como examinar e alterar o estado do programa. Todo o código que você vai invocar é chamado do construtor da página principal; Nenhum controle é adicionado e nenhum evento é tratado.  
  
 **Crie um aplicativo da Windows Store de c# padrão.** Abra o Visual Studio. Na home page, escolha o **novo projeto** link. Na caixa de diálogo Novo projeto, escolha **Visual c#** na **instalado** lista e, em seguida, escolha **Windows Store**. Na lista de modelos de projeto, escolha **aplicativo**. Visual Studio cria uma nova solução e projeto e exibe o designer de MainPage. XAML e o editor de código XAML.  
  
 **Abra o arquivo MainPage.xaml.cs.** Clique com botão direito em qualquer lugar no editor XAML e escolha **Exibir código**. O arquivo de code-behind MainPage.xaml.cs é exibido. Observe que apenas um método, o `MainPage()` construtor, está listado no arquivo.  
  
 **Substitua o construtor MainPage com o código de exemplo.** Exclua o método MainPage(). Siga este link: [código de exemplo de navegação (Xaml e c#) do depurador](../debugger/debugger-navigation-sample-code-xaml-and-csharp.md)e, em seguida, copie o código listado na seção c# para a área de transferência. (Escolha **volta** no navegador ou Visualizador da Ajuda para retornar a esta página de início rápido.) No editor do Visual Studio, cole o código no `partial class MainPage` bloco. Escolha CTRL + s para salvar o arquivo.  
  
 {1&gt;Agora você pode acompanhar os exemplos neste tópico.&lt;1}  
  
##  <a name="BKMK_StepInto"></a> Definir e executar até um ponto de interrupção, etapa em um método e examinar os dados de programa  
 A maneira mais comum que você pode iniciar uma sessão de depuração é escolher **iniciar depuração** da **depurar** menus (teclado: F5). Execução começa e continua até que um ponto de interrupção seja alcançado, você suspenda a execução manualmente, ocorra uma exceção ou o aplicativo seja encerrado.  
  
 Quando a execução é suspensa no depurador, você pode exibir o valor de uma variável ativa em uma dica de dados, passando o mouse sobre a variável. Você também pode abrir as janelas locais e Autos para ver listas de variáveis Active Directory e seus valores atuais. Adicionando uma ou mais variáveis para um permite a janela Inspeção você se concentrar no valor das variáveis como o aplicativo continua a execução.  
  
 Depois que você suspenda a execução do aplicativo (que também é chamado de invadir o depurador), você pode controlar a maneira como o restante do código do programa é executado. Você pode continuar a linha por linha, movendo-se de uma chamada de método para o método em si, ou você pode executar um método chamado em uma única etapa. Esses procedimentos são chamados percorrendo o aplicativo. Você também pode retomar a execução padrão do aplicativo, executando até o próximo ponto de interrupção definido ou até a linha em que você posicionou o cursor. Você pode parar a sessão de depuração a qualquer momento. O depurador foi projetado para executar as operações de limpeza necessárias e sair da execução.  
  
### <a name="example-1"></a>Exemplo 1  
 Neste exemplo, você definir um ponto de interrupção no construtor MainPage do arquivo MainPage.xaml.cs, intervir o primeiro método, exibe valores de variáveis e, em seguida, parar a depuração.  
  
 **Defina um ponto de interrupção.** Defina um ponto de interrupção na instrução `methodTrack = "Main Page";` no construtor MainPage. Escolha a linha na medianiz sombreada do editor de código fonte (teclado: Posicione o cursor na linha e escolha a tecla F9).  
  
 ![Intervir](../debugger/media/dbg-basics-stepinto.png "DBG_Basics_StepInto")  
  
 O ícone de ponto de interrupção aparece na medianiz.  
  
 **Execute o ponto de interrupção.** Iniciar a sessão de depuração, escolhendo **iniciar depuração** sobre o **depurar** menu (teclado: F5).  
  
 O aplicativo começa a ser executado e suspende a execução imediatamente antes da instrução em que você definir o ponto de interrupção. O ícone de linha atual na medianiz identifica o local e a instrução atual é realçada.  
  
 ![Defina um ponto de interrupção](../debugger/media/dbg-basics-setbreakpoint.png "DBG_Basics_SetBreakpoint")  
  
 Você agora está no controle da execução do aplicativo e pode examinar o estado do programa conforme você percorre as instruções do programa.  
  
 **Passar para o método.** Sobre o **Debug** menu, escolha **intervir** (teclado: F11).  
  
 ![Linha atual](../debugger/media/dbg-basics-currentline.png "DBG_Basics_CurrentLine")  
  
 Observe que o depurador vai para a próxima linha, que é uma chamada para o método de exemplo 1. Escolha Step Into novamente. O depurador vai para o ponto de entrada do método Example1. Isso indica que o método foi carregado na pilha de chamadas e a memória para variáveis locais foram alocados.  
  
 {1&gt;Quando você entra em uma linha de código, o depurador executa uma das seguintes ações:&lt;1}  
  
- {1&gt;Se a próxima instrução não for uma chamada para uma função em sua solução, o depurador executará a instrução, irá para a próxima instrução e suspenderá a execução.&lt;1}  
  
- Se a instrução for uma chamada para uma função em sua solução, o depurador se move para o ponto de entrada da função chamada e, em seguida, suspende a execução.  
  
  Continue entrar nas instruções de exemplo 1, até atingir o ponto de saída. O depurador realça a chave de fechamento do método.  
  
  **Examine os valores de variáveis em dicas de dados.** Quando você passa o mouse sobre um nome de variável, o nome, o valor e o tipo da variável é exibida em uma dica de dados.  
  
  ![Dica de dados do depurador](../debugger/media/dbg-basics-datatip.png "DBG_Basics_DataTip")  
  
  Passe o mouse sobre a variável `a`. Observe o nome, valor, tipo de dados. Passe o mouse sobre a variável `methodTrack`. Novamente, observe o nome, valor, tipo de dados.  
  
  **Examine os valores de variáveis na janela locais.** Sobre o **Debug** , aponte para **Windows**e, em seguida, escolha **locais**. (Teclado: Alt + 4).  
  
  ![Janela locais](../debugger/media/dbg-basics-localswindow.png "DBG_Basics_LocalsWindow")  
  
  As janelas de variáveis locais é uma exibição de árvore dos parâmetros e variáveis da função. As propriedades de uma variável de objeto são nós filho do próprio objeto. O `this` variável é um parâmetro oculto em todos os métodos do objeto que representa o objeto em si. Nesse caso, ele representa a classe MainPage. Porque `methodTrack` é um membro do tipo de classe, seu valor e os dados da MainPage são listados em uma linha embaixo `this`. Expanda o `this` nó para exibir o `methodTrack` informações.  
  
  **Adicione uma inspeção para a variável methodTrack.** O `methodWatch` variável é usada em todo este guia de início rápido para mostrar os métodos chamados nos exemplos. Para tornar mais fácil de exibir o valor da variável, adicione-o para uma janela de observação. O nome da variável na janela locais com o botão direito e, em seguida, escolha **Adicionar inspeção**.  
  
  ![Janela de inspeção](../debugger/media/dbg-basics-watchwindow.png "DBG_Basics_WatchWindow")  
  
  Você pode inspecionar diversas variáveis em uma janela inspeção. Os valores de variáveis inspecionadas, como valores nas janelas de dica de dados e locais são atualizados sempre que a execução é suspensa. Você também pode adicionar variáveis à janela Inspeção do editor de códigos. Selecione a variável para assistir, direito do mouse e, em seguida, escolha **Adicionar inspeção**.  
  
##  <a name="BKMK_StepIntoOverOut"></a> Para failover e fora de métodos  
 Em contraste a entrar em um método chamado por um método pai, percorrendo um método executa o método filho e, em seguida, suspende a execução no método de chamada como o pai é retomada. Você pode entrar em um método quando você estiver familiarizado com a maneira como o método funciona e tiver certeza de que sua execução não afetará o problema que você está investigando.  
  
 Entrar em uma linha de código que não contém uma chamada de método executa a linha da mesma forma passo a passo para a linha.  
  
 Sair de um método filha continua a execução do método e, em seguida, suspende a execução após o método retornar para seu método de chamada. Você pode sair de uma função longa quando tiver determinado que o restante da função não é significativo.  
  
 Percorrendo tanto sair de uma função de executam a função.  
  
 ![Etapa em, sobre e sair de métodos](../debugger/media/dbg-basics-stepintooverout.png "DBG_Basics_StepIntoOverOut")  
  
### <a name="example-2"></a>Exemplo 2  
 Neste exemplo, você entrar, failover e fora de métodos.  
  
 **Chame o método Example2 no construtor MainPage.** Edite o construtor MainPage e substitua a linha após `methodTrack = String.Empty;` com `Example2();`.  
  
 ![Chame o método de Example2 do método Demo](../debugger/media/dbg-basics-callexample2.png "DBG_Basics_CallExample2")  
  
 **Execute o ponto de interrupção.** Iniciar a sessão de depuração, escolhendo **iniciar depuração** sobre o **depurar** menu (teclado: F5). O depurador suspende a execução no ponto de interrupção.  
  
 **Depurar a linha de código.** Sobre o **Debug** menu, escolha **Step Over** (teclado: F10). O depurador executa a `methodTrack = "MainPage";` instrução da mesma maneira como entrar na instrução.  
  
 **Etapa em Example2 e Example2_A.** Escolha a tecla F11 para percorrer o método de exemplo 2. Continuar entrar nas instruções Example2 até que a linha `int x = Example2_A();`. Entrar novamente, essa linha para mover para o ponto de entrada de Example2_A. Continue a entrar em cada instrução de Example2_A até voltar à Example2.  
  
 ![Example2](../debugger/media/dbg-basics-example2.png "DBG_Basics_Example2")  
  
 **Passe por uma função.** Observe que na próxima linha em Example2, `int y = Example2_A();` é basicamente o mesmo que a linha anterior. Você pode passar sobre essa linha com segurança. Escolha a tecla F10 para mover a retomada de Example2 para essa segunda chamada para Example2_A. Escolha F10 para passar por esse método. Observe que o `methodTrack` cadeia de caracteres que indica o método Example2_A foi executado duas vezes. Você também observará que o depurador se move imediatamente para a próxima linha. Ele não suspender a execução em retoma o Example2 ponto.  
  
 **Sair de uma função.** Escolha a tecla F11 para entrar no método Example2_B. Observe que não é muito diferente de Example2_A Example2_B. Para sair do método, escolha **depuração circular** sobre o **depurar** menus (teclado: Shift + F11). Observe que o `methodTrack` variável indica que Example2_B foi executado e que o depurador foi retornado para o ponto em que Example2 será retomada.  
  
 **Pare a depuração.** No menu Depurar, escolha Stop Debugging (teclado: Shift + F5). Isso encerra a sessão de depuração.  
  
##  <a name="BKMK_ConditionCursorVisualize"></a> Defina um ponto de interrupção condicional, executar até o cursor e visualizar uma variável  
 Um ponto de interrupção condicional Especifica uma condição que faz com que o depurador suspender a execução. A condição é especificada por uma expressão de código que pode ser avaliada como true ou false. Por exemplo, você pode usar um ponto de interrupção condicional para examinar o estado do programa em um método chamado com frequência apenas quando uma variável atinge um determinado valor.  
  
 Executar até o cursor é como configurar um único ponto de interrupção. Quando a execução for suspensa, você poderá selecionar uma linha na origem e retomar a execução até que a linha selecionada seja atingida. Por exemplo, você pode percorrer um loop em um método e determinar o código no loop está sendo executado corretamente. Em vez de percorrer cada iteração do loop, você pode executar até o cursor que é posicionado após o loop é executado.  
  
 Às vezes, é difícil de ler um valor de variável na linha de dica de dados ou janela variável. O depurador pode exibir cadeias de caracteres, HTML e Xml em um visualizador de texto que apresente uma exibição formatada do valor em uma janela rolável.  
  
### <a name="example-3"></a>Exemplo 3:  
 Neste exemplo, você deve definir um ponto de interrupção condicional para parar em uma iteração específica de um loop e, em seguida, executar até o cursor posicionado após o loop. Você também pode exibir o valor de uma variável em um visualizador de texto.  
  
 **Chame o método Example3 no construtor MainPage.** Edite o construtor MainPage e substitua a linha após `methodTrack = String.Empty;` com a linha `Example3();`.  
  
 ![Chamar Example3 do método Demo](../debugger/media/dbg-basics-callexample3.png "DBG_Basics_CallExample3")  
  
 **Execute o ponto de interrupção.** Iniciar a sessão de depuração, escolhendo **iniciar depuração** sobre o **depurar** menu (teclado: F5). O depurador suspende a execução no ponto de interrupção no método MainPage.  
  
 **Etapa no método Example3.** Escolher **intervir** sobre o **depurar** menu (teclado: F11) para mover para o ponto de entrada do método Example3. Continue entrando no método até ter iterado um ou dois loops do `for` bloco. Observe que ele levaria muito tempo para percorrer todas as 1.000 iterações.  
  
 **Defina um ponto de interrupção condicional.** Na medianiz esquerda da janela de código, clique na linha `x += i;` e, em seguida, escolha **condição**. Escolha o **condição** caixa de seleção e, em seguida, digite `i == 500;` na caixa de texto. Escolha o **vale** opção e escolha **Okey**. O ponto de interrupção permite verificar o valor à 500ª iteração do loop `for`.  
  
 ![Caixa de diálogo de condição de ponto de interrupção](../debugger/media/dbg-basics-breakpointcondition.png "DBG_Basics_BreakpointCondition")  
  
 Você pode identificar um ícone de ponto de interrupção condicional pela sua cruz branca.  
  
 ![Ponto de interrupção condicional](../debugger/media/dbg-basics-conditionalbreakpoint.png "DBG_Basics_ConditionalBreakpoint")  
  
 **Execute o ponto de interrupção.** No menu Depurar, escolha continuar (teclado: F5). Na janela locais, confirme se o valor atual da `i` é 500. Observe que a variável `s` é representada como uma linha e é muito mais do que a janela.  
  
 **Visual de uma variável de cadeia de caracteres.** Clique no ícone de lupa na **valor** coluna o `s`.  
  
 A janela do Visualizador de texto é exibida e o valor da cadeia de caracteres é apresentado como uma cadeia de caracteres de várias linha.  
  
 **Execute até o cursor.** Clique na linha `methodTrack += "->Example3";` e, em seguida, escolha **executar até o Cursor** (teclado: mova o cursor para a linha. CTRL + F10). O depurador conclui as iterações do loop e então suspende a execução na linha.  
  
 **Pare a depuração.** No menu Depurar, escolha Stop Debugging (teclado: Shift + F5). Isso encerra a sessão de depuração.  
  
##  <a name="BKMK_EditContinueRecoverExceptions"></a> Editar e continuar, se recuperar de uma exceção  
 Em algumas circunstâncias, quando você entrar no código no depurador do Visual Studio, você tem a oportunidade de alterar o valor de variáveis e até mesmo a lógica de instruções. Essa funcionalidade é chamada de editar e continuar.  
  
 Editar e continuar pode ser especialmente útil quando você interromper uma exceção. Em vez de precisar parar e reiniciar a depuração de um procedimento longo e complicado para evitar a exceção, você pode "desenrolar" a exceção para mover a execução para o ponto imediatamente antes que a exceção ocorreu e, em seguida, altere a variável incorreto ou a instrução e Continue com a sessão de depuração atual no estado que não gera uma exceção.  
  
 Embora você possa usar Editar e continuar em uma ampla variedade de situações, as condições específicas que não dão suporte a editar e continuar são difíceis de especificar como as condições dependem da linguagem de programação, o estado atual da pilha do programa e o capacidade do depurador para alterar o estado sem corromper o processo. A melhor maneira de determinar se há suporte para uma alteração de edição é experimentá-la; o depurador informa imediatamente se não há suporte para a alteração.  
  
### <a name="example-4"></a>Exemplo 4  
 Neste exemplo, você executar o depurador a uma exceção, retroceder a exceção, corrija a lógica do método e, em seguida, altere o valor de uma variável para que você possa continuar a execução do método.  
  
 **Chame o método Example4 no construtor MainPage.** Edite o construtor MainPage() e substitua a linha após `methodTrack = String.Empty;` com a linha `Example4();`.  
  
 ![Chamar Example4 do método Demo](../debugger/media/dbg-basics-callexample4.png "DBG_Basics_CallExample4")  
  
 **Execute a exceção.** Iniciar a sessão de depuração, escolhendo **iniciar depuração** sobre o **depurar** menu (teclado: F5). Pressione F5 novamente para retomar a execução. O depurador suspende a execução na exceção no método Example4 e exibe uma caixa de diálogo de exceção.  
  
 ![Caixa de diálogo de exceção](../debugger/media/dbg-basics-exceptiondlg.png "DBG_Basics_ExceptionDlg")  
  
 **Altere a lógica do programa.** É óbvio que o erro está no `if` condição: o valor da `x` deve ser alterado quando `x` é igual a 0; quando não `x` não é igual a zero. Escolher **quebrar** para corrigir a lógica do método. Quando você tentar editar a linha, outra caixa de diálogo é exibida.  
  
 ![Caixa de diálogo Editar e continuar](../debugger/media/dbg-basics-editandcontinuedlg.png "DBG_Basics_EditAndContinueDlg")  
  
 Escolher **edite** e, em seguida, altere a linha `if (x != 0)` para `if (x == 0)`. O depurador mantém as alterações para a lógica do programa para o arquivo de origem.  
  
 **Altere o valor da variável.** Examinar o valor de `x` em uma dica de dados ou na janela locais. Ainda é 0 (zero). Se você tentar executar a instrução que causou a exceção original, ele só gerará novamente. Você pode alterar o valor de `x`. Na janela locais, clique duas vezes o **valor** coluna o **x** linha. Altere o valor de 0 a 1.  
  
 ![Editar um valor na janela locais](../debugger/media/dbg-basics-editandcontinuefix.png "DBG_Basics_EditAndContinueFix")  
  
 Escolha a tecla F11 para percorrer a instrução que anteriormente gerava uma exceção. Observe que a linha é executada sem erros. Escolha F11 novamente.  
  
 **Pare a depuração.** Sobre o **Debug** menu, escolha **parar depuração** (teclado: Shift + F5). Isso encerra a sessão de depuração.  
  
## <a name="see-also"></a>Consulte também  
 [Iniciar uma sessão de depuração (VB, c#, C++ e XAML)](../debugger/start-a-debugging-session-for-a-store-app-in-visual-studio-vb-csharp-cpp-and-xaml.md)   
 [Disparar de suspender, continuar e eventos para Windows Store em segundo plano)](../debugger/how-to-trigger-suspend-resume-and-background-events-for-windows-store-apps-in-visual-studio.md)   
 [Depurar aplicativos no Visual Studio](../debugger/debug-store-apps-in-visual-studio.md)



