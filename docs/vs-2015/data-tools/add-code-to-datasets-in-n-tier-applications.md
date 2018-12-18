---
title: Adicione o código a conjuntos de dados em aplicativos de n camadas | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- n-tier applications, extending datasets
ms.assetid: d43c2ccd-4902-43d8-b1a8-d10ca5d3210c
caps.latest.revision: 23
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 48f27d2e1bb72b7c5c0aaf1a66673beae003dd66
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49202209"
---
# <a name="add-code-to-datasets-in-n-tier-applications"></a>Adicionar código a conjuntos de dados em aplicativos de n camadas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Você pode estender a funcionalidade de um conjunto de dados, criando um arquivo de classe parcial para o conjunto de dados e adicionando código a ele (em vez de adicionar código para o *DatasetName*. Arquivo do DataSet). Classes parciais permitem codificar uma classe específica a ser dividido entre vários arquivos físicos. Para obter mais informações, consulte [parcial](http://msdn.microsoft.com/library/7adaef80-f435-46e1-970a-269fff63b448) ou [Classes e métodos parciais](http://msdn.microsoft.com/library/804cecb7-62db-4f97-a99f-60975bd59fa1).  
  
 O código que define um conjunto de dados é gerado sempre que forem feitas alterações a definição de conjunto de dados (na [criando e editando conjuntos de dados tipados](../data-tools/creating-and-editing-typed-datasets.md)). Esse código também é gerado quando você fizer alterações durante a execução de qualquer assistente que modifica a configuração de um conjunto de dados. Para impedir que seu código seja excluído durante a regeneração de um conjunto de dados, adicione código ao arquivo de classe parcial do conjunto de dados.  
  
 Por padrão, após você separar o conjunto de dados e `TableAdapter` código, o resultado é um arquivo de classe distintas em cada projeto. O projeto original tem uma filenamed *DatasetName*. VB (ou *DatasetName*. Designer.cs) que contém o `TableAdapter` código. O projeto que é designado na **projeto Dataset** propriedade tem um arquivo chamado *DatasetName*. DataSet.Designer.vb (ou *DatasetName*. DataSet.Designer.cs). Esse arquivo contém o código do conjunto de dados.  
  
> [!NOTE]
>  Quando você separa os conjuntos de dados e `TableAdapter`s (definindo o **projeto DataSet** propriedade), classes parciais do conjunto de dados existentes no projeto não serão movidas automaticamente. Classes parciais do conjunto de dados existente devem ser movidas manualmente para o projeto de conjunto de dados.  
  
> [!NOTE]
>  Quando o código de validação deve ser adicionado, o [criando e editando conjuntos de dados tipados](../data-tools/creating-and-editing-typed-datasets.md)fornece funcionalidade para gerar <xref:System.Data.DataTable.ColumnChanging> e <xref:System.Data.DataTable.RowChanging> manipuladores de eventos. Para obter mais informações, consulte [adicionar validação a um conjunto de dados de n camadas](../data-tools/add-validation-to-an-n-tier-dataset.md).  
  
### <a name="to-add-code-to-datasets-in-n-tier-applications"></a>Para adicionar código a conjuntos de dados em aplicativos de n camadas  
  
1.  Localize o projeto que contém o arquivo. xsd (o [criando e editando conjuntos de dados tipados](../data-tools/creating-and-editing-typed-datasets.md)).  
  
2.  Selecione o **. xsd** arquivo para abrir o [criando e editando conjuntos de dados tipados](../data-tools/creating-and-editing-typed-datasets.md).  
  
3.  Clique na tabela de dados ao qual você deseja adicionar o código (o nome da tabela na barra de título) e selecione**Exibir código**.  
  
     Uma classe parcial é criada e é aberto no Editor de códigos.  
  
4.  Adicione o código dentro da declaração de classe parcial.  
  
     O exemplo a seguir mostra onde adicionar código para o CustomersDataTable no NorthwindDataSet:  
  
    ```vb  
    Partial Public Class CustomersDataTable  
        ' Add code here to add functionality   
        ' to the CustomersDataTable.  
    End Class  
    ```  
  
    ```csharp  
    partial class CustomersDataTable  
    {  
        // Add code here to add functionality  
        // to the CustomersDataTable.  
    }  
    ```  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral dos aplicativos de dados de N camadas](../data-tools/n-tier-data-applications-overview.md)   
 [Adicionar código a TableAdapters em aplicativos de n camadas](../data-tools/add-code-to-tableadapters-in-n-tier-applications.md)   
 [TableAdapters](http://msdn.microsoft.com/library/09416de9-134c-4dc7-8262-6c8d81e3f364)   
 [Visão geral de TableAdapterManager](http://msdn.microsoft.com/library/33076d42-6b41-491a-ac11-6c6339aea650)   
 [Visão geral de atualização hierárquica](http://msdn.microsoft.com/library/c4f8e8b9-e4a5-4a02-8462-d03d1e8222d6)   
 [Criando aplicativos de dados](../data-tools/creating-data-applications.md)   
 [Ferramentas de conjunto de dados no Visual Studio](../data-tools/dataset-tools-in-visual-studio.md)

