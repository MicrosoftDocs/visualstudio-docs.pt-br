---
title: Salvar dados de um objeto em um banco de dados
description: Salvar dados de um objeto em um banco de dado usando as ferramentas de conjunto do dados no Visual Studio. Veja como salvar novos registros, atualizar registros existentes e excluir registros existentes.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Visual Studio], saving
- data access [Visual Studio], objects
- saving data
ms.assetid: efd6135a-40cf-4b0d-8f8b-41a5aaea7057
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 50debf24fa691ba74d082543b1c0bb1a27b5786e
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2021
ms.locfileid: "106215780"
---
# <a name="save-data-from-an-object-to-a-database"></a>Salvar dados de um objeto em um banco de dados

Você pode salvar dados em objetos em um banco de dado passando os valores do seu objeto para um dos métodos DBDirect do TableAdapter (por exemplo, `TableAdapter.Insert` ). Para obter mais informações, consulte [TableAdapter](../data-tools/create-and-configure-tableadapters.md).

Para salvar dados de uma coleção de objetos, faça um loop através da coleção de objetos (por exemplo, um loop for-Next) e envie os valores para cada objeto para o banco de dados usando um dos métodos do TableAdapter `DBDirect` .

Por padrão, os `DBDirect` métodos são criados em um TableAdapter que pode ser executado diretamente no banco de dados. Esses métodos podem ser chamados diretamente e não exigem <xref:System.Data.DataSet> ou <xref:System.Data.DataTable> objetos para reconciliar as alterações a fim de enviar atualizações para um banco de dados.

> [!NOTE]
> Quando você estiver configurando um TableAdapter, a consulta principal deverá fornecer informações suficientes para que os `DBDirect` métodos sejam criados. Por exemplo, se um TableAdapter estiver configurado para consultar dados de uma tabela que não tem uma coluna de chave primária definida, ele não gerará `DBDirect` métodos.

|Métodos DBDirect TableAdapter|Descrição|
| - |-----------------|
|`TableAdapter.Insert`|Adiciona novos registros a um banco de dados e permite que você passe valores de coluna individuais como parâmetros de método.|
|`TableAdapter.Update`|Atualiza os registros existentes em um banco de dados. O `Update` método usa valores originais e novos de coluna como parâmetros de método. Os valores originais são usados para localizar o registro original e os novos valores são usados para atualizar esse registro.<br /><br /> O `TableAdapter.Update` método também é usado para reconciliar as alterações em um conjunto de dados de volta para o Database por meio de uma <xref:System.Data.DataSet> <xref:System.Data.DataTable> <xref:System.Data.DataRow> matriz de <xref:System.Data.DataRow> s como parâmetros de método.|
|`TableAdapter.Delete`|Exclui os registros existentes do banco de dados com base nos valores de coluna originais passados como parâmetros de método.|

## <a name="to-save-new-records-from-an-object-to-a-database"></a>Para salvar novos registros de um objeto em um banco de dados

- Crie os registros passando os valores para o `TableAdapter.Insert` método.

     O exemplo a seguir cria um novo registro de cliente na `Customers` tabela passando os valores no `currentCustomer` objeto para o `TableAdapter.Insert` método.

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form3.cs" id="Snippet23":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form3.vb" id="Snippet23":::

## <a name="to-update-existing-records-from-an-object-to-a-database"></a>Para atualizar os registros existentes de um objeto para um banco de dados

- Modifique os registros chamando o `TableAdapter.Update` método, passando os novos valores para atualizar o registro e passando os valores originais para localizar o registro.

    > [!NOTE]
    > Seu objeto precisa manter os valores originais para passá-los para o `Update` método. Este exemplo usa propriedades com um `orig` prefixo para armazenar os valores originais.

     O exemplo a seguir atualiza um registro existente na `Customers` tabela passando os valores novos e originais no `Customer` objeto para o `TableAdapter.Update` método.

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form3.cs" id="Snippet24":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form3.vb" id="Snippet24":::

## <a name="to-delete-existing-records-from-a-database"></a>Para excluir registros existentes de um banco de dados

- Exclua os registros chamando o `TableAdapter.Delete` método e passando os valores originais para localizar o registro.

    > [!NOTE]
    > Seu objeto precisa manter os valores originais para passá-los para o `Delete` método. Este exemplo usa propriedades com um `orig` prefixo para armazenar os valores originais.

     O exemplo a seguir exclui um registro da `Customers` tabela passando os valores originais no `Customer` objeto para o `TableAdapter.Delete` método.

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form3.cs" id="Snippet25":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form3.vb" id="Snippet25":::

## <a name="net-security"></a>Segurança do .NET

Você deve ter permissão para executar o selecionado `INSERT` , `UPDATE` ou `DELETE` na tabela no banco de dados.

## <a name="see-also"></a>Confira também

- [Salvar dados novamente no banco de dados](../data-tools/save-data-back-to-the-database.md)
