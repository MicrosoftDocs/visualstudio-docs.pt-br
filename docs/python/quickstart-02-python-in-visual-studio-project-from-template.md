---
title: Início Rápido – Criar um projeto do Python usando em modelo
description: Neste início rápido, crie um projeto do Visual Studio para Python usando um modelo interno para compilar um aplicativo básico em Flask.
ms.date: 09/04/2018
ms.prod: visual-studio-dev15
ms.technology: vs-python
ms.topic: quickstart
author: kraigb
ms.author: kraigb
manager: douge
ms.workload:
- python
- data-science
ms.openlocfilehash: b9f361ba73f8fd1d3963ca39a90ac01ba9effe6f
ms.sourcegitcommit: 9ea4b62163ad6be556e088da1e2a355f31366f39
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43995996"
---
# <a name="quickstart-create-a-python-project-from-a-template-in-visual-studio"></a>Início Rápido: criar um projeto do Python com base em um modelo no Visual Studio

Depois de [instalar o suporte ao Python no Visual Studio 2017](installing-python-support-in-visual-studio.md), é fácil criar um novo projeto do Python usando uma variedade de modelos. Neste Início Rápido, crie um aplicativo simples em Flask usando um modelo. O projeto resultante é semelhante ao projeto que você cria manualmente em [Início Rápido: criar um aplicativo Web com o Flask](../ide/quickstart-python.md).

1. Inicie o Visual Studio 2017.

1. Na barra de menus superior, escolha **Arquivo** > **Novo** > **Projeto**. Em seguida, na caixa de diálogo **Novo Projeto**, pesquise por "flask em branco", selecione o modelo de **Projeto Web Flask em branco** na lista do meio, nomeie o projeto e selecione **OK**:

    ![Criar um novo projeto com o modelo de Projeto Web Flask em branco](media/quickstart-python-06-blank-flask-template.png)

1. O Visual Studio fará uma solicitação em uma caixa de diálogo com a mensagem **Este projeto requer pacotes externos.** Essa caixa de diálogo aparece porque o modelo inclui um arquivo *requirements.txt* que especifica uma dependência do Flask. O Visual Studio pode instalar os pacotes automaticamente e oferece a opção de instalá-los em um *ambiente virtual*. É recomendável usar um ambiente virtual na instalação em um ambiente global, portanto, selecione **Instalar em um ambiente virtual** para continuar.

    ![Instalar o Flask em um ambiente virtual](media/quickstart-python-07-install-into-virtual-environment.png)

1. O Visual Studio exibe a caixa de diálogo **Adicionar Ambiente Virtual**. Aceite o padrão e selecione **Criar**, depois aprove todas as solicitações de elevação.

    > [!Tip]
    > Quando você inicia um projeto, é altamente recomendável criar um ambiente virtual imediatamente, como a maioria dos modelos do Visual Studio solicita. Ambientes virtuais mantêm os requisitos exatos do projeto ao longo do tempo, conforme você adiciona e remove bibliotecas. É possível gerar facilmente um arquivo *requirements.txt*, que você usa para reinstalar essas dependências em outros computadores de desenvolvimento (como quando usar controle do código-fonte) e ao implantar o projeto em um servidor de produção. Para saber mais sobre ambientes virtuais e seus benefícios, veja [Usar ambientes virtuais](../python/selecting-a-python-environment-for-a-project.md#use-virtual-environments) e [Gerenciar os pacotes necessários com requirements.txt](../python/managing-required-packages-with-requirements-txt.md).

1. Depois que o Visual Studio criar esse ambiente, examine o **Gerenciador de Soluções** para ver se há um arquivo *app.py* junto com *requirements.txt*. Abra *app.py* para ver se o modelo forneceu um código como em [Início Rápido: criar um aplicativo Web com o Flask](../ide/quickstart-python.md), com algumas seções adicionadas. Todo o código mostrado abaixo é criado pelo modelo, portanto você não precisa colar nada no *app.py* por conta própria.

    O código começa com as importações necessárias:

    ```python
    from flask import Flask
    app = Flask(__name__)
    ```

    Em seguida está a linha seguinte que pode ser útil ao implantar um aplicativo em um host da Web:

    ```python
    wsgi_app = app.wsgi_app
    ```

    Depois, vem o decorador de rota em uma função simples que define uma exibição:

    ```python
    @app.route('/')
    def hello():
        """Renders a sample page."""
        return "Hello World!"
    ```

    Por fim, o código de inicialização abaixo permite que você defina o host e a porta por meio de variáveis de ambiente em vez de fazer o hard-coding deles. Esse código permite controlar facilmente a configuração nos computadores de desenvolvimento e produção sem alterar o código:

    ```python
    if __name__ == '__main__':
        import os
        HOST = os.environ.get('SERVER_HOST', 'localhost')
        try:
            PORT = int(os.environ.get('SERVER_PORT', '5555'))
        except ValueError:
            PORT = 5555
        app.run(HOST, PORT)
    ```

1. Selecione **Depurar** > **Iniciar Sem Depuração** para executar o aplicativo e abrir um navegador para `localhost:5555`.

**Pergunta: Quais outros modelos de Python o Visual Studio oferece?**

**Resposta**: Com a carga de trabalho de Python instalada, o Visual Studio fornece uma variedade de modelos de projeto, inclusive para as [estruturas da Web Flask, Bottle e Django](../python/python-web-application-project-templates.md), serviços de nuvem do Azure, diferentes cenários de aprendizado de máquina e até mesmo um modelo para criar um projeto a partir de uma estrutura de pasta existente que contenha um aplicativo do Python. Acesse-os por meio da caixa de diálogo **Arquivo** > **Novo** > **Projeto** selecionando o nó de linguagem **Python** e seus nós filhos.

O Visual Studio também fornece uma variedade de arquivos ou *modelos de item* para criar rapidamente uma classe do Python, um pacote do Python, um teste de unidade do Python, arquivos *web.config* e muito mais. Quando houver um projeto de Python aberto, acesse os modelos de item por meio do comando de menu **Projeto** > **Adicionar Novo Item**. Consulte a referência de [modelos de item](python-item-templates.md).

O uso de modelos pode economizar um tempo significativo ao iniciar um projeto ou criar um arquivo, além de ser uma ótima maneira de aprender sobre os diferentes tipos de aplicativo e estruturas de código. É útil levar reservar alguns minutos para criar projetos e itens a partir de vários modelos para se familiarizar com o que eles oferecem.

**Pergunta: Também é possível usar modelos do Cookiecutter?**

**Resposta**: Sim! De fato, o Visual Studio fornece integração direta com o Cookiecutter. Saiba mais sobre isso em [Início Rápido: criar um projeto a partir de um modelo do Cookiecutter](../python/quickstart-04-python-in-visual-studio-project-from-cookiecutter.md).

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Tutorial: trabalhar com Python no Visual Studio](tutorial-working-with-python-in-visual-studio-step-01-create-project.md)

## <a name="see-also"></a>Consulte também

- [Identificar manualmente um interpretador Python existente](managing-python-environments-in-visual-studio.md#manually-identify-an-existing-environment)
- [Instalar o suporte para Python no Visual Studio 2015 e anterior](installing-python-support-in-visual-studio.md)
- [Locais de instalação](installing-python-support-in-visual-studio.md#install-locations)
