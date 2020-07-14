---
title: Usando ferramentas do Visual Studio para Unity | Microsoft Docs
ms.custom: ''
ms.date: 07/03/2018
ms.technology: vs-unity-tools
ms.topic: how-to
ms.assetid: e67ec9a2-a449-413e-8930-9a471bd43a06
author: therealjohn
ms.author: johmil
manager: crdun
ms.workload:
- unity
ms.openlocfilehash: f65945f28a577201c1308694bb7196d464330dc1
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85815156"
---
# <a name="use-visual-studio-tools-for-unity"></a>Usar as Ferramentas do Visual Studio para Unity

Nesta seção, você aprenderá como usar os recursos de integração e produtividade das Ferramentas do Visual Studio para Unity e como usar o depurador do Visual Studio para desenvolvimento no Unity.

## <a name="open-unity-scripts-in-visual-studio"></a>Abrir scripts do Unity no Visual Studio

Depois que o Visual Studio é [definido como o editor de script externo para Unity](getting-started-with-visual-studio-tools-for-unity.md#configure-unity-for-use-with-visual-studio), abrir qualquer script do editor do Unity iniciará ou trocará automaticamente para o Visual Studio com o script escolhido aberto. Clique duas vezes em um script em seu projeto do Unity.

Outra opção é abrir o Visual Studio sem um script aberto no editor de código-fonte por meio da seleção de **Abrir Projeto em C#** no menu **Ativos** no Unity.

![Abrir um projeto C#](media/vstu_open-csharp-project.png)

## <a name="unity-documentation-access"></a>Acesso de documentação do Unity

Você pode acessar a documentação de script do Unity rapidamente pelo Visual Studio. Se as Ferramentas do Visual Studio para Unity não encontrarem a documentação da API localmente, elas tentarão localizá-la online.

- No Visual Studio, realce ou coloque o cursor sobre a API do Unity sobre a qual você deseja aprender e pressione **Ctrl** + **ALT** + **M**, **Ctrl** + **H**

## <a name="intellisense-for-unity-api-messages"></a>Intellisense para mensagens da API do Unity

O preenchimento de código Intellisense facilita a implementação de mensagens de API do Unity em scripts MonoBehaviour e auxilia no aprendizado da API do Unity. Para usar o IntelliSense para mensagens Unity:

1. Posicione o cursor em uma nova linha dentro do corpo de uma classe derivada de `MonoBehaviour`.

2. Comece a digitar o nome de uma mensagem do Unity, como `OnTriggerEnter`.

3. Após digitar as letras "**ont**", uma lista de sugestões do IntelliSense será exibida.

   ![Usando IntelliSense](media/vstu_intellisense1.png)

4. A seleção na lista pode ser alterada de três maneiras:

    - Com as teclas de direção **Para cima** e **Para baixo**.

    - Clicando com o mouse no item desejado.

    - Continuando a digitar o nome do item desejado.

5. O IntelliSense pode inserir a mensagem Unity selecionada, incluindo todos os parâmetros necessários:

    - Pressionando **Tab**.

    - Pressionando **Enter**.

    - Clicando duas vezes no item selecionado.

   ![Inserir mensagem Unity do IntelliSense](media/vstu_intellisense2.png)

## <a name="unity-monobehavior-scripting-wizard"></a>Assistente de script do Unity MonoBehavior

Você pode usar o assistente do MonoBehavior para exibir uma lista de todos os métodos de API do Unity e implementar rapidamente uma definição vazia. Esse recurso, especialmente com o opção **Gerar comentários de método** habilitada, será útil se você ainda estiver aprendendo o que está disponível na API do Unity.

Para criar definições de método MonoBehavior vazias usando o assistente do MonoBehavior:

1. No Visual Studio, posicione o cursor onde você deseja que os métodos sejam inseridos e pressione **Ctrl** + **Shift** + **M** para iniciar o assistente de monocomportamento.

2. Na janela **Criar métodos de script**, marque a caixa de seleção ao lado do nome de cada método que você quer adicionar.

3. Use a lista suspensa **versão do Framework** para selecionar a versão desejada.

4. Por padrão, os métodos são inseridos na posição do cursor. Como alternativa, você pode inseri-los após qualquer método que já esteja implementado em sua classe alterando o valor do **Ponto de inserção** na lista suspensa para o local desejado.

5. Se desejar que o Assistente gere comentários para os métodos que você selecionou, marque a caixa de seleção **Gerar comentários do método**. Esses comentários servem para ajudá-lo a entender quando o método é chamado e quais são suas responsabilidades gerais.

6. Selecione o botão **OK** para sair do assistente e inserir os métodos em seu código.

   ![A caixa de diálogo do assistente de monocomportamento.](../cross-platform/media/vstu_monobehavior_wizard_full.png "vstu_monobehavior_wizard_full")

## <a name="unity-project-explorer"></a>Gerenciador de Projetos do Unity

![A janela Explorador de projeto do Unity.](../cross-platform/media/vstu_unity_project_explorer.png "vstu_unity_project_explorer")

O Gerenciador de Projetos do Unity exibe todos os seus arquivos e diretórios de projeto do Unity da mesma maneira que o Editor do Unity. Isso é diferente de navegar nos scripts do Unity com a solução normal do Gerenciador de Soluções do Visual Studio, que os organiza em projetos e em uma solução gerada pelo Visual Studio.

- No menu principal do Visual Studio, escolha **Exibir > Gerenciador de Projetos do Unity**. Atalho de teclado: **ALT** + **Shift** + **E**

   ![Exiba a janela Explorador de projeto do Unity.](../cross-platform/media/vstu_view_unity_project_explorer.png "vstu_view_unity_project_explorer")

## <a name="unity-debugging"></a>Depuração do Unity

Ferramentas do Visual Studio para Unity permitem depurar scripts do editor e jogos para seu projeto do Unity usando um depurador poderoso do Visual Studio.

### <a name="debug-in-the-unity-editor"></a>Depuração no editor do Unity

#### <a name="start-debugging"></a>Iniciar a depuração

1. Conecte o Visual Studio com o Unity clicando no botão de **Reprodução** rotulado **Anexar ao Unity**, ou use o atalho de teclado **F5**.

   ![Clique em Executar no Visual Studio](media/vstu_play-button.png)

2. Alterne para o Unity e clique no botão **Reproduzir** para executar o jogo no editor.

   ![Clique em Executar no Unity](media/vstu_unity-play-button.png)

3. Quando o jogo estiver em execução no editor do Unity e ao mesmo conectado ao Visual Studio, qualquer ponto de interrupção encontrado pausará a execução do jogo e mostrará a linha de código em que o jogo atingiu o ponto de interrupção no Visual Studio.

#### <a name="stop-debugging"></a>Parar a depuração

- Clique no botão **Parar** no Visual Studio, ou use o atalho de teclado **Shift+F5**.

  ![Clique em Parar no Visual Studio](media/vstu_stop-debugger.png)

Para saber mais sobre a depuração no Visual Studio, confira [Primeiro acesso ao Depurador do Visual Studio](../debugger/debugger-feature-tour.md).

#### <a name="attach-to-unity-and-play"></a>Anexar ao Unity e Reproduzir

Para maior conveniência, você pode alterar o botão **Anexar ao Unity** para o modo **Anexar ao Unity e Reproduzir**.

1. Clique na **setinha para baixo** ao lado do botão **Anexar ao Unity**.

1. Selecione **Anexar ao Unity e Reproduzir** no menu suspenso.

    ![Anexar e reproduzir](media/vstu_attach-and-play.png)

O botão de reprodução muda para **Anexar ao Unity e Reproduzir**. Agora, ao clicar nesse botão ou usar o atalho de teclado **F5**, alterna automaticamente para o editor do Unity e executa o jogo no editor, além de anexar o depurador do Visual Studio.

Se você clicar no botão **Parar** no Visual Studio ou usar o atalho de teclado **Shift**+**F5**, o jogo será interrompido automaticamente no editor do Unity.

### <a name="debug-unity-player-builds"></a>Depuração de builds de player do Unity

Você pode depurar builds de desenvolvimento de vários player do Unity com o Visual Studio.

#### <a name="enable-script-debugging-in-a-unity-player"></a>Habilitar a depuração de scripts em um player do Unity

1. No Unity, abra as Configurações de Build selecionando **Arquivo > Configurações de Build**.

2. Na janela Configurações de Build, marque as caixas de seleção **Build de Desenvolvimento** e **Depuração de Script**.

   ![Defina as configurações de Build do Unity para depuração.](../cross-platform/media/vstu_debugging_build_settings.png "vstu_debugging_build_settings")

#### <a name="select-a-unity-instance-to-attach-the-debugger-to"></a>Selecione uma instância do Unity à qual anexar o depurador

- No Visual Studio, no menu principal, escolha **Depurar > Anexar Depurador do Unity**.

   ![Anexe o depurador do Unity.](../cross-platform/media/vstu_debugging_attach_unity_debugger.png "vstu_debugging_attach_unity_debugger")

   A caixa de diálogo **Selecionar Instância do Unity** exibe informações sobre cada instância do Unity a que você pode se conectar.

   ![Escolha uma instância do Unity ao qual se conectar.](../cross-platform/media/vstu_attach-debugger.png "vstu_connection_to_unity")

   **Projeto**

   O nome do projeto para Unity que está sendo executado nesta instância do Unity.

   **Computador** O nome do computador ou dispositivo no qual essa instância do Unity está em execução.

   **Digite** **Editor** se esta instância do Unity for executada como parte do Editor do Unity; **Player** se esta instância do Unity for um player autônomo.

   **Porta** O número da porta do soquete UDP pela qual esta instância do Unity está se comunicando.

> [!IMPORTANT]
> Como as Ferramentas do Visual Studio para Unity e a instância do Unity se comunicam por um soquete de rede UDP, o firewall pode perguntar sobre ele. Se isso acontecer, você precisará autorizar a conexão para que o VSTU e o Unity possam se comunicar.

### <a name="debug-a-dll-in-your-unity-project"></a>Depurar uma DLL no projeto do Unity

Muitos desenvolvedores do Unity estão escrevendo componentes de código como DLLs externas para que a funcionalidade que desenvolvem possa ser facilmente compartilhada com outros projetos. Ferramentas do Visual Studio para Unity facilitam a depuração do código nessas DLLs perfeitamente com outro código no seu projeto do Unity.

> [!NOTE]
> Neste momento, as Ferramentas do Visual Studio para Unity dá suporte somente DLLs gerenciadas. Elas não oferecem suporte à depuração de DLLs de código nativo, como aquelas escritas em C++.

Observe que o cenário descrito aqui pressupõe que você tenha o código-fonte, ou seja, se você estiver desenvolvendo ou reutilizando seu próprio código primário ou se você tiver o código-fonte em uma biblioteca de terceiros e pretender implantá-lo em seu projeto do Unity como uma DLL. Esse cenário não descreve como depurar uma DLL para a qual você não tem o código-fonte.

#### <a name="to-debug-a-managed-dll-project-used-in-your-unity-project"></a>Para depurar um projeto de DLL gerenciado usado em seu projeto do Unity

1. Adicione o projeto de DLL existente para a solução do Visual Studio gerada pelas Ferramentas do Visual Studio para Unity. Com menos frequência, você pode iniciar um novo projeto DLL gerenciado para conter componentes de código no seu projeto do Unity; Se esse for o caso, você poderá adicionar um novo projeto de DLL gerenciado para a solução do Visual Studio em vez disso. Para obter mais informações sobre como adicionar um projeto novo ou existente a uma solução, consulte [Como adicionar projetos a uma solução](https://msdn.microsoft.com/library/ff460187.aspx).

   ![Adicione o projeto DLL existente à solução.](../cross-platform/media/vstu_debugging_dll_add_existing.png "vstu_debugging_dll_add_existing")

   Em ambos os casos, as Ferramentas do Visual Studio para Unity mantêm a referência de projeto, mesmo se ele tiver de gerar novamente os arquivos de projeto e solução novamente, então, você precisa executar essas etapas de uma vez.

2. Faça referência ao perfil de framework do Unity correto no projeto de DLL. No Visual Studio, nas propriedades do projeto DLL, defina a propriedade **Estrutura de destino** para a versão do framework do Unity que você está usando. Essa é a Biblioteca de classes base di Unity que corresponde à compatibilidade de API que seu projeto tenha como alvo, como bibliotecas de classes base completas, micro ou da Web. Isso impede que a DLL chame métodos do framework que existem em outros frameworks ou níveis de compatibilidade, mas que podem não existir na versão de framework do Unity que você está usando.

> [!NOTE]
> O seguinte só é necessário se você estiver usando o runtime herdado do Unity. Se você estiver usando o novo runtime do Unity, não precisará mais usar esses perfis dedicados do 3.5. Use um perfil do .NET 4.x compatível com sua versão do Unity.

   ![Defina a estrutura de destino da DLL para o Unity Framework.](../cross-platform/media/vstu_debugging_dll_target_framework.png "vstu_debugging_dll_target_framework")

3. Copie a DLL para a pasta Ativos do seu projeto do Unity. No Unity, ativos são arquivos que são empacotados e implantados juntos com seu aplicativo do Unity para que eles possam ser carregados no tempo de execução. Como as DLLs são vinculadas em tempo de execução, as DLLs devem ser implantadas como ativos. Para serem implantadas como um ativo, o Editor do Unity exige que as DLLs sejam colocadas dentro da pasta Ativos em seu projeto do Unity. Há duas formas de fazer isso:

   - Modifique as configurações de build do seu projeto de DLL para incluir uma tarefa posterior ao build que copia os arquivos DLL e PDB de saída de sua pasta de saída para a pasta **Ativos** do seu projeto do Unity.

   - Modifique as configurações de build do seu projeto de DLL para definir a pasta de saída como a pasta **Ativos** do seu projeto do Unity. Arquivos DLL e PDB serão colocados na pasta **Ativos**.

   Os arquivos PDB são necessários para a depuração porque eles contêm símbolos de depuração da DLL e mapeiam o código da DLL para sua forma de código-fonte. Se você tem como objetivo o runtime herdado, as Ferramentas do Visual Studio para Unity usarão informações da DLL e PDB para criar um arquivo DLL.MDB, que é o formato de símbolo de depuração usado pelo mecanismo de script do Unity herdado. Se você tem como objetivo o novo runtime e usa o Portable-PDB, o Ferramentas do Visual Studio para Unity não tentará fazer nenhuma conversão de símbolo, pois o novo runtime do Unity é capaz de consumir nativamente PDBs portáteis.

   Veja mais informações sobre a geração de PDB [aqui](../debugger/how-to-set-debug-and-release-configurations.md). Se você tem como objetivo o novo runtime, certifique-se de que "Informações de depuração" está definido como "Portátil", para gerar o PDB portátil corretamente. Se você tem como objetivo o runtime herdado, precisará usar "Full".

4. Depure seu código. Agora você pode depurar seu código-fonte de DLL junto com o código-fonte do seu projeto do Unity e usar todos os recursos de depuração com os quais esteja acostumado, como pontos de interrupção e depuração no código.

## <a name="keyboard-shortcuts"></a>Atalhos do teclado

Você pode acessar rapidamente a funcionalidade Ferramentas do Unity para Visual Studio usando seus atalhos de teclado. Este é um resumo dos atalhos que estão disponíveis.

|Comando|Atalho|Nome de comando de atalho|
|-------------|--------------|---------------------------|
|Abrir o Assistente do MonoBehavior|**Ctrl** + **Shift** + **M**|**EditorContextMenus.CodeWindow.ImplementMonoBehaviours**|
|Abrir o Gerenciador de Projetos do Unity|**ALT** + **Shift** + **E**|**View.UnityProjectExplorer**|
|Acessar a documentação do Unity|**Ctrl** + **ALT** + **M, CTRL** + **H**|**Help.UnityAPIReference**|
|Anexar ao depurador do Unity (player ou editor)|**_nenhum padrão_**|**Debug.AttachUnityDebugger**|

Será possível alterar as combinações de teclas de atalho se não desejar o padrão. Para obter informações sobre como alterá-las, confira [Identificar e personalizar atalhos de teclado no Visual Studio](../ide/identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md).
