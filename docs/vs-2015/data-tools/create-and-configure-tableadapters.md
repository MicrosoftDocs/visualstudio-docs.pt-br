---
title: Criar e configurar TableAdapters | Microsoft Docs
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
- table adapters, creating
- creating TableAdapters
- data [Visual Studio], creating data components
- data [Visual Studio], TableAdapters
- data [Visual Studio], creating table adapters
ms.assetid: 08630d69-0d6c-4e8f-b42d-2922f45f8415
caps.latest.revision: 33
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 03cb6c67b4887762885a0cb920eb928359b4708b
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49917642"
---
# <a name="create-and-configure-tableadapters"></a>Criar e configurar TableAdapters
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
TableAdapters fornecem comunicação entre seu aplicativo e um banco de dados. Conectar-se ao banco de dados, executar consultas ou procedimentos armazenados e retornará um novos dados de tabela ou um existente de preenchimento <xref:System.Data.DataTable> com os dados retornados. TableAdapters também pode enviar dados atualizados do seu aplicativo no banco de dados.  
  
 TableAdapters são criados para você quando você executa uma das seguintes ações:  
  
- Execute o [Data Source Configuration Wizard](http://msdn.microsoft.com/library/c4df7de5-5da0-4064-940c-761dd6d9e28f) e selecione o **banco de dados** ou **serviço Web** tipo de fonte de dados.  
  
- Arrastar objetos de banco de dados do [Gerenciador de servidores](http://msdn.microsoft.com/library/4ea29b3b-bbb2-45e4-9082-eaf635c41c4d) para o **Dataset Designer**.  
  
  Você pode criar um novo TableAdapter e configurá-lo com uma fonte de dados arrastando um TableAdapter da caixa de ferramentas para uma área vazia na **Dataset Designer** superfície.  
  
  Para obter uma introdução a TableAdapters, consulte [preencher conjuntos de dados usando TableAdapters](../data-tools/fill-datasets-by-using-tableadapters.md).  
  
  [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]  
  
## <a name="use-the-tableadapter-configuration-wizard"></a>Use o Assistente de configuração do TableAdapter  
 Execute o **Assistente de configuração TableAdapter** para criar ou editar TableAdapters e suas DataTables associadas. Você pode configurar um TableAdapter existente clicando na **Dataset Designer**.  
  
 ![Assistente de configuração do adaptador de tabela de raddata](../data-tools/media/raddata-table-adapter-configuration-wizard.png "raddata Assistente de configuração do adaptador de tabela")  
  
 Se você arrastar um novo TableAdapter da caixa de ferramentas quando o **Dataset Designer** está no foco, as solicitações do assistente que você especifique qual fonte de dados o TableAdapter deve se conectar e quais tipos de comandos que ele devem usar para se comunicar com o banco de dados, instruções SQL ou procedimentos armazenados. Você não verá essa opção se você estiver configurando um TableAdapter que já está associado uma fonte de dados.  
  
-   Usando o **criar métodos para enviar atualizações diretamente ao banco de dados** opção equivale a definir o `GenerateDBDirectMethods` propriedade como true. A opção não está disponível quando a instrução SQL original não fornecer informações suficientes ou a consulta não é uma consulta atualizável. Essa situação pode ocorrer, por exemplo, no **INGRESSAR** consultas e consultas que retornam um valor único (escalar).  
  
-   Você tem a opção de criar um novo procedimento armazenado no banco de dados subjacente, se você tiver as permissões corretas para o banco de dados. Se você não tiver essas permissões, isso não será uma opção.  
  
-   Você também pode optar por executar os procedimentos armazenados existentes para o **selecionar**, **inserir**, **atualização**, e **excluir** comandos das TableAdapter. O procedimento armazenado que é atribuído para o **atualização** comando, por exemplo, é executado quando o `TableAdapter.Update()` método é chamado.  
  
     Mapear parâmetros desde o procedimento armazenado selecionado até as colunas correspondentes na tabela de dados. Por exemplo, se seu procedimento armazenado aceita um parâmetro chamado `@CompanyName` que ele passa para o `CompanyName` conjunto de colunas na tabela, o **coluna de origem** da `@CompanyName` parâmetro `CompanyName`.  
  
    > [!NOTE]
    >  O procedimento armazenado que é atribuído para o comando SELECT é executado chamando o método do TableAdapter que você nomeia na próxima etapa do assistente. O método padrão é `Fill`, portanto, o código que normalmente é usado para executar o procedimento SELECT é `TableAdapter.Fill(tableName)`. Se você alterar o nome padrão do `Fill`, substitua `Fill` com o nome atribuir e substituir "TableAdapter" pelo nome real do TableAdapter (por exemplo, `CustomersTableAdapter`).  
  
-   O **opções avançadas** no assistente que você possa gerar instruções INSERT, UPDATE e DELETE com base na instrução SELECT que é definida na **gerar instruções SQL** página. Usar a simultaneidade otimista e especificar se para atualizar a tabela de dados após a inserção e atualização instruções são executadas.  
  
## <a name="configure-a-tableadapters-fill-method"></a>Configurar o método de preenchimento de um TableAdapter  
 Às vezes, você talvez queira alterar o esquema de tabela do TableAdapter. Para fazer isso, você modifica o primário do TableAdapter `Fill` método. TableAdapters são criados com um primário `Fill` método que define o esquema da tabela de dados associado. O principal `Fill` método se baseia na consulta ou procedimento armazenado que você inseriu quando configurou o TableAdapter originalmente. É o primeiro método (superior) sob a tabela de dados no Designer de conjunto de dados.  
  
 ![TableAdapter com várias consultas](../data-tools/media/tableadapter.gif "TableAdapter")  
  
 As alterações que fizer ao TableAdapter principal do `Fill` método são refletidas no esquema da tabela de dados associado. Por exemplo, remover uma coluna da consulta no principal `Fill` método também remove a coluna da tabela de dados associado. Além disso, remover a coluna da principal `Fill` método remove a coluna de quaisquer consultas adicionais para aquele TableAdapter.  
  
 Você pode usar o Assistente de configuração de consulta do TableAdapter para criar e editar consultas adicionais para o TableAdapter. Essas consultas adicionais devem estar em conformidade com o esquema da tabela, a menos que elas retornam um valor escalar.  As consultas adicionais que têm um nomes que você especificar (por exemplo, `CustomersTableAdapter.FillByCity(NorthwindDataSet.Customers, "Seattle")`.)  
  
#### <a name="to-start-the-tableadapter-query-configuration-wizard-with-a-new-query"></a>Para iniciar o Assistente de configuração de consulta do TableAdapter com uma nova consulta  
  
1.  Abra o dataset na **Dataset Designer**.  
  
2.  Se você estiver criando uma nova consulta, arraste um **consulta** do objeto da **DataSet** guia da **caixa de ferramentas** em um <xref:System.Data.DataTable>, ou selecione **Add Query**no menu de atalho do TableAdapter. Você também pode arrastar uma **consulta** objeto em uma área vazia do **Dataset Designer**, que cria um TableAdapter sem um associado <xref:System.Data.DataTable>. Essas consultas só podem retornar valores únicos de (escalares) ou executar a atualização, inserção, ou exclua comandos no banco de dados.  
  
3.  Sobre o **escolha sua Conexão de dados** de tela, selecione ou crie a conexão que a consulta usará.  
  
    > [!NOTE]
    >  Essa tela aparece somente quando o designer não pode determinar a conexão apropriada para usar, ou quando não há conexões disponíveis.  
  
4.  Sobre o **escolher um tipo de comando** tela, selecione os seguintes métodos de busca de dados do banco de dados:  
  
    -   **Usar instruções SQL** permite que você digite uma instrução SQL para selecionar os dados de seu banco de dados.  
  
    -   **Criar novo procedimento armazenado** permite que você tenha o Assistente para cria um novo procedimento armazenado (em banco de dados) com base na instrução SELECT especificada.  
  
    -   **Use os procedimentos armazenados existentes** permite que você execute um procedimento armazenado existente quando executar a consulta.  
  
#### <a name="to-start-the-tableadapter-query-configuration-wizard-on-an-existing-query"></a>Para iniciar o Assistente de configuração de consulta do TableAdapter em uma consulta existente  
  
-   Se você estiver editando uma consulta TableAdapter existente, a consulta com o botão direito e, em seguida, escolha **configurar** no menu de atalho.  
  
    > [!NOTE]
    >  Clicando duas vezes na consulta principal de um TableAdapter reconfigura o TableAdapter e <xref:System.Data.DataTable> esquema. No entanto, clicando duas vezes uma consulta adicional em um TableAdapter, configura a consulta selecionada. O **Assistente de configuração TableAdapter** reconfigura a definição do TableAdapter, enquanto o Assistente de configuração de consulta do TableAdapter reconfigura a consulta selecionada.  
  
#### <a name="to-add-a-global--query-to-a-tableadapter"></a>Para adicionar uma consulta global a um TableAdapter  
  
-   *Consultas globais* são consultas SQL que retornam um valor único (escalar) ou nenhum valor. Normalmente, funções globais de realizar operações de banco de dados como inserções, atualizações, exclui. Eles também pode agregar informações, como uma contagem de clientes em uma tabela ou o total das taxas para todos os itens em uma ordem específica.  
  
     Adicionar consultas globais arrastando uma **consulta** do objeto da **conjunto de dados** guia da **caixa de ferramentas** em uma área vazia do **Dataset Designer**.  
  
-   Forneça uma consulta que realiza a tarefa desejada, por exemplo, `SELECT COUNT(*) AS CustomerCount FROM Customers`.  
  
    > [!NOTE]
    >  Arrastando um **consulta** do objeto diretamente para o **Dataset Designer** cria um método que retorna um valor escalar (único). Enquanto a consulta ou procedimento armazenado que você selecionar pode retornar mais de um único valor, o método que é criado pelo assistente retorna apenas um único valor. Por exemplo, a consulta pode retornar a primeira coluna da primeira linha dos dados retornados.  
  
## <a name="see-also"></a>Consulte também  
 [Preencher conjuntos de dados usando TableAdapters](../data-tools/fill-datasets-by-using-tableadapters.md)

