---
title: Estender a funcionalidade de um TableAdapter
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Visual Studio], TableAdapters
- data [Visual Studio], extending TableAdapters
- TableAdapters, adding functionality
ms.assetid: 418249c8-c7f3-47ef-a94c-744cb6fe6aaf
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 245ea6791fde96c1ff08d43d138c522f43749c6b
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85282417"
---
# <a name="extend-the-functionality-of-a-tableadapter"></a>Estender a funcionalidade de um TableAdapter

Você pode estender a funcionalidade de um TableAdapter adicionando código ao arquivo de classe parcial do TableAdapter.

O código que define um TableAdapter é regenerado quando qualquer alteração é feita no TableAdapter no **Designer de conjunto de dados**, ou quando um assistente modifica a configuração de um TableAdapter. Para impedir que seu código seja excluído durante a regeneração de um TableAdapter, adicione o código ao arquivo de classe parcial do TableAdapter.

As classes parciais permitem que o código de uma classe específica seja dividido entre vários arquivos físicos. Para obter mais informações, consulte [parcial](/dotnet/visual-basic/language-reference/modifiers/partial) ou [parcial (tipo)](/dotnet/csharp/language-reference/keywords/partial-type).

## <a name="locate-tableadapters-in-code"></a>Localizar TableAdapters no código

Embora os TableAdapters sejam projetados com o **Designer de conjunto de dados**, as classes do TableAdapter geradas não são classes aninhadas de <xref:System.Data.DataSet> . Os TableAdapters estão localizados em um namespace com base no nome do DataSet associado do TableAdapter. Por exemplo, se seu aplicativo contiver um conjunto de um DataSet chamado `HRDataSet` , os TableAdapters estarão localizados no `HRDataSetTableAdapters` namespace. (A Convenção de nomenclatura segue este padrão: *DataSetName*  +  `TableAdapters` ).

O exemplo a seguir pressupõe que um TableAdapter nomeado `CustomersTableAdapter` está em um projeto com `NorthwindDataSet` .

### <a name="to-create-a-partial-class-for-a-tableadapter"></a>Para criar uma classe parcial para um TableAdapter

1. Adicione uma nova classe ao seu projeto acessando o menu **projeto** e selecionando **Adicionar classe**.

2. Nome da classe `CustomersTableAdapterExtended`.

3. Selecione **Adicionar**.

4. Substitua o código pelo namespace correto e o nome da classe parcial do seu projeto da seguinte maneira:

     [!code-csharp[VbRaddataTableAdapters#2](../data-tools/codesnippet/CSharp/extend-the-functionality-of-a-tableadapter_1.cs)]
     [!code-vb[VbRaddataTableAdapters#2](../data-tools/codesnippet/VisualBasic/extend-the-functionality-of-a-tableadapter_1.vb)]

## <a name="see-also"></a>Veja também

- [Preencher conjuntos de dados usando TableAdapters](../data-tools/fill-datasets-by-using-tableadapters.md)
