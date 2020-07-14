---
title: Selecionar um interpretador e um ambiente do Python para um projeto
description: Especificamente, você pode selecionar um ambiente do Python, incluindo Anaconda e ambientes virtuais, a ser aplicado a um projeto específico.
ms.date: 03/18/2019
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 8bcb349f8ff99d1567bf94b83a96be6b2824c208
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85520465"
---
# <a name="how-to-select-a-python-environment-for-a-project"></a>Como selecionar um ambiente do Python para um projeto

Todo o código em um projeto Python é executado dentro do contexto de um ambiente específico, como um ambiente do Python global, um ambiente do Anaconda, um ambiente virtual ou um ambiente do Conda. O Visual Studio também usa esse ambiente para depuração, importação e conclusões de membro, verificação de sintaxe e outras tarefas que exigem serviços de linguagem específicos da versão do Python e um conjunto de pacotes instalados.

Todos os novos projetos do Python no Visual Studio são inicialmente configurados para usar o ambiente global padrão, que aparece sob o nó **ambientes Python** em **Gerenciador de soluções**:

![O ambiente de Python global padrão mostrado no Gerenciador de Soluções](media/environments/environments-project.png)

::: moniker range="vs-2017"
Para alterar o ambiente de um projeto, clique com o botão direito do mouse no nó **ambientes Python** e selecione **Adicionar/remover ambientes Python**. Na lista exibida, que inclui ambientes global, virtual e conda, selecione todos os que devem aparecer no nó **Ambientes do Python**:

![Caixa de diálogo Adicionar/Remover Ambientes do Python](media/environments/environments-add-remove.png)

Depois de marcar **OK**, todos os ambientes escolhidos são exibidos no nó **Ambientes de Python**. O ambiente ativado no momento aparece em negrito:

![Vários ambiente de Python mostrados no Gerenciador de Soluções](media/environments/environments-project-multiple.png)

Para ativar rapidamente outro ambiente, clique com o botão direito do mouse no nome desse ambiente e selecione **Ativar ambiente**. Sua escolha é salva com o projeto e esse ambiente é ativado sempre que você abrir o projeto futuramente. Se você desmarcar todas as opções na caixa de diálogo **Adicionar/Remover Ambientes de Python **, o Visual Studio ativa o ambiente padrão global.

O menu de contexto no nó **Ambientes do Python** também fornece comandos adicionais:

| Comando | Descrição |
| --- | --- |
| **Adicionar ambiente virtual** | Inicia o processo de criação de um novo ambiente virtual no projeto. Confira [Criar um ambiente virtual](#create-a-virtual-environment). |
| **Adicionar um ambiente virtual existente** | Solicita que você selecione uma pasta que contém um ambiente virtual e o adiciona à lista em **Ambientes do Python**, mas não o ativa. Confira [Ativar um ambiente virtual existente](#activate-an-existing-virtual-environment). |
| **Criar ambiente do Conda** | Alterna para a **Python Environments** *janela* de ambientes do Python na qual você insere um nome para o ambiente e especifica seu interpretador base. Confira [Ambientes do Conda](managing-python-environments-in-visual-studio.md#conda-environments). |
::: moniker-end

::: moniker range=">=vs-2019"
Para alterar o ambiente para um projeto, clique com botão direito no nó **Ambientes do Python** e selecione **Adicionar Ambiente**, ou selecione **Adicionar Ambiente** na lista suspensa do ambiente na barra de ferramentas do Python.

Na caixa de diálogo **Adicionar Ambiente**, selecione a guia **Ambiente existente** e selecione um novo ambiente na lista suspensa **Ambiente**:

![Selecionar um ambiente do projeto na caixa de diálogo Adicionar Ambientes](media/environments/environments-project-2019.png)

Se você já adicionou um ambiente diferente do padrão global a um projeto, talvez seja necessário ativar um ambiente recém-adicionado. Clique com o botão direito do mouse nesse ambiente sob o nó **Ambientes do Python** e selecione **Ativar Ambiente**. Para remover um ambiente do projeto, selecione **Remover**.

![Ativação e remoção de um ambiente de projeto](media/environments/environments-project-add-remove-2019.png)
::: moniker-end

## <a name="use-virtual-environments"></a>Usar ambientes virtuais

Um ambiente virtual é uma combinação exclusiva de um intérprete Python específico e um conjunto específico de bibliotecas diferente de outros ambientes conda e globais. Um ambiente virtual é específico a um projeto e é mantido em uma pasta do projeto. Essa pasta contém as bibliotecas instaladas do ambiente e um arquivo *pyvenv.cfg* que especifica o caminho do *interpretador de base* do ambiente em outro lugar no sistema de arquivos. Ou seja, um ambiente virtual não contém uma cópia do interpretador, apenas um link para ele.

Um benefício de usar um ambiente virtual é que, à medida que você desenvolve um projeto ao longo do tempo, o ambiente virtual sempre reflete as dependências exatas do projeto. (Um ambiente global compartilhado, por outro lado, contém qualquer número de bibliotecas, independentemente de você usá-las em seu projeto ou não). Você pode criar facilmente um arquivo de *requirements.txt* do ambiente virtual, que é usado para reinstalar essas dependências em outro computador de desenvolvimento ou de produção. Para saber mais, confira [Gerenciar pacotes necessários com requirements.txt](managing-required-packages-with-requirements-txt.md).

Quando você abre um projeto no Visual Studio que contém um arquivo *requirements.txt*, o Visual Studio oferece automaticamente a opção de recriar o ambiente virtual. Em computadores em que o Visual Studio não está instalado, você pode usar `pip install -r requirements.txt` para restaurar os pacotes.

Como um ambiente virtual contém um caminho embutido em código para o interpretador de base e é possível recriar o ambiente usando *requirements.txt*, normalmente você omite a pasta de todo o ambiente virtual no controle do código-fonte.

As seções a seguir explicam como ativar um ambiente virtual existente em um projeto e como criar um novo ambiente virtual.

No Visual Studio, um ambiente virtual pode ser ativado para um projeto como qualquer outro por meio do nó **Ambientes do Python** no **Gerenciador de Soluções**.

Assim que um ambiente virtual for adicionado ao projeto, ele será exibido na janela **Ambientes do Python**. Você pode ativá-lo como qualquer outro ambiente e gerenciar seus pacotes.

::: moniker range="vs-2017"
### <a name="create-a-virtual-environment"></a>Criar um ambiente virtual

Você pode criar um novo ambiente virtual diretamente no Visual Studio da seguinte maneira:

1. Clique com o botão direito do mouse em **ambientes Python** no **Gerenciador de soluções** e selecione **Adicionar ambiente virtual**, que abre a seguinte caixa de diálogo:

    ![Criando um ambiente virtual](media/environments/environments-add-virtual-1.png)

1. No **local do ambiente virtual**, especifique um caminho para o ambiente virtual. Se você especificar apenas um nome, o ambiente virtual será criado dentro do projeto atual em uma subpasta com o mesmo nome.

1. Selecione um ambiente como o interpretador base e selecione **Criar**. O Visual Studio exibe uma barra de progresso enquanto configura o ambiente, e baixa todos os pacotes necessários. Após a conclusão, o ambiente virtual aparecerá na janela **Ambientes de Python** para o projeto que o contém.

1. O ambiente virtual não está ativado por padrão. Para ativá-lo para o projeto, clique com o botão direito e selecione **Ativar Ambiente**.

> [!Note]
> Se o caminho do local identificar um ambiente virtual existente, o Visual Studio detectará automaticamente o interpretador base (usando o arquivo *orig-prefix.txt* no diretório *lib* do ambiente) e alterará o botão **Criar** para **Adicionar**.
>
> Se existir um arquivo *requirements.txt* ao adicionar um ambiente virtual, a caixa de diálogo **Adicionar Ambiente Virtual** exibirá uma opção para instalar os pacotes automaticamente, facilitando a recriação de um ambiente em outra máquina:
>
> ![Criar um ambiente virtual com requirements.txt](media/environments/environments-requirements-txt.png)
>
> De qualquer forma, o resultado é o mesmo que se você tivesse usado o comando **Adicionar ambiente virtual existente** .

### <a name="activate-an-existing-virtual-environment"></a>Ativar um ambiente virtual existente

Se você já tiver criado um ambiente virtual em outro lugar, você poderá ativá-lo para um projeto da seguinte maneira:

1. Clique com o botão direito do mouse em **ambientes Python** no **Gerenciador de soluções** e selecione **Adicionar ambiente virtual existente**.

1. Na caixa de diálogo de **procura** exibida, navegue até e selecione a pasta que contém o ambiente virtual e selecione **OK**. Se o Visual Studio detectar um arquivo *requirements.txt* nesse ambiente, ele perguntará se deve instalar esses pacotes.

1. Após alguns instantes, o ambiente virtual aparece sob o nó **ambientes Python** em **Gerenciador de soluções**. O ambiente virtual não está ativado por padrão, então clique duas vezes e selecione **Ativar Ambiente**.
::: moniker-end

::: moniker range=">=vs-2019"
### <a name="create-a-virtual-environment"></a>Criar um ambiente virtual

Você pode criar um novo ambiente virtual diretamente no Visual Studio da seguinte maneira:

1. Clique com o botão direito do mouse em **Ambientes do Python** no **Gerenciador de Soluções** e selecione **Adicionar Ambiente** ou selecione **Adicionar Ambientes** na lista suspensa de ambientes na barra de ferramentas do Python. Na caixa de diálogo **Adicionar Ambiente** que aparece, selecione a guia **Ambiente Virtual**:

    ![Guia ambiente virtual da caixa de diálogo Adicionar Ambiente](media/environments/environments-add-virtual-1-2019.png)

1. Especifique um nome para o ambiente virtual, selecione um interpretador de base e verifique seu local. Sob **Instalar pacotes do arquivo**, forneça o caminho para um arquivo *Requirements.txt*, se desejar.

1. Examine as outras opções na caixa de diálogo:

    | Opção | Descrição |
    | --- | --- |
    | Definir como ambiente atual | Depois que o ambiente for criado, ativa o novo ambiente no projeto selecionado. |
    | Definir como ambiente padrão para novos projetos | Define e ativa o ambiente virtual automaticamente em todos os novos projetos criados no Visual Studio. Ao usar essa opção, o ambiente virtual deve ser colocado em um local fora de um projeto específico.  |
    | Exibir na janela de ambientes do Python | Especifica se deve abrir a janela **Ambientes do Python** depois de criar o ambiente. |
    | Tornar esse ambiente disponível globalmente | Especifica se o ambiente virtual também atua como um ambiente global. Ao usar essa opção, o ambiente virtual deve ser colocado em um local fora de um projeto específico. |

1. Selecione **Criar** para finalizar o ambiente virtual. O Visual Studio exibe uma barra de progresso enquanto configura o ambiente, e baixa todos os pacotes necessários. Após a conclusão, o ambiente virtual é ativado e aparece no nó **Ambientes do Python** no **Gerenciador de Soluções**, e na janela **Ambientes do Python** para o projeto que o contém.

### <a name="activate-an-existing-virtual-environment"></a>Ativar um ambiente virtual existente

Se você já tiver criado um ambiente virtual em outro lugar, você poderá ativá-lo para um projeto da seguinte maneira:

1. Clique com o botão direito do mouse em **Ambientes de Python** no **Gerenciador de Soluções** e escolha **Adicionar Ambiente**.

1. Na caixa de diálogo de **procura** exibida, navegue até e selecione a pasta que contém o ambiente virtual e selecione **OK**. Se o Visual Studio detectar um arquivo *requirements.txt* nesse ambiente, ele perguntará se deve instalar esses pacotes.

1. Após alguns instantes, o ambiente virtual aparece sob o nó **ambientes Python** em **Gerenciador de soluções**. O ambiente virtual não está ativado por padrão, então clique duas vezes e selecione **Ativar Ambiente**.
::: moniker-end

### <a name="remove-a-virtual-environment"></a>Remover um ambiente virtual

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse no ambiente virtual e selecione **remover**.

1. O Visual Studio pergunta se você quer remover ou excluir o ambiente virtual. Selecionar **Remover** o torna indisponível ao projeto, mas o deixa no sistema de arquivos. Selecionar **Excluir** remove o ambiente do projeto e o exclui do sistema de arquivos. O interpretador de base não é afetado.

## <a name="view-installed-packages"></a>Exibir os pacotes instalados

No Gerenciador de Soluções, expanda qualquer nó de um ambiente específico para exibir rapidamente os pacotes instalados nesse ambiente (ou seja, você não pode importar e usar esses pacotes em seu código quando o ambiente estiver ativo):

![Pacotes do Python para um ambiente no Gerenciador de Soluções](media/environments/environments-installed-packages.png)

::: moniker range="vs-2017"
Para instalar novos pacotes, clique com o botão direito do mouse no ambiente e escolha **Instalar Pacote do Python** para alternar para a guia **Pacotes** apropriada na janela **Ambientes de Python**. Insira uma termo de pesquisa (geralmente o nome do pacote) e o Visual Studio exibirá os pacotes correspondentes.
::: moniker-end
::: moniker range=">=vs-2019"
Para instalar novos pacotes, clique com o botão direito no ambiente e escolha **Gerenciar Pacotes do Python** (ou use o botão de pacote na barra de ferramentas do Python) para alternar para a guia **Pacotes** apropriada na janela **Ambientes de Python**. Na guia **Pacotes**, insira um termo de pesquisa (geralmente o nome do pacote) e o Visual Studio exibirá os pacotes correspondentes.
::: moniker-end

No Visual Studio, os pacotes (e as dependências) para a maioria dos ambientes são baixados do [PyPI (Índice do Pacote do Python)](https://pypi.org), no qual você também pode pesquisar os pacotes disponíveis. A barra de status e a janela de saída do Visual Studio mostram informações sobre a instalação. Para desinstalar um pacote, clique com o botão direito do mouse nele e escolha **Remover**.

O gerenciador de pacotes conda geralmente usa `https://repo.continuum.io/pkgs/` como padrão de canal, mas há outros canais disponíveis. Saiba mais em [Gerenciar Canais](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-channels.html) (docs.conda.io).

Saiba que as entradas exibidas podem não ser precisas e a instalação e desinstalação podem não ser confiáveis nem estar disponíveis. O Visual Studio usa o gerenciador de pacotes do PIP, se disponível, e o baixa e o instala quando necessário. O Visual Studio também pode usar o gerenciador de pacotes easy_install. Os pacotes instalados usando `pip` ou `easy_install` por meio da linha de comando também são exibidos.

Observe também que o Visual Studio não oferece suporte no momento ao uso de `conda` para instalar os pacotes em um ambiente conda. Use `conda` na linha de comando.

> [!Tip]
> Uma situação comum em que o Pip não consegue instalar um pacote é quando o pacote inclui o código-fonte para componentes nativos em arquivos * \* . PYD* . Sem a versão necessária do Visual Studio instalada, o PIP não pode compilar esses componentes. A mensagem de erro exibida nessa situação é **erro: Não foi possível localizar vcvarsall.bat**. `easy_install`geralmente é capaz de baixar binários pré-compilados, e você pode baixar um compilador adequado para versões mais antigas do Python do [https://www.microsoft.com/download/details.aspx?id=44266](https://www.microsoft.com/download/details.aspx?id=44266) . Para obter mais detalhes, consulte [Como lidar com o problema “Não é possível localizar vcvarsallbat”](https://devblogs.microsoft.com/python/unable-to-find-vcvarsall-bat/) no blog da equipe das Ferramentas Python.

## <a name="see-also"></a>Confira também

- [Gerenciar ambientes do Python no Visual Studio](managing-python-environments-in-visual-studio.md)
- [Usar requirements.txt para dependências](managing-required-packages-with-requirements-txt.md)
- [Caminhos de pesquisa](search-paths.md)
- [Referência da janela de ambientes do Python](python-environments-window-tab-reference.md)
