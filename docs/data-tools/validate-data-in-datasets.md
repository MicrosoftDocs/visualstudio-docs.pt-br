---
title: Validar dados em conjuntos de dados
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- DataTable.ColumnChanging
- System.Data.DataTable.ColumnChanging
- System.Data.DataTable.RowChanging
- DataTable.RowChanging
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data validation, datasets
- data validation
- validating data, datasets
- updating datasets, validating data
ms.assetid: 79500596-1e4d-478e-a991-a636fd73a622
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 5a0a8846719c6ad57e65e1e308e9884e81e1997d
ms.sourcegitcommit: f37affbc1b885dfe246d4b2c295a6538b383a0ca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37174716"
---
# <a name="validate-data-in-datasets"></a>Validar dados em conjuntos de dados
Validação de dados é o processo de confirmar que os valores que estão sendo inseridos em objetos de dados estão em conformidade com as restrições no esquema do conjunto de dados. O processo de validação também confirma que esses valores são seguindo as regras que foram estabelecidas para seu aplicativo. É uma boa prática para validar dados antes de enviar atualizações para o banco de dados subjacente. Isso reduz os erros, bem como o número potencial de processamentos entre um aplicativo e o banco de dados.

Você pode confirmar que os dados que está sendo gravados em um conjunto de dados são válidos, criando verificações de validação no conjunto de dados em si. O conjunto de dados pode verificar os dados, independentemente de como a atualização está sendo executada — se diretamente pelos controles em um formulário, dentro de um componente, ou de alguma outra forma. Como o conjunto de dados é parte do seu aplicativo (ao contrário de back-end do banco de dados), é um lugar lógico para compilação de validação específica do aplicativo.

É o melhor lugar para adicionar validação ao seu aplicativo no arquivo de classe parcial do conjunto de dados. Na [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] ou [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)], abra o **Dataset Designer** e clique duas vezes na coluna ou tabela para a qual você deseja criar a validação. Essa ação cria automaticamente um <xref:System.Data.DataTable.ColumnChanging> ou <xref:System.Data.DataTable.RowChanging> manipulador de eventos.

## <a name="validate-data"></a>Validar dados
 Validação dentro de um conjunto de dados é feita das seguintes maneiras:

-   Criando sua própria validação específica de aplicativo que pode verificar valores em uma coluna de dados individuais durante alterações. Para obter mais informações, consulte [como: validar dados durante alterações de coluna](validate-data-in-datasets.md).

-   Criando sua própria validação de específicos do aplicativo que pode verificar valores de um inteiro de dados está mudando a linha. Para obter mais informações, consulte [como: validar dados durante alterações de linha](validate-data-in-datasets.md).

-   Criando chaves, restrições exclusivas, e assim por diante como parte da definição de esquema real do conjunto de dados.

-   Definindo as propriedades do <xref:System.Data.DataColumn> objeto, como <xref:System.Data.DataColumn.MaxLength%2A>, <xref:System.Data.DataColumn.AllowDBNull%2A>, e <xref:System.Data.DataColumn.Unique%2A>.

Vários eventos são gerados pelo <xref:System.Data.DataTable> quando uma alteração está ocorrendo em um registro de objeto:

-   O <xref:System.Data.DataTable.ColumnChanging> e <xref:System.Data.DataTable.ColumnChanged> eventos são gerados durante e após cada alteração em uma coluna individual. O <xref:System.Data.DataTable.ColumnChanging> evento é útil quando você deseja validar alterações em colunas específicas. Informações sobre a alteração proposta são passadas como um argumento com o evento.
-   O <xref:System.Data.DataTable.RowChanging> e <xref:System.Data.DataTable.RowChanged> eventos são gerados durante e após qualquer alteração em uma linha. O <xref:System.Data.DataTable.RowChanging> evento é mais geral. Ele indica que uma alteração está ocorrendo em algum lugar na linha, mas você não souber qual coluna foi alterada.

Por padrão, cada alteração em uma coluna, portanto, gera quatro eventos. A primeira é a <xref:System.Data.DataTable.ColumnChanging> e <xref:System.Data.DataTable.ColumnChanged> eventos para a coluna específica que está sendo alterado. Em seguida, estão os <xref:System.Data.DataTable.RowChanging> e <xref:System.Data.DataTable.RowChanged> eventos. Se várias alterações estão sendo feitas para a linha, os eventos serão gerados para cada alteração.

> [!NOTE]
>  A linha de dados <xref:System.Data.DataRow.BeginEdit%2A> método desativa a <xref:System.Data.DataTable.RowChanging> e <xref:System.Data.DataTable.RowChanged> eventos após cada alteração de coluna individual. Nesse caso, o evento não é gerado até que o <xref:System.Data.DataRow.EndEdit%2A> método foi chamado, quando o <xref:System.Data.DataTable.RowChanging> e <xref:System.Data.DataTable.RowChanged> eventos são gerados apenas uma vez. Para obter mais informações, consulte [desativar restrições ao preencher um conjunto de dados](../data-tools/turn-off-constraints-while-filling-a-dataset.md).

O evento que você escolher depende de quão granular que você deseja que seja a validação. Se for importante que você atualize um erro imediatamente quando uma coluna é alterado, validação de build usando o <xref:System.Data.DataTable.ColumnChanging> eventos. Caso contrário, use o <xref:System.Data.DataTable.RowChanging> evento, que pode resultar na captura de vários erros ao mesmo tempo. Além disso, se seus dados são estruturados de modo que o valor de uma coluna é validado com base no conteúdo de outra coluna, executar a validação durante o <xref:System.Data.DataTable.RowChanging> eventos.

Quando registros são atualizados, o <xref:System.Data.DataTable> objeto gera eventos que você pode responder enquanto alterações estão ocorrendo e depois que as alterações forem feitas.

Se seu aplicativo usa um conjunto de dados tipado, você pode criar manipuladores de eventos com rigidez de tipos. Isso adiciona quatro eventos tipados para a qual você pode criar manipuladores: `dataTableNameRowChanging`, `dataTableNameRowChanged`, `dataTableNameRowDeleting`, e `dataTableNameRowDeleted`. Esses manipuladores de eventos tipado passam um argumento que inclui os nomes de coluna da tabela que tornam mais fácil de escrever e ler o código.

## <a name="data-update-events"></a>Eventos de atualização de dados

|evento|Descrição|
|-----------|-----------------|
|<xref:System.Data.DataTable.ColumnChanging>|O valor em uma coluna está sendo alterado. O evento passa a linha e coluna para você, juntamente com o novo valor proposto.|
|<xref:System.Data.DataTable.ColumnChanged>|O valor em uma coluna foi alterado. O evento passa a linha e coluna para você, juntamente com o valor proposto.|
|<xref:System.Data.DataTable.RowChanging>|As alterações que foram feitas em um <xref:System.Data.DataRow> objeto está prestes a ser confirmadas de volta para o conjunto de dados. Se você não tiver chamado de <xref:System.Data.DataRow.BeginEdit%2A> método, o <xref:System.Data.DataTable.RowChanging> é gerado para cada alteração em uma coluna imediatamente após o <xref:System.Data.DataTable.ColumnChanging> evento foi gerado. Se você chamasse <xref:System.Data.DataRow.BeginEdit%2A> antes de fazer alterações, o <xref:System.Data.DataTable.RowChanging> é gerado somente quando você chama o <xref:System.Data.DataRow.EndEdit%2A> método.<br /><br /> O evento passa a linha para você, juntamente com um valor que indica o tipo de ação (alteração, inserção e assim por diante) que está sendo executado.|
|<xref:System.Data.DataTable.RowChanged>|Uma linha foi alterada. O evento passa a linha para você, juntamente com um valor que indica o tipo de ação (alteração, inserção e assim por diante) que está sendo executado.|
|<xref:System.Data.DataTable.RowDeleting>|Uma linha está sendo excluída. O evento passa a linha para você, juntamente com um valor que indica o tipo de ação (excluir) está sendo executado.|
|<xref:System.Data.DataTable.RowDeleted>|Uma linha foi excluída. O evento passa a linha para você, juntamente com um valor que indica o tipo de ação (excluir) está sendo executado.|

O <xref:System.Data.DataTable.ColumnChanging>, <xref:System.Data.DataTable.RowChanging>, e <xref:System.Data.DataTable.RowDeleting> eventos são gerados durante o processo de atualização. Você pode usar esses eventos para validar dados ou executar outros tipos de processamento. Como a atualização está em processo durante esses eventos, você poderá cancelá-lo lançando uma exceção, que impede a atualização terminar.

O <xref:System.Data.DataTable.ColumnChanged>, <xref:System.Data.DataTable.RowChanged> e <xref:System.Data.DataTable.RowDeleted> eventos são eventos de notificação que são gerados quando a atualização foi concluída com êxito. Esses eventos são úteis quando você deseja fazer outra ação com base em uma atualização bem-sucedida.

## <a name="validate-data-during-column-changes"></a>Validar dados durante alterações de coluna

> [!NOTE]
>  O **Dataset Designer** cria uma classe parcial na qual a validação lógica pode ser adicionada a um conjunto de dados. O conjunto de dados gerado pelo designer não exclua nem altere qualquer código na classe parcial.

Você pode validar dados quando o valor em uma coluna de dados é alterado respondendo ao <xref:System.Data.DataTable.ColumnChanging> eventos. Quando gerado, esse evento passa um argumento de evento (<xref:System.Data.DataColumnChangeEventArgs.ProposedValue%2A>) que contém o valor proposto para a coluna atual. Com base no conteúdo de `e.ProposedValue`, você pode:

-   Aceite o valor proposto, sem fazer nada.

-   Rejeitar o valor proposto, definindo o erro de coluna (<xref:System.Data.DataRow.SetColumnError%2A>) de dentro do manipulador de eventos de alteração de coluna.

-   Opcionalmente, usar um <xref:System.Windows.Forms.ErrorProvider> controle para exibir uma mensagem de erro para o usuário. Para obter mais informações, consulte [componente ErrorProvider](/dotnet/framework/winforms/controls/errorprovider-component-windows-forms).

Validação também pode ser executada durante a <xref:System.Data.DataTable.RowChanging> eventos.

## <a name="validate-data-during-row-changes"></a>Validar dados durante alterações de linha
Você pode escrever código para verificar se cada coluna que você deseja validar contém dados que atenda aos requisitos do seu aplicativo. Para fazer isso definindo a coluna para indicar que ele contém um erro se um valor proposto for inaceitável. Os exemplos a seguir definem um erro de coluna quando o `Quantity` coluna é 0 ou menos. Os manipuladores de eventos de alteração de linha devem se parecer com os exemplos a seguir.

### <a name="to-validate-data-when-a-row-changes-visual-basic"></a>Para validar dados quando uma linha é alterado (Visual Basic)

1.  Abra o dataset na **Dataset Designer**. Para obter mais informações, consulte [instruções passo a passo: Criando um conjunto de dados no Designer de conjunto de dados](walkthrough-creating-a-dataset-with-the-dataset-designer.md).

2.  Clique duas vezes a barra de título da tabela que você deseja validar. Essa ação cria automaticamente o <xref:System.Data.DataTable.RowChanging> manipulador de eventos do <xref:System.Data.DataTable> no arquivo de classe parcial do conjunto de dados.

    > [!TIP]
    >  Clique duas vezes à esquerda do nome da tabela para criar o manipulador de eventos de alteração de linha. Se você clicar duas vezes no nome da tabela, você pode editá-lo.

     [!code-vb[VbRaddataValidating#3](../data-tools/codesnippet/VisualBasic/validate-data-in-datasets_1.vb)]

### <a name="to-validate-data-when-a-row-changes-c"></a>Para validar dados quando uma linha for alterada (c#)

1.  Abra o dataset na **Dataset Designer**. Para obter mais informações, consulte [instruções passo a passo: Criando um conjunto de dados no Designer de conjunto de dados](walkthrough-creating-a-dataset-with-the-dataset-designer.md).

2.  Clique duas vezes a barra de título da tabela que você deseja validar. Essa ação cria um arquivo de classe parcial para o <xref:System.Data.DataTable>.

    > [!NOTE]
    >  O **Dataset Designer** não cria automaticamente um manipulador de eventos para o <xref:System.Data.DataTable.RowChanging> eventos. Você precisa criar um método para manipular o <xref:System.Data.DataTable.RowChanging> eventos e executar código para ligar o evento no método de inicialização da tabela.

3.  Copie o código a seguir para a classe parcial:

    ```csharp
    public override void EndInit()
    {
        base.EndInit();
        Order_DetailsRowChanging += TestRowChangeEvent;
    }

    public void TestRowChangeEvent(object sender, Order_DetailsRowChangeEvent e)
    {
        if ((short)e.Row.Quantity <= 0)
        {
            e.Row.SetColumnError("Quantity", "Quantity must be greater than 0");
        }
        else
        {
            e.Row.SetColumnError("Quantity", "");
        }
    }
    ```

## <a name="to-retrieve-changed-rows"></a>Para recuperar linhas alteradas
Cada linha em uma tabela de dados tem um <xref:System.Data.DataRow.RowState%2A> que controla o estado atual da linha, usando os valores na propriedade de <xref:System.Data.DataRowState> enumeração. Você pode retornar linhas alteradas de uma conjunto de dados ou tabela de dados chamando o `GetChanges` método de um <xref:System.Data.DataSet> ou <xref:System.Data.DataTable>. Você pode verificar se existem alterações antes de chamar `GetChanges` chamando o <xref:System.Data.DataSet.HasChanges%2A> método de um conjunto de dados.

> [!NOTE]
>  Depois de confirmar as alterações para uma conjunto de dados ou tabela de dados (chamando o <xref:System.Data.DataSet.AcceptChanges%2A> método), o `GetChanges` método não retorna nenhum dado. Se seu aplicativo precisar processar linhas alteradas, você deve processar as alterações antes de chamar o `AcceptChanges` método.

Chamar o <xref:System.Data.DataSet.GetChanges%2A> método de um conjunto de dados ou tabela de dados retorna um novo conjunto de dados ou uma tabela que contém somente os registros que foram alterados. Se você quiser obter registros específicos — por exemplo, somente registros novos ou somente registros modificados — você pode passar um valor da <xref:System.Data.DataRowState> enumeração como um parâmetro para o `GetChanges` método.

Use o <xref:System.Data.DataRowVersion> enumeração para acessar as versões diferentes de uma linha (por exemplo, os valores originais que estavam em uma linha antes de processá-la).

### <a name="to-get-all-changed-records-from-a-dataset"></a>Para obter todos os registros alterados de um conjunto de dados

-   Chamar o <xref:System.Data.DataSet.GetChanges%2A> método de um conjunto de dados.

     O exemplo a seguir cria um novo conjunto de dados chamado `changedRecords` e a preenche com todos os registros alterados de outro conjunto de dados chamado `dataSet1`.

     [!code-csharp[VbRaddataEditing#14](../data-tools/codesnippet/CSharp/validate-data-in-datasets_2.cs)]
     [!code-vb[VbRaddataEditing#14](../data-tools/codesnippet/VisualBasic/validate-data-in-datasets_2.vb)]

### <a name="to-get-all-changed-records-from-a-data-table"></a>Para obter todos os registros alterados de uma tabela de dados

-   Chamar o <xref:System.Data.DataTable.GetChanges%2A> método de um DataTable.

     O exemplo a seguir cria uma nova tabela de dados chamada `changedRecordsTable` e a preenche com todos os registros alterados de outra tabela de dados chamada `dataTable1`.

     [!code-csharp[VbRaddataEditing#15](../data-tools/codesnippet/CSharp/validate-data-in-datasets_3.cs)]
     [!code-vb[VbRaddataEditing#15](../data-tools/codesnippet/VisualBasic/validate-data-in-datasets_3.vb)]

### <a name="to-get-all-records-that-have-a-specific-row-state"></a>Para obter todos os registros que têm um estado de linha específico

-   Chame o `GetChanges` método de um conjunto de dados ou tabela de dados e passe um <xref:System.Data.DataRowState> valor de enumeração como um argumento.

     O exemplo a seguir mostra como criar um novo conjunto de dados chamado `addedRecords` e preenchê-lo apenas com os registros que foram adicionados para o `dataSet1` conjunto de dados.

     [!code-csharp[VbRaddataEditing#16](../data-tools/codesnippet/CSharp/validate-data-in-datasets_4.cs)]
     [!code-vb[VbRaddataEditing#16](../data-tools/codesnippet/VisualBasic/validate-data-in-datasets_4.vb)]

     O exemplo a seguir mostra como retornar todos os registros que foram adicionados recentemente para o `Customers` tabela:

     [!code-csharp[VbRaddataEditing#17](../data-tools/codesnippet/CSharp/validate-data-in-datasets_5.cs)]
     [!code-vb[VbRaddataEditing#17](../data-tools/codesnippet/VisualBasic/validate-data-in-datasets_5.vb)]

## <a name="access-the-original-version-of-a-datarow"></a>Acessar a versão original de uma DataRow
Quando forem feitas alterações a linhas de dados, o conjunto de dados manterá tanto o original (<xref:System.Data.DataRowVersion.Original>) e new (<xref:System.Data.DataRowVersion.Current>) versões da linha. Por exemplo, antes de chamar o `AcceptChanges` método, seu aplicativo pode acessar as versões diferentes de um registro (conforme definido no <xref:System.Data.DataRowVersion> enumeração) e processar as alterações de acordo.

> [!NOTE]
>  Versões diferentes de uma linha existem somente após ela ter sido editada e antes que ele o `AcceptChanges` método foi chamado. Após o `AcceptChanges` método foi chamado, as versões atuais e originais são as mesmas.

Passando o <xref:System.Data.DataRowVersion> valor juntamente com o índice da coluna (ou o nome da coluna como uma cadeia de caracteres) retorna o valor da versão de linha específica da coluna. A coluna alterada é identificada durante o <xref:System.Data.DataTable.ColumnChanging> e <xref:System.Data.DataTable.ColumnChanged> eventos. Isso é um bom momento para inspecionar as versões de linha diferente para fins de validação. No entanto, se você suspendeu temporariamente as restrições, esses eventos não serão gerados e você precisará programaticamente identificar quais colunas foram alteradas. Você pode fazer isso ao iterar por meio de <xref:System.Data.DataTable.Columns%2A> coleta e comparar as diferentes <xref:System.Data.DataRowVersion> valores.

### <a name="to-get-the-original-version-of-a-record"></a>Para obter a versão original de um registro

-   Acessar o valor de uma coluna, passando o <xref:System.Data.DataRowVersion> da linha que você deseja retornar.

     O exemplo a seguir mostra como usar um <xref:System.Data.DataRowVersion> valor para obter o valor original de um `CompanyName` campo em um <xref:System.Data.DataRow>:

     [!code-csharp[VbRaddataEditing#21](../data-tools/codesnippet/CSharp/validate-data-in-datasets_6.cs)]
     [!code-vb[VbRaddataEditing#21](../data-tools/codesnippet/VisualBasic/validate-data-in-datasets_6.vb)]

## <a name="access-the-current-version-of-a-datarow"></a>Acessar a versão atual de um DataRow

### <a name="to-get-the-current-version-of-a-record"></a>Para obter a versão atual de um registro

-   Acessar o valor de uma coluna e, em seguida, adicione um parâmetro para o índice que indica qual versão de uma linha que você deseja retornar.

     O exemplo a seguir mostra como usar um <xref:System.Data.DataRowVersion> valor para obter o valor atual de um `CompanyName` campo em um <xref:System.Data.DataRow>:

     [!code-csharp[VbRaddataEditing#22](../data-tools/codesnippet/CSharp/validate-data-in-datasets_7.cs)]
     [!code-vb[VbRaddataEditing#22](../data-tools/codesnippet/VisualBasic/validate-data-in-datasets_7.vb)]

## <a name="see-also"></a>Consulte também

- [Ferramentas de conjunto de dados no Visual Studio](../data-tools/dataset-tools-in-visual-studio.md)
- [Como: validar dados no controle DataGridView do Windows Forms](/dotnet/framework/winforms/controls/how-to-validate-data-in-the-windows-forms-datagridview-control)
- [Como: exibir ícones de erro para validação do formulário com o componente ErrorProvider de formulários do Windows](/dotnet/framework/winforms/controls/display-error-icons-for-form-validation-with-wf-errorprovider)