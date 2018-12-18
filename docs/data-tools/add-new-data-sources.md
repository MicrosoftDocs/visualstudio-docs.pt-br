---
title: Adicionar novas fontes de dados
ms.date: 11/21/2018
ms.topic: conceptual
f1_keywords:
- vs.datasource.datasourcefieldspicker
helpviewer_keywords:
- data [Visual Studio], data sources
- data sources
ms.assetid: ed28c625-bb89-4037-bfde-cfa435d182a2
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: fe32424632d06ed637b41dcd3d4b614afde369bd
ms.sourcegitcommit: 81e9d90843ead658bc73b30c869f25921d99e116
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2018
ms.locfileid: "52304604"
---
# <a name="add-new-data-sources"></a>Adicionar novas fontes de dados

No contexto das ferramentas de dados do .NET no Visual Studio, o termo *fonte de dados* refere-se aos objetos .NET que se conectam a um armazenamento de dados e disponibilizar os dados a um aplicativo .NET. Os designers do Visual Studio podem consumir a saída da fonte de dados para gerar o código clichê que associa os dados a formas quando você arrasta e solta os objetos de banco de dados a partir de **fontes de dados** janela. Esse tipo de fonte de dados pode ser:

- Uma classe em um modelo do Entity Framework que está associado a algum tipo de banco de dados.

- Um conjunto de dados que está associado a algum tipo de banco de dados.

- Uma classe que representa um serviço de rede como um serviço de dados do Windows Communication Foundation (WCF) ou um serviço REST.

- Uma classe que representa um serviço do SharePoint.

- Uma classe ou uma coleção em sua solução.

> [!NOTE]
> Se você não estiver usando recursos de vinculação de dados, conjuntos de dados, o Entity Framework, LINQ to SQL, WCF ou o SharePoint, o conceito de uma "fonte de dados" não se aplica. Basta conectar-se diretamente ao banco de dados usando os objetos SQLCommand e se comunicar diretamente com o banco de dados.

Você cria e edita fontes de dados usando o **Data Source Configuration Wizard** em um aplicativo Windows Forms ou Windows Presentation Foundation. Para o Entity Framework, primeiro crie as classes de entidade e, em seguida, iniciar o assistente, selecionando **Project** > **Add New Data Source** (descrito mais detalhadamente neste artigo).

![Assistente para Configuração da Fonte de Dados](../data-tools/media/data-source-configuration-wizard.png)

## <a name="data-sources-window"></a>janela Fontes de Dados

Depois de criar uma fonte de dados, ele aparece na **fontes de dados** janela da ferramenta.

> [!TIP]
> Para abrir o **fontes de dados** , verifique se seu projeto está aberto e, em seguida, pressione **Shift**+**Alt**+**1!d**ou escolha **modo de exibição** > **Other Windows** > **fontes de dados**.

Você pode arrastar uma fonte de dados do **fontes de dados** window em uma superfície de design do formulário ou controle. Isso faz com que o código clichê a ser gerado que exibe os dados do armazenamento de dados.

A ilustração a seguir mostra um conjunto de dados foi descartado em um formulário do Windows. Se você selecionar **F5** no aplicativo, os dados do banco de dados subjacente é exibida nos controles do formulário.

![Operação de arrastar do código-fonte de dados](../data-tools/media/raddata-data-source-drag-operation.png)

## <a name="data-source-for-a-database-or-a-database-file"></a>Fonte de dados para um banco de dados ou um arquivo de banco de dados

Você pode criar um conjunto de dados ou um modelo do Entity Framework para usar como uma fonte de dados para um banco de dados ou arquivo de banco de dados.

### <a name="dataset"></a>Conjunto de dados

Para criar um conjunto de dados como uma fonte de dados, execute as **Data Source Configuration Wizard** selecionando **Project** > **Add New Data Source**. Escolha o **banco de dados** fonte de dados de tipo e siga os prompts para especificar uma conexão de banco de dados novo ou existente, ou um arquivo de banco de dados.

### <a name="entity-classes"></a>Classes de entidade

Para criar um modelo do Entity Framework como uma fonte de dados:

1. Execute o **Assistente de modelo de dados de entidade** para criar as classes de entidade. Selecione **Project** > **Adicionar Novo Item** > **modelo de dados de entidade ADO.NET**.

   ![Novo item de projeto de modelo do Entity Framework](../data-tools/media/raddata-new-entity-framework-model-project-item.png)

1. Escolha o método que você deseja gerar o modelo por.

   ![Assistente de modelo de dados de entidade](../data-tools/media/raddata-entity-data-model-wizard.png)

1. Adicione o modelo como uma fonte de dados. As classes geradas aparecem na **Data Source Configuration Wizard** quando você escolhe a **objetos** categoria.

   ![Assistente de configuração de fonte de dados com Classes de entidade](../data-tools/media/raddata-data-source-configuration-wizard-with-entity-classes.png)

## <a name="data-source-for-a-service"></a>Fonte de dados para um serviço

Para criar uma fonte de dados de um serviço, execute as **Data Source Configuration Wizard** e escolha o **Service** tipo de fonte de dados. Isso é apenas um atalho para o **adicionar referência de serviço** caixa de diálogo, você também pode acessar clicando com o projeto no **Gerenciador de soluções** e selecionando **adicionar referência de serviço**.

Quando você cria uma fonte de dados de um serviço, o Visual Studio adiciona uma referência de serviço ao seu projeto. Visual Studio também cria objetos de proxy que correspondem aos objetos que o serviço retorna. Por exemplo, um serviço que retorna um conjunto de dados é representado no seu projeto como um conjunto de dados; um serviço que retorna que um tipo específico é representado no seu projeto como o tipo retornado.

Você pode criar uma fonte de dados entre os seguintes tipos de serviços:

- [WCF Data Services](/dotnet/framework/data/wcf/wcf-data-services-overview)

- [WCF services](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)

- Serviços da Web

    > [!NOTE]
    > Os itens que aparecem na **fontes de dados** janela são dependentes dos dados que o serviço retorna. Alguns serviços podem não fornecer informações suficientes para o **Assistente de Configuração de Fonte de Dados** criar objetos associáveis. Por exemplo, se o serviço retorna um conjunto de dados não tipado, nenhum item aparecerá na **fontes de dados** janela quando você concluir o assistente. Isso ocorre porque os conjuntos de dados não tipados não fornecem um esquema e, portanto, o assistente não tem informações suficientes para criar a fonte de dados.

## <a name="data-source-for-an-object"></a>Fonte de dados para um objeto

Você pode criar uma fonte de dados de qualquer objeto que expõe uma ou mais propriedades públicas executando o **Data Source Configuration Wizard** e, em seguida, selecionando a **objeto** tipo de fonte de dados. Todas as propriedades públicas de um objeto são exibidas na **fontes de dados** janela. Se você estiver usando o Entity Framework e gerou um modelo, isso é onde você pode encontrar as classes de entidade que são as fontes de dados para seu aplicativo.

Sobre o **selecione os objetos de dados** página, expanda os nós na exibição de árvore para localizar os objetos que você deseja associar a. O modo de exibição de árvore contém nós de seu projeto e para assemblies e outros projetos que são referenciados pelo seu projeto.

Se você deseja associar a um objeto em um assembly ou projeto que não aparece na exibição de árvore, clique em **adicionar referência** e usar o **caixa de diálogo Adicionar referência** para adicionar uma referência ao assembly ou projeto. Depois de adicionar a referência, o assembly ou projeto é adicionado à exibição em árvore.

> [!NOTE]
> Você precisará criar o projeto que contém os objetos antes dos objetos aparecem na exibição de árvore.

> [!NOTE]
> Para dar suporte à vinculação de dados de arrastar e soltar, objetos que implementam o <xref:System.ComponentModel.ITypedList> ou <xref:System.ComponentModel.IListSource> interface deve ter um construtor padrão. Caso contrário, o Visual Studio não é possível instanciar o objeto de fonte de dados, e ele exibirá um erro quando você arrasta o item para a superfície de design.

## <a name="data-source-for-a-sharepoint-list"></a>Fonte de dados para uma lista do SharePoint

Você pode criar uma fonte de dados de uma lista do SharePoint, executando o **Data Source Configuration Wizard** e selecionando o **SharePoint** tipo de fonte de dados. SharePoint expõe os dados por meio do WCF Data Services, portanto, criando uma fonte de dados do SharePoint é o mesmo que criar uma fonte de dados de um serviço. Selecionando o **SharePoint** item o **Data Source Configuration Wizard** abre o **Add Service Reference** caixa de diálogo, em que você se conectar ao serviço de dados do SharePoint Por que aponta para o servidor do SharePoint. Isso requer o SDK do SharePoint.

## <a name="see-also"></a>Consulte também

- [Ferramentas de dados do Visual Studio para .NET](../data-tools/visual-studio-data-tools-for-dotnet.md)