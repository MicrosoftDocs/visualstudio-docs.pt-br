---
title: Modelos de aplicativo Web para Python
description: Uma visão geral dos modelos do Visual Studio para aplicativos Web escritos em Python usando as estruturas Bottle, Flask e Django, incluindo configurações de depuração e publicação no Serviço de Aplicativo do Azure.
ms.date: 10/29/2018
ms.prod: visual-studio-dev15
ms.technology: vs-python
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: douge
ms.workload:
- python
- data-science
ms.openlocfilehash: 3245cd647f5da391bb0e36afc65d867137618808
ms.sourcegitcommit: bc43970c000f07c9cc2051f1264a9742943a9755
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51349329"
---
# <a name="python-web-application-project-templates"></a>Modelos de projeto de aplicativo Web Python

O Python no Visual Studio é compatível com o desenvolvimento de projetos da Web nas estruturas Bottle, Flask e Django por meio de modelos de projeto e um inicializador de depuração que pode ser configurado para manipular várias estruturas. Esses modelos incluem um arquivo *requirements.txt* para declarar as dependências necessárias. Ao criar um projeto com base em um desses modelos, o Visual Studio solicita que você instale esses pacotes (confira [Instalar os requisitos do projeto](#install-project-requirements) mais adiante neste artigo).

Você também pode usar o modelo genérico **Projeto Web** para outras estruturas, como Pyramid. Nesse caso, nenhuma estrutura é instalada com o modelo. Em vez disso, instale os pacotes necessários no ambiente em que você está usando para o projeto (confira [Janela de ambientes do Python – guia Pacote](python-environments-window-tab-reference.md#packages-tab)).

Para obter informações de como implantar um aplicativo Web do Python no Azure, confira [Publicar no Serviço de Aplicativo do Azure](publishing-python-web-applications-to-azure-from-visual-studio.md).

## <a name="use-a-project-template"></a>Usar um modelo de projeto

Crie um projeto com base em um modelo usando **Arquivo** > **Novo** > **Projeto**. Para ver os modelos de projetos da Web, selecione **Python** > **Web** à esquerda da caixa de diálogo. Em seguida, selecione um modelo de sua escolha, fornecendo nomes para o projeto e para a solução, defina opções para um diretório da solução e para o repositório Git e selecione **OK**.

![Caixa de diálogo Novo Projeto para aplicativos Web](media/projects-new-project-dialog-web.png)

O modelo genérico de **Projeto Web**, mencionado anteriormente, fornece apenas um projeto vazio do Visual Studio sem nenhum código e nenhuma suposição diferente além de ser um projeto do Python. Para obter detalhes sobre o modelo **Serviço de Nuvem do Azure**, confira [Projetos do serviço de nuvem do Azure para o Python](python-azure-cloud-service-project-template.md).

Todos os outros modelos se baseiam nas estruturas da Web Bottle, Flask ou Django e se enquadram em três grupos gerais, conforme descrito nas seções a seguir. Os aplicativos criados por um desses modelos contêm código suficiente para executar e depurar o aplicativo localmente. Cada um deles também fornece o [objeto de aplicativo WSGI](http://www.python.org/dev/peps/pep-3333/) necessário (python.org) para uso com servidores da Web de produção.

### <a name="blank-group"></a>Grupo em branco

Todos os modelos de **Projeto Web \<estrutura> em Branco** criam um projeto com um código de texto clichê mais ou menos mínimo e as dependências necessárias declaradas em um arquivo *requirements.txt*.

| Modelo | Descrição |
| --- | --- |
| **Projeto Web em Branco do Bottle** | Gera um aplicativo mínimo em *app.py* com uma home page do `/` e uma página `/hello/<name>` que ecoa `<name>` usando um modelo de página embutido muito curto. |
| **Projeto Web em Branco do Django** | Gera um projeto Django com a estrutura do site principal do Django, mas não aplicativos Django. Para obter mais informações, confira [Modelos do Django](python-django-web-application-project-template.md) e [Etapa 1 do tutorial – Conheça o Django](learn-django-in-visual-studio-step-01-project-and-solution.md). |
| **Projeto Web em Branco do Flask** | Gera um aplicativo mínimo com um único "Olá, Mundo!" página para `/`. Este aplicativo é semelhante ao resultado das seguintes etapas detalhadas em [Início rápido: use o Visual Studio para criar seu primeiro aplicativo Web Python](../ide/quickstart-python.md?toc=/visualstudio/python/toc.json&bc=/visualstudio/python/_breadcrumb/toc.json). Confira também [Etapa 1 do tutorial – Conheça o Flask](learn-flask-visual-studio-step-01-project-solution.md).

### <a name="web-group"></a>Grupo da Web

Todos os modelos de **Projeto Web da \<Framework>** criam um aplicativo Web inicial com um design idêntico, seja qual for a estrutura escolhida. O aplicativo tem as páginas Início, Sobre e Contato, juntamente com uma barra de navegação e um design responsivo usando a Inicialização. Cada aplicativo é configurado adequadamente para fornecer arquivos estáticos (CSS, JavaScript e fontes) e usa um mecanismo de modelo de página adequado para a estrutura.

| Modelo | Descrição |
| --- | --- |
| **Projeto Web do Bottle** | Gera um aplicativo cujos arquivos estáticos estão contidos na pasta *static* e são manipulados por meio do código em *app.py*. O roteamento para as páginas individuais está contido em *routes.py*, e a pasta *views* contém os modelos de página.|
| **Projeto Web do Django** | Gera um projeto e um aplicativo do Django com três páginas, suporte de autenticação e um banco de dados SQLite (mas nenhum modelo de dados). Para obter mais informações, confira [Modelos do Django](python-django-web-application-project-template.md) e [Etapa 4 do tutorial – Conheça o Django](learn-django-in-visual-studio-step-04-full-django-project-template.md). |
| **Projeto Web do Flask** | Gera um aplicativo cujos arquivos estáticos estão contidos na pasta *static*. O código em *views.py* manipula o roteamento, com modelos de página que usam o mecanismo Jinja contido na pasta *templates*. O arquivo *runserver.py* fornece o código de inicialização. Confira [Etapa 4 do tutorial – Conheça o Flask](learn-flask-visual-studio-step-04-full-flask-project-template.md). |
| **Projeto Web do Flask/Jade** | Gera o mesmo aplicativo que com o modelo **Projeto Web do Flask**, mas usando a extensão do Jade para o mecanismo de modelagem do Jinja. |

### <a name="polls-group"></a>Grupo de pesquisas

Os modelos **Votações do Projeto Web da \<estrutura>** criam um aplicativo Web inicial por meio do qual os usuários podem votar em diferentes perguntas da votação. Cada aplicativo é criado com base na estrutura dos modelos de projeto **Web** para usarem um banco de dados, a fim de gerenciar as votações e as respostas do usuário. Os aplicativos incluem modelos de dados adequados e uma página de aplicativo especial (/seed) que carrega votações de um arquivo *samples.json*.

| Modelo | Descrição |
| --- | --- |
| **Projeto Web de Votações do Bottle** | Gera um aplicativo que pode ser executado em um banco de dados em memória, no MongoDB ou no Armazenamento de Tabelas do Azure, configurado usando a variável de ambiente do `REPOSITORY_NAME`. Os modelos de dados e o código do armazenamento de dados estão contidos na pasta *models*, e o arquivo *settings.py* contém o código para determinar qual armazenamento de dados é usado. |
| **Projeto Web de Votações do Django** | Gera um projeto e um aplicativo do Django com três páginas e um banco de dados SQLite. Inclui personalizações na interface administrativa do Django para permitir que um administrador autenticado crie e gerencie pesquisas. Para obter mais informações, confira [Modelos do Django](python-django-web-application-project-template.md) e [Etapa 6 do tutorial – Conheça o Django](learn-django-in-visual-studio-step-06-polls-django-web-project-template.md). |
| **Projeto Web de Votações do Flask** | Gera um aplicativo que pode ser executado em um banco de dados em memória, no MongoDB ou no Armazenamento de Tabelas do Azure, configurado usando a variável de ambiente do `REPOSITORY_NAME`. Os modelos de dados e o código do armazenamento de dados estão contidos na pasta *models*, e o arquivo *settings.py* contém o código para determinar qual armazenamento de dados é usado. O aplicativo usa o mecanismo Jinja para modelos de página. Confira [Etapa 5 do tutorial – Conheça o Flask](learn-flask-visual-studio-step-05-polls-flask-web-project-template.md). |
| **Projeto Web de Votações do Flask/Jade** | Gera o mesmo aplicativo que com o modelo **Projeto Web de Votações do Flask**, mas usando a extensão do Jade para o mecanismo de modelagem do Jinja. |

## <a name="install-project-requirements"></a>Instalar requisitos de projeto

Ao criar um projeto com base em um modelo específico à estrutura, uma caixa de diálogo é exibida para ajudá-lo a instalar os pacotes necessários usando o PIP. Também recomendamos o uso de um [ambiente virtual](selecting-a-python-environment-for-a-project.md#use-virtual-environments) para projetos Web, para que as dependências corretas sejam incluídas durante a publicação do site:

![Caixa de diálogo que instala os pacotes necessários para um modelo de projeto](media/template-web-requirements-txt-wizard.png)

Se estiver usando o controle do código-fonte, normalmente, você omitirá a pasta de ambiente virtual, pois esse ambiente poderá ser recriado usando apenas o *requirements.txt*. A melhor maneira de excluir a pasta é primeiro selecionar **Eu os instalarei sozinho** no prompt mostrado acima. Em seguida, desabilite a confirmação automática antes de criar o ambiente virtual. Para obter detalhes, confira [Tutorial – Conheça o Django – Etapas 1-2 e 1-3](learn-django-in-visual-studio-step-01-project-and-solution.md#step-1-2-examine-the-git-controls-and-publish-to-a-remote-repository) e [Tutorial – Conheça o Flask – Etapas 1-2 e 1-3](learn-flask-visual-studio-step-01-project-solution.md#step-1-2-examine-the-git-controls-and-publish-to-a-remote-repository).

Ao implantar o Serviço de Aplicativo do Microsoft Azure, selecione uma versão do Python como uma [extensão de site](https://aka.ms/PythonOnAppService) e instalar os pacotes manualmente. Além disso, como o Serviço de Aplicativo do Azure **não** instala pacotes automaticamente de um arquivo *requirements.txt* quando implantado por meio do Visual Studio, siga os detalhes de configuração em [aka.ms/PythonOnAppService](https://aka.ms/PythonOnAppService).

Os Serviços de Nuvem do Microsoft Azure *dão* suporte ao arquivo *requirements.txt*. Consulte [Azure cloud service projects](python-azure-cloud-service-project-template.md) (Projetos do Serviço de Nuvem do Azure) para obter detalhes.

## <a name="debugging"></a>Depuração

Quando um projeto Web é iniciado para depuração, o Visual Studio inicia um servidor Web local em uma porta aleatória e abre seu navegador padrão para esse endereço e porta. Para especificar opções adicionais, clique com o botão direito do mouse no projeto, selecione **Propriedades** e selecione a guia **Inicializador da Web**:

![Propriedades do inicializador da Web para o modelo da Web genérico](media/template-web-launcher-properties.png)

No grupo **Depurar**:

- **Caminhos de Pesquisa**, **Argumentos de Script**, **Argumentos do Interpretador** e **Caminho do Interpretador**: essas opções são as mesmas da [depuração normal](debugging-python-in-visual-studio.md).
- **URL de Inicialização**: especifica a URL que é aberta no navegador. Usa como padrão `localhost`.
- **Número da Porta**: a porta a ser usada se nenhuma for especificada na URL (o Visual Studio seleciona uma automaticamente por padrão). Essa configuração permite substituir o valor padrão da variável de ambiente `SERVER_PORT`, que é usada pelos modelos para configurar a porta na qual o servidor de depuração local escuta.

As propriedades dos grupos **Executar Comando do Servidor** e **Depurar Comando do Servidor** (o último está abaixo do que é mostrado na imagem) determinam como o servidor Web é iniciado. Como muitas estruturas exigem o uso de um script fora do projeto atual, o script pode ser configurado aqui e o nome do módulo de inicialização pode ser passado como um parâmetro.

- **Comando**: pode ser um script do Python (arquivo *\*.py*), um nome de módulo (como em `python.exe -m module_name`) ou uma linha de código individual (como em `python.exe -c "code"`). O valor na lista suspensa indica qual desses tipos é pretendido.
- **Argumentos**: esses argumentos são passados na linha de comando após o comando.
- **Ambiente**: uma lista separada por nova linha de pares \<NAME>=\<VALUE> que especificam as variáveis de ambiente. Essas variáveis são definidas após todas as propriedades que podem modificar o ambiente, como o número da porta e os caminhos de pesquisa e, portanto, podem substituir esses valores.

Qualquer propriedade de projeto ou variável de ambiente pode ser especificada com a sintaxe do MSBuild, por exemplo: `$(StartupFile) --port $(SERVER_PORT)`.
`$(StartupFile)` é o caminho relativo para o arquivo de inicialização e `{StartupModule}` é o nome importável do arquivo de inicialização. `$(SERVER_HOST)` e `$(SERVER_PORT)` são variáveis de ambiente normais definidas pelas propriedades **URL de Inicialização** e **Número da Porta**, automaticamente ou pela propriedade **Ambiente**.

> [!Note]
> Os valores em **Executar Comando do Servidor** são usados com o comando **Depurar** > **Iniciar Servidor** ou **Ctrl**+**F5**; os valores no grupo **Depurar Comando do Servidor** são usados com o comando **Depurar** > **Iniciar Servidor de Depuração** ou **F5**.

### <a name="sample-bottle-configuration"></a>Configuração do Bottle de exemplo

O modelo de **Projeto Web Bottle** inclui um código de texto clichê que faz a configuração necessária. Um aplicativo importado do Bottle pode não incluir esse código; no entanto, nesse caso, as seguintes configurações iniciam o aplicativo usando o módulo `bottle` instalado:

- Grupo **Executar Comando do Servidor**:
  - **Comando**: `bottle` (módulo)
  - **Argumentos**: `--bind=%SERVER_HOST%:%SERVER_PORT% {StartupModule}:app`

- Grupo **Depurar Comando do Servidor**:
  - **Comando**: `bottle` (módulo)
  - **Argumentos** `--debug --bind=%SERVER_HOST%:%SERVER_PORT% {StartupModule}:app`

A opção `--reload` não é recomendada ao usar o Visual Studio para depuração.

### <a name="sample-pyramid-configuration"></a>Configuração de exemplo do Pyramid

Atualmente, a melhor forma de criar aplicativos do Pyramid é usando a ferramenta de linha de comando `pcreate`. Depois que um aplicativo for criado, ele poderá ser importado usando o modelo [**Com base em um código existente do Python**](managing-python-projects-in-visual-studio.md#create-a-project-from-existing-files). Depois de fazer isso, selecione a personalização **Projeto Web Genérico** para configurar as opções. Essas configurações presumem que o Pyramid está instalado em um ambiente virtual em `..\env`.

- Grupo **Depurar**:
  - **Porta do Servidor**: 6543 (ou o que estiver configurado nos arquivos *.ini*)

- Grupo **Executar Comando do Servidor**:
  - Comando: `..\env\scripts\pserve-script.py` (script)
  - Argumentos: `Production.ini`

- Grupo **Depurar Comando do Servidor**:
  - Comando: `..\env\scripts\pserve-script.py` (script)
  - Argumentos: `Development.ini`

> [!Tip]
> Provavelmente, será necessário configurar a propriedade **Diretório de Trabalho** do projeto, pois os aplicativos do Pyramid estão normalmente uma pasta abaixo da raiz do projeto.

### <a name="other-configurations"></a>Outras configurações

Se você tiver configurações para outra estrutura que gostaria de compartilhar ou se gostaria de solicitar configurações para outra estrutura, abra um [problema no GitHub](https://github.com/Microsoft/PTVS/issues).

## <a name="convert-a-project-to-azure-cloud-service"></a>Converter um projeto no Serviço de Nuvem do Azure

O comando **Converter em Projeto do Serviço de Nuvem do Microsoft Azure** (imagem abaixo) adiciona um projeto do Serviço de Nuvem à solução. Esse projeto inclui as configurações de implantação e a configuração das máquinas virtuais e dos serviços a serem usadas. Use o comando **Publicar** no projeto de nuvem para implantar nos Serviços de Nuvem, o comando **Publicar** no projeto do Python ainda implanta em Sites. Para obter mais informações, confira [Projetos do serviço de nuvem do Azure](python-azure-cloud-service-project-template.md).

![Comando Converter em projeto do serviço de nuvem do Microsoft Azure](media/template-web-convert-menu.png)

## <a name="see-also"></a>Consulte também

- [Referência de modelos de item do Python](python-item-templates.md)
- [Publicar no Serviço de Aplicativo do Azure](publishing-python-web-applications-to-azure-from-visual-studio.md)
