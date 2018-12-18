---
title: Separar conjuntos de dados e TableAdapters em diferentes projetos | Microsoft Docs
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
- TableAdapters, n-tier applications
- n-tier applications, separating Datasets and TableAdapters
ms.assetid: f66a3940-6227-46af-a930-9177f425f4fd
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 1e94c76254b14bdf82e4e7a219cbb0f35cb532f1
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49824308"
---
# <a name="separate-datasets-and-tableadapters-into-different-projects"></a>Conjuntos de dados e TableAdapters separados m diferentes projetos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Conjuntos de dados tipados foram aprimorados para que o [TableAdapters](http://msdn.microsoft.com/library/09416de9-134c-4dc7-8262-6c8d81e3f364) e classes de conjunto de dados podem ser geradas em projetos separados. Isso permite que você separe as camadas de aplicativos rapidamente e gerar aplicativos de dados de n camadas.  
  
 O procedimento a seguir descreve o processo de usar o[criando e editando conjuntos de dados tipados](../data-tools/creating-and-editing-typed-datasets.md) para gerar o código do conjunto de dados em um projeto separado do projeto que contém o gerado `TableAdapter` código.  
  
## <a name="separatedatasets-and-tableadapters"></a>Separatedatasets e TableAdapters  
 Quando você separa o código do conjunto de dados de `TableAdapter` código, o projeto que contém o código do conjunto de dados deve estar localizado na solução atual. Se este projeto não for encontrado na solução atual, ele não estará disponível na **projeto DataSet** listar na **propriedades** janela.  
  
 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]  
  
#### <a name="to-separate-the-dataset-into-a-different-project"></a>Para separar o conjunto de dados em um projeto diferente  
  
1. Abra uma solução que contém um conjunto de dados (arquivo. xsd).  
  
   > [!NOTE]
   >  Se a solução não contém o projeto no qual você deseja separar o código do conjunto de dados, criar o projeto, ou adicionar um projeto existente à solução.  
  
2. Clique duas vezes em um arquivo de conjunto de dados tipado (arquivo. xsd) no **Gerenciador de soluções** para abrir o conjunto de dados de **Dataset Designer**.  
  
3. Selecione uma área vazia do **Dataset Designer**.  
  
4. No **propriedades** janela, localize a **projeto DataSet** nó.  
  
5. No **projeto DataSet** , selecione o nome do projeto no qual você deseja gerar o código do conjunto de dados.  
  
    Depois de selecionar o projeto no qual você deseja gerar o código do conjunto de dados, o **arquivo de conjunto de dados** propriedade é preenchida com um nome de arquivo padrão. Você pode alterar esse nome, se necessário. Além disso, se você quiser gerar o código do conjunto de dados em um diretório específico, você pode definir as **pasta do projeto** propriedade para o nome de uma pasta.  
  
   > [!NOTE]
   >  Quando você separa os conjuntos de dados e TableAdapters (Configurando o **projeto DataSet** propriedade), classes parciais do conjunto de dados existentes no projeto não serão movidas automaticamente. Classes parciais do conjunto de dados existente devem ser movidas manualmente para o projeto de conjunto de dados.  
  
6. Salve o conjunto de dados.  
  
    O código do conjunto de dados é gerado para o projeto selecionado na **projeto DataSet** propriedade e o **TableAdapter** código é gerado para o projeto atual.  
  
   Por padrão, após você separar o conjunto de dados e `TableAdapter` código, o resultado é um arquivo de classe distintas em cada projeto. O projeto original tem um arquivo chamado DatasetName.Designer.vb (ou DatasetName.Designer.cs) que contém o `TableAdapter` código. O projeto que é designado na **projeto Dataset** propriedade tem um arquivo chamado DatasetName.DataSet.Designer.vb (ou DatasetName.DataSet.Designer.cs) que contém o código de conjunto de dados.  
  
> [!NOTE]
>  Para exibir o arquivo de classe gerado, selecione o conjunto de dados ou `TableAdapter` projeto. Em seguida, na **Gerenciador de soluções**, selecione **Mostrar todos os arquivos** .  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral dos aplicativos de dados de N camadas](../data-tools/n-tier-data-applications-overview.md)   
 [Passo a passo: Criando um aplicativo de dados de N camadas](../data-tools/walkthrough-creating-an-n-tier-data-application.md)   
 [Atualização hierárquica](../data-tools/hierarchical-update.md)   
 [Accessing data in Visual Studio](../data-tools/accessing-data-in-visual-studio.md)  (Acessando dados no Visual Studio)  
 [ADO.NET](http://msdn.microsoft.com/library/5b96ed06-9759-4966-a797-a1d5f6ee50ca)

