---
title: Ferramentas do conjunto de dados
ms.date: 11/21/2018
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.topic: conceptual
f1_keywords:
- vs.data.DataSet
helpviewer_keywords:
- untyped datasets
- datasets [Visual Basic], extended properties
- typed datasets
- current record in dataset
- XML [Visual Basic], datasets
- DataSet class, about datasets
- unique constraints (datasets)
- data relationships
- parent records in datasets
- extended properties, in typed datasets
- datasets [Visual Basic]
- schemas [Visual Basic], datasets
- datasets [Visual Basic], msprop
- master-detail tables, datasets
- databases [Visual Basic], updating
- msprop
- foreign keys, datasets
- DataSet class
- datasets [Visual Basic], filling
- case sensitivity, datasets
- constraints [Visual Basic], datasets
- child records
- related tables, datasets
- updating datasets, about dataset updates
- data caching, datasets
- DataRelation object, datasets
- untyped datasets, compared to typed datasets
- cache [Visual Studio], datasets
- datasets [Visual Basic], relationships
- related tables
- XML schemas, about XML schemas and datasets
- relationships, datasets
- typed datasets, compared to untyped datasets
- datasets [Visual Basic], populating
- datasets [Visual Basic], namespace
- data adapters, populating datasets
ms.assetid: ee57f4f6-9fe1-4e0a-be9a-955c486ff427
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- data-storage
ms.openlocfilehash: 3a8a1ac0f2ac4e4b147fbe11dba8d88ccea4c255
ms.sourcegitcommit: 81e9d90843ead658bc73b30c869f25921d99e116
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2018
ms.locfileid: "52304981"
---
# <a name="dataset-tools-in-visual-studio"></a>Ferramentas de conjunto de dados no Visual Studio

> [!NOTE]
> Conjuntos de dados e classes relacionadas são herdadas tecnologias do .NET do início dos anos 2000 que habilitam aplicativos para trabalhar com dados na memória enquanto os aplicativos estão desconectados do banco de dados. Eles são especialmente úteis para aplicativos que permitem aos usuários modificar os dados e manter as alterações no banco de dados. Embora os conjuntos de dados provaram para ser uma tecnologia muito bem-sucedida, é recomendável que novos aplicativos .NET usam Entity Framework. Entity Framework fornece uma maneira mais natural para trabalhar com dados tabulares como modelos de objeto, e ele tem uma interface de programação mais simples.

Um `DataSet` objeto é um objeto na memória que é basicamente um minibanco de dados. Ela contém `DataTable`, `DataColumn`, e `DataRow` objetos em que você pode armazenar e modificar dados de um ou mais bancos de dados sem a necessidade de manter uma conexão aberta. O conjunto de dados mantém informações sobre as alterações nos seus dados, portanto, as atualizações podem ser controladas e enviadas de volta para o banco de dados quando seu aplicativo se torna reconectado.

Conjuntos de dados e classes relacionadas são definidas na <xref:System.Data?displayProperty=fullName> namespace na biblioteca de classes do .NET Framework. Você pode criar e modificar conjuntos de dados dinamicamente no código usando o ADO.NET. A documentação nesta seção mostra como trabalhar com conjuntos de dados usando os designers do Visual Studio. Conjuntos de dados que são criados por meio do uso de designers **TableAdapter** objetos para interagir com o banco de dados. Usam conjuntos de dados que são criados de forma programática **DataAdapter** objetos. Para obter informações sobre como criar conjuntos de dados programaticamente, consulte [DataAdapters e DataReaders](/dotnet/framework/data/adonet/dataadapters-and-datareaders).

Se seu aplicativo precisa apenas ler dados de um banco de dados e não executar atualizações, adiciona ou exclui, você geralmente pode obter um melhor desempenho usando um `DataReader` o objeto para recuperar dados em um genérico `List` objeto ou outro objeto de coleção. Se você estiver exibindo os dados, você pode associar dados a interface do usuário a coleção.

## <a name="dataset-workflow"></a>Fluxo de trabalho do conjunto de dados

O Visual Studio fornece ferramentas para simplificar o trabalho com conjuntos de dados. O fluxo de trabalho de ponta a ponta básico é:

- Use o [janela Data Sources](add-new-data-sources.md#data-sources-window) para criar um novo conjunto de dados de uma ou mais fontes de dados. Use o **Dataset Designer** para configurar o conjunto de dados e definir suas propriedades. Por exemplo, você precisa especificar quais tabelas da fonte de dados para incluir e quais colunas de cada tabela. Escolha cuidadosamente conservar a quantidade de memória que exige que o conjunto de dados. Para obter mais informações, consulte [Create and configure datasets (Criar e configurar conjuntos de dados)](../data-tools/create-and-configure-datasets-in-visual-studio.md).

- Especifica as relações entre as tabelas para que as chaves estrangeiras são tratadas corretamente. Para obter mais informações, consulte [preencher conjuntos de dados usando TableAdapters](../data-tools/fill-datasets-by-using-tableadapters.md).

- Use o **Assistente de configuração TableAdapter** para especificar a consulta ou procedimento armazenado que preenche o conjunto de dados e quais operações de banco de dados (update, delete e assim por diante) para implementar. Para saber mais, consulte estes tópicos:

    - [Preencher conjuntos de dados usando TableAdapters](../data-tools/fill-datasets-by-using-tableadapters.md)

    - [Editar dados em conjuntos de dados](../data-tools/edit-data-in-datasets.md)

    - [Validando dados em conjuntos de dados](../data-tools/validate-data-in-datasets.md)

    - [Salvar dados de volta no banco de dados](../data-tools/save-data-back-to-the-database.md)

- Consultar e pesquisar os dados no conjunto de dados. Para obter mais informações, consulte [conjuntos de dados de consulta](../data-tools/query-datasets.md). [!INCLUDE[linq_dataset](../data-tools/includes/linq_dataset_md.md)] Habilita [LINQ (consulta integrada à linguagem)](/dotnet/csharp/linq/) sobre os dados em um <xref:System.Data.DataSet> objeto. Para obter mais informações, consulte [LINQ to DataSet](/dotnet/framework/data/adonet/linq-to-dataset).

- Use o **fontes de dados** janela associar controles de interface do usuário para o conjunto de dados ou de suas colunas individuais e para especificar quais colunas são editáveis pelo usuário. Para obter mais informações, consulte [Associar Controles a Dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md).

## <a name="datasets-and-n-tier-architecture"></a>Arquitetura de N camadas e conjuntos de dados

Para obter informações sobre conjuntos de dados em aplicativos de N camadas, consulte [trabalhar com conjuntos de dados em aplicativos de n camadas](../data-tools/work-with-datasets-in-n-tier-applications.md).

## <a name="datasets-and-xml"></a>Conjuntos de dados e XML

Para obter informações sobre como converter conjuntos de dados para e do XML, consulte [dados XML de leitura para um conjunto de dados](../data-tools/read-xml-data-into-a-dataset.md) e [salvar um conjunto de dados como XML](../data-tools/save-a-dataset-as-xml.md).

## <a name="see-also"></a>Consulte também

- [Ferramentas de dados do Visual Studio para .NET](../data-tools/visual-studio-data-tools-for-dotnet.md)