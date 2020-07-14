---
title: Referência da janela de ambientes do Python
description: Detalhes sobre cada uma das guias que aparecem na janela Ambientes de Python no Visual Studio.
ms.date: 03/18/2019
ms.topic: reference
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: f08709c5231b2981db67900f47b49503269e948b
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545490"
---
# <a name="python-environments-window-tabs-reference"></a>Referência as guias da janela Ambientes do Python

Para abrir a janela **Ambientes de Python**:

- Selecione o comando de menu **Exibir**  >  **outros**  >  **ambientes Python** do Windows.
- Clique com o botão direito do mouse no nó **Ambientes do Python** de um projeto no **Gerenciador de Soluções** e escolha **Exibir Todos os Ambientes do Python**.

Se você expandir a janela de **ambientes Python** horizontalmente, essas opções serão mostradas como guias, com as quais você pode achar mais conveniente trabalhar. Para maior clareza, as guias neste artigo são mostradas na exibição expandida.

::: moniker range="vs-2017"
![Exibição expandida da janela Ambientes do Python](media/environments/environments-expanded-view.png)
::: moniker-end
::: moniker range=">=vs-2019"
![Exibição expandida da janela Ambientes do Python](media/environments/environments-expanded-view-2019.png)
::: moniker-end

## <a name="overview-tab"></a>Guia Visão Geral

Fornece informações básicas e comandos para o ambiente:

::: moniker range="vs-2017"
![Guia Visão Geral de Ambientes do Python](media/environments/environments-overview-tab.png)
::: moniker-end
::: moniker range=">=vs-2019"
![Guia Visão Geral de Ambientes do Python](media/environments/environments-overview-tab-2019.png)
::: moniker-end

| Comando | Descrição |
| --- | --- |
| **Tornar este ambiente padrão para novos projetos** | Definir o ambiente ativo, o que pode fazer com que o Visual Studio (2017 versão 15.5 e anteriores) pare de responder brevemente enquanto carrega o banco de dados do IntelliSense. Ambientes com muitos pacotes podem parar de responder por um período maior. |
| **Visitar o site do distribuidor** | Abre um navegador para a URL fornecida para a distribuição de Python. Python 3. x, por exemplo, vai para python.org. |
| **Abrir a janela interativa** | Abre a [janela interativa (REPL)](python-interactive-repl-in-visual-studio.md) para esse ambiente dentro do Visual Studio, aplicando quaisquer [scripts de inicialização (veja abaixo)](#startup-scripts). |
| **Explorar scripts interativos** | Veja os [scripts de inicialização](#startup-scripts). |
| **Usar o modo interativo do IPython** | Quando definido, abre a janela **interativa** com ipython por padrão. Isso habilita os gráficos embutidos e a sintaxe estendida do IPython como `name?` para exibir a ajuda e `!command` para comandos shell. Essa opção é recomendada quando estiver usando uma distribuição Anaconda, pois ela requer pacotes extras. Para obter mais informações, confira [Usar o IPython na Janela Interativa](interactive-repl-ipython.md). |
| **Abrir no PowerShell** | Inicia o interpretador em uma janela de comando do PowerShell. |
| (Links de pasta e do programa) | Forneça acesso rápido à pasta de instalação do ambiente, ao interpretador de *python.exe* e ao interpretador de *pythonw.exe* . O primeiro abre no Windows Explorer, os dois últimos abrem uma janela do console. |

### <a name="startup-scripts"></a>Scripts de inicialização

Como você janelas interativas no fluxo de trabalho diário, provavelmente desenvolverá funções auxiliares que você usa regularmente. Por exemplo, você pode criar uma função que abre um dataframe no Excel e, em seguida, salvar esse código como um script de inicialização para que ele esteja sempre disponível na janela **interativa** .

Os scripts de inicialização contêm código que a janela **interativa** carrega e executa automaticamente, incluindo importações, definições de função e, literalmente, qualquer outra coisa. Esses scripts são referenciados de duas maneiras:

1. Quando você instala um ambiente, o Visual Studio cria uma pasta *Documentos\Visual Studio \<version> \Python \\ \<environment> scripts* em que &lt; &gt; a versão é a versão do Visual Studio (como 2017 ou 2019) e &lt; o ambiente &gt; corresponde ao nome do ambiente. Você pode navegar facilmente para a pasta específica do ambiente com o comando **Explorar scripts interativos**. Quando você inicia a janela **Interativa** para esse ambiente, ela carrega e executa qualquer arquivo *.py* que for encontrado aqui em ordem alfabética.

1. O controle **Scripts** na guia **Ferramentas** > **Opções** > **Python** > **Janelas Interativas** (confira [Opções de janelas Interativas](python-support-options-and-settings-in-visual-studio.md#interactive-windows-options)) destina-se a especificar uma pasta adicional para os scripts de inicialização que estão carregados e são executados em todos os ambientes. No entanto, esse recurso não funciona no momento.

## <a name="configure-tab"></a>Guia Configurar

Se estiver disponível, a guia **Configurar** conterá detalhes, conforme descrito na tabela abaixo. Se essa guia não estiver presente, isso significa que o Visual Studio está gerenciando todos os detalhes automaticamente.

::: moniker range="vs-2017"
![Guia Configurar de Ambientes do Python](media/environments/environments-configure-tab.png)
::: moniker-end
::: moniker range=">=vs-2019"
![Guia Configurar de Ambientes do Python](media/environments/environments-configure-tab-2019.png)
::: moniker-end

| Campo | Descrição |
| --- | --- |
| **Descrição** | O nome a ser fornecido para o ambiente. |
| **Caminho do prefixo** | A localização da pasta base do interpretador. Ao preencher esse valor e clicar em **Detecção Automática**, o Visual Studio tenta preencher os outros campos para você. |
| **Caminho do interpretador** | O caminho para o executável do interpretador, normalmente, o caminho do prefixo seguido por **python.exe** |
| **Interpretador em janelas** | O caminho para o executável que não é de console, geralmente, é o caminho do prefixo seguido por **pythonw.exe**. |
| **Caminho da biblioteca**<br/>(se estiver disponível) | Especifica a raiz da biblioteca padrão, mas esse valor poderá ser ignorado se o Visual Studio conseguir solicitar um caminho mais preciso do interpretador. |
| **Versão da linguagem** | Selecionada no menu suspenso. |
| **Arquitetura** | Normalmente detectado e preenchido automaticamente, caso contrário especifica **32** bits ou **64 bits**. |
| **Variável de ambiente do caminho** | A variável de ambiente que o interpretador usa para encontrar caminhos de pesquisa. O Visual Studio altera o valor da variável ao iniciar o Python, para que ela contenha os caminhos de pesquisa do projeto. Normalmente, essa propriedade deve ser definida como **PYTHONPATH**, mas alguns interpretadores usam outro valor. |

## <a name="packages-tab"></a>Guia Pacotes

*Também chamada de "pip" em versões anteriores.*

Gerencia os pacotes instalados no ambiente usando pip (a guia **Pacotes (PyPI)**) ou o conda (a guia **Pacotes (Conda)**, para ambientes do conda no Visual Studio 2017 versão 15.7 e posteriores). Nessa guia, você também pode procurar e instalar novos pacotes, incluindo as dependências dele.

Os pacotes que já estão instalados são exibidos com controles para atualizar (uma seta para cima) e desinstalar (X em um círculo) o pacote:

![Guia de pacotes de ambientes do Python](media/environments/environments-pip-tab-controls.png)

Inserir um termo de pesquisa filtra a lista de pacotes instalados, bem como os pacotes que podem ser instalados do PyPI.

::: moniker range="vs-2017"
![Guia de pacotes de ambientes do Python com uma pesquisa em "num"](media/environments/environments-pip-tab.png)
::: moniker-end
::: moniker range=">=vs-2019"
![Guia de pacotes de ambientes do Python com uma pesquisa em "num"](media/environments/environments-pip-tab-2019.png)
::: moniker-end

Como você pode ver na imagem acima, os resultados da pesquisa mostram um número de pacotes que correspondem ao termo de pesquisa; no entanto, a primeira entrada da lista é um comando para executar a **instalação \<name> do Pip** diretamente. Se você estiver na guia **pacotes (Conda)** , em vez disso, consulte **Conda \<name> install **:

::: moniker range="vs-2017"
![Guia Pacotes do Conda mostrando um comando conda install](media/environments/environments-conda-tab-install.png)
::: moniker-end
::: moniker range=">=vs-2019"
![Guia Pacotes do Conda mostrando um comando conda install](media/environments/environments-conda-tab-install-2019.png)
::: moniker-end

Em ambos os casos, você pode personalizar a instalação pela adição de argumentos na caixa de pesquisa após o nome do pacote. Quando você inclui argumentos, os resultados da pesquisa mostram **pip install** ou **conda install** seguido do conteúdo da caixa de pesquisa:

::: moniker range="vs-2017"
![Usando argumentos em comandos pip e conda install](media/environments/environments-pip-tab-arguments.png)
::: moniker-end
::: moniker range=">=vs-2019"
![Usando argumentos em comandos pip e conda install](media/environments/environments-pip-tab-arguments-2019.png)
::: moniker-end

Instalar um pacote cria subpastas dentro da pasta *Lib* do ambiente no sistema de arquivos. Por exemplo, se você tiver Python 3.6 instalado em *c:\Python36*, os pacotes são instalados em *c:\Python36\Lib*, se você tiver o Anaconda3 instalado em *c:\Program Files\Anaconda3*, os pacotes serão instalados em *c:\Program Files\Anaconda3\Lib*. Nos ambientes do conda, os pacotes são instalados na pasta do ambiente.

### <a name="grant-administrator-privileges-for-package-install"></a>Conceder privilégios de administrador à instalação do pacote

Ao instalar os pacotes em um ambiente que está localizado em uma área protegida do sistema de arquivos, como *c:\Program Files\Anaconda3\Lib*, o Visual Studio deve executar `pip install` com privilégios elevados para permitir que ele crie subpastas do pacote. Quando a elevação é necessária, o Visual Studio exibe o prompt, os **privilégios de administrador podem ser necessários para instalar, atualizar ou remover pacotes para este ambiente**:

![Solicitação de elevação para a instalação do pacote](media/environments/environments-pip-elevate.png)

**Elevar agora** concede privilégios administrativos para executar o PIP para uma única operação, sujeita também a qualquer prompt de permissão do sistema operacional. A seleção de **continuar sem privilégios de administrador** tenta instalar o pacote, mas a Pip falha ao tentar criar pastas com saída, como **erro: não foi possível criar ' C:\Program Files\Anaconda3\Lib\site-packages\png.py ': permissão negada.**

Selecionar **Sempre elevar ao instalar o u remover pacotes** impede que a caixa de diálogo apareça para o ambiente em questão. Para que a caixa de diálogo apareça novamente, vá para **ferramentas**  >  **Opções**  >  **Python**  >  **geral** e selecione o botão **redefinir todas as caixas de diálogo ocultas permanentemente**.

Nessa mesma guia de **Opções** , você também pode selecionar **sempre executar Pip como administrador** para suprimir a caixa de diálogo para todos os ambientes. Consulte [Opções – guia Geral](python-support-options-and-settings-in-visual-studio.md#general-options).

### <a name="security-restrictions-with-older-versions-of-python"></a>Restrições de segurança com versões mais antigas do Python

Ao usar o Python 2.6, 3.1 e 3.2, o Visual Studio mostra o aviso **Devido a restrições de segurança, a instalação por meio da Internet pode não funcionar nesta versão do Python**:

![Mensagem sobre as restrições de pip install com a versão mais antiga do Python](media/environments/environments-old-version-restriction.png)

O motivo do aviso é que com essas versões anteriores do Python, `pip install` o não contém suporte para a camada de segurança de transporte (TLS) 1,2, que é necessária para baixar pacotes da origem do pacote, PyPI.org. Compilações personalizadas do Python podem dar suporte a TLS 1,2, caso em que isso `pip install` pode funcionar.

É possível baixar o *get-pip.py* apropriado para um pacote em [bootstrap.pypa.io](https://bootstrap.pypa.io/), fazer o download manual de um pacote em [pypi.org](https://pypi.org/) e, em seguida, instalar o pacote dessa cópia local.

No entanto, a recomendação é apenas atualizar para o Python 2.7 ou 3.3+; nesse caso, o aviso não é exibido.

::: moniker range="vs-2017"
## <a name="intellisense-tab"></a>Guia IntelliSense

Mostra o status atual do banco de dados de preenchimento do IntelliSense:

![Guia IntelliSense de Ambientes do Python](media/environments/environments-intellisense-tab.png)

- No Visual Studio 2017 versão 15.5 e anteriores, as conclusões do IntelliSense dependem de um banco de dados que é compilado para essa biblioteca. A criação do banco de dados é feita em segundo plano quando uma biblioteca é instalada, mas pode levar algum tempo e não pode ser concluída quando você começa a escrever código.
- O Visual Studio 2017 versão 15.6 e versões posteriores usam um método mais rápido para fornecer conclusões que não dependem do banco de dados por padrão. Por esse motivo, a guia é rotulada **IntelliSense [banco de dados desabilitado]**. Você pode habilitar o banco de dados desmarcando a opção **ferramentas**  >  **Opções**  >  **Python**  >  **experimental**  >  **usar novo estilo IntelliSense para ambientes**.

Quando o Visual Studio detecta um novo ambiente (ou você adiciona um), ele começa a compilar o banco de dados automaticamente, analisando os arquivos de origem da biblioteca. Esse processo pode levar de um minuto a uma hora ou mais, dependendo do que está instalado. (Anaconda, por exemplo, vem com muitas bibliotecas e demora algum tempo para compilar o banco de dados.) Depois de concluído, você obtém o IntelliSense detalhado e não precisa atualizar o banco de dados novamente (com o botão **Atualizar BD** ) até instalar mais bibliotecas.

As bibliotecas para as quais os dados não foram compilados serão marcadas com um **!**; se o banco de dados de um ambiente não estiver concluído, um **!** também é exibido ao lado da lista do ambiente principal.

::: moniker-end

## <a name="see-also"></a>Consulte também

- [Gerenciar ambientes do Python no Visual Studio](managing-python-environments-in-visual-studio.md)
- [Selecionar um interpretador para um projeto](selecting-a-python-environment-for-a-project.md)
- [Usar requirements.txt para dependências](managing-required-packages-with-requirements-txt.md)
- [Caminhos de pesquisa](search-paths.md)
