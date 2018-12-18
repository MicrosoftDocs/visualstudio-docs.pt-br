---
title: Selecionar um interpretador e um ambiente do Python para um projeto
description: Como selecionar um ambiente ou um interpretador do Python a ser usado para um projeto do Visual Studio, incluindo Anaconda e ambientes virtuais.
ms.date: 11/08/2018
ms.prod: visual-studio-dev15
ms.technology: vs-python
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: douge
ms.workload:
- python
- data-science
ms.openlocfilehash: 0bff5e81fbfda45908315091063833b31abbdd8c
ms.sourcegitcommit: bc43970c000f07c9cc2051f1264a9742943a9755
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51349446"
---
# <a name="how-to-select-a-python-environment-for-a-project"></a>Como selecionar um ambiente do Python para um projeto

Todo o código em um projeto Python é executado dentro do contexto de um ambiente específico, como um ambiente do Python global, um ambiente do Anaconda, um ambiente virtual ou um ambiente do Conda. O Visual Studio também usa esse ambiente para depuração, importação e conclusões de membro, verificação de sintaxe e outras tarefas que exigem serviços de linguagem específicos da versão do Python e um conjunto de pacotes instalados.

Todos os novos projetos Python no Visual Studio são inicialmente configurados para usar o ambiente padrão global, que aparece sob o nó **Ambientes de Python** no **Gerenciador de Soluções**:

![O ambiente de Python global padrão mostrado no Gerenciador de Soluções](media/environments-project.png)

Para alterar o ambiente de um projeto, clique com o botão direito do mouse no nó **Ambientes de Python** e escolha **Adiconar/Remover Ambientes de Python**. Na lista exibida, que inclui ambientes global, virtual e conda, selecione todos os que devem aparecer no nó **Ambientes do Python**:

![Caixa de diálogo Adicionar/Remover Ambientes do Python](media/environments-add-remove.png)

Depois de marcar **OK**, todos os ambientes escolhidos são exibidos no nó **Ambientes de Python**. O ambiente ativado no momento aparece em negrito:

![Vários ambiente de Python mostrados no Gerenciador de Soluções](media/environments-project-multiple.png)

Para ativar rapidamente outro ambiente, clique com o botão direito do mouse no nome desse ambiente e selecione **Ativar ambiente**. Sua escolha é salva com o projeto e esse ambiente é ativado sempre que você abrir o projeto futuramente. Se você desmarcar todas as opções na caixa de diálogo **Adicionar/Remover Ambientes de Python** , o Visual Studio ativa o ambiente padrão global.

O menu de contexto no nó **Ambientes do Python** também fornece comandos adicionais:

| Comando | Descrição |
| --- | --- |
| **Adicionar ambiente virtual** | Inicia o processo de criação de um novo ambiente virtual no projeto. Confira [Criar um ambiente virtual](#create-a-virtual-environment). |
| **Adicionar um ambiente virtual existente** | Solicita que você selecione uma pasta que contém um ambiente virtual e o adiciona à lista em **Ambientes do Python**, mas não o ativa. Confira [Ativar um ambiente virtual existente](#activate-an-existing-virtual-environment). |
| **Criar ambiente do Conda** | Alterna para a *janela* **Ambientes do Python**, em que você insere um nome para o ambiente e especifica o interpretador de base. Confira [Ambientes do Conda](managing-python-environments-in-visual-studio.md#conda-environments). |

## <a name="use-virtual-environments"></a>Usar ambientes virtuais

Um ambiente virtual é uma combinação exclusiva de um intérprete Python específico e um conjunto específico de bibliotecas diferente de outros ambientes conda e globais. Um ambiente virtual é específico a um projeto e é mantido em uma pasta do projeto. Essa pasta contém as bibliotecas instaladas do ambiente e um arquivo *pyvenv.cfg* que especifica o caminho do *interpretador de base* do ambiente em outro lugar no sistema de arquivos. Ou seja, um ambiente virtual não contém uma cópia do interpretador, apenas um link para ele. 

Um benefício de usar um ambiente virtual é que, à medida que você desenvolve um projeto ao longo do tempo, o ambiente virtual sempre reflete as dependências exatas do projeto. (Um ambiente compartilhado global, por outro lado, contém qualquer número de bibliotecas, não importa se você as usa no projeto ou não.) É possível criar facilmente um arquivo *requirements.txt* pelo ambiente virtual, que é usado para reinstalar essas dependências em outro computador de desenvolvimento ou produção. Para saber mais, confira [Gerenciar pacotes necessários com requirements.txt](managing-required-packages-with-requirements-txt.md).

Quando você abre um projeto no Visual Studio que contém um arquivo *requirements.txt*, o Visual Studio oferece automaticamente a opção de recriar o ambiente virtual. Em computadores em que o Visual Studio não está instalado, você pode usar `pip install -r requirements.txt` para restaurar os pacotes.

Como um ambiente virtual contém um caminho embutido em código para o interpretador de base e é possível recriar o ambiente usando *requirements.txt*, normalmente você omite a pasta de todo o ambiente virtual no controle do código-fonte.

As seções a seguir explicam como ativar um ambiente virtual existente em um projeto e como criar um novo ambiente virtual.

No Visual Studio, um ambiente virtual pode ser ativado para um projeto como qualquer outro por meio do nó **Ambientes do Python** no **Gerenciador de Soluções**.

Assim que um ambiente virtual for adicionado ao projeto, ele será exibido na janela **Ambientes do Python**. Você pode ativá-lo como qualquer outro ambiente e gerenciar seus pacotes.

### <a name="create-a-virtual-environment"></a>Criar um ambiente virtual

Você pode criar um novo ambiente virtual diretamente do Visual Studio da seguinte maneira:

1. Clique com o botão direito do mouse em **Ambientes de Python** no **Gerenciador de Soluções** e escolha **Adicionar Ambiente Virtual**, que abre a seguinte caixa de diálogo:

    ![Criando um ambiente virtual](media/environments-add-virtual-1.png)

1. No **local do ambiente virtual**, especifique um caminho para o ambiente virtual. Se você especificar apenas um nome, o ambiente virtual será criado dentro do projeto atual em uma subpasta com o mesmo nome.

1. Selecione um ambiente como o interpretador base e selecione **Criar**. O Visual Studio exibe uma barra de progresso enquanto configura o ambiente, e baixa todos os pacotes necessários. Neste ponto, o ambiente virtual aparece na janela **Ambientes de Python** para o projeto que o contém.

1. O ambiente virtual não está ativado por padrão. Para ativá-lo para o projeto, clique com o botão direito e selecione **Ativar Ambiente**.

> [!Note]
> Se o caminho do local identificar um ambiente virtual existente, o Visual Studio detectará automaticamente o interpretador base (usando o arquivo *orig-prefix.txt* no diretório *lib* do ambiente) e alterará o botão **Criar** para **Adicionar**.
>
> Se existir um arquivo *requirements.txt* ao adicionar um ambiente virtual, a caixa de diálogo **Adicionar Ambiente Virtual** exibirá uma opção para instalar os pacotes automaticamente, facilitando a recriação de um ambiente em outra máquina:
>
> ![Criar um ambiente virtual com requirements.txt](media/environments-requirements-txt.png)
>
> De qualquer forma, o resultado será como se você tivesse usado o comando **Adicionar ambiente virtual existente**.

### <a name="activate-an-existing-virtual-environment"></a>Ativar um ambiente virtual existente

Se você já tiver criado um ambiente virtual em outro lugar, você poderá ativá-lo para um projeto da seguinte maneira:

1. Clique com o botão direito do mouse em **Ambientes de Python** no **Gerenciador de Soluções** e escolha **Adicionar ambiente virtual existente**.

1. Na caixa de diálogo **Procurar** que aparece, navegue até a pasta que contém o ambiente virtual, marque-a e escolha **OK**. Se o Visual Studio detectar um arquivo *requirements.txt* nesse ambiente, ele perguntará se deve instalar esses pacotes.

1. Após alguns instantes, o ambiente virtual aparecerá no nó **Ambientes de Python** no **Gerenciador de Soluções**. O ambiente virtual não está ativado por padrão, então clique duas vezes e selecione **Ativar Ambiente**.

### <a name="remove-a-virtual-environment"></a>Remover um ambiente virtual

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse no ambiente virtual e escolha **Remover**.

1. O Visual Studio pergunta se você quer remover ou excluir o ambiente virtual. Selecionar **Remover** o torna indisponível ao projeto, mas o deixa no sistema de arquivos. Selecionar **Excluir** remove o ambiente do projeto e o exclui do sistema de arquivos. O interpretador de base não é afetado.

## <a name="view-installed-packages"></a>Exibir os pacotes instalados

No Gerenciador de Soluções, expanda qualquer nó de um ambiente específico para exibir rapidamente os pacotes instalados nesse ambiente (ou seja, você não pode importar e usar esses pacotes em seu código quando o ambiente estiver ativo):

![Pacotes do Python para um ambiente no Gerenciador de Soluções](media/environments-installed-packages.png)

Para instalar novos pacotes, clique com o botão direito do mouse no ambiente e escolha **Instalar Pacote do Python** para alternar para a guia **Pacotes** na janela **Ambientes de Python**. Insira uma termo de pesquisa (geralmente o nome do pacote) e o Visual Studio exibirá os pacotes correspondentes.

No Visual Studio, os pacotes (e as dependências) são baixados no [PyPI (Índice do Pacote do Python)](https://pypi.org), no qual você também pode pesquisar os pacotes disponíveis. A barra de status e a janela de saída do Visual Studio mostram informações sobre a instalação. Para desinstalar um pacote, clique com o botão direito do mouse nele e escolha **Remover**.

Saiba que as entradas exibidas podem não ser precisas e a instalação e desinstalação podem não ser confiáveis nem estar disponíveis. O Visual Studio usa o gerenciador de pacotes do PIP, se disponível, e o baixa e o instala quando necessário. O Visual Studio também pode usar o gerenciador de pacotes easy_install. Os pacotes instalados usando `pip` ou `easy_install` por meio da linha de comando também são exibidos.

Observe também que o Visual Studio não oferece suporte no momento ao uso de `conda` para instalar os pacotes em um ambiente conda. Use `conda` na linha de comando.

> [!Tip]
> Uma situação comum em que o PIP não conseguirá instalar um pacote ocorrerá quando o pacote incluir o código-fonte para componentes nativos em arquivos *\*.pyd*. Sem a versão necessária do Visual Studio instalada, o PIP não pode compilar esses componentes. A mensagem de erro exibida nessa situação é **erro: Não foi possível localizar vcvarsall.bat**. O `easy_install` consegue baixar os binários pré-compilados e é possível baixar um compilador adequado para versões mais antigas do Python em [https://aka.ms/VCPython27](https://aka.ms/VCPython27). Para obter mais detalhes, consulte [Como lidar com o problema “Não é possível localizar vcvarsallbat”](https://blogs.msdn.microsoft.com/pythonengineering/2016/04/11/unable-to-find-vcvarsall-bat/) no blog da equipe das Ferramentas Python.

## <a name="see-also"></a>Consulte também

- [Gerenciar ambientes do Python no Visual Studio](managing-python-environments-in-visual-studio.md)
- [Usar requirements.txt para dependências](managing-required-packages-with-requirements-txt.md)
- [Caminhos de pesquisa](search-paths.md)
- [Referência à janela Ambientes do Python](python-environments-window-tab-reference.md)
