---
title: Visão geral para desenvolvedores de Visual Basic
description: Saiba como usar o Visual Studio para editar, depurar e compilar código e, em seguida, publicar um aplicativo como um desenvolvedor de Visual Basic.
ms.date: 03/02/2021
ms.technology: vs-ide-general
ms.custom:
- vs-acquisition
- get-started
- SEO-VS-2020
ms.topic: conceptual
author: TerryGLee
ms.author: tglee
manager: jmartens
dev_langs:
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 486201d61f6bd2d149c9aea66efee1814ce667e7
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112386625"
---
# <a name="welcome-to-the-visual-studio-ide--visual-basic"></a>Bem-vindo ao IDE do Visual Studio | Visual Basic

O *ambiente de desenvolvimento integrado* do Visual Studio é um painel de inicialização criativo que você pode usar para editar, depurar e compilar o código e, em seguida, publicar um aplicativo. Um IDE (ambiente de desenvolvimento integrado) é um programa repleto de recursos que pode ser usado por muitos aspectos do desenvolvimento de software. Além do editor e do depurador padrão fornecidos pela maioria dos IDEs, o Visual Studio inclui compiladores, ferramentas de preenchimento de código, designers gráficos e muitos outros recursos para facilitar o processo de desenvolvimento de software.

::: moniker range="vs-2017"

![O IDE do Visual Studio](../media/visual-studio-ide.png)

::: moniker-end

::: moniker range=">=vs-2019"

[![O IDE do Visual Studio 2019](media/vs-2019/ide-overview.png)](media/vs-2019/ide-overview.png#lightbox)

::: moniker-end

Esta imagem mostra o Visual Studio com um projeto aberto e várias importantes janelas de ferramentas que você provavelmente usará:

- O [Gerenciador de Soluções](../../ide/solutions-and-projects-in-visual-studio.md) (parte superior direita) permite exibir, navegar e gerenciar os arquivos de código. **Gerenciador de soluções** pode ajudar a organizar seu código agrupando os arquivos em [soluções e projetos](tutorial-projects-solutions.md).

- A [janela do editor](../../ide/writing-code-in-the-code-and-text-editor.md) (parte central), na qual você provavelmente passará a maior parte do tempo, exibe o conteúdo do arquivo. É nela em que você pode editar o código ou criar uma interface do usuário, como uma janela com botões e caixas de texto.

- A [janela de Saída](../../ide/reference/output-window.md) (parte central inferior) é o local em que o Visual Studio envia notificações, como mensagens de erro e de depuração, avisos do compilador, mensagens de status da publicação e muito mais. Cada fonte de mensagem tem uma guia própria.

- O [Team Explorer](/azure/devops/user-guide/work-team-explorer?view=vsts&preserve-view=true) (canto inferior direito) permite que você acompanhe itens de trabalho e compartilhe o código com outras pessoas usando tecnologias de controle de versão como o [Git](https://git-scm.com/) e o [TFVC (Controle de Versão do Team Foundation)](/azure/devops/repos/tfvc/overview?view=vsts&preserve-view=true).

## <a name="editions"></a>Edições

O Visual Studio está disponível para Windows e Mac. O [Visual Studio para Mac](/visualstudio/mac/) tem muitas das mesmas funcionalidades do Visual Studio 2017 e é otimizado para o desenvolvimento de aplicativos móveis e multiplataforma. Este artigo concentra-se na versão do Visual Studio 2017 para Windows.

Há três edições do Visual Studio 2017: Community, Professional e Enterprise. Veja [Comparar IDEs do Visual Studio 2017](https://visualstudio.microsoft.com/vs/compare/) para saber quais recursos são compatíveis com cada edição.

## <a name="popular-productivity-features"></a>Recursos de produtividade populares

Alguns dos recursos populares no Visual Studio que ajudam você a ser mais produtivo durante o desenvolvimento de software incluem:

- Rabiscos e [Ações Rápidas](../../ide/quick-actions.md)

   Rabiscos são sublinhados ondulados que alertam você sobre erros ou problemas potenciais no código durante a digitação. Essas pistas visuais permitem que você corrija os problemas imediatamente sem esperar que o erro seja descoberto durante o build ou quando você executar o programa. Se você focalizar um rabisco, verá informações adicionais sobre o erro. Uma lâmpada também pode ser exibida na margem esquerda com ações, conhecidas como Ações Rápidas, para corrigir o erro.

   ::: moniker range="vs-2017"

   ![Rabiscos no Visual Studio](media/squiggles-error.png)

   ::: moniker-end

   ::: moniker range=">=vs-2019"

   ![Rabiscos no Visual Studio](media/vs-2019/squiggles-error.png)

   ::: moniker-end

- [Refatoração](../../ide/refactoring-in-visual-studio.md)

   A refatoração inclui operações como renomeação inteligente de variáveis, extração de uma ou mais linhas de código em um novo método, alteração da ordem dos parâmetros de método e muito mais.

   ::: moniker range="vs-2017"

   ![Menu Refatoração no Visual Studio](media/refactoring-menu.png)

   ::: moniker-end

   ::: moniker range=">=vs-2019"

   ![Menu Refatoração no Visual Studio](media/vs-2019/refactorings-menu.png)

   ::: moniker-end

- [IntelliSense](../../ide/using-intellisense.md)

   IntelliSense é um termo usado para um conjunto de recursos que exibe informações sobre o código diretamente no editor e, em alguns casos, escreve pequenos trechos de código para você. É como ter a documentação básica embutida no editor, o que evita que você tenha que consultar informações de tipo em outro lugar. Os recursos do IntelliSense variam de acordo com a linguagem. Para saber mais, consulte [C# IntelliSense](../../ide/visual-csharp-intellisense.md), [Visual C++ IntelliSense](../../ide/visual-cpp-intellisense.md), [JavaScript IntelliSense](../../ide/javascript-intellisense.md) e [Visual Basic IntelliSense](../../ide/visual-basic-specific-intellisense.md). A seguinte ilustração mostra como o IntelliSense exibe uma lista de membros para um tipo:

   ::: moniker range="vs-2017"

   ![Lista de membros do Visual Studio](media/intellisense-list-members.png)

   ::: moniker-end

   ::: moniker range=">=vs-2019"

   ![Lista de membros do Visual Studio](media/vs-2019/intellisense-list-members.png)

   ::: moniker-end

- Caixa de pesquisa

   O Visual Studio pode parecer assustador, às vezes, com tantas propriedades, opções e menus. A caixa de pesquisa é uma ótima maneira de encontrar rapidamente o que você precisa no Visual Studio. Quando você começa a digitar o nome de algo que está procurando, o Visual Studio lista resultados que levam você exatamente para o local em que precisa ir. Caso você precise adicionar uma funcionalidade ao Visual Studio, por exemplo, para adicionar suporte a outra linguagem de programação, a caixa de pesquisa fornecerá resultados que abrem o Instalador do Visual Studio para instalar uma carga de trabalho ou um componente individual.

   > [!TIP]
   > Pressione **Ctrl** + **Q** como um atalho para a caixa de pesquisa.

   ::: moniker range="vs-2017"

   ![Caixa de pesquisa Início Rápido no Visual Studio 2017](../media/quick-launch-nuget.png)

   Para obter mais informações, consulte [Início Rápido](../../ide/reference/quick-launch-environment-options-dialog-box.md).

   ::: moniker-end

   ::: moniker range=">=vs-2019"

   ![Caixa de pesquisa no Visual Studio 2019](media/vs-2019/quick-launch.png)

   ::: moniker-end

- [Live Share](/visualstudio/liveshare/)

   Edite e depure de maneira colaborativa com outras pessoas em tempo real, independentemente do tipo de aplicativo ou linguagem de programação. Você pode compartilhar seu projeto atual de forma instantânea e segura e, conforme necessário, compartilhar sessões de depuração, instâncias de terminal, aplicativos Web do localhost, chamadas de voz e muito mais.

- [Hierarquia de chamadas](../../ide/reference/call-hierarchy.md)

   A janela **Hierarquia de Chamadas** mostra os métodos que chamam um método selecionado. Essas podem ser informações úteis quando você está considerando alterar ou remover o método ou quando está tentando rastrear um bug.

   ::: moniker range="vs-2017"

   ![Exibir a hierarquia de chamadas no Visual Studio](media/call-hierarchy.png)

   ::: moniker-end

   ::: moniker range=">=vs-2019"

   ![Exibir a hierarquia de chamadas no Visual Studio](media/vs-2019/call-hierarchy.png)

   ::: moniker-end

- [CodeLens](../../ide/find-code-changes-and-other-history-with-codelens.md)

   O CodeLens ajuda você a encontrar referências e alterações no código, bugs vinculados, itens de trabalho, revisões de código e testes de unidade, tudo isso sem sair do editor.

   ::: moniker range="vs-2017"

   ![CodeLens no Visual Studio](media/codelens.png)

   ::: moniker-end

   ::: moniker range=">=vs-2019"

   ![CodeLens no Visual Studio](media/vs-2019/codelens.png)

   ::: moniker-end

- [Ir para Definição](../../ide/go-to-and-peek-definition.md)

   O recurso Ir para Definição leva você diretamente para o local em que uma função ou um tipo está definido.

   ::: moniker range="vs-2017"

   ![Ir para Definição no Visual Studio 2017](media/go-to-definition-menu.png)

   ::: moniker-end

   ::: moniker range=">=vs-2019"

   ![Ir para Definição no Visual Studio 2019](media/vs-2019/go-to-definition-menu.png)

   ::: moniker-end

- [Inspecionar definição](../../ide/how-to-view-and-edit-code-by-using-peek-definition-alt-plus-f12.md)

   A janela **Espiar Definição** mostra a definição de um método ou um tipo sem, na verdade, abrir um arquivo separado.

   ::: moniker range="vs-2017"

   ![Inspecionar Definição no Visual Studio](media/peek-definition.png)

   ::: moniker-end

   ::: moniker range=">=vs-2019"

   ![Inspecionar Definição no Visual Studio](media/vs-2019/peek-definition.png)

   ::: moniker-end

## <a name="install-the-visual-studio-ide"></a>Instalar o IDE do Visual Studio

Nesta seção, você criará um projeto simples para experimentar algumas coisas que pode fazer com o Visual Studio. Você vai alterar o tema de cores, use [IntelliSense](../../ide/using-intellisense.md) como um auxílio de codificação e depurar um aplicativo para ver o valor de uma variável durante a execução do programa.

::: moniker range="vs-2017"

Para começar, [baixe o Visual Studio](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) e instale-o no sistema. O instalador modular permite que você selecione e instale *cargas de trabalho*, que são grupos de recursos necessários para a linguagem de programação ou plataforma que você preferir. Para seguir as etapas de [criação de um programa](#create-a-program), selecione a carga de trabalho **Desenvolvimento multiplataforma do .NET Core** durante a instalação.

::: moniker-end

::: moniker range=">=vs-2019"

Para começar, [baixe o Visual Studio](https://visualstudio.microsoft.com/downloads) e instale-o no sistema. O instalador modular permite que você selecione e instale *cargas de trabalho*, que são grupos de recursos necessários para a linguagem de programação ou plataforma que você preferir. Para seguir as etapas de [criação de um programa](#create-a-program), selecione a carga de trabalho **Desenvolvimento multiplataforma do .NET Core** durante a instalação.

::: moniker-end

![Carga de trabalho de desenvolvimento multiplataforma do .NET Core no Instalador do Visual Studio](../media/dotnet-core-cross-platform-workload.png)

Ao iniciar o Visual Studio pela primeira vez, como opção, você pode [entrar](../../ide/signing-in-to-visual-studio.md) usando sua conta Microsoft ou sua conta corporativa ou de estudante.

## <a name="customize-visual-studio"></a>Personalizar o Visual Studio

Personalize a interface do usuário do Visual Studio, incluindo a alteração do tema de cores padrão.

### <a name="change-the-color-theme"></a>Alterar o tema de cores

Para alterar para o tema **Escuro**:

::: moniker range="vs-2017"

1. Abra o Visual Studio.

::: moniker-end

::: moniker range=">=vs-2019"

1. Abra o Visual Studio. Na janela iniciar, selecione **continuar sem código**.


    :::image type="content" source="media/vs-2019/continue-without-code.png" alt-text="Captura de tela da janela inicial no Visual Studio 2019, com o link ' continuar sem código ' realçado.":::

   O IDE abre.

::: moniker-end

2. Na barra de menus, escolha **ferramentas**  >  **Opções** para abrir a caixa de diálogo **Opções** .

3. Na   >  página opções **gerais** do ambiente, altere a seleção de **tema de cores** para **escuro** e clique em **OK**.

   ![Alterar o tema de cores para escuro no Visual Studio](media/change-color-theme.png)

   O tema de cores para todo o IDE é alterado para **Escuro**.

   ::: moniker range="vs-2017"

   ![Visual Studio no tema escuro](../../ide/media/quickstart-personalize-dark-theme.png)

   ::: moniker-end

   ::: moniker range=">=vs-2019"

   ![Visual Studio no tema escuro](media/vs-2019/dark-theme.png)

   ::: moniker-end

### <a name="select-environment-settings"></a>Selecionar configurações do ambiente

Primeiro, configuraremos o Visual Studio para usar configurações de ambiente adequadas aos desenvolvedores em Visual Basic.

1. Na barra de menus, escolha **ferramentas**  >  **importar e exportar configurações**.

2. No **Assistente de importação e exportação de configurações**, selecione **redefinir todas as configurações** na primeira página e clique em **Avançar**.

3. Na página **salvar configurações atuais** , selecione uma opção para salvar as configurações atuais ou não e clique em **Avançar**. Se você ainda não personalizou as configurações, selecione **Não, apenas redefina as configurações, substituindo minhas configurações atuais**.

4. Na página **escolher uma coleção padrão de configurações** , escolha **Visual Basic** e clique em **concluir**.

5. Na página **Redefinir conclusão** , clique em **fechar**.

Para conhecer outras maneiras pelas quais você pode personalizar o IDE, confira [Personalizar o Visual Studio](../../ide/personalizing-the-visual-studio-ide.md).

## <a name="create-a-program"></a>Criar um programa

Vamos nos aprofundar e criar um programa simples.

::: moniker range="vs-2017"

1. Na barra de menus do Visual Studio, escolha **arquivo** > **novo projeto**.

   ![Arquivo > Novo projeto na barra de menus](media/file-new-project-menu.png)

   A caixa de diálogo **novo projeto** mostra vários *modelos* de projeto. Um modelo contém as configurações e os arquivos básicos necessários para um tipo de projeto fornecido.

1. Escolha a categoria **.NET Core** em **Visual Basic** e escolha o modelo **Aplicativo de Console (.NET Core)**. Na caixa de texto **Nome**, digite **HelloWorld** e, em seguida, selecione o botão **OK**.

   ![Modelo de aplicativo .NET Core](media/overview-npd.png)

   > [!NOTE]
   > Se você não vir a categoria **.NET Core**, será necessário instalar a carga de trabalho **Desenvolvimento de plataforma cruzada do .NET Core**. Para fazer isso, escolha o link **Abrir o Instalador do Visual Studio** na parte inferior esquerda da caixa de diálogo **Novo Projeto**. Depois que o Instalador do Visual Studio for aberto, role a tela para baixo, selecione a carga de trabalho **Desenvolvimento multiplataforma do .NET Core** e, em seguida, selecione **Modificar**.

   O Visual Studio cria o projeto. É um aplicativo "Olá, Mundo" simples que chama o método <xref:System.Console.WriteLine?displayProperty=nameWithType> para exibir a cadeia de caracteres literal "Olá, Mundo!" na janela do console (saída do programa).

   Logo em seguida, você deverá ver algo parecido com isto:

   ![Visual Studio IDE](media/overview-ide-console-app.png)

   O código Visual Basic para o aplicativo é mostrado na janela do editor, que ocupa a maior parte do espaço. Observe que o texto é colorizado automaticamente para indicar diferentes partes do código, como palavras-chave e tipos. Além disso, pequenas linhas verticais tracejadas no código indicam a correspondência de chaves e os números de linha ajudam a localizar o código posteriormente. Escolha os pequenos sinais de subtração demarcados para recolher ou expandir blocos de código. Esse recurso de estrutura de tópicos do código permite ocultar os códigos desnecessários, ajudando a minimizar a desordem na tela. Os arquivos de projeto são listados no lado direito em uma janela chamada **Gerenciador de Soluções**.

   ![IDE do Visual Studio com caixas de vermelhas](media/overview-ide-console-app-red-boxes.png)

   Há outros menus e outras janelas de ferramentas disponíveis, mas por enquanto, vamos seguir em frente.

1. Agora, inicie o aplicativo. Você pode fazer isso escolhendo **Iniciar Sem Depuração** no menu **Depurar** na barra de menus. Você também pode pressionar **Ctrl** + **F5**.

   ![Menu Depurar > Iniciar Sem Depuração](../media/overview-start-without-debugging.png)

   O Visual Studio compila o aplicativo e uma janela do console é aberta com a mensagem **Olá, Mundo!**. Agora você tem um aplicativo em execução.

   ![Janela do console](../media/overview-console-window.png)

1. Para fechar a janela do console, pressione qualquer tecla do teclado.

1. Vamos adicionar um código adicional ao aplicativo. Adicione o código Visual Basic a seguir antes da linha que diz `Console.WriteLine("Hello World!")`:

   ```vb
   Console.WriteLine("What is your name?")
   Dim name = Console.ReadLine()
   ```

   Esse código exibe **Qual é seu nome?** na janela do console e, em seguida, aguarda até que o usuário insira um texto seguido da tecla **Enter**.

1. Altere a linha que indica `Console.WriteLine("Hello World!")` para o seguinte código:

   ```vb
   Console.WriteLine("Hello " + name + "!")
   ```

1. Execute o aplicativo novamente pressionando **Ctrl** + **F5**.

   O Visual Studio recompila o aplicativo e uma janela do console é aberta e solicita seu nome.

1. Insira seu nome na janela do console e pressione **Enter**.

   ![Entrada da janela do console](../media/overview-console-input.png)

1. Pressione qualquer tecla para fechar a janela do console e interromper o programa em execução.

::: moniker-end

::: moniker range=">=vs-2019"

1. Na barra de menus do Visual Studio, escolha **arquivo**  >  **novo**  >  **projeto**. (Como alternativa, pressione **Ctrl** + **Shift** + **N**.)

    :::image type="content" source="media/vs-2019/file-new-project.png" alt-text="Captura de tela do arquivo > nova seleção de projeto de > na barra de menus do Visual Studio 2019.":::

   A janela **Criar um novo projeto** é aberta e mostra diversos *modelos* de projeto. Um modelo contém os arquivos básicos e as configurações necessárias para um determinado tipo de projeto.

1. Para localizar o modelo desejado, digite ou insira **console do .net core** na caixa de pesquisa. A lista de modelos disponíveis é filtrada automaticamente com base nas palavras-chave que você inseriu. Você pode filtrar ainda mais os resultados do modelo escolhendo **Visual Basic** na lista suspensa **todos os idiomas** , **Windows** na lista **todas as plataformas** e **console** na lista **todos os tipos de projeto** .

   Selecione o modelo de **aplicativo de console** e clique em **Avançar**.

    :::image type="content" source="media/vs-2019/create-new-project.png" alt-text="Captura de tela da janela ' criar um novo projeto ' no Visual Studio 2019, em que você seleciona o modelo desejado.":::

1. Na janela **configurar seu novo projeto** , digite **HelloWorld** na caixa **nome do projeto** , opcionalmente, altere o local do diretório para os arquivos do projeto (a localidade padrão é `C:\Users\<name>\source\repos` ) e clique em **Avançar**.

    :::image type="content" source="media/vs-2019/configure-new-project.png" alt-text="Captura de tela da janela ' configurar seu novo projeto ' no Visual Studio 2019, em que você insere o nome do projeto.":::

1. Na janela **informações adicionais** , verifique se **.NET Core 3,1** aparece no menu suspenso **estrutura de destino** e, em seguida, clique em **criar**.

    :::image type="content" source="media/vs-2019/create-project-additional-info.png" alt-text="Captura de tela da janela ' informações adicionais ' no Visual Studio 2019, onde você seleciona a versão do .NET Core Framework que deseja.":::

   O Visual Studio cria o projeto. É um aplicativo "Olá, Mundo" simples que chama o método <xref:System.Console.WriteLine?displayProperty=nameWithType> para exibir a cadeia de caracteres literal "Olá, Mundo!" na janela do console (saída do programa).

   Logo em seguida, você deverá ver algo parecido com isto:

   ![Visual Studio IDE](media/overview-ide-console-app.png)

   O código Visual Basic para o aplicativo é mostrado na janela do editor, que ocupa a maior parte do espaço. Observe que o texto é colorizado automaticamente para indicar diferentes partes do código, como palavras-chave e tipos. Além disso, pequenas linhas verticais tracejadas no código indicam a correspondência de chaves e os números de linha ajudam a localizar o código posteriormente. Escolha os pequenos sinais de subtração demarcados para recolher ou expandir blocos de código. Esse recurso de estrutura de tópicos do código permite ocultar os códigos desnecessários, ajudando a minimizar a desordem na tela. Os arquivos de projeto são listados no lado direito em uma janela chamada **Gerenciador de Soluções**.

   ![IDE do Visual Studio com caixas de vermelhas](media/overview-ide-console-app-red-boxes.png)

   Há outros menus e outras janelas de ferramentas disponíveis, mas por enquanto, vamos seguir em frente.

1. Agora, inicie o aplicativo. Você pode fazer isso escolhendo **Iniciar Sem Depuração** no menu **Depurar** na barra de menus. Você também pode pressionar **Ctrl** + **F5**.

   ![Menu Depurar > Iniciar Sem Depuração](media/vs-2019/start-without-debugging.png)

   O Visual Studio compila o aplicativo e uma janela do console é aberta com a mensagem **Olá, Mundo!**. Agora você tem um aplicativo em execução.

   ![Captura de tela da janela do console mostrando a mensagem de Olá, Mundo.](../media/vs-2019/overview-console-window.png)

1. Para fechar a janela do console, pressione qualquer tecla do teclado.

1. Vamos adicionar um código adicional ao aplicativo. Adicione o código Visual Basic a seguir antes da linha que diz `Console.WriteLine("Hello World!")`:

   ```vb
   Console.WriteLine("What is your name?")
   Dim name = Console.ReadLine()
   ```

   Esse código exibe **Qual é seu nome?** na janela do console e, em seguida, aguarda até que o usuário insira um texto seguido da tecla **Enter**.

1. Altere a linha que indica `Console.WriteLine("Hello World!")` para o seguinte código:

   ```vb
   Console.WriteLine("Hello " + name + "!")
   ```

1. Execute o aplicativo novamente pressionando **Ctrl** + **F5**.

   O Visual Studio recompila o aplicativo e uma janela do console é aberta e solicita seu nome.

1. Insira seu nome na janela do console e pressione **Enter**.

   ![Captura de tela da janela do console mostrando o que é sua pergunta de nome e a resposta do aplicativo.](../media/vs-2019/overview-console-input.png)

1. Pressione qualquer tecla para fechar a janela do console e interromper o programa em execução.

::: moniker-end

## <a name="use-refactoring-and-intellisense"></a>Usar a refatoração e o IntelliSense

Vamos examinar algumas das maneiras pelas quais a [refatoração](../../ide/refactoring-in-visual-studio.md) e o [IntelliSense](../../ide/using-intellisense.md) podem ajudar você a codificar com mais eficiência.

Primeiro, vamos renomear a variável `name`:

1. Clique duas vezes na variável `name` para selecioná-la.

2. Digite o novo nome da variável, **username**.

   Observe que uma caixa cinza é exibida ao redor da variável e uma lâmpada é exibida na margem.

3. Selecione o ícone de lâmpada para mostrar as [Ações Rápidas](../../ide/quick-actions.md) disponíveis. Selecione **Renomear 'name' como 'username'**.

   ![Ação de renomeação no Visual Studio](media/rename-quick-action.png)

   A variável é renomeada no projeto, o que, em nosso caso, são apenas dois locais.

4. Agora vamos dar uma olhada no IntelliSense. Abaixo da linha que indica `Console.WriteLine("Hello &quot; + username + &quot;!")`, digite o seguinte fragmento de código:

    ```vb
   Dim now = Date.
   ```

   Uma caixa exibe os membros da classe <xref:System.DateTime>. Além disso, a descrição do membro atualmente selecionado é exibida em uma caixa separada.

   ![O IntelliSense lista membros no Visual Studio](media/intellisense-list-members.png)

5. Selecione o membro chamado **Now**, que é uma propriedade da classe, clicando duas vezes nele ou selecionando-o usando as teclas de direção e pressionando **Tab**.

6. Abaixo disso, digite ou cole as seguintes linhas de código:

   ```vb
   Dim dayOfYear = now.DayOfYear
   Console.Write("Day of year: ")
   Console.WriteLine(dayOfYear)
   ```

   > [!TIP]
   > <xref:System.Console.Write%2A?displayProperty=nameWithType> é um pouco diferente de <xref:System.Console.WriteLine%2A?displayProperty=nameWithType>, pois não adiciona um terminador de linha após a impressão. Isso significa que a próxima parte do texto que é enviada para a saída será impressa na mesma linha. Focalize cada um desses métodos no código para ver a descrição.

7. Em seguida, usaremos a refatoração novamente para tornar o código um pouco mais conciso. Clique na variável `now` na linha `Dim now = Date.Now`.

   Observe que um pequeno ícone de chave de fenda é exibido na margem dessa linha.

8. Clique no ícone de chave de fenda para ver quais sugestões estão disponíveis no Visual Studio. Nesse caso, está mostrando a refatoração [Variável temporária embutida](../../ide/reference/inline-temporary-variable.md) para remover uma linha de código sem alterar o comportamento geral do código:

   ![Refatoração de variável temporária embutida no Visual Studio](media/inline-temporary-variable-refactoring.png)

9. Clique em **Variável temporária embutida** para refatorar o código.

::: moniker range="vs-2017"

10. Execute o programa novamente pressionando **Ctrl** + **F5**. A saída é parecida com esta:

    ![Janela do console com saída do programa](../media/overview-console-final.png)

::: moniker-end

::: moniker range=">=vs-2019"

10. Execute o programa novamente pressionando **Ctrl** + **F5**. A saída é parecida com esta:

    ![Janela do console com saída do programa](../media/vs-2019/overview-console-final.png)

::: moniker-end

## <a name="debug-code&quot;></a>Depurar o código

Ao escrever o código, você precisa executá-lo e testá-lo para verificar se há bugs. O sistema de depuração do Visual Studio permite que você execute em etapas uma instrução no código por vez e inspecione variáveis durante o processo. Defina *pontos de interrupção* que interrompem a execução do código em uma linha específica. Observe como o valor de uma variável é alterado durante a execução do código e muito mais.

Vamos definir um ponto de interrupção para ver o valor da variável `username` enquanto o programa está &quot;em andamento&quot;.

1. Encontre a linha de código que indica `Console.WriteLine(&quot;Hello &quot; + username + &quot;!")`. Para definir um ponto de interrupção nessa linha de código, ou seja, para fazer com que o programa pause a execução nessa linha, clique na margem mais à esquerda do editor. Clique também em qualquer lugar na linha de código e, em seguida, pressione **F9**.

   Um círculo vermelho é exibido na margem da extrema esquerda, e o código é realçado em vermelho.

   ![Ponto de interrupção na linha de código no Visual Studio](media/breakpoint.png)

1. Inicie a depuração selecionando **depurar**  >  **Iniciar Depuração** ou pressionando **F5**.

1. Quando a janela do console for exibida e solicitar seu nome, digite-o e pressione **Enter**.

   O foco retorna para o editor de códigos do Visual Studio e a linha de código com o ponto de interrupção é realçada em amarelo. Isso significa que ela é a próxima linha de código que será executada pelo programa.

1. Passe o mouse sobre a variável `username` para ver seu valor. Como alternativa, clique com o botão direito do mouse em `username` e selecione **Adicionar Inspeção** para adicionar a variável à janela **Inspeção**, na qual você também pode ver o valor.

   ![Valor da variável durante a depuração no Visual Studio](media/debugging-variable-value.png)

1. Para permitir que o programa seja executado até a conclusão, pressione **F5** novamente.

Para obter mais detalhes sobre a depuração no Visual Studio, consulte [Tour dos recursos do depurador](../../debugger/debugger-feature-tour.md).

## <a name="next-steps"></a>Próximas etapas

Explore ainda mais o Visual Studio seguindo um dos seguintes artigos introdutórios:

> [!div class="nextstepaction"]
> [Saiba como usar o editor de códigos](tutorial-editor.md)

> [!div class="nextstepaction"]
> [Saiba mais sobre projetos e soluções](tutorial-projects-solutions.md)

## <a name="see-also"></a>Confira também

- Descubra [mais recursos do Visual Studio](../../ide/advanced-feature-overview.md)
- Visite [visualstudio.microsoft.com](https://visualstudio.microsoft.com/vs/)
- Leia [The Visual Studio blog](https://devblogs.microsoft.com/visualstudio/) (O blog do Visual Studio)
