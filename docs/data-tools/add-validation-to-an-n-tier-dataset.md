---
title: Adicionar validação a um conjunto de dados de n camadas
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- n-tier applications, validating
- validation [Visual Basic], n-tier data applications
- validating n-tier data applications
ms.assetid: 34ce4db6-09bb-4b46-b435-b2514aac52d3
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 91dbe04c85491a38a221edfb064702085136780f
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85283015"
---
# <a name="add-validation-to-an-n-tier-dataset"></a>Adicionar validação a um conjunto de dados de n camadas
Adicionar validação a um conjunto de um DataSet que é separado em uma solução de n camadas é basicamente o mesmo que adicionar validação a um conjunto de um único arquivo (um conjunto de um DataSet em um único projeto). O local sugerido para executar a validação nos dados é durante os <xref:System.Data.DataTable.ColumnChanging> eventos e/ou <xref:System.Data.DataTable.RowChanging> de uma tabela de dados.

O conjunto de dados fornece a funcionalidade para criar classes parciais para as quais você pode adicionar o código do usuário a eventos de alteração de coluna e linha das tabelas de dados no DataSet. Para obter mais informações sobre como adicionar código a um conjunto de dados em uma solução de n camadas, consulte [Adicionar código a conjuntos de dados em aplicativos de n camadas](../data-tools/add-code-to-datasets-in-n-tier-applications.md)e [Adicionar código a TableAdapters em aplicativos de n camadas](../data-tools/add-code-to-tableadapters-in-n-tier-applications.md). Para obter mais informações sobre classes parciais, consulte [como dividir uma classe em classes parciais (Designer de classe) ou em](../ide/class-designer/how-to-split-a-class-into-partial-classes.md) [classes e métodos parciais](/dotnet/csharp/programming-guide/classes-and-structs/partial-classes-and-methods).

> [!NOTE]
> Quando você separa conjuntos de valores de TableAdapters (definindo a propriedade de **projeto DataSet** ), as classes parciais DataSet existentes no projeto não serão movidas automaticamente. As classes parciais de DataSet existentes devem ser movidas manualmente para o projeto DataSet.

> [!NOTE]
> O DataSet Designer não cria automaticamente manipuladores de eventos em C# para os <xref:System.Data.DataTable.ColumnChanging> <xref:System.Data.DataTable.RowChanging> eventos e. Você precisa criar manualmente um manipulador de eventos e conectar o manipulador de eventos ao evento subjacente. Os procedimentos a seguir descrevem como criar os manipuladores de eventos necessários no Visual Basic e no C#.

## <a name="validate-changes-to-individual-columns"></a>Validar alterações em colunas individuais
Valide os valores em colunas individuais manipulando o <xref:System.Data.DataTable.ColumnChanging> evento. O <xref:System.Data.DataTable.ColumnChanging> evento é gerado quando um valor em uma coluna é modificado. Crie um manipulador de eventos para o <xref:System.Data.DataTable.ColumnChanging> evento clicando duas vezes na coluna desejada na **Designer de conjunto de dados**.

Na primeira vez que você clicar duas vezes em uma coluna, o designer gerará um manipulador de eventos para o <xref:System.Data.DataTable.ColumnChanging> evento. `If...Then`Também é criada uma instrução que testa a coluna específica. Por exemplo, o código a seguir é gerado quando você clica duas vezes na coluna **DataDeEntrega** na tabela pedidos do Northwind:

```vb
Private Sub OrdersDataTable_ColumnChanging(ByVal sender As System.Object, ByVal e As System.Data.DataColumnChangeEventArgs) Handles Me.ColumnChanging
    If (e.Column.ColumnName = Me.RequiredDateColumn.ColumnName) Then
        ' Add validation code here.
    End If
End Sub
```

> [!NOTE]
> Em projetos C#, o Designer de Conjunto de Dados cria apenas classes parciais para o conjunto de e tabelas individuais no DataSet. O Designer de Conjunto de Dados não cria automaticamente manipuladores de eventos para os <xref:System.Data.DataTable.ColumnChanging> <xref:System.Data.DataTable.RowChanging> eventos e em C#, como no Visual Basic. Em projetos C#, você precisa construir manualmente um método para manipular o evento e vincular o método ao evento subjacente. O procedimento a seguir fornece as etapas para criar os manipuladores de eventos necessários no Visual Basic e no C#.

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

#### <a name="to-add-validation-during-changes-to-individual-column-values"></a>Para adicionar validação durante alterações em valores de coluna individuais

1. Abra o conjunto de um clicando duas vezes no arquivo *. xsd* em **Gerenciador de soluções**. Para obter mais informações, consulte [Walkthrough: Criando um conjunto de dados no designer de conjunto de dados](walkthrough-creating-a-dataset-with-the-dataset-designer.md).

2. Clique duas vezes na coluna que você deseja validar. Essa ação cria o <xref:System.Data.DataTable.ColumnChanging> manipulador de eventos.

    > [!NOTE]
    > O Designer de Conjunto de Dados não cria automaticamente um manipulador de eventos para o evento C#. O código necessário para lidar com o evento em C# está incluído na próxima seção. `SampleColumnChangingEvent`é criado e conectado ao <xref:System.Data.DataTable.ColumnChanging> evento no <xref:System.Data.DataTable.EndInit%2A> método.

3. Adicione o código para verificar se `e.ProposedValue` contém dados que atendem aos requisitos do seu aplicativo. Se o valor proposto for inaceitável, defina a coluna para indicar que ela contém um erro.

     O exemplo de código a seguir valida que a coluna **Quantity** contém um valor maior que 0. Se **Quantity** for menor ou igual a 0, a coluna será definida como um erro. A `Else` cláusula limpará o erro se **Quantity** for maior que 0. O código no manipulador de eventos de alteração de coluna deve ser semelhante ao seguinte:

    ```vb
    If (e.Column.ColumnName = Me.QuantityColumn.ColumnName) Then
        If CType(e.ProposedValue, Short) <= 0 Then
            e.Row.SetColumnError(e.Column, "Quantity must be greater than 0")
        Else
            e.Row.SetColumnError(e.Column, "")
        End If
    End If
    ```

    ```csharp
    // Add this code to the DataTable partial class.

    public override void EndInit()
    {
        base.EndInit();
        // Hook up the ColumnChanging event
        // to call the SampleColumnChangingEvent method.
        ColumnChanging += SampleColumnChangingEvent;
    }

    public void SampleColumnChangingEvent(object sender, System.Data.DataColumnChangeEventArgs e)
    {
        if (e.Column.ColumnName == QuantityColumn.ColumnName)
        {
            if ((short)e.ProposedValue <= 0)
            {
                e.Row.SetColumnError("Quantity", "Quantity must be greater than 0");
            }
            else
            {
                e.Row.SetColumnError("Quantity", "");
            }
        }
    }
    ```

## <a name="validate-changes-to-whole-rows"></a>Validar alterações em linhas inteiras
Valide os valores em linhas inteiras manipulando o <xref:System.Data.DataTable.RowChanging> evento. O <xref:System.Data.DataTable.RowChanging> evento é gerado quando os valores em todas as colunas são confirmados. É necessário validar no <xref:System.Data.DataTable.RowChanging> evento quando o valor em uma coluna depende do valor em outra coluna. Por exemplo, considere OrderDate e DataDeEntrega na tabela Orders no Northwind.

Quando os pedidos são inseridos, a validação garante que um pedido não seja inserido com uma DataDeEntrega que esteja em ou antes da DataDoPedido. Neste exemplo, os valores para as colunas DataDeEntrega e DataDoPedido precisam ser comparados, portanto, a validação de uma alteração de coluna individual não faz sentido.

Crie um manipulador de eventos para o <xref:System.Data.DataTable.RowChanging> evento clicando duas vezes no nome da tabela na barra de título da tabela no **Designer de conjunto de dados**.

#### <a name="to-add-validation-during-changes-to-whole-rows"></a>Para adicionar validação durante alterações em linhas inteiras

1. Abra o conjunto de um clicando duas vezes no arquivo *. xsd* em **Gerenciador de soluções**. Para obter mais informações, consulte [Walkthrough: Criando um conjunto de dados no designer de conjunto de dados](walkthrough-creating-a-dataset-with-the-dataset-designer.md).

2. Clique duas vezes na barra de título da tabela de dados no designer.

     Uma classe parcial é criada com um `RowChanging` manipulador de eventos e é aberta no editor de código.

    > [!NOTE]
    > O Designer de Conjunto de Dados não cria automaticamente um manipulador de eventos para o <xref:System.Data.DataTable.RowChanging> evento em projetos C#. Você precisa criar um método para manipular o <xref:System.Data.DataTable.RowChanging> evento e executar o código e, em seguida, vincular o evento no método de inicialização da tabela.

3. Adicione o código de usuário dentro da declaração de classe parcial.

4. O código a seguir mostra onde adicionar o código de usuário para validar durante o <xref:System.Data.DataTable.RowChanging> evento. O exemplo de C# também inclui código para vincular o método manipulador de eventos ao `OrdersRowChanging` evento.

    ```vb
    Partial Class OrdersDataTable
        Private Sub OrdersDataTable_OrdersRowChanging(ByVal sender As System.Object, ByVal e As OrdersRowChangeEvent) Handles Me.OrdersRowChanging
            ' Add logic to validate columns here.
            If e.Row.RequiredDate <= e.Row.OrderDate Then
                ' Set the RowError if validation fails.
                e.Row.RowError = "Required Date cannot be on or before the OrderDate"
            Else
                ' Clear the RowError when validation passes.
                e.Row.RowError = ""
            End If
        End Sub
    End Class
    ```

    ```csharp
    partial class OrdersDataTable
    {
        public override void EndInit()
        {
            base.EndInit();
            // Hook up the event to the
            // RowChangingEvent method.
            OrdersRowChanging += RowChangingEvent;
        }

        public void RowChangingEvent(object sender, OrdersRowChangeEvent e)
        {
            // Perform the validation logic.
            if (e.Row.RequiredDate <= e.Row.OrderDate)
            {
                // Set the row to an error when validation fails.
                e.Row.RowError = "Required Date cannot be on or before the OrderDate";
            }
            else
            {
                // Clear the RowError if validation passes.
                e.Row.RowError = "";
            }
        }
    }
    ```

## <a name="see-also"></a>Veja também

- [Visão geral de aplicativos de dados de N camadas](../data-tools/n-tier-data-applications-overview.md)
- [Walkthrough: Criando um aplicativo de dados de N camadas](../data-tools/walkthrough-creating-an-n-tier-data-application.md)
- [Validando dados em conjuntos de dados](../data-tools/validate-data-in-datasets.md)
