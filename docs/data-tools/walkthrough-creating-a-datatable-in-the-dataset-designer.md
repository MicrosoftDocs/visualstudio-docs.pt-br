---
title: 'Instruções passo a passo: criando um DataTable no Designer de Conjunto de Dados'
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- DataTable objects, creating
- Dataset Designer, creating data tables
- tables [Visual Studio], creating
- data [Visual Studio], Dataset Designer
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 2cff383b6e06d8793a7730c36df01e2538b02c36
ms.sourcegitcommit: f37affbc1b885dfe246d4b2c295a6538b383a0ca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37174479"
---
# <a name="walkthrough-create-a-datatable-in-the-dataset-designer"></a>Passo a passo: Criar uma DataTable no Dataset Designer

Este passo a passo explica como criar uma <xref:System.Data.DataTable> (sem um TableAdapter) usando o **Dataset Designer**. Para obter informações sobre como criar tabelas de dados que incluem TableAdapters, consulte [criar e configurar TableAdapters](../data-tools/create-and-configure-tableadapters.md).

## <a name="create-a-new-windows-forms-application"></a>Criar um novo aplicativo Windows Forms

1. No Visual Studio, sobre o **arquivo** menu, selecione **New** > **projeto**.

2. Expanda o **Visual c#** ou **Visual Basic** no painel esquerdo, em seguida, selecione **área de trabalho do Windows**.

3. No painel central, selecione a **aplicativo do Windows Forms** tipo de projeto.

4. Nomeie o projeto **DataTableWalkthrough**e, em seguida, escolha **Okey**.

     O **DataTableWalkthrough** projeto é criado e adicionado ao **Gerenciador de soluções**.

## <a name="add-a-new-dataset-to-the-application"></a>Adicionar um novo conjunto de dados para o aplicativo

1.  Sobre o **Project** menu, selecione **Adicionar Novo Item**.

     A caixa de diálogo **Adicionar Novo Item** é exibida.

2.  No painel esquerdo, selecione **dados**, em seguida, selecione **conjunto de dados** no painel central.

3.  Escolha **Adicionar**.

     O Visual Studio adiciona um arquivo chamado **dataSet1** ao projeto e abre-o na **Dataset Designer**.

## <a name="add-a-new-datatable-to-the-dataset"></a>Adicionar uma nova DataTable para o conjunto de dados

1.  Arraste uma **DataTable** da **conjunto de dados** guia da **caixa de ferramentas** para o **Dataset Designer**.

     Uma tabela denominada **DataTable1** é adicionado ao conjunto de dados.

2.  Clique na barra de título do **DataTable1** e renomeie- `Music`.

## <a name="add-columns-to-the-datatable"></a>Adicionar colunas à tabela de dados

1.  Clique com botão direito do **música** tabela. Aponte para **Add**e, em seguida, clique em **coluna**.

2.  Nome da coluna `SongID`.

3.  No **propriedades** janela, defina as <xref:System.Data.DataColumn.DataType%2A> propriedade <xref:System.Int16?displayProperty=fullName>.

4.  Repita esse processo e adicione as seguintes colunas:

     `SongTitle`: <xref:System.String?displayProperty=fullName>

     `Artist`: <xref:System.String?displayProperty=fullName>

     `Genre`: <xref:System.String?displayProperty=fullName>

## <a name="set-the-primary-key-for-the-table"></a>Defina a chave primária da tabela

Todas as tabelas de dados devem ter uma chave primária. Uma chave primária identifica exclusivamente um registro específico em uma tabela de dados.

Para definir a chave primária, clique com botão direito do **SongID** coluna e clique **definir chave primária**. Um ícone de chave aparece ao lado de **SongID** coluna.

## <a name="save-your-project"></a>Salve seu projeto

Para salvar a **DataTableWalkthrough** do projeto, no **arquivo** menu, selecione **Salvar tudo**.

## <a name="see-also"></a>Consulte também

- [Criar e configurar conjuntos de dados no Visual Studio](../data-tools/create-and-configure-datasets-in-visual-studio.md)
- [Associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md)
- [Validando dados](../data-tools/validate-data-in-datasets.md)