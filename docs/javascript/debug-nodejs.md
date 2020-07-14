---
title: Depurar um aplicativo JavaScript ou TypeScript
description: O Visual Studio fornece suporte para depuração de aplicativos JavaScript e TypeScript no Visual Studio
ms.date: 11/01/2019
ms.topic: how-to
ms.devlang: javascript
author: mikejo5000
ms.author: mikejo
manager: jillfra
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: 801ea23430d13dbefd9498c57b07881235275961
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85285186"
---
# <a name="debug-a-javascript-or-typescript-app-in-visual-studio"></a>Depurar um aplicativo JavaScript ou TypeScript no Visual Studio

Depure o código JavaScript e TypeScript usando o Visual Studio. Defina e atinja pontos de interrupção, anexe o depurador, inspecione variáveis, exiba a pilha de chamadas e use outras funcionalidades de depuração.

> [!TIP]
> Se você ainda não instalou o Visual Studio, vá para a página de [downloads do Visual Studio](https://visualstudio.microsoft.com/downloads/) para instalá-lo gratuitamente. Dependendo do tipo de desenvolvimento de aplicativo que você estiver fazendo, talvez você precise instalar a **carga de trabalho de desenvolvimento em Node.js** com o Visual Studio.

## <a name="debug-server-side-script"></a>Depurar um script do servidor

1. Com o projeto aberto no Visual Studio, abra um arquivo JavaScript do servidor (como *server.js*), clique na medianiz da medianiz esquerda para definir um ponto de interrupção:

    ![Definir um ponto de interrupção](../javascript/media/tutorial-nodejs-react-set-breakpoint.png)

    Pontos de interrupção são o recurso mais básico e essencial da depuração confiável. Um ponto de interrupção indica quando o Visual Studio deve suspender o código em execução para que você possa examinar os valores das variáveis ou o comportamento de memória ou se uma ramificação de código está sendo executada ou não.

1. Para executar o aplicativo, pressione **F5** (**Depurar** > **Iniciar Depuração**).

    O depurador pausa no ponto de interrupção definido (a instrução atual é marcada em amarelo). Agora, você pode inspecionar o estado do aplicativo passando o mouse sobre as variáveis que estão no escopo, usando as janelas do depurador, como **Locais** e **Inspecionar**.

1. Pressione **F5** para continuar o aplicativo.

1. Caso deseje usar as Ferramentas para Desenvolvedores do Chrome ou as Ferramentas F12, pressione **F12**. Você pode usar essas ferramentas para examinar o DOM e interagir com o aplicativo usando o Console do JavaScript.

## <a name="debug-client-side-script"></a>Depurar um script do lado do cliente

::: moniker range=">=vs-2019"
O Visual Studio fornece suporte de depuração do lado do cliente somente para Chrome e Microsoft Edge (Chromium). Em alguns cenários, o depurador atinge automaticamente os pontos de interrupção no código JavaScript e TypeScript e em scripts inseridos em arquivos HTML. Para depurar o script do lado do cliente em aplicativos ASP.NET, consulte a postagem do blog [Depurar JavaScript no Microsoft Edge](https://devblogs.microsoft.com/visualstudio/debug-javascript-in-microsoft-edge-from-visual-studio/) e esta [postagem para o Google Chrome](https://devblogs.microsoft.com/aspnet/client-side-debugging-of-asp-net-projects-in-google-chrome). Para depurar o TypeScript no ASP.NET Core, consulte também [criar um aplicativo ASP.NET Core com TypeScript](tutorial-aspnet-with-typescript.md).
::: moniker-end
::: moniker range="vs-2017"
O Visual Studio fornece suporte de depuração do lado do cliente somente para Chrome e Internet Explorer. Em alguns cenários, o depurador atinge automaticamente os pontos de interrupção no código JavaScript e TypeScript e em scripts inseridos em arquivos HTML. Para depurar o script do lado do cliente em aplicativos ASP.NET, consulte a postagem do blog [depuração do lado do cliente de projetos do ASP.net no Google Chrome](https://devblogs.microsoft.com/aspnet/client-side-debugging-of-asp-net-projects-in-google-chrome/).
::: moniker-end

Para aplicativos que não sejam o ASP.NET, siga as etapas descritas aqui.

### <a name="prepare-your-app-for-debugging"></a>Preparar seu aplicativo para depuração

Se a fonte for minificada ou criada por um transcompilador como o TypeScript ou o Babel, o uso de [mapas de origem](#generate_source_maps) será necessário para proporcionar a melhor experiência de depuração. Sem mapas de origem, você ainda poderá anexar o depurador a um script do lado do cliente em execução. No entanto, você só poderá definir e atingir pontos de interrupção no arquivo minificado ou transcompilado, não no arquivo de origem original. Por exemplo, em um aplicativo Vue.js, o script minificado é passado como uma cadeia de caracteres para uma instrução `eval`, e não há nenhuma maneira de executar esse código em etapas com eficiência usando o depurador do Visual Studio, a menos que você use mapas de origem. Em cenários de depuração complexos, você também pode usar o Chrome Ferramentas para Desenvolvedores ou as ferramentas F12 para o Microsoft Edge.

Para obter ajuda para gerar mapas de origem, consulte [gerar mapas de origem para depuração](#generate_source_maps).

### <a name="prepare-the-browser-for-debugging"></a><a name="prepare_the_browser_for_debugging"></a>Preparar o navegador para depuração

::: moniker range=">=vs-2019"
Para este cenário, use o Microsoft Edge (Chromium), atualmente chamado de **Microsoft Edge beta** no IDE ou Chrome.
::: moniker-end
::: moniker range="vs-2017"
Para este cenário, use o Chrome.
::: moniker-end

1. Feche todas as janelas do navegador de destino.

   Outras instâncias do navegador podem impedir que o navegador seja aberto com a depuração habilitada. (As extensões do navegador podem estar em execução e impedindo o modo de depuração completa, portanto, talvez seja necessário abrir o Gerenciador de tarefas para localizar instâncias inesperadas do Chrome.)

   ::: moniker range=">=vs-2019"
   Para o Microsoft Edge (Chromium), também Desligue todas as instâncias do Chrome. Como ambos os navegadores usam a base de código Chromium, isso fornece os melhores resultados.
   ::: moniker-end

2. Inicie seu navegador com a depuração habilitada.

    ::: moniker range=">=vs-2019"
    A partir do Visual Studio 2019, você pode definir o `--remote-debugging-port=9222` sinalizador na inicialização do navegador selecionando **procurar com...** > na barra de ferramentas de **depuração** , escolhendo **Adicionar**e, em seguida, definindo o sinalizador no campo **argumentos** . Use um nome amigável diferente para o navegador, como **borda com depuração** ou **Chrome com depuração**. Para obter detalhes, confira [Notas sobre a versão](/visualstudio/releases/2019/release-notes-v16.2).

    ![Definir o navegador para abrir com a depuração habilitada](../javascript/media/tutorial-nodejs-react-edge-with-debugging.png)

    Como alternativa, abra o comando **executar** no botão **Iniciar** do Windows (clique com o botão direito do mouse e escolha **executar**) e digite o seguinte comando:

    `msedge --remote-debugging-port=9222`

    ou

    `chrome.exe --remote-debugging-port=9222`
    ::: moniker-end

    ::: moniker range="vs-2017"
    Abra o comando **Executar** do botão **Iniciar** do Windows (clique com o botão direito do mouse e escolha **Executar**) e digite o seguinte comando:

    `chrome.exe --remote-debugging-port=9222`
    ::: moniker-end

    Isso inicia o navegador com a depuração habilitada.

    O aplicativo ainda não está em execução e, portanto, você obtém uma página vazia do navegador.

### <a name="attach-the-debugger-to-client-side-script"></a>Anexar o depurador ao script do lado do cliente

Para anexar o depurador do Visual Studio e clicar em pontos de interrupção no código do lado do cliente, o depurador precisa de ajuda para identificar o processo correto. Esta é uma maneira de permitir isso.

1. Alterne para o Visual Studio e defina um ponto de interrupção no código-fonte, que pode ser um arquivo JavaScript, um arquivo TypeScript ou um arquivo JSX. (Defina o ponto de interrupção em uma linha de código que permite pontos de interrupção, como uma instrução de retorno ou uma declaração var.)

    ![Definir um ponto de interrupção](../javascript/media/tutorial-nodejs-react-set-breakpoint-client-code.png)

    Para localizar o código específico em um arquivo transcompilado, use **Ctrl** + **F** (**Editar**  >  **Localizar e substituir**  >  **localização rápida**).

    Para o código do lado do cliente, para atingir um ponto de interrupção em um arquivo TypeScript, *. Vue*ou JSX normalmente requer o uso de [mapas de origem](#generate_source_maps). Um mapa de origem deve ser configurado corretamente para dar suporte à depuração no Visual Studio.

2. Selecione o navegador de destino como o destino de depuração no Visual Studio e pressione **Ctrl** + **F5** (**depurar**  >  **Iniciar sem depuração**) para executar o aplicativo no navegador.

    ::: moniker range=">=vs-2019"
    Se você criou uma configuração de navegador com um nome amigável, escolha-a como seu destino de depuração.
    ::: moniker-end

    O aplicativo será aberto em uma nova guia do navegador.

3. Escolha **depuração**  >  **anexar ao processo**.

    > [!TIP]
    > A partir do Visual Studio 2017, depois de anexar ao processo pela primeira vez seguindo estas etapas, você pode reanexar rapidamente ao mesmo processo escolhendo **depurar**  >  **reanexar para processar**.

4. Na caixa de diálogo **anexar ao processo** , obtenha uma lista filtrada de instâncias do navegador às quais você pode anexar.
    ::: moniker range=">=vs-2019"
    No Visual Studio 2019, escolha o depurador correto para seu navegador de destino, **JavaScript (Chrome)** ou **JavaScript (Microsoft Edge-Chromium)** no campo **anexar a** , digite **Chrome** ou **Edge** na caixa de filtro para filtrar os resultados da pesquisa.
    ::: moniker-end
    ::: moniker range="vs-2017"
    No Visual Studio 2017, escolha **código WebKit** no campo **anexar a** , digite **Chrome** na caixa de filtro para filtrar os resultados da pesquisa.
    ::: moniker-end

5. Selecione o processo de navegador com a porta de host correta (localhost neste exemplo) e selecione **anexar**.

    A porta (por exemplo, 1337) também pode aparecer no campo **título** para ajudá-lo a selecionar a instância correta do navegador.

    ::: moniker range=">=vs-2019"
    O exemplo a seguir mostra como isso se parece com o navegador Microsoft Edge (Chromium).

    ![Anexar ao processo](../javascript/media/tutorial-nodejs-react-attach-to-process-edge.png)
    ::: moniker-end
    ::: moniker range="vs-2017"
    ![Anexar ao processo](../javascript/media/tutorial-nodejs-react-attach-to-process.png)

    Você sabe que o depurador foi anexado corretamente quando o Explorador do DOM e o Console do JavaScript são abertos no Visual Studio. Essas ferramentas de depuração são semelhantes às Ferramentas para Desenvolvedores do Chrome e às Ferramentas F12 do Microsoft Edge.
    ::: moniker-end

    > [!TIP]
    > Se o depurador não anexar e você vir a mensagem "falha ao iniciar o adaptador de depuração" ou "não é possível anexar ao processo. Uma operação não é válida no estado atual. ", use o Gerenciador de tarefas do Windows para fechar todas as instâncias do navegador de destino antes de iniciar o navegador no modo de depuração. As extensões de navegador podem estar em execução e impedindo o modo de depuração completa.

6. Como o código com o ponto de interrupção pode já ter sido executado, atualize a página do navegador. Se necessário, tome medidas para fazer com que o código com o ponto de interrupção seja executado.

    Enquanto estiver em pausa no depurador, você pode examinar o estado do aplicativo passando o mouse sobre as variáveis e usando as janelas do depurador. Você pode avançar o depurador percorrendo o código (**F5**, **F10** e **F11**). Para obter mais informações sobre os recursos básicos de depuração, consulte [primeira olhada no depurador](../debugger/debugger-feature-tour.md).

    Você pode atingir o ponto de interrupção em um arquivo *. js* ou arquivo de origem transcompilado, dependendo de seu tipo de aplicativo, que etapas você seguiu anteriormente e outros fatores, como o estado do navegador. De qualquer forma, você pode percorrer o código e examinar as variáveis.

   * Se você precisar dividir o código em um arquivo de origem TypeScript, JSX ou *. Vue* e não puder fazê-lo, verifique se o seu ambiente está configurado corretamente, conforme descrito na seção solução de [problemas](#troubleshooting_source_maps) .

   * Se você precisar dividir o código em um arquivo JavaScript transcompilado (por exemplo, *app-bundle.js*) e não puder fazê-lo, remova o arquivo do mapa de origem, *filename.js. map*.

### <a name="troubleshooting-breakpoints-and-source-maps"></a><a name="troubleshooting_source_maps"></a>Solucionando problemas de pontos de interrupção e mapas de origem

Se você precisar dividir o código em um arquivo de origem TypeScript ou JSX e não puder fazê-lo, use **anexar ao processo** conforme descrito nas etapas anteriores para anexar o depurador. Verifique se o seu ambiente está configurado corretamente:

* Você fechou todas as instâncias de navegador, incluindo as extensões Chrome (usando o Gerenciador de tarefas), para que você possa executar o navegador no modo de depuração.
      
* Certifique-se [de iniciar o navegador no modo de depuração](#prepare_the_browser_for_debugging).

* Verifique se o arquivo de mapa de origem inclui o caminho relativo correto para o arquivo de origem e se ele não inclui prefixos sem suporte, como *webpack:///*, que impede que o depurador do Visual Studio Localize um arquivo de origem. Por exemplo, uma referência como *webpack:///.app.TSX* pode ser corrigida para *./app.TSX*. Você pode fazer isso manualmente no arquivo do mapa de origem (que é útil para teste) ou por meio de uma configuração de compilação personalizada. Para obter mais informações, consulte [gerar mapas de origem para depuração](#generate_source_maps).

Como alternativa, se você precisar dividir o código em um arquivo de origem (por exemplo, *app. TSX*) e não puder fazê-lo, tente usar a `debugger;` instrução no arquivo de origem ou definir pontos de interrupção no Chrome ferramentas para desenvolvedores (ou as ferramentas F12 para o Microsoft Edge) em vez disso.

## <a name="generate-source-maps-for-debugging"></a><a name="generate_source_maps"></a> Gerar mapas de origem para depuração

O Visual Studio tem a capacidade de usar e gerar mapas de origem em arquivos de origem JavaScript. Isso costuma ser necessário se a fonte é minificada ou criada por um transcompilador como o TypeScript ou o Babel. As opções disponíveis dependem do tipo de projeto.

* Por padrão, um projeto TypeScript no Visual Studio gera mapas de origem para você. Para obter mais informações, consulte [Configurar mapas de origem usando um tsconfig.jsno arquivo](#configure_source_maps).

* Em um projeto JavaScript, você pode gerar mapas de origem usando um Agrupador como webpack e um compilador como o compilador TypeScript (ou Babel), que pode ser adicionado ao seu projeto. Para o compilador TypeScript, você também deve adicionar um *tsconfig.jsno* arquivo e definir a `sourceMap` opção do compilador. Para obter um exemplo que mostra como fazer isso usando uma configuração básica de webpack, confira [Criar um aplicativo Node.js com o React](../javascript/tutorial-nodejs-with-react-and-jsx.md).

> [!NOTE]
> Caso não esteja familiarizado com mapas de origem, leia [Introduction to JavaScript Source Maps](https://www.html5rocks.com/en/tutorials/developertools/sourcemaps/) (Introdução a mapas de origem JavaScript) antes de continuar. 

Para definir configurações avançadas para mapas de origem, use um *tsconfig.json* ou as configurações do projeto em um projeto TypeScript, mas não ambos.

Para habilitar a depuração usando o Visual Studio, você precisa verificar se as referências ao arquivo de origem no mapa de origem gerado estão corretas (isso pode exigir testes). Por exemplo, se você estiver usando o webpack, as referências no arquivo do mapa de origem incluem o prefixo *webpack:///* , que impede que o Visual Studio Localize um arquivo de origem TYPESCRIPT ou JSX. Especificamente, quando você corrige isso para fins de depuração, a referência ao arquivo de origem (como *app. TSX*) deve ser alterada de algo como *webpack:///./app.TSX* para algo como *./app.TSX*, que habilita a depuração (o caminho é relativo ao arquivo de origem). O exemplo a seguir mostra como você pode configurar mapas de origem no webpack, que é um dos pacotes mais comuns, para que eles funcionem com o Visual Studio.

(Somente webpack) Se você estiver definindo o ponto de interrupção em um TypeScript de arquivo JSX (em vez de um arquivo JavaScript transcompilado), precisará atualizar sua configuração do webpack. Por exemplo, em *webpack-config.js*, talvez seja necessário substituir o seguinte código:

```javascript
  output: {
    filename: "./app-bundle.js", // This is an example of the filename in your project
  },
```

por este código:

```javascript
  output: {
    filename: "./app-bundle.js", // Replace with the filename in your project
    devtoolModuleFilenameTemplate: '[resource-path]'  // Removes the webpack:/// prefix
  },
```

Essa é uma configuração somente de desenvolvimento para habilitar a depuração do código do lado do cliente no Visual Studio.

Para cenários complicados, as ferramentas de navegador (**F12**) às vezes funcionam melhor para depuração, pois não exigem alterações em prefixos personalizados.

### <a name="configure-source-maps-using-a-tsconfigjson-file"></a><a name="configure_source_maps"></a>Configurar mapas de origem usando um tsconfig.jsno arquivo

Se você adicionar um arquivo *tsconfig.json* ao projeto, o Visual Studio tratará a raiz do diretório como um projeto TypeScript. Para adicionar o arquivo, clique com o botão direito do mouse em seu projeto no Gerenciador de Soluções e escolha **adicionar > novo Item > arquivo de configuração JSON do TypeScript**. Um arquivo *tsconfig.json* como o mostrado a seguir é adicionado ao projeto.

```json
{
  "compilerOptions": {
    "noImplicitAny": false,
    "noEmitOnError": true,
    "removeComments": false,
    "sourceMap": true,
    "target": "es5"
  },
  "exclude": [
    "node_modules",
    "wwwroot"
  ]
}
```

#### <a name="compiler-options-for-tsconfigjson"></a>Opções do compilador para tsconfig.json

* **inlineSourceMap**: emitir um único arquivo com mapas de origem em vez de criar um mapa de origem separado para cada arquivo de origem.
* **inlineSources**: emitir a origem junto com os mapas de origem em um único arquivo; requer a definição de *inlineSourceMap* ou *sourceMap* .
* **mapRoot**: especifica o local em que o depurador deve localizar arquivos de mapa de origem (*. map*) em vez do local padrão. Use esse sinalizador se os arquivos *.map* em tempo de execução precisarem estar em uma localização diferente dos arquivos *.js*. A localização especificada é inserida no mapa de origem para direcionar o depurador à localização dos arquivos *.map*.
* **sourceMap**: gera um arquivo *. map* correspondente.
* **sourceRoot**: especifica o local em que o depurador deve localizar arquivos TypeScript em vez dos locais de origem. Use esse sinalizador se as origens em tempo de execução precisarem estar em uma localização diferente da localização em tempo de design. A localização especificada é inserida no mapa de origem para direcionar o depurador ao local em que se encontram os arquivos de origem.

Para obter mais detalhes sobre as opções do compilador, confira a página [Opções do compilador](https://www.typescriptlang.org/docs/handbook/compiler-options.html) no Manual do TypeScript.

### <a name="configure-source-maps-using-project-settings-typescript-project"></a>Configurar mapas de origem usando configurações de projeto (projeto TypeScript)

Defina também as configurações de mapa de origem usando as propriedades do projeto clicando com o botão direito do mouse no projeto e, em seguida, escolhendo **Projeto > Propriedades > Build TypeScript > Depuração**.

Estas configurações do projeto estão disponíveis.

* **Gerar mapas de origem** (equivalente **a sourceMap** em *tsconfig.jsem*): gera o arquivo *. map* correspondente.
* **Especificar o diretório raiz dos mapas de origem** (equivalente a **mapRoot** em *tsconfig.jsem*): especifica o local onde o depurador deve encontrar arquivos de mapa em vez dos locais gerados. Use esse sinalizador se os arquivos *.map* em tempo de execução precisarem estar em uma localização diferente dos arquivos .js. A localização especificada é inserida no mapa de origem para direcionar o depurador ao local em que se encontram os arquivos de mapa.
* **Especificar o diretório raiz de arquivos TypeScript** (equivalente a **sourceRoot** no *tsconfig.js*): especifica o local em que o depurador deve localizar arquivos TypeScript em vez de locais de origem. Use esse sinalizador se os arquivos de origem em tempo de execução precisarem estar em uma localização diferente da localização em tempo de design. A localização especificada é inserida no mapa de origem para direcionar o depurador ao local em que se encontram os arquivos de origem.

## <a name="debug-javascript-in-dynamic-files-using-razor-aspnet"></a>Depurar JavaScript em arquivos dinâmicos usando o Razor (ASP.NET)

::: moniker range=">=vs-2019"
A partir do Visual Studio 2019, o Visual Studio fornece suporte de depuração somente para Chrome e Microsoft Edge (Chromium).
::: moniker-end
::: moniker range="vs-2017"
O Visual Studio fornece suporte de depuração somente para o Chrome e o Internet Explorer.
::: moniker-end

No entanto, você não pode acessar automaticamente pontos de interrupção em arquivos gerados com sintaxe Razor (cshtml, vbhtml). Há duas abordagens que podem ser usadas para depurar esse tipo de arquivo:

* **Coloque a `debugger;` instrução onde você deseja interromper**: isso faz com que o script dinâmico interrompa a execução e inicie a depuração imediatamente enquanto ele está sendo criado.
* **Carregar a página e abrir o documento dinâmico no Visual Studio**: você precisará abrir o arquivo dinâmico durante a depuração, definir seu ponto de interrupção e atualizar a página para que esse método funcione. Dependendo se você estiver usando o Chrome ou o Internet Explorer, você encontrará o arquivo usando uma das seguintes estratégias:

   Para o Chrome, acesse **Gerenciador de Soluções > Documentos de Script > NomeDaPágina**.

    > [!NOTE]
    > Ao usar o Chrome, você pode receber uma mensagem **nenhuma fonte está disponível entre \<script> marcas**. Não se preocupe. Basta continuar a depuração.

   ::: moniker range=">=vs-2019"
   Para o Microsoft Edge (Chromium), use o mesmo procedimento que o Chrome.
   ::: moniker-end

   ::: moniker range="vs-2017"
   Para o Internet Explorer, acesse **Gerenciador de Soluções > Documentos de Script > Windows Internet Explorer > NomeDaPágina**.
   ::: moniker-end

Para obter mais informações, confira [Depuração do lado do cliente de projetos ASP.NET no Google Chrome](https://devblogs.microsoft.com/aspnet/client-side-debugging-of-asp-net-projects-in-google-chrome/).
