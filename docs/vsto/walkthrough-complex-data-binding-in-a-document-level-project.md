---
title: 'Walkthrough: ligação de dados complexa em um projeto de nível de documento'
description: Saiba como você pode associar várias células em uma planilha do Microsoft Excel a campos no banco de dados Northwind SQL Server.
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Office development in Visual Studio], binding data
- complex data [Office development in Visual Studio]
- multiple column data binding [Office development in Visual Studio]
- data binding [Office development in Visual Studio], multiple columns
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: a85f46cf9c234ad662966372a8d014ae0f98be84
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826363"
---
# <a name="walkthrough-complex-data-binding-in-a-document-level-project"></a>Walkthrough: ligação de dados complexa em um projeto de nível de documento
  Este tutorial demonstra os conceitos básicos da ligação de dados complexa em um projeto de nível de documento. Você pode associar várias células em uma Microsoft Office planilha do Excel a campos no banco de dados Northwind SQL Server.

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 Este passo a passo ilustra as seguintes tarefas:

- Adicionar uma fonte de dados ao projeto de pasta de trabalho.

- Adicionar controles vinculados a dados a uma planilha.

- Salvar alterações de dados de volta no banco de dado.

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>Pré-requisitos
 Você precisará dos seguintes componentes para concluir este passo a passo:

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] ou [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)].

- Acesso a um servidor com o banco de dados Northwind SQL Server exemplo.

- Permissões para ler e gravar no banco de dados de SQL Server.

## <a name="create-a-new-project"></a>Criar um novo projeto
 A primeira etapa é criar um projeto de pasta de trabalho do Excel.

### <a name="to-create-a-new-project"></a>Para criar um novo projeto

1. Crie um projeto de pasta de trabalho do Excel com o nome **minha vinculação de dados complexa**. No assistente, selecione **criar um novo documento**.

     Para obter mais informações, consulte [como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).

     O Visual Studio abre a nova pasta de trabalho do Excel no designer e adiciona o projeto de **ligação de dados complexo** a **Gerenciador de soluções**.

## <a name="create-the-data-source"></a>Criar a fonte de dados
 Use a janela **Data Sources** para adicionar um conjunto de dados tipado ao seu projeto.

### <a name="to-create-the-data-source"></a>Para criar a fonte de dados

1. Se a janela **fontes de dados** não estiver visível, exiba-a por, na barra de menus, escolhendo **Exibir**  >  **outras**  >  **fontes de dados** do Windows.

2. Escolha **Adicionar nova fonte de dados** para iniciar o **Assistente de configuração de fonte de dados**.

3. Selecione **banco de dados** e clique em **Avançar**.

4. Selecione uma conexão de dados para o exemplo da Northwind SQL Server Database ou adicione uma nova conexão usando o botão **nova conexão** .

5. Depois que uma conexão for selecionada ou criada, clique em **Avançar**.

6. Desmarque a opção para salvar a conexão, se ela estiver selecionada, e clique em **Avançar**.

7. Expanda o nó **tabelas** na janela **objetos de banco de dados** .

8. Marque a caixa de seleção ao lado da tabela **funcionários** .

9. Clique em **Concluir**.

   O assistente adiciona a tabela **Employees** à janela **fontes de dados** . Ele também adiciona um conjunto de um dataset tipado ao seu projeto que está visível no **Gerenciador de soluções**.

## <a name="add-controls-to-the-worksheet"></a>Adicionar controles à planilha
 Uma planilha exibirá a tabela **Employees** quando a pasta de trabalho for aberta. Os usuários poderão fazer alterações nos dados e, em seguida, salvar essas alterações de volta no banco de dado clicando em um botão.

 Para associar a planilha à tabela automaticamente, você pode adicionar um <xref:Microsoft.Office.Tools.Excel.ListObject> controle à planilha na janela **Data Sources** . Para dar ao usuário a opção de salvar as alterações, adicione um <xref:System.Windows.Forms.Button> controle da **caixa de ferramentas**.

#### <a name="to-add-a-list-object"></a>Para adicionar um objeto de lista

1. Verifique se a pasta de trabalho **meus dados complexos Binding.xlsx** está aberta no designer do Visual Studio, com **Sheet1** exibida.

2. Abra a janela **fontes de dados** e selecione o nó **funcionários** .

3. Clique na seta suspensa exibida.

4. Selecione **ListObject** na lista suspensa.

5. Arraste a tabela **Employees** para a célula **a6**.

     Um <xref:Microsoft.Office.Tools.Excel.ListObject> controle chamado `EmployeesListObject` é criado na célula **a6**. Ao mesmo tempo, um <xref:System.Windows.Forms.BindingSource> nome `EmployeesBindingSource` , um adaptador de tabela e uma <xref:System.Data.DataSet> instância são adicionados ao projeto. O controle está associado ao <xref:System.Windows.Forms.BindingSource> , que, por sua vez, está associado à <xref:System.Data.DataSet> instância.

### <a name="to-add-a-button"></a>Para adicionar um botão

1. Na guia **controles comuns** da caixa de **ferramentas**, adicione um <xref:System.Windows.Forms.Button> controle à célula **a4** da planilha.

   A próxima etapa é adicionar texto ao botão quando a planilha for aberta.

## <a name="initialize-the-control"></a>Inicializar o controle
 Adicione texto ao botão no manipulador de <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> eventos.

### <a name="to-initialize-the-control"></a>Para inicializar o controle

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse em **Plan1. vb** ou **Plan1. cs** e clique em **Exibir código** no menu de atalho.

2. Adicione o código a seguir ao `Sheet1_Startup` método para definir o texto para o b `utton` .

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet3.cs" id="Snippet8":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet3.vb" id="Snippet8":::

3. Somente para C#, adicione um manipulador de eventos para o <xref:System.Windows.Forms.Control.Click> evento ao `Sheet1_Startup` método.

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet3.cs" id="Snippet9":::

   Agora, adicione o código para manipular o <xref:System.Windows.Forms.Control.Click> evento do botão.

## <a name="save-changes-to-the-database"></a>Salvar alterações no banco de dados
 Todas as alterações feitas nos dados existem somente no conjunto de dados local até que sejam explicitamente salvas no banco de dado.

### <a name="to-save-changes-to-the-database"></a>Para salvar as alterações no banco de dados

1. Adicione um manipulador de eventos para o <xref:System.Windows.Forms.Control.Click> evento do `button` e adicione o código a seguir para confirmar todas as alterações que foram feitas no conjunto de dados de volta para o Database.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet3.cs" id="Snippet10":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet3.vb" id="Snippet10":::

## <a name="test-the-application"></a>Testar o aplicativo
 Agora você pode testar sua pasta de trabalho para verificar se os dados aparecem como esperado e se você pode manipular os dados no objeto de lista.

### <a name="to-test-the-data-binding"></a>Para testar a associação de dados

- Pressione **F5**.

     Verifique se a pasta de trabalho é aberta, se o objeto de lista está preenchido com os dados da tabela **Employees** .

### <a name="to-modify-data"></a>Para modificar dados

1. Clique na célula **B7**, que deve conter o nome **Davolio**.

2. Digite o nome **Anderson** e pressione **Enter**.

### <a name="to-modify-a-column-header"></a>Para modificar um cabeçalho de coluna

1. Clique na célula que contém o cabeçalho de coluna **LastName**.

2. Digite **Last Name**, incluindo um espaço entre as duas palavras, e pressione **Enter**.

### <a name="to-save-data"></a>Para salvar dados

1. Clique em **salvar** na planilha.

2. Saia do Excel. Clique em **não** quando for solicitado a salvar as alterações feitas.

3. Pressione **F5** para executar o projeto novamente.

     O objeto List é preenchido com dados da tabela **Employees** .

4. Observe que o nome na célula **B7** ainda é **Anderson**, que é a alteração de dados que você criou e salvou de volta no banco de dados. O cabeçalho de coluna **LastName** mudou de volta para seu formulário original sem espaço, porque o cabeçalho da coluna não está associado ao banco de dados e você não salvou as alterações feitas na planilha.

### <a name="to-add-new-rows"></a>Para adicionar novas linhas

1. Selecione uma célula dentro do objeto de lista.

    Uma nova linha é exibida na parte inferior da lista, com um asterisco ( **\*** ) na primeira célula da nova linha.

2. Adicione as seguintes informações na linha vazia.

   |IDFuncionário|LastName|Nome|Título|
   |----------------|--------------|---------------|-----------|
   |10|Ito|Shu|Gerente de Vendas|

### <a name="to-delete-rows"></a>Para excluir linhas

- Clique com o botão direito do mouse no número 16 (linha 16) no lado esquerdo da planilha e clique em **excluir**.

### <a name="to-sort-the-rows-in-the-list"></a>Para classificar as linhas na lista

1. Selecione uma célula dentro da lista.

     Botões de seta aparecem em cada cabeçalho de coluna.

2. Clique no botão de seta no cabeçalho da coluna **Last Name** .

3. Clique em **classificar em ordem crescente**.

     As linhas são classificadas alfabeticamente pelos últimos nomes.

### <a name="to-filter-information"></a>Para filtrar informações

1. Selecione uma célula dentro da lista.

2. Clique no botão de seta no cabeçalho da coluna **título** .

3. Clique em **representante de vendas**.

     A lista mostra apenas as linhas que têm **representante de vendas** na coluna **título** .

4. Clique no botão de seta no cabeçalho da coluna **título** novamente.

5. Clique em **(tudo)**.

     A filtragem é removida e todas as linhas são exibidas.

## <a name="next-steps"></a>Próximas etapas
 Este tutorial mostra as noções básicas de associação de uma tabela em um banco de dados a um objeto de lista. Estas são algumas tarefas que podem vir a seguir:

- Armazene os dados em cache para que eles possam ser usados offline. Para obter mais informações, consulte [como armazenar em cache os dados para uso offline ou em um servidor](../vsto/how-to-cache-data-for-use-offline-or-on-a-server.md).

- Implante a solução. Para obter mais informações, consulte [implantar uma solução do Office](../vsto/deploying-an-office-solution.md).

- Crie uma relação mestre/detalhes entre um campo e uma tabela. Para obter mais informações, consulte [Walkthrough: criar uma relação de detalhes mestre usando um conjunto de dados em cache](../vsto/walkthrough-creating-a-master-detail-relation-using-a-cached-dataset.md).

## <a name="see-also"></a>Consulte também
- [Associar dados a controles em soluções do Office](../vsto/binding-data-to-controls-in-office-solutions.md)
- [Dados em soluções do Office](../vsto/data-in-office-solutions.md)
- [Walkthrough: vinculação de dados simples em um projeto de nível de documento](../vsto/walkthrough-simple-data-binding-in-a-document-level-project.md)
