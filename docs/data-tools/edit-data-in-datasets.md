---
title: Editar dados em conjuntos de dados
description: Aprenda a editar dados em conjuntos de dados. Saiba como editar linhas de conjunto de registros, inserir novas linhas em um conjunto de um, determinar se há linhas alteradas e localizar linhas com erros.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- datasets [Visual Basic], editing data
- data [Visual Studio], editing in datasets
ms.assetid: 50d5c580-fbf7-408f-be70-e63ac4f4d0eb
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 38ceec2cafd3476342d9319d9b5d034564759fad
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2021
ms.locfileid: "106215897"
---
# <a name="edit-data-in-datasets"></a>Editar dados em conjuntos de dados
Você edita dados em tabelas de dados da mesma forma que edita os dados em uma tabela em qualquer banco de dado. O processo pode incluir inserção, atualização e exclusão de registros na tabela. Em um formulário vinculado a dados, você pode especificar quais campos são editáveis pelo usuário. Nesses casos, a infraestrutura de ligação de dados lida com todo o controle de alterações para que as alterações possam ser enviadas de volta para o banco mais tarde. Se você fizer edições programaticamente nos dados e pretende enviar essas alterações de volta ao banco de dado, deverá usar os objetos e métodos que fazem o controle de alterações para você.

Além de alterar os dados reais, você também pode consultar um <xref:System.Data.DataTable> para retornar linhas específicas de dados. Por exemplo, você pode consultar linhas individuais, versões específicas de linhas (originais e propostas), linhas que foram alteradas ou linhas com erros.

## <a name="to-edit-rows-in-a-dataset"></a>Para editar linhas em um conjunto de registros
Para editar uma linha existente em um <xref:System.Data.DataTable> , você precisa localizar o <xref:System.Data.DataRow> que deseja editar e, em seguida, atribuir os valores atualizados às colunas desejadas.

Se você não souber o índice da linha que deseja editar, use o `FindBy` método para pesquisar pela chave primária:

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet3":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet3":::

Se você souber o índice de linha, poderá acessar e editar as linhas da seguinte maneira:

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet5":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet5":::

## <a name="to-insert-new-rows-into-a-dataset"></a>Para inserir novas linhas em um conjunto de registros
Os aplicativos que usam controles vinculados a dados normalmente adicionam novos registros por meio do botão **Adicionar novo** em um [controle BindingNavigator](/dotnet/framework/winforms/controls/bindingnavigator-control-windows-forms).

Para adicionar manualmente novos registros a um DataSet, crie uma nova linha de dados chamando o método na DataTable. Em seguida, adicione a linha à <xref:System.Data.DataRow> coleção ( <xref:System.Data.DataTable.Rows%2A> ) do <xref:System.Data.DataTable> :

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet1":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet1":::

Para manter as informações que o conjunto de dados precisa para enviar atualizações para a fonte, use o <xref:System.Data.DataRow.Delete%2A> método para remover linhas em uma tabela de dados. Por exemplo, se seu aplicativo usa um TableAdapter (ou <xref:System.Data.Common.DataAdapter> ), o método do TableAdapter `Update` exclui linhas no banco de dados que têm um <xref:System.Data.DataRow.RowState%2A> de <xref:System.Data.DataRowState.Deleted> .

Se seu aplicativo não precisar enviar atualizações de volta para uma fonte de dados, será possível remover os registros acessando diretamente a coleção de linhas de dados ( <xref:System.Data.DataRowCollection.Remove%2A> ).

#### <a name="to-delete-records-from-a-data-table"></a>Para excluir registros de uma tabela de dados

- Chame o <xref:System.Data.DataRow.Delete%2A> método de a <xref:System.Data.DataRow> .

     Esse método não remove fisicamente o registro. Em vez disso, ele marca o registro para exclusão.

    > [!NOTE]
    > Se você obtiver a propriedade Count de um <xref:System.Data.DataRowCollection> , a contagem resultante incluirá os registros que foram marcados para exclusão. Para obter uma contagem precisa de registros que não estão marcados para exclusão, você pode executar um loop na coleção examinando a <xref:System.Data.DataRow.RowState%2A> propriedade de cada registro. (Os registros marcados para exclusão têm um <xref:System.Data.DataRow.RowState%2A> de <xref:System.Data.DataRowState.Deleted> .) Como alternativa, você pode criar um modo de exibição de dados de um DataSet que filtra com base no estado de linha e obter a propriedade Count a partir daí.

O exemplo a seguir mostra como chamar o <xref:System.Data.DataRow.Delete%2A> método para marcar a primeira linha na `Customers` tabela como excluída:

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet8":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet8":::

## <a name="determine-if-there-are-changed-rows"></a>Determinar se há linhas alteradas
Quando são feitas alterações nos registros em um conjunto de dados, as informações sobre essas alterações são armazenadas até você confirmá-las. As alterações são confirmadas quando você chama o `AcceptChanges` método de um conjunto de dados ou de uma tabela data, ou quando você chama o `Update` método de um TableAdapter ou adaptador de dados.

As alterações são controladas de duas maneiras em cada linha de dados:

- Cada linha de dados contém informações relacionadas ao seu <xref:System.Data.DataRow.RowState%2A> (por exemplo,,, <xref:System.Data.DataRowState.Added> <xref:System.Data.DataRowState.Modified> <xref:System.Data.DataRowState.Deleted> ou <xref:System.Data.DataRowState.Unchanged> ).

- Cada linha de dados alterada contém várias versões dessa linha ( <xref:System.Data.DataRowVersion> ), a versão original (antes das alterações) e a versão atual (após as alterações). Durante o período em que uma alteração está pendente (a hora em que você pode responder ao <xref:System.Data.DataTable.RowChanging> evento), uma terceira versão — a versão proposta — também está disponível.

O <xref:System.Data.DataSet.HasChanges%2A> método de um conjunto de um DataSet retorna `true` se foram feitas alterações no DataSet. Depois de determinar que as linhas alteradas existem, você pode chamar o `GetChanges` método de um <xref:System.Data.DataSet> ou <xref:System.Data.DataTable> retornar um conjunto de linhas alteradas.

#### <a name="to-determine-if-changes-have-been-made-to-any-rows"></a>Para determinar se foram feitas alterações em qualquer linha

- Chame o <xref:System.Data.DataSet.HasChanges%2A> método de um conjunto de registros para verificar se há linhas alteradas.

O exemplo a seguir mostra como verificar o valor de retorno do <xref:System.Data.DataSet.HasChanges%2A> método para detectar se há linhas alteradas em um conjunto de registros chamado `NorthwindDataset1` :

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet12":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet12":::

## <a name="determine-the-type-of-changes"></a>Determinar o tipo de alterações
Você também pode verificar para ver quais tipos de alterações foram feitas em um conjunto de um DataSet, passando um valor da <xref:System.Data.DataRowState> enumeração para o <xref:System.Data.DataSet.HasChanges%2A> método.

#### <a name="to-determine-what-type-of-changes-have-been-made-to-a-row"></a>Para determinar que tipo de alterações foram feitas em uma linha

- Passe um <xref:System.Data.DataRowState> valor para o <xref:System.Data.DataSet.HasChanges%2A> método.

O exemplo a seguir mostra como verificar um conjunto de `NorthwindDataset1` registros chamado para determinar se alguma nova linha foi adicionada a ele:

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet13":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet13":::

## <a name="to-locate-rows-that-have-errors"></a>Para localizar linhas com erros
Ao trabalhar com colunas individuais e linhas de dados, você pode encontrar erros. Você pode verificar a `HasErrors` propriedade para determinar se há erros em um <xref:System.Data.DataSet> , <xref:System.Data.DataTable> ou <xref:System.Data.DataRow> .

1. Verifique a `HasErrors` propriedade para ver se há erros no conjunto de os.

2. Se a `HasErrors` propriedade for `true` , itere pelas coleções de tabelas e, em seguida, as pelas linhas, para localizar a linha com o erro.

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet23":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet23":::

## <a name="see-also"></a>Confira também

- [Ferramentas de conjunto de dados no Visual Studio](../data-tools/dataset-tools-in-visual-studio.md)
