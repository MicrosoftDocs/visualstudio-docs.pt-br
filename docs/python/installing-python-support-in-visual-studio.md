---
title: Instalar o suporte do Python
description: Como instalar as PTVS (Ferramentas Python para Visual Studio) no Visual Studio 2017, 2015, 2013, 2012 e 2010, incluindo opções e locais de instalação.
ms.date: 03/13/2019
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 910b3b5491660cbcd6132aff68ebeabafaeea0d5
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85540641"
---
# <a name="how-to-install-python-support-in-visual-studio-on-windows"></a>Como instalar o suporte do Python no Visual Studio no Windows

Para instalar o suporte do Python para Visual Studio (também conhecido como Ferramentas Python para Visual Studio ou PTVS), siga as instruções na seção que corresponda à sua versão do Visual Studio:

- [Visual Studio 2017 e Visual Studio de 2019](#visual-studio-2017-and-2019)
- [Visual Studio 2015](#visual-studio-2015)
- [Visual Studio 2013 e anterior](#visual-studio-2013-and-earlier)

Para testar rapidamente o suporte do Python após seguir as etapas de instalação, abra a janela do **Python Interactive** pressionando **ALT** + **I** e inserindo `2+2` . Se você não vir a saída de `4`, verifique as etapas novamente.

> [!Tip]
> A carga de trabalho do Python inclui a extensão útil Cookiecutter, que fornece uma interface gráfica do usuário para descobrir modelos e opções de modelo de entrada e criar projetos e arquivos. Para obter detalhes, confira [Usar o Cookiecutter](using-python-cookiecutter-templates.md).

> [!Note]
> O suporte ao Python não está disponível atualmente no Visual Studio para Mac, mas está disponível no Mac e no Linux por meio do Visual Studio Code. Confira [Perguntas e respostas](overview-of-python-tools-for-visual-studio.md#questions-and-answers).

<a name="visual-studio-2017-and-2019"></a>
## <a name="visual-studio-2019-and-visual-studio-2017"></a>Visual Studio 2019 e Visual Studio de 2017

1. Baixe e execute o Instalador do Visual Studio mais recente. Se já tiver o Visual Studio instalado, execute o Instalador do Visual Studio, selecione a opção **Modificar** (consulte [Modificar o Visual Studio](../install/modify-visual-studio.md)) e vá para a etapa 2.

    > [!div class="nextstepaction"]
    > [Instalar a Comunidade do Visual Studio 2019](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Community&rel=15&rid=34347&utm_source=docs&utm_medium=clickbutton&utm_campaign=python_gettingstarted)

    >[!Tip]
    > A edição Community é para desenvolvedores individuais, aprendizado em sala de aula, pesquisa acadêmica e desenvolvimento de software livre. Para outros usos, instale o [Visual Studio 2019 Professional](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Professional&rel=15&rid=34347&utm_source=docs&utm_medium=clickbutton&utm_campaign=python_gettingstarted) ou o [Visual Studio 2019 Enterprise](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Enterprise&rel=15&rid=34347&utm_source=docs&utm_medium=clickbutton&utm_campaign=python_gettingstarted).

1. O instalador apresenta uma lista de cargas de trabalho, que são grupos de opções relacionadas para áreas de desenvolvimento específicas. Para Python, selecione a carga de trabalho **Desenvolvimento do Python**.

    ![Carga de trabalho de desenvolvimento do Python no instalador do Visual Studio](media/installation-python-workload.png)

    ::: moniker range="vs-2017"
    Opcional: se estiver trabalhando com ciência de dados, considere também a carga de trabalho para **Aplicativos de ciência de dados e análise**. Essa carga de trabalho inclui suporte para as linguagens Python, R e F#. Para obter mais informações, veja [Carga de trabalho para Aplicativos de ciência de dados e análise](data-science-and-analytical-applications-workload.md).

    > [!Note]
    > As cargas de trabalho para Python e para Ciência de dados estão disponíveis apenas com a versão Visual Studio 2017 15.2 e posterior.

    ::: moniker-end

    ::: moniker range=">=vs-2019"
    Opcional: se estiver trabalhando com ciência de dados, considere também a carga de trabalho para **Aplicativos de ciência de dados e análise**. Essa carga de trabalho inclui suporte para as linguagens Python e F#. Para obter mais informações, veja [Carga de trabalho para Aplicativos de ciência de dados e análise](data-science-and-analytical-applications-workload.md).
    ::: moniker-end

1. No lado direito do instalador, escolha opções adicionais se desejado. Ignore essa etapa para aceitar as opções padrão.

    ::: moniker range="vs-2017"
    ![Opções de desenvolvimento do Python no instalador do Visual Studio](media/installation-python-options.png)
    ::: moniker-end

    ::: moniker range=">=vs-2019"
    ![Opções de desenvolvimento do Python no instalador do Visual Studio 2019](media/installation-python-options-2019.png)
    ::: moniker-end

    ::: moniker range="<=vs-2017"
    | Opção | Descrição |
    | --- | --- |
    | Distribuições do Python | Escolha qualquer combinação de opções disponíveis, como variantes de 32 bits e de 64 bits das distribuições do Python 2, do Python 3, do Miniconda, do Anaconda2 e do Anaconda3 com as quais planeja trabalhar. Cada uma delas inclui o interpretador, o runtime e as bibliotecas da distribuição. O Anaconda, especificamente, é uma plataforma de ciência de dados aberta que inclui uma grande variedade de pacotes pré-instalados. (Você pode retornar ao instalador do Visual Studio a qualquer momento para adicionar ou remover distribuições.)  **Observação**: se você tiver instalado uma distribuição fora do instalador do Visual Studio, não será necessário verificar a opção equivalente aqui. O Visual Studio automaticamente detecta as instalações existentes do Python. Confira [A janela Ambientes do Python](managing-python-environments-in-visual-studio.md#the-python-environments-window). Além disso, se uma versão mais nova que a mostrada no instalador do Python estiver disponível, você poderá instalar essa versão separadamente, e o Visual Studio a detectará. |
    | **Suporte do modelo Cookiecutter** | Instala a interface gráfica do usuário Cookiecutter para descobrir modelos, inserir opções de modelo e criar projetos e arquivos. Confira [Usar a extensão Cookiecutter](using-python-cookiecutter-templates.md). |
    | **Suporte Web do Python** | Instala as ferramentas para desenvolvimento para a Web, incluindo suporte à edição HTML, CSS e JavaScript, juntamente com modelos para projetos que usam as estruturas Bottle, Flask e Django. Veja [Modelos de projeto Web do Python](python-web-application-project-templates.md). |
    | **Suporte ao Python IoT** | Compatível com o desenvolvimento do Windows IoT Core usando Python. |
    | **Ferramentas de desenvolvimento nativo do Python** | Instala o compilador do C++ e outros componentes necessários para desenvolver extensões nativas para Python. Confira [Criar uma extensão do C++ para o Python](working-with-c-cpp-python-in-visual-studio.md). Além disso, instale a carga de trabalho **Desenvolvimento de área de trabalho C++** para obter suporte total a C++. |
    | **Principais ferramentas dos Serviços de Nuvem do Azure** | Fornece suporte adicional para os Serviços de Nuvem do Azure do desenvolvedor no Python. Consulte [projetos de serviço de nuvem do Azure](python-azure-cloud-service-project-template.md). |
    ::: moniker-end

    ::: moniker range=">=vs-2019"
    | Opção | Descrição |
    | --- | --- |
    | Distribuições do Python | Escolha qualquer combinação de opções disponíveis, como variantes de 32 bits e de 64 bits das distribuições do Python 2, do Python 3, do Miniconda, do Anaconda2 e do Anaconda3 com as quais planeja trabalhar. Cada uma delas inclui o interpretador, o runtime e as bibliotecas da distribuição. O Anaconda, especificamente, é uma plataforma de ciência de dados aberta que inclui uma grande variedade de pacotes pré-instalados. (Você pode retornar ao instalador do Visual Studio a qualquer momento para adicionar ou remover distribuições.)  **Observação**: se você tiver instalado uma distribuição fora do instalador do Visual Studio, não será necessário verificar a opção equivalente aqui. O Visual Studio automaticamente detecta as instalações existentes do Python. Confira [A janela Ambientes do Python](managing-python-environments-in-visual-studio.md#the-python-environments-window). Além disso, se uma versão mais nova que a mostrada no instalador do Python estiver disponível, você poderá instalar essa versão separadamente, e o Visual Studio a detectará. |
    | **Suporte do modelo Cookiecutter** | Instala a interface gráfica do usuário Cookiecutter para descobrir modelos, inserir opções de modelo e criar projetos e arquivos. Confira [Usar a extensão Cookiecutter](using-python-cookiecutter-templates.md). |
    | **Suporte Web do Python** | Instala as ferramentas para desenvolvimento para a Web, incluindo suporte à edição HTML, CSS e JavaScript, juntamente com modelos para projetos que usam as estruturas Bottle, Flask e Django. Veja [Modelos de projeto Web do Python](python-web-application-project-templates.md). |
    | **Ferramentas de desenvolvimento nativo do Python** | Instala o compilador do C++ e outros componentes necessários para desenvolver extensões nativas para Python. Confira [Criar uma extensão do C++ para o Python](working-with-c-cpp-python-in-visual-studio.md). Além disso, instale a carga de trabalho **Desenvolvimento de área de trabalho C++** para obter suporte total a C++. |
    | **Principais ferramentas dos Serviços de Nuvem do Azure** | Fornece suporte adicional para os Serviços de Nuvem do Azure do desenvolvedor no Python. Consulte [projetos de serviço de nuvem do Azure](python-azure-cloud-service-project-template.md). |
    ::: moniker-end

1. Após a instalação, o instalador fornece opções para modificar, iniciar, reparar ou desinstalar o Visual Studio. O botão **Modificar** transforma-se em **Atualizar** quando há atualizações do Visual Studio disponíveis para os componentes instalados. (A opção **Modificar** está disponível no menu suspenso.) Você também pode iniciar o Visual Studio e o instalador no menu **Iniciar** do Windows pesquisando "Visual Studio".

    ![Iniciando, modificando ou desinstalando o Visual Studio no instalador](media/installation-vs-launch.png)

### <a name="troubleshooting"></a>Solução de problemas

Se você encontrar problemas ao instalar ou executar o Python no Visual Studio, tente o seguinte:

- Determine se o mesmo erro ocorre usando a CLI do Python, ou seja, executando *python.exe* em um prompt de comando.
- Use a opção [**reparar**](../install/repair-visual-studio.md) no instalador do Visual Studio.
- Repare ou reinstale o Python por meio de **configurações**  >  **aplicativos & recursos** no Windows.

**Erro de exemplo**: Falha ao iniciar o processo interativo: System.ComponentModel.Win32Exception (0x80004005): erro desconhecido (0xc0000135) em Microsoft.PythonTools.Repl.PythonInteractiveEvaluator.d__43.MoveNext().

## <a name="visual-studio-2015"></a>Visual Studio 2015

1. Execute o instalador do Visual Studio por meio do **Painel de Controle > Programas e Recursos**, selecionando **Microsoft Visual Studio 2015** e, em seguida, **Alterar**.

1. No instalador, selecione **Modificar**.

1. Selecione **linguagens de programação**  >  **ferramentas Python para Visual Studio** e, em seguida, **Avançar**:

    ![Opção PTVS no instalador do Visual Studio 2015](media/installation-vs2015.png)

1. Depois que a instalação do Visual Studio for concluída, [instale um interpretador do Python de sua escolha](installing-python-interpreters.md). O Visual Studio 2015 oferece suporte somente para o Python 3.5 e anteriores; as versões posteriores geram uma mensagem como **Versão 3.6 do Python incompatível**. Se você já tiver um interpretador instalado e o Visual Studio não o detectar automaticamente, consulte [Identificar manualmente um ambiente existente](managing-python-environments-in-visual-studio.md#manually-identify-an-existing-environment).

## <a name="visual-studio-2013-and-earlier"></a>Visual Studio 2013 e anterior

1. Instale a versão apropriada das Ferramentas Python para Visual Studio para sua versão do Visual Studio:

    - Visual Studio 2013: [PTVS 2.2.2 para Visual Studio 2013](https://github.com/Microsoft/PTVS/releases/v2.2.2). A caixa de diálogo **arquivo**  >  **novo projeto** no Visual Studio 2013 fornece um atalho para esse processo.
    - Visual Studio 2010 e 2012: [PTVS 2.1.1 para Visual Studio 2010 e 2012](https://github.com/Microsoft/PTVS/releases/v2.1.1)

1. [Instale um interpretador do Python de sua escolha](installing-python-interpreters.md). Se você já tiver um interpretador instalado e o Visual Studio não o detectar automaticamente, consulte [Identificar manualmente um ambiente existente](managing-python-environments-in-visual-studio.md#manually-identify-an-existing-environment).

## <a name="install-locations"></a>Locais de instalação

Por padrão, o suporte do Python é instalado para todos os usuários em um computador.

Para o Visual Studio 2019 e Visual Studio 2017, a carga de trabalho do Python é instalada em *%ProgramFiles(x86)%\Microsoft Visual Studio\\<VS_version>\\<VS_edition>Common7\IDE\Extensions\Microsoft\Python*, em que &lt;version&gt; é 2019 ou 2017 e &lt;VS_edition&gt; é Community, Professional ou Enterprise.

Para o Visual Studio 2015 e anterior, os caminhos de instalação são os seguintes:

- 32 bits:
  - Caminho: *% arquivos de programas (x86)% \ Microsoft Visual Studio \<VS_ver> \Common7\IDE\Extensions\Microsoft\Python Tools for Visual Studio \\<PTVS_ver>*
  - Local do caminho no Registro: **HKEY_LOCAL_MACHINE\Software\Microsoft\PythonTools\\<VS_ver>\InstallDir**
- 64 bits:
  - Caminho: *% Program Files%\Microsoft Visual Studio \<VS_ver> \Common7\IDE\Extensions\Microsoft\Python Tools for visual studio \\<PTVS_ver>*
  - Local do caminho no Registro: **HKEY_LOCAL_MACHINE\Software\Wow6432Node\Microsoft\PythonTools\\<VS_ver>\InstallDir**

onde:

- &lt;VS_ver&gt; é:
  - 14.0 para Visual Studio 2015
  - 12.0 para Visual Studio 2013
  - 11.0 para Visual Studio 2012
  - 10.0 para Visual Studio 2010
- &lt;PTVS_ver &gt; é um número de versão, como 2.2.2, 2.1.1, 2,0, 1,5, 1,1 ou 1,0.

### <a name="user-specific-installations-15-and-earlier"></a>Instalações específicas ao usuário (1.5 e anterior)

As Ferramentas Python para Visual Studio 1.5 e anterior permitiam a instalação apenas para o usuário atual e, nesse caso, o caminho da instalação é *%LocalAppData%\Microsoft\VisualStudio\\<VS_ver>\Extensions\Microsoft\Ferramentas Python para Visual Studio\\<PTVS_ver>*, em que &lt;VS_ver&gt; e &lt;PTVS_ver&gt; são iguais ao descrito acima.
