---
title: Tutorial – Saiba mais sobre o Flask no Visual Studio, etapa 3
description: Uma explicação dos conceitos básicos do Flask no contexto de projetos do Visual Studio, demonstrando especificamente como fornecer arquivos estáticos, adicionar páginas ao aplicativo e usar a herança do modelo
ms.date: 09/04/2018
ms.prod: visual-studio-dev15
ms.technology: vs-python
ms.topic: tutorial
author: kraigb
ms.author: kraigb
manager: douge
ms.workload:
- python
- data-science
ms.openlocfilehash: 6cdc8e3658b02c7c4371181d6c0e5723d0a3537c
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2018
ms.locfileid: "43775750"
---
# <a name="step-3-serve-static-files-add-pages-and-use-template-inheritance"></a>Etapa 3: Fornecer arquivos estáticos, adicionar páginas e usar a herança do modelo

**Etapa anterior: [Criar um aplicativo do Flask com modos de exibição e modelos de página](learn-flask-visual-studio-step-02-create-app.md)**

Nas etapas anteriores deste tutorial, você aprendeu como criar um aplicativo mínimo do Flask com uma única página HTML autocontido. No entanto, aplicativos Web modernos geralmente são compostos por várias páginas e usam recursos compartilhados, como arquivos CSS e JavaScript, para fornecer comportamento e estilo consistentes.

Nesta etapa, você aprenderá a:

> [!div class="checklist"]
> - Usar modelos de item do Visual Studio para adicionar rapidamente novos arquivos de diferentes tipos com código clichê conveniente (etapa 3-1)
> - Fornecer arquivos estáticos do código (etapa 3-2, opcional)
> - Adicionar mais páginas ao aplicativo (etapa 3-3)
> - Usar a herança do modelo para criar um cabeçalho e uma barra de navegação usados nas páginas (etapa 3-4)

## <a name="step-3-1-become-familiar-with-item-templates"></a>Etapa 3-1: Familiarizar-se com os modelos de item

À medida que desenvolve um aplicativo do Flask, geralmente você adiciona vários outros arquivos Python, HTML, CSS e JavaScript. Para cada tipo de arquivo (bem como para outros arquivos, como *web.config*, que podem ser necessários para a implantação), o Visual Studio fornece [modelos de item](python-item-templates.md) convenientes para você começar.

Para ver os modelos disponíveis, vá para **Gerenciador de Soluções**, clique com o botão direito do mouse na pasta em que você deseja criar o item, selecione **Adicionar** > **Novo Item**:

![Caixa de diálogo Adicionar Novo Item no Visual Studio](media/flask/step03-add-new-item-dialog.png)

Para usar um modelo, selecione o modelo desejado, especifique um nome para o arquivo e selecione **OK**. A adição de um item dessa maneira adiciona automaticamente o arquivo ao projeto do Visual Studio e marca as alterações para controle do código-fonte.

### <a name="question-how-does-visual-studio-know-which-item-templates-to-offer"></a>Pergunta: Como o Visual Studio sabe quais modelos de item oferecer?

Resposta: O arquivo de projeto do Visual Studio (*.pyproj*) contém um identificador de tipo de projeto que o marca como um projeto do Python. O Visual Studio usa esse identificador de tipo para mostrar apenas os modelos de item adequados para o tipo de projeto. Dessa forma, o Visual Studio pode fornecer um conjunto avançado de modelos de item para muitos tipos de projeto sem solicitar que você os classifique toda vez.

## <a name="step-3-2-serve-static-files-from-your-app"></a>Etapa 3-2: Fornecer arquivos estáticos do seu aplicativo

Em um aplicativo Web criado com Python (usando qualquer estrutura), seus arquivos em Python sempre são executados no servidor do host da Web e nunca são transmitidos para o computador de um usuário. Mas outros arquivos, como CSS e JavaScript, são usados exclusivamente pelo navegador, de modo que o servidor do host simplesmente os entrega como estão sempre que são solicitados. Esses arquivos são chamados de "estáticos", e o Flask pode fornecê-los automaticamente sem que você precise escrever código. Dentro de arquivos HTML, por exemplo, é possível referenciar arquivos estáticos usando um caminho relativo no projeto. A primeira seção desta etapa adiciona um arquivo CSS ao modelo de página existente.

Quando você precisar entregar um arquivo estático do código, como por meio de uma implementação de ponto de extremidade de API, o Flask fornecerá um método conveniente que permite a você referenciar arquivos usando caminhos relativos dentro de uma pasta chamada *static* (na raiz do projeto). A segunda seção desta etapa demonstra esse método usando um arquivo de dados estático simples.

Em qualquer caso, você pode organizar os arquivos em *static* como desejar.

### <a name="use-a-static-file-in-a-template"></a>Usar um arquivo estático em um modelo

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse na pasta **HelloFlask** no projeto do Visual Studio, selecione **Adicionar** > **Nova pasta** e nomeie a pasta `static`.

1. Clique com o botão direito do mouse na pasta **static** e selecione **Adicionar** > **Novo item**. Na caixa de diálogo exibida, selecione o modelo **Folha de estilos**, nomeie o arquivo `site.css` e selecione **OK**. O arquivo **site.css** é exibido no projeto e aberto no editor. A estrutura de pastas deve ser semelhante à imagem a seguir:

    ![Estrutura de arquivos estáticos, conforme mostrado no Gerenciador de Soluções](media/flask/step03-static-file-structure.png)

1. Substitua o conteúdo de *site.css* pelo seguinte código e salve o arquivo:

    ```css
    .message {
        font-weight: 600;
        color: blue;
    }
    ```

1. Substitua o conteúdo do arquivo *templates/index.html* do aplicativo pelo código a seguir, que substitui o elemento `<strong>` usado na etapa 2 por um `<span>` que referencia a classe de estilo `message`. O uso de uma classe de estilo dessa maneira oferece muito mais flexibilidade ao estilo do elemento.

    ```html
    <html>
        <head>
            <title>{{ title }}</title>
            <link rel="stylesheet" type="text/css" href="/static/site.css" />
        </head>
        <body>
            <span class="message">{{ message }}</span>{{ content }}
        </body>
    </html>
    ```

1. Execute o projeto para observar os resultados. Interrompa o aplicativo quando terminar e confirme as alterações no controle do código-fonte se desejar (conforme explicado na [etapa 2](learn-flask-visual-studio-step-02-create-app.md#commit-to-source-control)).

### <a name="serve-a-static-file-from-code"></a>Fornecer um arquivo estático do código

O Flask fornece uma função chamada `serve_static_file` que você pode chamar por meio do código para referenciar qualquer arquivo dentro da pasta *static* do projeto. O processo a seguir cria um ponto de extremidade de API simples que retorna um arquivo de dados estáticos.

1. Se você ainda não fez isto, crie uma pasta *static*: no **Gerenciador de Soluções**, clique com o botão direito do mouse na pasta **HelloFlask** no projeto do Visual Studio, selecione **Adicionar** > **Nova pasta** e nomeie a pasta `static`.

1. Na pasta *static*, crie um arquivo de dados JSON estático chamado *data.json* com o seguinte conteúdo (dados de exemplo sem sentido):

    ```json
    {
        "01": {
            "note" : "Data is very simple because we're demonstrating only the mechanism."
        }
    }
    ```

1. Em *views.py*, adicione uma função com a rota /api/data que retorna o arquivo de dados estático usando o método `send_static_file`:

    ```python
    @app.route('/api/data')
    def get_data():
      return app.send_static_file('data.json')
    ```

1. Execute o aplicativo e navegue até o ponto de extremidade /api/data para ver se o arquivo estático será retornado. Interrompa o aplicativo ao terminar.

### <a name="question-are-there-any-conventions-for-organizing-static-files"></a>Pergunta: Há convenções para organizar arquivos estáticos?

Resposta: Você pode adicionar outros arquivos CSS, JavaScript e HTML à sua pasta *static* como quiser. Uma maneira comum de organizar arquivos estáticos é criar subpastas chamadas *fonts*, *scripts* e *content* (para folhas de estilo e outros arquivos).

### <a name="question-how-do-i-handle-url-variables-and-query-parameters-in-an-api"></a>Pergunta: Como fazer para manipular variáveis de URL e parâmetros de consulta em uma API?

Resposta: Confira a resposta na etapa 1-4 para a [Pergunta: Como o Flask trabalha com rotas de URL de variável e parâmetros de consulta?](learn-flask-visual-studio-step-01-project-solution.md#qa-url-variables)

## <a name="step-3-3-add-a-page-to-the-app"></a>Etapa 3-3: Adicionar uma página ao aplicativo

A adição de outra página ao aplicativo significa o seguinte:

- Adicione uma função em Python que defina o modo de exibição.
- Adicione um modelo para a marcação da página.
- Adicione o roteamento necessário ao arquivo *urls.py* do projeto do Flask.

As etapas a seguir adicionam uma página "Sobre" ao projeto "HelloFlask" e links para essa página na home page:

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse na pasta **templates**, selecione **Adicionar** > **Novo item**, selecione o modelo de item **Página HTML**, nomeie o arquivo `about.html` e selecione **OK**.

    > [!Tip]
    > Se o comando **Novo Item** não for exibido no menu **Adicionar**, verifique se você interrompeu o aplicativo para que o Visual Studio saia do modo de depuração.

1. Substitua o conteúdo de *about.html* pela seguinte marcação (substitua o link explícito para a home page por uma barra de navegação simples na etapa 3-4):

    ```html
    <html>
        <head>
            <title>{{ title }}</title>
            <link rel="stylesheet" type="text/css" href="/static/site.css" />
        </head>
        <body>
            <div><a href="home">Home</a></div>
            {{ content }}
        </body>
    </html>
    ```

1. Abra o arquivo *views.py* do aplicativo e adicione uma função chamada `about` que usa o modelo:

    ```python
    @app.route('/about')
    def about():
        return render_template(
            "about.html",
            title = "About HelloFlask",
            content = "Example app page for Flask.")
    ```

1. Abra o arquivo *templates/index.html* e adicione a seguinte linha imediatamente dentro do elemento `<body>` para criar um link para a página About (novamente, substitua esse link por uma barra de navegação na etapa 3-4):

    ```html
    <div><a href="about">About</a></div>
    ```

1. Salve todos os arquivos usando o comando de menu **Arquivo** > **Salvar Tudo** ou apenas pressione **Ctrl**+**Shift**+**S**. (Tecnicamente, essa etapa não é necessária, pois a execução do projeto no Visual Studio salva os arquivos automaticamente. No entanto, é bom conhecer esse comando).

1. Execute o projeto para observar os resultados e verificar a navegação entre as páginas. Interrompa o aplicativo quando terminar.

### <a name="question-does-the-name-of-a-page-function-matter-to-flask"></a>Pergunta: o nome de uma função de página é importante para o Flask?

Resposta: não, porque ele é o decorador `@app.route` que determina as URLs para as quais o Flask chama a função para gerar uma resposta. Normalmente, os desenvolvedores correspondem o nome da função à rota, mas essa correspondência não é obrigatória.

## <a name="step-3-4-use-template-inheritance-to-create-a-header-and-nav-bar"></a>Etapa 3-4: Usar a herança do modelo para criar um cabeçalho e uma barra de navegação

Em vez de ter links de navegação explícitos em cada página, os aplicativos Web modernos normalmente usam um cabeçalho de marca e uma barra de navegação que fornece os links de página mais importantes, menus pop-up e assim por diante. Para garantir que o cabeçalho e a barra de navegação sejam os mesmos em todas as páginas, não repita o mesmo código em todos os modelos de página. Em vez disso, defina as partes comuns de todas as páginas em um único local.

O sistema de modelos do Flask (Jinja por padrão) fornece dois meios para reutilização de elementos específicos em vários modelos: inclui e herança.

- *Includes* corresponde a outros modelos de página que você insere em um local específico no modelo de referência usando a sintaxe `{% include <template_path> %}`. Você também pode usar uma variável se quiser alterar o caminho dinamicamente no código. Os elementos Inclui normalmente são usados no corpo de uma página para extrair o modelo compartilhado em um local específico na página.

- *Inheritance* usa o `{% extends <template_path> %}` no início de um modelo de página para especificar um modelo de base compartilhado no qual o modelo de referência se baseará. O elemento Herança costuma ser usado para definir um layout compartilhado, uma barra de navegação e outras estruturas para as páginas de um aplicativo, de modo que os modelos de referência tem apenas adicionar ou modificar áreas específicas do modelo de base chamadas *blocks*.

Em ambos os casos, `<template_path>` é relativo à pasta *templates* do aplicativo (`../` ou `./` também é permitido).

Um modelo de base delineia *blocos* usando as marcações `{% block <block_name> %}` e `{% endblock %}`. Se um modelo de referência usar marcações com o mesmo nome de bloco, o conteúdo do bloco substituirá o do modelo de base.

As etapas a seguir demonstram a herança:

1. Na pasta *templates* do aplicativo, crie um arquivo HTML (usando o menu de contexto **Adicionar** > **Novo item** ou **Adicionar** > **Página HTML**) chamado *layout.html* e substitua o conteúdo pela marcação abaixo. Veja que esse modelo contém um bloco chamado "conteúdo", que representa tudo o que as páginas de referência precisam substituir:

    ```html
    <!DOCTYPE html>
    <html>
    <head>
        <meta charset="utf-8" />
        <title>{{ title }}</title>
        <link rel="stylesheet" type="text/css" href="/static/site.css" />
    </head>

    <body>
        <div class="navbar">
            <a href="/" class="navbar-brand">Hello Flask</a>
            <a href="{{ url_for('home') }}" class="navbar-item">Home</a>
            <a href="{{ url_for('about') }}" class="navbar-item">About</a>
        </div>

        <div class="body-content">
            {% block content %}
            {% endblock %}
            <hr/>
            <footer>
                <p>&copy; 2018</p>
            </footer>
        </div>
    </body>
    </html>
    ```

1. Adicione os seguintes estilos ao arquivo *static/site.css* do aplicativo (este passo a passo não está tentando demonstrar o design responsivo; esses estilos servem apenas para gerar um resultado interessante):

    ```css
    .navbar {
        background-color: lightslategray;
        font-size: 1em;
        font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
        color: white;
        padding: 8px 5px 8px 5px;
    }

    .navbar a {
        text-decoration: none;
        color: inherit;
    }

    .navbar-brand {
        font-size: 1.2em;
        font-weight: 600;
    }

    .navbar-item {
        font-variant: small-caps;
        margin-left: 30px;
    }

    .body-content {
        padding: 5px;
        font-family:'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }
    ```

1. Modifique *templates/index.html* para se referir ao modelo base e substituir o bloco de conteúdo. Veja que, usando a herança, esse modelo se torna simples:

    ```html
    {% extends "layout.html" %}
    {% block content %}
    <span class="message">{{ message }}</span>{{ content }}
    {% endblock %}
    ```

1. Modifique *templates/about.html* para se referir também ao modelo base e substituir o bloco de conteúdo:

    ```html
    {% extends "layout.html" %}
    {% block content %}
    {{ content }}
    {% endblock %}
    ```

1. Execute o servidor para observar os resultados. Feche o servidor ao terminar.

    ![Aplicativo em execução mostrando a barra de navegação](media/flask/step03-nav-bar.png)

1. Como você fez alterações significativas no aplicativo, é novamente um bom momento para [confirmar suas alterações no controle do código-fonte](learn-django-in-visual-studio-step-02-create-an-app.md#commit-to-source-control).

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Usar o modelo completo Projeto Web do Flask](learn-flask-visual-studio-step-04-full-flask-project-template.md)

## <a name="go-deeper"></a>Aprofunde-se um pouco mais

- [Implantar o aplicativo Web no Serviço de Aplicativo do Azure](publishing-python-web-applications-to-azure-from-visual-studio.md)
- Para ver mais funcionalidades de modelos Jinja, como o fluxo de controle, confira [Jinja Template Designer Documentation](http://jinja.pocoo.org/docs/2.10/templates) (Documentação de Designer de Modelo do Jinja) (jinja.pocoo.org)
- Para obter detalhes sobre o uso de `url_for`, confira [url_for](http://flask.pocoo.org/docs/1.0/api/?highlight=url_for#flask.url_for) na documentação do objeto do Aplicativo Flask (flask.pocoo.org)
- Código-fonte do tutorial no GitHub: [Microsoft/python-sample-vs-learning-flask](https://github.com/Microsoft/python-sample-vs-learning-flask)
