---
title: Tutorial – Saiba mais sobre Django no Visual Studio, etapa 1
description: Um passo a passo com as noções básicas do Django no contexto dos projetos do Visual Studio, demonstrando o suporte que o Visual Studio oferece para o desenvolvimento do Django.
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
ms.openlocfilehash: 32779861c3f7b8a0bc8ea9e8a3a42d00a8226e1a
ms.sourcegitcommit: f61ad0e8babec8810295f039e67629f4bdebeef0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/19/2018
ms.locfileid: "52001237"
---
# <a name="tutorial-get-started-with-the-django-web-framework-in-visual-studio"></a>Tutorial: Introdução à estrutura da Web do Django no Visual Studio

O [Django](https://www.djangoproject.com/) é uma estrutura do Python de alto nível projetada para um desenvolvimento da Web rápido, seguro e escalonável. Este tutorial explora a estrutura do Django no contexto dos modelos de projeto que o Visual Studio fornece para simplificar a criação de aplicativos Web baseados no Django.

Neste tutorial, você aprenderá como:

> [!div class="checklist"]
> - Criar um projeto básico do Django em um repositório Git usando o modelo "Projeto Web em Branco do Django" (etapa 1)
> - Criar um aplicativo do Django com uma página e renderizar essa página usando um modelo (etapa 2)
> - Fornecer arquivos estáticos, adicionar páginas e usar a herança do modelo (etapa 3)
> - Usar o modelo Projeto Web do Django para criar um aplicativo com várias páginas e design responsivo (etapa 4)
> - Autenticar usuários (etapa 5)
> - Usar o modelo Pesquisas Projeto Web do Django para criar um aplicativo que usa modelos, migrações de banco de dados e personalizações na interface administrativa (etapa 6)

## <a name="prerequisites"></a>Pré-requisitos

- Visual Studio 2017 no Windows com as seguintes opções:
  - A carga de trabalho **desenvolvimento do Python** (guia **Carga de Trabalho** no instalador). Para obter instruções, confira [Instalar o suporte do Python no Visual Studio](installing-python-support-in-visual-studio.md).
  - **GIT para Windows** e **Extensão GitHub para Visual Studio** na guia **Componentes individuais** em **Code Tools**.

Os modelos de projeto do Django também estão incluídos em todas as versões anteriores das Ferramentas Python para Visual Studio, embora os detalhes possam ser diferentes dos que são discutidos neste tutorial (especialmente diferentes nas versões anteriores da estrutura do Django).

No momento, não há suporte para o desenvolvimento do Python no Visual Studio para Mac. No Mac e no Linux, use a [Extensão Python no Visual Studio Code](https://code.visualstudio.com/docs/python/python-tutorial).

### <a name="visual-studio-projects-and-django-projects"></a>"Projetos do Visual Studio" e "Projetos do Django"

Na terminologia do Django, um "projeto do Django" é composto de vários arquivos de configuração do nível de site, juntamente com um ou mais "aplicativos" que você implementa em um host Web para criar um aplicativo Web completo. Um projeto do Django pode conter vários aplicativos e o mesmo aplicativo pode estar presente em vários projetos do Django.

Um projeto do Visual Studio, por sua vez, pode conter o projeto do Django juntamente com vários aplicativos. Para simplificar, sempre que este tutorial referir-se apenas a um "projeto," ele estará se referindo ao projeto do Visual Studio. Quando se referir ao "projeto do Django" do aplicativo Web, ele usará "projeto do Django" especificamente.

No decorrer deste tutorial, você criará uma única solução do Visual Studio que contém três projetos independentes do Django, cada um contendo um único aplicativo do Django. Se você mantiver os projetos na mesma solução, poderá facilmente alternar entre diferentes arquivos para comparação.

## <a name="step-1-1-create-a-visual-studio-project-and-solution"></a>Etapa 1-1: Criar uma solução e um projeto do Visual Studio

Ao trabalhar com o Django na linha de comando, você geralmente inicia um projeto executando o comando `django-admin startproject <project_name>`. No Visual Studio, se você usar o modelo "Projeto Web em Branco do Django", fornecerá a mesma estrutura em uma solução e projeto do Visual Studio.

1. No Visual Studio, escolha **Arquivo** > **Novo** > **Projeto**, pesquise "Django" e escolha o modelo **Projeto Web Django em Branco**. O modelo também pode ser encontrado em **Python** > **Web** na lista à esquerda.

    ![Nova caixa de diálogo do projeto no Visual Studio para o Projeto Web em Branco do Django](media/django/step01-new-blank-project.png)

1. Nos campos, na parte inferior da caixa de diálogo, insira as informações a seguir (conforme mostrado no gráfico anterior) e, em seguida, escolha **OK**:

    - **Nome**: defina o nome do projeto do Visual Studio como **BasicProject**. Esse nome também é usado para o projeto do Django.
    - **Local**: especifique um local no qual criar o projeto e a solução do Visual Studio.
    - **Solução**: mantenha esse controle definido com a opção padrão **Criar nova solução**.
    - **Nome da solução**: definido como **LearningDjango**, que é apropriado para a solução como um contêiner para vários projetos neste tutorial.
    - **Criar diretório para a solução**: deixar definido (o padrão).
    - **Criar um novo repositório Git**: escolha essa opção (que é clara por padrão) para que o Visual Studio crie um repositório Git local quando criar a solução. Caso essa opção não seja exibida, execute o instalador do Visual Studio 2017 e adicione o **GIT para Windows** e a **Extensão do GitHub para Visual Studio** à guia **Componentes individuais** em **Ferramentas de código**.

1. Após alguns instantes, o Visual Studio fará uma solicitação em uma caixa de diálogo com a mensagem **Este projeto exige pacotes externos** (mostrado abaixo). Essa caixa de diálogo é exibida porque o modelo inclui um arquivo *requirements.txt* que referencia o último pacote do Django 1.x. Escolha **Mostrar pacotes necessários** para ver as dependências exatas.

    ![Solicitação dizendo que o projeto requer pacotes externos](media/django/step01-requirements-prompt-install-myself.png)

1. Escolha a opção **Eu vou instalá-los sozinho**. Crie o ambiente virtual logo em seguida para garantir que ele será excluído do controle do código-fonte. (O ambiente pode ser sempre criado com base em *requirements.txt*.)

## <a name="step-1-2-examine-the-git-controls-and-publish-to-a-remote-repository"></a>Etapa 1-2: Examinar os controles do Git e publicar em um repositório remoto

Como você marcou a opção **Criar novo repositório Git** na caixa de diálogo **Novo Projeto**, o projeto já ficará confirmado no controle do código-fonte local assim que o processo de criação for concluído. Nesta etapa, familiarize-se com os controles do Git do Visual Studio e a janela do **Team Explorer** onde você trabalha com o controle do código-fonte.

1. Observe os controles do Git no canto inferior da janela principal do Visual Studio. Da esquerda para direita, esses controles mostram confirmações não enviadas, as alterações não confirmadas, o nome do repositório e a ramificação atual:

    ![Controles do Git na janela do Visual Studio](media/django/step01-git-controls.png)

    > [!Note]
    > Se você não marcar a opção **Criar novo repositório Git** na caixa de diálogo **Novo Projeto**, os controles do Git mostrarão apenas um comando **Adicionar ao controle do código-fonte** que criará um repositório local.
    >
    > ![Se você não tiver criado um repositório, o comando Adicionar ao controle do código-fonte será exibido no Visual Studio](media/django/step01-git-add-to-source-control.png)

1. Marque o botão de alterações e o Visual Studio abrirá a janela do **Team Explorer** na página **Alterações**. Como o projeto recém-criado já está automaticamente confirmado no controle do código-fonte, você não verá as alterações pendentes.

    ![Janela do Team Explorer na página Alterações](media/django/step01-team-explorer-changes.png)

1. Na barra de status do Visual Studio, marque o botão de confirmação não enviada (a seta para cima com um **2**) para abrir a página **Sincronização** no **Team Explorer**. Como você tem apenas um repositório local, a página oferece opções simples para publicar o repositório em diferentes repositórios remotos.

    ![Janela do Team Explorer mostrando opções do repositório Git disponíveis para o controle do código-fonte](media/django/step01-team-explorer.png)

    Você pode escolher o serviço que desejar para seus próprios projetos. Este tutorial mostra o uso do GitHub, em que o código de exemplo concluído do tutorial é mantido no repositório [Microsoft/python-sample-vs-learning-django](https://github.com/Microsoft/python-sample-vs-learning-django).

1. Ao selecionar qualquer um dos controles **Publicar**, o **Team Explorer** solicitará mais informações. Por exemplo, ao publicar o exemplo deste tutorial, o próprio repositório teve que ser criado primeiro, caso em que a opção **Enviar por Push para o Repositório Remoto** foi usada com a URL do repositório.

    ![Janela do Team Explorer para efetuar push para um repositório remoto existente](media/django/step01-push-to-github.png)

    Se você não tiver um repositório, as opções **Publicar no GitHub** e **Enviar por Push para o Azure DevOps** permitirão criar um repositório diretamente no Visual Studio.

1. Ao trabalhar com este tutorial, adquira o hábito de usar periodicamente os controles no Visual Studio para confirmar e enviar alterações por push. Este tutorial envia-lhe lembretes nos pontos apropriados.

> [!Tip]
> Para navegar rapidamente no **Team Explorer**, selecione o cabeçalho (que indica **Alterações** ou **Efetuar Push** nas imagens acima) para ver um menu pop-up das páginas disponíveis.

### <a name="question-what-are-some-advantages-of-using-source-control-from-the-beginning-of-a-project"></a>Pergunta: Quais são algumas vantagens de usar o controle do código-fonte a partir do início de um projeto?

Resposta: Em primeiro lugar, se você usar o controle do código-fonte desde o início, especialmente se também usar um repositório remoto, terá um backup regular em um local fora do projeto. Em vez de manter um projeto apenas em um sistema de arquivos local, o controle do código-fonte também oferece um histórico de alterações completo e facilita a reversão de um único arquivo ou todo o projeto para um estado anterior. O histórico de alterações ajuda a determinar a causa das regressões (falhas de teste). Além disso, o controle do código-fonte é essencial se várias pessoas estiverem trabalhando em um projeto, pois ele gerencia substituições e fornece a resolução de conflitos. Por fim, o controle do código-fonte, que é basicamente uma forma de automação, deixa você preparado para automatizar o gerenciamento de compilações, testes e versões. Esse recurso realmente representa o primeiro passo no uso de DevOps em um projeto e, como os obstáculos para entrar são muito baixos, realmente não há motivos para não usar o controle do código-fonte desde o início.

Para uma discussão mais aprofundada sobre o controle do código-fonte usado como automação, confira [A origem da verdade: a função dos repositórios no DevOps](https://msdn.microsoft.com/magazine/mt763232), um artigo da MSDN Magazine destinado a aplicativos móveis, mas que também se aplica a aplicativos Web.

### <a name="question-can-i-prevent-visual-studio-from-auto-committing-a-new-project"></a>Pergunta: É possível evitar que o Visual Studio confirme automaticamente um novo projeto?

Resposta: Sim. Para desabilitar a confirmação automática, vá para a página **Configurações** no **Team Explorer**, escolha **Git** > **Configurações Globais**, desmarque o opção rotulada como **Confirmar alterações após mesclagem por padrão** e, em seguida, escolha **Atualizar**.

## <a name="step-1-3-create-the-virtual-environment-and-exclude-it-from-source-control"></a>Etapa 1-3: Criar o ambiente virtual e excluí-lo do controle do código-fonte

Agora que você configurou o controle do código-fonte para o projeto, é possível criar o ambiente virtual que contém os pacotes necessários do Django para o projeto. Você pode usar o **Team Explorer** para excluir a pasta do ambiente do controle do código-fonte.

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse no nó **Ambientes do Python** e escolha **Adicionar Ambiente Virtual**.

    ![Comando Adicionar Ambiente Virtual no Gerenciador de Soluções](media/django/step01-add-virtual-environment-command.png)

1. Uma caixa de diálogo **Adicionar Ambiente Virtual** é exibida contendo a mensagem **Encontramos um arquivo requirements.txt.** Esta mensagem indica que o Visual Studio usa esse arquivo para configurar o ambiente virtual.

    ![Caixa de diálogo Adicionar Ambiente Virtual com a mensagem requirements.txt](media/django/step01-add-virtual-environment-found-requirements.png)

1. Escolha **Criar** para aceitar os padrões. (Se desejar, o nome do ambiente virtual pode ser alterado. Essa ação alterará apenas o nome da subpasta, mas `env` é uma convenção padrão).

1. Caso seja solicitado, concorde com os privilégios de administrador e aguarde alguns minutos enquanto o Visual Studio faz o download e instala pacotes. Para o Django isso significa expandir vários milhares de arquivos em muitas subpastas! Você pode ver o progresso na janela **Saída** no Visual Studio. Enquanto você aguarda, analise as seções de perguntas a seguir.

1. Nos controles do GIT do Visual Studio (na barra de status), selecione o indicador de alterações (mostrando **99&#42;**) que abre a página **Alterações** no **Team Explorer**.

    A criação do ambiente virtual apresentou milhares de alterações, mas nenhuma delas precisará ser incluída no controle do código-fonte já que você (ou qualquer outra pessoa que venha a clonar o projeto) poderá sempre recriar o ambiente com base em *requirements.txt*.

    Para excluir o ambiente virtual, clique com o botão direito do mouse na pasta **env** e selecione **Ignorar estes itens locais**.

    ![Como ignorar um ambiente virtual em alterações de controle do código-fonte](media/django/step01-ignore-local-items.png)

1. Depois de excluir o ambiente virtual, as únicas alterações restantes são as referentes ao arquivo de projeto e a *.gitignore*. O arquivo *.gitignore* contém uma entrada adicional para a pasta do ambiente virtual. Você pode clicar duas vezes no arquivo para ver uma comparação.

1. Digite uma mensagem de confirmação, escolha o botão **Confirmar Todos** e, se desejar, envie as confirmações por push para o repositório remoto.

### <a name="question-why-do-i-want-to-create-a-virtual-environment"></a>Pergunta: Por que criar um ambiente virtual?

Resposta: Um ambiente virtual é uma ótima maneira de isolar as dependências exatas do seu aplicativo. Esse isolamento evita conflitos em um ambiente global do Python e auxilia nos testes e na colaboração. Com o tempo, à medida que desenvolver um aplicativo, invariavelmente, você introduzirá muitos pacotes úteis do Python. Mantendo os pacotes em um ambiente virtual específico do projeto, você pode atualizar com facilidade o arquivo *requirements.txt* do projeto que descreve esse ambiente, incluído no controle do código-fonte. Quando o projeto é copiado para outros computadores, incluindo servidores de build, servidores de implantação e outros computadores de desenvolvimento, é fácil recriar o ambiente usando apenas o *requirements.txt* (é por isso que o ambiente não precisa estar no controle do código-fonte). Para obter mais informações, confira [Usar ambientes virtuais](selecting-a-python-environment-for-a-project.md#use-virtual-environments).

### <a name="question-how-do-i-remove-a-virtual-environment-thats-already-committed-to-source-control"></a>Pergunta: Como faço para remover um ambiente virtual que já está confirmado no controle do código-fonte?

Resposta: Primeiro, edite o arquivo *.gitignore* para excluir a pasta: localize a seção ao final com o comentário `# Python Tools for Visual Studio (PTVS)` e adicione uma nova linha à pasta do ambiente virtual, como `/BasicProject/env`. (Como o Visual Studio não mostra o arquivo no **Gerenciador de Soluções**, abra-o diretamente usando o comando de menu **Arquivo** > **Abrir** > **Arquivo**. Abra também o arquivo no **Team Explorer**: na página **Configurações**, selecione **Configurações do Repositório**, vá para a seção **Arquivos Ignorar e de Atributos** e, em seguida, selecione o link **Editar** ao lado de **.gitignore**.)

Em segundo lugar, abra uma janela Comando, navegue para a pasta, como *BasicProject*, que contém a pasta do ambiente virtual, como *env*, e execute `git rm -r env`. Em seguida, confirme essas alterações na linha de comando (`git commit -m 'Remove venv'`) ou confirme na página **Alterações** do **Team Explorer**.

## <a name="step-1-4-examine-the-boilerplate-code"></a>Etapa 1-4: Examinar o código de texto clichê

Após concluir a criação do projeto, analise o código do projeto do Django de texto clichê (que é novamente o mesmo gerado pelo comando `django-admin startproject <project_name>` da CLI).

1. Na raiz do projeto está *manage.py*, o utilitário administrativo de linha de comando do Django que o Visual Studio define automaticamente como o arquivo de inicialização do projeto. Execute o utilitário na linha de comando usando `python manage.py <command> [options]`. Para tarefas comuns do Django, o Visual Studio fornece comandos de menu apropriados. Clique com o botão direito do mouse no projeto no **Gerenciador de Soluções** e escolha **Python** para ver a lista. Você encontrará alguns desses comandos no decorrer deste tutorial.

    ![Comandos do Django em um menu de contexto do projeto do Python](media/django/step01-django-commands-menu.png)

2. Em seu projeto, é uma pasta com o mesmo nome do projeto. Ela contém os arquivos do projeto básico do Django:

   - *__init.py*: um arquivo vazio que informa o Python se essa pasta é um pacote do Python.
   - *wsgi.py*: um ponto de entrada para os servidores Web compatíveis com WSGI para atender ao projeto. Este arquivo normalmente fica como está, pois ele fornece os ganchos para os servidores Web de produção.
   - *settings.py*: contém as configurações do projeto do Django, que você modifica no decorrer do desenvolvimento de um aplicativo Web.
   - *urls.py*: contém um sumário do projeto do Django, que você também modifica no decorrer do desenvolvimento.

     ![Arquivos do projeto do Django no Gerenciador de Soluções](media/django/step01-django-project-in-solution-explorer.png)

3. Conforme observado anteriormente, o modelo do Visual Studio também adiciona um arquivo *requirements.txt* ao projeto especificando a dependência de pacote do Django. A presença desse arquivo é que faz com que você seja convidado a criar um ambiente virtual ao desenvolver o projeto pela primeira vez.

### <a name="question-can-visual-studio-generate-a-requirementstxt-file-from-a-virtual-environment-after-i-install-other-packages"></a>Pergunta: O Visual Studio pode gerar um arquivo requirements.txt a partir de um ambiente virtual depois de instalar outros pacotes?

Resposta: Sim. Expanda o nó **Ambientes do Python**, clique com o botão direito do mouse no ambiente virtual e escolha o comando **Gerar requirements.txt**. É recomendável usar esse comando periodicamente conforme você modifica o ambiente e confirma as alterações em *requirements.txt* no controle do código-fonte, juntamente com outras alterações de código que dependem desse ambiente. Se você configurar a integração contínua em um servidor de compilação, deverá gerar o arquivo e confirmar as alterações sempre que modificar o ambiente.

## <a name="step-1-5-run-the-empty-django-project"></a>Etapa 1-5: Executar o projeto vazio do Django

1. No Visual Studio, selecione **Depurar** > **Iniciar Depuração** (**F5**) ou use o botão **Servidor Web** na barra de ferramentas (o navegador visto pode variar):

    ![Executar o botão da barra de ferramentas do servidor Web no Visual Studio](media/django/run-web-server-toolbar-button.png)

1. Executar o servidor significa executar o comando `manage.py runserver <port>`, que inicia o servidor de desenvolvimento interno do Django. Se o Visual Studio informar **Falha ao iniciar o depurador** com uma mensagem que alerta para a ausência de um arquivo de inicialização, clique com o botão direito do mouse em **manage.py** no **Gerenciador de Soluções** e selecione **Definir como Arquivo de Inicialização**.

1. Ao iniciar o servidor, você vê uma janela do console aberta que também exibe o log do servidor. O Visual Studio abre automaticamente um navegador com a página `http://localhost:<port>`. No entanto, como o projeto do Django não tem aplicativos, o Django exibe apenas uma página padrão para confirmar que o que você tem até agora está funcionando corretamente:

    ![Modo de exibição padrão do projeto do Django](media/django/step01-first-run-success.png)

1. Quando terminar, interrompa o servidor fechando a janela do console ou usando o comando **Depurar** > **Parar Depuração** no Visual Studio.

### <a name="question-is-django-a-web-server-as-well-as-a-framework"></a>Pergunta: O Django é um servidor Web além de ser uma estrutura?

Resposta: Sim e não. O Django tem um servidor Web interno que é usado para fins de desenvolvimento. Esse servidor Web é o que é usado quando você executa o aplicativo Web localmente, por exemplo, durante a depuração no Visual Studio. Porém, quando você implanta em um host Web, o Django usa o servidor Web do host. O módulo *wsgi.py* no projeto do Django cuida da conexão com os servidores de produção.

### <a name="question-whats-the-difference-between-using-the-debug-menu-commands-and-the-server-commands-on-the-projects-python-submenu"></a>Pergunta: Qual é a diferença entre usar os comandos do menu Depuração e os comandos do servidor no submenu do Python do projeto?

Resposta: Além dos comandos do menu **Depurar** e dos botões da barra de ferramentas, você também pode iniciar o servidor usando os comandos **Python** > **Executar servidor** ou **Python** > **Executar o servidor de depuração** no menu de contexto do projeto. Os dois comandos abrem uma janela de console na qual você vê a URL local (localhost:port) do servidor em execução. Mesmo assim, abra manualmente um navegador usando essa URL já que a execução do servidor de depuração não inicia automaticamente o depurador do Visual Studio. Se desejar, você pode posteriormente anexar um depurador ao processo em execução usando o comando **Depurar** > **Anexar ao Processo**.

## <a name="next-steps"></a>Próximas etapas

Neste ponto, o projeto básico do Django não possui aplicativos. Crie um aplicativo na próxima etapa. Como você normalmente trabalha mais com aplicativos do Django do que com o projeto do Django, no momento, não será necessário saber mais sobre os arquivos de texto clichê.

> [!div class="nextstepaction"]
> [Criar um aplicativo do Django com modos de exibição e modelos de página](learn-django-in-visual-studio-step-02-create-an-app.md)

## <a name="go-deeper"></a>Aprofunde-se um pouco mais

- Código do projeto do Django: [Como gravar seu primeiro aplicativo do Django, parte 1](https://docs.djangoproject.com/en/2.0/intro/tutorial01/) (docs.djangoproject.com)
- Utilitário administrativo: [django-admin e manage.py](https://docs.djangoproject.com/en/2.0/ref/django-admin/) (docs.djangoproject.com)
- Código-fonte do tutorial no GitHub: [Microsoft/python-sample-vs-learning-django](https://github.com/Microsoft/python-sample-vs-learning-django)
