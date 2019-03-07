---
title: Usar a DataRelation para criar relações entre conjuntos de dados
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vbData.Microsoft.VSDesigner.DataSource.DesignRelation
- vbdata.Microsoft.VSDesigner.DataSource.DesignRelation
helpviewer_keywords:
- relationships, about relationships
- datasets [Visual Basic], relationships
- relationships, datasets
ms.assetid: cfe274f0-71fe-40f6-994e-7c7f6273c9ba
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 611accb591b63f31ffe6a14535d470f2807f0e99
ms.sourcegitcommit: 21d667104199c2493accec20c2388cf674b195c3
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2019
ms.locfileid: "55951729"
---
# <a name="create-relationships-between-datasets"></a>Criar relações entre conjuntos de dados
Conjuntos de dados que contêm dados relacionados a tabelas usam <xref:System.Data.DataRelation> objetos para representar uma relação pai/filho entre as tabelas e para retornar registros relacionados uns dos outros. Adicionar tabelas relacionadas a conjuntos de dados usando o **Data Source Configuration Wizard**, ou o **Dataset Designer**, cria e configura o <xref:System.Data.DataRelation> objeto para você.

O <xref:System.Data.DataRelation> objeto executa duas funções:

-   Ele pode disponibilizar os registros relacionados a um registro que você está trabalhando. Ele fornece registros filho se você estiver em um registro pai (<xref:System.Data.DataRow.GetChildRows%2A>) e um registro pai se você estiver trabalhando com um registro filho (<xref:System.Data.DataRow.GetParentRow%2A>).

-   Ele pode impor restrições de integridade referencial, como excluir registros filho relacionados quando você exclui um registro pai.

É importante compreender a diferença entre uma associação verdadeira e a função de um <xref:System.Data.DataRelation> objeto. Em uma associação verdadeira, os registros são tirados das tabelas pai e filho e colocados em um conjunto de registros único e simples. Quando você usa um <xref:System.Data.DataRelation> do objeto, nenhum novo conjunto de registros é criado. Em vez disso, a DataRelation controla a relação entre tabelas e mantém registros pai e filho em sincronia.

## <a name="datarelation-objects-and-constraints"></a>Objetos DataRelation e restrições
Um <xref:System.Data.DataRelation> objeto também é usado para criar e impor as restrições a seguir:

-   Uma restrição exclusiva, que garante que uma coluna na tabela contém sem duplicatas.

-   Uma restrição de chave estrangeira, que pode ser usada para manter a integridade referencial entre uma tabela pai e filho em um conjunto de dados.

Restrições que você especifica em uma <xref:System.Data.DataRelation> objeto são implementadas automaticamente criando objetos apropriados ou definindo propriedades. Se você cria uma restrição foreign key usando o <xref:System.Data.DataRelation> object, instâncias do <xref:System.Data.ForeignKeyConstraint> classe são adicionados à <xref:System.Data.DataRelation> do objeto <xref:System.Data.DataRelation.ChildKeyConstraint%2A> propriedade.

Uma restrição exclusiva é implementada simplesmente definindo a <xref:System.Data.DataColumn.Unique%2A> propriedade de uma coluna de dados para `true` ou pela adição de uma instância das <xref:System.Data.UniqueConstraint> classe para o <xref:System.Data.DataRelation> do objeto <xref:System.Data.DataRelation.ParentKeyConstraint%2A> propriedade. Para obter informações sobre suspender restrições em um conjunto de dados, consulte [desativar restrições ao preencher um conjunto de dados](../data-tools/turn-off-constraints-while-filling-a-dataset.md).

### <a name="referential-integrity-rules"></a>Regras de integridade referencial
Como parte da restrição foreign key, você pode especificar regras de integridade referencial que são aplicadas em três pontos:

-   Quando um registro pai é atualizado

-   Quando um registro pai é excluído

-   Quando uma alteração foi aceito ou rejeitada

As regras que você pode fazer são especificados no <xref:System.Data.Rule> enumeração e estão listadas na tabela a seguir.

|Regra de restrição de chave estrangeira|Ação|
| - |------------|
|<xref:System.Data.Rule.Cascade>|A alteração (update ou delete) feita no registro pai também é feita em registros relacionados na tabela filho.|
|<xref:System.Data.Rule.SetNull>|Registros filho não são excluídos, mas a chave estrangeira nos registros filho é definida como <xref:System.DBNull>. Com essa configuração, os registros filho podem ser deixados como "órfãos" — ou seja, eles não têm nenhuma relação com registros pai. **Observação:** usar essa regra pode resultar em dados inválidos na tabela filho.|
|<xref:System.Data.Rule.SetDefault>|A chave estrangeira nos registros filho relacionados é definida como seu valor padrão (conforme estabelecido da coluna <xref:System.Data.DataColumn.DefaultValue%2A> propriedade).|
|<xref:System.Data.Rule.None>|Nenhuma alteração é feita para registros filho relacionados. Com essa configuração, os registros filho podem conter referências a registros pai inválido.|

Para obter mais informações sobre atualizações em tabelas de conjunto de dados, consulte [salvar dados no banco de dados](../data-tools/save-data-back-to-the-database.md).

### <a name="constraint-only-relations"></a>Relações de restrição
Quando você cria um <xref:System.Data.DataRelation> do objeto, você tem a opção de especificar que a relação seja usada somente para impor restrições — ou seja, ele também não será usado para acessar registros relacionados. Você pode usar essa opção para gerar um conjunto de dados que é um pouco mais eficiente e que contém menos métodos que aquela com a capacidade de registros relacionados. No entanto, você não poderá acessar registros relacionados. Por exemplo, uma relação somente restrição impede a exclusão de um registro pai que ainda tem registros filho, e você não pode acessar os registros filho por meio do pai.

## <a name="manually-creating-a-data-relation-in-the-dataset-designer"></a>Criar manualmente uma relação de dados no Designer de conjunto de dados
Quando você cria tabelas de dados usando as ferramentas de design de dados no Visual Studio, as relações são criadas automaticamente se as informações podem ser obtidas da fonte de dados. Se você adicionar manualmente as tabelas de dados do **DataSet** guia da **caixa de ferramentas**, talvez você precise criar o relacionamento manualmente. Para obter informações sobre como criar <xref:System.Data.DataRelation> objetos programaticamente, consulte [adicionando DataRelations](/dotnet/framework/data/adonet/dataset-datatable-dataview/adding-datarelations).

As relações entre tabelas de dados são exibidos como linhas na **Dataset Designer**, com uma chave e uma marca inteligente ilustrando o aspecto de um-para-muitos da relação. Por padrão, o nome da relação não aparecem na superfície de design.

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

#### <a name="to-create-a-relationship-between-two-data-tables"></a>Para criar uma relação entre duas tabelas de dados

1.  Abra o conjunto de dados no **Designer de Conjunto de Dados**. Para obter mais informações, consulte [instruções passo a passo: Criando um conjunto de dados no Designer de conjunto de dados](walkthrough-creating-a-dataset-with-the-dataset-designer.md).

2.  Arraste uma **relação** objeto o **conjunto de dados** toolbox para a tabela de dados filho na relação.

     O **relação** caixa de diálogo é aberta, preenchendo as **tabela filho** caixa com a tabela que você arrastou o **relação** do objeto para.

3.  Selecione a tabela pai a partir de **tabela pai** caixa. A tabela pai contém registros no lado "um" de uma relação um-para-muitos.

4.  Verificar se a tabela filho correta é exibida na **tabela filho** caixa. A tabela filho contém registros no lado "muitos" de uma relação um-para-muitos.

5.  Digite um nome para a relação na **nome** caixa ou deixe o nome padrão com base nas tabelas selecionadas. Esse é o nome do real <xref:System.Data.DataRelation> objeto no código.

6.  Selecione as colunas que unem as tabelas na **colunas de chave** e **as colunas de chave estrangeira** lista.

7.  Selecione se deseja criar uma relação, restrição ou ambos.

8.  Marque ou desmarque a **Nested Relation** caixa. Selecionar esta opção define a <xref:System.Data.DataRelation.Nested%2A> propriedade para `true`, e ele faz com que o filho linhas de relação ser aninhadas dentro da coluna pai quando essas linhas são gravadas como dados XML ou sincronizadas com <xref:System.Xml.XmlDataDocument>. Para obter mais informações, consulte [aninhamento de DataRelations](/dotnet/framework/data/adonet/dataset-datatable-dataview/nesting-datarelations).

9. Defina as regras a serem impostos quando você estiver fazendo alterações em registros nessas tabelas. Para obter mais informações, consulte <xref:System.Data.Rule>.

10. Clique em **Okey** para criar a relação. Uma linha de relação é exibida no designer entre as duas tabelas.

#### <a name="to-display-a-relation-name-in-the-dataset-designer"></a>Para exibir um nome de relação no Designer de conjunto de dados

1.  Abra o conjunto de dados no **Designer de Conjunto de Dados**. Para obter mais informações, consulte [instruções passo a passo: Criando um conjunto de dados no Designer de conjunto de dados](walkthrough-creating-a-dataset-with-the-dataset-designer.md).

2.  Dos **dados** menu, selecione o **Mostrar rótulos de relação** comando para exibir o nome da relação. Desmarque desse comando para ocultar o nome da relação.

## <a name="see-also"></a>Consulte também

- [Criar e configurar conjuntos de dados no Visual Studio](../data-tools/create-and-configure-datasets-in-visual-studio.md)