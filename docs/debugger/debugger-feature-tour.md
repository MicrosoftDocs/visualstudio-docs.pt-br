---
title: Introdução à depuração no VS 2017
description: Introdução à depuração de aplicativos usando o depurador do Visual Studio
ms.custom: mvc
ms.date: 06/15/2018
ms.technology: vs-ide-debug
ms.topic: quickstart
helpviewer_keywords:
- debugger
ms.assetid: c763d706-3213-494f-b4d2-990b6e1ec456
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: d5c479251b7002e506f1dff5e64a028875aa8f80
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49882660"
---
# <a name="first-look-at-the-visual-studio-debugger"></a>Introdução ao Depurador do Visual Studio

Este tópico apresenta as ferramentas de depurador fornecidas pelo Visual Studio. No contexto do Visual Studio, quando você *depura seu aplicativo*, significa que você está executando o aplicativo com o depurador anexado (ou seja, no modo de depurador). Quando você faz isso, o depurador fornece várias maneiras de mostrar o que o código está fazendo enquanto é executado. Você pode percorrer o código e examinar os valores armazenados em variáveis, definir inspeções em variáveis para ver quando os valores mudam, examinar o caminho de execução do código e assim por diante. Se esta é sua primeira tentativa de depurar um código, leia [Como depurar para iniciantes absolutos](../debugger/debugging-absolute-beginners.md) antes continuar neste tópico.

Os recursos descritos aqui são aplicáveis a C#, C++, Visual Basic, JavaScript e a outras linguagens compatíveis com o Visual Studio (exceto quando indicado).

## <a name="set-a-breakpoint-and-start-the-debugger"></a>Definir um ponto de interrupção e iniciar o depurador

Para depurar, você precisa iniciar o aplicativo com o depurador anexado ao processo do aplicativo. **F5** (**Depurar > Iniciar Depuração**) é a maneira mais comum de fazer isso. No entanto, talvez você ainda não definiu pontos de interrupção para examinar o código do seu aplicativo, portanto faremos isso primeiro e, em seguida, iniciaremos a depuração. Pontos de interrupção são o recurso mais básico e essencial da depuração confiável. Um ponto de interrupção indica quando o Visual Studio deve suspender o código em execução para que você possa examinar os valores das variáveis ou o comportamento de memória ou se uma ramificação de código está sendo executada ou não. 

Se você tem um arquivo aberto no editor de código, é possível definir um ponto de interrupção clicando na margem à esquerda de uma linha de código.

![Definir um ponto de interrupção](../debugger/media/dbg-tour-set-a-breakpoint.gif "Definir um ponto de interrupção")

Pressione **F5** (**Depurar > Iniciar Depuração**) ou o botão **Iniciar Depuração** ![Iniciar Depuração](../debugger/media/dbg-tour-start-debugging.png "Iniciar Depuração") na barra de ferramentas Depurar e o depurador será executado até o primeiro ponto de interrupção que encontrar. Se o aplicativo ainda não estiver em execução, F5 iniciará o depurador e o interromperá no primeiro ponto de interrupção.

Os pontos de interrupção são um recurso útil quando você sabe qual linha ou seção de código deseja examinar em detalhes.

## <a name="navigate"></a> Navegar pelo código no depurador usando comandos de etapa

Nós fornecemos os atalhos de teclado para a maioria dos comandos porque eles tornam a navegação pelo código do aplicativo mais rápida. (Os comandos equivalentes, como comandos de menu, são mostrados entre parênteses).

Para iniciar seu aplicativo com o depurador anexado, pressione **F11** (**Depurar > Intervir**). F11 é o comando **Intervir**, que avança a execução do aplicativo uma instrução por vez. Quando você inicia o aplicativo com F11, o depurador é interrompido na primeira instrução que é executada.

![F11 Intervir](../debugger/media/dbg-tour-f11.png "F11 Intervir")

A seta amarela representa a instrução na qual o depurador ficou em pausa, que também suspende a execução do aplicativo no mesmo ponto (essa instrução ainda não foi executada).

F11 é uma boa maneira de examinar o fluxo de execução com o máximo de detalhes. (Também vamos mostrar algumas outras opções para percorrer o código com mais rapidez). Por padrão, o depurador ignora as partes do código que não são do usuário (se quiser saber mais detalhes, confira [Apenas Meu Código](../debugger/just-my-code.md)).

>[!NOTE]
> No código gerenciado, você verá uma caixa de diálogo perguntando se deseja ser notificado quando passar automaticamente por propriedades e operadores (comportamento padrão). Se você quiser alterar a configuração depois, desabilite a configuração **Passar por propriedades e operadores** no menu **Ferramentas > Opções** em **Depuração**.

## <a name="step-over-code-to-skip-functions"></a>Passar pelo código para ignorar funções

Quando você estiver em uma linha de código que é uma chamada de função ou de método, poderá pressionar **F10** (**Depurar > Passar**) em vez de F11.

Pressionar F10 avança o depurador sem intervir em funções ou métodos no código do aplicativo (o código ainda é executado). Ao pressionar F10, será possível ignorar o código no qual você não está interessado. Dessa forma, você poderá chegar rapidamente no código que está mais interessado.

## <a name="step-into-a-property"></a>Intervir em uma propriedade

Como mencionado anteriormente, por padrão, o depurador ignora propriedades gerenciadas e campos, mas o comando **Intervir Específico** permite substituir esse comportamento.

Clique com o botão direito do mouse em uma propriedade ou um campo e escolha **Intervir Específico** e, em seguida, escolha uma das opções disponíveis.

![Intervir Específico](../debugger/media/dbg-tour-step-into-specific.png "Intervir Específico")

Neste exemplo, **Intervir Específico** nos leva ao código de `Path.set`.

![Intervir Específico](../debugger/media/dbg-tour-step-into-specific-2.png "Intervir Específico")

## <a name="run-to-a-point-in-your-code-quickly-using-the-mouse"></a>Executar rapidamente até um ponto no código usando o mouse

Enquanto estiver no depurador, passe o mouse sobre uma linha de código até que o botão **Executar com um Clique** (Realizar a execução até aqui) ![Executar com um Clique](../debugger/media/dbg-tour-run-to-click.png "RunToClick") apareça à esquerda.

![Executar com um Clique](../debugger/media/dbg-tour-run-to-click-2.png "Executar com um Clique")

> [!NOTE]
> O botão **Executar com um Clique** (Realizar a execução até aqui) é novo no [!include[vs_dev15](../misc/includes/vs_dev15_md.md)].

Clique no botão **Executar com um Clique** (Realizar a execução até aqui). O depurador avança até a linha de código em que você clicou.

O uso desse botão é semelhante à configuração de um ponto de interrupção temporário. Esse comando também é útil para percorrer rapidamente uma região visível do código do aplicativo. Você pode usar **Executar com um Clique** em qualquer arquivo aberto.

## <a name="advance-the-debugger-out-of-the-current-function"></a>Avançar o depurador para fora da função atual

Às vezes, talvez você queira continuar a sessão de depuração, avançando o depurador até o fim da função atual.

Pressione **Shift + F11** (ou **Depurar > Sair**).

Este comando retoma a execução do aplicativo (e avança o depurador) até que a função atual retorne.

## <a name="run-to-cursor"></a>Executar até o cursor

Pare o depurador pressionando o botão vermelho **Parar Depuração** ![Parar Depuração](../debugger/media/dbg-tour-stop-debugging.png "Parar Depuração") ou **Shift** + **F5**.

Clique com o botão direito do mouse em uma linha de código do seu aplicativo e escolha **Executar até o Cursor**. Esse comando inicia a depuração e define um ponto de interrupção temporário na linha de código atual.

![Executar até o Cursor](../debugger/media/dbg-tour-run-to-cursor.png "Executar até o Cursor")

Se você tiver definido pontos de interrupção, o depurador parará no primeiro ponto de interrupção que encontrar.

Pressione **F5** até alcançar a linha de código em que você selecionou **Executar até o Cursor**.

Esse comando é útil quando você está editando o código e deseja definir rapidamente um ponto de interrupção temporário e iniciar o depurador ao mesmo tempo.

> [!NOTE]
> Você pode usar **Executar até o Cursor** na janela **Pilha de Chamadas** enquanto está depurando.

## <a name="restart-your-app-quickly"></a>Reinicie o aplicativo rapidamente

Clique no botão **Reiniciar** ![Reiniciar Aplicativo](../debugger/media/dbg-tour-restart.png "Reiniciar Aplicativo") na barra de ferramentas Depurar (**Ctrl + Shift + F5**).

Ao pressionar **Reiniciar**, você economiza tempo em comparação com a opção de parar o aplicativo e reiniciar o depurador. O depurador é pausado no primeiro ponto de interrupção que é encontrado pela execução do código.

Se você quiser parar o depurador e voltar para o editor de código, poderá pressionar a o botão de parada ![Parar Depuração](../debugger/media/dbg-tour-stop-debugging.png "Parar Depuração") vermelho em vez de **Reiniciar**.

## <a name="inspect-variables-with-data-tips"></a>Inspecionar variáveis com dicas de dados

Agora que você sabe um pouco mais sobre a navegação, é uma boa oportunidade começar a inspecionar o estado do aplicativo (variáveis) com o depurador. Os recursos que permitem que você inspecione variáveis são alguns dos mais úteis do depurador e há diferentes maneiras de fazer isso. Muitas vezes, ao tentar depurar um problema, você tenta descobrir se as variáveis estão armazenando os valores que elas deveriam conter em um estado específico do aplicativo.

Com o depurador em pausa, passe o mouse sobre um objeto com o mouse e você verá o valor da propriedade padrão (neste exemplo, o nome do arquivo `market 031.jpg` é o valor da propriedade padrão).

![Exibir uma Dica de Dados](../debugger/media/dbg-tour-data-tips.gif "Exibir uma Dica de Dados")

Expanda o objeto para ver todas as suas propriedades (como a propriedade `FullPath` neste exemplo).

Muitas vezes, durante a depuração, queremos uma maneira rápida de verificar valores de propriedade em objetos e as dicas de dados são uma ótima maneira de fazer isso.

> [!TIP]
> Na maioria das linguagens compatíveis, você pode editar o código durante uma sessão de depuração. Para obter mais informações, confira [Editar e Continuar](../debugger/edit-and-continue.md).

## <a name="inspect-variables-with-the-autos-and-locals-windows"></a>Inspecionar variáveis com as janelas Autos e Locais

Durante a depuração, examine a janela **Autos** na parte inferior do editor de códigos.

![Janela Autos](../debugger/media/dbg-tour-autos-window.png "Janela Autos")

Na janela **Autos**, veja as variáveis, bem como seus valores atuais e os respectivos tipos. A janela **Autos** mostra todas as variáveis usadas na linha atual ou na linha anterior (No C++, a janela mostra as variáveis nas três linhas de código anteriores. Verifique a documentação para saber o comportamento específico a uma linguagem).

> [!NOTE]
> Em JavaScript, há compatibilidade com a janela **Locais**, mas não com a janela **Autos**.

Em seguida, examine a janela **Locais**. A janela **Locais** mostra as variáveis que estão no escopo no momento.

![Janela Locais](../debugger/media/dbg-tour-locals-window.png "Janela Locais")

Neste exemplo, o objeto `this` e o objeto `f` estão no escopo. Para obter mais informações, confira [Inspecionar variáveis nas janelas Locais e Autos](../debugger/autos-and-locals-windows.md).

## <a name="set-a-watch"></a>Definir uma inspeção

Você pode usar uma janela **Inspeção** para especificar uma variável (ou uma expressão) que deseja acompanhar.

Durante a depuração, clique com o botão direito do mouse em um objeto e escolha **Adicionar Inspeção**.

![Janela Inspeção](../debugger/media/dbg-tour-watch-window.png "Janela Inspeção")

Neste exemplo, há uma inspeção definida no objeto `f` e você pode ver seu valor sendo alterado, conforme percorre o depurador. Ao contrário das outras janelas de variáveis, a janela **Inspeção** sempre mostra as variáveis que você está inspecionando (eles ficam esmaecidas quando estão fora do escopo).

Para obter mais informações, confira [Definir uma Inspeção usando as janelas Inspeção e QuickWatch](../debugger/watch-and-quickwatch-windows.md)

## <a name="examine-the-call-stack"></a>Examinar a pilha de chamadas

Clique na janela **Pilha de Chamadas** durante a depuração, a qual fica aberta por padrão no painel inferior direito.

![Examinar a Pilha de Chamadas](../debugger/media/dbg-tour-call-stack.png "Examinar a Pilha de Chamadas")

A janela **Pilha de Chamadas** mostra a ordem em que os métodos e as funções são chamados. A linha superior mostra a função atual (o método `Update` neste exemplo). A segunda linha mostra que `Update` foi chamado por meio da propriedade `Path.set` e assim por diante. A pilha de chamadas é uma boa maneira de examinar e entender o fluxo de execução de um aplicativo.

> [!NOTE]
> A janela **Pilha de Chamadas** é semelhante à perspectiva de Depuração em alguns IDEs, como o Eclipse.

Você pode clicar duas vezes em uma linha de código para examinar esse código-fonte. Isso também altera o escopo atual que está sendo inspecionado pelo depurador. Isso não avança o depurador.

Você também pode usar os menus acessados ao clicar com o botão direito do mouse na janela **Pilha de Chamadas** para fazer outras coisas. Por exemplo, você pode inserir pontos de interrupção em funções especificas, reiniciar o aplicativo usando **Executar até o Cursor** e examinar o código-fonte. Confira [Como examinar a Pilha de Chamadas](../debugger/how-to-use-the-call-stack-window.md).

## <a name="exception"></a> Examinar uma exceção

Quando seu aplicativo gera uma exceção, o depurador leva você até a linha de código que lançou a exceção.

![Auxiliar de Exceção](../debugger/media/dbg-tour-exception-helper.png "Auxiliar de Exceção")

Neste exemplo, o **Auxiliar de Exceção** mostra uma exceção `System.Argument` e uma mensagem de erro que diz que o caminho não é um formato válido. Portanto, sabemos que o erro ocorreu em um método ou um argumento de função.

Neste exemplo, a chamada `DirectoryInfo` gerou o erro na cadeia de caracteres vazia armazenada na variável `value`.

O Auxiliar de Exceção é um ótimo recurso que pode ajudá-lo a depurar erros. Você também pode fazer coisas como exibir detalhes do erro e adicionar uma inspeção por meio do Auxiliar de Exceção. Ou, se necessário, você pode alterar as condições para lançar a exceção específica.

> [!NOTE]
> O Auxiliar de Exceção substitui o Assistente de Exceção no [!include[vs_dev15](../misc/includes/vs_dev15_md.md)].

Expanda o nó **Configurações de Exceção** para ver mais opções de como lidar com esse tipo de exceção, mas você não precisa alterar nada neste tour!

## <a name="debug-live-aspnet-apps-in-azure-app-service"></a>Depurar aplicativos ASP.NET dinâmicos no Serviço de Aplicativo do Azure

O **Depurador de Instantâneos** tira um instantâneo de seus aplicativos em produção quando o código no qual você está interessado é executado. Para instruir o depurador a tirar um instantâneo, defina snappoints e logpoints em seu código. O depurador permite ver exatamente o que deu errado sem afetar o tráfego do seu aplicativo de produção. O Depurador de Instantâneo pode ajudar a reduzir drasticamente o tempo que leva para resolver problemas que ocorrem em ambientes de produção.

![Iniciar o depurador de instantâneos](../debugger/media/snapshot-launch.png "Iniciar o Depurador de Instantâneos")

A coleção de instantâneos está disponível para aplicativos do ASP.NET em execução no Serviço de Aplicativo do Azure. Aplicativos ASP.NET devem estar em execução no .NET Framework 4.6.1 ou posterior e os aplicativos ASP.NET Core devem ser executados no .NET Core 2.0 ou posterior no Windows.

Para obter mais informações, confira [Depurar aplicativos ASP.NET dinâmicos usando o Depurador de Instantâneos](../debugger/debug-live-azure-applications.md).

## <a name="view-snapshots-with-intellitrace-step-back-visual-studio-enterprise"></a>Exibir instantâneos com o retrocesso do IntelliTrace (Visual Studio Enterprise)

O **retrocesso do IntelliTrace** tira automaticamente um instantâneo do seu aplicativo em cada evento de etapa do depurador e do ponto de interrupção. Os instantâneos registrados permitem retornar aos pontos de interrupção ou às etapas anteriores e exibir o estado do aplicativo como ele era no passado. O retrocesso do IntelliTrace poderá poupar seu tempo quando você desejar ver o estado do aplicativo anterior, mas não desejar reiniciar a depuração nem recriar o estado do aplicativo desejado.

É possível navegar e exibir instantâneos usando os botões **Voltar** e **Avançar** na barra de ferramentas Depurar. Esses botões navegam pelos eventos exibidos na guia **Eventos** na janela **Ferramentas de Diagnóstico**.

![Botões Voltar e Avançar Etapa](../debugger/media/intellitrace-step-back-icons-description.png  "Botões Voltar e Avançar Etapa")

Para obter mais informações, confira a página [Inspecionar estados anteriores do aplicativo usando o IntelliTrace](../debugger/view-historical-application-state.md).

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você obteve uma visão rápida de muitos recursos do depurador. Convém uma visão mais detalhada sobre esses recursos usando um aplicativo de exemplo

> [!div class="nextstepaction"]
> [Aprenda a depurar usando o Visual Studio](../debugger/getting-started-with-the-debugger.md)
