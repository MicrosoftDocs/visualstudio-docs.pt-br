---
title: Editar dados em conjuntos de dados
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- datasets [Visual Basic], editing data
- data [Visual Studio], editing in datasets
ms.assetid: 50d5c580-fbf7-408f-be70-e63ac4f4d0eb
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: b51b5b4be12f76e2237ff93659617e1c1843722a
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/01/2020
ms.locfileid: "75586647"
---
# <a name="edit-data-in-datasets"></a>Editar dados em conjuntos de dados
Você edita dados em tabelas de dados da mesma forma que edita os dados em uma tabela em qualquer banco de dado. O processo pode incluir inserção, atualização e exclusão de registros na tabela. Em um formulário vinculado a dados, você pode especificar quais campos são editáveis pelo usuário. Nesses casos, a infraestrutura de ligação de dados lida com todo o controle de alterações para que as alterações possam ser enviadas de volta para o banco mais tarde. Se você fizer edições programaticamente nos dados e pretende enviar essas alterações de volta ao banco de dado, deverá usar os objetos e métodos que fazem o controle de alterações para você.

Além de alterar os dados reais, você também pode consultar uma <xref:System.Data.DataTable> para retornar linhas específicas de dados. Por exemplo, você pode consultar linhas individuais, versões específicas de linhas (originais e propostas), linhas que foram alteradas ou linhas com erros.

## <a name="to-edit-rows-in-a-dataset"></a>Para editar linhas em um conjunto de registros
Para editar uma linha existente em um <xref:System.Data.DataTable>, você precisa localizar o <xref:System.Data.DataRow> que deseja editar e, em seguida, atribuir os valores atualizados às colunas desejadas.

Se você não souber o índice da linha que deseja editar, use o método `FindBy` para pesquisar pela chave primária:

[!code-csharp[VbRaddataEditing#3](../data-tools/codesnippet/CSharp/edit-data-in-datasets_1.cs)]
[!code-vb[VbRaddataEditing#3](../data-tools/codesnippet/VisualBasic/edit-data-in-datasets_1.vb)]

Se você souber o índice de linha, poderá acessar e editar as linhas da seguinte maneira:

[!code-csharp[VbRaddataEditing#5](../data-tools/codesnippet/CSharp/edit-data-in-datasets_2.cs)]
[!code-vb[VbRaddataEditing#5](../data-tools/codesnippet/VisualBasic/edit-data-in-datasets_2.vb)]

## <a name="to-insert-new-rows-into-a-dataset"></a>Para inserir novas linhas em um conjunto de registros
Os aplicativos que usam controles vinculados a dados normalmente adicionam novos registros por meio do botão **Adicionar novo** em um [controle BindingNavigator](/dotnet/framework/winforms/controls/bindingnavigator-control-windows-forms).

Para adicionar manualmente novos registros a um DataSet, crie uma nova linha de dados chamando o método na DataTable. Em seguida, adicione a linha à coleção de <xref:System.Data.DataRow> (<xref:System.Data.DataTable.Rows%2A>) do <xref:System.Data.DataTable>:

[!code-csharp[VbRaddataEditing#1](../data-tools/codesnippet/CSharp/edit-data-in-datasets_3.cs)]
[!code-vb[VbRaddataEditing#1](../data-tools/codesnippet/VisualBasic/edit-data-in-datasets_3.vb)]

Para manter as informações que o conjunto de dados precisa para enviar atualizações para a fonte, use o método <xref:System.Data.DataRow.Delete%2A> para remover linhas em uma tabela de dados. Por exemplo, se seu aplicativo usa um TableAdapter (ou <xref:System.Data.Common.DataAdapter>), o método `Update` do TableAdapter exclui linhas no banco de dados que têm um <xref:System.Data.DataRow.RowState%2A> de <xref:System.Data.DataRowState.Deleted>.

Se seu aplicativo não precisar enviar atualizações de volta para uma fonte de dados, será possível remover os registros acessando diretamente a coleção de linhas de dados (<xref:System.Data.DataRowCollection.Remove%2A>).

#### <a name="to-delete-records-from-a-data-table"></a>Para excluir registros de uma tabela de dados

- Chame o método de <xref:System.Data.DataRow.Delete%2A> de um <xref:System.Data.DataRow>.

     Esse método não remove fisicamente o registro. Em vez disso, ele marca o registro para exclusão.

    > [!NOTE]
    > Se você obter a propriedade Count de um <xref:System.Data.DataRowCollection>, a contagem resultante incluirá os registros que foram marcados para exclusão. Para obter uma contagem precisa de registros que não estão marcados para exclusão, você pode executar um loop na coleção examinando a propriedade <xref:System.Data.DataRow.RowState%2A> de cada registro. (Os registros marcados para exclusão têm uma <xref:System.Data.DataRow.RowState%2A> de <xref:System.Data.DataRowState.Deleted>.) Como alternativa, você pode criar um modo de exibição de dados de um DataSet que filtra com base no estado de linha e obter a propriedade Count a partir daí.

O exemplo a seguir mostra como chamar o método <xref:System.Data.DataRow.Delete%2A> para marcar a primeira linha na tabela `Customers` como excluído:

[!code-csharp[VbRaddataEditing#8](../data-tools/codesnippet/CSharp/edit-data-in-datasets_4.cs)]
[!code-vb[VbRaddataEditing#8](../data-tools/codesnippet/VisualBasic/edit-data-in-datasets_4.vb)]

## <a name="determine-if-there-are-changed-rows"></a>Determinar se há linhas alteradas
Quando são feitas alterações nos registros em um conjunto de dados, as informações sobre essas alterações são armazenadas até você confirmá-las. Você confirma as alterações ao chamar o método `AcceptChanges` de um conjunto de dados ou uma tabela data, ou quando chama o método `Update` de um TableAdapter ou adaptador de dados.

As alterações são controladas de duas maneiras em cada linha de dados:

- Cada linha de dados contém informações relacionadas à sua <xref:System.Data.DataRow.RowState%2A> (por exemplo, <xref:System.Data.DataRowState.Added>, <xref:System.Data.DataRowState.Modified>, <xref:System.Data.DataRowState.Deleted>ou <xref:System.Data.DataRowState.Unchanged>).

- Cada linha de dados alterada contém várias versões dessa linha (<xref:System.Data.DataRowVersion>), a versão original (antes das alterações) e a versão atual (após as alterações). Durante o período em que uma alteração está pendente (a hora em que você pode responder ao evento <xref:System.Data.DataTable.RowChanging>), uma terceira versão — a versão proposta — também está disponível.

O método <xref:System.Data.DataSet.HasChanges%2A> de um conjunto de um DataSet retorna `true` se foram feitas alterações no DataSet. Depois de determinar que as linhas alteradas existem, você pode chamar o método `GetChanges` de um <xref:System.Data.DataSet> ou <xref:System.Data.DataTable> para retornar um conjunto de linhas alteradas.

#### <a name="to-determine-if-changes-have-been-made-to-any-rows"></a>Para determinar se foram feitas alterações em qualquer linha

- Chame o método <xref:System.Data.DataSet.HasChanges%2A> de um conjunto de registros para verificar se há linhas alteradas.

O exemplo a seguir mostra como verificar o valor de retorno do método <xref:System.Data.DataSet.HasChanges%2A> para detectar se há quaisquer linhas alteradas em um conjunto de registros chamado `NorthwindDataset1`:

[!code-csharp[VbRaddataEditing#12](../data-tools/codesnippet/CSharp/edit-data-in-datasets_5.cs)]
[!code-vb[VbRaddataEditing#12](../data-tools/codesnippet/VisualBasic/edit-data-in-datasets_5.vb)]

## <a name="determine-the-type-of-changes"></a>Determinar o tipo de alterações
Você também pode verificar para ver quais tipos de alterações foram feitas em um conjunto de um DataSet, passando um valor da enumeração <xref:System.Data.DataRowState> para o método <xref:System.Data.DataSet.HasChanges%2A>.

#### <a name="to-determine-what-type-of-changes-have-been-made-to-a-row"></a>Para determinar que tipo de alterações foram feitas em uma linha

- Passe um valor de <xref:System.Data.DataRowState> para o método <xref:System.Data.DataSet.HasChanges%2A>.

O exemplo a seguir mostra como verificar um conjunto de registros chamado `NorthwindDataset1` para determinar se alguma nova linha foi adicionada a ele:

[!code-csharp[VbRaddataEditing#13](../data-tools/codesnippet/CSharp/edit-data-in-datasets_6.cs)]
[!code-vb[VbRaddataEditing#13](../data-tools/codesnippet/VisualBasic/edit-data-in-datasets_6.vb)]

## <a name="to-locate-rows-that-have-errors"></a>Para localizar linhas com erros
Ao trabalhar com colunas individuais e linhas de dados, você pode encontrar erros. Você pode verificar a propriedade `HasErrors` para determinar se há erros em um <xref:System.Data.DataSet>, <xref:System.Data.DataTable>ou <xref:System.Data.DataRow>.

1. Verifique a propriedade `HasErrors` para ver se há erros no conjunto de um.

2. Se a propriedade `HasErrors` for `true`da, itere pelas coleções de tabelas e, em seguida, pelas linhas, para localizar a linha com o erro.

[!code-csharp[VbRaddataEditing#23](../data-tools/codesnippet/CSharp/edit-data-in-datasets_7.cs)]
[!code-vb[VbRaddataEditing#23](../data-tools/codesnippet/VisualBasic/edit-data-in-datasets_7.vb)]

## <a name="see-also"></a>Veja também

- [Ferramentas de conjunto de dados no Visual Studio](../data-tools/dataset-tools-in-visual-studio.md)
