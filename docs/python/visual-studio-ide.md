---
title: Visão geral do Visual Studio para desenvolvedores do Python
titleSuffix: ''
ms.date: 03/13/2019
ms.topic: overview
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
dev_langs:
- Python
ms.workload:
- python
- data-science
ms.openlocfilehash: b97655efac3fc42f5e5790e32c97de169e61a6b5
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85520582"
---
# <a name="welcome-to-the-visual-studio-ide--python"></a>Bem-vindo ao IDE do Visual Studio | Python

O *ambiente de desenvolvimento integrado* do Visual Studio é um painel de inicialização criativo para o Python (e outras linguagens) que você pode usar para editar, depurar e testar o código e, em seguida, publicar um aplicativo. Um IDE (ambiente de desenvolvimento integrado) é um programa repleto de recursos que pode ser usado por muitos aspectos do desenvolvimento de software. Além do editor e do depurador padrão fornecidos pela maioria dos IDEs, o Visual Studio inclui ferramentas de preenchimento de código, ambientes de REPL interativo e outras funcionalidades para facilitar o processo de desenvolvimento de software.

[![Visual Studio com um projeto Python](media/tour-ide-overview.png)](media/tour-ide-overview.png#lightbox)

Esta imagem mostra o Visual Studio com um projeto aberto do Python e várias janelas de ferramentas importantes que você provavelmente usará:

- O [**Gerenciador de Soluções**](../ide/solutions-and-projects-in-visual-studio.md) (parte superior direita) permite exibir, navegar e gerenciar os arquivos de código. **Gerenciador de soluções** pode ajudar a organizar seu código agrupando os arquivos em [soluções e projetos](../get-started/tutorial-projects-solutions.md).
  - Ao lado do **Gerenciador de Soluções** estão os [**Ambientes do Python**](managing-python-environments-in-visual-studio.md), nos quais você gerencia os diferentes interpretadores do Python instalados no computador.

  ::: moniker range=">=vs-2019"
  - Também é possível abrir e executar código Python em uma pasta sem criar arquivos de projeto e solução do Visual Studio. Para obter mais informações, consulte [início rápido: abrir e executar o código Python em uma pasta](quickstart-05-python-visual-studio-open-folder.md).
  ::: moniker-end

- A [janela do editor](../ide/writing-code-in-the-code-and-text-editor.md) (parte central), na qual você provavelmente passará a maior parte do tempo, exibe o conteúdo do arquivo. É nela que você [edita o código Python](editing-python-code-in-visual-studio.md), navega na estrutura de código e define pontos de interrupção durante as sessões de depuração. Com o Python, você também pode selecionar o código e pressionar Ctrl+Enter para executar o código em uma [janela de REPL interativo](python-interactive-repl-in-visual-studio.md).

- A [Janela de Saída](../ide/reference/output-window.md) (parte central inferior) é o local em que o Visual Studio envia notificações, como mensagens de erro e de depuração, avisos, mensagens de status da publicação, entre outros. Cada fonte de mensagem tem uma guia própria.
  - Uma [janela de REPL Interativo do Python](python-interactive-repl-in-visual-studio.md) é exibida na mesma área da Janela de Saída.

- O [Team Explorer](/azure/devops/user-guide/work-team-explorer?view=vsts) (canto inferior direito) permite que você acompanhe itens de trabalho e compartilhe o código com outras pessoas usando tecnologias de controle de versão como o [Git](https://git-scm.com/) e o [TFVC (Controle de Versão do Team Foundation)](/azure/devops/repos/tfvc/overview?view=vsts).

## <a name="editions"></a>Edições

O Visual Studio está disponível para o Windows e o Mac; no entanto, o suporte ao Python está disponível apenas no Visual Studio para Windows.

Há três edições do Visual Studio no Windows: Comunidade, Professional e Enterprise. Veja [Comparar IDEs do Visual Studio](https://visualstudio.microsoft.com/vs/compare/) para saber quais recursos são compatíveis com cada edição.

## <a name="popular-productivity-features"></a>Recursos de produtividade populares

Alguns dos recursos populares no Visual Studio que ajudam você a ser mais produtivo durante o desenvolvimento de software incluem:

- [IntelliSense](editing-python-code-in-visual-studio.md#intellisense)

   IntelliSense é um termo usado para um conjunto de recursos que exibe informações sobre o código diretamente no editor e, em alguns casos, escreve pequenos trechos de código para você. É como ter a documentação básica embutida no editor, o que evita que você tenha que consultar informações de tipo em outro lugar. As funcionalidades do IntelliSense variam de acordo com a linguagem e o artigo [Editando o código Python](editing-python-code-in-visual-studio.md#intellisense) traz detalhes sobre o Python. A seguinte ilustração mostra como o IntelliSense exibe uma lista de membros para um tipo:

   ![Preenchimento de membro com o Visual Studio IntelliSense](media/code-editing-completions-simple.png)

- [Refatoração](refactoring-python-code.md)

   Se você clicar com o botão direito do mouse em uma parte do código e selecionar **Ações rápidas e Refatorações**, o Visual Studio fornecerá operações como renomeação inteligente de variáveis, extração de uma ou mais linhas de código em um novo método, alteração da ordem dos parâmetros de método, entre outros.

   ![Refatoração no Visual Studio](media/tour-ide-refactor-extract-method.png)

- [Linting](refactoring-python-code.md)

   O linting verifica se há erros e problemas comuns no código Python, incentivando você a usar bons padrões de codificação do Python.

   ![Comando PyLint no menu de contexto em projetos do Python](media/code-pylint-command.png)

- Caixa de pesquisa

   O Visual Studio pode parecer assustador, às vezes, com tantas propriedades, opções e menus. A caixa de pesquisa é uma ótima maneira de encontrar rapidamente o que você precisa no Visual Studio. Quando você começa a digitar o nome de algo que está procurando, o Visual Studio lista resultados que levam você exatamente para o local em que precisa ir. Caso você precise adicionar uma funcionalidade ao Visual Studio, por exemplo, para adicionar suporte a outra linguagem de programação, a caixa de pesquisa fornecerá resultados que abrem o Instalador do Visual Studio para instalar uma carga de trabalho ou um componente individual.

   ![Caixa de pesquisa no Visual Studio](media/tour-ide-quick-launch.png)

- Rabiscos e [Ações Rápidas](../ide/quick-actions.md)

   Rabiscos são sublinhados ondulados que alertam você sobre erros ou problemas potenciais no código durante a digitação. Essas pistas visuais permitem que você corrija os problemas imediatamente sem esperar que o erro seja descoberto durante o build ou quando você executar o programa. Se você focalizar um rabisco, verá informações adicionais sobre o erro. Uma lâmpada também pode ser exibida na margem esquerda com ações, conhecidas como Ações Rápidas, para corrigir o erro.

   ![Rabiscos no Visual Studio](media/tour-ide-squiggles.png)

- [Acessar e Escolher Definição](../ide/go-to-and-peek-definition.md)

   O recurso **ir para definição** leva você diretamente para o local onde uma função ou tipo é definido. O comando **Inspecionar Definição** exibe a definição em uma janela sem abrir um arquivo separado. O comando **Localizar Todas as Referências** também fornece uma maneira útil de descobrir em que local um identificador especificado foi definido e usado.

   ![Comandos de navegação de código](media/tour-ide-navigation-commands.png)

## <a name="powerful-features-for-python"></a>Funcionalidades avançadas do Python

::: moniker range=">=vs-2019"
- [Executar código sem um projeto](quickstart-05-python-visual-studio-open-folder.md)

    A partir do Visual Studio 2019, você pode abrir uma pasta que contém o código Python para aproveitar recursos como IntelliSense e depuração sem precisar criar um projeto do Visual Studio para o código.
::: moniker-end

- [Colaborar usando o Visual Studio](/visualstudio/liveshare/)
  
    O Visual Studio Live Share permite que você edite e depure de forma colaborativa com outras pessoas em tempo real, independente da linguagem de programação usada ou dos tipos de aplicativo criados. 

- [REPL Interativo do Python](python-interactive-repl-in-visual-studio.md)

    O Visual Studio fornece uma janela interativa REPL (leitura-avaliação-impressão-loop) para cada um dos ambientes do Python, que é uma melhoria do REPL obtido com *python.exe* na linha de comando. Na janela **Interativa**, você pode inserir um código Python arbitrário e ver resultados imediatos.

    ![Janela interativa do Python](media/interactive-window.png)

- [Depuração](debugging-python-in-visual-studio.md)

    O Visual Studio fornece uma experiência de depuração abrangente para Python, incluindo anexar a processos em execução, avaliar expressões na **inspeção** e janelas **imediatas** , inspecionar variáveis locais, pontos de interrupção, instruções Step in/out/over, **definir a próxima instrução**e muito mais. Você também pode depurar um código Python remoto executado em computadores Linux.

    ![Depurando o Python no Visual Studio](media/remote-debugging-breakpoint-hit.png)

- [Interagindo com o C++](working-with-c-cpp-python-in-visual-studio.md)

    Muitas bibliotecas criadas para o Python são escritas em C++ para um desempenho ideal. O Visual Studio fornece funcionalidades sofisticadas para o desenvolvimento de extensões em C++, incluindo a [depuração de modo misto](debugging-mixed-mode-c-cpp-python-in-visual-studio.md).

    ![Depuração de modo misto do Python e do C++ juntos](media/mixed-mode-debugging.png)

- [Criação de perfil](profiling-python-code-in-visual-studio.md)

    Ao usar um interpretador baseado em CPython, você pode avaliar o desempenho do código Python no Visual Studio.

    ![Relatório de desempenho de criação de perfil](media/profiling-results.png)

- [Testes de unidade](unit-testing-python-in-visual-studio.md)

    O Visual Studio fornece suporte integrado para descoberta, execução e depuração de testes de unidade, tudo no contexto do IDE.

    ![Teste de unidade mostrando um status de teste com falha](media/unit-test-A-fail.png)

## <a name="next-steps"></a>Próximas etapas

Explore ainda mais o Python no Visual Studio seguindo um destes tutoriais ou inícios rápidos:

> [!div class="nextstepaction"]
> [Início rápido: criar um aplicativo Web com o Flask](../ide/quickstart-python.md?toc=/visualstudio/python/toc.json&bc=/visualstudio/python/_breadcrumb/toc.json)

> [!div class="nextstepaction"]
> [Trabalhar com o Python no Visual Studio](tutorial-working-with-python-in-visual-studio-step-01-create-project.md)

> [!div class="nextstepaction"]
> [Introdução à estrutura da Web do Django no Visual Studio](learn-django-in-visual-studio-step-01-project-and-solution.md)

> [!div class="nextstepaction"]
> [Introdução à estrutura da Web Flask no Visual Studio](learn-flask-visual-studio-step-01-project-solution.md)

## <a name="see-also"></a>Confira também

- Descubra [mais recursos do Visual Studio](../ide/advanced-feature-overview.md)
- Visite [visualstudio.microsoft.com](https://visualstudio.microsoft.com/vs/)
- Leia [The Visual Studio blog](https://devblogs.microsoft.com/visualstudio/) (O blog do Visual Studio)
