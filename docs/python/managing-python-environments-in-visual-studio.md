---
title: Gerenciar ambientes e interpretadores Python
description: Use a janela Ambientes Python para gerenciar ambientes globais, virtuais e conda, para instalar interpretadores e pacotes Python e atribuir ambientes a projetos do Visual Studio.
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
ms.openlocfilehash: f69178fde2a0912d39c813028385f21f6ca87d7a
ms.sourcegitcommit: bc43970c000f07c9cc2051f1264a9742943a9755
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51349355"
---
# <a name="how-to-create-and-manage-python-environments-in-visual-studio"></a>Como criar e gerenciar ambientes Python no Visual Studio

Um *ambiente* Python é um contexto em que você executa o código Python e inclui ambientes globais, virtuais e conda. Um ambiente é composto por um interpretador, uma biblioteca (normalmente a Biblioteca Padrão do Python) e um conjunto de pacotes instalados. Juntos, esses componentes determinam quais constructos de linguagem e qual sintaxe são válidos, qual funcionalidade do sistema operacional pode ser acessada e quais pacotes podem ser usados.

No Visual Studio no Windows, use a janela **Ambientes do Python**, conforme descrito neste artigo, para gerenciar ambientes e selecionar um como o padrão para novos projetos. Outros aspectos dos ambientes são encontrados nos seguintes artigos:

- Para qualquer projeto, você pode [selecionar um ambiente específico](selecting-a-python-environment-for-a-project.md) em vez de usar o padrão.

- Para obter detalhes de como criar e usar ambientes virtuais para projetos Python, confira [Usar ambientes virtuais](selecting-a-python-environment-for-a-project.md#use-virtual-environments).

- Se desejar instalar pacotes em um ambiente, confira a [referência da guia Pacotes](python-environments-window-tab-reference.md#packages-tab).

- Para instalar outro interpretador do Python, confira [Instalar interpretadores do Python](installing-python-interpreters.md). Em geral, se você baixar e executar um instalador de uma distribuição principal do Python, o Visual Studio detectará que a nova instalação e o ambiente aparecem na janela **Ambientes do Python** e podem ser selecionados para projetos.

Se você está começando a usar o Python no Visual Studio, os artigos a seguir também fornecem informações gerais:

- [Trabalhar com o Python no Visual Studio](overview-of-python-tools-for-visual-studio.md)
- [Instalar o suporte ao Python no Visual Studio](installing-python-support-in-visual-studio.md)

> [!Note]
> Você não pode gerenciar ambientes de código Python abertos somente como uma pasta usando o comando **Arquivo** > **Abrir** > **Pasta**. Em vez disso, [Crie um projeto em Python com o código existente](quickstart-01-python-in-visual-studio-project-from-existing-code.md) para aproveitar os recursos do ambiente do Visual Studio.

## <a name="the-python-environments-window"></a>A janela Ambientes do Python

*(As capturas de tela mostradas nesta seção representam o Visual Studio 15.8. Você poderá ver uma interface do usuário diferente dependendo da sua versão do Visual Studio.)*

Os ambientes conhecidos pelo Visual Studio são exibidos na janela **Ambientes Python**. Para abrir a janela, use um dos seguintes métodos:

- Selecione o comando de menu **Exibir** > **Outras Janelas** > **Ambientes do Python**.
- Clique com o botão direito do mouse no nó **Ambientes do Python** de um projeto no **Gerenciador de Soluções** e selecione **Exibir Todos os Ambientes do Python**:

    ![Comando Exibir Todos os Ambientes no Gerenciador de Soluções](media/environments-view-all.png)

Em ambos os casos, a janela **Ambientes do Python** é exibida junto com o **Gerenciador de Soluções**:

![Janela Ambientes do Python](media/environments-default-view.png)

O Visual Studio procura por ambientes globais instalados usando o Registro (seguindo o [PEP 514](https://www.python.org/dev/peps/pep-0514/)), junto com os ambientes virtuais e os ambientes do Conda (confira [Tipos de ambientes](#types-of-environments)). Se um ambiente esperado na lista não for exibido, confira [Manually identify an existing environment](#manually-identify-an-existing-environment) (Identificar manualmente um ambiente existente).

Quando você seleciona um ambiente na lista, o Visual Studio exibe várias propriedades e comandos para esse ambiente na guia **Visão geral**. Por exemplo, é possível ver na imagem acima que o local do interpretador é *C:\Python36-32*. Use a lista suspensa embaixo da lista de ambientes para alternar para diferentes guias como **Pacotes** e **IntelliSense**. Essas guias são descritas na [referência à guia da janela Ambientes do Python](python-environments-window-tab-reference.md).

A seleção de um ambiente não altera sua relação com nenhum projeto. O ambiente padrão, mostrado em negrito na lista, é aquele que o Visual Studio usa para os novos projetos. Para usar um ambiente diferente com os novos projetos, use o comando **Tornar este ambiente o padrão para novos projetos**. Dentro do contexto de um projeto sempre é possível selecionar um ambiente específico. Para obter mais informações, confira [Selecionar um ambiente para um projeto](selecting-a-python-environment-for-a-project.md).

À direita de cada ambiente listado está um controle que abre uma janela **Interativa** nesse ambiente. (No Visual Studio 2017 15.5 e anterior, é exibido outro controle que atualiza o banco de dados do IntelliSense para esse ambiente. Confira [Referência à guia da janela Ambientes](python-environments-window-tab-reference.md#intellisense-tab) para obter detalhes sobre o banco de dados.)

> [!Tip]
> Ao expandir a janela **Ambientes do Python** até o tamanho suficiente, você obtém uma exibição mais completa de seus ambientes que pode ser mais conveniente para trabalhar.
>
> ![Exibição expandida da janela Ambientes do Python](media/environments-expanded-view.png)

> [!Note]
> Embora o Visual Studio respeite a opção de pacotes de site do sistema, ele não fornece uma maneira de alterá-lo no próprio Visual Studio.

|   |   |
|---|---|
| ![ícone de câmera para vídeo](../install/media/video-icon.png "Assistir a um vídeo") | [Assista a um vídeo (Microsoft Virtual Academy)](https://mva.microsoft.com/en-US/training-courses/python-tools-for-visual-studio-2017-18121?l=qrDmN4LWE_8305918567) sobre os ambientes do Python no Visual Studio (2min35s).|

### <a name="what-if-no-environments-appear"></a>E se nenhum ambiente aparecer?

Se nenhum ambiente aparecer, isso significa que o Visual Studio não conseguiu detectar as instalações de Python nos locais padrão. Por exemplo, você pode ter instalado o Visual Studio 2017 mas limpou todas as opções de interpretador nas opções do instalador para a carga de trabalho do Python. Da mesma forma, você pode ter instalado o Visual Studio 2015 ou anterior, mas não instalou um interpretador manualmente (confira [Instalar interpretadores do Python](installing-python-interpreters.md)).

Se você souber que tem um interpretador do Python no computador, mas o Visual Studio (qualquer versão) não detectá-lo, use o comando **+ Personalizado** para especificar o local manualmente. Consulte a próxima seção, [Identificar manualmente um ambiente existente](#manually-identify-an-existing-environment).

> [!Tip]
> O Visual Studio detecta atualizações para um interpretador existente, como a atualização do Python 2.7.11 para 2.7.14 usando os instaladores de python.org. Durante o processo de instalação, o ambiente mais antigo desaparece da lista **Ambientes Python** antes de a atualização aparecer em seu lugar.
>
> No entanto, se você mover manualmente um interpretador e seu ambiente usando o sistema de arquivos, o Visual Studio não saberá o novo local. Para obter mais informações, confira [Mover um interpretador](installing-python-interpreters.md#move-an-interpreter).

### <a name="types-of-environments"></a>Tipos de ambientes

O Visual Studio pode trabalhar com ambientes globais, virtuais e do Conda.

#### <a name="global-environments"></a>Ambientes globais

Cada instalação do Python (por exemplo, Python 2.7, Python 3.6, Python 3.7, Anaconda 4.4.0 etc., confira [Instalar interpretadores do Python](installing-python-interpreters.md)) mantém seu próprio *ambiente global*. Cada ambiente é composto pelo interpretador do Python específico e sua biblioteca padrão, por um conjunto de pacotes pré-instalados e por todos os pacotes adicionais instalados durante a ativação desse ambiente. A instalação de um pacote em um ambiente global o torna disponível para todos os projetos que usam esse ambiente. Se o ambiente estiver em uma área protegida do sistema de arquivos (em *c:\Arquivos de Programas*, por exemplo), a instalação de pacotes exigirá privilégios de administrador.

Os ambientes globais estão disponíveis para todos os projetos no computador. No Visual Studio, selecione um ambiente global como o padrão, que é usado para todos os projetos, a menos que você escolha especificamente um diferente para um projeto. Para obter mais informações, confira [Selecionar um ambiente para um projeto](selecting-a-python-environment-for-a-project.md).

#### <a name="virtual-environments"></a>Ambientes virtuais

Embora trabalhar em um ambiente global seja uma maneira fácil de começar, ao longo do tempo, esse ambiente ficará desorganizado, com muitos pacotes diferentes que você terá instalado para diferentes projetos. Essa desorganização dificultará o teste completo de um aplicativo em relação a um conjunto específico de pacotes com as versões conhecidas, que é exatamente o tipo de ambiente que você configuraria em um servidor Web ou em um servidor de build. Também poderão ocorrer conflitos quando dois projetos exigirem pacotes incompatíveis ou versões diferentes do mesmo pacote.

Por esse motivo, os desenvolvedores geralmente criam um *ambiente virtual* para um projeto. Um ambiente virtual é uma subpasta em um projeto que contém uma cópia de um interpretador específico. Quando você ativa o ambiente virtual, todos os pacotes passam a ser instalados somente na subpasta desse ambiente. Ao executar um programa em Python nesse ambiente, você sabe que ele será executado somente em relação a esses pacotes específicos.

O Visual Studio dá suporte direto para a criação de um ambiente virtual para um projeto. Por exemplo, se você abrir um projeto que contenha um *requirements.txt* ou criar um projeto usando um modelo que inclua esse arquivo, o Visual Studio solicitará que você crie automaticamente um ambiente virtual e instale essas dependências.

A qualquer momento dentro de um projeto aberto, você pode criar um ambiente virtual. No **Gerenciador de Soluções**, expanda o nó do projeto, clique com o botão direito do mouse no nó **Ambientes do Python** e selecione “Adicionar Ambiente Virtual”. Para obter mais informações, confira [Criar um ambiente virtual](selecting-a-python-environment-for-a-project.md#create-a-virtual-environment).

O Visual Studio também fornece um comando para gerar um arquivo *requirements.txt* de um ambiente virtual, facilitando a recriação do ambiente em outros computadores. Para obter mais informações, confira [Usar ambientes virtuais](selecting-a-python-environment-for-a-project.md#use-virtual-environments).

#### <a name="conda-environments"></a>Ambientes do Conda

Um ambiente do conda é aquele criado usando a ferramenta `conda`, ou com o gerenciamento do conda integrado no Visual Studio 2017 versão 15.7 e superior. (Exige o Anaconda ou Miniconda; o Anaconda está disponível por meio do instalador do Visual Studio. Consulte [Instalação – Visual Studio 2017](installing-python-support-in-visual-studio.md#visual-studio-2017).)

1. Selecione **+ Criar ambiente do conda** na janela **Ambientes do Python**, que abre uma guia **Criar novo ambiente do conda**:

    ![Criar uma guia para um novo ambiente do conda](media/environments-conda-1.png)

1. Insira um nome para o ambiente no campo **Nome**, selecione um interpretador base do Python no campo **Python** e selecione **Criar**.

1. A janela **Saída** mostra o progresso do novo ambiente, com algumas instruções da CLI após a conclusão da criação:

    ![Criação bem-sucedida de um ambiente do conda](media/environments-conda-2.png)

1. No Visual Studio, você pode ativar um ambiente do Conda para um projeto da mesma forma como faria com qualquer outro ambiente, conforme descrito em [Selecionar um ambiente para um projeto](selecting-a-python-environment-for-a-project.md).

1. Para instalar pacotes no ambiente, use a [guia Pacotes](python-environments-window-tab-reference.md#packages-tab).

> [!Note]
> Para obter melhores resultados com ambientes do conda, use o conda 4.4.8 ou posterior (as versões do conda são diferentes das versões do Anaconda). Instale o Anaconda 5.1 por meio do instalador do Visual Studio 2017.

Para ver a versão do conda, na qual os ambientes do conda são armazenados, bem como outras informações, execute `conda info` em um prompt de comando do Anaconda (ou seja, um prompt de comando no qual o Anaconda está no caminho):

```cli
conda info
```

As pastas de ambiente do conda são exibidas da seguinte maneira:

```output
       envs directories : c:\anaconda3\envs
                          C:\Users\user\AppData\Local\conda\conda\envs
                          C:\Users\user\.conda\envs
```

Como os ambientes do conda não são armazenados com um projeto, eles atuam da mesma forma para ambientes globais. Por exemplo, a instalação de um novo pacote em um ambiente do conda torna esse pacote disponível para todos os projetos que usam esse ambiente.

Para o Visual Studio 2017 versão 15.6 e anterior, você pode usar ambientes do conda apontando-os manualmente, conforme descrito em [Identificar manualmente um ambiente existente](#manually-identify-an-existing-environment).

O Visual Studio 2017 versão 15.7 e posterior detecta ambientes do conda automaticamente e exibe-os na janela **Ambientes do Python**, conforme descrito na próxima seção.

## <a name="manually-identify-an-existing-environment"></a>Identificar manualmente um ambiente existente

Use as seguintes etapas para identificar um ambiente instalado em um local não padrão (incluindo ambientes do conda no Visual Studio 2017 versão 15.6 e posterior):

1. Selecione **+ Personalizado** na janela **Ambientes do Python**, que abre a guia **Configurar**:

    ![Exibição padrão de um novo ambiente personalizado](media/environments-custom-1.png)

1. Insira um nome para o ambiente no campo **Descrição**.

1. Insira ou procure (usando **...**) o caminho do interpretador no campo **Caminho do prefixo**.

1. Se o Visual Studio detectar um interpretador Python nessa localização (como o caminho mostrado abaixo para um ambiente de conda), ele habilitará o comando **Detecção Automática**. A seleção de **Detecção Automática** preenche os campos restantes. Você também pode preencher esses campos manualmente.

    ![Habilitar o comando Detecção Automática](media/environments-custom-2.png)

    ![Preenchimento dos campos de ambiente depois de usar a Detecção Automática](media/environments-custom-3.png)

1. Quando os campos contiverem os valores desejados, selecione **Aplicar** para salvar a configuração. Agora, você pode usar o ambiente como qualquer outro no Visual Studio.

1. Se você precisar remover um ambiente identificado manualmente, selecione o comando **Remover** na guia **Configurar**. Ambientes detectados automaticamente não oferecem essa opção. Para saber mais, confira [Guia Configurar](python-environments-window-tab-reference.md#configure-tab).

## <a name="fix-or-delete-invalid-environments"></a>Corrigir ou excluir ambientes inválidos

Se o Visual Studio encontra entradas do Registro para um ambiente, mas o caminho para o interpretador é inválido, a janela **Ambientes do Python** mostra o nome com uma fonte riscada:

![A janela Ambientes do Python mostrando um ambiente inválido](media/environments-invalid-entry.png)

Para corrigir um ambiente que você deseja manter, primeiro tente usar o processo **Reparar** do instalador dele. Os instaladores para o Python 3.x padrão, por exemplo, incluem essa opção.

Para corrigir um ambiente que não tem uma opção de reparo, ou para remover um ambiente inválido, use as etapas a seguir para modificar o Registro diretamente. O Visual Studio atualiza automaticamente a janela **Ambientes do Python** quando você faz alterações no Registro.

1. Execute *regedit.exe*.
1. Navegue para **HKEY_LOCAL_MACHINE\SOFTWARE\Python** para interpretadores de 32 bits ou **HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Python** para interpretadores de 64 bits. Para o IronPython, procure **IronPython**.
1. Expanda o nó que corresponde à distribuição, como **PythonCore** para o CPython ou **ContinuumAnalytics** para o Anaconda. Para o IronPython, expanda o nó de número de versão.
1. Inspecione os valores no nó **InstallPath**:

    ![Entradas do Registro para uma instalação típica do CPython](media/environments-registry-entries.png)

    - Se o ambiente ainda existir no computador, altere o valor de **ExecutablePath** para o local correto. Corrija também os valores **(Padrão)** e **WindowedExecutablePath**, conforme necessário.
    - Se o ambiente não existir mais no computador e você desejar removê-lo da janela **Ambientes do Python**, exclua o nó pai de **InstallPath**, como **3.6** na imagem acima.

## <a name="see-also"></a>Consulte também

- [Instalar intérpretes do Python](installing-python-interpreters.md)
- [Selecionar um intérprete para um projeto](selecting-a-python-environment-for-a-project.md)
- [Usar requirements.txt para dependências](managing-required-packages-with-requirements-txt.md)
- [Caminhos de pesquisa](search-paths.md)
- [Referência à janela Ambientes do Python](python-environments-window-tab-reference.md)
