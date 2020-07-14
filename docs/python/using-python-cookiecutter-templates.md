---
title: Usar modelos do CookieCutter com o Python
description: O Visual Studio oferece suporte à extensão Cookiecutter gráfica para descobrir os modelos para o código Python e criar projetos a partir desses modelos.
ms.date: 01/28/2019
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 026953ff52f4aa5c34dd4656432fed8ef2a48580
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85535142"
---
# <a name="use-the-cookiecutter-extension"></a>Usar a extensão Cookiecutter

O [Cookiecutter](https://cookiecutter.readthedocs.io/en/latest/) fornece uma interface gráfica do usuário para descobrir modelos e opções de modelo de entrada e criar projetos e arquivos. Ele é incluído no Visual Studio 2017 e posterior e pode ser instalado separadamente em versões anteriores do Visual Studio.

O Cookiecutter exige o Python 3.3 ou posterior (32 ou 64 bits) ou o Anaconda 3 4.2 ou posterior (32 ou 64 bits). Se um interpretador do Python adequado não estiver disponível, o Visual Studio exibirá um aviso. Se você instalar um interpretador do Python enquanto o Visual Studio estiver em execução, clique no botão **página inicial** na barra de ferramentas CookieCutter para detectar o intérprete recentemente instalado. (Veja [ambientes Python](managing-python-environments-in-visual-studio.md) para obter mais informações sobre ambientes em geral.)

Depois de instalado, selecione **Exibir**  >  **CookieCutter Explorer** para abrir sua janela:

![Janela principal do Cookiecutter](media/cookiecutter-overview.png)

## <a name="cookiecutter-workflow"></a>Fluxo de trabalho do Cookiecutter

Trabalhar com o Cookiecutter é um processo que inclui procurar e selecionar um modelo, cloná-lo no computador local, configurar opções e, em seguida, criar um código com base nesse modelo, conforme descrito nas próximas seções.

### <a name="browse-templates"></a>Procurar modelos

A home page do Cookiecutter exibe uma lista de modelos a serem escolhidos, organizados nos seguintes grupos:

| Agrupar | Descrição |
| --- | --- |
| **Instalado** | Modelos que foram instalados no computador local. Quando um modelo online é usado, seu repositório é clonado automaticamente em uma subpasta de *~/.cookiecutters*. É possível excluir um modelo instalado escolhido pressionando **Delete**. |
| **Recomendadas** | Modelos carregados do feed recomendado. O feed padrão é coletado pela Microsoft. Consulte [Opções do Cookiecutter](#cookiecutter-options) abaixo para obter detalhes sobre como personalizar o feed. |
| **GitHub** | Resultados da pesquisa do GitHub para a palavra-chave cookiecutter. Os resultados do GitHub retornam paginados e, se houver mais resultados disponíveis, a opção **Carregar Mais** será exibida ao final da lista. |
| **Personalizado** | Quando uma localização personalizada é inserida na caixa de pesquisa, ela é exibida nesse grupo. É possível digitar um caminho completo para o repositório GitHub ou o caminho completo para uma pasta no disco local. |

### <a name="cloning"></a>Clonar

Ao selecionar um modelo seguido por **Avançar**, o Cookiecutter faz uma cópia local com a qual trabalhará.

Se você selecionar um modelo dos grupos **Recomendados** ou **GitHub** ou inserir uma URL personalizada na caixa de pesquisa e selecionar esse modelo, ele será clonado e instalado no computador local. Se o modelo tiver sido instalado em uma sessão anterior do Visual Studio, ele será excluído automaticamente e a última versão será clonada.

Se você selecionar um modelo do grupo **Instalados** ou inserir um caminho de pasta personalizada na caixa de pesquisa e selecionar esse modelo, o Visual Studio carregará o modelo sem cloná-lo.

> [!Important]
> Os modelos do Cookiecutter são clonados em uma única pasta *~/.cookiecutters*. Cada subpasta é nomeada de acordo com o nome do repositório Git, que não inclui o nome de usuário do GitHub. Poderão surgir conflitos se você clonar modelos diferentes com o mesmo nome que são de autores diferentes. Nesse caso, o Cookiecutter impede que você substitua o modelo existente por um modelo diferente com o mesmo nome. Para instalar o outro modelo, é necessário primeiro excluir existente.

### <a name="set-template-options"></a>Configurar opções de modelo

Depois que o modelo for instalado localmente, o Cookiecutter exibirá uma página de opções na qual é possível especificar a localização em que você deseja que o Cookiecutter gere arquivos, junto com outras opções:

![Página de opções do Cookiecutter](media/cookiecutter-template-options.png)

Cada modelo do Cookiecutter define seu próprio conjunto de opções e especifica um valor padrão para cada um (exibido como o texto sugerido em cada campo de entrada). Um valor padrão pode ser um snippet de código, geralmente, quando ele é um valor dinâmico que usa outras opções.

É possível personalizar os valores padrão de opções específicas com um arquivo de configuração do usuário. Quando a extensão Cookiecutter detecta um arquivo de configuração do usuário, ela substitui os valores padrão do modelo pelos valores padrão da configuração do usuário. Esse comportamento é abordado na seção [Configuração do usuário](https://cookiecutter.readthedocs.io/en/latest/advanced/user_config.html) da documentação do Cookiecutter.

Se o modelo especificar tarefas específicas do Visual Studio a serem executadas após a geração de código, uma opção adicional **Executar tarefas adicionais após a conclusão** será exibida, que permite recusar essas tarefas. O uso mais comum de tarefas é abrir um navegador da Web, abrir arquivos no editor, instalar dependências e assim por diante.

### <a name="create"></a>Criar

Depois de configurar as opções, selecione **Criar** para gerar o código (um aviso será exibido se a pasta de saída não estiver vazia). Se estiver familiarizado com a saída do modelo e não se incomodar em substituir arquivos, ignore o aviso. Caso contrário, selecione **Cancelar**, especifique uma pasta vazia e, em seguida, copie manualmente os arquivos criados para a pasta de saída não vazia.

Depois que os arquivos forem criados com êxito, o Cookiecutter fornecerá uma opção para abri-los no **Gerenciador de Soluções**:

![Cookiecutter mostrando o comando Gerenciador de Soluções](media/cookiecutter-files-created.png)

## <a name="cookiecutter-options"></a>Opções do Cookiecutter

As opções de CookieCutter estão disponíveis por meio de **ferramentas**  >  **Opções**  >  **CookieCutter**:

![Opções do Cookiecutter](media/cookiecutter-tools-options.png)

| Opção | Descrição |
| --- | --- |
| **URL de feed recomendada** | A localização do feed recomendado dos modelos. Pode ser uma URL ou um caminho para um arquivo local. Deixe a URL vazia para usar o feed padrão coletado pela Microsoft. O feed fornece uma lista simples de localizações de modelos, separadas por novas linhas. Para solicitar alterações ao feed coletado, faça uma solicitação pull [na fonte, no GitHub](https://github.com/Microsoft/PTVS/blob/master/Python/Product/Cookiecutter/CookiecutterFeed.txt). |
| **Mostrar Ajuda** | Controla a visibilidade da barra de informações de ajuda na parte superior da janela do Cookiecutter. |

## <a name="optimize-cookiecutter-templates-for-visual-studio"></a>Otimizar modelos do Cookiecutter para o Visual Studio

Para obter noções básicas sobre como criar um modelo do Cookiecutter, consulte a [documentação do Cookiecutter](https://cookiecutter.readthedocs.io/en/latest/first_steps.html). A extensão Cookiecutter para o Visual Studio dá suporte aos modelos criados para o Cookiecutter v1.4.

A renderização padrão de uma variável de modelo depende do tipo de dados (cadeia de caracteres ou lista):

- Cadeia de caracteres: rótulo do nome da variável, caixa de texto para inserção do valor e uma marca-d'água mostrando o valor padrão. A dica de ferramenta na caixa de texto mostra o valor padrão.
- Lista: rótulo do nome da variável e caixa de combinação para seleção de um valor. A dica de ferramenta na caixa de combinação mostra o valor padrão.

É possível melhorar essa renderização especificando metadados adicionais no arquivo *cookiecutter.json* que são específicos ao Visual Studio (e ignorados pela CLI do Cookiecutter). Todas as propriedades são opcionais:

| Propriedade | Descrição |
| --- | --- |
| Rotular | Especifica o que é exibido acima do editor para a variável, em vez do nome da variável. |
| Descrição | Especifica a dica de ferramenta que é exibida no controle de edição, em vez do valor padrão dessa variável. |
| URL | Altera o rótulo para um hiperlink, com uma dica de ferramenta que mostra a URL. Se você clicar no hiperlink, o navegador padrão do usuário será aberto nessa URL. |
| Seletor | Permite a personalização do editor para uma variável. Atualmente, há suporte para os seguintes seletores:<ul><li>`string`: caixa de texto padrão, o padrão para cadeias de caracteres.</li><li>`list`: caixa de combinação padrão, o padrão para listas.</li><li>`yesno`: caixa de combinação para escolher entre `y` e `n`, para cadeias de caracteres.</li><li>`odbcConnection`: Caixa de texto com um botão **...** que abre um diálogo de conexão de banco de dados.</li></ul> |

Exemplo:

```json
{
    "site_name": "web-app",
    "python_version": ["3.5.2", "2.7.12"],
    "use_azure": "y",

    "_visual_studio": {
        "site_name": {
            "label": "Site name",
            "description": "E.g. <site-name>.azurewebsites.net (can only contain alphanumeric characters and `-`)"
        },
        "python_version": {
            "label": "Python version",
            "description": "The version of Python to run the site on"
        },
        "use_azure" : {
            "label": "Use Azure",
            "description": "Include Azure deployment files",
            "selector": "yesno",
            "url": "https://azure.microsoft.com"
        }
    }
}
```

### <a name="run-visual-studio-tasks"></a>Executar tarefas do Visual Studio

O Cookiecutter tem um recurso chamado *Pós-gerar Ganchos*, que permite a execução do código arbitrário do Python após a geração dos arquivos. Embora seja flexível, ele não permite fácil acesso ao Visual Studio.

Por exemplo, talvez você deseje abrir um arquivo no editor do Visual Studio, em seu navegador da Web ou disparar a interface do usuário do Visual Studio que solicita que o usuário crie um ambiente virtual e instale os requisitos do pacote.

Para permitir esses cenários, o Visual Studio procura metadados estendidos em *cookiecutter.json*, que descreve os comandos a serem executados depois que o usuário abrir os arquivos gerados no **Gerenciador de Soluções** ou depois que os arquivos forem adicionados a um projeto existente. (Novamente, o usuário pode recusar a execução das tarefas desmarcando **Executar tarefas adicionais após a conclusão** nas opções de modelo.)

Exemplo:

```json
"_visual_studio_post_cmds": [
    {
        "name": "File.OpenFile",
        "args": "{{cookiecutter._output_folder_path}}\\readme.txt"
    },
    {
        "name": "Cookiecutter.ExternalWebBrowser",
        "args": "https://docs.microsoft.com"
    },
    {
        "name": "Python.InstallProjectRequirements",
        "args": "{{cookiecutter._output_folder_path}}\\dev-requirements.txt"
    }
]
```

Os comandos são especificados pelo nome e devem usar o nome não localizado (em inglês) para funcionar em instalações localizadas do Visual Studio. Você pode testar e descobrir os nomes de comando na janela de **comando** do Visual Studio.

Se desejar passar um único argumento, especifique-o como uma cadeia de caracteres, como no exemplo anterior.

Se não precisar passar um argumento, deixe-o como uma cadeia de caracteres vazia ou omita-o do JSON:

```json
"_visual_studio_post_cmds": [
    {
        "name": "View.WebBrowser"
    }
]
```

Use uma matriz para vários argumentos. Para opções, divida a opção e seu valor em argumentos separados e use a delimitação correta. Por exemplo:

```json
"_visual_studio_post_cmds": [
    {
        "name": "File.OpenFile",
        "args": [
            "{{cookiecutter._output_folder_path}}\\read me.txt",
            "/e:",
            "Source Code (text) Editor"
        ]
    }
]
```

Os argumentos podem se referir a outras variáveis do Cookiecutter. Nos exemplos acima, a variável `_output_folder_path` interna é usada para formar um caminho absoluto para os arquivos gerados.

Observe que o comando `Python.InstallProjectRequirements` apenas funciona ao adicionar arquivos a um projeto existente. Essa limitação existe porque o comando é processado pelo projeto Python no **Gerenciador de Soluções** e não há nenhum projeto para receber a mensagem no **Gerenciador de Soluções** - **Exibição de Pasta**. Esperamos remover a limitação de uma versão futura (e fornecer um melhor suporte à **exibição de pasta** em geral).

## <a name="troubleshooting"></a>Solução de problemas

### <a name="error-loading-template"></a>Erro ao carregar o modelo

Alguns modelos podem estar usando tipos de dados inválidos, como booliano, em seu *cookiecutter.json*. Reporte essas instâncias para o autor do modelo selecionando o link **Problemas** no painel de informações do modelo.

### <a name="hook-script-failed"></a>Script de gancho com falha

Alguns modelos podem usar scripts pós-geração que não são compatíveis com a interface do usuário do Cookiecutter. Por exemplo, os scripts que consultam a entrada do usuário falha devido a não ter um console de terminal.

### <a name="hook-script-not-supported-on-windows"></a>Script de gancho sem suporte no Windows

Se o pós-script for *.sh*, ele poderá não ser associado a um aplicativo no computador Windows. Você poderá ver uma caixa de diálogo do Windows solicitando que você encontre um aplicativo compatível na Windows Store.

### <a name="templates-with-known-issues"></a>Modelos com problemas conhecidos

Falhas de clone:

- **wildfish/cookiecutter-django-crud** (caractere inválido `|` no nome da subpasta)
- **cookiecutter-pyvanguard** (caractere inválido `|` no nome da subpasta)

Falhas de carregamento:

- **chrisdev/wagtail-CookieCutter-Foundation** (usa um tipo booliano em *cookiecutter.jsem*)
- **quintoandar/cookiecutter-android** (nenhuma pasta de modelos)

Falhas de execução:

- **iknite/cookiecutter-ansible-role** (pós-script de gancho exige entrada do console)
- **benregn/cookiecutter-django-ansible** (Erro Jinja)

Usa bash (não fatal):

- **openstack-dev/cookiecutter**
