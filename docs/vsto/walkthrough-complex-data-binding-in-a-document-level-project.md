---
title: 'Passo a passo: Vinculação de dados complexos em um projeto de nível de documento'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Office development in Visual Studio], binding data
- complex data [Office development in Visual Studio]
- multiple column data binding [Office development in Visual Studio]
- data binding [Office development in Visual Studio], multiple columns
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 6886908f01ceaeb36ed83ba0970ef250873d69c2
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49841878"
---
# <a name="walkthrough-complex-data-binding-in-a-document-level-project"></a>Passo a passo: Vinculação de dados complexos em um projeto de nível de documento
  Este passo a passo demonstra as Noções básicas de vinculação de dados complexos em um projeto de nível de documento. Você pode vincular várias células em uma planilha do Microsoft Office Excel para os campos no banco de dados Northwind do SQL Server.  
  
 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]  
  
 Esta explicação passo a passo ilustra as seguintes tarefas:  
  
- Adicionando uma fonte de dados ao seu projeto de pasta de trabalho.  
  
- Adicionando controles ligados a dados a uma planilha.  
  
- Salvando alterações de dados no banco de dados.  
  
  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:  
  
-   [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]  
  
-   [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] ou [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)].  
  
-   Acesso a um servidor com o banco de dados de exemplo Northwind do SQL Server.  
  
-   Permissões para ler e gravar no banco de dados do SQL Server.  
  
## <a name="create-a-new-project"></a>Criar um novo projeto  
 A primeira etapa é criar um projeto de pasta de trabalho do Excel.  
  
### <a name="to-create-a-new-project"></a>Para criar um novo projeto  
  
1.  Criar um projeto de pasta de trabalho do Excel com o nome **vinculação de dados complexos de meu**. No assistente, selecione **criar um novo documento**.  
  
     Para obter mais informações, consulte [como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).  
  
     Visual Studio abre a nova pasta de trabalho do Excel no designer e adiciona o **minha vinculação de dados complexos** projeto ao **Gerenciador de soluções**.  
  
## <a name="create-the-data-source"></a>Criar a fonte de dados  
 Use o **fontes de dados** janela para adicionar um conjunto de dados tipado ao seu projeto.  
  
### <a name="to-create-the-data-source"></a>Para criar a fonte de dados  
  
1. Se o **fontes de dados** janela não estiver visível, exibi-lo, na barra de menus, escolhendo **exibição** > **Other Windows**  >   **Fontes de dados**.  
  
2. Escolher **Add New Data Source** para iniciar o **Data Source Configuration Wizard**.  
  
3. Selecione **banco de dados** e, em seguida, clique em **próxima**.  
  
4. Selecione uma conexão de dados para o banco de dados do SQL Server de exemplo Northwind, ou adicionar uma nova conexão usando o **nova Conexão** botão.  
  
5. Depois que uma conexão foi selecionado ou criado, clique em **próxima**.  
  
6. Desmarque a opção para salvar a conexão se ela está selecionada e clique **próxima**.  
  
7. Expanda o **tabelas** nó na **objetos de banco de dados** janela.  
  
8. Marque a caixa de seleção ao lado de **funcionários** tabela.  
  
9. Clique em **Finalizar**.  
  
   O assistente adiciona as **funcionários** de tabela para o **fontes de dados** janela. Ele também adiciona um dataset tipado ao seu projeto que está visível no **Gerenciador de soluções**.  
  
## <a name="add-controls-to-the-worksheet"></a>Adicionar controles à planilha  
 Uma planilha exibirá os **funcionários** tabela quando a pasta de trabalho é aberta. Os usuários poderão fazer alterações aos dados e, em seguida, salvar essas alterações no banco de dados, clicando em um botão.  
  
 Para associar a planilha para a tabela automaticamente, você pode adicionar um <xref:Microsoft.Office.Tools.Excel.ListObject> controle na planilha do **fontes de dados** janela. Para dar ao usuário a opção de salvar as alterações, adicione uma <xref:System.Windows.Forms.Button> controlar do **caixa de ferramentas**.  
  
#### <a name="to-add-a-list-object"></a>Para adicionar um objeto de lista  
  
1.  Verifique se que o **Meus Binding.xlsx dados complexos** pasta de trabalho é aberta no designer do Visual Studio, com **Sheet1** exibido.  
  
2.  Abra o **fontes de dados** janela e selecione o **funcionários** nó.  
  
3.  Clique na seta suspensa que aparece.  
  
4.  Selecione **ListObject** na lista suspensa.  
  
5.  Arraste o **funcionários** tabela para a célula **A6**.  
  
     Um <xref:Microsoft.Office.Tools.Excel.ListObject> controle chamado `EmployeesListObject` é criado na célula **A6**. Ao mesmo tempo, uma <xref:System.Windows.Forms.BindingSource> nomeado `EmployeesBindingSource`, um adaptador de tabela e um <xref:System.Data.DataSet> instância são adicionados ao projeto. O controle é associado à <xref:System.Windows.Forms.BindingSource>, que por sua vez é associado a <xref:System.Data.DataSet> instância.  
  
### <a name="to-add-a-button"></a>Para adicionar um botão  
  
1. Do **controles comuns** guia da **caixa de ferramentas**, adicione um <xref:System.Windows.Forms.Button> controle à célula **A4** da planilha.  
  
   A próxima etapa é adicionar texto ao botão quando a planilha é aberta.  
  
## <a name="initialize-the-control"></a>Inicializar o controle  
 Adicionar texto ao botão no <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> manipulador de eventos.  
  
### <a name="to-initialize-the-control"></a>Ao inicializar o controle  
  
1. Na **Gerenciador de soluções**, clique com botão direito **Sheet1.vb** ou **Sheet1.cs**e, em seguida, clique em **Exibir código** no menu de atalho.  
  
2. Adicione o seguinte código para o `Sheet1_Startup` método para definir o texto para o b`utton`.  
  
    [!code-csharp[Trin_VstcoreDataExcel#8](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet3.cs#8)]
    [!code-vb[Trin_VstcoreDataExcel#8](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet3.vb#8)]  
  
3. Apenas para c#, adicione um manipulador de eventos para o <xref:System.Windows.Forms.Control.Click> eventos para o `Sheet1_Startup` método.  
  
    [!code-csharp[Trin_VstcoreDataExcel#9](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet3.cs#9)]  
  
   Agora adicione código para manipular o <xref:System.Windows.Forms.Control.Click> evento do botão.  
  
## <a name="save-changes-to-the-database"></a>Salvar alterações no banco de dados  
 Todas as alterações foram feitas para os dados existem somente no conjunto de dados local até que eles são salvos no banco de dados explicitamente.  
  
### <a name="to-save-changes-to-the-database"></a>Para salvar as alterações no banco de dados  
  
1.  Adicionar um manipulador de eventos para o <xref:System.Windows.Forms.Control.Click> eventos do `button`e adicione o seguinte código para confirmar todas as alterações que foram feitas no conjunto de dados no banco de dados.  
  
     [!code-csharp[Trin_VstcoreDataExcel#10](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet3.cs#10)]
     [!code-vb[Trin_VstcoreDataExcel#10](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet3.vb#10)]  
  
## <a name="test-the-application"></a>Testar o aplicativo  
 Agora você pode testar sua pasta de trabalho para verificar se os dados aparecem conforme o esperado, e que você pode manipular os dados no objeto da lista.  
  
### <a name="to-test-the-data-binding"></a>Para testar a associação de dados  
  
-   Pressione **F5**.  
  
     Verifique se que, quando a pasta de trabalho é aberto, o objeto de lista é preenchido com dados do **funcionários** tabela.  
  
### <a name="to-modify-data"></a>Para modificar dados  
  
1.  Clique na célula **B7**, que deve conter o nome **Davolio**.  
  
2.  Digite o nome **Anderson**, em seguida, pressione **Enter**.  
  
### <a name="to-modify-a-column-header"></a>Para modificar um cabeçalho de coluna  
  
1.  Clique na célula que contém o cabeçalho de coluna **LastName**.  
  
2.  Tipo de **Sobrenome**, incluindo um espaço entre as duas palavras e, em seguida, pressione **Enter**.  
  
### <a name="to-save-data"></a>Para salvar dados  
  
1.  Clique em **salvar** na planilha.  
  
2.  Saia do Excel. Clique em **não** quando for solicitado a salvar as alterações feitas por você.  
  
3.  Pressione **F5** para executar o projeto novamente.  
  
     O objeto de lista é preenchido com os dados do **funcionários** tabela.  
  
4.  Observe que o nome na célula **B7** ainda **Anderson**, quais são os dados de alterar o que você fez e salvo no banco de dados. O cabeçalho da coluna **LastName** foi alterado para seu formato original sem espaço, porque o cabeçalho de coluna não está associado ao banco de dados e você não salvou as alterações feitas à planilha.  
  
### <a name="to-add-new-rows"></a>Para adicionar novas linhas  
  
1. Selecione uma célula dentro do objeto de lista.  
  
    Uma nova linha aparece na parte inferior da lista, com um asterisco (* *\\* * *) na primeira célula da nova linha.  
  
2. Adicione as seguintes informações na linha vazia.  
  
   |EmployeeID|LastName|FirstName|Título|  
   |----------------|--------------|---------------|-----------|  
   |10|Shu|Shu|Gerente de vendas|  
  
### <a name="to-delete-rows"></a>Para excluir linhas  
  
-   O número de 16 (linha 16) no lado esquerdo da planilha com o botão direito e, em seguida, clique em **excluir**.  
  
### <a name="to-sort-the-rows-in-the-list"></a>Para classificar as linhas na lista  
  
1.  Selecione uma célula dentro da lista.  
  
     Botões de seta aparecerão em cada cabeçalho de coluna.  
  
2.  Clique no botão de seta para a **Sobrenome** cabeçalho de coluna.  
  
3.  Clique em **classificar em ordem crescente**.  
  
     As linhas são classificadas em ordem alfabética por sobrenome.  
  
### <a name="to-filter-information"></a>Para filtrar informações  
  
1.  Selecione uma célula dentro da lista.  
  
2.  Clique no botão de seta para a **título** cabeçalho de coluna.  
  
3.  Clique em **representante de vendas**.  
  
     A lista mostra somente as linhas que têm **representante de vendas** na **título** coluna.  
  
4.  Clique no botão de seta para a **título** cabeçalho da coluna novamente.  
  
5.  Clique em **(All)**.  
  
     A filtragem é removida e todas as linhas são exibidos.  
  
## <a name="next-steps"></a>Próximas etapas  
 Este passo a passo mostra as Noções básicas de vinculação de uma tabela em um banco de dados para um objeto de lista. Estas são algumas tarefas que podem vir a seguir:  
  
-   Armazenar em cache os dados para que possa ser usado offline. Para obter mais informações, consulte [como: armazenar em Cache dados para uso offline ou em um servidor](../vsto/how-to-cache-data-for-use-offline-or-on-a-server.md).  
  
-   Implante a solução. Para obter mais informações, consulte [implantar uma solução do Office](../vsto/deploying-an-office-solution.md).  
  
-   Crie uma relação mestre/detalhes entre um campo e uma tabela. Para obter mais informações, consulte [instruções passo a passo: criar uma relação de detalhes mestre usando um conjunto de dados armazenados em cache](../vsto/walkthrough-creating-a-master-detail-relation-using-a-cached-dataset.md).  
  
## <a name="see-also"></a>Consulte também  
 [Associar dados a controles em soluções do Office](../vsto/binding-data-to-controls-in-office-solutions.md)   
 [Dados em soluções do Office](../vsto/data-in-office-solutions.md)   
 [Passo a passo: Associação de dados simples em um projeto de nível de documento](../vsto/walkthrough-simple-data-binding-in-a-document-level-project.md)  
  
  