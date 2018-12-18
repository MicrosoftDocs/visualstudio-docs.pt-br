---
title: Adicionar validação a um conjunto de dados de n camadas | Microsoft Docs
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
- n-tier applications, validating
- validation [Visual Basic], n-tier data applications
- validating n-tier data applications
ms.assetid: 34ce4db6-09bb-4b46-b435-b2514aac52d3
caps.latest.revision: 27
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: a0f7c21dcffb7c17f859d79d3aed5522beb14acf
ms.sourcegitcommit: d462dd10746624ad139f1db04edd501e7737d51e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50220528"
---
# <a name="add-validation-to-an-n-tier-dataset"></a>Adicionar validação a um conjunto de dados de n camadas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Adicionando validação a um conjunto de dados que é separado em uma solução de n camadas é basicamente o mesmo que adicionar validação a um conjunto de dados de arquivo único (um conjunto de dados em um único projeto). O local sugerido para executar a validação nos dados é durante o <xref:System.Data.DataTable.ColumnChanging> e/ou <xref:System.Data.DataTable.RowChanging> eventos de uma tabela de dados.  
  
 O [criando e editando conjuntos de dados tipados](../data-tools/creating-and-editing-typed-datasets.md) fornece a funcionalidade para criar classes parciais para o qual você pode adicionar código de usuário para a coluna e linha – eventos das tabelas de dados no conjunto de dados de alteração. Para obter mais informações sobre como adicionar código a um conjunto de dados em uma solução de n camadas, consulte [adicione o código a conjuntos de dados em aplicativos de n camadas](../data-tools/add-code-to-datasets-in-n-tier-applications.md), e [adicionar código a TableAdapters em aplicativos de n camadas](../data-tools/add-code-to-tableadapters-in-n-tier-applications.md). Para obter mais informações sobre classes parciais, consulte [como: dividir uma classe em Classes parciais (Designer de classe)](../ide/how-to-split-a-class-into-partial-classes-class-designer.md) ou [Classes e métodos parciais](http://msdn.microsoft.com/library/804cecb7-62db-4f97-a99f-60975bd59fa1).  
  
> [!NOTE]
>  Quando você separa os conjuntos de dados de TableAdapters (Configurando o **projeto DataSet** propriedade), classes parciais do conjunto de dados existentes no projeto não serão movidas automaticamente. Classes parciais do conjunto de dados existente devem ser movidas manualmente para o projeto de conjunto de dados.  
  
> [!NOTE]
>  O Designer de conjunto de dados não cria automaticamente manipuladores de eventos em c# para o <xref:System.Data.DataTable.ColumnChanging> e <xref:System.Data.DataTable.RowChanging> eventos. Você precisa criar um manipulador de eventos manualmente e conectar o manipulador de eventos ao evento subjacente. Os procedimentos a seguir descrevem como criar manipuladores de eventos necessários no Visual Basic e c#.  
  
## <a name="validatechanges-to-individual-columns"></a>Validatechanges para colunas individuais  
 Valide os valores em colunas individuais manipulando o <xref:System.Data.DataTable.ColumnChanging> eventos. O <xref:System.Data.DataTable.ColumnChanging> é gerado quando um valor em uma coluna é modificado. Crie um manipulador de eventos para o <xref:System.Data.DataTable.ColumnChanging> evento clicando duas vezes na coluna desejada na [criando e editando conjuntos de dados tipados](../data-tools/creating-and-editing-typed-datasets.md).  
  
 Na primeira vez que você clique duas vezes em uma coluna, o designer gera um manipulador de eventos para o <xref:System.Data.DataTable.ColumnChanging> eventos. Um `If…Then` instrução também é criada que testa a coluna específica. Por exemplo, o código a seguir é gerado quando você clica duas vezes a coluna RequiredDate na tabela Orders do Northwind:  
  
```vb  
Private Sub OrdersDataTable_ColumnChanging(ByVal sender As System.Object, ByVal e As System.Data.DataColumnChangeEventArgs) Handles Me.ColumnChanging  
    If (e.Column.ColumnName = Me.RequiredDateColumn.ColumnName) Then  
        ' Add validation code here.  
    End If  
End Sub  
```  
  
> [!NOTE]
>  Em projetos c#, o Designer de conjunto de dados só cria classes parciais para o conjunto de dados e tabelas individuais no conjunto de dados. O Designer de conjunto de dados não cria automaticamente manipuladores de eventos para o <xref:System.Data.DataTable.ColumnChanging> e <xref:System.Data.DataTable.RowChanging> eventos no c#, como ele faz no Visual Basic. Em projetos c#, você precisa criar manualmente um método para manipular o evento e conectar o método ao evento subjacente. O procedimento a seguir fornece as etapas para criar os manipuladores de eventos necessários no Visual Basic e c#.  
  
 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]  
  
#### <a name="to-add-validation-during-changes-to-individual-column-values"></a>Para adicionar validação durante alterações a valores de colunas individuais  
  
1.  Abra o conjunto de dados a [criando e editando conjuntos de dados tipados](../data-tools/creating-and-editing-typed-datasets.md) clicando duas vezes o **. xsd** de arquivo no **Gerenciador de soluções**. Para obter mais informações, consulte [como: abrir um conjunto de dados no Designer de conjunto de dados](http://msdn.microsoft.com/library/36fc266f-365b-42cb-aebb-c993dc2c47c3).  
  
2.  Clique duas vezes a coluna que você deseja validar. Essa ação cria o <xref:System.Data.DataTable.ColumnChanging> manipulador de eventos.  
  
    > [!NOTE]
    >  O Designer de conjunto de dados não cria automaticamente um manipulador de eventos para o evento em C#. O código que é necessário para manipular o evento em c# está incluído na próxima seção. `SampleColumnChangingEvent` é criado e, em seguida, conectado à <xref:System.Data.DataTable.ColumnChanging> evento no <xref:System.Data.DataTable.EndInit%2A> método.  
  
3.  Adicione código para verificar que `e.ProposedValue` contém dados que atenda aos requisitos do seu aplicativo. Se o valor proposto for inaceitável, configure a coluna para indicar que ele contém um erro.  
  
     O exemplo de código a seguir valida que o **quantidade** coluna contém mais do que 0. Se **quantidade** é menor que ou igual a 0, a coluna é definida como um erro. O `Else` cláusula limpa o erro se **quantidade** for maior que 0. O código no manipulador de eventos de alteração de coluna deve se parecer com o seguinte:  
  
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
    // C#  
    // Add this code to the DataTable   
    // partial class.  
  
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
  
## <a name="validatechanges-to-whole-rows"></a>Validatechanges em linhas inteiras  
 Valide os valores em todas as linhas manipulando o <xref:System.Data.DataTable.RowChanging> eventos. O <xref:System.Data.DataTable.RowChanging> evento é gerado quando os valores em todas as colunas são confirmados. É necessário validar no <xref:System.Data.DataTable.RowChanging> evento quando o valor em uma coluna depende do valor em outra coluna. Por exemplo, considere OrderDate e RequiredDate na tabela de pedidos no Northwind.  
  
 Quando os pedidos estão sendo inseridos, validação garante que um pedido não é inserido com uma RequiredDate é igual ou anterior à OrderDate. Neste exemplo, os valores para colunas de RequiredDate e OrderDate precisam ser comparadas, para que validar uma alteração de coluna individual não faz sentido.  
  
 Crie um manipulador de eventos para o <xref:System.Data.DataTable.RowChanging> evento clicando duas vezes no nome da tabela na barra de título da tabela na [criando e editando conjuntos de dados tipados](../data-tools/creating-and-editing-typed-datasets.md).  
  
#### <a name="to-add-validation-during-changes-to-whole-rows"></a>Para adicionar a validação durante alterações em linhas inteiras  
  
1.  Abra o conjunto de dados a [criando e editando conjuntos de dados tipados](../data-tools/creating-and-editing-typed-datasets.md) clicando duas vezes o **. xsd** de arquivo no **Gerenciador de soluções**. Para obter mais informações, consulte [como: abrir um conjunto de dados no Designer de conjunto de dados](http://msdn.microsoft.com/library/36fc266f-365b-42cb-aebb-c993dc2c47c3).  
  
2.  Clique duas vezes a barra de título da tabela de dados no designer.  
  
     Uma classe parcial é criada com um `RowChanging` manipulador de eventos e é aberto no Editor de códigos.  
  
    > [!NOTE]
    >  O Designer de conjunto de dados não cria automaticamente um manipulador de eventos para o <xref:System.Data.DataTable.RowChanging> eventos em projetos c#. Você precisa criar um método para manipular o <xref:System.Data.DataTable.RowChanging> eventos e executar código para ligar o evento no método de inicialização da tabela.  
  
3.  Adicione o código do usuário dentro da declaração de classe parcial.  
  
4.  O código a seguir mostra onde adicionar código de usuário para validação durante o <xref:System.Data.DataTable.RowChanging> eventos para o Visual Basic:  
  
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
  
5.  O código a seguir mostra como criar o `RowChanging` manipulador de eventos e onde adicionar código de usuário para validação durante o <xref:System.Data.DataTable.RowChanging> evento para c#:  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Visão geral dos aplicativos de dados de N camadas](../data-tools/n-tier-data-applications-overview.md)   
 [Passo a passo: Criando um aplicativo de dados de N camadas](../data-tools/walkthrough-creating-an-n-tier-data-application.md)   
 [Validando dados em conjuntos de dados](../data-tools/validate-data-in-datasets.md)

