---
title: Ferramentas de conjunto de dados no Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.data.DataSet
dev_langs:
- VB
- CSharp
- C++
- aspx
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
caps.latest.revision: 53
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: b5881542c78c5c055d1cbc26d54eb5e478a13124
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49254339"
---
# <a name="dataset-tools-in-visual-studio"></a>Ferramentas de conjunto de dados no Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
OBSERVAÇÃO]
>  Conjuntos de dados e classes relacionadas são herdadas tecnologias do .NET do início dos anos 2000 que habilitam aplicativos para trabalhar com dados na memória enquanto os aplicativos estão desconectados do banco de dados. Eles são especialmente úteis para aplicativos que permitem aos usuários modificar os dados e manter as alterações no banco de dados. Embora os conjuntos de dados provaram para ser uma tecnologia muito bem-sucedida, é recomendável que novos aplicativos .NET usam Entity Framework. Entity Framework fornece uma maneira mais natural para trabalhar com dados tabulares como modelos de objeto, e ele tem uma interface de programação mais simples.  
  
 Um objeto de conjunto de dados é um objeto na memória que é basicamente um minibanco de dados. Ele contém objetos DataRow, DataTable e DataColumn em que você pode armazenar e modificar dados de um ou mais bancos de dados sem a necessidade de manter uma conexão aberta. O conjunto de dados mantém informações sobre as alterações nos seus dados, portanto, as atualizações podem ser controladas e enviadas de volta para o banco de dados quando seu aplicativo se torna reconectado.  
  
 Conjuntos de dados e classes relacionadas são definidas no namespace System. Data, na biblioteca de classes do .NET Framework. Você pode criar e modificar conjuntos de dados dinamicamente no código. Para obter mais informações sobre como fazer isso, consulte o ADO.NET. A documentação nesta seção mostra como trabalhar com conjuntos de dados usando os designers do Visual Studio. Uma coisa a saber: conjuntos de dados que são feitos por meio de designers de usam objetos do TableAdapter para interagir com o banco de dados, enquanto que conjuntos de dados que são feitos por meio de programação usam DataAdapter objetos. Para obter informações sobre como criar conjuntos de dados programaticamente, consulte [DataAdapters e DataReaders](http://msdn.microsoft.com/library/cc952ca2-ec19-46ab-9189-15174b52cb74).  
  
 Se seu aplicativo precisa apenas ler dados de um banco de dados e não executar atualizações, adiciona ou exclui, você geralmente pode obter um melhor desempenho por meio de um objeto DataReader para recuperar dados em um objeto List genérico ou outro objeto da coleção. Se você estiver exibindo os dados, você pode associar dados a interface do usuário a coleção.  
  
## <a name="dataset-workflow"></a>Fluxo de trabalho do conjunto de dados  
 O Visual Studio fornece muitas ferramentas para simplificar o trabalho com conjuntos de dados. O fluxo de trabalho de ponta a ponta básico é:  
  
-   Use o **fonte de dados** janela para criar um novo conjunto de dados de uma ou mais fontes de dados. Use o **Dataset Designer** para configurar o conjunto de dados e definir suas propriedades. Por exemplo, você precisa especificar quais tabelas da fonte de dados para incluir e quais colunas de cada tabela. Escolha cuidadosamente conservar a quantidade de memória que exigirão o conjunto de dados. Para obter mais informações, consulte [Create and configure datasets (Criar e configurar conjuntos de dados)](../data-tools/create-and-configure-datasets-in-visual-studio.md).  
  
-   Especifica as relações entre as tabelas para que as chaves estrangeiras são tratadas corretamente. Para obter mais informações, consulte [preencher conjuntos de dados usando TableAdapters](../data-tools/fill-datasets-by-using-tableadapters.md).  
  
-   Use o **Assistente de configuração TableAdapter** para especificar a consulta ou procedimento armazenado que preencherá o conjunto de dados e quais operações de banco de dados (update, delete e assim por diante) para implementar. Para saber mais, consulte estes tópicos:  
  
    -   [Preencher conjuntos de dados usando TableAdapters](../data-tools/fill-datasets-by-using-tableadapters.md)  
  
    -   [Editar dados em conjuntos de dados](../data-tools/edit-data-in-datasets.md)  
  
    -   [Validando dados em conjuntos de dados](../data-tools/validate-data-in-datasets.md)  
  
    -   [Salvar dados de volta no banco de dados](../data-tools/save-data-back-to-the-database.md)  
  
-   Consultar e pesquisar os dados no conjunto de dados. Para obter mais informações, consulte [conjuntos de dados de consulta](../data-tools/query-datasets.md). [!INCLUDE[linq_dataset](../includes/linq-dataset-md.md)] Habilita [LINQ (consulta integrada à linguagem)](http://msdn.microsoft.com/library/a73c4aec-5d15-4e98-b962-1274021ea93d) sobre os dados em um <xref:System.Data.DataSet> objeto. Para obter mais informações, consulte [LINQ to DataSet](http://msdn.microsoft.com/library/743e3755-3ecb-45a2-8d9b-9ed41f0dcf17).  
  
-   Use o **fontes de dados** janela associar controles de interface do usuário para o conjunto de dados ou de suas colunas individuais e para especificar quais colunas são editáveis pelo usuário. Para obter mais informações, consulte [associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md).  
  
## <a name="datasets-and-n-tier-architecture"></a>Arquitetura de N camadas e conjuntos de dados  
 Para obter informações sobre conjuntos de dados em aplicativos de N camadas, consulte [trabalhar com conjuntos de dados em aplicativos de n camadas](../data-tools/work-with-datasets-in-n-tier-applications.md).  
  
## <a name="datasets-and-xml"></a>Conjuntos de dados e XML  
 Para obter informações sobre como converter conjuntos de dados para e do XML, consulte [dados XML de leitura para um conjunto de dados](../data-tools/read-xml-data-into-a-dataset.md) e [salvar um conjunto de dados como XML](../data-tools/save-a-dataset-as-xml.md).  
  
## <a name="see-also"></a>Consulte também  
 [Ferramentas de dados do Visual Studio para .NET](../data-tools/visual-studio-data-tools-for-dotnet.md)

