---
title: Conjuntos de dados e TableAdapters separados m diferentes projetos
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- TableAdapters, n-tier applications
- n-tier applications, separating Datasets and TableAdapters
ms.assetid: f66a3940-6227-46af-a930-9177f425f4fd
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 504e2411d20a85c85047e4827d613bf4f48034e9
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85281546"
---
# <a name="separate-datasets-and-tableadapters-into-different-projects"></a>Conjuntos de dados e TableAdapters separados m diferentes projetos
Os conjuntos de linhas tipados foram aprimorados para que as classes [TableAdapters](create-and-configure-tableadapters.md) e DataSet possam ser geradas em projetos separados. Isso permite que você separe rapidamente as camadas do aplicativo e gere aplicativos de dados de n camadas.

O procedimento a seguir descreve o processo de usar o **Designer de conjunto de dados** para gerar código de conjunto de conteúdo em um projeto separado do projeto que contém o código do TableAdapter gerado.

## <a name="separate-datasets-and-tableadapters"></a>Conjuntos de valores separados e TableAdapters
Quando você separa o código do DataSet do código do TableAdapter, o projeto que contém o código do conjunto de conteúdo deve estar localizado na solução atual. Se esse projeto não estiver localizado na solução atual, ele não estará disponível na lista de **projetos DataSet** na janela **Propriedades** .

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

#### <a name="to-separate-the-dataset-into-a-different-project"></a>Para separar o DataSet em um projeto diferente

1. Abra uma solução que contenha um conjunto de um (arquivo *. xsd* ).

    > [!NOTE]
    > Se a solução não contiver o projeto no qual você deseja separar o código do conjunto de seus, crie o projeto ou adicione um projeto existente à solução.

2. Clique duas vezes em um arquivo de conjunto de arquivos digitado (um arquivo *. xsd* ) em **Gerenciador de soluções** para abrir o conjunto de **Designer de conjunto de dados**.

3. Selecione uma área vazia da **Designer de conjunto de dados**.

4. Na janela **Propriedades** , localize o nó do **projeto DataSet** .

5. Na lista **projeto DataSet** , selecione o nome do projeto no qual você deseja gerar o código do conjunto de um.

     Depois de selecionar o projeto no qual você deseja gerar o código do conjunto de um, a propriedade do **arquivo DataSet** é populada com um nome de arquivo padrão. Você pode alterar esse nome, se necessário. Além disso, se você quiser gerar o código do conjunto de informações em um diretório específico, poderá definir a propriedade **pasta do projeto** como o nome de uma pasta.

    > [!NOTE]
    > Quando você separa DataSets e TableAdapters (definindo a propriedade de **projeto DataSet** ), as classes parciais DataSet existentes no projeto não serão movidas automaticamente. As classes parciais de DataSet existentes devem ser movidas manualmente para o projeto DataSet.

6. Salve o conjunto de um.

     O código do conjunto de um é gerado no projeto selecionado na propriedade de **projeto DataSet** e o código **TableAdapter** é gerado para o projeto atual.

Por padrão, depois de separar o DataSet e o código do TableAdapter, o resultado é um arquivo de classe discreto em cada projeto. O projeto original tem um arquivo chamado *DataSetName. designer. vb* (ou *DataSetName.designer.cs*) que contém o código do TableAdapter. O projeto designado na Propriedade Project do **conjunto** de conteúdo tem um arquivo chamado *DataSetName. DataSet. designer. vb* (ou *DataSetName.DataSet.designer.cs*) que contém o código do conjunto de conteúdo.

> [!NOTE]
> Para exibir o arquivo de classe gerado, selecione o conjunto de DataSet ou o projeto do TableAdapter. Em seguida, em **Gerenciador de soluções**, selecione **Mostrar todos os arquivos**.

## <a name="see-also"></a>Veja também

- [Visão geral de aplicativos de dados de N camadas](../data-tools/n-tier-data-applications-overview.md)
- [Walkthrough: Criando um aplicativo de dados de N camadas](../data-tools/walkthrough-creating-an-n-tier-data-application.md)
- [Atualização hierárquica](../data-tools/hierarchical-update.md)
- [Acessando dados no Visual Studio](../data-tools/accessing-data-in-visual-studio.md)
- [ADO.NET](/dotnet/framework/data/adonet/index)
