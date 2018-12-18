---
title: Tutorial – Saiba mais sobre o Flask no Visual Studio, etapa 5
description: Um passo a passo das noções básicas do Flask no contexto dos projetos do Visual Studio, especificamente as funcionalidades dos modelos de Pesquisas do Projeto Web do Flask e Pesquisas do Projeto Web do Flask/Jade.
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
ms.openlocfilehash: bf6c9299f994ba1f5272c68724171fb42e85a679
ms.sourcegitcommit: 1abb9cf4c3ccb90e3481ea8079272c98aad12875
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50143197"
---
# <a name="step-5-use-the-polls-flask-web-project-template"></a>Etapa 5 – Usar o modelo Projeto Web do Flask de pesquisas

**Etapa anterior: [Usar o modelo Projeto Web completo do Flask](learn-flask-visual-studio-step-04-full-flask-project-template.md)**

Depois de entender o modelo "Projeto Web do Flask" do Visual Studio, agora será possível examinar o terceiro modelo do Flask, "Pesquisas do Projeto Web do Flask", criado sobre a mesma base de código.

Nesta etapa, você aprenderá a:

> [!div class="checklist"]
> - Criar um projeto com base no modelo e inicializar o banco de dados (etapa 5-1)
> - Compreender os modelos de dados (etapa 5-2)
> - Compreender os armazenamentos de dados de backup (etapa 5-3)
> - Compreender os detalhes da votação e as visualizações dos resultados (etapa 5-4)

O Visual Studio também fornece o modelo "Projeto Web de Votações do Flask/Jade", que produz um aplicativo idêntico, mas usa a extensão do Jade para o mecanismo de modelagem do Jinja. Para obter detalhes, confira [Etapa 4 – Modelo Projeto Web do Flask/Jade](learn-flask-visual-studio-step-04-full-flask-project-template.md#the-flaskjade-web-project-template).

## <a name="step-5-1-create-the-project"></a>Etapa 5-1: Criar o projeto

1. No Visual Studio, acesse **Gerenciador de Soluções**, clique com o botão direito do mouse na solução **LearningFlask** criada anteriormente neste tutorial e selecione **Adicionar** > **Novo Projeto**. (Como alternativa, se você quiser usar uma nova solução, selecione **Arquivo** > **Novo** > **Projeto**).

1. Na caixa de diálogo Novo Projeto, pesquise e selecione o modelo **Projeto Web de Votações do Flask**, nomeie o projeto "FlaskPolls" e selecione **OK**.

1. Como os outros modelos de projeto do Visual Studio, o modelo de "Projeto Web de Votações do Flask" inclui um arquivo *requirements.txt*. O Visual Studio solicita o local em que essas dependências serão instaladas. Escolha a opção **Instalar em um ambiente virtual** e, na caixa de diálogo **Adicionar Ambiente Virtual**, selecione **Criar** para aceitar os padrões. (Esse modelo requer o Flask, bem como os pacotes azure-storage e pymongo; o "Pesquisas do Projeto Web do Flask/Jade" também requerem pyjade.)

1. Defina o projeto **FlaskPolls** para ser o padrão para a solução do Visual Studio clicando com o botão direito do mouse no projeto em **Gerenciador de Soluções** e selecionando **Definir como Projeto de Inicialização**. O projeto de inicialização, mostrado em negrito, é o que é executado quando você inicia o depurador.

1. Selecione **Depurar** > **Iniciar Depuração** (**F5**) ou use o botão **Servidor Web** na barra de ferramentas para executar o servidor:

    ![Executar o botão da barra de ferramentas do servidor Web no Visual Studio](media/django/run-web-server-toolbar-button.png)

1. O aplicativo criado pelo modelo tem três páginas, Página inicial, Sobre e Contato, que você navega usando a barra de navegação superior. Leve alguns minutos para examinar as diferentes partes do aplicativo (as páginas Sobre e Contato são muito semelhantes ao "Projeto Web do Flask" e não serão mais discutidas).

    ![Exibição completa do aplicativo Pesquisas do Projeto Web do Flask](media/flask/step06-full-app-view.png)

1. Na home page, o botão **Criar Votações de Exemplo** inicializa o armazenamento de dados do aplicativo com três votações diferentes descritas na página *models/samples.json*. Por padrão, o aplicativo usa um banco de dados na memória (conforme mostrado na página Sobre), que é redefinido cada vez que o aplicativo é reiniciado. O aplicativo também contém código para trabalhar com o Armazenamento do Azure e com o MongoDB, conforme será ainda descrito neste artigo.

1. Depois que você tiver inicializado o armazenamento de dados, poderá votar nas diferentes votações conforme mostrado na home page (a barra de navegação e o rodapé são omitidos para fins de brevidade):

    ![Exibição do aplicativo Votações depois que o armazenamento de dados é inicializado](media/flask/step06-polls-initialized.png)

1. Selecionar uma votação exibe opções específicas:

    ![Interface para votar em uma votação](media/flask/step06-polls-voting-interface.png)

1. Depois de votar, o aplicativo mostrará uma página de resultados e permitirá que você vote novamente:

    ![Visualização dos resultados após a votação](media/flask/step06-polls-results.png)

1. Você pode deixar o aplicativo em execução para as seções a seguir.

    Caso deseje interromper o aplicativo e [confirmar as alterações no controle do código-fonte](learn-flask-visual-studio-step-02-create-app.md#commit-to-source-control), primeiro abra a página **Alterações** no **Team Explorer**, clique com o botão direito do mouse na pasta do ambiente virtual (provavelmente **env**) e selecione **Ignorar estes itens locais**.

### <a name="examine-the-project-contents"></a>Examine o conteúdo do projeto

Conforme observado anteriormente, quase tudo o que está em um projeto criado com base no modelo "Pesquisas do Projeto Web do Flask" (e o modelo do "Pesquisas do Projeto Web do Flask/Jade) deverá ser conhecido se você tiver explorado os outros modelos de projeto no Visual Studio. As etapas adicionais neste artigo resumem as mais alterações e adições mais significativas, ou seja, modelos de dados e modos de exibição adicionais.

## <a name="step-5-2-understand-the-data-models"></a>Etapa 5-2: Compreender os modelos de dados

Os modelos de dados do aplicativo são classes do Python nomeadas Votação e Opção, definidas em *models/\_\_init\_\_.py*. Uma Votação representa uma pergunta, para a qual uma coleção de instâncias de Opção representam as respostas disponíveis. Uma Votação também mantém o número total de votos (para qualquer opção) e um método para calcular as estatísticas usadas para gerar exibições:

```python
class Poll(object):
    """A poll object for use in the application views and repository."""
    def __init__(self, key=u'', text=u''):
        """Initializes the poll."""
        self.key = key
        self.text = text
        self.choices = []
        self.total_votes = None

    def calculate_stats(self):
        """Calculates some statistics for use in the application views."""
        total = 0
        for choice in self.choices:
            total += choice.votes
        for choice in self.choices:
            choice.votes_percentage = choice.votes / float(total) * 100 \
                if total > 0 else 0
        self.total_votes = total

class Choice(object):
    """A poll choice object for use in the application views and repository."""
    def __init__(self, key=u'', text=u'', votes=0):
        """Initializes the poll choice."""
        self.key = key
        self.text = text
        self.votes = votes
        self.votes_percentage = None
```

Esses modelos de dados são abstrações genéricas que permitem que os modos de exibição do aplicativo trabalhar em diferentes tipos de backup de armazenamentos de dados, que serão descritos na próxima etapa.

## <a name="step-5-3-understand-the-backing-data-stores"></a>Etapa 5-3: Compreender os armazenamentos de dados de backup

O aplicativo criado pelo modelo "Pesquisas do Projeto Web do Flask" pode ser executado em um armazenamento de dados na memória, no Armazenamento de Tabelas do Azure ou em um banco de dados MongoDB.

O mecanismo de armazenamento de dados funciona da seguinte maneira:

1. O tipo de repositório é especificado por meio da variável de ambiente `REPOSITORY_NAME`, que pode ser definida como "memory", "azuretablestore" ou "mongodb". Um trecho de código em *settings.py* recupera o nome, usando "memória" como o padrão. Se desejar alterar o repositório de backup, será necessário definir a variável de ambiente e reiniciar o aplicativo.

    ```python
    from os import environ
    REPOSITORY_NAME = environ.get('REPOSITORY_NAME', 'memory')
    ```

1. Em seguida, o código *settings.py* inicializa um objeto `REPOSITORY_SETTINGS`. Se desejar usar o repositório de tabelas do Azure ou o MongoDB, será necessário inicializar primeiro os armazenamentos de dados em outro lugar e então definir as variáveis de ambiente necessárias que informarão ao aplicativo como se conectar ao armazenamento:

    ```python
    if REPOSITORY_NAME == 'azuretablestorage':
        REPOSITORY_SETTINGS = {
            'STORAGE_NAME': environ.get('STORAGE_NAME', ''),
            'STORAGE_KEY': environ.get('STORAGE_KEY', ''),
            'STORAGE_TABLE_POLL': environ.get('STORAGE_TABLE_POLL', 'polls'),
            'STORAGE_TABLE_CHOICE': environ.get('STORAGE_TABLE_CHOICE', 'choices'),
        }
    elif REPOSITORY_NAME == 'mongodb':
        REPOSITORY_SETTINGS = {
            'MONGODB_HOST': environ.get('MONGODB_HOST', None),
            'MONGODB_DATABASE': environ.get('MONGODB_DATABASE', 'polls'),
            'MONGODB_COLLECTION': environ.get('MONGODB_COLLECTION', 'polls'),
        }
    elif REPOSITORY_NAME == 'memory':
        REPOSITORY_SETTINGS = {}
    else:
        raise ValueError('Unknown repository.')
    ```

1. Em *views.py*, o aplicativo chama um método de fábrica para inicializar um objeto `Repository` usando o nome e as configurações do armazenamento de dados:

    ```python
    from FlaskPolls.models import PollNotFound
    from FlaskPolls.models.factory import create_repository
    from FlaskPolls.settings import REPOSITORY_NAME, REPOSITORY_SETTINGS

    repository = create_repository(REPOSITORY_NAME, REPOSITORY_SETTINGS)
    ```

1. O método `factory.create_repository` é encontrado em *models\factory.py*, que apenas importa o módulo de repositório adequado e cria uma instância de `Repository`:

    ```python
    def create_repository(name, settings):
        """Creates a repository from its name and settings. The settings
        is a dictionary where the keys are different for every type of repository.
        See each repository for details on the required settings."""
        if name == 'azuretablestorage':
            from .azuretablestorage import Repository
        elif name == 'mongodb':
            from .mongodb import Repository
        elif name == 'memory':
            from .memory import Repository
        else:
            raise ValueError('Unknown repository.')

        return Repository(settings)
    ```

1. As implementações da classe `Repository` que são específicas de cada armazenamento de dados podem ser encontradas em *models\azuretablestorage.py*, *models\mongodb.py* e *models\memory.py*. A implementação de Armazenamento do Azure usa o pacote azure-storage; a implementação do banco de dados Mongo usa o pacote pymongo. Conforme observado na etapa 5-1, ambos os pacotes são incluídos no arquivo *requirements.txt* do modelo de projeto. Explorar os detalhes é um exercício para o leitor.

Em resumo, a classe `Repository` resume as especificidades do armazenamento de dados, e o aplicativo usa variáveis de ambiente em tempo de execução para selecionar e configurar quais das três implementações usar.

As etapas a seguir adicionam suporte a um armazenamento de dados diferente dos três fornecidos pelo modelo de projeto se desejado:

1. Copie *memory.py* para um novo arquivo para ter a interface básica para a classe `Repository`.
1. Modifique a implementação da classe conforme seja adequado para o armazenamento de dados que você está usando.
1. Modifique *factory.py* para adicionar outro caso `elif` que reconheça o nome do armazenamento de dados adicionado e importe o módulo apropriado.
1. Modifique *settings.py* para reconhecer outro nome na variável de ambiente `REPOSITORY_NAME` e inicializar `REPOSITORY_SETTINGS` adequadamente.

### <a name="seed-the-data-store-from-samplesjson"></a>Propagar o armazenamento de dados de samples.json

Inicialmente, qualquer armazenamento de dados escolhido não contém nenhuma votação. Portanto, a home page do aplicativo exibe a mensagem **Nenhuma votação disponível** com o botão **Criar Votações de Exemplo**. No entanto, depois de selecionar o botão, o modo de exibição é alterado para exibir as votações disponíveis. Essa opção ocorre por meio de marcas condicionais em *templates\index.html* (algumas linhas em branco foram omitidas para fins de brevidade):

```html
{% extends "layout.html" %}
{% block content %}
<h2>{{title}}.</h2>

{% if polls %}
<table class="table table-hover">
    <tbody>
        {% for poll in polls %}
        <tr>
            <td>
                <a href="/poll/{{poll.key}}">{{poll.text}}</a>
            </td>
        </tr>
        {% endfor %}
    </tbody>
</table>
{% else %}
<p>No polls available.</p>
<br />
<form action="/seed" method="post">
    <button class="btn btn-primary" type="submit">Create Sample Polls</button>
</form>
{% endif %}
{% endblock %}
```

A variável `polls` no modelo vem de uma chamada a `repository.get_polls`, que não retorna nada até que o armazenamento de dados seja inicializado.

Selecionar o botão **Criar Votações de Exemplo** navega até a URL /seed. O manipulador para essa rota é definido em *views.py*:

```python
@app.route('/seed', methods=['POST'])
def seed():
    """Seeds the database with sample polls."""
    repository.add_sample_polls()
    return redirect('/')
```

A chamada a `repository.add_sample_polls()` termina em uma das implementações `Repository` específicas para seu armazenamento de dados escolhido. Cada implementação chama o método `_load_samples_json` encontrado em *models\_\_init\_\_.py* para carregar o arquivo *models\samples.json* na memória. Em seguida, ela itera por esses dados para criar os objetos `Poll` e `Choice` necessários no armazenamento de dados.

Após a conclusão desse processo, a instrução `redirect('/')` no método `seed` navega de volta para a home page. Como agora `repository.get_polls` retorna um objeto de dados, as marcas condicionais em *templates\index.html* agora renderizam uma tabela que contém as votações.

### <a name="question-how-does-one-add-new-polls-to-the-app"></a>Pergunta: como adicionar novas votações ao aplicativo?

Resposta: o aplicativo, conforme fornecido por meio do modelo de projeto, não inclui uma facilidade para adicionar ou editar votações. É possível modificar *models\samples.json* para criar dados de inicialização, mas fazer isso significará redefinir o armazenamento de dados. Para implementar funcionalidades de edição, é necessário estender a interface de classe `Repository` com métodos para criar as instâncias `Choice` e `Poll` necessárias. Em seguida, implemente uma interface do usuário em outras páginas que usam esses métodos.

## <a name="step-5-4-understand-the-poll-detail-and-results-views"></a>Etapa 5-4: Compreender os detalhes da votação e as visualizações dos resultados

A maioria dos modos de exibição gerados pelos modelos "Pesquisas do Projeto Web do Flask" e "Pesquisas do Projeto Web do Flask/Jade", como os modos de exibição para as páginas Sobre e Contato, é muito semelhantes aos modos de exibição criados pelo modelo "Projeto Web do Flask" (ou "Projeto Web do Flask/Jade") com o qual você trabalhou anteriormente neste tutorial. Na seção anterior você também aprendeu como a home page é implementada para mostrar o botão de inicialização ou a lista de votações.

O que sobra aqui é examinar os votos (detalhes) e a visualização dos resultados de uma votação individual.

Quando você seleciona uma votação na home page, o aplicativo navega até a URL /poll/\<chave\>, em que *chave* é o identificador exclusivo de uma votação. Em *views.py*, é possível ver que a função `details` é atribuída para manipular esse roteamento de URL para GET e solicitações. Também é possível ver que o uso de `<key>` na rota de URL mapeia qualquer rota desse formulário para a mesma função e gera um argumento para a função do mesmo nome:

```python
@app.route('/poll/<key>', methods=['GET', 'POST'])
def details(key):
    """Renders the poll details page."""
    error_message = ''
    if request.method == 'POST':
        try:
            choice_key = request.form['choice']
            repository.increment_vote(key, choice_key)
            return redirect('/results/{0}'.format(key))
        except KeyError:
            error_message = 'Please make a selection.'

    return render_template(
        'details.html',
        title='Poll',
        year=datetime.now().year,
        poll=repository.get_poll(key),
        error_message=error_message,
    )
```

Para mostrar uma votação (solicitações GET), essa função apenas chama *templates\details.html*, que itera pela matriz `choices` da votação, criando um botão de opção para cada uma.

```html
{% extends "layout.html" %}

{% block content %}

<h2>{{poll.text}}</h2>
<br />

{% if error_message %}
<p class="text-danger">{{error_message}}</p>
{% endif %}

<form action="/poll/{{poll.key}}" method="post">
    {% for choice in poll.choices %}
    <div class="radio">
        <label>
            <input type="radio" name="choice" id="choice{{choice.key}}" value="{{choice.key}}" />
            {{ choice.text }}
        </label>
    </div>
    {% endfor %}
    <br />
    <button class="btn btn-primary" type="submit">Vote</button>
</form>

{% endblock %}
```

Como o botão **Votar** tem `type="submit"`, selecioná-lo gera uma solicitação POST de volta para a mesma URL roteada para a função `details` mais uma vez. Desta vez, no entanto, ela extrai a opção dos dados do formulário e redireciona para /results/\<opção\>.

A URL /results/\<key\> é então encaminhada para a função `results` em *views.py*, que, por sua vez, chama o método `calculate_stats` da votação e emprega *templates\results.html* para a renderização:

```python
@app.route('/results/<key>')
def results(key):
    """Renders the results page."""
    poll = repository.get_poll(key)
    poll.calculate_stats()
    return render_template(
        'results.html',
        title='Results',
        year=datetime.now().year,
        poll=poll,
    )
```

O modelo *results.html*, por sua vez, apenas itera por meio das opções da votação e gera uma barra de progresso para cada uma:

```html
{% extends "layout.html" %}

{% block content %}

<h2>{{poll.text}}</h2>
<br />

{% for choice in poll.choices %}
<div class="row">
    <div class="col-sm-5">{{choice.text}}</div>
    <div class="col-sm-5">
        <div class="progress">
            <div class="progress-bar" role="progressbar" aria-valuenow="{{choice.votes}}" aria-valuemin="0" aria-valuemax="{{poll.total_votes}}" style="width: {{choice.votes_percentage}}%;">
                {{choice.votes}}
            </div>
        </div>
    </div>
</div>
{% endfor %}

<br />
<a class="btn btn-primary" href="/poll/{{poll.key}}">Vote again?</a>

{% endblock %}
```

## <a name="next-steps"></a>Próximas etapas

> [!Note]
> Se você tiver confirmando sua solução do Visual Studio para controle de origem ao longo deste tutorial, agora será um bom momento para fazer outra confirmação. Sua solução deve corresponder ao código-fonte do tutorial no GitHub: [Microsoft/python-sample-vs-learning-flask](https://github.com/Microsoft/python-sample-vs-learning-flask).

Agora você explorou a totalidade dos modelos "Projeto Web em Branco do Flask", "Projeto Web do Flask[/Jade]" e "Pesquisa Projeto Web de Flask[/Jade]" no Visual Studio. Você conheceu todas as noções básicas do Flask, como usar modos de exibição, modelos e roteamento, e viu como usar armazenamentos de dados de backup. Agora você poderá começar a usar um aplicativo Web por sua conta com os modos de exibição e modelos de que precisar.

A execução de um aplicativo Web no computador de desenvolvimento é apenas uma etapa para disponibilizar o aplicativo para seus clientes. As próximas etapas podem incluir as seguintes tarefas:

- Implante o aplicativo Web em um servidor de produção, como o Serviço de Aplicativo do Azure. Confira [Publicar no Serviço de Aplicativo do Azure](publishing-python-web-applications-to-azure-from-visual-studio.md).

- Adicione uma implementação de repositório que usa outro armazenamento de dados em nível de produção como o PostgreSQL, o MySQL e o SQL Server (que podem ser hospedados no Azure). Também é possível usar o [SDK do Azure para Python](azure-sdk-for-python.md) para trabalhar com serviços de armazenamento do Azure como tabelas e blobs, bem como o Cosmos DB.

- Configure um pipeline de integração contínua/implantação contínua em um serviço como o Azure DevOps. Além de trabalhar com o controle do código-fonte (por meio do Azure Repos, do GitHub ou em outro local), você pode configurar um projeto do Azure DevOps para executar automaticamente os testes de unidade como um pré-requisito para o lançamento, bem como configurar o pipeline para implantação em um servidor de preparo para testes adicionais antes de implantar na produção. O Azure DevOps, além disso, integra-se às soluções de monitoramento, como o App Insights e fecha o ciclo de inteiro com ferramentas ágeis de planejamento. Para saber mais, confira [Criar um pipeline de CI/CD para Python com o projeto do Azure DevOps](/azure/devops-project/azure-devops-project-python?view=vsts) e também a [documentação geral do Azure DevOps](/azure/devops/?view=vsts).
