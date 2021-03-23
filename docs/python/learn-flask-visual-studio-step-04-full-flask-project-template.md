---
title: Tutorial Aprenda a usar o Flask no Visual Studio, etapa 4, modelos de projeto Web
titleSuffix: ''
description: Um passo a passo das noções básicas do Flask no contexto dos projetos do Visual Studio, especificamente as funcionalidades fornecidas pelos modelos Projeto Web do Flask e Projeto Web do Flask/Jade.
ms.date: 01/07/2019
ms.topic: tutorial
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 7926a7983e43545ad47e8bc975f051821c108c18
ms.sourcegitcommit: f1dff6c4532c43b0444aa12ea57e90bb7dba6fba
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/23/2021
ms.locfileid: "104805998"
---
# <a name="step-4-use-the-full-flask-web-project-template"></a>Etapa 4: Usar o modelo Projeto Web do Flask completo

**Etapa anterior: [Fornecer arquivos estáticos, adicionar páginas e usar a herança do modelo](learn-flask-visual-studio-step-03-serve-static-files-add-pages.md)**

Agora que você explorou as noções básicas do Flask ao compilar um aplicativo com o modelo "Projeto de Aplicativo em Branco do Flask" no Visual Studio, é possível compreender facilmente o aplicativo mais completo produzido pelo modelo "Projeto Web do Flask".

Nesta etapa, agora você poderá:

> [!div class="checklist"]
> - Criar um aplicativo Web do Flask mais completo usando o modelo "Projeto Web do Flask" e examinar a estrutura do projeto (etapa 4-1)
> - Entender os modos de exibição e os modelos de página criados pelo modelo de projeto, que consistem em três páginas que são herdadas a partir de um modelo de página de base e que emprega bibliotecas JavaScript estáticas como jQuery e Bootstrap (etapa 4-2)
> - Entender o roteamento de URL fornecido pelo modelo (etapa 4-3)

Este artigo aplica-se também ao modelo "Projeto Web do Flask/Jade", que produz um aplicativo idêntico ao do "Projeto Web do Flask" usando o mecanismo de modelagem do Jade, em vez do Jinja. Detalhes adicionais são incluídos ao fim deste artigo.

## <a name="step-4-1-create-a-project-from-the-template"></a>Etapa 4-1: Criar um projeto com base no modelo

1. No Visual Studio, acesse **Gerenciador de soluções**, clique com o botão direito do mouse na solução **LearningFlask** criada anteriormente neste tutorial e selecione **Adicionar**  >  **novo projeto**. (Como alternativa, se você quiser usar uma nova solução, selecione **arquivo**  >  **Novo**  >  **Projeto** .)

1. Na caixa de diálogo novo projeto, procure e selecione o modelo de **projeto Web Flask** , chame o projeto "FlaskWeb" e selecione **OK**.

1. Como o modelo novamente inclui um arquivo *requirements.txt*, o Visual Studio solicita o local em que essas dependências serão instaladas. Escolha a opção **Instalar em um ambiente virtual** e, na caixa de diálogo **Adicionar Ambiente Virtual**, selecione **Criar** para aceitar os padrões.

1. Depois que o Visual Studio concluir a configuração do ambiente virtual, defina o projeto **FlaskWeb** como o padrão para a solução do Visual Studio clicando com o botão direito do mouse no projeto em **Gerenciador de soluções** e selecionando **definir como projeto de inicialização**. O projeto de inicialização, mostrado em negrito, é o que é executado quando você inicia o depurador.

    ![Gerenciador de Soluções mostrando o projeto FlaskWeb como o projeto de inicialização](media/flask/step04-second-project-in-solution-set-as-startup-project.png)

1. Selecione **depurar**  >  **Iniciar Depuração** (**F5**) ou use o botão **servidor Web** na barra de ferramentas para executar o servidor:

    ![Executar o botão da barra de ferramentas do servidor Web no Visual Studio](media/flask/run-web-server-toolbar-button.png)

1. O aplicativo criado pelo modelo tem três páginas, Página inicial, Sobre e Contato, que você navega usando a barra de navegação. Levar um minuto ou dois para examinar as diferentes partes do aplicativo. Para autenticar com o aplicativo por meio do comando **Login**, use as credenciais de superusuário criadas anteriormente.

    ![Exibição completa do navegador do aplicativo Projeto Web do Flask](media/flask/step04-full-app-desktop-view.png)

1. O aplicativo criado pelo modelo "Projeto Web do Flask" usa Bootstrap para layout responsivo que acomoda fatores de forma móveis. Para ver essa capacidade de resposta, redimensione o navegador para uma exibição específica para que o conteúdo seja renderizado verticalmente e a barra de navegação se transforme em um ícone de menu:

    ![Exibição (estreita) móvel do aplicativo Projeto Web do Flask](media/flask/step04-full-app-mobile-view.png)

1. Você pode deixar o aplicativo em execução para as seções a seguir.

    Caso deseje interromper o aplicativo e [confirmar as alterações no controle do código-fonte](learn-flask-visual-studio-step-02-create-app.md#commit-to-source-control), primeiro abra a página **Alterações** no **Team Explorer**, clique com o botão direito do mouse na pasta do ambiente virtual (provavelmente **env**) e selecione **Ignorar estes itens locais**.

### <a name="examine-what-the-template-creates"></a>Examine o que o modelo cria

O modelo "Projeto Web do Flask" cria a estrutura abaixo. O conteúdo é muito semelhante ao que você criou nas etapas anteriores. A diferença é que o modelo "Projeto Web do Flask" contém mais estrutura na pasta *static*, porque ela inclui jQuery e Bootstrap para obter um design responsivo. O modelo também adiciona uma página Contato. Em geral, se você seguiu as etapas anteriores deste tutorial, você já deve conhecer tudo com base no modelo.

- Arquivos na raiz do projeto:
  - *runserver.py*, um script para executar o aplicativo em um servidor de desenvolvimento.
  - *requirements.txt* contendo uma dependência do Flask 0.x.
- A pasta *FlaskWeb* contém todos os arquivos de aplicativo:
  - init.py marca o código do aplicativo como um módulo python, cria o objeto Flask e importa as exibições do aplicativo. *\_ \_ \_ \_*
  - *views.py* contém o código para renderizar páginas.
  - A pasta *static* contém subpastas chamadas *content* (arquivos CSS), *fonts* (arquivos de fonte) e *scripts* (arquivos JavaScript).
  - A pasta *templates* contém um modelo base *layout.html* juntamente com *about.html*, *contact.html* e *index.html*, para páginas específicas que estendem *layout.html*.

### <a name="question-is-it-possible-to-share-a-virtual-environment-between-visual-studio-projects"></a>Pergunta: É possível compartilhar um ambiente virtual entre projetos do Visual Studio?

Resposta: Sim, mas faça isso sabendo que diferentes projetos provavelmente usam pacotes diferentes ao longo do tempo e, portanto, um ambiente virtual compartilhado deve conter todos os pacotes para todos os projetos que o usam.

No entanto, para usar um ambiente virtual existente, faça o seguinte:

1. Quando for solicitado a instalar dependências no Visual Studio, selecione a opção **Eu os instalarei por conta própria** opção.
1. No **Gerenciador de Soluções**, clique com o botão direito do mouse no nó **Ambientes do Python** e escolha **Adicionar Ambiente Virtual Existente**.
1. Navegue até e selecione a pasta que contém o ambiente virtual e selecione **OK**.

## <a name="step-4-2-understand-the-views-and-page-templates-created-by-the-project-template"></a>Etapa 4-2: Entender os modos de exibição e os modelos de página criados pelo modelo de projeto

Quando você executa o projeto, observe que o aplicativo contém três modos de exibição: Página inicial, Sobre e Contato. O código dessas exibições é encontrado na pasta *FlaskWeb/views.py*. Cada função de exibição simplesmente chama `flask.render_template` com o caminho para um modelo e uma lista de variáveis de argumentos para os valores darem ao modelo. Por exemplo, a página Sobre é tratada pela função `about` (cujo decorador fornece o roteamento de URL):

```python
@app.route('/about')
def about():
    """Renders the about page."""
    return render_template(
        'about.html',
        title='About',
        year=datetime.now().year,
        message='Your application description page.'
    )
```

As funções `home` e `contact` são quase idênticas, com decoradores semelhantes e argumentos ligeiramente diferentes.

Os modelos estão localizados na pasta *templates* do aplicativo. O modelo base, *layout.html*, é o mais abrangente. Ele se refere a todos os arquivos estáticos necessários (JavaScript e CSS), define um bloco nomeado "conteúdo" que outras páginas substituem e fornece outro bloco chamado "scripts". Os seguintes trechos anotados de *layout.html* mostram essas áreas específicas:

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />

    <!-- Define a viewport for Bootstrap's responsive rendering -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{{ title }} - My Flask Application</title>

    <link rel="stylesheet" type="text/css" href="/static/content/bootstrap.min.css" />
    <link rel="stylesheet" type="text/css" href="/static/content/site.css" />
    <script src="/static/scripts/modernizr-2.6.2.js"></script>
</head>

<body>
    <!-- Navbar omitted -->

    <div class="container body-content">
        <!-- "content" block that pages are expected to override -->
        {% block content %}{% endblock %}
        <hr />
        <footer>
            <p>&copy; {{ year }} - My Flask Application</p>
        </footer>
    </div>

    <!-- Additional scripts; use the "scripts" block to add page-specific scripts.  -->
    <script src="/static/scripts/jquery-1.10.2.js"></script>
    <script src="/static/scripts/bootstrap.js"></script>
    <script src="/static/scripts/respond.js"></script>
    {% block scripts %}{% endblock %}

</body>
</html>
```

Cada um dos modelos de página individual, *about.html*, *contact.html* e *index.html*, estende o modelo base *layout.html*. *about.html* é o mais simples e mostra as marcações `{% extends %}` e `{% block content %}`:

```html
{% extends "app/layout.html" %}

{% block content %}

<h2>{{ title }}.</h2>
<h3>{{ message }}</h3>

<p>Use this area to provide additional information.</p>

{% endblock %}
```

*index.html* e *contact.html* usam a mesma estrutura e fornecem mais conteúdo no bloco "conteúdo".

## <a name="the-flaskjade-web-project-template"></a>O modelo Projeto Web do Flask/Jade

Conforme observado no início deste artigo, o Visual Studio fornece um modelo "Projeto Web do Flask/Jade", que cria um aplicativo visualmente idêntico ao produzido pelo "Projeto Web do Flask". A principal diferença é que ele usa o mecanismo de modelagem Jade, que é uma extensão do Jinja que implementa os mesmos conceitos com uma linguagem mais sucinta. Especificamente, o Jade usa palavras-chave em vez de marcas entre delimitadores {% %}, por exemplo, e permite que você se refira a elementos HTML e estilos CSS usando palavras-chave.

Para habilitar o Jade, o modelo de projeto inclui primeiro o pacote pyjade em *requirements.txt*.

O arquivo *\_ \_ init \_ \_ . py* do aplicativo contém uma linha para

```python
app.jinja_env.add_extension('pyjade.ext.jinja.PyJadeExtension')
```

Na pasta *templates*, são exibidos arquivos *.jade* em vez de modelos *.html*, e as exibições em *views.py* referenciam esses arquivos em suas chamadas a `flask.render_template`. Caso contrário, o código de modos de exibição é o mesmo.

Abrindo um dos arquivos *.jade*, você pode ver a expressão mais sucinta de um modelo. Por exemplo, este é o conteúdo de *templates/layout.jade*, conforme criado pelo modelo "Projeto Web do Flask/Jade":

```jade
doctype html
html
  head
    meta(charset='utf-8')
    meta(name='viewport', content='width=device-width, initial-scale=1.0')
    title #{title} - My Flask/Jade Application
    link(rel='stylesheet', type='text/css', href='/static/content/bootstrap.min.css')
    link(rel='stylesheet', type='text/css', href='/static/content/site.css')
    script(src='/static/scripts/modernizr-2.6.2.js')
  body
    .navbar.navbar-inverse.navbar-fixed-top
      .container
        .navbar-header
          button.navbar-toggle(type='button', data-toggle='collapse', data-target='.navbar-collapse')
            span.icon-bar
            span.icon-bar
            span.icon-bar
          a.navbar-brand(href='/') Application name
        .navbar-collapse.collapse
          ul.nav.navbar-nav
            li
              a(href='/') Home
            li
              a(href='/about') About
            li
              a(href='/contact') Contact
    .container.body-content
      block content
      hr
      footer
        p &copy; #{year} - My Flask/Jade Application

    script(src='/static/scripts/jquery-1.10.2.js')
    script(src='/static/scripts/bootstrap.js')
    script(src='/static/scripts/respond.js')

    block scripts
```

E este é o conteúdo de *templates/about.jade*, mostrando o uso de `#{ <name>}` para espaços reservados:

```jade
extends layout

block content
  h2 #{title}.
  h3 #{message}
  p Use this area to provide additional information.
```

Fique à vontade para fazer experimentos com sintaxes do Jinja e do Jade para ver qual funciona melhor para você.

## <a name="next-steps"></a>Próximas etapas

::: moniker range="vs-2017"
- [O modelo Pesquisa Projeto Web de Flask](learn-flask-visual-studio-step-05-polls-flask-web-project-template.md)
::: moniker-end

::: moniker range=">=vs-2019"
> [!Note]
> Se você tiver confirmando sua solução do Visual Studio para controle de origem ao longo deste tutorial, agora será um bom momento para fazer outra confirmação. Sua solução deve corresponder ao código-fonte do tutorial no GitHub: [Microsoft/python-sample-vs-learning-flask](https://github.com/Microsoft/python-sample-vs-learning-flask).

Agora você explorou a totalidade dos modelos "Projeto Web em Branco do Flask", "Projeto Web do Flask[/Jade]" e "Pesquisa Projeto Web de Flask[/Jade]" no Visual Studio. Você conheceu todas as noções básicas do Flask, como usar modos de exibição, modelos e roteamento, e viu como usar armazenamentos de dados de backup. Agora você poderá começar a usar um aplicativo Web por sua conta com os modos de exibição e modelos de que precisar.

A execução de um aplicativo Web no computador de desenvolvimento é apenas uma etapa para disponibilizar o aplicativo para seus clientes. As próximas etapas podem incluir as seguintes tarefas:

- Implante o aplicativo Web em um servidor de produção, como o Serviço de Aplicativo do Azure. Confira [Publicar no Serviço de Aplicativo do Azure](publishing-python-web-applications-to-azure-from-visual-studio.md).

- Adicione uma implementação de repositório que usa outro armazenamento de dados em nível de produção como o PostgreSQL, o MySQL e o SQL Server (que podem ser hospedados no Azure). Também é possível usar o [SDK do Azure para Python](/azure/python/) para trabalhar com serviços de armazenamento do Azure como tabelas e blobs, bem como o Cosmos DB.

- Configure um pipeline de integração contínua/implantação contínua em um serviço como o Azure DevOps. Além de trabalhar com o controle do código-fonte (por meio do Azure Repos, do GitHub ou em outro local), você pode configurar um projeto do Azure DevOps para executar automaticamente os testes de unidade como um pré-requisito para o lançamento, bem como configurar o pipeline para implantação em um servidor de preparo para testes adicionais antes de implantar na produção. O Azure DevOps, além disso, integra-se às soluções de monitoramento, como o App Insights e fecha o ciclo de inteiro com ferramentas ágeis de planejamento. Saiba mais em [Criar um pipeline de CI/CD para Python com o projeto do Azure DevOps](/azure/devops-project/azure-devops-project-python?view=vsts&preserve-view=true) e também a [documentação geral do Azure DevOps](/azure/devops/?view=vsts&preserve-view=true).
::: moniker-end

## <a name="go-deeper"></a>Aprofunde-se um pouco mais

- [Como gravar seu primeiro aplicativo do Flask, parte 4 – Modos de exibição genéricos e de formulários](https://docs.djangoproject.com/en/2.0/intro/tutorial04/) (docs.djangoproject.com)
- [Jade no GitHub (documentação)](https://github.com/liuliqiang/pyjade) (github.com)
- Código-fonte do tutorial no GitHub: [Microsoft/python-sample-vs-learning-flask](https://github.com/Microsoft/python-sample-vs-learning-flask)
