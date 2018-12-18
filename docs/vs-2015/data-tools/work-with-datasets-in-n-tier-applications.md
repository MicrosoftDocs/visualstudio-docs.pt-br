---
title: Trabalhar com conjuntos de dados em aplicativos de n camadas | Microsoft Docs
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
- datasets [Visual Basic], n-tier applications
- multi-tier database applications
- DataSet project [VS n-tier applications]
- distributed applications [VS n-tier applications]
- data [Visual Basic], n-tier applications
- TableAdapters, n-tier applications
- n-tier applications
- tiers, n-tier applications
- typed datasets, n-tier applications
- multiple tier applications
ms.assetid: f6ae2ee0-ea5f-4a79-8f4b-e21c115afb20
caps.latest.revision: 25
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: d05204edfd7c3cd5daecad3a1cb21ba5ba7e60d8
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49205966"
---
# <a name="work-with-datasets-in-n-tier-applications"></a>Trabalhar com conjuntos de dados em aplicativos de n camadas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Aplicativos de dados de N camadas * são aplicativos centrados em dados que são separados em várias camadas lógicas (ou *camadas*). Em outras palavras, um aplicativo de dados de N camadas é um aplicativo separado em vários projetos, com camada de acesso a dados, camada lógica de negócios e camada de apresentação em seu próprio projeto. Para obter mais informações, consulte [visão geral dos aplicativos de dados de N camadas](../data-tools/n-tier-data-applications-overview.md).  
  
 Os conjuntos de dados tipados foram aprimorados para que as classes TableAdapters e de conjuntos de dados possam ser geradas em projetos discretos. Com isso, é possível separar com rapidez as camadas de aplicativos e gerar aplicativos de dados de N camadas.  
  
 Suporte de N camadas em conjuntos de dados tipados permite desenvolvimento iterativo da arquitetura do aplicativo para um design de n camadas. Ela também remove a necessidade de separar manualmente o código em mais de um projeto. Comece a projetar a camada de dados usando o [criando e editando conjuntos de dados tipados](../data-tools/creating-and-editing-typed-datasets.md). Quando estiver pronto para assumir a arquitetura do aplicativo a um design de n camadas, defina as **projeto DataSet** propriedade de um conjunto de dados para gerar a classe de conjunto de dados em um projeto separado.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Separar conjuntos de dados e TableAdapters em diferentes projetos](../data-tools/separate-datasets-and-tableadapters-into-different-projects.md)  
 Descreve como mover a classe do conjunto de dados gerada para fora do projeto que contém as classes TableAdapter geradas e para dentro de um novo projeto.  
  
 [Adicionar código a TableAdapters em aplicativos de N camadas](../data-tools/add-code-to-tableadapters-in-n-tier-applications.md)  
 Descreve como gerar uma classe parcial na qual é possível adicionar código para um TableAdapter de N camadas.  
  
 [Como adicionar código a conjuntos de dados em aplicativos de N camadas](../data-tools/add-code-to-datasets-in-n-tier-applications.md)  
 Descreve como gerar uma classe parcial na qual é possível adicionar código para um conjunto de dados de N camadas.  
  
 [Adicionar validação a um conjunto de dados de N camadas](../data-tools/add-validation-to-an-n-tier-dataset.md)  
 Descreve onde adicionar código para executar validação na alteração de dados.  
  
 [Passo a passo: criando um aplicativo de dados de N camadas](../data-tools/walkthrough-creating-an-n-tier-data-application.md)  
 Fornece instruções passo a passo para criar um conjunto de dados tipado e separar o código do TableAdapter e do conjunto de dados em vários projetos.  
  
 [Passo a passo: Adicionando validação a um aplicativo de dados de N camadas](http://msdn.microsoft.com/library/b35d072c-31f0-49ba-a225-69177592c265)  
 Fornece instruções passo a passo para adicionar validação para o aplicativo que foi criado no passo a passo dados de n camadas do aplicativo.  
  
## <a name="reference"></a>Referência  
 <xref:System.Data.DataSet>  
  
 <xref:System.Data.TypedTableBase%601>  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Visão geral de aplicativos de dados de N camadas](../data-tools/n-tier-data-applications-overview.md)  
  
 [Atualização hierárquica](../data-tools/hierarchical-update.md)  
  
 [Ferramentas de conjunto de dados no Visual Studio](../data-tools/dataset-tools-in-visual-studio.md)  
  
 [Acessando dados no Visual Studio](../data-tools/accessing-data-in-visual-studio.md)  
  
 [Visão geral de TableAdapter](../data-tools/tableadapter-overview.md)  
  
 [Aplicativos de N camadas e remotos com o LINQ to SQL](http://msdn.microsoft.com/library/854a1cdd-53cb-45f5-83ca-63962a9b3598)

