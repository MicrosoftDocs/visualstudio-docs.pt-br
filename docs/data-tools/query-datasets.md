---
title: Consultar conjuntos de dados
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
ms.assetid: 7b1a91cf-8b5a-4fc0-ac36-0dc2d336fa1b
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 2276828a67cec2562063d220ef3173d98fdf487b
ms.sourcegitcommit: f37affbc1b885dfe246d4b2c295a6538b383a0ca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37174287"
---
# <a name="query-datasets"></a>Consultar conjuntos de dados
Para procurar registros específicos em um conjunto de dados, use o `FindBy` método na DataTable, escrever sua própria instrução foreach para executar um loop pela coleção de linhas da tabela, ou use [LINQ to DataSet](/dotnet/framework/data/adonet/linq-to-dataset).

## <a name="dataset-case-sensitivity"></a>Conjunto de dados diferenciação
Dentro de um conjunto de dados, nomes de coluna e tabela diferenciam maiusculas de minúsculas por padrão — ou seja, uma tabela em um conjunto de dados chamado "Clientes" pode também ser referida como "clientes". Isso coincide com as convenções de nomenclatura em vários bancos de dados, incluindo o SQL Server. No SQL Server, o comportamento padrão é que os nomes dos elementos de dados não podem ser diferenciados apenas por maiusculas.

> [!NOTE]
>  Ao contrário de conjuntos de dados, documentos XML diferenciam maiusculas de minúsculas, portanto, os nomes de elementos de dados definidos em esquemas diferenciam maiusculas de minúsculas. Por exemplo, o protocolo de esquema permite que o esquema definir uma tabela chamada "Clientes" e uma tabela diferente chamada "clientes". Isso pode resultar em conflitos de nome quando um esquema que contém elementos que diferem somente maiusculas é usado para gerar uma classe de conjunto de dados.

Diferenciar maiusculas de minúsculas, no entanto, podem ser um fator em como os dados são interpretados no conjunto de dados. Por exemplo, se você filtrar dados em uma tabela de conjunto de dados, os critérios de pesquisa podem retornar resultados diferentes dependendo se a comparação não diferencia maiusculas de minúsculas. Você pode controlar a diferenciação de filtragem, pesquisa e classificação definindo o conjunto de dados <xref:System.Data.DataSet.CaseSensitive%2A> propriedade. Todas as tabelas no conjunto de dados herdam o valor dessa propriedade por padrão. (Você pode substituir essa propriedade para cada tabela individual, definindo a tabela <xref:System.Data.DataTable.CaseSensitive%2A> propriedade.)

## <a name="locate-a-specific-row-in-a-data-table"></a>Localizar uma linha específica em uma tabela de dados

#### <a name="to-find-a-row-in-a-typed-dataset-with-a-primary-key-value"></a>Para localizar uma linha em um dataset digitado com um valor de chave primária

-   Para localizar uma linha, chamar fortemente tipado `FindBy` método que usa a chave primária da tabela.

     No exemplo a seguir, o `CustomerID` coluna é a chave primária do `Customers` tabela. Isso significa que o gerado `FindBy` método é `FindByCustomerID`. O exemplo mostra como atribuir um determinado <xref:System.Data.DataRow> a uma variável usando o gerado `FindBy` método.

     [!code-csharp[VbRaddataEditing#18](../data-tools/codesnippet/CSharp/query-datasets_1.cs)]
     [!code-vb[VbRaddataEditing#18](../data-tools/codesnippet/VisualBasic/query-datasets_1.vb)]

#### <a name="to-find-a-row-in-an-untyped-dataset-with-a-primary-key-value"></a>Para localizar uma linha em um conjunto de dados sem tipo com um valor de chave primária

-   Chame o <xref:System.Data.DataRowCollection.Find%2A> método de um <xref:System.Data.DataRowCollection> coleção, passando a chave primária como um parâmetro.

     O exemplo a seguir mostra como declarar uma nova linha chamada `foundRow` e atribua a ela o valor de retorno de <xref:System.Data.DataRowCollection.Find%2A> método. Se a chave primária for encontrada, o conteúdo do índice da coluna 1 é exibido em uma caixa de mensagem.

     [!code-csharp[VbRaddataEditing#19](../data-tools/codesnippet/CSharp/query-datasets_2.cs)]
     [!code-vb[VbRaddataEditing#19](../data-tools/codesnippet/VisualBasic/query-datasets_2.vb)]

## <a name="find-rows-by-column-values"></a>Localizar linhas por valores de coluna

#### <a name="to-find-rows-based-on-the-values-in-any-column"></a>Para localizar linhas com base nos valores em qualquer coluna

-   Tabelas de dados são criadas com o <xref:System.Data.DataTable.Select%2A> método, que retorna uma matriz de <xref:System.Data.DataRow>s com base na expressão passada para o <xref:System.Data.DataTable.Select%2A> método. Para obter mais informações sobre como criar expressões válidas, consulte a seção "Sintaxe da expressão" da página o <xref:System.Data.DataColumn.Expression%2A> propriedade.

     O exemplo a seguir mostra como usar o <xref:System.Data.DataTable.Select%2A> método da <xref:System.Data.DataTable> para localizar linhas específicas.

     [!code-csharp[VbRaddataEditing#20](../data-tools/codesnippet/CSharp/query-datasets_3.cs)]
     [!code-vb[VbRaddataEditing#20](../data-tools/codesnippet/VisualBasic/query-datasets_3.vb)]

## <a name="access-related-records"></a>Registros relacionados de acesso
Quando estão relacionadas a tabelas em um conjunto de dados, um <xref:System.Data.DataRelation> objeto pode disponibilizar os registros relacionados em outra tabela. Por exemplo, um conjunto de dados que contém `Customers` e `Orders` tabelas podem ser disponibilizadas.

Você pode usar um <xref:System.Data.DataRelation> objeto para localizar registros relacionados chamando o <xref:System.Data.DataRow.GetChildRows%2A> método de um <xref:System.Data.DataRow> na tabela pai. Esse método retorna uma matriz de registros filho relacionados. Ou, você pode chamar o <xref:System.Data.DataRow.GetParentRow%2A> método de um <xref:System.Data.DataRow> na tabela filho. Esse método retorna um único <xref:System.Data.DataRow> da tabela pai.

Esta página fornece exemplos que usam conjuntos de dados tipados. Para obter informações sobre navegar em relações em conjuntos de dados não tipados, consulte [navegando em DataRelations](/dotnet/framework/data/adonet/dataset-datatable-dataview/navigating-datarelations).

> [!NOTE]
>  Se você estiver trabalhando em um aplicativo Windows Forms e usando os recursos de vinculação de dados para exibir dados, o formulário gerado pelo designer pode fornecer funcionalidade suficiente para seu aplicativo. Para obter mais informações, consulte [associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md). Especificamente, consulte [relacionamentos em conjuntos de dados](relationships-in-datasets.md).

Os exemplos de código a seguir demonstram como navegar para cima e para relacionamentos em conjuntos de dados tipados. O uso de exemplos de código digitado <xref:System.Data.DataRow>s (`NorthwindDataSet.OrdersRow`) e o FindBy gerado*PrimaryKey* (`FindByCustomerID`) métodos para localizar uma linha desejada e retornar os registros relacionados. Os exemplos de compilar e executam corretamente somente se você tiver:

-   Uma instância de um conjunto de dados denominado `NorthwindDataSet` com um `Customers` tabela.

-   Um `Orders` tabela.

-   Uma relação nomeada `FK_Orders_Customers`relacionando as duas tabelas.

Além disso, ambas as tabelas precisam ser preenchida com dados para todos os registros a serem retornados.

#### <a name="to-return-the-child-records-of-a-selected-parent-record"></a>Para retornar os registros de um registro pai selecionado filho

-   Chame o <xref:System.Data.DataRow.GetChildRows%2A> método de um determinado `Customers` dados de linha e retornar uma matriz de linhas do `Orders` tabela:

     [!code-csharp[VbRaddataDatasets#6](../data-tools/codesnippet/CSharp/query-datasets_4.cs)]
     [!code-vb[VbRaddataDatasets#6](../data-tools/codesnippet/VisualBasic/query-datasets_4.vb)]

#### <a name="to-return-the-parent-record-of-a-selected-child-record"></a>Para retornar o registro pai de um registro filho selecionado

-   Chame o <xref:System.Data.DataRow.GetParentRow%2A> método de um determinado `Orders` linha de dados e retornar uma única linha do `Customers` tabela:

     [!code-csharp[VbRaddataDatasets#7](../data-tools/codesnippet/CSharp/query-datasets_5.cs)]
     [!code-vb[VbRaddataDatasets#7](../data-tools/codesnippet/VisualBasic/query-datasets_5.vb)]

## <a name="see-also"></a>Consulte também

- [Ferramentas de conjunto de dados no Visual Studio](../data-tools/dataset-tools-in-visual-studio.md)