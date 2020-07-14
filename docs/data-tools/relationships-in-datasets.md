---
title: Usar DataRelation para criar relações entre conjuntos de os
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vbData.Microsoft.VSDesigner.DataSource.DesignRelation
- vbdata.Microsoft.VSDesigner.DataSource.DesignRelation
helpviewer_keywords:
- relationships, about relationships
- datasets [Visual Basic], relationships
- relationships, datasets
ms.assetid: cfe274f0-71fe-40f6-994e-7c7f6273c9ba
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 95476e56ceecfca84251c1b43cf0bb9ddf84f8b5
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85281754"
---
# <a name="create-relationships-between-datasets"></a>Criar relações entre conjuntos de dados
DataSets que contêm tabelas de dados relacionadas usam <xref:System.Data.DataRelation> objetos para representar uma relação pai/filho entre as tabelas e para retornar registros relacionados uns dos outros. Adicionar tabelas relacionadas a conjuntos de dados usando o **Assistente de configuração de fonte de dados**ou o **Designer de conjunto de dados**, cria e configura o <xref:System.Data.DataRelation> objeto para você.

O <xref:System.Data.DataRelation> objeto executa duas funções:

- Ele pode disponibilizar os registros relacionados a um registro com o qual você está trabalhando. Ele fornecerá registros filho se você estiver em um registro pai ( <xref:System.Data.DataRow.GetChildRows%2A> ) e um registro pai se estiver trabalhando com um registro filho ( <xref:System.Data.DataRow.GetParentRow%2A> ).

- Ele pode impor restrições para a integridade referencial, como excluir registros filho relacionados quando você exclui um registro pai.

É importante entender a diferença entre uma junção verdadeira e a função de um <xref:System.Data.DataRelation> objeto. Em uma junção verdadeira, os registros são tirados das tabelas pai e filho e colocados em um único conjunto de registros simples. Quando você usa um <xref:System.Data.DataRelation> objeto, nenhum novo conjunto de registros é criado. Em vez disso, a DataRelation acompanha a relação entre as tabelas e mantém os registros pai e filho sincronizados.

## <a name="datarelation-objects-and-constraints"></a>Objetos e restrições de DataRelation
Um <xref:System.Data.DataRelation> objeto também é usado para criar e impor as seguintes restrições:

- Uma restrição UNIQUE, que garante que uma coluna na tabela não contenha duplicatas.

- Uma restrição FOREIGN-KEY, que pode ser usada para manter a integridade referencial entre uma tabela pai e filho em um conjunto de um DataSet.

As restrições que você especificar em um <xref:System.Data.DataRelation> objeto são implementadas criando automaticamente objetos apropriados ou definindo propriedades. Se você criar uma restrição FOREIGN-KEY usando o <xref:System.Data.DataRelation> objeto, as instâncias da <xref:System.Data.ForeignKeyConstraint> classe serão adicionadas à <xref:System.Data.DataRelation> Propriedade do objeto <xref:System.Data.DataRelation.ChildKeyConstraint%2A> .

Uma restrição UNIQUE é implementada simplesmente definindo a <xref:System.Data.DataColumn.Unique%2A> propriedade de uma coluna de dados como `true` ou adicionando uma instância da <xref:System.Data.UniqueConstraint> classe à <xref:System.Data.DataRelation> Propriedade do objeto <xref:System.Data.DataRelation.ParentKeyConstraint%2A> . Para obter informações sobre como suspender restrições em um conjunto de dados, consulte [desativar restrições ao preencher um conjunto de](../data-tools/turn-off-constraints-while-filling-a-dataset.md)dados.

### <a name="referential-integrity-rules"></a>Regras de integridade referencial
Como parte da restrição FOREIGN-KEY, você pode especificar regras de integridade referencial que são aplicadas em três pontos:

- Quando um registro pai é atualizado

- Quando um registro pai é excluído

- Quando uma alteração é aceita ou rejeitada

As regras que você pode fazer são especificadas na <xref:System.Data.Rule> enumeração e são listadas na tabela a seguir.

|Regra de restrição FOREIGN-KEY|Ação|
| - |------------|
|<xref:System.Data.Rule.Cascade>|A alteração (Update ou Delete) feita no registro pai também é feita em registros relacionados na tabela filho.|
|<xref:System.Data.Rule.SetNull>|Os registros filho não são excluídos, mas a chave estrangeira nos registros filho é definida como <xref:System.DBNull> . Com essa configuração, os registros filho podem ser deixados como "órfãos", ou seja, não têm relação com os registros pai. **Observação:** O uso dessa regra pode resultar em dados inválidos na tabela filho.|
|<xref:System.Data.Rule.SetDefault>|A chave estrangeira nos registros filho relacionados é definida como seu valor padrão (conforme estabelecido pela propriedade da coluna <xref:System.Data.DataColumn.DefaultValue%2A> ).|
|<xref:System.Data.Rule.None>|Nenhuma alteração é feita em registros filho relacionados. Com essa configuração, os registros filho podem conter referências a registros pai inválidos.|

Para obter mais informações sobre atualizações em tabelas de DataSet, consulte [salvar dados de volta no banco de dados](../data-tools/save-data-back-to-the-database.md).

### <a name="constraint-only-relations"></a>Relações somente de restrição
Ao criar um <xref:System.Data.DataRelation> objeto, você tem a opção de especificar que a relação seja usada somente para impor restrições, ou seja, ela também não será usada para acessar registros relacionados. Você pode usar essa opção para gerar um conjunto de registros que seja um pouco mais eficiente e que contenha menos métodos do que um com a funcionalidade de registros relacionados. No entanto, você não poderá acessar os registros relacionados. Por exemplo, uma relação somente de restrição impede que você exclua um registro pai que ainda tem registros filho, e você não pode acessar os registros filho por meio do pai.

## <a name="manually-creating-a-data-relation-in-the-dataset-designer"></a>Criando manualmente uma relação de dados no Designer de Conjunto de Dados
Quando você cria tabelas de dados usando as ferramentas de design de dados no Visual Studio, as relações são criadas automaticamente se as informações podem ser coletadas da origem dos seus dados. Se você adicionar tabelas de dados manualmente a partir da guia **DataSet** da **caixa de ferramentas**, talvez seja necessário criar a relação manualmente. Para obter informações sobre como criar <xref:System.Data.DataRelation> objetos programaticamente, consulte [adicionando DataRelations](/dotnet/framework/data/adonet/dataset-datatable-dataview/adding-datarelations).

As relações entre tabelas de dados aparecem como linhas na **Designer de conjunto de dados**, com um glifo de chave e infinito, que ilustra o aspecto de um para muitos da relação. Por padrão, o nome da relação não aparece na superfície de design.

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

#### <a name="to-create-a-relationship-between-two-data-tables"></a>Para criar uma relação entre duas tabelas de dados

1. Abra o conjunto de dados no **Designer de Conjunto de Dados**. Para obter mais informações, consulte [Walkthrough: Criando um conjunto de dados no designer de conjunto de dados](walkthrough-creating-a-dataset-with-the-dataset-designer.md).

2. Arraste um objeto **relation** da caixa de ferramentas **DataSet** para a tabela de dados filho na relação.

     A caixa de diálogo **relação** é aberta, preenchendo a caixa **tabela filho** com a tabela na qual você arrastou o objeto de **relação** .

3. Selecione a tabela pai na caixa **tabela pai** . A tabela pai contém registros no lado "um" de uma relação um-para-muitos.

4. Verifique se a tabela filho correta é exibida na caixa **tabela filho** . A tabela filho contém registros no lado "muitos" de uma relação um-para-muitos.

5. Digite um nome para a relação na caixa **nome** ou deixe o nome padrão com base nas tabelas selecionadas. Este é o nome do objeto real <xref:System.Data.DataRelation> no código.

6. Selecione as colunas que unem as tabelas nas listas **colunas de chave** e **colunas de chave estrangeira** .

7. Selecione se deseja criar uma relação, uma restrição ou ambas.

8. Marque ou desmarque a caixa de **relação aninhada** . A seleção dessa opção define a <xref:System.Data.DataRelation.Nested%2A> propriedade como `true` e faz com que as linhas filhas da relação sejam aninhadas dentro da coluna pai quando essas linhas são gravadas como dados XML ou sincronizadas com o <xref:System.Xml.XmlDataDocument> . Para obter mais informações, consulte [aninhando DataRelations](/dotnet/framework/data/adonet/dataset-datatable-dataview/nesting-datarelations).

9. Defina as regras a serem impostas quando você estiver fazendo alterações em registros nessas tabelas. Para obter mais informações, consulte <xref:System.Data.Rule>.

10. Clique em **OK** para criar a relação. Uma linha de relação aparece no designer entre as duas tabelas.

#### <a name="to-display-a-relation-name-in-the-dataset-designer"></a>Para exibir um nome de relação no Designer de Conjunto de Dados

1. Abra o conjunto de dados no **Designer de Conjunto de Dados**. Para obter mais informações, consulte [Walkthrough: Criando um conjunto de dados no designer de conjunto de dados](walkthrough-creating-a-dataset-with-the-dataset-designer.md).

2. No menu **dados** , selecione o comando **Mostrar rótulos de relação** para exibir o nome da relação. Limpe esse comando para ocultar o nome da relação.

## <a name="see-also"></a>Veja também

- [Criar e configurar conjuntos de dados no Visual Studio](../data-tools/create-and-configure-datasets-in-visual-studio.md)
