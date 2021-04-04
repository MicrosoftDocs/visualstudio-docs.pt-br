---
title: Atualização hierárquica
description: Revise as atualizações hierárquicas, que envolvem salvar dados atualizados (de um conjunto com mais de duas tabelas relacionadas) de volta a um BD, mantendo as regras de integridade referencial.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- saving data, changed data
- data [Visual Basic], hierarchical update
- saving updated data
- datasets [Visual Basic], hierarchical update
- hierarchical update
- saving data, hierarchical update
- modified data saving
- updated data saving
- related tables, saving
ms.assetid: 68bae3f6-ec9b-45ee-a33a-69395029f54c
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: d43d4267ce0e180a525e990e372b7a6773a9cc51
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2021
ms.locfileid: "106215806"
---
# <a name="hierarchical-update"></a>Atualização hierárquica

A *atualização hierárquica* refere-se ao processo de salvar dados atualizados (de um DataSet com duas ou mais tabelas relacionadas) de volta a um banco de dado, mantendo regras de integridade referencial. A *integridade referencial* refere-se às regras de consistência fornecidas pelas restrições em um banco de dados que controlam o comportamento de inserção, atualização e exclusão de registros relacionados. Por exemplo, é a integridade referencial que impõe a criação de um registro de cliente antes de permitir que os pedidos sejam criados para esse cliente.  Para obter mais informações sobre relações em conjuntos de dados, consulte [relações em conjuntos de](../data-tools/relationships-in-datasets.md)dados.

O recurso de atualização hierárquica usa um `TableAdapterManager` para gerenciar os `TableAdapter` s em um dataset tipado. O `TableAdapterManager` componente é uma classe gerada pelo Visual Studio, não um tipo .net. Quando você arrasta uma tabela da janela **fontes de dados** para uma página do Windows Form ou WPF, o Visual Studio adiciona uma variável do tipo TableAdapterManager ao formulário ou à página e você a vê no designer na bandeja de componentes. Para obter informações detalhadas sobre a `TableAdapterManager` classe, consulte a seção de referência do TableAdapterManager de [TableAdapters](../data-tools/create-and-configure-tableadapters.md).

Por padrão, um conjunto de testes trata tabelas relacionadas como "somente relações", o que significa que ela não impõe restrições de chave estrangeira. Você pode modificar essa configuração em tempo de design usando o **Designer de conjunto de dados**. Selecione a linha de relação entre duas tabelas para abrir a caixa de diálogo **relação** . As alterações feitas aqui determinarão como o se `TableAdapterManager` comporta ao enviar as alterações nas tabelas relacionadas de volta para o banco de dados.

## <a name="enable-hierarchical-update-in-a-dataset"></a>Habilitar atualização hierárquica em um conjunto de um DataSet

Por padrão, a atualização hierárquica está habilitada para todos os novos conjuntos de valores que são adicionados ou criados em um projeto. Ativar ou desativar a atualização hierárquica definindo a propriedade **Hierarchical Update** de um dataset tipado no DataSet como **true** ou **false**:

![Configuração de atualização hierárquica](../data-tools/media/hierarchical-update-setting.png)

## <a name="create-a-new-relation-between-tables"></a>Criar uma nova relação entre tabelas

Para criar uma nova relação entre duas tabelas, na Designer de Conjunto de Dados, selecione a barra de título de cada tabela, clique com o botão direito do mouse e selecione **Adicionar relação**.

![Menu Adicionar relação de atualização hierárquica](../data-tools/media/hierarchical-update-add-relation-menu.png)

## <a name="understand-foreign-key-constraints-cascading-updates-and-deletes"></a>Entender as restrições de chave estrangeira, as atualizações em cascata e as exclusões

É importante entender como as restrições de chave estrangeira e o comportamento em cascata no banco de dados são criados no código do dataset gerado.

Por padrão, as tabelas de dados em um DataSet são geradas com relações ( <xref:System.Data.DataRelation> ) que correspondem às relações no banco de dados. No entanto, a relação no DataSet não é gerada como uma restrição FOREIGN-KEY. O <xref:System.Data.DataRelation> é configurado como **somente relação** sem <xref:System.Data.ForeignKeyConstraint.UpdateRule%2A> ou <xref:System.Data.ForeignKeyConstraint.DeleteRule%2A> em vigor.

Por padrão, as atualizações em cascata e as exclusões em cascata são desativadas mesmo que a relação de banco de dados esteja definida com atualizações em cascata e/ou exclusões em cascata ativadas. Por exemplo, criar um novo cliente e um novo pedido e, em seguida, tentar salvar os dados pode causar um conflito com as restrições Foreign-Key que são definidas no Database. Para obter mais informações, consulte [desativar restrições ao preencher um conjunto de](turn-off-constraints-while-filling-a-dataset.md)dados.

## <a name="set-the-order-to-perform-updates"></a>Definir a ordem para executar atualizações

Definir a ordem para executar atualizações define a ordem das inserções, atualizações e exclusões individuais que são necessárias para salvar todos os dados modificados em todas as tabelas de um DataSet. Quando a atualização hierárquica está habilitada, as inserções são executadas primeiro, depois as atualizações e, em seguida, as exclusões. O `TableAdapterManager` fornece uma `UpdateOrder` propriedade que pode ser definida para executar atualizações primeiro, depois insere e, em seguida, exclui.

> [!NOTE]
> É importante entender que a ordem de atualização é tudo inclusiva. Ou seja, quando as atualizações são executadas, inserções e exclusões são executadas para todas as tabelas no conjunto de conjuntos.

Para definir a `UpdateOrder` propriedade, depois de arrastar itens da [janela fontes de dados](add-new-data-sources.md#data-sources-window) para um formulário, selecione o `TableAdapterManager` na bandeja de componentes e, em seguida, defina a `UpdateOrder` Propriedade na janela **Propriedades** .

## <a name="create-a-backup-copy-of-a-dataset-before-performing-a-hierarchical-update"></a>Criar uma cópia de backup de um conjunto de um DataSet antes de executar uma atualização hierárquica

Quando você salva dados (chamando o `TableAdapterManager.UpdateAll()` método), as `TableAdapterManager` tentativas de atualizar os dados para cada tabela em uma única transação. Se qualquer parte da atualização de qualquer tabela falhar, toda a transação será revertida. Na maioria das situações, a reversão retorna o aplicativo ao seu estado original.

No entanto, às vezes, talvez você queira restaurar o conjunto de os conjuntos de backup. Um exemplo disso pode ocorrer quando você estiver usando valores de incremento automático. Por exemplo, se uma operação de salvamento não for bem-sucedida, os valores de incremento automático não serão redefinidos no conjunto de e o conjunto de um continuará criando valores de incremento automático. Isso deixa uma lacuna na numeração que pode não ser aceitável em seu aplicativo. Em situações em que esse é um problema, o `TableAdapterManager` fornece uma `BackupDataSetBeforeUpdate` propriedade que substitui o conjunto de um existente por uma cópia de backup se a transação falhar.

> [!NOTE]
> A cópia de backup só está na memória enquanto o `TableAdapterManager.UpdateAll` método está em execução. Portanto, não há nenhum acesso programático a esse conjunto de backups porque ele substitui o conjunto de um original ou sai do escopo assim que o `TableAdapterManager.UpdateAll` método termina de ser executado.

## <a name="modify-the-generated-save-code-to-perform-the-hierarchical-update"></a>Modificar o código de salvamento gerado para executar a atualização hierárquica

Salve as alterações das tabelas relacionadas de dados no conjunto de dados para o banco de dados chamando o método `TableAdapterManager.UpdateAll` e passando no nome do conjunto de dados que contém as tabelas relacionadas. Por exemplo, execute o método `TableAdapterManager.UpdateAll(NorthwindDataset)` para enviar atualizações de todas as tabelas no NorthwindDataset para o banco de dados back-end.

Depois de soltar os itens da janela **Fontes de Dados**, o código é automaticamente adicionado ao evento `Form_Load` para preencher cada tabela (os métodos `TableAdapter.Fill`). O código também é adicionado ao evento de clique do botão **Salvar** do <xref:System.Windows.Forms.BindingNavigator> para salvar os dados do conjunto de dados de volta ao banco de dados (o método `TableAdapterManager.UpdateAll`).

O código salvar gerado também contém uma linha de código que chama o método `CustomersBindingSource.EndEdit`. Mais especificamente, ele chama o <xref:System.Windows.Forms.BindingSource.EndEdit%2A> método do primeiro <xref:System.Windows.Forms.BindingSource> que é adicionado ao formulário. Em outras palavras, esse código só é gerado para a primeira tabela que é arrastada da janela **fontes de dados** para o formulário. A chamada <xref:System.Windows.Forms.BindingSource.EndEdit%2A> confirma as alterações que estão em processo em qualquer controle de associação de dados sendo editado no momento. Portanto, se um controle associado a dados ainda estiver em foco e você clicar no botão **Salvar**, todas as edições pendentes nesse controle serão confirmadas antes da gravação real (o método `TableAdapterManager.UpdateAll`).

> [!NOTE]
> O **Designer de conjunto de dados** apenas adiciona o `BindingSource.EndEdit` código para a primeira tabela que é descartada no formulário. Portanto, é necessário adicionar uma linha de código para chamar o método `BindingSource.EndEdit` para cada tabela relacionada no formulário. Para este passo a passo, isso significa que você precisa adicionar uma chamada ao método `OrdersBindingSource.EndEdit`.

### <a name="to-update-the-code-to-commit-changes-to-the-related-tables-before-saving"></a>Para atualizar o código para confirmar as alterações às tabelas relacionadas antes de salvar

1. Clique duas vezes no botão **Salvar** no <xref:System.Windows.Forms.BindingNavigator> para abrir **Form1** no Editor de Códigos.

2. Adicione uma linha de código para chamar o método `OrdersBindingSource.EndEdit` após a linha que chama o método `CustomersBindingSource.EndEdit`. O código no evento de clique do botão **Salvar** deve ser semelhante ao seguinte:

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VSProDataOrcasHierarchicalUpdate/VB/Form1.vb" id="Snippet1":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VSProDataOrcasHierarchicalUpdate/CS/Form1.cs" id="Snippet1":::

Além de confirmar as alterações em uma tabela filho relacionada antes de salvar dados em um banco de dados, você também pode confirmar registros pais recém-criados antes de adicionar novos registros filhos a um conjunto de dados. Em outras palavras, talvez seja necessário adicionar o novo registro pai ( `Customer` ) ao conjunto de registros antes que as restrições de chave estrangeira permitam que novos registros filho ( `Orders` ) sejam adicionados ao conjunto de recursos. Para realizar isso, você pode usar o evento filho `BindingSource.AddingNew`.

> [!NOTE]
> Se você precisa confirmar novos registros pai depende do tipo de controle usado para associar à fonte de dados. Neste tutorial, você usa controles individuais para associar à tabela pai. Isso requer o código adicional para confirmar o novo registro pai. Se os registros pai foram exibidos em um controle de associação complexo como o <xref:System.Windows.Forms.DataGridView> , essa <xref:System.Windows.Forms.BindingSource.EndEdit%2A> chamada adicional para o registro pai não seria necessária. Isso porque a funcionalidade subjacente de associação de dados do controle processa a confirmação dos novos registros.

### <a name="to-add-code-to-commit-parent-records-in-the-dataset-before-adding-new-child-records"></a>Para adicionar código para confirmar registros pais no conjunto de dados antes de adicionar novos registros filhos

1. Crie um manipulador de eventos para o evento `OrdersBindingSource.AddingNew`.

    - Abra o **Form1** no modo de exibição de design, selecione **OrdersBindingSource** na bandeja de componentes, selecione **eventos** na janela **Propriedades** e clique duas vezes no evento **AddingNew** .

2. Adicione uma linha de código ao manipulador de eventos que chama o `CustomersBindingSource.EndEdit` método. O código no manipulador de eventos `OrdersBindingSource_AddingNew` deve ser semelhante ao seguinte:

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VSProDataOrcasHierarchicalUpdate/VB/Form1.vb" id="Snippet2":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VSProDataOrcasHierarchicalUpdate/CS/Form1.cs" id="Snippet2":::

## <a name="tableadaptermanager-reference"></a>Referência do TableAdaptermanager

Por padrão, uma `TableAdapterManager` classe é gerada quando você cria um conjunto de um DataSet que contém tabelas relacionadas. Para impedir que a classe seja gerada, altere o valor da `Hierarchical Update` Propriedade do conjunto de valores para false. Quando você arrasta uma tabela que tem uma relação na superfície de design de uma página do Windows Form ou WPF, o Visual Studio declara uma variável de membro da classe. Se você não usar DataBinding, será necessário declarar manualmente a variável.

A `TableAdapterManager` classe não é um tipo .net. Portanto, você não pode procurar na documentação. Ele é criado no momento do design como parte do processo de criação do conjunto de um.

A seguir estão os métodos e as propriedades usados com frequência da `TableAdapterManager` classe:

|Membro|Descrição|
|------------|-----------------|
|Método `UpdateAll`|Salva todos os dados de todas as tabelas de dados.|
|Propriedade `BackUpDataSetBeforeUpdate`|Determina se deve ser criada uma cópia de backup do conjunto de um antes da execução do `TableAdapterManager.UpdateAll` método. Boolean.|
|*TableName* `TableAdapter` Propriedade|Representa um `TableAdapter` . O gerado `TableAdapterManager` contém uma propriedade para cada uma `TableAdapter` gerencia. Por exemplo, um conjunto de um DataSet com uma tabela Customers e Orders é gerado com um `TableAdapterManager` que contém `CustomersTableAdapter` e `OrdersTableAdapter` Propriedades.|
|Propriedade `UpdateOrder`|Controla a ordem dos comandos individuais INSERT, Update e Delete. Defina isso para um dos valores na `TableAdapterManager.UpdateOrderOption` enumeração.<br /><br /> Por padrão, o `UpdateOrder` é definido como **InsertUpdateDelete**. Isso significa que inserções, atualizações e, em seguida, exclusões são executadas para todas as tabelas no DataSet.|

## <a name="see-also"></a>Confira também

- [Salvar dados novamente no banco de dados](../data-tools/save-data-back-to-the-database.md)
