---
title: Tutorial – Saiba mais sobre Django no Visual Studio, etapa 3
description: Uma explicação dos conceitos básicos do Django no contexto de projetos do Visual Studio, demonstrando especificamente como fornecer arquivos estáticos, adicionar páginas ao aplicativo e usar a herança do modelo
ms.date: 11/19/2018
ms.prod: visual-studio-dev15
ms.technology: vs-python
ms.topic: tutorial
author: kraigb
ms.author: kraigb
manager: douge
ms.workload:
- python
- data-science
ms.openlocfilehash: bea209e2d7cf751c66f3e627311a2985c79f55c3
ms.sourcegitcommit: f61ad0e8babec8810295f039e67629f4bdebeef0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/19/2018
ms.locfileid: "52001289"
---
# <a name="step-3-serve-static-files-add-pages-and-use-template-inheritance"></a>Etapa 3: Fornecer arquivos estáticos, adicionar páginas e usar a herança do modelo

**Etapa anterior: [Criar um aplicativo do Django com modos de exibição e modelos de página](learn-django-in-visual-studio-step-02-create-an-app.md)**

Nas etapas anteriores deste tutorial, você aprendeu como criar um aplicativo mínimo em Django com uma única página HTML autocontido. No entanto, aplicativos Web modernos geralmente são compostos por várias páginas e usam recursos compartilhados, como arquivos CSS e JavaScript, para fornecer comportamento e estilo consistentes.

Nesta etapa, você aprenderá a:

> [!div class="checklist"]
> - Usar modelos de item do Visual Studio para adicionar rapidamente novos arquivos de diferentes tipos com código clichê conveniente (etapa 3-1)
> - Configurar o projeto em Django para fornecer arquivos estáticos (etapa 3-2)
> - Adicionar mais páginas ao aplicativo (etapa 3-3)
> - Usar a herança do modelo para criar um cabeçalho e uma barra de navegação usados nas páginas (etapa 3-4)

## <a name="step-3-1-become-familiar-with-item-templates"></a>Etapa 3-1: Familiarizar-se com os modelos de item

À medida que desenvolve um aplicativo do Django, geralmente você adiciona vários outros arquivos Python, HTML, CSS e JavaScript. Para cada tipo de arquivo (bem como para outros arquivos, como *web.config*, que podem ser necessários para a implantação), o Visual Studio fornece [modelos de item](python-item-templates.md) convenientes para você começar.

Para ver os modelos disponíveis, vá para **Gerenciador de Soluções**, clique com o botão direito do mouse na pasta em que você deseja criar o item, selecione **Adicionar** > **Novo Item**:

![Caixa de diálogo Adicionar Novo Item no Visual Studio](media/django/step03-add-new-item-dialog.png)

Para usar um modelo, selecione o modelo desejado, especifique um nome para o arquivo e selecione **OK**. A adição de um item dessa maneira adiciona automaticamente o arquivo ao projeto do Visual Studio e marca as alterações para controle do código-fonte.

### <a name="question-how-does-visual-studio-know-which-item-templates-to-offer"></a>Pergunta: Como o Visual Studio sabe quais modelos de item oferecer?

Resposta: O arquivo de projeto do Visual Studio (*.pyproj*) contém um identificador de tipo de projeto que o marca como um projeto do Python. O Visual Studio usa esse identificador de tipo para mostrar apenas os modelos de item adequados para o tipo de projeto. Dessa forma, o Visual Studio pode fornecer um conjunto avançado de modelos de item para muitos tipos de projeto sem solicitar que você os classifique toda vez.

## <a name="step-3-2-serve-static-files-from-your-app"></a>Etapa 3-2: Fornecer arquivos estáticos do seu aplicativo

Em um aplicativo Web criado com Python (usando qualquer estrutura), seus arquivos em Python sempre são executados no servidor do host da Web e nunca são transmitidos para o computador de um usuário. Mas outros arquivos, como CSS e JavaScript, são usados exclusivamente pelo navegador, de modo que o servidor do host simplesmente os entrega como estão sempre que são solicitados. Esses arquivos são chamados de "estáticos", e o Django pode fornecê-los automaticamente sem que você precise escrever algum código.

Um projeto do Django é configurado por padrão para fornecer arquivos estáticos da pasta *static* do aplicativo, graças a estas linhas em *settings.py* do projeto do Django:

```python
# Static files (CSS, JavaScript, Images)
# https://docs.djangoproject.com/en/1.9/howto/static-files/

STATIC_URL = '/static/'

STATIC_ROOT = posixpath.join(*(BASE_DIR.split(os.path.sep) + ['static']))
```

Você pode organizar os arquivos usando qualquer estrutura de pastas desejada dentro de *static* e, em seguida, usar caminhos relativos dentro dessa pasta para referenciar os arquivos. Para demonstrar esse processo, as seguintes etapas adicionam um arquivo CSS ao aplicativo e, em seguida, usam essa folha de estilos no modelo *index.html*:

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse na pasta **HelloDjangoApp** do projeto do Visual Studio, selecione **Adicionar** > **Nova pasta** e nomeie a pasta `static`.

1. Clique com o botão direito do mouse na pasta **static** e selecione **Adicionar** > **Novo item**. Na caixa de diálogo exibida, selecione o modelo **Folha de estilos**, nomeie o arquivo `site.css` e selecione **OK**. O arquivo **site.css** é exibido no projeto e aberto no editor. A estrutura de pastas deve ser semelhante à imagem a seguir:

    ![Estrutura de arquivos estáticos, conforme mostrado no Gerenciador de Soluções](media/django/step03-static-file-structure.png)

1. Substitua o conteúdo de *site.css* pelo seguinte código e salve o arquivo:

    ```css
    .message {
        font-weight: 600;
        color: blue;
    }
    ```

1. Substitua o conteúdo do arquivo *templates/HelloDjangoApp/index.html* do aplicativo pelo código a seguir, que substitui o elemento `<strong>` usado na etapa 2 por um `<span>` que referencia a classe de estilo `message`. O uso de uma classe de estilo dessa maneira oferece muito mais flexibilidade ao estilo do elemento. (Se você ainda não moveu o *index.html* para uma subpasta nos *modelos* ao usar o VS 2017 15.7 e anteriores, veja [Namespacing de modelo](learn-django-in-visual-studio-step-02-create-an-app.md#template-namespacing) na etapa 2-4.)

    ```html
    <html>
        <head>
            <title>{{ title }}</title>
            {% load staticfiles %} <!-- Instruct Django to load static files -->
            <link rel="stylesheet" type="text/css" href="{% static 'site.css' %}" />
        </head>
        <body>
            <span class="message">{{ message }}</span>{{ content }}
        </body>
    </html>
    ```

1. Execute o projeto para observar os resultados. Pare o servidor quando terminar e confirme as alterações no controle do código-fonte se desejar (conforme explicado na [etapa 2](learn-django-in-visual-studio-step-02-create-an-app.md#commit-to-source-control)).

### <a name="question-what-is-the-purpose-of-the--load-staticfiles--tag"></a>Pergunta: Qual é a finalidade da marcação {% load staticfiles %}?

Resposta: A linha `{% load staticfiles %}` é necessária antes da referência a arquivos estáticos em elementos como `<head>` e `<body>`. No exemplo mostrado nesta seção, "staticfiles" se refere a um conjunto de marcações de modelo do Django personalizado que permite o uso da sintaxe `{% static %}` para se referir a arquivos estáticos.  Sem `{% load staticfiles %}`, você verá uma exceção quando o aplicativo for executado.

### <a name="question-are-there-any-conventions-for-organizing-static-files"></a>Pergunta: Há convenções para organizar arquivos estáticos?

Resposta: Você pode adicionar outros arquivos CSS, JavaScript e HTML à sua pasta *static* como quiser. Uma maneira comum de organizar arquivos estáticos é criar subpastas chamadas *fonts*, *scripts* e *content* (para folhas de estilo e outros arquivos). Em cada caso, lembre-se de incluir essas pastas no caminho relativo para o arquivo nas referências `{% static %}`.

## <a name="step-3-3-add-a-page-to-the-app"></a>Etapa 3-3: Adicionar uma página ao aplicativo

A adição de outra página ao aplicativo significa o seguinte:

- Adicione uma função em Python que defina o modo de exibição.
- Adicione um modelo para a marcação da página.
- Adicione o roteamento necessário ao arquivo *urls.py* do projeto do Django.

As etapas a seguir adicionam uma página "Sobre" ao projeto "HelloDjangoApp" e links para essa página na página inicial:

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse na pasta **templates/HelloDjangoApp**, selecione **Adicionar** > **Novo item**, selecione o modelo de item **Página HTML**, nomeie o arquivo `about.html` e selecione **OK**.

    > [!Tip]
    > Se o comando **Novo Item** não aparecer no menu **Adicionar**, verifique se que você interrompeu o servidor para que o Visual Studio saia do modo de depuração.

1. Substitua o conteúdo de *about.html* pela seguinte marcação (substitua o link explícito para a home page por uma barra de navegação simples na etapa 3-4):

    ```html
    <html>
        <head>
            <title>{{ title }}</title>
            {% load staticfiles %}
            <link rel="stylesheet" type="text/css" href="{% static 'site.css' %}" />
        </head>
        <body>
            <div><a href="home">Home</a></div>
            {{ content }}
        </body>
    </html>
    ```

1. Abra o arquivo *views.py* do aplicativo e adicione uma função chamada `about` que usa o modelo:

    ```python
    def about(request):
        return render(
            request,
            "HelloDjangoApp/about.html",
            {
                'title' : "About HelloDjangoApp",
                'content' : "Example app page for Django."
            }
        )
    ```

1. Abra o arquivo *urls.py* do projeto do Django e adicione a seguinte linha à matriz `urlPatterns`:

    ```python
    url(r'^about$', HelloDjangoApp.views.about, name='about'),
    ```

1. Abra o arquivo *templates/HelloDjangoApp/index.html* e adicione a seguinte linha abaixo do elemento `<body>` para criar um link para a página About (novamente, substitua esse link por uma barra de navegação na etapa 3-4):

    ```html
    <div><a href="about">About</a></div>
    ```

1. Salve todos os arquivos usando o comando de menu **Arquivo** > **Salvar Tudo** ou apenas pressione **Ctrl**+**Shift**+**S**. (Tecnicamente, essa etapa não é necessária, pois a execução do projeto no Visual Studio salva os arquivos automaticamente. No entanto, é bom conhecer esse comando).

1. Execute o projeto para observar os resultados e verificar a navegação entre as páginas. Feche o servidor ao terminar.

### <a name="question-i-tried-using-index-for-the-link-to-the-home-page-but-it-didnt-work-why"></a>Pergunta: Tentei usar "index" no link para a página inicial, mas não funcionou. Por quê?

Resposta: Embora a função de exibição em *views.py* seja nomeada `index`, os padrões de roteamento de URL no arquivo *urls.py* do projeto do Django não contêm uma expressão regular que corresponda à cadeia de caracteres "index". Para fazer a correspondência com essa cadeia de caracteres, você precisa adicionar outra entrada para o padrão `^index$`.

Como mostrado na próxima seção, é muito melhor usar a marcação `{% url '<pattern_name>' %}` no modelo de página para se referir ao *nome* de um padrão, caso em que o Django cria a URL adequada para você. Por exemplo, substitua `<div><a href="home">Home</a></div>` em *about.html* por `<div><a href="{% url 'index' %}">Home</a></div>`. O uso de 'index' funciona aqui porque o primeiro padrão de URL em *urls.py* é, na verdade, chamado de 'index' (em virtude do argumento `name='index'`). Você também pode usar "home" para se referir ao segundo padrão.

## <a name="step-3-4-use-template-inheritance-to-create-a-header-and-nav-bar"></a>Etapa 3-4: Usar a herança do modelo para criar um cabeçalho e uma barra de navegação

Em vez de ter links de navegação explícitos em cada página, os aplicativos Web modernos normalmente usam um cabeçalho de marca e uma barra de navegação que fornece os links de página mais importantes, menus pop-up e assim por diante. Para garantir que o cabeçalho e a barra de navegação sejam os mesmos em todas as páginas, não repita o mesmo código em todos os modelos de página. Em vez disso, defina as partes comuns de todas as páginas em um único local.

O sistema de modelos do Django fornece dois meios para reutilização de elementos específicos em vários modelos: includes e inheritance.

- *Includes* corresponde a outros modelos de página que você insere em um local específico no modelo de referência usando a sintaxe `{% include <template_path> %}`. Você também pode usar uma variável se quiser alterar o caminho dinamicamente no código. Os elementos Inclui normalmente são usados no corpo de uma página para extrair o modelo compartilhado em um local específico na página.

- *Inheritance* usa o `{% extends <template_path> %}` no início de um modelo de página para especificar um modelo de base compartilhado no qual o modelo de referência se baseará. O elemento Herança costuma ser usado para definir um layout compartilhado, uma barra de navegação e outras estruturas para as páginas de um aplicativo, de modo que os modelos de referência tem apenas adicionar ou modificar áreas específicas do modelo de base chamadas *blocks*.

Em ambos os casos, `<template_path>` é relativo à pasta *templates* do aplicativo (`../` ou `./` também é permitido).

Um modelo de base delineia blocos usando as marcas `{% block <block_name> %}` e `{% endblock %}`. Se um modelo de referência usar marcações com o mesmo nome de bloco, o conteúdo do bloco substituirá o do modelo de base.

As etapas a seguir demonstram a herança:

1. Na pasta *templates/HelloDjangoApp* do aplicativo, crie um arquivo HTML (usando o menu de contexto **Adicionar** > **Novo item** ou **Adicionar** > **Página HTML**) chamado *layout.html* e substitua seu conteúdo pela marcação abaixo. Veja que esse modelo contém um bloco chamado "conteúdo", que representa tudo o que as páginas de referência precisam substituir:

    ```html
    <!DOCTYPE html>
    <html>
    <head>
        <meta charset="utf-8" />
        <title>{{ title }}</title>
        {% load staticfiles %}
        <link rel="stylesheet" type="text/css" href="{% static 'site.css' %}" />
    </head>

    <body>
        <div class="navbar">
           <a href="/" class="navbar-brand">Hello Django</a>
           <a href="{% url 'home' %}" class="navbar-item">Home</a>
           <a href="{% url 'about' %}" class="navbar-item">About</a>
        </div>

        <div class="body-content">
    {% block content %}{% endblock %}
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

1. Modifique *templates/HelloDjangoApp/index.html* para se referir ao modelo base e substituir o bloco de conteúdo. Veja que, usando a herança, esse modelo se torna simples:

    ```html
    {% extends "HelloDjangoApp/layout.html" %}
    {% block content %}
    <span class="message">{{ message }}</span>{{ content }}
    {% endblock %}
    ```

1. Modifique *templates/HelloDjangoApp/about.html* para também se referir ao modelo base e substituir o bloco de conteúdo:

    ```html
    {% extends "HelloDjangoApp/layout.html" %}
    {% block content %}
    {{ content }}
    {% endblock %}
    ```

1. Execute o servidor para observar os resultados. Feche o servidor ao terminar.

    ![Aplicativo em execução mostrando a barra de navegação](media/django/step03-nav-bar.png)

1. Como você fez alterações significativas no aplicativo, é novamente um bom momento para [confirmar suas alterações no controle do código-fonte](learn-django-in-visual-studio-step-02-create-an-app.md#commit-to-source-control).

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Usar o modelo Projeto Web Django completo](learn-django-in-visual-studio-step-04-full-django-project-template.md)

## <a name="go-deeper"></a>Aprofunde-se um pouco mais

- [Implantar o aplicativo Web no Serviço de Aplicativo do Azure](publishing-python-web-applications-to-azure-from-visual-studio.md)
- [Como gravar seu primeiro aplicativo do Django, parte 3 (modos de exibição)](https://docs.djangoproject.com/en/2.0/intro/tutorial03/) (docs.djangoproject.com)
- Para conhecer mais recursos de modelos do Django, como o fluxo de controle, confira [A linguagem de modelos do Django](https://docs.djangoproject.com/en/2.0/ref/templates/language/) (docs.djangoproject.com)
- Para obter detalhes completos sobre como usar a marcação `{% url %}`, confira [url](https://docs.djangoproject.com/en/2.0/ref/templates/builtins/#url) dentro de [Referência de marcações de modelo internas e filtros para modelos do Django](https://docs.djangoproject.com/en/2.0/ref/templates/builtins/) (docs.djangoproject.com)
- Código-fonte do tutorial no GitHub: [Microsoft/python-sample-vs-learning-django](https://github.com/Microsoft/python-sample-vs-learning-django)
