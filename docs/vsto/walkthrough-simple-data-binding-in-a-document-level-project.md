---
title: 'Walkthrough: vinculação de dados simples em um projeto de nível de documento'
description: Aprenda os conceitos básicos da ligação de dados em um projeto de nível de documento e que um único campo de dados em um SQL Server banco de dado está associado a um intervalo nomeado no Microsoft Excel.
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data binding [Office development in Visual Studio], worksheet cell to Database field
- worksheets [Office development in Visual Studio], binding worksheet cell to Database field
- Database field [Office development in Visual Studio]
- data [Office development in Visual Studio], binding data
- simple data binding [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 36d4da65a6cd39c53f1f9d8edf4f9d9b1fe46284
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826844"
---
# <a name="walkthrough-simple-data-binding-in-a-document-level-project"></a>Walkthrough: vinculação de dados simples em um projeto de nível de documento
  Este tutorial demonstra os conceitos básicos da vinculação de dados em um projeto de nível de documento. Um único campo de dados em um banco de dado SQL Server está associado a um intervalo nomeado no Microsoft Office Excel. O Walkthrough também mostra como adicionar controles que permitem percorrer todos os registros na tabela.

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 Este passo a passo ilustra as seguintes tarefas:

- Criando uma fonte de dados para um projeto do Excel.

- Adicionando controles a uma planilha.

- Rolagem por meio de registros de banco de dados.

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>Pré-requisitos
 Você precisará dos seguintes componentes para concluir este passo a passo:

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] ou [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)].

- Acesso a um servidor com o banco de dados Northwind SQL Server exemplo.

- Permissões para ler e gravar no banco de dados de SQL Server.

## <a name="create-a-new-project"></a>Criar um novo projeto
 Nesta etapa, você criará um projeto de pasta de trabalho do Excel.

### <a name="to-create-a-new-project"></a>Para criar um novo projeto

1. Crie um projeto de pasta de trabalho do Excel com o nome **minha vinculação de dados simples**, usando Visual Basic ou C#. Verifique se **a seleção criar um novo documento** está selecionada. Para obter mais informações, consulte [como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).

   O Visual Studio abre a nova pasta de trabalho do Excel no designer e adiciona o meu projeto de **vinculação de dados simples** a **Gerenciador de soluções**.

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

8. Marque a caixa de seleção ao lado da tabela **clientes** .

9. Clique em **Concluir**.

   O assistente adiciona a tabela **Customers** à janela **fontes de dados** . Ele também adiciona um conjunto de um dataset tipado ao seu projeto que está visível no **Gerenciador de soluções**.

## <a name="add-controls-to-the-worksheet"></a>Adicionar controles à planilha
 Para esta explicação, você precisa de dois intervalos nomeados e quatro botões na primeira planilha. Primeiro, adicione os dois intervalos nomeados da janela **fontes de dados** para que eles sejam associados automaticamente à fonte de dados. Em seguida, adicione os botões da **caixa de ferramentas**.

### <a name="to-add-two-named-ranges"></a>Para adicionar dois intervalos nomeados

1. Verifique se a pasta de trabalho *meus dados simples Binding.xlsx* está aberta no designer do Visual Studio, com **Sheet1** exibida.

2. Abra a janela **Data Sources** e expanda o nó **Customers** .

3. Selecione a coluna **CompanyName** e clique na seta suspensa que aparece.

4. Selecione **NamedRange** na lista suspensa e arraste a coluna **CompanyName** para a célula **a1**.

     Um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle chamado `companyNameNamedRange` é criado na célula **a1**. Ao mesmo tempo, um <xref:System.Windows.Forms.BindingSource> nome `customersBindingSource` , um adaptador de tabela e uma <xref:System.Data.DataSet> instância são adicionados ao projeto. O controle está associado ao <xref:System.Windows.Forms.BindingSource> , que, por sua vez, está associado à <xref:System.Data.DataSet> instância.

5. Selecione a coluna **CustomerID** na janela **Data Sources** e clique na seta suspensa exibida.

6. Clique em **NamedRange** na lista suspensa e arraste a coluna **CustomerID** para a célula **B1**.

7. Outro <xref:Microsoft.Office.Tools.Excel.NamedRange> controle chamado `customerIDNamedRange` é criado na célula **B1** e associado a <xref:System.Windows.Forms.BindingSource> .

### <a name="to-add-four-buttons"></a>Para adicionar quatro botões

1. Na guia **controles comuns** da caixa de **ferramentas**, adicione um <xref:System.Windows.Forms.Button> controle à célula **a3** da planilha.

    Esse botão é denominado `Button1` .

2. Adicione mais três botões às células a seguir nesta ordem, para que os nomes sejam como mostrado:

   |Célula|(Nome)|
   |----------|--------------|
   |B3|Button2|
   |C3|Button3|
   |D3|Button4|

   A próxima etapa é adicionar texto aos botões e, em C#, adicionar manipuladores de eventos.

## <a name="initialize-the-controls"></a>Inicializar os controles
 Defina o texto do botão e adicione manipuladores de eventos durante o <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> evento.

### <a name="to-initialize-the-controls"></a>Para inicializar os controles

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse em **Plan1. vb** ou **Plan1. cs** e clique em **Exibir código** no menu de atalho.

2. Adicione o código a seguir ao `Sheet1_Startup` método para definir o texto para cada botão.

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs" id="Snippet2":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb" id="Snippet2":::

3. Somente para C#, adicione manipuladores de eventos para os eventos de clique de botão ao `Sheet1_Startup` método.

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs" id="Snippet3":::

   Agora, adicione o código para manipular os <xref:System.Windows.Forms.Control.Click> eventos dos botões para que o usuário possa navegar pelos registros.

## <a name="add-code-to-enable-scrolling-through-the-records"></a>Adicionar código para habilitar a rolagem pelos registros
 Adicione código ao <xref:System.Windows.Forms.Control.Click> manipulador de eventos de cada botão para percorrer os registros.

### <a name="to-move-to-the-first-record"></a>Para mover para o primeiro registro

1. Adicione um manipulador de eventos para o <xref:System.Windows.Forms.Control.Click> evento do `Button1` botão e adicione o seguinte código para mover para o primeiro registro:

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs" id="Snippet4":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb" id="Snippet4":::

### <a name="to-move-to-the-previous-record"></a>Para mover para o registro anterior

1. Adicione um manipulador de eventos para o <xref:System.Windows.Forms.Control.Click> evento do `Button2` botão e adicione o seguinte código para mover a posição de volta por um:

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs" id="Snippet5":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb" id="Snippet5":::

### <a name="to-move-to-the-next-record"></a>Para mover para o próximo registro

1. Adicione um manipulador de eventos para o <xref:System.Windows.Forms.Control.Click> evento do `Button3` botão e adicione o seguinte código para avançar a posição em um:

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs" id="Snippet6":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb" id="Snippet6":::

### <a name="to-move-to-the-last-record"></a>Para mover para o último registro

1. Adicione um manipulador de eventos para o <xref:System.Windows.Forms.Control.Click> evento do `Button4` botão e adicione o seguinte código para mover para o último registro:

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs" id="Snippet7":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb" id="Snippet7":::

## <a name="test-the-application"></a>Testar o aplicativo
 Agora você pode testar sua pasta de trabalho para verificar se você pode navegar pelos registros no banco de dados.

### <a name="to-test-your-workbook"></a>Para testar sua pasta de trabalho

1. Pressione **F5** para executar o projeto.

2. Confirme se o primeiro registro aparece nas células **a1** e **B1**.

3. Clique no **>** `Button3` botão () e confirme se o próximo registro aparece na célula **a1** e **B1**.

4. Clique nos outros botões de rolagem para confirmar se o registro é alterado conforme o esperado.

## <a name="next-steps"></a>Próximas etapas
 Este tutorial mostra as noções básicas de associação de um intervalo nomeado a um campo em um banco de dados. Estas são algumas tarefas que podem vir a seguir:

- Armazene os dados em cache para que eles possam ser usados offline. Para obter mais informações, consulte [como armazenar em cache os dados para uso offline ou em um servidor](../vsto/how-to-cache-data-for-use-offline-or-on-a-server.md).

- Associe células a várias colunas em uma tabela, em vez de a um campo. Para obter mais informações, consulte [Walkthrough: ligação de dados complexa em um projeto de nível de documento](../vsto/walkthrough-complex-data-binding-in-a-document-level-project.md).

- Use um <xref:System.Windows.Forms.BindingNavigator> controle para percorrer os registros. Para obter mais informações, consulte [como navegar dados com o controle BindingNavigator Windows Forms](/dotnet/framework/winforms/controls/bindingnavigator-control-overview-windows-forms).

## <a name="see-also"></a>Consulte também
- [Associar dados a controles em soluções do Office](../vsto/binding-data-to-controls-in-office-solutions.md)
- [Dados em soluções do Office](../vsto/data-in-office-solutions.md)
- [Walkthrough: ligação de dados complexa em um projeto de nível de documento](../vsto/walkthrough-complex-data-binding-in-a-document-level-project.md)
