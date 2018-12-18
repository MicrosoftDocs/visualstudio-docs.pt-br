---
title: Salvar dados no banco de dados | Microsoft Docs
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
caps.latest.revision: 31
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 6b6fd99b2b1a41d6baa3a110b2a595afb1dd7e3f
ms.sourcegitcommit: c9a01c599ce19a5845605b3b28c0229fd0abb93f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2018
ms.locfileid: "52281843"
---
# <a name="save-data-back-to-the-database"></a>Salvar dados novamente no banco de dados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
O conjunto de dados é uma cópia na memória dos dados. Se você modificar esses dados, é uma boa prática para salvar essas alterações no banco de dados. Você fazer isso em uma destas três maneiras:  
  
- Chamando um do `Update` métodos de um TableAdapter  
  
- Chamando um dos métodos DBDirect TableAdapter  
  
- Chamando o método UpdateAll no `TableAdapterManager` que o Visual Studio gera para você quando o conjunto de dados contiver tabelas relacionadas a outras tabelas no conjunto de dados  
  
  Ao associar dados a tabelas de conjunto de dados a controles em uma página de formulário do Windows ou XAML, a arquitetura de vinculação de dados faz todo o trabalho para você.  
  
  Se você estiver familiarizado com TableAdapters, você pode ir diretamente para um destes tópicos:  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Como inserir novos registros em um banco de dados](../data-tools/insert-new-records-into-a-database.md)|Como executar atualizações e inserções usando objetos de comando ou TableAdapters|  
|[Atualizar dados usando um TableAdapter](../data-tools/update-data-by-using-a-tableadapter.md)|Como realizar atualizações com TableAdapters|  
|[Atualização hierárquica](../data-tools/hierarchical-update.md)|Como realizar atualizações de um conjunto de dados com duas ou mais tabelas relacionadas|  
|[Lidar com uma exceção de simultaneidade](../data-tools/handle-a-concurrency-exception.md)|Como tratar exceções quando dois usuários tentam alterar os mesmos dados em um banco de dados ao mesmo tempo|  
|[Como salvar dados pelo uso de uma transação](../data-tools/save-data-by-using-a-transaction.md)|Como salvar dados em uma transação usando o objeto TransactionScope e o namespace System. Transactions|  
|[Salvando dados em uma transação](../data-tools/save-data-in-a-transaction.md)|Como salvar dados em uma transação usando o namespace System. Transactions|  
|[Salvar dados em um banco de dados (várias tabelas)](../data-tools/save-data-to-a-database-multiple-tables.md)|Como editar registros e salvar alterações em várias tabelas no banco de dados|  
|[Salvar dados de um objeto em um banco de dados](../data-tools/save-data-from-an-object-to-a-database.md)|Como transmitir dados de um objeto que não está em um conjunto de dados para um banco de dados usando um método TableAdapter DbDirect|  
|[Salvando dados com os métodos DBDirect TableAdapter](../data-tools/save-data-with-the-tableadapter-dbdirect-methods.md)|Como usar o TableAdapter para enviar consultas SQL diretamente para o banco de dados|  
|[Salvar um conjunto de dados como XML](../data-tools/save-a-dataset-as-xml.md)|Como salvar um conjunto de dados em um documento XML|  
  
## <a name="two-stage-updates"></a>Atualizações de dois estágios  
 Atualizar uma fonte de dados é um processo de duas etapas. A primeira etapa é atualizar o conjunto de dados com novos registros, registros alterados ou registros excluídos. Se seu aplicativo nunca enviar essas alterações de volta para a fonte de dados, em seguida, você terá concluído com a atualização.  
  
 Se você enviar as alterações no banco de dados, uma segunda etapa é necessária. Se você não estiver usando controles ligados a dados, você precisa chamar manualmente o método Update do mesmo TableAdapter (ou adaptador de dados) que você usou para preencher o conjunto de dados. No entanto, você também pode usar adaptadores diferentes, por exemplo, para mover dados de uma fonte de dados para outro ou para atualizar várias fontes de dados. Se você não estiver usando a associação de dados e está salvando as alterações para tabelas relacionadas, você precisa instanciar manualmente uma variável da classe TableAdapterManager gerado automaticamente e, em seguida, chame seu método UpdateAll.  
  
 ![Atualizações de conjunto de dados do Visual Basic](../data-tools/media/vbdatasetupdates.gif "vbDatasetUpdates")  
Processo de atualização de dois estágios e a função do DataRowVersion em uma atualização bem-sucedida  
  
 Um conjunto de dados contém coleções de tabelas, que contêm uma coleção de linhas. Se você pretende atualizar uma fonte de dados subjacente mais tarde, você deve usar os métodos na propriedade DataTable.DataRowCollection quando adicionar ou remover linhas. Esses métodos realizam o controle de alterações que é necessário para atualizar a fonte de dados. Se você chamar a coleção RemoveAt na propriedade de linhas, a exclusão não ser comunicada de volta para o banco de dados.  
  
## <a name="merge-datasets"></a>Mesclar conjuntos de dados  
 Você pode atualizar o conteúdo de um conjunto de dados por *mesclando* -lo com outro conjunto de dados. Isso envolve copiar o conteúdo de um *fonte* conjunto de dados para o dataset chamado (conhecido como o *destino* conjunto de dados). Ao mesclar conjuntos de dados, novos registros no conjunto de dados de origem são adicionados ao conjunto de dados de destino. Além disso, as colunas extras no conjunto de dados de origem são adicionadas ao conjunto de dados de destino. Mesclar conjuntos de dados é útil quando você tem um conjunto de dados local e obter um segundo conjunto de dados de outro aplicativo. Também é útil quando você receber um segundo conjunto de dados de um componente como um serviço web XML, ou quando você precisar integrar dados de vários conjuntos de dados.  
  
 Ao mesclar conjuntos de dados, você pode passar um argumento booleano (`preserveChanges`) que informa o <xref:System.Data.DataSet.Merge%2A> método se deseja manter modificações existentes no conjunto de dados de destino. Como conjuntos de dados mantém várias versões de registros, é importante ter em mente que mais de uma versão dos registros está sendo mesclada. A tabela a seguir mostra como um registro em dois conjuntos de dados é mesclado:  
  
|DataRowVersion|Conjunto de dados de destino|Conjunto de dados de origem|  
|--------------------|--------------------|--------------------|  
|Original|James Wilson|James C. Wilson|  
|Atual|Jim Wilson|James C. Wilson|  
  
 Chamar o <xref:System.Data.DataSet.Merge%2A> método na tabela anterior com `preserveChanges=false targetDataset.Merge(sourceDataset)` resulta no seguinte:  
  
|DataRowVersion|Conjunto de dados de destino|Conjunto de dados de origem|  
|--------------------|--------------------|--------------------|  
|Original|James C. Wilson|James C. Wilson|  
|Atual|James C. Wilson|James C. Wilson|  
  
 Chamar o <xref:System.Data.DataSet.Merge%2A> método com `preserveChanges = true targetDataset.Merge(sourceDataset, true)` resulta no seguinte:  
  
|DataRowVersion|Conjunto de dados de destino|Conjunto de dados de origem|  
|--------------------|--------------------|--------------------|  
|Original|James C. Wilson|James C. Wilson|  
|Atual|Jim Wilson|James C. Wilson|  
  
> [!CAUTION]
>  No `preserveChanges = true` cenário, se o <xref:System.Data.DataSet.RejectChanges%2A> método é chamado em um registro no conjunto de dados de destino, em seguida, ele será revertido para os dados originais da *origem* conjunto de dados. Isso significa que, se você tentar atualizar a fonte de dados original com o conjunto de dados de destino, talvez ele não conseguir localizar a linha original para atualizar. Você pode impedir uma violação de simultaneidade preenchendo outro conjunto de dados com os registros atualizados da fonte de dados e, em seguida, executar uma mesclagem para impedir uma violação de simultaneidade. (Uma violação de simultaneidade ocorre quando outro usuário modifica um registro na fonte de dados depois que o conjunto de dados tiver sido preenchido.)  
  
## <a name="update-constraints"></a>Restrições de atualização  
 Para fazer alterações em uma linha de dados existente, adicionar ou atualizar dados nas colunas individuais. Se o conjunto de dados contiver restrições (como chaves estrangeiras ou restrições não anuláveis), é possível que o registro pode ser temporariamente em um estado de erro conforme você atualizá-lo. Ou seja, ele pode ser em um estado de erro depois de concluir a atualização de uma coluna, mas antes de chegar ao próximo.  
  
 Para evitar violações de restrição, você pode suspender temporariamente as restrições de atualização. Isso serve para duas finalidades:  
  
- Ela impede que um erro que está sendo gerada depois que você terminar de atualizar uma coluna, mas ainda não tiver a atualização foi iniciada outra.  
  
- Impede a atualização de determinados eventos sejam acionados (eventos que são geralmente usados para validação).  
  
  Depois de concluir uma atualização, você pode habilitar novamente verificação de restrição, que também habilita novamente os eventos de atualização e gera-os.  
  
> [!NOTE]
>  No Windows Forms, a arquitetura de vinculação de dados que é incorporada ao datagrid suspende a restrição de verificação até que o foco sair de uma linha, e você não precisará chamar explicitamente o <xref:System.Data.DataRow.BeginEdit%2A>, <xref:System.Data.DataRow.EndEdit%2A>, ou <xref:System.Data.DataRow.CancelEdit%2A> métodos.  
  
 As restrições são automaticamente desativado quando o <xref:System.Data.DataSet.Merge%2A> método é invocado em um conjunto de dados. Quando a mesclagem for concluída, se houver qualquer restrição no conjunto de dados não pode ser habilitado, um <xref:System.Data.ConstraintException> é gerada. Nessa situação, o <xref:System.Data.DataSet.EnforceConstraints%2A> estiver definida como `false,` e todas as violações de restrição devem ser resolvidas antes de redefinir o <xref:System.Data.DataSet.EnforceConstraints%2A> propriedade `true`.  
  
 Depois de concluir uma atualização, você pode habilitar novamente verificação de restrição, que também habilita novamente os eventos de atualização e gera-os.  
  
 Para obter mais informações sobre a suspensão de eventos, consulte [desativar restrições ao preencher um conjunto de dados](../data-tools/turn-off-constraints-while-filling-a-dataset.md).  
  
## <a name="dataset-update-errors"></a>Erros de atualização do conjunto de dados  
 Quando você atualiza um registro em um conjunto de dados, há a possibilidade de um erro. Por exemplo, você pode inadvertidamente gravar dados do tipo incorreto a uma coluna, ou dados que é muito longos ou dados que tem algum outro problema de integridade. Ou talvez você tenha verificações de validação específica do aplicativo que podem gerar erros personalizados durante qualquer estágio de um evento de atualização. Para obter mais informações, consulte [validar dados em conjuntos de dados](../data-tools/validate-data-in-datasets.md).  
  
## <a name="maintaining-information-about-changes"></a>Manutenção de informações sobre as alterações  
 Informações sobre as alterações em um conjunto de dados são mantidas de duas maneiras: por sinalizar linhas que indicam que eles foram alterados (<xref:System.Data.DataRow.RowState%2A>) e, mantendo diversas cópias de um registro (<xref:System.Data.DataRowVersion>). Usando essas informações, os processos podem determinar o que mudou no conjunto de dados e podem enviar atualizações adequadas para a fonte de dados.  
  
### <a name="rowstate-property"></a>Propriedade RowState  
 O <xref:System.Data.DataRow.RowState%2A> propriedade de um <xref:System.Data.DataRow> objeto é um valor que fornece informações sobre o status de uma linha específica de dados.  
  
 A tabela a seguir fornece detalhes sobre os valores possíveis do <xref:System.Data.DataRowState> enumeração:  
  
|Valor de DataRowState|Descrição|  
|------------------------|-----------------|  
|<xref:System.Data.DataRowState>|A linha foi adicionada como um item para um <xref:System.Data.DataRowCollection>. (Uma linha nesse estado não tem uma versão original correspondente, pois ela não existia quando a última <xref:System.Data.DataRow.AcceptChanges%2A> método foi chamado).|  
|<xref:System.Data.DataRowState>|A linha foi excluída usando o <xref:System.Data.DataRow.Delete%2A> de um <xref:System.Data.DataRow> objeto.|  
|<xref:System.Data.DataRowState>|A linha foi criada, mas não faz parte de nenhum <xref:System.Data.DataRowCollection>. Um <xref:System.Data.DataRow> objeto estiver nesse estado imediatamente após ele ter sido criado, antes ele foi adicionado a uma coleção e depois que ele foi removido de uma coleção.|  
|<xref:System.Data.DataRowState>|Um valor de coluna na linha foi alterado de alguma forma.|  
|<xref:System.Data.DataRowState>|A linha não foi alterada desde a última chamada a <xref:System.Data.DataRow.AcceptChanges%2A>.|  
  
### <a name="datarowversion-enumeration"></a>Enumeração DataRowVersion  
 Conjuntos de dados mantêm várias versões de registros. O <xref:System.Data.DataRowVersion> enumeração de um <xref:System.Data.DataRow> objeto é um valor que pode ser usado para retornar uma versão específica de um <xref:System.Data.DataRow> objeto.  
  
 A tabela a seguir fornece detalhes sobre os valores possíveis do <xref:System.Data.DataRowVersion> enumeração:  
  
|Valor de DataRowVersion|Descrição|  
|--------------------------|-----------------|  
|<xref:System.Data.DataRowVersion>|A versão atual de um registro contém todas as modificações que foram executadas no registro desde a última vez <xref:System.Data.DataRow.AcceptChanges%2A> foi chamado. Se a linha tiver sido excluída, não há nenhuma versão atual.|  
|<xref:System.Data.DataRowVersion>|O valor padrão de um registro, conforme definido pela fonte de dados ou esquema de conjunto de dados.|  
|<xref:System.Data.DataRowVersion>|A versão original de um registro é uma cópia do registro como ele era que as últimas alterações foram confirmadas no conjunto de dados. Em termos práticos, isso é normalmente a versão de um registro como lida de uma fonte de dados.|  
|<xref:System.Data.DataRowVersion>|A versão proposta de um registro que está disponível temporariamente enquanto você está no meio de uma atualização — ou seja, entre a hora em que você chamou o <xref:System.Data.DataRow.BeginEdit%2A> método e o <xref:System.Data.DataRow.EndEdit%2A> método. Você normalmente acessa a versão proposta de um registro em um manipulador para um evento, como <xref:System.Data.DataTable.RowChanging>. Invocar o <xref:System.Data.DataRow.CancelEdit%2A> método reverte as alterações e exclui a versão de linha de dados.|  
  
 As versões originais e atuais são úteis quando informações de atualização são transmitidas para uma fonte de dados. Normalmente, quando uma atualização é enviada à fonte de dados, as novas informações para o banco de dados estão na versão atual de um registro. Informações da versão original são usadas para localizar o registro para atualizar.  
  
 Por exemplo, caso em que a chave primária de um registro é alterada, você precisa de uma maneira de localizar o registro correto na fonte de dados para atualizar as alterações. Se nenhuma versão original existia, o registro provavelmente seria acrescentado à fonte de dados, resultando não apenas em um registro extra indesejado, mas em um registro que está desatualizado e imprecisas. As duas versões também são usadas no controle de simultaneidade. Você pode comparar a versão original em relação a um registro na fonte de dados para determinar se o registro foi alterado desde que foi carregado no conjunto de dados.  
  
 A versão proposta é útil quando você precisa executar a validação antes de confirmar as alterações, na verdade, o conjunto de dados.  
  
 Mesmo se os registros tiverem sido alterados, não há sempre versões originais ou atuais dessa linha. Quando você insere uma nova linha na tabela, não há nenhuma versão original, somente a versão atual. Da mesma forma, se você excluir uma linha por meio da chamada da tabela `Delete` método, há uma versão original, mas nenhuma versão atual.  
  
 Você pode testar para ver se uma versão específica de um registro existe consultando a uma linha de dados <xref:System.Data.DataRow.HasVersion%2A> método. Você pode acessar qualquer versão de um registro, passando um <xref:System.Data.DataRowVersion> valor de enumeração como um argumento opcional quando você solicitar o valor de uma coluna.  
  
## <a name="getting-changed-records"></a>Obter registros alterados  
 É uma prática comum não deve atualizar todos os registros em um conjunto de dados. Por exemplo, um usuário pode estar trabalhando com um Windows Forms <xref:System.Windows.Forms.DataGridView> controle que exibe o número de registros. No entanto, o usuário pode atualizar apenas alguns registros, exclua uma e inserir um novo. Conjuntos de dados e tabelas de dados fornecem um método (`GetChanges`) para retornar somente as linhas que foram modificadas.  
  
 Você pode criar subconjuntos de registros alterados usando o `GetChanges` método de uma tabela de dados (<xref:System.Data.DataTable.GetChanges%2A>) ou do conjunto de dados (<xref:System.Data.DataSet.GetChanges%2A>) em si. Se você chamar o método para a tabela de dados, ele retorna uma cópia da tabela com apenas os registros alterados. Da mesma forma, se você chamar o método no conjunto de dados, obtenha um novo conjunto de dados com apenas registros alterados nele.  
  
 `GetChanges` por si só retorna todos os registros alterados. Em contraste, passando o desejado <xref:System.Data.DataRowState> como um parâmetro para o `GetChanges` método, você pode especificar o subconjunto de registros alterados que você deseja: recentemente registros, registros marcados para exclusão, registros separados, ou registros modificados.  
  
 Obter um subconjunto de registros alterados é útil quando você deseja enviar os registros para outro componente para processamento. Em vez de enviar todo o conjunto de dados, você pode reduzir a sobrecarga de se comunicar com o outro componente obtendo somente os registros que o componente precisa. Para obter mais informações, consulte [como: recuperar linhas alteradas](http://msdn.microsoft.com/library/6ff0cbd0-5253-48e7-888a-144d56c2e0a9).  
  
## <a name="committing-changes-in-the-dataset"></a>Confirmando alterações no conjunto de dados  
 Como as alterações são feitas no conjunto de dados, o <xref:System.Data.DataRow.RowState%2A> propriedade de linhas alteradas é definida. As versões originais e atuais de registros são estabelecidas, mantidas e disponibilizadas para você pelo <xref:System.Data.DataRowView.RowVersion%2A> propriedade. Os metadados que são armazenados nas propriedades de uma dessas linhas alteradas são necessário para enviar as atualizações corretas para a fonte de dados.  
  
 Se as alterações de refletem o estado atual da fonte de dados, você não precisa manter essas informações. Normalmente, há duas vezes quando o conjunto de dados e sua origem estão em sincronia:  
  
- Imediatamente depois que você carregou informações no conjunto de dados, como quando você lê dados da origem.  
  
- Depois de enviar as alterações do conjunto de dados para a fonte de dados (mas não antes, porque você pode perder as informações de alteração que é necessário para enviar alterações para o banco de dados).  
  
  Você pode confirmar as alterações pendentes para o conjunto de dados chamando o <xref:System.Data.DataSet.AcceptChanges%2A> método. Normalmente, <xref:System.Data.DataSet.AcceptChanges%2A> é chamado durante os seguintes tempos em seu aplicativo.  
  
- Depois que você carregar o conjunto de dados. Se você carregar um conjunto de dados chamando um TableAdapter `Fill` método e, em seguida, o adaptador confirma automaticamente as alterações para você. No entanto, se você carregar um conjunto de dados, mesclando outro conjunto de dados para ele, em seguida, você precisa confirmar as alterações manualmente.  
  
  > [!NOTE]
  >  Você pode impedir que o adaptador confirme automaticamente as alterações quando você chama o `Fill` método definindo o `AcceptChangesDuringFill` propriedades do adaptador para `false`. Se ele for definido como `false`, em seguida, a <xref:System.Data.DataRow.RowState%2A> de cada linha que é inserida durante o preenchimento é definido como <xref:System.Data.DataRowState>.  
  
- Depois que você envie alterações de conjunto de dados para outro processo, como um serviço Web XML.  
  
  > [!CAUTION]
  >  Confirmação da alteração dessa maneira apaga qualquer informação de alteração. Não as alterações sejam confirmadas até depois que você concluir a execução de operações que exigem que o aplicativo saber quais alterações foram feitas no conjunto de dados.  
  
  Esse método realiza o seguinte:  
  
- Grava o <xref:System.Data.DataRowVersion> versão de um registro em seu <xref:System.Data.DataRowVersion> versão e substituirá a versão original.  
  
- Remove qualquer linha em que o <xref:System.Data.DataRow.RowState%2A> estiver definida como <xref:System.Data.DataRowState>.  
  
- Define o <xref:System.Data.DataRow.RowState%2A> propriedade de um registro para <xref:System.Data.DataRowState>.  
  
  O <xref:System.Data.DataSet.AcceptChanges%2A> método está disponível em três níveis. Você pode chamá-lo em um <xref:System.Data.DataRow> alterações do objeto para confirmações apenas naquela linha. Você também pode chamá-lo em um <xref:System.Data.DataTable> objeto para confirmar todas as linhas em uma tabela. Por fim, você pode chamá-lo sobre a <xref:System.Data.DataSet> objeto para confirmar todas as alterações pendentes em todos os registros de todas as tabelas do conjunto de dados.  
  
  A tabela a seguir descreve quais alterações são confirmadas com base em qual objeto que o método é chamado em.  
  
|Método|Resultado|  
|------------|------------|  
|<xref:System.Data.DataRow.AcceptChanges%2A?displayProperty=fullName>|As alterações são confirmadas somente sobre a linha específica.|  
|<xref:System.Data.DataTable.AcceptChanges%2A?displayProperty=fullName>|As alterações são confirmadas em todas as linhas na tabela específica.|  
|<xref:System.Data.DataSet.AcceptChanges%2A?displayProperty=fullName>|As alterações são confirmadas em todas as linhas em todas as tabelas do conjunto de dados.|  
  
> [!NOTE]
>  Se você carregar um conjunto de dados chamando um TableAdapter `Fill` método, você não precisa aceitar explicitamente as alterações. Por padrão, o `Fill` chamadas de método a `AcceptChanges` método depois de terminar de preencher a tabela de dados.  
  
 Um método relacionado, `RejectChanges`, desfaz o efeito das alterações copiando a <xref:System.Data.DataRowVersion> versão volta para o <xref:System.Data.DataRowVersion> versão dos registros. Ele também define o <xref:System.Data.DataRow.RowState%2A> de cada registro de volta para <xref:System.Data.DataRowState>.  
  
## <a name="data-validation"></a>Validação de dados  
 Para verificar se os dados em seu aplicativo atendem os requisitos dos processos que ele é passado para, muitas vezes você precisa adicionar validação. Isso pode envolver a verificação de que uma entrada do usuário em um formulário está correta, validação de dados que são enviados para seu aplicativo por outro aplicativo, ou até mesmo verificando que informações calculadas no seu componente esteja dentro das restrições de sua fonte de dados e os requisitos do aplicativo.  
  
 Você pode validar os dados de várias maneiras:  
  
- Na camada de negócios, adicionando código ao seu aplicativo para validar dados. O conjunto de dados é um único lugar, você pode fazer isso. O conjunto de dados fornece algumas das vantagens de validação de back-end — como a capacidade para validar alterações como valores de coluna e linha estão mudando. Para obter mais informações, consulte [validar dados em conjuntos de dados](../data-tools/validate-data-in-datasets.md).  
  
- Na camada de apresentação, adicionando validação a formulários. Para obter mais informações, consulte [validação de entrada do usuário nos Windows Forms](http://msdn.microsoft.com/library/4ec07681-1dee-4bf9-be5e-718f635a33a1).  
  
- Nos dados de back-end, enviando dados para a fonte de dados — por exemplo, o banco de dados — e permitindo que ele aceite ou rejeite os dados. Se você estiver trabalhando com um banco de dados que tem recursos sofisticados para validação de dados e fornecendo informações de erro, isso pode ser uma abordagem prática porque você pode validar os dados, independentemente de onde eles vêm. No entanto, essa abordagem não pode acomodar requisitos de validação específicos do aplicativo. Além disso, ter a fonte de dados a validar os dados pode resultar em várias viagens de ida e a fonte de dados, dependendo de como seu aplicativo facilita a resolução de erros de validação gerados pelo back-end.  
  
  > [!IMPORTANT]
  >  Ao usar comandos de dados com um <xref:System.Data.SqlClient.SqlCommand.CommandType%2A> propriedade é definida como <xref:System.Data.CommandType>, cuidadosamente verifique informações que são enviadas de um cliente antes de passá-la para seu banco de dados. Usuários mal-intencionados podem tentar enviar (injetar) instruções de SQL modificadas ou adicionais em um esforço para obter acesso não autorizado ou danificar o banco de dados. Antes de você transferir a entrada do usuário para um banco de dados, sempre verifique se que as informações são válidas. É uma prática recomendada sempre usar consultas parametrizadas ou procedimentos armazenados quando possível. Para obter mais informações, consulte [Visão geral de explorações de script](http://msdn.microsoft.com/library/772c7312-211a-4eb3-8d6e-eec0aa1dcc07).  
  
  Depois que alterações foram feitas em um conjunto de dados, você pode transmitir as alterações em uma fonte de dados. Mais comumente, fazer isso chamando o `Update` método de um TableAdapter (ou adaptador de dados). O método loops a cada registro em uma tabela de dados, determina que tipo de atualização é necessário (atualizar, inserir ou excluir), se houver, e, em seguida, executa o comando apropriado.  
  
## <a name="transmitting-updates-to-the-data-source"></a>Transmitir atualizações à fonte de dados  
 Como uma ilustração de como as atualizações são feitas, suponha que seu aplicativo usa um conjunto de dados que contém uma única tabela de dados. O aplicativo busca duas linhas do banco de dados. Após a recuperação, a tabela de dados na memória tem esta aparência:  
  
```  
(RowState)     CustomerID   Name             Status  
(Unchanged)    c200         Robert Lyon      Good  
(Unchanged)    c400         Nancy Buchanan    Pending  
```  
  
 Seu aplicativo altera o status de Nancy Buchanan como "Preferencial". Como resultado dessa alteração, o valor da <xref:System.Data.DataRow.RowState%2A> propriedade para aquela linha muda de <xref:System.Data.DataRowState> para <xref:System.Data.DataRowState>. O valor de <xref:System.Data.DataRow.RowState%2A> propriedade para a primeira linha permanece <xref:System.Data.DataRowState>. A tabela de dados agora fica assim:  
  
```  
(RowState)     CustomerID   Name             Status  
(Unchanged)    c200         Robert Lyon      Good  
(Modified)     c400         Nancy Buchanan    Preferred  
```  
  
 Seu aplicativo agora chama o `Update` método para transmitir o conjunto de dados no banco de dados. O método verifica se cada linha por vez. A primeira linha, o método não transmite nenhuma instrução SQL no banco de dados, porque essa linha não foi alterada desde que foi originalmente buscada do banco de dados.  
  
 Para a segunda linha, no entanto, o `Update` método automaticamente chama o comando de dados correto e transmite para o banco de dados. A sintaxe específica da instrução SQL depende do dialeto do SQL que é compatível com o armazenamento de dados subjacente. Mas as seguintes características gerais da instrução SQL transmitida digno de nota:  
  
-   A instrução SQL transmitida é uma instrução UPDATE. O adaptador sabe para usar uma instrução UPDATE porque o valor da <xref:System.Data.DataRow.RowState%2A> é de propriedade <xref:System.Data.DataRowState>.  
  
-   A instrução SQL transmitida inclui uma cláusula WHERE que indica que o destino da instrução UPDATE é a linha onde `CustomerID = 'c400'`. Esta parte da instrução SELECT distingue a linha de destino de todas as outras porque o `CustomerID` é a chave primária da tabela de destino. As informações para a cláusula WHERE é derivada da versão original do registro (`DataRowVersion.Original`), no caso dos valores que são necessárias para identificar a linha foram alterados.  
  
-   A instrução SQL transmitida inclui a cláusula SET, para definir os novos valores das colunas modificadas.  
  
    > [!NOTE]
    >  Se o TableAdapter `UpdateCommand` propriedade foi definida para o nome de um procedimento armazenado, o adaptador não constrói uma instrução SQL. Em vez disso, ele chama o procedimento armazenado com os parâmetros apropriados passados.  
  
## <a name="passing-parameters"></a>Passando parâmetros  
 Você geralmente pode usar parâmetros para passar os valores para os registros que serão atualizadas no banco de dados.  Quando o TableAdapter `Update` método executa uma instrução UPDATE, ele precisa preencher os valores de parâmetro. Ele obtém esses valores da `Parameters` coleta para o comando de dados apropriada — nesse caso, o `UpdateCommand` objeto no TableAdapter.  
  
 Se você usou as ferramentas do Visual Studio para gerar um adaptador de dados, o `UpdateCommand` objeto contém uma coleção de parâmetros que correspondem a cada espaço reservado de parâmetro na instrução.  
  
 O <xref:System.Data.SqlClient.SqlParameter.SourceColumn%2A?displayProperty=fullName> propriedade de cada parâmetro aponta para uma coluna na tabela de dados. Por exemplo, o `SourceColumn` propriedade para o `au_id` e `Original_au_id` parâmetros é definido como qualquer coluna na tabela de dados que contém a id do autor. Quando o adaptador `Update` execuções de método, ele lê o autor coluna id do registro que está sendo atualizado e preenche os valores na instrução.  
  
 Em uma instrução UPDATE, você precisa especificar novos valores (aqueles que será gravado no registro), bem como os antigos valores (de modo que o registro pode ser localizado no banco de dados). Portanto, há dois parâmetros para cada valor: um para a cláusula SET e outra para a cláusula WHERE. Ambos os parâmetros leiam dados do registro que está sendo atualizado, mas eles obtêm versões diferentes do valor da coluna de acordo com o parâmetro [SourceVersion Property](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.sourceversion.aspx). O parâmetro para a cláusula SET obtém a versão atual e o parâmetro para a cláusula WHERE obtém a versão original.  
  
> [!NOTE]
>  Você também pode definir valores `Parameters` coleção por conta própria no código, que você normalmente faria em um manipulador de eventos para o adaptador de dados <xref:System.Data.DataTable.RowChanging> eventos.  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral de TableAdapter](../data-tools/tableadapter-overview.md)   
 [Atualizar dados usando um TableAdapter](../data-tools/update-data-by-using-a-tableadapter.md)   
 [Visão geral de aplicativos de dados no Visual Studio](../data-tools/overview-of-data-applications-in-visual-studio.md)   
 [Conectando-se a dados no Visual Studio](../data-tools/connecting-to-data-in-visual-studio.md)   
 [Preparando o aplicativo para receber dados](http://msdn.microsoft.com/library/c17bdb7e-c234-4f2f-9582-5e55c27356ad)   
 [Buscando dados no aplicativo](../data-tools/fetching-data-into-your-application.md)   
 [Associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md)   
 [Editando dados no aplicativo](../data-tools/editing-data-in-your-application.md)   
 [Validando dados](http://msdn.microsoft.com/library/b3a9ee4e-5d4d-4411-9c56-c811f2b4ee7e)   
 [Salvando dados](../data-tools/saving-data.md)

