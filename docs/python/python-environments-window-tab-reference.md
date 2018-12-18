---
title: Referência da janela de ambientes do Python
description: Detalhes sobre cada uma das guias que aparecem na janela Ambientes de Python no Visual Studio.
ms.date: 09/04/2018
ms.prod: visual-studio-dev15
ms.technology: vs-python
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: douge
ms.workload:
- python
- data-science
ms.openlocfilehash: 45a14fb5667d7eb28d4d298731886db662985d17
ms.sourcegitcommit: 9ea4b62163ad6be556e088da1e2a355f31366f39
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43996071"
---
# <a name="python-environments-window-tabs-reference"></a>Referência as guias da janela Ambientes do Python

Para abrir a janela **Ambientes de Python**:

- Selecione o comando de menu **Exibir** > **Outras Janelas** > **Ambientes do Python**.
- Clique com o botão direito do mouse no nó **Ambientes do Python** de um projeto no **Gerenciador de Soluções** e escolha **Exibir Todos os Ambientes do Python**.

Se você expandir a janela **Ambientes do Python** até um tamanho grande o suficiente, essas opções serão mostradas como guias, o que talvez você considere mais conveniente para trabalhar. Para maior clareza, as guias neste artigo são mostradas na exibição expandida.

![Exibição expandida da janela Ambientes do Python](media/environments-expanded-view.png)

## <a name="overview-tab"></a>Guia Visão Geral

Fornece informações básicas e comandos para o ambiente:

![Guia Visão Geral de Ambientes do Python](media/environments-overview-tab.png)

| Comando | Descrição |
| --- | --- |
| **Tornar este ambiente padrão para novos projetos** | Definir o ambiente ativo, o que pode fazer com que o Visual Studio (2017 versão 15.5 e anteriores) pare de responder brevemente enquanto carrega o banco de dados do IntelliSense. Ambientes com muitos pacotes podem parar de responder por um período maior. |
| **Visitar o site do distribuidor** | Abre um navegador para a URL fornecida para a distribuição de Python. Python 3. x, por exemplo, vai para python.org. |
| **Abrir a janela interativa** | Abre a [janela interativa (REPL)](python-interactive-repl-in-visual-studio.md) para esse ambiente dentro do Visual Studio, aplicando quaisquer [scripts de inicialização (veja abaixo)](#startup-scripts). |
| **Explorar scripts interativos** | Veja os [scripts de inicialização](#startup-scripts). |
| **Usar o modo interativo do IPython** | Quando definido, abre a janela **Interativa** com IPython por padrão. Isso habilita os gráficos embutidos e a sintaxe estendida do IPython como `name?` para exibir a ajuda e `!command` para comandos shell. Essa opção é recomendada quando estiver usando uma distribuição Anaconda, pois ela requer pacotes extras. Para obter mais informações, confira [Usar o IPython na Janela Interativa](interactive-repl-ipython.md). |
| **Abrir no PowerShell** | Inicia o interpretador em uma janela de comando do PowerShell. |
| (Links de pasta e do programa) | Os interpretadores *python.exe* e *pythonw.exe* fornecem acesso rápido à pasta de instalação do ambiente. O primeiro abre no Windows Explorer, os dois últimos abrem uma janela do console. |

### <a name="startup-scripts"></a>Scripts de inicialização

Como você janelas interativas no fluxo de trabalho diário, provavelmente desenvolverá funções auxiliares que você usa regularmente. Por exemplo, você pode criar uma função que abre um DataFrame no Excel e, em seguida, salva esse código como um script de inicialização para que ele esteja sempre disponível na janela **Interativa**.

Os scripts de inicialização contêm o código que a janela **Interativa** carrega e executa automaticamente, incluindo importações, definições de função e literalmente qualquer outra coisa. Esses scripts são referenciados de duas maneiras:

1. Quando você instala um ambiente, o Visual Studio cria uma pasta *Documents\Visual Studio 2017\Python Scripts\\\<environment>* em que &lt;environment&gt; corresponde ao nome do ambiente. Você pode navegar facilmente para a pasta específica do ambiente com o comando **Explorar scripts interativos**. Quando você inicia a janela **Interativa** para esse ambiente, ela carrega e executa qualquer arquivo *.py* que for encontrado aqui em ordem alfabética.

1. O controle **Scripts** na guia **Ferramentas** > **Opções** > **Ferramentas Python** > **Janelas Interativas** (confira [Opções de janelas Interativas](python-support-options-and-settings-in-visual-studio.md#interactive-windows-options)) destina-se a especificar uma pasta adicional para os scripts de inicialização que estão carregados e são executados em todos os ambientes. No entanto, esse recurso não funciona no momento.

## <a name="configure-tab"></a>Guia Configurar

Se estiver disponível, conterá detalhes, conforme descrito na tabela abaixo. Se essa guia não estiver presente, isso significa que o Visual Studio está gerenciando todos os detalhes automaticamente.

![Guia Configurar de Ambientes do Python](media/environments-configure-tab.png)

| Campo | Descrição |
| --- | --- |
| **Descrição** | O nome a ser fornecido para o ambiente. |
| **Caminho do prefixo** | A localização da pasta base do interpretador. Ao preencher esse valor e clicar em **Detecção Automática**, o Visual Studio tenta preencher os outros campos para você. |
| **Caminho do interpretador** | O caminho para o executável do interpretador, normalmente, o caminho do prefixo seguido por **python.exe** |
| **Interpretador de janela** | O caminho para o executável que não é de console, geralmente, é o caminho do prefixo seguido por **pythonw.exe**. |
| **Caminho da biblioteca**<br/>(se estiver disponível) | Especifica a raiz da biblioteca padrão, mas esse valor poderá ser ignorado se o Visual Studio conseguir solicitar um caminho mais preciso do interpretador. |
| **Versão da linguagem** | Selecionada no menu suspenso. |
| **Arquitetura** | Normalmente, detectada e preenchida automaticamente. Caso contrário, especifica **32 bits** ou **64 bits**. |
| **Variável de ambiente do caminho** | A variável de ambiente que o interpretador usa para encontrar caminhos de pesquisa. O Visual Studio altera o valor da variável ao iniciar o Python, para que ela contenha os caminhos de pesquisa do projeto. Normalmente, essa propriedade deve ser definida como **PYTHONPATH**, mas alguns interpretadores usam outro valor. |

## <a name="packages-tab"></a>Guia Pacotes

*Também chamada de "pip" em versões anteriores.*

Gerencia os pacotes instalados no ambiente usando PIP, permitindo também pesquisar e instalar novos (incluindo as dependências). No Visual Studio 2017 versão 15.7 e posterior, uma guia **Pacotes (Conda)** é exibida, que usa o gerenciador de pacotes do Conda. (Se não vir essa opção, defina a opção **Ferramentas** > **Opções** > **Python** > **Experimental** > **Usar gerenciador de pacotes Conda quando estiver disponível (em vez de PIP)** e reinicie o Visual Studio.)

Os pacotes que já estão instalados são exibidos com controles para atualizar (uma seta para cima) e desinstalar (X em um círculo) o pacote:

![Guia de pacotes de ambientes do Python](media/environments-pip-tab-controls.png)

Inserir um termo de pesquisa filtra a lista de pacotes instalados, bem como os pacotes que podem ser instalados do PyPI.

![Guia de pacotes de ambientes do Python com uma pesquisa em "num"](media/environments-pip-tab.png)

Como você pode ver na imagem acima, os resultados da pesquisa mostram vários pacotes que correspondem ao termo de pesquisa. A primeira entrada na lista, no entanto, é um comando para executar **pip install \<name>** diretamente. Caso esteja na guia **Pacotes (Conda)**, você verá **conda install \<name>**:

![Guia Pacotes do Conda mostrando um comando conda install](media/environments-conda-tab-install.png)

Em ambos os casos, você pode personalizar a instalação pela adição de argumentos na caixa de pesquisa após o nome do pacote. Quando você inclui argumentos, os resultados da pesquisa mostram **pip install** ou **conda install** seguido do conteúdo da caixa de pesquisa:

![Usando argumentos em comandos pip e conda install](media/environments-pip-tab-arguments.png)

Instalar um pacote cria subpastas dentro da pasta *Lib* do ambiente no sistema de arquivos. Por exemplo, se você tiver Python 3.6 instalado em *c:\Python36*, os pacotes são instalados em *c:\Python36\Lib*, se você tiver o Anaconda3 instalado em *c:\Program Files\Anaconda3*, os pacotes serão instalados em *c:\Program Files\Anaconda3\Lib*.

### <a name="grant-administrator-privileges-for-package-install"></a>Conceder privilégios de administrador à instalação do pacote

Ao instalar os pacotes em um ambiente que está localizado em uma área protegida do sistema de arquivos, como *c:\Program Files\Anaconda3\Lib*, o Visual Studio deve executar `pip install` com privilégios elevados para permitir que ele crie subpastas do pacote. Quando a elevação é necessária, o Visual Studio exibe o prompt **Podem ser necessários privilégios de administrador para instalar, atualizar ou remover pacotes para esse ambiente**:

![Solicitação de elevação para a instalação do pacote](media/environments-pip-elevate.png)

**Elevar agora** concede privilégios administrativos para executar o PIP para uma única operação, sujeita também a qualquer prompt de permissão do sistema operacional. Escolher **Continuar sem privilégios de administrador** tenta instalar o pacote, mas o PIP falha ao tentar criar pastas com uma saída como **erro: não foi possível criar 'C:\Arquivos de Programas\Anaconda3\Lib\site-packages\png.py': permissão negada.**

Selecionar **Sempre elevar ao instalar o u remover pacotes** impede que a caixa de diálogo apareça para o ambiente em questão. Para fazer a caixa de diálogo aparecer novamente, vá para **Ferramentas** > **Opções** > **Ferramentas Python** > **Geral** e escolha o botão **Redefinir todas as caixas de diálogo permanentemente ocultas**.

Nessa mesma guia de **Opções**, você também pode escolher **Sempre executar o PIP como administrador** para suprimir a caixa de diálogo para todos os ambientes. Consulte [Opções – guia Geral](python-support-options-and-settings-in-visual-studio.md#general-options).

### <a name="security-restrictions-with-older-versions-of-python"></a>Restrições de segurança com versões mais antigas do Python

Ao usar o Python 2.6, 3.1 e 3.2, o Visual Studio mostra o aviso **Devido a restrições de segurança, a instalação por meio da Internet pode não funcionar nesta versão do Python**:

![Mensagem sobre as restrições de pip install com a versão mais antiga do Python](media/environments-old-version-restriction.png)

O motivo para o aviso é que, com essas versões mais antigas do Python, `pip install` não contém suporte para o protocolo TLS 1.2, que é necessário para baixar pacotes da origem do pacote, pypi.org. Os builds personalizados do Python podem dar suporte ao TLS 1.2; nesse caso, `pip install` poderá funcionar.

É possível baixar o *get-pip.py* apropriado para um pacote em [bootstrap.pypa.io](https://bootstrap.pypa.io/), fazer o download manual de um pacote em [pypi.org](https://pypi.org/) e, em seguida, instalar o pacote dessa cópia local.

No entanto, a recomendação é apenas atualizar para o Python 2.7 ou 3.3+; nesse caso, o aviso não é exibido.

## <a name="intellisense-tab"></a>Guia IntelliSense

Mostra o status atual do banco de dados de preenchimento do IntelliSense:

![Guia IntelliSense de Ambientes do Python](media/environments-intellisense-tab.png)

- No **Visual Studio 2017 versão 15.5** e anteriores, as conclusões do IntelliSense dependem de um banco de dados que é compilado para essa biblioteca. A criação do banco de dados é feita em segundo plano quando uma biblioteca é instalada, mas pode levar algum tempo e não pode ser concluída quando você começa a escrever código.
- O **Visual Studio 2017 versão 15.6** e versões posteriores usam um método mais rápido para fornecer conclusões que não dependem do banco de dados por padrão. Por esse motivo, a guia é rotulada **IntelliSense [banco de dados desabilitado]**. É possível habilitar o banco de dados desmarcando a opção **Ferramentas** > **Opções** > **Python** > **Experimental** > **Usar novo estilo de IntelliSense para ambientes**.

Quando o Visual Studio detecta um novo ambiente (ou você adiciona um), ele começa a compilar o banco de dados automaticamente, analisando os arquivos de origem da biblioteca. Esse processo pode levar de um minuto a uma hora ou mais, dependendo do que está instalado. (O Anaconda, por exemplo, é fornecido com várias bibliotecas e leva algum tempo para compilar o banco de dados.) Depois de concluído, você obtém um IntelliSense detalhado não precisa atualizar o banco de dados novamente (com o botão **Atualizar Banco de Dados**) quando instalar mais bibliotecas.

As bibliotecas para as quais os dados não foram compilados serão marcadas com um **!**; se o banco de dados de um ambiente não estiver concluído, um **!** também é exibido ao lado da lista do ambiente principal.

## <a name="see-also"></a>Consulte também

- [Gerenciar ambientes do Python no Visual Studio](managing-python-environments-in-visual-studio.md)
- [Selecionar um intérprete para um projeto](selecting-a-python-environment-for-a-project.md)
- [Usar requirements.txt para dependências](managing-required-packages-with-requirements-txt.md)
- [Caminhos de pesquisa](search-paths.md)
