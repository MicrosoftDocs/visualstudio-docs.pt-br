---
title: Início Rápido – Clonar um repositório de código Python
description: Neste início rápido, crie um projeto de Python em Visual Studio por meio da clonagem do repositório de koans do Python usando o Visual Studio Team Explorer.
ms.date: 12/06/2018
ms.topic: quickstart
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 55db74b2b2882aac12ac1587c4e972e31f7dfe10
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99902393"
---
# <a name="quickstart-clone-a-repository-of-python-code-in-visual-studio"></a>Início Rápido: clonar um repositório de código do Python no Visual Studio

Depois de [instalar o suporte do Python no Visual Studio](installing-python-support-in-visual-studio.md), adicione a extensão do GitHub para Visual Studio. A extensão permite que você clone facilmente um repositório de código Python e crie um projeto usando-o de dentro do IDE. Também é possível clonar repositórios na linha de comando e, em seguida, trabalhar com eles no Visual Studio.

## <a name="install-the-github-extension-for-visual-studio"></a>Instale a extensão do GitHub para o Visual Studio

[!INCLUDE[install-github-extension](includes/install-github-extension.md)]

## <a name="work-with-github-in-visual-studio"></a>Trabalhe com o GitHub no Visual Studio

1. Inicie o Visual Studio.

1. Selecione **Exibir**  >  **Team Explorer** para abrir a janela de **Team Explorer** na qual você pode se conectar ao GitHub ou Azure Repos ou clonar um repositório. Se a página **Conectar** não estiver exibida abaixo, selecione o ícone de plug na barra de ferramentas superior, que levará você à página.

    ![Janela do Team Explorer mostrando o Azure Repos, o GitHub e a clonagem de um repositório](media/team-explorer.png)

1. Em **Repositórios Git Locais**, selecione o comando **Clonar**, insira `https://github.com/gregmalcolm/python_koans` no campo de URL, insira uma pasta para os arquivos clonados e selecione o botão **Clonar**.

    > [!Tip]
    > A pasta que você especifica em **Team Explorer** é a pasta exata para receber os arquivos clonados. Ao contrário do comando `git clone`, a criação de um clone no **Team Explorer** não cria automaticamente uma subpasta com o nome do repositório.

1. Após a conclusão da clonagem, o repositório será exibido na lista **Repositórios Git Locais**. Clique duas vezes em que nome para navegar até o dashboard do repositório no **Team Explorer**.

1. Em **Soluções**, selecione **Novo**.

    ![Janela do Team Explorer, criando um novo projeto com base em um clone](media/team-explorer-new-project.png)

1. Na caixa de diálogo **novo projeto** que aparece, navegue até a linguagem **Python** (ou pesquise "Python"), selecione um **código Python existente**, especifique um nome para o projeto, defina **local** para a mesma pasta que o repositório e selecione **OK**. No assistente que é exibido, selecione **Concluir**.

1. Selecione **Exibir**  >  **Gerenciador de soluções** no menu.

1. No **Gerenciador de Soluções**, expanda o nó **python3**, clique com botão direito do mouse em **contemplate_koans.py** e selecione **Definir como Arquivo de Inicialização**. Esta etapa informa ao Visual Studio qual arquivo deve ser usado ao executar o projeto.

1. Selecione **projeto**  >  **koans Propriedades** no menu, selecione a guia **geral** e defina diretório de **trabalho** como "python3". Esta etapa é necessária porque, por padrão, o Visual Studio define o diretório de trabalho como a raiz do projeto em vez da localização do arquivo de inicialização (*python3\contemplate_koans.py*, que você também pode ver nas propriedades do projeto). O código do programa procurará um arquivo *koans.txt* na pasta de trabalho, portanto sem a alteração desse valor, você verá um erro de runtime.

    ![Configurar o diretório de trabalho para um projeto do Python](media/projects-set-working-directory.png)

1. Pressione **Ctrl** + **F5** ou selecione **depurar**  >  **Iniciar sem Depurar** para executar o programa. Se você encontrar um **FileNotFoundError** para *koans.txt*, verifique a configuração do diretório de trabalho conforme descrito na etapa anterior.

1. Quando o programa é executado com êxito, ele exibe um erro de asserção na linha 17 do *python3/koans/about_asserts.py*. Isso é intencional: o programa foi projetado para ensinar Python, fazendo com que você corrija todos os erros intencionais. (Mais detalhes são encontrados em [Ruby Koans](https://rubykoans.com/), que inspirou os Koans do Python).

    ![Primeira saída do programa koans do Python](media/koans-output.png)

1. Abra *python3/koans/about_asserts.py*, navegando até ele no **Gerenciador de Soluções** e clique duas vezes no arquivo. Observe que os números de linha não aparecem no editor por padrão. Para alterar isso, selecione **ferramentas**  >  **Opções**, selecione **Mostrar todas as configurações** na parte inferior da caixa de diálogo e, em seguida, navegue até **Editor de texto**  >  **Python**  >  **geral** e selecione **números de linha**:

    ![Ativando o número de linha para arquivos do Python](media/options-general-line-numbers.png)

1. Corrija o erro, alterando o argumento `False` na linha 17 para `True`. A linha deve ficar assim:

    ```python
    self.assertTrue(True) # This should be True
    ```

1. Execute o programa novamente. Se o Visual Studio alertar sobre erros, responder com **Sim** para continuar a execução do código. Você verá que a primeira verificação é bem-sucedida e o programa é interrompido no próximo koan. Continue corrigindo os erros e executando novamente o programa se quiser.

> [!Important]
> Neste Início Rápido, você criou um clone direto do repositório *python_koans* no GitHub. Esse tipo de repositório é protegido pelo autor contra alterações diretas, portanto, a tentativa de confirmar as alterações no repositório falhará. Na prática, os desenvolvedores criam fork desse tipo de repositório em suas próprias contas do GitHub, fazem as alterações ali mesmo e, em seguida, criam solicitações de pull para enviar essas alterações para o repositório original. Quando você tiver seu próprio fork, use a URL dele em vez da URL do repositório original usada anteriormente.

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Tutorial: trabalhar com Python no Visual Studio](tutorial-working-with-python-in-visual-studio-step-01-create-project.md)

## <a name="see-also"></a>Confira também

- [Identificar manualmente um interpretador Python existente](managing-python-environments-in-visual-studio.md#manually-identify-an-existing-environment)
- [Como instalar o suporte do Python no Visual Studio no Windows](installing-python-support-in-visual-studio.md)
- [Locais de instalação](installing-python-support-in-visual-studio.md#install-locations)
