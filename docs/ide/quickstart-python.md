---
title: 'Início rápido: usar o Visual Studio para criar um aplicativo Web Python'
description: Neste início rápido, você usa o Visual Studio e a estrutura do Flask para criar um aplicativo Web simples em Python.
ms.date: 10/29/2018
ms.prod: visual-studio-dev15
ms.technology: vs-python
ms.topic: quickstart
author: kraigb
ms.author: kraigb
manager: douge
ms.workload:
- python
- data-science
ms.openlocfilehash: 025adc3a99e2c5aabe2588852885e537553ddce6
ms.sourcegitcommit: d462dd10746624ad139f1db04edd501e7737d51e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50219270"
---
# <a name="quickstart-create-your-first-python-web-app-using-visual-studio"></a>Início rápido: crie seu primeiro aplicativo Web Python usando o Visual Studio

Nesta introdução de 5 a 10 minutos do Visual Studio como um IDE do Python, você criará um aplicativo Web Python simples na estrutura Flask. Crie o projeto por meio de etapas simples para ajudarão a saber mais sobre os recursos básicos do Visual Studio.

Se você ainda não tiver instalado o Visual Studio, acesse [Downloads do Visual Studio](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) para instalá-lo gratuitamente. No instalador, selecione a carga de trabalho de **Desenvolvimento de Python**.

## <a name="create-the-project"></a>Criar o projeto

As seguintes etapas criam um projeto vazio que serve como um contêiner para o aplicativo:

1. Abra o Visual Studio 2017.

1. Na barra de menus superior, escolha **Arquivo > Novo > Projeto**.

1. Na caixa de diálogo **Novo Projeto**, digite "Projeto Web Python" no campo de pesquisa no canto superior direito, escolha **Projeto Web** na lista do meio, nomeie o projeto como "HelloPython" e escolha **Ok**.

    ![Caixa de diálogo Novo projeto com o projeto Web do Python selecionado](media/quickstart-python-00-web-project.png)

    Se os modelos de projeto Python não forem exibidos, cancele a caixa de diálogo **Novo Projeto** e, na barra de menus superior, escolha **Ferramentas > Obter Ferramentas e Recursos** para abrir o **Instalador do Visual Studio**. Escolha a carga de trabalho **Desenvolvimento de Python** e, em seguida, selecione **Modificar**.

    ![Carga de trabalho de desenvolvimento do Python no instalador do Visual Studio](../python/media/installation-python-workload.png)

1. O novo projeto será aberto no **Gerenciador de Soluções** no painel direito. O projeto está vazio neste momento porque ele não contém outros arquivos.

    ![Gerenciador de Soluções mostrando o projeto vazio recém-criado](media/quickstart-python-01-empty-project.png)

**Pergunta: Qual é a vantagem de criar um projeto no Visual Studio para um aplicativo de Python?**

**Resposta**: Os aplicativos Python costumam ser definidos usando somente arquivos e pastas, mas essa estrutura simples pode se tornar complexa conforme os aplicativos aumentam e talvez envolvem arquivos gerados automaticamente, JavaScript para aplicativos Web e assim por diante. Um projeto do Visual Studio ajuda a gerenciar essa complexidade. O projeto (um arquivo *.pyproj*) identifica todos os arquivos de origem e de conteúdo associados ao projeto, contém informações de build de cada arquivo, mantém as informações para a integração com sistemas de controle de código-fonte e ajuda a organizar o aplicativo em componentes lógicos.

**Pergunta: O que é a "solução" mostrada no Gerenciador de Soluções?**

**Resposta**: Uma solução do Visual Studio é um contêiner que ajuda você a gerenciar um ou mais projetos relacionados como um grupo e armazena configurações que não são específicas de um projeto. Os projetos em uma solução também podem fazer referência uns aos outros, para que a execução de um projeto (um aplicativo do Python) cria automaticamente um segundo projeto (como uma extensão de C++ usada no aplicativo do Python).

## <a name="install-the-flask-library"></a>Instalar a biblioteca Flask

Aplicativos Web em Python quase sempre usam uma das muitas bibliotecas Python disponíveis para lidar com detalhes de baixo nível como o roteamento de solicitações da Web e formatação de respostas. Para essa finalidade, o Visual Studio fornece uma variedade de modelos para aplicativos Web, e um deles você usará mais adiante neste Início Rápido.

Aqui, use as etapas a seguir para instalar a biblioteca Flask no "ambiente global" padrão que o Visual Studio usa para este projeto.

1. Expanda o nó **Ambiente do Python** no projeto para ver o ambiente padrão para o projeto.

    ![Gerenciador de soluções mostrando o ambiente padrão](media/quickstart-python-02-default-environment.png)

1. Clique com o botão direito do mouse no ambiente e selecione **Instalar pacote Python**. Esse comando abre a janela **Ambientes de Python** na guia Pacotes.

1. Insira “flask” no campo de pesquisa e selecione **pip install flask from PyPI**. Aceite os prompts de privilégios de administrador e observe o andamento na janela **Saída** janela no Visual Studio. (Um prompt para elevação é exibido quando a pasta de pacotes do ambiente global está localizada em uma área protegida como *C:\Arquivos de Programas*.)

    ![Instalar a biblioteca Flask](media/quickstart-python-03-install-package.png)

1. Uma vez instalada, a biblioteca aparece no ambiente em **Gerenciador de Soluções**, o que significa que você pode utilizá-la no código Python.

    ![Biblioteca Flask instalada](media/quickstart-python-04-package-installed.png)

> [!Note]
> Em vez de instalar as bibliotecas no ambiente global, os desenvolvedores geralmente criam um “ambiente virtual” no qual instalar bibliotecas para um projeto específico. Modelos do Visual Studio geralmente oferecem essa opção, conforme discutido em [Início Rápido: criar um projeto de Python usando um modelo](../python/quickstart-02-python-in-visual-studio-project-from-template.md).

**Pergunta: Onde posso saber mais sobre outros pacotes do Python disponíveis?**

**Resposta**: Acesse o [Índice de pacotes do Python](https://pypi.org/).

## <a name="add-a-code-file"></a>Adicionar um arquivo de código

Agora você está pronto para adicionar um pouco de código Python para implementar um aplicativo Web mínimo.

1. Clique com o botão direito do mouse no projeto no **Gerenciador de Soluções** e selecione **Adicionar > Novo Item**.

1. Na caixa de diálogo exibida, selecione **Arquivo Python vazio**, nomeie-o como *app.py* e selecione **Adicionar**. O Visual Studio abre o arquivo automaticamente em uma janela do editor.

1. Copie o código a seguir e cole-o em *app.py*:

    ```python
    from flask import Flask

    # Create an instance of the Flask class that is the WSGI application.
    # The first argument is the name of the application module or package,
    # typically __name__ when using a single module.
    app = Flask(__name__)

    # Flask route decorators map / and /hello to the hello function.
    # To add other resources, create functions that generate the page contents
    # and add decorators to define the appropriate resource locators for them.

    @app.route('/')
    @app.route('/hello')
    def hello():
        # Render the page
        return "Hello Python!"

    if __name__ == '__main__':
        # Run the app server on localhost:4449
        app.run('localhost', 4449)
    ```

1. Talvez você tenha percebido que a caixa de diálogo **Adicionar > Novo item** exibe muitos outros tipos de arquivos que você pode adicionar ao projeto do Python, incluindo uma classe do Python, um pacote do Python, um teste de unidade do Python, arquivos *web.config* e muito mais. Em geral, esses modelos de item, como são chamados, são uma ótima maneira de criar rapidamente arquivos com código clichê útil.

**Pergunta: Onde posso saber mais sobre o Flask?**

**Resposta**: Consulte a documentação do Flask, começando pelo [Início Rápido do Flask](http://flask.pocoo.org/docs/0.12/quickstart/#quickstart).

## <a name="run-the-application"></a>Executar o aplicativo

1. Clique com o botão direito do mouse em *app.py* no **Gerenciador de Soluções** e selecione **Definir como arquivo de inicialização**. Esse comando identifica o arquivo de código para iniciar em Python ao executar o aplicativo.

    ![Definir o arquivo de inicialização para um projeto no Gerenciador de Soluções](media/quickstart-python-05-set-as-startup-file.png)

2. Clique com o botão direito do mouse no projeto no **Gerenciador de Soluções** e selecione **Propriedades**. Selecione a guia **Depurar** e defina a propriedade **Número da porta** para `4449`. Essa etapa garante que o Visual Studio inicie um navegador com `localhost:4449` para corresponder aos argumentos `app.run` no código.

3. Selecione **Depurar > Iniciar sem depuração** (**Ctrl**+**F5**) para salvar as alterações nos arquivos e executar o aplicativo.

4. É exibida uma janela de comando com a mensagem “* Em execução em <https://localhost:4449/>”, e uma janela do navegador deverá ser aberta para `localhost:4449`, exibindo a mensagem “Olá, Python!” A solicitação GET também aparece na janela de comando com um status 200.

    Se um navegador não for aberto automaticamente, inicie o navegador de sua escolha e navegue até `localhost:4449`.

    Caso apareça somente o shell interativo do Python na janela de comando ou se essa janela piscar brevemente na tela, verifique se você definiu *app.py* como o arquivo de inicialização na etapa 1 acima.

5. Navegue até `localhost:4449/hello` para testar se o decorador do recurso `/hello` também funciona. Novamente, a solicitação GET aparece na janela de comando com um status 200. Fique à vontade para experimentar algumas outras URLs para ver se elas exibem os códigos de status 404 na janela de comando.

6. Feche a janela de comando para interromper o aplicativo e, em seguida, feche a janela do navegador.

**Pergunta: Qual é a diferença entre o comando Iniciar Sem Depuração e Iniciar Depuração?**

**Resposta**: Use **Iniciar Depuração** para executar o aplicativo no contexto do [depurador do Visual Studio](../python/debugging-python-in-visual-studio.md), o que permite que você defina pontos de interrupção, examine variáveis e depure seu código linha por linha. Os aplicativos podem ser executados mais lentamente no depurador devido aos vários ganchos que possibilitam a depuração. **Iniciar Sem Depuração**, por outro lado, executa o aplicativo diretamente, como se fosse executado na linha de comando, sem nenhum contexto de depuração, e também inicia automaticamente um navegador e navega para a URL especificada na guia  **Depurar** das propriedades do projeto.

## <a name="next-steps"></a>Próximas etapas

Parabéns por executar seu primeiro aplicativo do Python no Visual Studio. Você aprendeu um pouco sobre como usar o Visual Studio como um IDE do Python!

> [!div class="nextstepaction"]
> [Implantar o aplicativo no Serviço de Aplicativo do Azure](../python/publishing-python-web-applications-to-azure-from-visual-studio.md)

Como as etapas seguidas neste Início Rápido são razoavelmente genéricas, você provavelmente percebeu que elas podem e devem ser automatizadas. Essa automação é a função dos modelos de projeto do Visual Studio. Acompanhe o [Início Rápido – Criar um projeto Python usando um modelo](../python/quickstart-02-python-in-visual-studio-project-from-template.md) para obter uma demonstração que cria um aplicativo Web semelhante ao que você criou neste artigo, mas com menos etapas.

Para continuar com um tutorial mais completo sobre o Python no Visual Studio, incluindo o uso da janela interativa, da depuração, da visualização de dados e o trabalho com o Git, acompanhe o [Tutorial: Introdução ao Python no Visual Studio](../python/tutorial-working-with-python-in-visual-studio-step-01-create-project.md).

Para explorar mais do que o Visual Studio tem a oferecer, selecione os links abaixo.

- Saiba mais sobre os [Modelos de aplicativo Web Python no Visual Studio](../python/python-web-application-project-templates.md).
- Saiba mais sobre [Depuração de Python](../python/debugging-python-in-visual-studio.md)
- Saiba mais sobre o [IDE do Visual Studio](../ide/visual-studio-ide.md) de modo geral.
