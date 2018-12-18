---
title: Visão geral de TableAdapter | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vbData.Microsoft.VSDesigner.DataSource.DataAccessor
- vbdata.Microsoft.VSDesigner.DataSource.DataAccessor
- TableAdapter
- vs.data.TableAdapter
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- data [Visual Studio], table adapters
- TableAdapters, queries
- data [Visual Studio], TableAdapters
- query data in Visual Studio
- TableAdapter.GetData
- TableAdapter.Fill
- data [Visual Studio], datasets
- TableAdapters
- table adapters
ms.assetid: a87c46a0-52ab-432a-a864-9ba55069f9eb
caps.latest.revision: 40
author: gewarren
ms.author: gewarren
manager: ghogen
robots: noindex,nofollow
ms.openlocfilehash: fb5ebcdaa1bebe67c2fb8e378c7345467dd10b78
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49269042"
---
# <a name="tableadapter-overview"></a>Visão geral de TableAdapter
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

TableAdapters são componentes gerados pelo designer que se conectar a um banco de dados, executam consultas ou procedimentos armazenados e preencher sua DataTable com os dados retornados. TableAdapters também são usadas para enviar dados atualizados do seu aplicativo no banco de dados. Você pode ter tantas consultas quanto você deseja em um TableAdapter desde que elas retornam dados de acordo com o esquema da tabela à qual o TableAdapter está associado. O diagrama a seguir mostra como os TableAdapters interagem com bancos de dados e outros objetos na memória:  
  
 ![Fluxo de dados em um aplicativo cliente](../data-tools/media/clientdatadiagram.gif "ClientDataDiagram")  
  
 Enquanto TableAdapters são criados com o **Dataset Designer**, as classes TableAdapter geradas não são geradas como classes aninhadas do <xref:System.Data.DataSet>. Eles estão localizados em um namespace separado para cada conjunto de dados específico. Por exemplo, se você tiver um conjunto de dados denominado `NorthwindDataSet`, os TableAdapters associados com o <xref:System.Data.DataTable>s na `NorthwindDataSet` estaria no `NorthwindDataSetTableAdapters` namespace. Para acessar um determinado TableAdapter programaticamente, você deve declarar uma nova instância do TableAdapter. Por exemplo:  
  
 [!code-csharp[VbRaddataTableAdapters#7](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataTableAdapters/CS/Class1.cs#7)]
 [!code-vb[VbRaddataTableAdapters#7](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataTableAdapters/VB/Class1.vb#7)]  
  
## <a name="associated-datatable-schema"></a>Esquema de DataTable associados  
 Quando a criação de um TableAdapter, a consulta inicial ou o procedimento armazenado é usado para definir o esquema do TableAdapter associado do <xref:System.Data.DataTable>. Você executa essa consulta inicial ou o procedimento armazenado, chamando o TableAdapter `Fill` método (que preenche o TableAdapter associado do <xref:System.Data.DataTable>). Todas as alterações feitas à consulta principal do TableAdapter são refletidas no esquema da tabela de dados associado. Por exemplo, a remoção de uma coluna da consulta principal remove a coluna da tabela de dados associada. Se quaisquer consultas adicionais no TableAdapter usam instruções SQL retornando colunas que não estão na consulta principal, o designer tentará sincronizar as alterações de coluna entre a consulta principal e quaisquer consultas adicionais. Para obter mais informações, consulte [como: editar TableAdapters](http://msdn.microsoft.com/library/ca178745-e35a-45f1-a395-23cddfd8f855).  
  
## <a name="tableadapter-update-commands"></a>Comandos de atualização do TableAdapter  
 A funcionalidade de atualização de um TableAdapter é dependente de quantidade de informações está disponível com base na consulta principal fornecida no Assistente do TableAdapter. Por exemplo, TableAdapters configurados para buscar valores de várias tabelas (JOINs), valores escalares, exibições ou os resultados de funções de agregação não são inicialmente criados com a capacidade de enviar atualizações de volta para o banco de dados subjacente. No entanto, você pode configurar os comandos INSERT, UPDATE e DELETE manualmente na **propriedades** janela.  
  
## <a name="tableadapter-queries"></a>Consultas TableAdapter  
 ![TableAdapter com várias consultas](../data-tools/media/tableadapter.gif "TableAdapter")  
  
 TableAdapters pode conter várias consultas para preencher suas tabelas de dados associado. Você pode definir tantas consultas para um TableAdapter requer que seu aplicativo, desde que cada consulta retorna dados de acordo com o mesmo esquema que sua tabela de dados associada. Isso permite que o carregamento de dados que satisfaçam critérios diferentes. Por exemplo, se seu aplicativo contiver uma tabela de clientes, você pode criar uma consulta que preenche a tabela com todos os clientes cujo nome começa com uma determinada letra e outra consulta que preenche a tabela com todos os clientes localizados no mesmo estado. Para preencher uma `Customers` tabela com os clientes em um determinado estado, você pode criar um `FillByState` consulta que leva um parâmetro para o valor de estado: `SELECT * FROM Customers WHERE State = @State`. Execute a consulta chamando o `FillByState` método e passar o valor do parâmetro como este: `CustomerTableAdapter.FillByState("WA")`. Para obter mais informações, consulte [como: criar consultas do TableAdapter](../data-tools/how-to-create-tableadapter-queries.md).  
  
 Além das consultas que retornam dados do mesmo esquema como tabela de dados do TableAdapter, você pode adicionar consultas que retornam valores escalares de (único). Por exemplo, criar uma consulta que retorna uma contagem de clientes (`SELECT Count(*) From Customers`) é válido para um `CustomersTableAdapter` mesmo que os dados retornados não estiver de acordo com o esquema da tabela.  
  
## <a name="clearbeforefill-property"></a>Propriedade ClearBeforeFill  
 Por padrão, toda vez que executar uma consulta para preencher a tabela de dados de um TableAdapter, os dados são limpos e somente os resultados da consulta são carregados na tabela. Defina o TableAdapter `ClearBeforeFill` propriedade para `false` se você deseja adicionar ou mesclar os dados retornados de uma consulta aos dados existentes em uma tabela de dados. Independentemente se você limpar os dados, você precisa explicitamente enviar atualizações de volta para o banco de dados, se desejado. Portanto, lembre-se de salvar as alterações feitas aos dados na tabela antes de executar outra consulta que preenche a tabela. Para obter mais informações, consulte [atualizar dados usando um TableAdapter](../data-tools/update-data-by-using-a-tableadapter.md).  
  
## <a name="tableadapter-inheritance"></a>Herança do TableAdapter  
 TableAdapters estendem a funcionalidade dos adaptadores de dados padrão, encapsulando um configurado <xref:System.Data.Common.DataAdapter>. Por padrão, o TableAdapter herda <xref:System.ComponentModel.Component> e não pode ser convertido para o <xref:System.Data.Common.DataAdapter> classe. Converter um TableAdapter para um <xref:System.Data.Common.DataAdapter> resulta em um <xref:System.InvalidCastException>. Para alterar a classe base de um TableAdapter, você pode digitar uma classe que deriva de <xref:System.ComponentModel.Component> no **classe Base** propriedade do TableAdapter no **Dataset Designer**.  
  
## <a name="tableadapter-methods-and-properties"></a>As propriedades e métodos do TableAdapter  
 A classe TableAdapter não é parte do [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)], como tal, você não pode pesquisar por ele na documentação ou o **Pesquisador de objetos**. Ele é criado em tempo de design quando você usa um dos assistentes mencionados acima. O nome atribuído a um TableAdapter quando ela é criada se baseia no nome da tabela que você está trabalhando com. Por exemplo, quando criar um TableAdapter com base em uma tabela no banco de dados denominado `Orders`, o TableAdapter seria nomeado `OrdersTableAdapter`. O nome da classe do TableAdapter pode ser alterado usando o **nome** propriedade no **Dataset Designer**.  
  
 A seguir está as propriedades dos TableAdapters e métodos mais usados:  
  
|Membro|Descrição|  
|------------|-----------------|  
|`TableAdapter.Fill`|Preenche a tabela de dados associados do TableAdapter com os resultados do comando SELECT do TableAdapter. Para obter mais informações, consulte [como: preencher um conjunto de dados com dados](../data-tools/how-to-fill-a-dataset-with-data.md).|  
|`TableAdapter.Update`|Envia as alterações no banco de dados e retorna um inteiro que representa o número de linhas afetadas pela atualização. Para obter mais informações, consulte [atualizar dados usando um TableAdapter](../data-tools/update-data-by-using-a-tableadapter.md).|  
|`TableAdapter.GetData`|Retorna um novo <xref:System.Data.DataTable> preenchido com dados.|  
|`TableAdapter.Insert`|Cria uma nova linha na tabela de dados. Para obter mais informações, consulte [como: adicionar linhas a uma DataTable](http://msdn.microsoft.com/library/78ebbb43-c402-49cf-81da-0715289487bf).|  
|`TableAdapter.ClearBeforeFill`|Determina se uma tabela de dados é esvaziada antes de chamar um do `Fill` métodos.|  
  
## <a name="tableadapter-update-method"></a>Método Update do TableAdapter  
 TableAdapters usam comandos de dados para leitura e gravação do banco de dados. Inicial do TableAdapter `Fill` consulta (principal) é usada como base para criar o esquema da tabela de dados associado, bem como o `InsertCommand`, `UpdateCommand`, e `DeleteCommand` comandos associados a `TableAdapter.Update` método. Isso significa que chamar um TableAdapter `Update` método executa as instruções criadas quando o TableAdapter foi originalmente configurado, e não uma das consultas adicionais adicionada com o **deAssistentedeconfiguraçãodeconsultadoTableAdapter**.  
  
 Quando você usa um TableAdapter, ele efetivamente executa as mesmas operações com os comandos que você geralmente deseja executar. Por exemplo, quando você chama o adaptador `Fill` método, o adaptador executa o comando de dados no seu `SelectCommand` propriedade e usa um leitor de dados (por exemplo, <xref:System.Data.SqlClient.SqlDataReader>) para carregar o resultado na tabela de dados. Da mesma forma, quando você chama o adaptador `Update` método, ele executa o comando apropriado (em de `UpdateCommand`, `InsertCommand`, e `DeleteCommand` propriedades) para cada registro na tabela de dados alterado.  
  
> [!NOTE]
>  Se não houver informações suficientes na consulta principal, o `InsertCommand`, `UpdateCommand`, e `DeleteCommand` comandos são criados por padrão quando o TableAdapter é gerado. Se o principal do TableAdapter consulta é mais de uma instrução SELECT única tabela, é possível que o designer não será capaz de gerar a `InsertCommand`, `UpdateCommand`, e `DeleteCommand`. Se esses comandos não são gerados, você poderá receber um erro ao executar o `TableAdapter.Update` método.  
  
## <a name="tableadapter-generatedbdirectmethods"></a>TableAdapter GenerateDbDirectMethods  
 Além de `InsertCommand`, `UpdateCommand`, e `DeleteCommand`, TableAdapters são criados com métodos que podem ser executados diretamente no banco de dados. Esses métodos (`TableAdapter.Insert`, `TableAdapter.Update`, e `TableAdapter.Delete`) podem ser chamados diretamente para manipular dados no banco de dados. Isso significa que você pode chamar esses métodos individuais do seu código em vez de chamar o TableAdapter para lidar com as inserções, atualizações e exclusões pendentes para a tabela de dados associada.  
  
 Se você não deseja criar esses métodos diretos, defina o TableAdapter **GenerateDbDirectMethods** propriedade `false` (no **propriedades** janela). Consultas adicionais adicionadas ao TableAdapter são consultas autônomas — elas não geram esses métodos.  
  
## <a name="tableadapter-support-for-nullable-types"></a>Suporte do TableAdapter para tipos anuláveis  
 Os TableAdapters oferecem suporte a tipos anuláveis `Nullable(Of T)` e `T?`. Para obter mais informações sobre tipos anuláveis no Visual Basic, consulte [tipos de valor anuláveis](http://msdn.microsoft.com/library/9ac3b602-6f96-4e6d-96f7-cd4e81c468a6). Para obter mais informações sobre tipos anuláveis no c#, consulte [usando tipos anuláveis](http://msdn.microsoft.com/library/0bacbe72-ce15-4b14-83e1-9c14e6380c28).  
  
## <a name="see-also"></a>Consulte também  
 [Instruções passo a passo de dados](http://msdn.microsoft.com/library/15a88fb8-3bee-4962-914d-7a1f8bd40ec4)   
 [Como conectar-se a dados em um banco de dados](../data-tools/how-to-connect-to-data-in-a-database.md)   
 [Passo a passo: Conectando a dados em um banco de dados (Windows Forms)](http://msdn.microsoft.com/library/02d39aa6-8993-4602-be13-a13536af3d1c)   
 [Preparando o aplicativo para receber dados](http://msdn.microsoft.com/library/c17bdb7e-c234-4f2f-9582-5e55c27356ad)   
 [Buscando dados no aplicativo](../data-tools/fetching-data-into-your-application.md)   
 [Associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md)   
 [Editando dados no aplicativo](../data-tools/editing-data-in-your-application.md)   
 [Validando dados](http://msdn.microsoft.com/library/b3a9ee4e-5d4d-4411-9c56-c811f2b4ee7e)   
 [Salvando dados](../data-tools/saving-data.md)