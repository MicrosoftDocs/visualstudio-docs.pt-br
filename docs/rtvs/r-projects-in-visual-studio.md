---
title: Projetos R
description: Como criar um gerenciador de projetos de R no Visual Studio, incluindo propriedades, comandos de projeto e modelos.
ms.date: 06/29/2017
ms.prod: visual-studio-dev15
ms.technology: vs-rtvs
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: douge
ms.workload:
- data-science
ms.openlocfilehash: 154243351f3ff3e7babc502c2cf96dea6bcf5bf0
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49813825"
---
# <a name="create-r-projects-in-visual-studio"></a>Criar projetos do R no Visual Studio

Um projeto do R (um arquivo *.rxproj*) identifica todos os arquivos de código-fonte e de conteúdo associados a ele. Ele também contém informações de build de cada arquivo, mantém as informações para integração com sistemas de controle do código-fonte e ajuda a organizar o aplicativo em componentes lógicos. As informações relacionadas ao workspace, como a lista de pacotes instalados, no entanto, são mantidas separadamente no próprio workspace.

Os projetos são sempre gerenciados em uma *solução* do Visual Studio, que pode conter vários projetos que podem fazer referências entre si. Consulte [Usar vários tipos de projeto no Visual Studio](#use-multiple-project-types-in-visual-studio).

## <a name="creating-a-new-r-project"></a>Criando um novo projeto R

1. Inicie o Visual Studio.
1. Escolha **Arquivo > Novo > Projeto...** (**Ctrl**+**Shift**+**N**)
1. Selecione "Projeto R" em **Modelos > R**, dê ao projeto um nome e um local e selecione **OK**:

    ![Caixa de diálogo Novo Projeto para R no Visual Studio (RTVS no VS2017)](media/getting-started-01-new-project.png)

Esse comando cria um projeto com um arquivo *script.R* vazio aberto no editor. Observe também no **Gerenciador de Soluções** que há outros dois arquivos no projeto:

![Conteúdo de um projeto R criado usando um modelo](media/projects-template-results.png)

O *.Rhistory* registra todos os comandos que você insere na janela [R Interativo](interactive-repl-for-r-in-visual-studio.md). Você pode abrir uma janela de histórico dedicada com o comando **Ferramentas do R** > **Janelas** > **Histórico**. Essa janela tem um botão de barra de ferramentas e itens do menu de contexto para limpar o conteúdo do histórico.

O arquivo *rproject.rproj* mantém determinadas configurações do projeto específicas do R que não são gerenciadas pelo Visual Studio de nenhum outro modo:

| Propriedade | Padrão | Descrição |
| --- | --- | --- |
| Versão | 1.0 | A versão das Ferramentas do R para Visual Studio usadas para criar o projeto. |
| RestoreWorkspace | Padrão | Carregar automaticamente as variáveis do Workspace anteriores do arquivo `.RData` no diretório do projeto. |
| SaveWorkspace | Padrão | Salvar as variáveis de workspace atual no arquivo `.RData` no diretório do projeto ao fechar um projeto. |
| AlwaysSaveHistory | Padrão | Salvar o histórico da janela interativa atual no arquivo `.RHistory` no diretório do projeto ao fechar um projeto. |
| EnableCodeIndexing | Sim | Determina se deseja executar uma tarefa de indexação em segundo plano para acelerar as pesquisas de código. |
| UseSpacesForTab | Sim | Determina se deseja inserir espaços (Sim) ou um caractere de tabulação (Não) quando a tecla **Tab** é pressionada no editor. |
| NumSpacesForTab | 2 | O número de espaços a serem inseridos se UseSpacesForTab for Sim. |
| Codificando | UTF-8 | A codificação padrão para arquivos `.R`. |
| RnwWeave | Sweave | Pacote a ser usado ao introduzir um arquivo Rnw. |
| LaTeX | pdfLaTeX | Biblioteca a ser usada ao converter RMarkdwon em PDF. |

### <a name="converting-a-folder-of-files-to-an-r-project"></a>Converter uma pasta de arquivos em um projeto R

Se você tem uma pasta existente de arquivos *.R* que deseja gerenciar em um projeto, siga as etapas a seguir:

1. Crie um novo projeto no Visual Studio como na seção anterior.
1. Copie os arquivos para a pasta do projeto.
1. No Gerenciador de Soluções do Visual Studio, clique com o botão direito do mouse no projeto, selecione **Adicionar** > **Item Existente** e navegue até os arquivos que deseja adicionar. Esses arquivos aparecem na árvore do projeto depois de selecionar **OK**.
1. Para organizar o código em subpastas, clique com o botão direito do mouse no projeto, selecione **Adicionar** > **Nova Pasta** e, em seguida, copie os arquivos nessa pasta e adicione os itens existentes da etapa 3.

## <a name="project-properties"></a>Propriedades de projeto

Para abrir as páginas de propriedades do projeto, clique com o botão direito do mouse no projeto no **Gerenciador de Soluções** e selecione **Propriedades** ou clique no item de menu **Projeto > Propriedades do (nome do projeto)*. A janela aberta exibe propriedades do projeto:


| Tabulação | Propriedade | Descrição | 
| --- | --- | --- | 
| Executar | Arquivo de inicialização | O nome do arquivo que é executado com o comando **Arquivo de inicialização de origem**, **F5**, **Depurar** > **Iniciar depuração** ou **Depurar** > **Iniciar sem depuração**. Clicar com o botão direito do mouse no arquivo no projeto e selecionar **Definir como script de inicialização do R** também o define como o arquivo de inicialização. | 
| | Redefinir R Interativo em execução | Limpa todas as variáveis de workspace da janela interativa ao executar o projeto. Isso garante que não haja nenhum conteúdo no workspace que restou das execuções anteriores. | 
| | Caminho do projeto remoto | Caminho para um workspace remoto. | 
| | Transferir arquivos em execução | Indica se os arquivos do projeto, sujeitos ao filtro em **Arquivos para transferir**, devem ser copiados para um workspace remoto com cada execução. | 
| | Arquivos para transferir | Nomes de arquivo e curingas que indicam os arquivos específicos para copiar em um workspace remoto se **Transferir arquivos em execução** estiver selecionado. | 
| Configurações | (Arquivo Settings.R) | As configurações do projeto do R vêm dos arquivos *Settings.R* ou **.Settings.R* que estão localizados dentro do projeto. Se não houver nenhum arquivo de configurações, você poderá adicionar variáveis e salvar a página e, em seguida, um arquivo padrão *Settings.R* será criado para você. Também é possível adicionar o arquivo de configurações ao projeto por meio do comando de menu **Arquivo** > **Adicionar Novo Item**. <br/> As configurações são armazenadas como código R e o arquivo pode ser obtido antes da execução de outros módulos, portanto, pré-populando o ambiente com configurações predefinidas. | 

## <a name="r-specific-project-commands"></a>Comandos de projeto específico do R

Os projetos do Visual Studio dão suporte a vários comandos gerais por meio do menu acionado por clique com o botão direito do mouse e o menu **Projeto**. Para obter detalhes sobre esses recursos gerais, confira [Soluções e projetos no Visual Studio](../ide/solutions-and-projects-in-visual-studio.md). No entanto, tenha em mente que as RTVS (Ferramentas do R para Visual Studio) adicionam vários comandos próprios ao menu acionado por clique com o botão direito do mouse nos projetos do R e também arquivos e pastas dentro do projeto.

| Comando | Descrição |
| --- | --- |
| Definir diretório de trabalho aqui | Define o diretório de trabalho da janela do R Interativo para a pasta do projeto, que também pode ser usado em qualquer subpasta dentro de um projeto. |
| Abrir pasta que contém | Abre o Windows Explorer no local do arquivo selecionado. |
| Adicionar script R | Cria e abre um arquivo *.R* com um nome padrão. Você também pode usar o comando **Adicionar** > **Novo Item** para criar arquivos *.R*, além de vários outros tipos de arquivo. Consulte [Modelos de item específicos do R](#r-specific-item-templates). |
| Adicionar R Markdown | Cria e abre um documento *.rmd* com um nome padrão. Você também pode usar o comando **Adicionar** > **Novo Item** para criar arquivos *.rmd*, além de vários outros tipos de arquivo. Consulte [Modelos de item específicos do R](#r-specific-item-templates).  |
| Publicar procedimentos armazenados | Inicia um processo para publicar todos os procedimentos armazenados contidos em scripts R. Veja [Trabalhar com procedimentos armazenados do SQL Server](integrating-sql-server-with-r.md#work-with-sql-server-stored-procedures). | 

## <a name="r-specific-item-templates"></a>Modelos de item específicos do R

As RTVS incluem vários modelos para tipos de arquivo específicos. Você pode acessar os modelos clicando com o botão direito do mouse em um projeto do R e selecionando **Adicionar** > **Novo Item**, selecionando **Projeto** > **Adicionar Novo Item** ou usando **Arquivo** > **Novo** > **Arquivo** e selecionando a guia **R**. A melhor maneira de explorar um modelo é criar um novo projeto e inserir arquivos de cada tipo.

> [!Note]
> Os comandos **Adicionar** > **Novo Item** também exibem tipos de arquivos gerais que não estão listados na tabela. Com **Arquivo** > **Novo** > **Arquivo** esses tipos estão contidos na guia **Geral**.

| Tipo de arquivo | Descrição |
| --- | --- |
| Script R | Um arquivo de texto que contém os mesmos comandos que podem ser inseridos na linha de comando R. |
| R Markdown | Um arquivo contendo um documento [R Markdown](rmarkdown-with-r-in-visual-studio.md). |
| Configurações do R | Um arquivo que contém as configurações do aplicativo R. | 
| Documentação do R | Um arquivo de documentação do R genérico que contém apenas os campos nome, alias e título. |
| Documentação do R (função) | Um arquivo de documentação do R que contém vários campos com comentários para descrever uma função. |
| Documentação do R (conjunto de dados) | Um arquivo de documentação do R que contém vários campos com comentários para descrever um conjunto de dados. |
| Consulta SQL | E um arquivo *.sql* vazio. Veja [Trabalhar com o SQL Server e R](integrating-sql-server-with-r.md). |
| Procedimento armazenado com R | Um arquivo R com uma consulta SQL filho e um arquivo de modelo de procedimento armazenado filho. Veja [Trabalhar com o SQL Server e R](integrating-sql-server-with-r.md). |

## <a name="use-multiple-project-types-in-visual-studio"></a>Usar vários tipos de projeto no Visual Studio

As soluções do Visual Studio fornecem um local conveniente para reunir e gerenciar projetos relacionados em um único lugar lógico. As soluções ajudam você a manter seu código organizado e facilita a colaboração entre equipes.

No exemplo abaixo, a solução contém um projeto R com um modelo criado usando R e Azure Machine Learning, um projeto Python/scikit-learn, um projeto C++ que contém módulos para trabalho com uso intensivo de computação, um projeto SQL para gerenciamento de dados e um projeto Python/Bottle para o site da web que publica o resultado:

![Gerenciador de Soluções do Visual Studio mostrando vários projetos relacionados em uma solução](media/projects-polyglot.png)

O projeto realçado em negrito é o projeto de "inicialização" da solução. Para alterá-lo, clique com o botão direito do mouse em um projeto diferente e selecione **Definir como projeto de inicialização**.

> [!Note]
> No momento, não há nenhum R explícito para integração com a linguagem C#/C++ em vigor (como há para Python, confira [Criar uma extensão do C++ para Python](../python/working-with-c-cpp-python-in-visual-studio.md)).  No entanto, há bibliotecas disponíveis que fornecem o pontes de C# e C++ para R.

Para obter mais informações de como gerenciar projetos e soluções em geral, confira [Soluções e projetos no Visual Studio](../ide/solutions-and-projects-in-visual-studio.md).
