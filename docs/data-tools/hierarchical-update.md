---
title: Atualização hierárquica
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
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 52225ba4801fcee92b3f68fd6ec1cf7cc6c63086
ms.sourcegitcommit: 81e9d90843ead658bc73b30c869f25921d99e116
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2018
ms.locfileid: "52305709"
---
# <a name="hierarchical-update"></a>Atualização hierárquica

*Atualização hierárquica* refere-se ao processo de salvar dados atualizados (de um conjunto de dados com duas ou mais tabelas relacionadas) para um banco de dados, mantendo as regras de integridade referencial. *A integridade referencial* refere-se às regras de consistência fornecido pelas restrições em um banco de dados que controlam o comportamento de inserção, atualização e exclusão de registros relacionados. Por exemplo, é a integridade referencial que impõe a criação de um registro de cliente antes de permitir que os pedidos a ser criado para esse cliente.  Para obter mais informações sobre relacionamentos em conjuntos de dados, consulte [relacionamentos em conjuntos de dados](../data-tools/relationships-in-datasets.md).

O recurso de atualização hierárquica usa um `TableAdapterManager` para gerenciar o `TableAdapter`s em um dataset tipado. O `TableAdapterManager` componente é uma classe gerada pelo Visual Studio, portanto, não é parte do [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)]. Quando você arrasta uma tabela das **fontes de dados** janela para uma página de formulário do Windows ou do WPF, Visual Studio adiciona uma variável do tipo TableAdapterManager para o formulário ou página e vê-lo no designer na bandeja de componentes. Para obter informações detalhadas sobre o `TableAdapterManager` classe, consulte a seção de referência do TableAdapterManager [TableAdapters](../data-tools/create-and-configure-tableadapters.md).

Por padrão, um conjunto de dados trata tabelas relacionadas como "apenas relações" o que significa que ele não impõe restrições de chave estrangeira. Você pode modificar essa configuração em tempo de design usando o **Dataset Designer**. Selecione a linha de relação entre duas tabelas para abrir o **relação** caixa de diálogo. As alterações feitas aqui determinam como o `TableAdapterManager` se comporta quando ele envia as alterações nas tabelas relacionadas no banco de dados.

## <a name="enable-hierarchical-update-in-a-dataset"></a>Habilitar atualização hierárquica em um conjunto de dados

Por padrão, a atualização hierárquica está habilitada para todos os novos conjuntos de dados que são adicionados ou criados em um projeto. Ativar ou desativar a atualização hierárquica, definindo o **Hierarchical Update** propriedade de um dataset tipado no conjunto de dados como **verdadeiro** ou **False**:

![Configuração de atualização hierárquica](../data-tools/media/hierarchical-update-setting.png)

## <a name="create-a-new-relation-between-tables"></a>Criar uma nova relação entre tabelas

Para criar uma nova relação entre duas tabelas, no Designer de conjunto de dados, selecione a barra de título de cada tabela, clique com botão direito e selecione **Adicionar relação**.

![Atualização hierárquica Adicionar menu de relação](../data-tools/media/hierarchical-update-add-relation-menu.png)

## <a name="understand-foreign-key-constraints-cascading-updates-and-deletes"></a>Entender as restrições foreign key, atualizações em cascata e exclusões

É importante entender como restrições de chave estrangeira e comportamento em cascata no banco de dados são criados no código do conjunto de dados gerada.

Por padrão, as tabelas de dados em um conjunto de dados são geradas com relacionamentos (<xref:System.Data.DataRelation>) que coincidem com os relacionamentos no banco de dados. No entanto, a relação no conjunto de dados não é gerada como uma restrição de chave estrangeira. O <xref:System.Data.DataRelation> está configurado como **relação apenas** sem <xref:System.Data.ForeignKeyConstraint.UpdateRule%2A> ou <xref:System.Data.ForeignKeyConstraint.DeleteRule%2A> em vigor.

Por padrão, atualizações em cascata e exclusões em cascata são desativadas, mesmo se a relação de banco de dados é definida com atualizações em cascata e/ou exclusões em cascata ativado. Por exemplo, criando um novo cliente e um novo pedido e, em seguida, tentar salvar os dados podem causar um conflito com as restrições de chave estrangeira são definidas no banco de dados. Para obter mais informações, consulte [desativar restrições ao preencher um conjunto de dados](turn-off-constraints-while-filling-a-dataset.md).

## <a name="set-the-order-to-perform-updates"></a>Defina a ordem para executar atualizações

Definindo a ordem para executar atualizações define a ordem do indivíduo inserções, atualizações e exclusões que é necessárias para salvar todos os dados modificados em todas as tabelas de um conjunto de dados. Quando a atualização hierárquica é habilitada, inserções são executadas em primeiro lugar, em seguida, atualiza e, em seguida, exclui. O `TableAdapterManager` fornece um `UpdateOrder` propriedade que pode ser definida para executar atualizações em primeiro lugar, em seguida, inserções e exclusões.

> [!NOTE]
> É importante entender que a ordem de atualização é totalmente inclusiva. Ou seja, quando as atualizações são executadas, inserções e exclusões são executadas para todas as tabelas no conjunto de dados.

Para definir a `UpdateOrder` propriedade, depois de arrastar itens da [janela fontes de dados](add-new-data-sources.md#data-sources-window) para um formulário, selecione o `TableAdapterManager` na bandeja de componentes e em seguida, defina a `UpdateOrder` propriedade no **propriedades** janela.

## <a name="create-a-backup-copy-of-a-dataset-before-performing-a-hierarchical-update"></a>Criar uma cópia de backup de um conjunto de dados antes de executar uma atualização hierárquica

Quando você salva dados (chamando o `TableAdapterManager.UpdateAll()` método), o `TableAdapterManager` tenta atualizar os dados para cada tabela em uma única transação. Se qualquer parte da atualização para qualquer tabela falhar, toda a transação será revertida. Na maioria das situações, a reversão retorna seu aplicativo para seu estado original.

No entanto, às vezes, você talvez queira restaurar o conjunto de dados da cópia de backup. Um exemplo disso pode ocorrer quando você estiver usando valores de incremento automático. Por exemplo, se um salvamento operação não for bem-sucedida, os valores de incremento automático não são redefinidos no conjunto de dados e o conjunto de dados continua a criar valores de incremento automático. Isso deixa uma lacuna na numeração que pode não ser aceitável em seu aplicativo. Em situações em que isso é um problema, o `TableAdapterManager` fornece um `BackupDataSetBeforeUpdate` propriedade que substitui o conjunto de dados existente por uma cópia de backup se a transação falhar.

> [!NOTE]
> A cópia de backup está apenas na memória enquanto o `TableAdapterManager.UpdateAll` método está sendo executado. Portanto, não há nenhum acesso programático a esse conjunto de dados de backup porque ele substitui o conjunto de dados original ou sai do escopo assim que o `TableAdapterManager.UpdateAll` método termina a execução.

## <a name="modify-the-generated-save-code-to-perform-the-hierarchical-update"></a>Modificar o gerado salvar o código para executar a atualização hierárquica

Salve as alterações das tabelas relacionadas de dados no conjunto de dados para o banco de dados chamando o método `TableAdapterManager.UpdateAll` e passando no nome do conjunto de dados que contém as tabelas relacionadas. Por exemplo, execute o método `TableAdapterManager.UpdateAll(NorthwindDataset)` para enviar atualizações de todas as tabelas no NorthwindDataset para o banco de dados back-end.

Depois de soltar os itens da janela **Fontes de Dados**, o código é automaticamente adicionado ao evento `Form_Load` para preencher cada tabela (os métodos `TableAdapter.Fill`). O código também é adicionado ao evento de clique do botão **Salvar** do <xref:System.Windows.Forms.BindingNavigator> para salvar os dados do conjunto de dados de volta ao banco de dados (o método `TableAdapterManager.UpdateAll`).

O código salvar gerado também contém uma linha de código que chama o método `CustomersBindingSource.EndEdit`. Mais especificamente, ele chama o <xref:System.Windows.Forms.BindingSource.EndEdit%2A> método do primeiro <xref:System.Windows.Forms.BindingSource>que é adicionado ao formulário. Em outras palavras, esse código é gerado apenas para a primeira tabela que é arrastada do **fontes de dados** janela para o formulário. A chamada <xref:System.Windows.Forms.BindingSource.EndEdit%2A> confirma as alterações que estão em processo em qualquer controle de associação de dados sendo editado no momento. Portanto, se um controle associado a dados ainda estiver em foco e você clicar no botão **Salvar**, todas as edições pendentes nesse controle serão confirmadas antes da gravação real (o método `TableAdapterManager.UpdateAll`).

> [!NOTE]
> O **Dataset Designer** apenas adiciona o `BindingSource.EndEdit` código para a primeira tabela que é arrastada para o formulário. Portanto, é necessário adicionar uma linha de código para chamar o método `BindingSource.EndEdit` para cada tabela relacionada no formulário. Para este passo a passo, isso significa que você precisa adicionar uma chamada ao método `OrdersBindingSource.EndEdit`.

### <a name="to-update-the-code-to-commit-changes-to-the-related-tables-before-saving"></a>Para atualizar o código para confirmar as alterações às tabelas relacionadas antes de salvar

1.  Clique duas vezes no botão **Salvar** no <xref:System.Windows.Forms.BindingNavigator> para abrir **Form1** no Editor de Códigos.

2.  Adicione uma linha de código para chamar o método `OrdersBindingSource.EndEdit` após a linha que chama o método `CustomersBindingSource.EndEdit`. O código no evento de clique do botão **Salvar** deve ser semelhante ao seguinte:

     [!code-vb[VSProDataOrcasHierarchicalUpdate#1](../data-tools/codesnippet/VisualBasic/hierarchical-update_1.vb)]
     [!code-csharp[VSProDataOrcasHierarchicalUpdate#1](../data-tools/codesnippet/CSharp/hierarchical-update_1.cs)]

Além de confirmar as alterações em uma tabela filho relacionada antes de salvar dados em um banco de dados, você também pode confirmar registros pais recém-criados antes de adicionar novos registros filhos a um conjunto de dados. Em outras palavras, você talvez precise adicionar o novo registro pai (`Customer`) ao conjunto de dados antes de habilitar a restrições de chave estrangeira novos registros filhos (`Orders`) a ser adicionado ao conjunto de dados. Para realizar isso, você pode usar o evento filho `BindingSource.AddingNew`.

> [!NOTE]
> Se você precisa confirmar novos registros pais depende do tipo de controle que é usada para associar à fonte de dados. Neste passo a passo, você pode usar controles individuais para associar a tabela pai. Isso exige que o código adicional para confirmar o novo registro pai. Se os registros pai em vez disso, foram exibidos em um controle de vinculação complexa como o <xref:System.Windows.Forms.DataGridView>adicionais nesse <xref:System.Windows.Forms.BindingSource.EndEdit%2A> chamada para o registro pai não seria necessário. Isso porque a funcionalidade subjacente de associação de dados do controle processa a confirmação dos novos registros.

### <a name="to-add-code-to-commit-parent-records-in-the-dataset-before-adding-new-child-records"></a>Para adicionar código para confirmar registros pais no conjunto de dados antes de adicionar novos registros filhos

1.  Crie um manipulador de eventos para o evento `OrdersBindingSource.AddingNew`.

    -   Abra **Form1** no modo de design, selecione **OrdersBindingSource** na bandeja de componentes, selecione **eventos** no **propriedades** janela, e em seguida, clique duas vezes o **AddingNew** eventos.

2.  Adicionar uma linha de código ao manipulador de eventos que chama o `CustomersBindingSource.EndEdit` método. O código no manipulador de eventos `OrdersBindingSource_AddingNew` deve ser semelhante ao seguinte:

     [!code-vb[VSProDataOrcasHierarchicalUpdate#2](../data-tools/codesnippet/VisualBasic/hierarchical-update_2.vb)]
     [!code-csharp[VSProDataOrcasHierarchicalUpdate#2](../data-tools/codesnippet/CSharp/hierarchical-update_2.cs)]

## <a name="tableadaptermanager-reference"></a>Referência de TableAdapterManager

Por padrão, um `TableAdapterManager` classe é gerada quando você cria um conjunto de dados contiver tabelas relacionadas. Para impedir que a classe que está sendo gerado, altere o valor da `Hierarchical Update` propriedade do conjunto de dados como false. Quando você arrasta uma tabela que tem uma relação na superfície de design de um formulário do Windows ou a página do WPF, o Visual Studio declara uma variável de membro da classe. Se você não usar a associação de dados, você precisa declarar manualmente a variável.

O `TableAdapterManager` classe não é parte do [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)]. Portanto, você não pode procurar por ele na documentação. Ele é criado em tempo de design como parte do processo de criação de conjunto de dados.

A seguir estão os métodos usados com frequência e as propriedades do `TableAdapterManager` classe:

|Membro|Descrição|
|------------|-----------------|
|Método `UpdateAll`|Salva todos os dados de todas as tabelas de dados.|
|Propriedade `BackUpDataSetBeforeUpdate`|Determina se é necessário criar uma cópia de backup do conjunto de dados antes de executar o `TableAdapterManager.UpdateAll` método. Valor booliano.|
|*tableName* `TableAdapter` propriedade|Representa um `TableAdapter`. Gerado `TableAdapterManager` contém uma propriedade para cada `TableAdapter` que ele gerencia. Por exemplo, um conjunto de dados com uma tabela Customers e Orders é gerado com um `TableAdapterManager` que contém `CustomersTableAdapter` e `OrdersTableAdapter` propriedades.|
|Propriedade `UpdateOrder`|Controla a ordem da individual inserção, atualização e comandos de exclusão. Defina isso para um dos valores a `TableAdapterManager.UpdateOrderOption` enumeração.<br /><br /> Por padrão, o `UpdateOrder` é definido como **InsertUpdateDelete**. Isso significa que insere, em seguida, atualiza e exclui, em seguida, são executadas para todas as tabelas no conjunto de dados.|

## <a name="see-also"></a>Consulte também

- [Salvar dados de volta no banco de dados](../data-tools/save-data-back-to-the-database.md)
