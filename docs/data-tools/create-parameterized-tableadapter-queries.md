---
title: Criar consultas TableAdapter parametrizadas
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Visual Studio], TableAdapters
- TableAdapters, parameterized queries
- data [Visual Studio], searching data
- queries [Visual Studio], creating
- TableAdapters, searching data
- queries [Visual Studio], TableAdapters
ms.assetid: 104d1d19-b5a9-4071-b81e-1b3af08e9c7b
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: a2b94e10dd09d26a17a7574db97880567f7725cd
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85282599"
---
# <a name="create-parameterized-tableadapter-queries"></a>Criar consultas TableAdapter parametrizadas

Uma consulta parametrizada retorna dados que atendem às condições de uma cláusula WHERE dentro da consulta. Por exemplo, você pode parametrizar uma lista de clientes para exibir apenas clientes em uma determinada cidade, adicionando `WHERE City = @City` ao final da instrução SQL que retorna uma lista de clientes.

Você cria consultas de TableAdapter com parâmetros no **Designer de conjunto de dados**. Você também pode criá-los em um aplicativo do Windows com o comando **parametrizar fonte de dados** no menu **dados** . O comando **parametrizar fonte de dados** cria controles no formulário onde você pode inserir os valores de parâmetro e executar a consulta.

> [!NOTE]
> Ao construir uma consulta parametrizada, use a notação de parâmetro específica para o banco de dados com o qual você está codificando. Por exemplo, acesso e fontes dados OleDb usam o ponto de interrogação '?' para denotar parâmetros, portanto, a cláusula WHERE seria algo como: `WHERE City = ?`.

## <a name="create-a-parameterized-tableadapter-query"></a>Criar uma consulta TableAdapter parametrizada

### <a name="to-create-a-parameterized-query-in-the-dataset-designer"></a>Para criar uma consulta parametrizada no Designer de Conjunto de Dados

- Crie um novo TableAdapter, adicionando uma cláusula WHERE com os parâmetros desejados à instrução SQL. Para obter mais informações, consulte [criar e configurar TableAdapters](../data-tools/create-and-configure-tableadapters.md).

     -ou-

- Acrescente uma consulta a um TableAdapter existente, adicionando uma cláusula WHERE com os parâmetros desejados à instrução SQL.

### <a name="to-create-a-parameterized-query-while-designing-a-data-bound-form"></a>Para criar uma consulta parametrizada durante a criação de um formulário com associação de dados

1. Selecione um controle no seu formulário que já esteja associado a um conjunto de dados. Para obter mais informações, consulte [associar controles de Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md).

2. No menu **dados** , selecione **Adicionar consulta**.

3. Preencha a caixa de diálogo **Pesquisar Construtor de Critérios**, adicionando uma cláusula WHERE com os parâmetros desejados à instrução SQL.

### <a name="to-add-a-query-to-an-existing-data-bound-form"></a>Adicionar uma consulta a um formulário associado a dados existente

1. Abra o formulário no **Designer de Formulários do Windows**.

2. No menu **dados** , selecione Adicionar **marcas inteligentes**de **consulta** ou de dados.

    > [!NOTE]
    > Se **Adicionar Consulta** não estiver disponível no menu **Dados**, selecione um controle no formulário que exibe a fonte de dados no qual deseja adicionar a parametrização. Por exemplo, se o formulário exibir dados em um controle <xref:System.Windows.Forms.DataGridView>, selecione-o. Se o formulário exibir dados em controles individuais, selecione qualquer controle associado a dados.

3. Na área **selecionar tabela de fonte de dados** , selecione a tabela à qual você deseja adicionar a parametrização.

4. Digite um nome na caixa **Nome da nova consulta** ao criar uma nova consulta.

     -ou-

     Selecione uma consulta na caixa **Nome da consulta existente**.

5. Na caixa de **texto consulta** , digite uma consulta que aceite parâmetros.

6. Selecione **OK**.

     Um controle para inserir o parâmetro e um botão **Carregar** são adicionados ao formulário em um controle <xref:System.Windows.Forms.ToolStrip>.

### <a name="query-for-null-values"></a>Consultar valores nulos

Os parâmetros do TableAdapter podem ser atribuídos a valores nulos quando você deseja consultar registros que não têm valor atual. Por exemplo, considere a seguinte consulta que tem um `ShippedDate` parâmetro em sua `WHERE` cláusula:

```sql
SELECT CustomerID, OrderDate, ShippedDate
FROM Orders
WHERE (ShippedDate = @ShippedDate) OR (ShippedDate IS NULL)
```

Se essa fosse uma consulta em um TableAdapter, você poderia consultar todos os pedidos que não foram enviados com o seguinte código:

[!code-csharp[VbRaddataTableAdapters#8](../data-tools/codesnippet/CSharp/create-parameterized-tableadapter-queries_1.cs)]
[!code-vb[VbRaddataTableAdapters#8](../data-tools/codesnippet/VisualBasic/create-parameterized-tableadapter-queries_1.vb)]

Para habilitar uma consulta para aceitar valores nulos:

1. Na **Designer de conjunto de dados**, selecione a consulta do TableAdapter que precisa aceitar valores de parâmetro nulos.

2. Na janela **Propriedades** , selecione **parâmetros**e clique no botão de reticências (**...**) para abrir o **Editor de coleção de parâmetros**.

3. Selecione o parâmetro que permite valores nulos e defina a propriedade **AllowDBNull** como `true` .

## <a name="see-also"></a>Veja também

- [Preencher conjuntos de dados usando TableAdapters](../data-tools/fill-datasets-by-using-tableadapters.md)
