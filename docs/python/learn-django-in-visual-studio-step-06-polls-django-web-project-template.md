---
title: Tutorial – Saiba mais sobre Django no Visual Studio, etapa 6
description: Um passo a passo dos conceitos básicos do Django no contexto dos projetos do Visual Studio, especificamente os recursos do modelo de pesquisas do Projeto Web do Django, como a personalização administrativa.
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
ms.openlocfilehash: 94c858a847e0e5029a989a6939a2094ed3792903
ms.sourcegitcommit: f61ad0e8babec8810295f039e67629f4bdebeef0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/19/2018
ms.locfileid: "52001250"
---
# <a name="step-6-use-the-polls-django-web-project-template"></a>Etapa 6: Usar o modelo Projeto Web do Django de pesquisas

**Etapa anterior: [Autenticar usuários em Django](learn-django-in-visual-studio-step-05-django-authentication.md)**

Depois de entender o modelo de "Projeto Web do Django" do Visual Studio, você agora pode examinar o terceiro modelo do Django, "Pesquisas do projeto Web do Django", que tem como base a mesma base de código e demonstra o trabalho com um banco de dados.

Nesta etapa, você aprenderá a:

> [!div class="checklist"]
> - Criar um projeto do modelo e inicializar o banco de dados (etapa 6-1)
> - Compreender os modelos de dados (etapa 6-2)
> - Aplicar migrações (etapa 6-3)
> - Entender os modos de exibição e os modelos de página criados pelo modelo de projeto (etapa 6-4)
> - Criar uma interface de administração personalizada (etapa 6-5)

Um projeto criado usando este modelo é semelhante ao obtido seguindo o tutorial [Como escrever seu primeiro aplicativo do Django](https://docs.djangoproject.com/en/2.0/intro/tutorial01/) nos documentos do Django. O aplicativo Web consiste em um site público que permite às pessoas exibirem pesquisas e votarem nelas, juntamente com uma interface administrativa personalizada por meio da qual você pode gerenciar pesquisas. Ele usa o mesmo sistema de autenticação que o modelo "Projeto Web do Django" e usa mais o banco de dados implementando modelos do Django conforme explorado nas seções a seguir.

## <a name="step-6-1-create-the-project-and-initialize-the-database"></a>Etapa 6-1: Criar o projeto e inicializar o banco de dados

1. No Visual Studio, acesse o **Gerenciador de Soluções**, clique com o botão direito do mouse na solução **LearningDjango** criada anteriormente neste tutorial e selecione **Adicionar** > **Novo Projeto**. (Como alternativa, se você quiser usar uma nova solução, selecione **Arquivo** > **Novo** > **Projeto**).

1. Na caixa de diálogo Novo Projeto, pesquise e selecione o modelo **Projeto Web de Votações do Django**, nomeie o projeto "DjangoPolls" e selecione **OK**.

1. Como os outros modelos de projeto do Visual Studio, o modelo de "Projeto Web de Votações do Django" inclui um arquivo *requirements.txt*. Os prompts do Visual Studio solicitam o local em que essas dependências serão instaladas. Escolha a opção **Instalar em um ambiente virtual** e, na caixa de diálogo **Adicionar Ambiente Virtual**, selecione **Criar** para aceitar os padrões.

1. Quando o Python concluir a configuração do ambiente virtual, siga as instruções no *readme.html* exibido para inicializar o banco de dados e criar um superusuário do Django (ou seja, um administrador). As etapas são primeiro clicar com o botão direito do mouse no projeto **DjangoPolls** no **Gerenciador de Soluções**, selecionar o comando **Python** > **Django Migrate**, clicar com o botão direito do mouse novamente no projeto, selecionar o comando **Python** > **Django Create Superuser** e seguir os prompts. (Se você tentar criar um superusuário pela primeira vez, verá um erro porque o banco de dados não foi inicializado).

1. Defina o projeto **DjangoPolls** para ser o padrão para a solução do Visual Studio clicando com o botão direito do mouse no projeto em **Gerenciador de Soluções** e selecionando **Definir como Projeto de Inicialização**. O projeto de inicialização, mostrado em negrito, é o que é executado quando você inicia o depurador.

1. Selecione **Depurar** > **Iniciar Depuração** (**F5**) ou use o botão **Servidor Web** na barra de ferramentas para executar o servidor:

    ![Executar o botão da barra de ferramentas do servidor Web no Visual Studio](media/django/run-web-server-toolbar-button.png)

1. O aplicativo criado pelo modelo tem três páginas, Página inicial, Sobre e Contato, que você navega usando a barra de navegação superior. Leve alguns minutos para examinar as diferentes partes do aplicativo (as páginas Sobre e Contato são muito semelhantes ao "Projeto Web do Django" e não serão mais discutidas).

    ![Exibição completa do navegador do aplicativo de pesquisas de Projeto Web do Django](media/django/step06-full-app-view.png)

1. Selecione também o link **Administração** na barra de navegação, que exibe uma tela de logon para demonstrar que a interface administrativa é autorizada somente para administradores autenticados. Use as credenciais de superusuário e você será encaminhado para a página "/admin", que é habilitada por padrão ao usar este modelo de projeto.

    ![Exibição administrativa do aplicativo de pesquisas de Projeto Web do Django](media/django/step06-polls-administrative-interface.png)

1. Você pode deixar o aplicativo em execução para as seções a seguir.

    Caso deseje interromper o aplicativo e [confirmar as alterações no controle do código-fonte](learn-django-in-visual-studio-step-02-create-an-app.md#commit-to-source-control), primeiro abra a página **Alterações** no **Team Explorer**, clique com o botão direito do mouse na pasta do ambiente virtual (provavelmente **env**) e selecione **Ignorar estes itens locais**.

### <a name="examine-the-project-contents"></a>Examine o conteúdo do projeto

Conforme observado anteriormente, quase tudo o que está em um projeto criado a partir do modelo "Pesquisas do Projeto Web do Django" deverá ser conhecido se você tiver explorado os outros modelos de projeto no Visual Studio. As etapas adicionais neste artigo resumem as mais alterações e adições mais significativas, ou seja, modelos de dados e modos de exibição adicionais.

### <a name="question-what-does-the-django-migrate-command-do"></a>Pergunta: O que faz o comando Django Migrate?

Resposta: O comando **Django Migrate** especificamente executa o comando `manage.py migrate`, que executa todos os scripts na pasta *app/migrations* que não foram executados anteriormente. Nesse caso, o comando executa o script *0001_initial.py* nessa pasta para configurar o esquema necessário no banco de dados.

O script de migração em si é criado pelo comando `manage.py makemigrations`, que examina o arquivo *models.py* do aplicativo, compara-o com o estado atual do banco de dados e, em seguida, gera os scripts necessários para migrar o esquema de banco de dados para que ele corresponda aos modelos atuais. Esse recurso do Django é muito eficiente durante a atualização e modificação dos modelos ao longo do tempo. Ao gerar e executar migrações, você mantém os modelos e o banco de dados em sincronia com facilidade.

Você trabalha com uma migração na etapa 6-3 neste artigo.

## <a name="step-6-2-understand-data-models"></a>Etapa 6-2: Compreender os modelos de dados

Os modelos do aplicativo, chamados Votação e Opção, são definidos em *app/models.py*. Cada um é uma classe do Python que deriva de `django.db.models.Model` e usa métodos da classe `models` como `CharField` e `IntegerField` para definir campos no modelo, que são mapeados para colunas de banco de dados.

```python
from django.db import models
from django.db.models import Sum

class Poll(models.Model):
    """A poll object for use in the application views and repository."""
    text = models.CharField(max_length=200)
    pub_date = models.DateTimeField('date published')

    def total_votes(self):
        """Calculates the total number of votes for this poll."""
        return self.choice_set.aggregate(Sum('votes'))['votes__sum']

    def __unicode__(self):
        """Returns a string representation of a poll."""
        return self.text

class Choice(models.Model):
    """A poll choice object for use in the application views and repository."""
    poll = models.ForeignKey(Poll)
    text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)

    def votes_percentage(self):
        """Calculates the percentage of votes for this choice."""
        total = self.poll.total_votes()
        return self.votes / float(total) * 100 if total > 0 else 0

    def __unicode__(self):
        """Returns a string representation of a choice."""
        return self.text
```

Como você pode ver, uma Pesquisa mantém uma descrição em seu campo `text` e uma data de publicação no `pub_date`. Esses campos são os únicos que existem para a Votação no banco de dados; o campo `total_votes` é calculado em tempo de execução.

Uma Opção está relacionada a uma Pesquisa por meio do campo `poll`, contém uma descrição no `text`e mantém uma contagem para aquela opção no `votes`. O campo `votes_percentage` é calculado em tempo de execução e não foi encontrado no banco de dados.

A lista completa de tipos de campo é `CharField` (texto limitado) `TextField` (texto ilimitado), `EmailField`, `URLField`, `DateTimeField`, `IntegerField`, `DecimalField`, `BooleanField`, `ForeignKey` e `ManyToMany`. Cada campo utiliza alguns atributos, como `max_length`. O atributo `blank=True` significa que o campo é opcional; `null=true` significa que um valor é opcional. Também há um atributo `choices` que limita valores a valores em uma matriz de tuplas de valor de dados/valor de exibição. (Veja a [Referência de campo de modelo](https://docs.djangoproject.com/en/2.0/ref/models/fields/) na documentação do Django).

Você pode confirmar exatamente o que está armazenado no banco de dados examinando o arquivo *db.sqlite3* no projeto usando uma ferramenta como o [navegador SQLite](https://sqlitebrowser.org/). No banco de dados, você verá que um campo de chave estrangeira como `poll` no modelo Escolher está armazenado como `poll_id`; o Django trata o mapeamento automaticamente.

Em geral, trabalhar com seu banco de dados no Django significa trabalhar exclusivamente por meio de seus modelos de forma que o Django possa gerenciar o banco de dados subjacente em seu nome.

### <a name="seed-the-database-from-samplesjson"></a>Propagar o banco de dados de samples.json

Inicialmente, o banco de dados não contém pesquisas. Você pode usar a interface administrativa na URL "/admin" para adicionar votações manualmente, e também pode visitar a página "/seed" no site em execução para adicionar uma semente ao banco de dados com votações definidas no arquivo *samples.json* do aplicativo.

O *urls.py* do projeto do Django tem um padrão de URL adicionado, `url(r'^seed$', app.views.seed, name='seed'),`. A exibição `seed` em *app/views.py* carrega o arquivo *samples.json* e cria os objetos de modelo necessários. O Django, em seguida, cria automaticamente os registros correspondentes no banco de dados subjacente.

Observe o uso do decorador `@login_required` para indicar o nível de autorização para o modo de exibição.

```python
@login_required
def seed(request):
    """Seeds the database with sample polls."""
    samples_path = path.join(path.dirname(__file__), 'samples.json')
    with open(samples_path, 'r') as samples_file:
        samples_polls = json.load(samples_file)

    for sample_poll in samples_polls:
        poll = Poll()
        poll.text = sample_poll['text']
        poll.pub_date = timezone.now()
        poll.save()

        for sample_choice in sample_poll['choices']:
            choice = Choice()
            choice.poll = poll
            choice.text = sample_choice
            choice.votes = 0
            choice.save()

    return HttpResponseRedirect(reverse('app:home'))
```

Para ver o efeito, execute o aplicativo primeiro para verificar se não há alguma pesquisa. Visite a URL "/seed" e, quando o aplicativo retornar para a página inicial, você verá que as pesquisas ficaram disponíveis. Novamente, fique à vontade para examinar o arquivo *db.sqlite3* bruto com uma ferramenta como o [navegador SQLite](https://sqlitebrowser.org/).

![O aplicativo de pesquisas do Projeto Web do Django com um banco de dados de propagação](media/django/step06-app-with-seeded-database.png)

### <a name="question-is-it-possible-to-initialize-the-database-using-the-django-administrative-utility"></a>Pergunta: É possível inicializar o banco de dados usando o utilitário administrativo do Django?

Resposta: Sim, você pode usar o [comando django-admin loaddata](https://docs.djangoproject.com/en/1.9/ref/django-admin/#loaddata) para realizar a mesma tarefa que a página de propagação no aplicativo. Ao trabalhar em um aplicativo Web completo, você pode usar uma combinação dos dois métodos: inicializar um banco de dados da linha de comando e, em seguida, converter a página de propagação aqui para uma API para a qual você pode enviar qualquer outro JSON arbitrário em vez de depender de um arquivo codificado.

## <a name="step-6-3-use-migrations"></a>Etapa 6-3: Usar migrações

Quando você executou o comando `manage.py makemigrations` (usando o menu de contexto no Visual Studio) depois de criar o projeto, o Django criou o arquivo *app/migrations/0001_initial.py*. Esse arquivo contém um script que cria as tabelas de banco de dados iniciais.

Como você inevitavelmente fará alterações a seus modelos ao longo do tempo, o Django facilitará a atualização do esquema de banco de dados subjacente com esses modelos. O fluxo de trabalho geral é o seguinte:

1. Faça alterações nos modelos no arquivo *models.py*.
1. No Visual Studio, clique com o botão direito no projeto no **Gerenciador de Soluções** e selecione o comando **Python** > **Django Make Migrations**. Conforme descrito anteriormente, esse comando gera scripts no *app/migrations* para migrar o banco de dados de seu estado atual para o novo estado.
1. Para aplicar os scripts para o banco de dados real, clique com o botão direito no projeto novamente e selecione **Python** > **Django Migrate**.

O Django controla quais migrações foram aplicadas a qualquer banco de dados determinado, de modo que, quando você executar o comando de migração, o Django aplicará as migrações necessárias. Se você criar um novo banco de dados vazio, por exemplo, executar o comando de migração atualiza-o com seus modelos atuais aplicando todos os scripts de migração. Da mesma forma, se você fizer várias alterações do modelo e gerar migrações de um computador de desenvolvimento, poderá aplicar as migrações cumulativas ao seu banco de dados de produção, executando o comando de migração no servidor de produção. O Django novamente aplica-se apenas a esses scripts de migração que foram gerados desde a última migração do banco de dados de produção.

Para ver o efeito de alterar um modelo, tente as seguintes etapas:

1. Adicionar um campo de autor opcional ao modelo Poll em *app/models.py* adicionando a seguinte linha após o campo `pub_date` para adicionar um campo `author` opcional:

    ```python
    author = models.CharField(max_length=100, blank=True)
    ```

1. Salve o arquivo e, em seguida, no **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto **DjangoPolls** e selecione o comando **Python** > **Django Make Migrations**.
1. Selecione o comando **Projeto** > **Mostrar Todos os Arquivos** para ver o script recém-gerado na pasta **migrations**, cujo nome começa com **002_auto_**. Clique com o botão direito no arquivo e selecione **Include In Project**. Você pode selecionar **Project** > **Show All Files** novamente para restaurar o modo de exibição original. (Veja a segunda pergunta abaixo para obter detalhes sobre esta etapa).
1. Se desejar, abra o arquivo para examinar como os scripts do Django são alterados do estado de modelo anterior para o novo estado.
1. Clique com o botão direito no projeto do Visual Studio novamente e selecione **Python** > **Django Migrate** para aplicar as alterações ao banco de dados.
1. Se desejar, abra o banco de dados em um visualizador apropriado para confirmar a alteração.

Em geral, o recurso de migração do Django significa que você nunca precisa gerenciar seu esquema de banco de dados manualmente. Basta fazer alterações em seus modelos, gerar scripts de migração e aplicá-las com o comando de migração.

### <a name="question-what-happens-if-i-forget-to-run-the-migrate-command-after-making-changes-to-models"></a>Pergunta: O que acontece se eu esquecer de executar o comando de migração depois de fazer alterações nos modelos?

Resposta: Se os modelos não corresponderem ao que está no banco de dados, o Django falhará em tempo de execução com as exceções adequadas. Por exemplo, se você esquecer de migrar a alteração do modelo mostrada na seção anterior, verá o erro **no such column: app_poll.author**:

![Erro mostrado quando uma alteração de modelo não tiver sido migrada](media/django/step06-exception-when-forgetting-to-migrate.png).

### <a name="question-why-doesnt-solution-explorer-show-newly-generated-scripts-after-running-django-make-migrations"></a>Pergunta: Por que o Gerenciador de Soluções não mostra os scripts gerados recentemente após executar Django Make Migrations?

Resposta: Embora os scripts recém-gerados estejam na pasta *app/migrations* e sejam aplicados quando o comando **Django Migrate** é executado, eles não são exibidos automaticamente no **Gerenciador de Soluções** porque não foram adicionados ao projeto do Visual Studio. Para torná-las visíveis, primeiro selecione o comando de menu **Project** > **Show All Files** ou botão da barra de ferramentas descrito na imagem abaixo. Esse comando faz o **Gerenciador de Soluções** mostrar todos os arquivos na pasta do projeto, com um ícone de contorno pontilhado para itens que não foram adicionados ao projeto em si. Clique com o botão direito nos arquivos que você deseja adicionar e selecione **Include In Project**, que também os inclui no controle de origem com a próxima confirmação.

![Comando Include In Project no Gerenciador de Soluções](media/django/step06-include-migrations-script-in-project.png)

### <a name="question-can-i-see-what-migrations-would-be-applied-before-running-the-migrate-command"></a>Pergunta: Posso ver quais migrações serão aplicadas antes de executar o comando de migração?

Resposta: Sim, use o [comando django-admin showmigrations](https://docs.djangoproject.com/en/2.0/ref/django-admin/#showmigrations).

## <a name="step-6-4-understand-the-views-and-page-templates-created-by-the-project-template"></a>Etapa 6-4: Entender os modos de exibição e os modelos de página criados pelo modelo de projeto

A maioria dos modos de exibição gerados pelo modelo "Pesquisas de Projeto Web do Django", como os modos de exibição para as páginas Sobre e Contato, é muito semelhantes a exibições criadas pelo modelo "Projeto Web do Django" com o qual você trabalhou anteriormente neste tutorial. A diferença no aplicativo de pesquisas de aplicativo é que sua página inicial usa modelos, assim como várias páginas adicionadas para votação e visualizar os resultados da pesquisa.

Em primeiro lugar, a primeira linha na matriz `urlpatterns` do projeto do Django no arquivo *urls.py* é mais do que apenas um simples roteamento para uma exibição do aplicativo. Em vez disso, ele efetua pull do próprio arquivo *urls.py* do aplicativo:

```python
from django.conf.urls import url, include
import app.views

urlpatterns = [
    url(r'^', include('app.urls', namespace="app")),
    # ..
]
```

O arquivo *app/urls.py* contém um código de roteamento mais interessante (comentários explicativos adicionados):

```python
urlpatterns = [
    # Home page routing
    url(r'^$',
        app.views.PollListView.as_view(
            queryset=Poll.objects.order_by('-pub_date')[:5],
            context_object_name='latest_poll_list',
            template_name='app/index.html',),
        name='home'),

    # Routing for a poll page, which use URLs in the form <poll_id>/,
    # where the id number is captured as a group named "pk".
    url(r'^(?P<pk>\d+)/$',
        app.views.PollDetailView.as_view(
            template_name='app/details.html'),
        name='detail'),

    # Routing for <poll_id>/results pages, again using a capture group
    # named pk.
    url(r'^(?P<pk>\d+)/results/$',
        app.views.PollResultsView.as_view(
            template_name='app/results.html'),
        name='results'),

    # Routing for <poll_id>/vote pages, with the capture group named
    # poll_id this time, which becomes an argument passed to the view.
    url(r'^(?P<poll_id>\d+)/vote/$', app.views.vote, name='vote'),
]
```

Se você não estiver familiarizado com as expressões regulares mais complexas usadas aqui, poderá colar a expressão em [regex101.com](https://regex101.com/) para obter uma explicação em linguagem simples. (Será necessário escapar as barras invertidas `/` adicionando uma barra invertida, `\` antes delas; o escape não é necessário no Python devido ao prefixo `r` na cadeia de caracteres, que significa "bruto").

No Django, a sintaxe `?P<name>pattern` cria um grupo chamado `name`, que é passado como argumentos para exibições na ordem em que aparecem. No código mostrado anteriormente, `PollsDetailView` e `PollsResultsView` recebem um argumento denominado `pk` e `app.views.vote` recebe um argumento denominado `poll_id`.

Você também pode ver que a maioria das exibições não é apenas uma referência direta a uma função de exibição em *app/views.py*. Em vez disso, a maioria se refere a uma classe no mesmo arquivo que deriva de `django.views.generic.ListView` ou `django.views.generic.DetailView`. As classes base fornecem os métodos `as_view`, que levam um argumento `template_name` para identificar o modelo. A classe base `ListView`, como usado para a página inicial, também espera uma propriedade `queryset` que contém os dados e uma propriedade `context_object_name` com o nome de variável pelo qual você deseja se referir aos dados no modelo, nesse caso `latest_poll_list`.

Agora você pode examinar a `PollListView` da home page, que é definida da seguinte maneira em *app/views.py*:

```python
class PollListView(ListView):
    """Renders the home page, with a list of all polls."""
    model = Poll

    def get_context_data(self, **kwargs):
        context = super(PollListView, self).get_context_data(**kwargs)
        context['title'] = 'Polls'
        context['year'] = datetime.now().year
        return context
```

Tudo o que foi feito aqui é para identificar o modelo de que o modo de exibição funciona com (Pesquisa) e substitui o método `get_context_data` para adicionar os valores `title` e `year` para o contexto.

O núcleo do modelo (*templates/app/index.html*) é o seguinte:

```html
{% if latest_poll_list %}
<table class="table table-hover">
    <tbody>
        {% for poll in latest_poll_list %}
        <tr>
            <td>
                <a href="{% url 'app:detail' poll.id %}">{{poll.text}}</a>
            </td>
        </tr>
        {% endfor %}
    </tbody>
</table>
{% else %}
<!-- ... other content omitted ... -->
{% endif %}
```

Em suma, o modelo recebe a lista de objetos de pesquisa no `latest_poll_list` e, em seguida, itera por meio dessa lista para criar uma linha da tabela que contém um link para cada pesquisa usando o valor `text` da pesquisa. Na marcação `{% url %}`, "app:detail" refere-se ao padrão de URL em *app/urls.py* chamado "detail", usando `poll.id` como argumento. O efeito disso é que o Django cria uma URL usando o padrão apropriado e usa isso para o link. Essa certa garantia de durabilidade significa que você pode alterar esse padrão de URL a qualquer momento e os links gerados automaticamente para corresponder.

As classes `PollDetailView` e `PollResultsView` em *app/views.py* (não mostradas aqui) são praticamente idênticas a `PollListView`, exceto pelo fato de que derivam de `DetailView`. Seus respectivos modelos, *app/templates/details.html* e *app/templates/results.html*, colocam então os campos apropriados dos modelos dentro de vários controles HTML. Uma parte exclusiva em *details.html* é que as opções para uma votação estão contidas dentro de um formulário HTML que, quando enviado, executa um POST na URL /vote. Conforme visto anteriormente, esse padrão de URL é roteado para `app.views.vote`, que é implementado da seguinte maneira (observe o argumento `poll_id`, que é novamente um grupo nomeado na expressão regular usada no roteamento para este modo de exibição):

```python
def vote(request, poll_id):
    """Handles voting. Validates input and updates the repository."""
    poll = get_object_or_404(Poll, pk=poll_id)
    try:
        selected_choice = poll.choice_set.get(pk=request.POST['choice'])
    except (KeyError, Choice.DoesNotExist):
        return render(request, 'app/details.html', {
            'title': 'Poll',
            'year': datetime.now().year,
            'poll': poll,
            'error_message': "Please make a selection.",
    })
    else:
        selected_choice.votes += 1
        selected_choice.save()
        return HttpResponseRedirect(reverse('app:results', args=(poll.id,)))
```

Aqui o modo de exibição não tem seu próprio modelo correspondente como as outras páginas. Em vez disso, ele valida a pesquisas selecionada, mostrando 404 se o a pesquisa não existir (no caso de alguém inserir uma URL como "vote/1a2b3c"). Em seguida, ele verifica se a opção votada é válida para a pesquisa. Caso contrário, o bloco `except` processa a página de detalhes novamente com uma mensagem de erro. Se a opção for válida, o modo de exibição também incluirá o voto e redirecionará para a página de resultados.

## <a name="step-6-5-create-a-custom-administration-interface"></a>Etapa 6-5: Criar uma interface de administração personalizada

As últimas partes do modelo "Pesquisas de Projeto Web do Django" são extensões personalizadas para a interface administrativa padrão do Django, conforme mostrado anteriormente neste artigo na etapa 6-1. A interface padrão fornece o usuário e o gerenciamento de grupo, nada mais. O modelo de projeto de pesquisa adiciona recursos que permitem que você gerencie pesquisas também.

Em primeiro lugar, os padrões de URL em *urls.py* do projeto do Django tem `url(r'^admin/', include(admin.site.urls)),` incluído por padrão; o padrão "admin/doc" também está incluído, mas está com marca de comentário.

Em seguida, o aplicativo contém o arquivo *admin.py*, que o Django executa automaticamente quando você visita a interface administrativa, graças à inclusão de `django.contrib.admin` na matriz `INSTALLED_APPS` de *settings.py*. O código nesse arquivo, conforme fornecido pelo modelo de projeto, é o seguinte:

```python
from django.contrib import admin
from app.models import Choice, Poll

class ChoiceInline(admin.TabularInline):
    """Choice objects can be edited inline in the Poll editor."""
    model = Choice
    extra = 3

class PollAdmin(admin.ModelAdmin):
    """Definition of the Poll editor."""
    fieldsets = [
        (None, {'fields': ['text']}),
        ('Date information', {'fields': ['pub_date']}),
    ]
    inlines = [ChoiceInline]
    list_display = ('text', 'pub_date')
    list_filter = ['pub_date']
    search_fields = ['text']
    date_hierarchy = 'pub_date'

admin.site.register(Poll, PollAdmin)
```

Como você pode ver, a classe `PollAdmin` deriva de `django.contrib.admin.ModelAdmin` e personaliza vários de seus campos usando nomes do modelo `Poll`, que ele gerencia. Esses campos são descritos nas [opções de ModelAdmin](https://docs.djangoproject.com/en/2.0/ref/contrib/admin/#modeladmin-options) na documentação do Django.

A chamada para `admin.site.register` em seguida conecta-se a essa classe para o modelo (`Poll`) e a inclui na interface de administração. O resultado geral é mostrado abaixo:

![Exibição administrativa do aplicativo de pesquisas de Projeto Web do Django](media/django/step06-polls-administrative-interface.png)

## <a name="next-steps"></a>Próximas etapas

> [!Note]
> Se você tiver confirmando sua solução do Visual Studio para controle de origem ao longo deste tutorial, agora será um bom momento para fazer outra confirmação. A solução deve corresponder ao código-fonte do tutorial no GitHub: [Microsoft/python-sample-vs-learning-django](https://github.com/Microsoft/python-sample-vs-learning-django).

Agora você explorou a totalidade dos modelos de "Projeto em branco da Web do Django", "Projeto da Web do Django" e "Pesquisas de Projeto Web do Django" no Visual Studio. Você aprendeu as noções básicas do Django como o uso de modelos e modos de exibição e explorou roteamento, autenticação e uso de modelos de banco de dados. Agora você deverá ser capaz de criar um aplicativo Web por sua conta com os modos de exibição e os modelos de que precisar.

A execução de um aplicativo Web no computador de desenvolvimento é apenas uma etapa para disponibilizar o aplicativo para seus clientes. As próximas etapas podem incluir as seguintes tarefas:

- Implante o aplicativo Web em um servidor de produção, como o Serviço de Aplicativo do Azure. Confira [Publicar no Serviço de Aplicativo do Azure](publishing-python-web-applications-to-azure-from-visual-studio.md).

- Personalizar a página 404 criando um modelo chamado *templates/404.html*. Quando presente, o Django usa esse modelo, em vez de seu padrão. Para saber mais, veja [Modos de exibição de erro](https://docs.djangoproject.com/en/2.0/ref/views/#error-views) na documentação do Django.

- Escreva testes de unidade em *tests.py*; os modelos de projeto do Visual Studio fornecem pontos iniciais para eles e mais informações podem ser encontradas em [Escrevendo seu primeiro aplicativo do Django, parte 5 – teste](https://docs.djangoproject.com/en/2.0/intro/tutorial05/) e [Testando no Django](https://docs.djangoproject.com/en/2.0/topics/testing/) na documentação do Django.

- Altere o aplicativo de SQLite para um repositório de dados de nível de produção como PostgreSQL, MySQL e SQL Server (que pode ser hospedado no Azure). Conforme descrito em [Quando usar o SQLite](https://www.sqlite.org/whentouse.html) (sqlite.org), o SQLite funciona bem para sites de tráfego baixo a médio com menos de 100 mil acessos por dia, mas não é recomendado para volumes maiores. Também é limitado a um único computador, de modo que ele não pode ser usado em qualquer cenário de vários servidores, como balanceamento de carga e replicação geográfica. Para obter informações sobre o suporte do Django para outros bancos de dados, veja [Instalação do banco de dados](https://docs.djangoproject.com/en/2.0/intro/tutorial02/#database-setup). Você também pode usar o [SDK do Azure para Python](azure-sdk-for-python.md) para trabalhar com serviços de armazenamento do Azure como tabelas e blobs.

- Configure um pipeline de integração contínua/implantação contínua em um serviço como o Azure DevOps. Além de trabalhar com o controle do código-fonte (por meio do Azure Repos, do GitHub ou em outro local), você pode configurar um projeto do Azure DevOps para executar automaticamente os testes de unidade como um pré-requisito para o lançamento, bem como configurar o pipeline para implantação em um servidor de preparo para testes adicionais antes de implantar na produção. O Azure DevOps, além disso, integra-se às soluções de monitoramento, como o App Insights e fecha o ciclo de inteiro com ferramentas ágeis de planejamento. Para saber mais, confira [Criar um pipeline de CI/CD para Python com o projeto do Azure DevOps](/azure/devops-project/azure-devops-project-python?view=vsts) e também a [documentação geral do Azure DevOps](/azure/devops/?view=vsts).
