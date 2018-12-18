---
title: Conjuntos de dados e TableAdapters separados m diferentes projetos
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- TableAdapters, n-tier applications
- n-tier applications, separating Datasets and TableAdapters
ms.assetid: f66a3940-6227-46af-a930-9177f425f4fd
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 01e572a2ac20d1cfb103e1600307b51bdf58a0b8
ms.sourcegitcommit: f37affbc1b885dfe246d4b2c295a6538b383a0ca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37174313"
---
# <a name="separate-datasets-and-tableadapters-into-different-projects"></a>Conjuntos de dados e TableAdapters separados m diferentes projetos
Conjuntos de dados tipados foram aprimorados para que o [TableAdapters](create-and-configure-tableadapters.md) e classes de conjunto de dados podem ser geradas em projetos separados. Isso permite que você separe as camadas de aplicativos rapidamente e gerar aplicativos de dados de n camadas.

O procedimento a seguir descreve o processo de usar o **Dataset Designer** para gerar o código do conjunto de dados em um projeto separado do projeto que contém o código gerado do TableAdapter.

## <a name="separate-datasets-and-tableadapters"></a>Conjuntos de dados separados e os TableAdapters
Quando você separar o código do conjunto de dados de código TableAdapter, o projeto que contém o código do conjunto de dados deve estar localizado na solução atual. Se este projeto não for encontrado na solução atual, ele não estará disponível na **projeto DataSet** listar na **propriedades** janela.

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

#### <a name="to-separate-the-dataset-into-a-different-project"></a>Para separar o conjunto de dados em um projeto diferente

1.  Abrir uma solução que contém um conjunto de dados (*. xsd* arquivo).

    > [!NOTE]
    >  Se a solução não contém o projeto no qual você deseja separar o código do conjunto de dados, criar o projeto, ou adicionar um projeto existente à solução.

2.  Clique duas vezes em um arquivo de conjunto de dados tipado (um *. xsd* arquivo) em **Gerenciador de soluções** para abrir o conjunto de dados do **Dataset Designer**.

3.  Selecione uma área vazia do **Dataset Designer**.

4.  No **propriedades** janela, localize a **projeto DataSet** nó.

5.  No **projeto DataSet** , selecione o nome do projeto no qual você deseja gerar o código do conjunto de dados.

     Depois de selecionar o projeto no qual você deseja gerar o código do conjunto de dados, o **arquivo de conjunto de dados** propriedade é preenchida com um nome de arquivo padrão. Você pode alterar esse nome, se necessário. Além disso, se você quiser gerar o código do conjunto de dados em um diretório específico, você pode definir as **pasta do projeto** propriedade para o nome de uma pasta.

    > [!NOTE]
    >  Quando você separa os conjuntos de dados e TableAdapters (Configurando o **projeto DataSet** propriedade), classes parciais do conjunto de dados existentes no projeto não serão movidas automaticamente. As classes parciais do conjunto de dados existentes devem ser movidas manualmente para o projeto de conjunto de dados.

6.  Salve o conjunto de dados.

     O código do conjunto de dados é gerado para o projeto selecionado na **projeto DataSet** propriedade e o **TableAdapter** código é gerado para o projeto atual.

Por padrão, após você separar o conjunto de dados e o código TableAdapter, o resultado é um arquivo de classe distintas em cada projeto. O projeto original tem um arquivo chamado *DatasetName.Designer.vb* (ou *DatasetName.Designer.cs*) que contém o código do TableAdapter. O projeto que é designado na **projeto Dataset** propriedade tem um arquivo chamado *DatasetName.DataSet.Designer.vb* (ou *DatasetName.DataSet.Designer.cs*) que contém o código do conjunto de dados.

> [!NOTE]
>  Para exibir o arquivo de classe gerado, selecione o conjunto de dados ou projeto do TableAdapter. Em seguida, na **Gerenciador de soluções**, selecione **Mostrar todos os arquivos**.

## <a name="see-also"></a>Consulte também

- [Visão geral dos aplicativos de dados de N camadas](../data-tools/n-tier-data-applications-overview.md)
- [Passo a passo: Criando um aplicativo de dados de N camadas](../data-tools/walkthrough-creating-an-n-tier-data-application.md)
- [Atualização hierárquica](../data-tools/hierarchical-update.md)
- [Acessando dados no Visual Studio](../data-tools/accessing-data-in-visual-studio.md)
- [ADO.NET](/dotnet/framework/data/adonet/index)