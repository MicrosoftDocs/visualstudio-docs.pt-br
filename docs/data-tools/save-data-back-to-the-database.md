---
title: Salvar dados novamente no banco de dados
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- datasets [Visual Basic], validating data
- data validation, datasets
- data [Visual Studio], saving
- row version
- updating datasets, constraints
- datasets [Visual Basic], about datasets
- datasets [Visual Basic], merging
- updates, constraints in datasets
- saving data, about saving data
- datasets [Visual Basic], constraints
- TableAdapters
ms.assetid: afe6cb8a-dc6a-428b-b07b-903ac02c890b
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 493637f81df15fadf65d6c7d90e980e322919b13
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85281741"
---
# <a name="save-data-back-to-the-database"></a>Salvar dados novamente no banco de dados

O DataSet é uma cópia de dados na memória. Se você modificar esses dados, é uma boa prática salvar essas alterações de volta no banco de dado. Faça isso de uma das três maneiras:

- Chamando um dos `Update` métodos de um TableAdapter

- Chamando um dos `DBDirect` métodos do TableAdapter

- Chamando o `UpdateAll` método no TableAdapterManager que o Visual Studio gera para você quando o conjunto de um contém tabelas relacionadas a outras tabelas no conjunto de um

Quando os dados associam tabelas de DataSet a controles em uma página do Windows Form ou XAML, a arquitetura de vinculação de dados faz todo o trabalho para você.

Se você estiver familiarizado com os TableAdapters, poderá ir diretamente para um destes tópicos:

|Tópico|Descrição|
|-----------|-----------------|
|[Como inserir novos registros em um banco de dados](../data-tools/insert-new-records-into-a-database.md)|Como executar atualizações e inserções usando TableAdapters ou objetos de comando|
|[Atualizar dados usando um TableAdapter](../data-tools/update-data-by-using-a-tableadapter.md)|Como executar atualizações com TableAdapters|
|[Atualização hierárquica](../data-tools/hierarchical-update.md)|Como executar atualizações de um conjunto de informações com duas ou mais tabelas relacionadas|
|[Lidar com uma exceção de simultaneidade](../data-tools/handle-a-concurrency-exception.md)|Como tratar exceções quando dois usuários tentam alterar os mesmos dados em um banco de dado ao mesmo tempo|
|[Como salvar dados usando uma transação](../data-tools/save-data-by-using-a-transaction.md)|Como salvar dados em uma transação usando o sistema. Namespace de transações e um objeto TransactionScope|
|[Salvar dados em uma transação](../data-tools/save-data-in-a-transaction.md)|Walkthrough que cria um aplicativo Windows Forms para demonstrar o salvamento de dados em um banco de dado dentro de uma transação|
|[Salvar dados em um banco de dados (várias tabelas)](../data-tools/save-data-to-a-database-multiple-tables.md)|Como editar registros e salvar alterações em várias tabelas de volta no banco de dados|
|[Salvar dados de um objeto em um banco de dados](../data-tools/save-data-from-an-object-to-a-database.md)|Como passar dados de um objeto que não está em um DataSet para um Database usando um método DbDirect TableAdapter|
|[Salvando dados com os métodos DBDirect TableAdapter](../data-tools/save-data-with-the-tableadapter-dbdirect-methods.md)|Como usar o TableAdapter para enviar consultas SQL diretamente para o banco de dados|
|[Salvar um conjunto de dados como XML](../data-tools/save-a-dataset-as-xml.md)|Como salvar um conjunto de um DataSet em um documento XML|

## <a name="two-stage-updates"></a>Atualizações de dois estágios

A atualização de uma fonte de dados é um processo de duas etapas. A primeira etapa é atualizar o conjunto de recursos com novos registros, registros alterados ou registros excluídos. Se seu aplicativo nunca enviar essas alterações de volta para a fonte de dados, você terá concluído a atualização.

Se você enviar as alterações de volta ao banco de dados, uma segunda etapa será necessária. Se você não estiver usando controles vinculados a dados, será necessário chamar manualmente o `Update` método do mesmo TableAdapter (ou adaptador de dados) que você usou para popular o DataSet. No entanto, você também pode usar adaptadores diferentes, por exemplo, para mover dados de uma fonte de dados para outra ou para atualizar várias fontes de dados. Se você não estiver usando a vinculação de dados e estiver salvando alterações para tabelas relacionadas, será necessário instanciar manualmente uma variável da classe gerada automaticamente `TableAdapterManager` e, em seguida, chamar seu `UpdateAll` método.

![Diagrama conceitual de atualizações de DataSet](../data-tools/media/vbdatasetupdates.gif)

Um conjunto de registros contém coleções de tabelas, que contêm coleções de linhas. Se você pretende atualizar uma fonte de dados subjacente posteriormente, deve usar os métodos na `DataTable.DataRowCollection` propriedade ao adicionar ou remover linhas. Esses métodos executam o controle de alterações necessário para atualizar a fonte de dados. Se você chamar a `RemoveAt` coleção na propriedade Rows, a exclusão não será comunicada de volta ao banco de dados.

## <a name="merge-datasets"></a>Mesclar conjuntos de os

Você pode atualizar o conteúdo de um conjunto de um DataSet *mesclando* -o com outro conjunto de um. Isso envolve a cópia do conteúdo de um conjunto de *fonte de origem* para o conjunto de código de chamada (referido como o DataSet de *destino* ). Quando você mescla conjuntos de os, os novos registros no conjunto de recursos de origem são adicionados ao conjunto de fonte de destino. Além disso, colunas extras no conjunto de fonte de origem são adicionadas ao DataSet de destino. A mesclagem de conjuntos de aplicativos é útil quando você tem um conjunto de um DataSet local e Obtém um segundo conjunto de um outro aplicativo. Ele também é útil quando você obtém um segundo conjunto de dados de um componente, como um Web Service XML, ou quando você precisa integrá-los a partir de vários DataSets.

Ao mesclar conjuntos de valores, você pode passar um argumento booliano ( `preserveChanges` ) que informa ao <xref:System.Data.DataSet.Merge%2A> método se as modificações existentes devem ser retidas no conjunto de valores de destino. Como os conjuntos de informações mantêm várias versões de registros, é importante ter em mente que mais de uma versão dos registros está sendo mesclada. A tabela a seguir mostra como um registro em dois conjuntos de valores é mesclado:

|DataRowVersion|Conjunto de dados de destino|Conjunto de dados de origem|
| - | - | - |
|Original|James Wilson|James C. Wilson|
|Current|Jim Wilson|James C. Wilson|

Chamar o <xref:System.Data.DataSet.Merge%2A> método na tabela anterior com `preserveChanges=false targetDataset.Merge(sourceDataset)` resultados nos seguintes dados:

|DataRowVersion|Conjunto de dados de destino|Conjunto de dados de origem|
| - | - | - |
|Original|James C. Wilson|James C. Wilson|
|Current|James C. Wilson|James C. Wilson|

Chamar o <xref:System.Data.DataSet.Merge%2A> método com `preserveChanges = true targetDataset.Merge(sourceDataset, true)` resulta nos seguintes dados:

|DataRowVersion|Conjunto de dados de destino|Conjunto de dados de origem|
| - | - | - |
|Original|James C. Wilson|James C. Wilson|
|Current|Jim Wilson|James C. Wilson|

> [!CAUTION]
> No `preserveChanges = true` cenário, se o <xref:System.Data.DataSet.RejectChanges%2A> método for chamado em um registro no conjunto de dados de destino, ele será revertido para os dados originais do DataSet de *origem* . Isso significa que se você tentar atualizar a fonte de dados original com o DataSet de destino, talvez não seja possível localizar a linha original a ser atualizada. Você pode evitar uma violação de simultaneidade preenchendo outro conjunto de dados com os registros atualizados da fonte e, em seguida, executando uma mesclagem para evitar uma violação de simultaneidade. (Uma violação de simultaneidade ocorre quando outro usuário modifica um registro na fonte de dados depois que ele é preenchido.)

## <a name="update-constraints"></a>Atualizar restrições

Para fazer alterações em uma linha de dados existente, adicione ou atualize dados nas colunas individuais. Se o conjunto de registros contiver restrições (como chaves estrangeiras ou restrições não anuláveis), é possível que o registro esteja temporariamente em um estado de erro à medida que você atualizá-lo. Ou seja, ele pode estar em um estado de erro depois que você terminar de atualizar uma coluna, mas antes de chegar ao próximo.

Para evitar violações de restrição prematuro, você pode suspender temporariamente as restrições de atualização. Isso serve para duas finalidades:

- Isso impede que um erro seja gerado depois que você terminar de atualizar uma coluna, mas não tiver iniciado a atualização de outra.

- Ele impede que determinados eventos de atualização sejam gerados (eventos que geralmente são usados para validação).

> [!NOTE]
> No Windows Forms, a arquitetura de vinculação de dados criada no DataGrid suspende a verificação de restrição até que o foco saia de uma linha e você não precise chamar explicitamente os <xref:System.Data.DataRow.BeginEdit%2A> <xref:System.Data.DataRow.EndEdit%2A> métodos, ou <xref:System.Data.DataRow.CancelEdit%2A> .

As restrições são desabilitadas automaticamente quando o <xref:System.Data.DataSet.Merge%2A> método é invocado em um conjunto de uma. Quando a mesclagem for concluída, se houver alguma restrição no conjunto de um que não possa ser habilitado, um <xref:System.Data.ConstraintException> será gerado. Nessa situação, a <xref:System.Data.DataSet.EnforceConstraints%2A> propriedade é definida como `false,` e todas as violações de restrição devem ser resolvidas antes de redefinir a <xref:System.Data.DataSet.EnforceConstraints%2A> propriedade para `true` .

Depois de concluir uma atualização, você pode reabilitar a verificação de restrição, que também habilita novamente os eventos de atualização e os gera.

Para obter mais informações sobre como suspender eventos, consulte [desativar restrições ao preencher um conjunto de](../data-tools/turn-off-constraints-while-filling-a-dataset.md)dados.

## <a name="dataset-update-errors"></a>Erros de atualização do conjunto de atualizações

Quando você atualiza um registro em um conjunto de registros, há a possibilidade de um erro. Por exemplo, você pode, inadvertidamente, gravar dados do tipo errado em uma coluna ou dados muito longos ou dados que tenham algum outro problema de integridade. Ou, você pode ter verificações de validação específicas do aplicativo que podem gerar erros personalizados durante qualquer estágio de um evento de atualização. Para obter mais informações, consulte [Validate data in DataSets](../data-tools/validate-data-in-datasets.md).

## <a name="maintain-information-about-changes"></a>Manter informações sobre alterações

As informações sobre as alterações em um conjunto de dados são mantidas de duas maneiras: sinalizando linhas que indicam que foram alteradas ( <xref:System.Data.DataRow.RowState%2A> ) e mantendo várias cópias de um registro ( <xref:System.Data.DataRowVersion> ). Usando essas informações, os processos podem determinar o que foi alterado no conjunto de dados e podem enviar as atualizações apropriadas para a fonte.

### <a name="rowstate-property"></a>Propriedade RowState

A <xref:System.Data.DataRow.RowState%2A> propriedade de um <xref:System.Data.DataRow> objeto é um valor que fornece informações sobre o status de uma linha de dados específica.

A tabela a seguir detalha os possíveis valores da <xref:System.Data.DataRowState> enumeração:

|Valor de DataRowState|Descrição|
| - |-----------------|
|<xref:System.Data.DataRowState.Added>|A linha foi adicionada como um item a um <xref:System.Data.DataRowCollection> . (Uma linha nesse estado não tem uma versão original correspondente, pois ela não existia quando o último <xref:System.Data.DataRow.AcceptChanges%2A> método foi chamado).|
|<xref:System.Data.DataRowState.Deleted>|A linha foi excluída usando o <xref:System.Data.DataRow.Delete%2A> de um <xref:System.Data.DataRow> objeto.|
|<xref:System.Data.DataRowState.Detached>|A linha foi criada, mas não faz parte de nenhum <xref:System.Data.DataRowCollection>. Um <xref:System.Data.DataRow> objeto está nesse estado imediatamente após ele ter sido criado, antes de ser adicionado a uma coleção e depois de ser removido de uma coleção.|
|<xref:System.Data.DataRowState.Modified>|Um valor de coluna na linha foi alterado de alguma forma.|
|<xref:System.Data.DataRowState.Unchanged>|A linha não foi alterada desde a última chamada a <xref:System.Data.DataRow.AcceptChanges%2A>.|

### <a name="datarowversion-enumeration"></a>Enumeração DataRowVersion

Os conjuntos de valores mantêm várias versões de registros. Os <xref:System.Data.DataRowVersion> campos são usados ao recuperar o valor encontrado em um <xref:System.Data.DataRow> usando a <xref:System.Data.DataRow.Item%2A> propriedade ou o <xref:System.Data.DataRow.GetChildRows%2A> método do <xref:System.Data.DataRow> objeto.

A tabela a seguir detalha os possíveis valores da <xref:System.Data.DataRowVersion> enumeração:

|Valor de DataRowVersion|Descrição|
| - |-----------------|
|<xref:System.Data.DataRowVersion.Current>|A versão atual de um registro contém todas as modificações que foram executadas no registro desde a última vez que o <xref:System.Data.DataRow.AcceptChanges%2A> foi chamado. Se a linha tiver sido excluída, não haverá nenhuma versão atual.|
|<xref:System.Data.DataRowVersion.Default>|O valor padrão de um registro, conforme definido pelo esquema ou pela fonte de dados do conjunto.|
|<xref:System.Data.DataRowVersion.Original>|A versão original de um registro é uma cópia do registro como foi a última vez que as alterações foram confirmadas no conjunto de registros. Em termos práticos, normalmente essa é a versão de um registro como lido de uma fonte de dados.|
|<xref:System.Data.DataRowVersion.Proposed>|A versão proposta de um registro que está disponível temporariamente enquanto você está no meio de uma atualização — ou seja, entre a hora em que você chamou o <xref:System.Data.DataRow.BeginEdit%2A> método e o <xref:System.Data.DataRow.EndEdit%2A> método. Normalmente, você acessa a versão proposta de um registro em um manipulador para um evento, como <xref:System.Data.DataTable.RowChanging> . Invocar o <xref:System.Data.DataRow.CancelEdit%2A> método reverte as alterações e exclui a versão proposta da linha de dados.|

As versões original e atual são úteis quando as informações de atualização são transmitidas para uma fonte de dados. Normalmente, quando uma atualização é enviada para a fonte de dados, as novas informações do banco de dado estão na versão atual de um registro. As informações da versão original são usadas para localizar o registro a ser atualizado.

Por exemplo, em um caso em que a chave primária de um registro é alterada, você precisa de uma maneira de localizar o registro correto na fonte de dados para atualizar as alterações. Se nenhuma versão original existir, o registro provavelmente será acrescentado à fonte de dados, resultando não apenas em um registro adicional indesejado, mas em um registro que não é preciso e desatualizado. As duas versões também são usadas no controle de simultaneidade. Você pode comparar a versão original com um registro na fonte de dados para determinar se o registro foi alterado desde que ele foi carregado no conjunto.

A versão proposta é útil quando você precisa executar a validação antes de realmente confirmar as alterações no conjunto de os.

Mesmo que os registros tenham mudado, nem sempre há versões originais ou atuais dessa linha. Quando você insere uma nova linha na tabela, não há nenhuma versão original, apenas uma versão atual. Da mesma forma, se você excluir uma linha chamando o método da tabela `Delete` , haverá uma versão original, mas nenhuma versão atual.

Você pode testar para ver se existe uma versão específica de um registro consultando o método de uma linha de dados <xref:System.Data.DataRow.HasVersion%2A> . Você pode acessar qualquer uma das versões de um registro, passando um <xref:System.Data.DataRowVersion> valor de enumeração como um argumento opcional ao solicitar o valor de uma coluna.

## <a name="get-changed-records"></a>Obter registros alterados

É uma prática comum não atualizar todos os registros em um conjunto de um. Por exemplo, um usuário pode estar trabalhando com um controle de Windows Forms <xref:System.Windows.Forms.DataGridView> que exibe vários registros. No entanto, o usuário pode atualizar apenas alguns registros, excluir um e inserir um novo. DataSets e tabelas de dados fornecem um método ( `GetChanges` ) para retornar apenas as linhas que foram modificadas.

Você pode criar subconjuntos de registros alterados usando o `GetChanges` método de uma tabela de dados ( <xref:System.Data.DataTable.GetChanges%2A> ) ou do conjunto ( <xref:System.Data.DataSet.GetChanges%2A> ). Se você chamar o método para a tabela de dados, ele retornará uma cópia da tabela com apenas os registros alterados. Da mesma forma, se você chamar o método no conjunto de registros, obterá um novo conjunto de novos com os registros alterados.

`GetChanges`por si só, retorna todos os registros alterados. Por outro lado, ao passar o desejado <xref:System.Data.DataRowState> como um parâmetro para o `GetChanges` método, você pode especificar qual subconjunto de registros alterados deseja: registros recém-adicionados, registros que são marcados para exclusão, registros desanexados ou registros modificados.

Obter um subconjunto de registros alterados é útil quando você deseja enviar registros para outro componente para processamento. Em vez de enviar o conjunto de registros inteiro, você pode reduzir a sobrecarga de comunicação com o outro componente obtendo apenas os registros de que o componente precisa.

## <a name="commit-changes-in-the-dataset"></a>Confirmar alterações no conjunto de

Conforme as alterações são feitas no conjunto de registros, a <xref:System.Data.DataRow.RowState%2A> propriedade das linhas alteradas é definida. As versões original e atual dos registros são estabelecidas, mantidas e disponibilizadas para você pela <xref:System.Data.DataRowView.RowVersion%2A> propriedade. Os metadados armazenados nas propriedades dessas linhas alteradas são necessários para enviar as atualizações corretas para a fonte de dados.

Se as alterações refletirem o estado atual da fonte de dados, você não precisará mais manter essas informações. Normalmente, há duas ocasiões em que o conjunto de e sua fonte estão em sincronia:

- Imediatamente após você ter carregado as informações no conjunto de dados, como quando você lê o dado da origem.

- Depois de enviar as alterações do conjunto de dados para a origem (mas não antes, porque você perderia as informações de alteração necessárias para enviar alterações ao banco de dado).

Você pode confirmar as alterações pendentes para o conjunto de acordo chamando o <xref:System.Data.DataSet.AcceptChanges%2A> método. Normalmente, <xref:System.Data.DataSet.AcceptChanges%2A> é chamado nos seguintes horários:

- Depois de carregar o conjunto de um. Se você carregar um conjunto de um dataset chamando o método de um TableAdapter `Fill` , o adaptador automaticamente confirmará as alterações para você. No entanto, se você carregar um conjunto de um DataSet mesclando outro conjunto de um para ele, precisará confirmar as alterações manualmente.

    > [!NOTE]
    > Você pode impedir que o adaptador confirme automaticamente as alterações ao chamar o `Fill` método definindo a `AcceptChangesDuringFill` Propriedade do adaptador como `false` . Se for definido como `false` , o <xref:System.Data.DataRow.RowState%2A> de cada linha inserida durante o preenchimento será definido como <xref:System.Data.DataRowState.Added> .

- Depois de enviar alterações de conjunto de um para outro processo, como um serviço Web XML.

    > [!CAUTION]
    > Confirmar a alteração dessa forma apaga qualquer informação de alteração. Não confirme as alterações até concluir a execução de operações que exigem que seu aplicativo saiba quais alterações foram feitas no conjunto de aplicativos.

Esse método realiza o seguinte:

- Grava a <xref:System.Data.DataRowVersion.Current> versão de um registro em sua <xref:System.Data.DataRowVersion.Original> versão e substitui a versão original.

- Remove qualquer linha para a qual a <xref:System.Data.DataRow.RowState%2A> propriedade está definida <xref:System.Data.DataRowState.Deleted> .

- Define a <xref:System.Data.DataRow.RowState%2A> propriedade de um registro como <xref:System.Data.DataRowState.Unchanged> .

O <xref:System.Data.DataSet.AcceptChanges%2A> método está disponível em três níveis. Você pode chamá-lo em um <xref:System.Data.DataRow> objeto para confirmar as alterações apenas dessa linha. Você também pode chamá-lo em um <xref:System.Data.DataTable> objeto para confirmar todas as linhas de uma tabela. Por fim, você pode chamá-lo no <xref:System.Data.DataSet> objeto para confirmar todas as alterações pendentes em todos os registros de todas as tabelas do conjunto de recursos.

A tabela a seguir descreve quais alterações são confirmadas com base em qual objeto o método é chamado:

|Método|Result|
|------------|------------|
|<xref:System.Data.DataRow.AcceptChanges%2A?displayProperty=fullName>|As alterações são confirmadas somente na linha específica.|
|<xref:System.Data.DataTable.AcceptChanges%2A?displayProperty=fullName>|As alterações são confirmadas em todas as linhas na tabela específica.|
|<xref:System.Data.DataSet.AcceptChanges%2A?displayProperty=fullName>|As alterações são confirmadas em todas as linhas em todas as tabelas do conjunto de registros.|

> [!NOTE]
> Se você carregar um conjunto de um dataset chamando o método de um TableAdapter `Fill` , não precisará aceitar as alterações explicitamente. Por padrão, o `Fill` método chama o `AcceptChanges` método depois de concluir o preenchimento da tabela de dados.

Um método relacionado, <xref:System.Data.DataSet.RejectChanges%2A> , desfaz o efeito das alterações copiando a <xref:System.Data.DataRowVersion.Original> versão de volta para a <xref:System.Data.DataRowVersion.Current> versão dos registros. Ele também define o <xref:System.Data.DataRow.RowState%2A> de cada registro de volta para <xref:System.Data.DataRowState.Unchanged> .

## <a name="data-validation"></a>Validação de dados

Para verificar se os dados em seu aplicativo atendem aos requisitos dos processos para os quais ele foi passado, muitas vezes você precisa adicionar a validação. Isso pode envolver a verificação de que a entrada de um usuário em um formulário está correta, Validando os dados que são enviados ao seu aplicativo por outro aplicativo ou até mesmo verificando se as informações calculadas em seu componente se enquadram nas restrições da fonte de dados e dos requisitos do aplicativo.

Você pode validar os dados de várias maneiras:

- Na camada de negócios, adicionando código ao seu aplicativo para validar dados. O conjunto de espaço de os é um lugar que você pode fazer. O conjunto de recursos fornece algumas das vantagens da validação de back-end, como a capacidade de validar alterações, pois os valores de coluna e de linha estão sendo alterados. Para obter mais informações, consulte [Validate data in DataSets](../data-tools/validate-data-in-datasets.md).

- Na camada de apresentação, adicionando validação a formulários. Para obter mais informações, consulte [validação de entrada do usuário em Windows Forms](/dotnet/framework/winforms/user-input-validation-in-windows-forms).

- No back-end de dados, enviando dados para a fonte de dados — por exemplo, o banco de dado — e permitindo que ele aceite ou rejeite os dados. Se você estiver trabalhando com um banco de dados que tenha recursos sofisticados para validação de dado e fornecimento de informações de erro, isso pode ser uma abordagem prática porque você pode validar os dados independentemente de onde eles vêm. No entanto, essa abordagem pode não acomodar requisitos de validação específicos do aplicativo. Além disso, ter a fonte de dados validar dados pode resultar em várias viagens de ida e volta para a fonte de dados, dependendo de como seu aplicativo facilita a resolução de erros de validação gerados pelo back-end.

   > [!IMPORTANT]
   > Ao usar comandos de dados com uma <xref:System.Data.SqlClient.SqlCommand.CommandType%2A> propriedade definida como <xref:System.Data.CommandType.Text> , verifique cuidadosamente as informações enviadas de um cliente antes de passá-las para o banco de dados. Usuários maliciosos podem tentar enviar (injetar) instruções SQL modificadas ou adicionais para obter acesso não autorizado ou para danificar o banco de dados. Antes de transferir a entrada do usuário para um banco de dados, sempre verifique se as informações são válidas. É uma prática recomendada sempre usar consultas parametrizadas ou procedimentos armazenados quando possível.

## <a name="transmit-updates-to-the-data-source"></a>Transmitir atualizações para a fonte de dados

Depois que as alterações tiverem sido feitas em um conjunto de dados, você poderá transmitir as alterações para uma fonte. Normalmente, você faz isso chamando o `Update` método de um TableAdapter (ou adaptador de dados). O método percorre cada registro em uma tabela de dados, determina qual tipo de atualização é necessário (Update, INSERT ou Delete), se houver, e executa o comando apropriado.

Como uma ilustração de como as atualizações são feitas, suponha que seu aplicativo use um conjunto de dados que contenha uma única tabela. O aplicativo busca duas linhas do banco de dados. Após a recuperação, a tabela de dados na memória tem esta aparência:

```sql
(RowState)     CustomerID   Name             Status
(Unchanged)    c200         Robert Lyon      Good
(Unchanged)    c400         Nancy Buchanan    Pending
```

Seu aplicativo altera o status de Nancy Buchanan para "preferencial". Como resultado dessa alteração, o valor da <xref:System.Data.DataRow.RowState%2A> propriedade para essa linha muda de <xref:System.Data.DataRowState.Unchanged> para <xref:System.Data.DataRowState.Modified> . O valor da <xref:System.Data.DataRow.RowState%2A> propriedade para a primeira linha permanece <xref:System.Data.DataRowState.Unchanged> . A tabela de dados agora tem esta aparência:

```sql
(RowState)     CustomerID   Name             Status
(Unchanged)    c200         Robert Lyon      Good
(Modified)     c400         Nancy Buchanan    Preferred
```

Agora, seu aplicativo chama o `Update` método para transmitir o conjunto de dados para o Database. O método inspeciona cada linha por vez. Para a primeira linha, o método transmite nenhuma instrução SQL para o banco de dados porque essa linha não foi alterada desde que foi obtida originalmente do banco de dados.

No entanto, para a segunda linha, o `Update` método invoca automaticamente o comando de dados correto e o transmite para o banco de dado. A sintaxe específica da instrução SQL depende do dialeto do SQL com suporte do armazenamento de dados subjacente. Mas, as seguintes características gerais da instrução SQL transmitida são notáveis:

- A instrução SQL transmitida é uma instrução UPDATE. O adaptador sabe usar uma instrução UPDATE porque o valor da <xref:System.Data.DataRow.RowState%2A> propriedade é <xref:System.Data.DataRowState.Modified> .

- A instrução SQL transmitida inclui uma cláusula WHERE que indica que o destino da instrução UPDATE é a linha em que `CustomerID = 'c400'` . Essa parte da instrução SELECT distingue a linha de destino de todas as outras porque a `CustomerID` é a chave primária da tabela de destino. As informações da cláusula WHERE são derivadas da versão original do registro ( `DataRowVersion.Original` ), caso os valores necessários para identificar a linha tenham sido alterados.

- A instrução SQL transmitida inclui a cláusula SET, para definir os novos valores das colunas modificadas.

   > [!NOTE]
   > Se a propriedade do TableAdapter `UpdateCommand` tiver sido definida como o nome de um procedimento armazenado, o adaptador não construirá uma instrução SQL. Em vez disso, ele invoca o procedimento armazenado com os parâmetros apropriados passados.

## <a name="pass-parameters"></a>Passar parâmetros

Normalmente, você usa parâmetros para passar os valores para os registros que serão atualizados no banco de dados. Quando o método do TableAdapter `Update` executa uma instrução UPDATE, ele precisa preencher os valores de parâmetro. Ele obtém esses valores da `Parameters` coleção para o comando de dados apropriado — nesse caso, o `UpdateCommand` objeto no TableAdapter.

Se você usou as ferramentas do Visual Studio para gerar um adaptador de dados, o `UpdateCommand` objeto contém uma coleção de parâmetros que correspondem a cada espaço reservado de parâmetro na instrução.

A <xref:System.Data.SqlClient.SqlParameter.SourceColumn%2A?displayProperty=fullName> propriedade de cada parâmetro aponta para uma coluna na tabela de dados. Por exemplo, a `SourceColumn` propriedade para os `au_id` `Original_au_id` parâmetros e é definida como qualquer coluna na tabela de dados que contenha a ID do autor. Quando o método do adaptador `Update` é executado, ele lê a coluna ID do autor do registro que está sendo atualizado e preenche os valores na instrução.

Em uma instrução UPDATE, você precisa especificar os novos valores (aqueles que serão gravados no registro), bem como os valores antigos (para que o registro possa ser localizado no banco de dados). Há, portanto, dois parâmetros para cada valor: um para a cláusula SET e outro para a cláusula WHERE. Ambos os parâmetros lêem dados do registro que está sendo atualizado, mas eles obtêm versões diferentes do valor da coluna com base na Propriedade do parâmetro <xref:System.Data.SqlClient.SqlParameter.SourceVersion> . O parâmetro da cláusula SET Obtém a versão atual e o parâmetro da cláusula WHERE Obtém a versão original.

> [!NOTE]
> Você também pode definir valores na `Parameters` coleção por conta própria no código, que normalmente faria em um manipulador de eventos para o evento do adaptador de dados <xref:System.Data.DataTable.RowChanging> .

## <a name="see-also"></a>Veja também

- [Ferramentas de conjunto de dados no Visual Studio](../data-tools/dataset-tools-in-visual-studio.md)
- [Criar e configurar TableAdapters](create-and-configure-tableadapters.md)
- [Atualizar dados usando um TableAdapter](../data-tools/update-data-by-using-a-tableadapter.md)
- [Associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md)
- [Validar os dados](validate-data-in-datasets.md)
- [Como: Adicionar, modificar e excluir entidades (WCF Data Services)](/dotnet/framework/data/wcf/how-to-add-modify-and-delete-entities-wcf-data-services)
