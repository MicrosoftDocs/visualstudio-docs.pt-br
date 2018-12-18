---
title: 'Passo a passo: Criar uma relação de detalhes mestre usando um conjunto de dados armazenados em cache'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- master-detail tables [Office development in Visual Studio], walkthroughs
- data caching [Office development in Visual Studio], Master/Detail Relation
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 9d877eae119c922939ea61007a845e5bd7049076
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49933151"
---
# <a name="walkthrough-create-a-master-detail-relation-using-a-cached-dataset"></a>Passo a passo: Criar uma relação de detalhes mestre usando um conjunto de dados armazenados em cache
  Este passo a passo demonstra como criar uma relação mestre/detalhes em uma planilha e os dados de cache para que a solução possa ser usada offline.  
  
 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]  
  
 Durante este passo a passo, você aprenderá a:  
  
-   Adicione controles a uma planilha.  
  
-   Configure um conjunto de dados sejam armazenados em cache em uma planilha.  
  
-   Adicione código para habilitar a rolagem por meio de registros.  
  
-   Teste seu projeto.  
  
> [!NOTE]  
>  Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, confira [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:  
  
-   [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]  
  
-   [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] ou [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)].  
  
-   Acesso ao banco de dados de exemplo Northwind do SQL Server. O banco de dados pode ser no computador de desenvolvimento ou em um servidor.  
  
-   Permissões para ler e gravar no banco de dados do SQL Server.  
  
## <a name="create-a-new-project"></a>Criar um novo projeto  
 Nesta etapa, você criará um projeto de pasta de trabalho do Excel.  
  
### <a name="to-create-a-new-project"></a>Para criar um novo projeto  
  
1. Criar um projeto de pasta de trabalho do Excel com o nome **Meus Master-Detail**, usando o Visual Basic ou c#. Certifique-se de que **criar um novo documento** está selecionado. Para obter mais informações, consulte [como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).  
  
   Visual Studio abre a nova pasta de trabalho do Excel no designer e adiciona o **Meus Master-Detail** projeto ao **Gerenciador de soluções**.  
  
## <a name="create-the-data-source"></a>Criar a fonte de dados  
 Use o **fontes de dados** janela para adicionar um conjunto de dados tipado ao seu projeto.  
  
### <a name="to-create-the-data-source"></a>Para criar a fonte de dados  
  
1. Se o **fontes de dados** janela não estiver visível, exibi-lo, na barra de menus, escolhendo **exibição** > **Other Windows**  >   **Fontes de dados**.  
  
2. Escolher **Add New Data Source** para iniciar o **Data Source Configuration Wizard**.  
  
3. Selecione **banco de dados** e, em seguida, clique em **próxima**.  
  
4. Selecione uma conexão de dados para o banco de dados do SQL Server de exemplo Northwind, ou adicionar uma nova conexão usando o **nova Conexão** botão.  
  
5. Depois de selecionar ou criar uma conexão, clique em **próxima**.  
  
6. Desmarque a opção para salvar a conexão se ela está selecionada e clique **próxima**.  
  
7. Expanda o **tabelas** nó na **objetos de banco de dados** janela.  
  
8. Selecione o **pedidos** tabela e o **detalhes do pedido** tabela.  
  
9. Clique em **Finalizar**.  
  
   O assistente adiciona as duas tabelas para o **fontes de dados** janela. Ele também adiciona um dataset tipado ao seu projeto que está visível no **Gerenciador de soluções**.  
  
## <a name="add-controls-to-the-worksheet"></a>Adicionar controles à planilha  
 Nesta etapa, você adicionará um intervalo nomeado, um objeto de lista e dois botões para a primeira planilha. Primeiro, adicione o intervalo nomeado e o objeto de lista dos **fontes de dados** janela, de modo que eles são vinculados automaticamente a fonte de dados. Em seguida, adicione os botões do **caixa de ferramentas**.  
  
### <a name="to-add-a-named-range-and-a-list-object"></a>Para adicionar um intervalo nomeado e um objeto de lista  
  
1.  Verificar se o **Meus Master-Detail.xlsx** pasta de trabalho é aberta no designer do Visual Studio, com **Sheet1** exibido.  
  
2.  Abra o **fontes de dados** janela e expanda o **pedidos** nó.  
  
3.  Selecione o **OrderID** coluna e, em seguida, clique na seta suspensa exibida.  
  
4.  Clique em **NamedRange** na lista suspensa e, em seguida, arraste o **OrderID** coluna para uma célula **A2**.  
  
     Um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle chamado `OrderIDNamedRange` é criado na célula **A2**. Ao mesmo tempo, uma <xref:System.Windows.Forms.BindingSource> nomeado `OrdersBindingSource`, um adaptador de tabela e um <xref:System.Data.DataSet> instância são adicionados ao projeto. O controle é associado à <xref:System.Windows.Forms.BindingSource>, que por sua vez é associado a <xref:System.Data.DataSet> instância.  
  
5.  Role para baixo após as colunas que estão sob o **pedidos** tabela. Na parte inferior da lista é o **detalhes do pedido** tabela; está aqui porque ele é um filho do **pedidos** tabela. Selecione esta opção **detalhes do pedido** da tabela, não aquela que está no mesmo nível que o **pedidos** de tabela e, em seguida, clique na seta suspensa exibida.  
  
6.  Clique em **ListObject** na lista suspensa e, em seguida, arraste o **OrderDetails** tabela para a célula **A6**.  
  
7.  Um <xref:Microsoft.Office.Tools.Excel.ListObject> controle chamado **Order_DetailsListObject** é criado na célula **A6**e associado para o <xref:System.Windows.Forms.BindingSource>.  
  
### <a name="to-add-two-buttons"></a>Para adicionar dois botões  
  
1. Do **controles comuns** guia da **caixa de ferramentas**, adicione um <xref:System.Windows.Forms.Button> controle à célula **A3** da planilha.  
  
    Esse botão é denominado `Button1`.  
  
2. Adicione outro <xref:System.Windows.Forms.Button> controle a célula **B3** da planilha.  
  
    Esse botão é denominado `Button2`.  
  
   Em seguida, marque o conjunto de dados sejam armazenados em cache no documento.  
  
## <a name="cache-the-dataset"></a>Armazenar em cache o conjunto de dados  
 Marcar o conjunto de dados sejam armazenados em cache no documento, tornando o conjunto de dados públicos e definindo o **CacheInDocument** propriedade.  
  
### <a name="to-cache-the-dataset"></a>Para armazenar em cache o conjunto de dados  
  
1. Selecione **NorthwindDataSet** na bandeja de componentes.  
  
2. No **propriedades** janela, altere o **modificadores** propriedade a ser **público**.  
  
    Conjuntos de dados devem ser públicos antes de o cache está habilitado.  
  
3. Alterar o **CacheInDocument** propriedade **verdadeiro**.  
  
   A próxima etapa é adicionar texto a botões e no c#, adicione código para ligar os manipuladores de eventos.  
  
## <a name="initialize-the-controls"></a>Inicializar os controles  
 Definir o texto do botão e adicionar manipuladores de eventos durante o <xref:Microsoft.Office.Tools.Excel.Workbook.Startup> eventos.  
  
### <a name="to-initialize-the-data-and-the-controls"></a>Para inicializar os dados e os controles  
  
1.  Na **Gerenciador de soluções**, clique com botão direito **Sheet1.vb** ou **Sheet1.cs**e, em seguida, clique em **Exibir código** no menu de atalho.  
  
2.  Adicione o seguinte código para o `Sheet1_Startup` método para definir o texto dos botões.  
  
     [!code-vb[Trin_VstcoreDataExcel#15](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet2.vb#15)]
     [!code-csharp[Trin_VstcoreDataExcel#15](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet2.cs#15)]  
  
3.  Apenas para c#, adicionar manipuladores de eventos para o botão, clique em eventos para o `Sheet1_Startup` método.  
  
     [!code-csharp[Trin_VstcoreDataExcel#16](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet2.cs#16)]  
  
## <a name="add-code-to-enable-scrolling-through-the-records"></a>Adicione código para habilitar a rolagem por meio de registros  
 Adicione código para o <xref:System.Windows.Forms.Control.Click> manipulador de eventos de cada botão para percorrer os registros.  
  
### <a name="to-scroll-through-the-records"></a>Para percorrer os registros  
  
1.  Adicionar um manipulador de eventos para o <xref:System.Windows.Forms.Control.Click> eventos de `Button1`e adicione o seguinte código para percorrer os registros com versões anteriores:  
  
     [!code-vb[Trin_VstcoreDataExcel#17](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet2.vb#17)]
     [!code-csharp[Trin_VstcoreDataExcel#17](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet2.cs#17)]  
  
2.  Adicionar um manipulador de eventos para o <xref:System.Windows.Forms.Control.Click> eventos de `Button2`e adicione o seguinte código para percorrer os registros:  
  
     [!code-vb[Trin_VstcoreDataExcel#18](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet2.vb#18)]
     [!code-csharp[Trin_VstcoreDataExcel#18](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet2.cs#18)]  
  
## <a name="test-the-application"></a>Testar o aplicativo  
 Agora você pode testar sua pasta de trabalho para certificar-se de que os dados aparecem conforme o esperado, e você pode usar a solução offline.  
  
### <a name="to-test-the-data-caching"></a>Para testar o cache de dados  
  
1.  Pressione **F5**.  
  
2.  Verifique se que o intervalo nomeado e o objeto de lista são preenchidos com dados da fonte de dados.  
  
3.  Rolar por alguns dos registros clicando nos botões.  
  
4.  Salve a pasta de trabalho e, em seguida, feche a pasta de trabalho e o Visual Studio.  
  
5.  Desabilite a conexão ao banco de dados. Desconecte o cabo de rede do seu computador, se o banco de dados está localizado em um servidor ou parar o serviço SQL Server se o banco de dados no computador de desenvolvimento.  
  
6.  Abra o Excel e, em seguida, abra **Meus Master-Detail.xlsx** da *\bin* diretório (*\My Master-Detail\bin* no Visual Basic ou *\My Master-Detail\bin\ Depurar* em c#).  
  
7.  Role por meio de alguns dos registros para ver a planilha opera normalmente quando desconectado.  
  
8.  Reconectar-se ao banco de dados. Conectar o computador à rede novamente se o banco de dados está localizado em um servidor ou iniciar o serviço do SQL Server, se o banco de dados no computador de desenvolvimento.  
  
## <a name="next-steps"></a>Próximas etapas  
 Este passo a passo mostra as Noções básicas de criação de uma relação de dados mestre/detalhes em uma planilha e um conjunto de dados de cache. Estas são algumas tarefas que podem vir a seguir:  
  
-   Implante a solução. Para obter mais informações, consulte [implantar uma solução do Office](../vsto/deploying-an-office-solution.md)  
  
## <a name="see-also"></a>Consulte também  
 [Associar dados a controles em soluções do Office](../vsto/binding-data-to-controls-in-office-solutions.md)   
 [Dados em soluções do Office](../vsto/data-in-office-solutions.md)   
 [Dados de cache](../vsto/caching-data.md)   
 [Visão geral dos controles de host e de itens de host](../vsto/host-items-and-host-controls-overview.md)  
  
  