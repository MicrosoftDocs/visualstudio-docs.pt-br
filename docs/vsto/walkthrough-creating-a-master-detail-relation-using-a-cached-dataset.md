---
title: Criar relação de detalhes mestre usando conjunto de armazenamento em cache
description: Saiba como criar uma relação mestre/detalhes em uma planilha e armazenar em cache os dados para que a solução possa ser usada offline.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- master-detail tables [Office development in Visual Studio], walkthroughs
- data caching [Office development in Visual Studio], Master/Detail Relation
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 177b21e2278153693601adf7b7dc18b751cf184e
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824842"
---
# <a name="walkthrough-create-a-master-detail-relation-using-a-cached-dataset"></a>Walkthrough: criar uma relação de detalhes mestre usando um conjunto de um DataSet armazenado em cache
  Este tutorial demonstra como criar uma relação mestre/detalhes em uma planilha e armazenar em cache os dados para que a solução possa ser usada offline.

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 Durante este passo a passo, você aprenderá a:

- Adicionar controles a uma planilha.

- Configure um conjunto de uma para ser armazenado em cache em uma planilha.

- Adicione código para habilitar a rolagem pelos registros.

- Teste seu projeto.

> [!NOTE]
> Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, consulte [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).

## <a name="prerequisites"></a>Pré-requisitos
 Você precisará dos seguintes componentes para concluir este passo a passo:

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] ou [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)].

- Acesso ao banco de dados Northwind SQL Server exemplo. O banco de dados pode estar no seu computador de desenvolvimento ou em um servidor.

- Permissões para ler e gravar no banco de dados de SQL Server.

## <a name="create-a-new-project"></a>Criar um novo projeto
 Nesta etapa, você criará um projeto de pasta de trabalho do Excel.

### <a name="to-create-a-new-project"></a>Para criar um novo projeto

1. Crie um projeto de pasta de trabalho do Excel com o nome **meu mestre-detalhe**, usando Visual Basic ou C#. Verifique se **a seleção criar um novo documento** está selecionada. Para obter mais informações, consulte [como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).

   O Visual Studio abre a nova pasta de trabalho do Excel no designer e adiciona o meu projeto de **detalhes mestre** a **Gerenciador de soluções**.

## <a name="create-the-data-source"></a>Criar a fonte de dados
 Use a janela **Data Sources** para adicionar um conjunto de dados tipado ao seu projeto.

### <a name="to-create-the-data-source"></a>Para criar a fonte de dados

1. Se a janela **fontes de dados** não estiver visível, exiba-a por, na barra de menus, escolhendo **Exibir**  >  **outras**  >  **fontes de dados** do Windows.

2. Escolha **Adicionar nova fonte de dados** para iniciar o **Assistente de configuração de fonte de dados**.

3. Selecione **banco de dados** e clique em **Avançar**.

4. Selecione uma conexão de dados para o exemplo da Northwind SQL Server Database ou adicione uma nova conexão usando o botão **nova conexão** .

5. Depois de selecionar ou criar uma conexão, clique em **Avançar**.

6. Desmarque a opção para salvar a conexão, se ela estiver selecionada, e clique em **Avançar**.

7. Expanda o nó **tabelas** na janela **objetos de banco de dados** .

8. Selecione a tabela **pedidos** e a tabela **detalhes do pedido** .

9. Clique em **Concluir**.

   O assistente adiciona as duas tabelas à janela **fontes de dados** . Ele também adiciona um conjunto de um dataset tipado ao seu projeto que está visível no **Gerenciador de soluções**.

## <a name="add-controls-to-the-worksheet"></a>Adicionar controles à planilha
 Nesta etapa, você adicionará um intervalo nomeado, um objeto de lista e dois botões à primeira planilha. Primeiro, adicione o intervalo nomeado e o objeto de lista da janela **fontes de dados** para que eles sejam associados automaticamente à fonte de dados. Em seguida, adicione os botões da **caixa de ferramentas**.

### <a name="to-add-a-named-range-and-a-list-object"></a>Para adicionar um intervalo nomeado e um objeto de lista

1. Verifique se a pasta de trabalho **meu Master-Detail.xlsx** está aberta no designer do Visual Studio, com **Sheet1** exibida.

2. Abra a janela **fontes de dados** e expanda o nó **pedidos** .

3. Selecione a coluna **OrderID** e clique na seta suspensa exibida.

4. Clique em **NamedRange** na lista suspensa e arraste a coluna **OrderID** para a célula **a2**.

     Um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle chamado `OrderIDNamedRange` é criado na célula **a2**. Ao mesmo tempo, um <xref:System.Windows.Forms.BindingSource> nome `OrdersBindingSource` , um adaptador de tabela e uma <xref:System.Data.DataSet> instância são adicionados ao projeto. O controle está associado ao <xref:System.Windows.Forms.BindingSource> , que, por sua vez, está associado à <xref:System.Data.DataSet> instância.

5. Role para baixo após as colunas que estão sob a tabela **Orders** . Na parte inferior da lista está a tabela **detalhes do pedido** ; Ele está aqui porque é um filho da tabela **Orders** . Selecione esta tabela **detalhes do pedido** , não aquela que está no mesmo nível que a tabela **pedidos** e clique na seta suspensa exibida.

6. Clique em **ListObject** na lista suspensa e arraste a tabela **OrderDetails** para a célula **a6**.

7. Um <xref:Microsoft.Office.Tools.Excel.ListObject> controle chamado **Order_DetailsListObject** é criado na célula **a6** e associado ao <xref:System.Windows.Forms.BindingSource> .

### <a name="to-add-two-buttons"></a>Para adicionar dois botões

1. Na guia **controles comuns** da caixa de **ferramentas**, adicione um <xref:System.Windows.Forms.Button> controle à célula **a3** da planilha.

    Esse botão é denominado `Button1` .

2. Adicione outro <xref:System.Windows.Forms.Button> controle à célula **B3** da planilha.

    Esse botão é denominado `Button2` .

   Em seguida, marque o conjunto de armazenamento a ser armazenado em cache no documento.

## <a name="cache-the-dataset"></a>Armazenar o conjunto de armazenamento em cache
 Marque o conjunto de armazenamento a ser armazenado em cache no documento tornando o conjunto de um público e definindo a propriedade **CacheInDocument** .

### <a name="to-cache-the-dataset"></a>Para armazenar em cache o conjunto de armazenamento

1. Selecione **NorthwindDataSet** na bandeja de componentes.

2. Na janela **Propriedades** , altere a propriedade **modificadores** para **público**.

    Os conjuntos de valores devem ser públicos antes da habilitação do Caching.

3. Altere a propriedade **CacheInDocument** para **true**.

   A próxima etapa é adicionar texto aos botões e, em C#, adicionar código para conectar os manipuladores de eventos.

## <a name="initialize-the-controls"></a>Inicializar os controles
 Defina o texto do botão e adicione manipuladores de eventos durante o <xref:Microsoft.Office.Tools.Excel.Workbook.Startup> evento.

### <a name="to-initialize-the-data-and-the-controls"></a>Para inicializar os dados e os controles

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse em **Plan1. vb** ou **Plan1. cs** e clique em **Exibir código** no menu de atalho.

2. Adicione o código a seguir ao `Sheet1_Startup` método para definir o texto para os botões.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet2.vb" id="Snippet15":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet2.cs" id="Snippet15":::

3. Somente para C#, adicione manipuladores de eventos para os eventos de clique de botão ao `Sheet1_Startup` método.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet2.cs" id="Snippet16":::

## <a name="add-code-to-enable-scrolling-through-the-records"></a>Adicionar código para habilitar a rolagem pelos registros
 Adicione código ao <xref:System.Windows.Forms.Control.Click> manipulador de eventos de cada botão para percorrer os registros.

### <a name="to-scroll-through-the-records"></a>Para percorrer os registros

1. Adicione um manipulador de eventos para o <xref:System.Windows.Forms.Control.Click> evento de `Button1` e adicione o seguinte código para mover-se para trás pelos registros:

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet2.vb" id="Snippet17":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet2.cs" id="Snippet17":::

2. Adicione um manipulador de eventos para o <xref:System.Windows.Forms.Control.Click> evento de `Button2` e adicione o seguinte código para avançar pelos registros:

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet2.vb" id="Snippet18":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet2.cs" id="Snippet18":::

## <a name="test-the-application"></a>Testar o aplicativo
 Agora você pode testar sua pasta de trabalho para certificar-se de que os dados aparecem como esperado e que você pode usar a solução offline.

### <a name="to-test-the-data-caching"></a>Para testar o cache de dados

1. Pressione **F5**.

2. Verifique se o intervalo nomeado e o objeto de lista estão preenchidos com dados da fonte de dados.

3. Percorra alguns dos registros clicando nos botões.

4. Salve a pasta de trabalho e, em seguida, feche a pasta de trabalho e o Visual Studio.

5. Desabilite a conexão com o banco de dados. Desconecte o cabo de rede do seu computador se o banco de dados estiver localizado em um servidor ou pare o serviço SQL Server se o banco de dados estiver em seu computador de desenvolvimento.

6. Abra o Excel e, em seguida, abra **meu Master-Detail.xlsx** no diretório *\Bin* (*\Meus Master-Detail\bin* em Visual Basic ou *\Meus Master-Detail\bin\debug* em C#).

7. Percorra alguns dos registros para ver que a planilha funciona normalmente quando desconectada.

8. Reconecte-se ao banco de dados. Conecte o computador à rede novamente, se o banco de dados estiver localizado em um servidor, ou inicie o serviço de SQL Server se o banco de dados estiver em seu computador de desenvolvimento.

## <a name="next-steps"></a>Próximas etapas
 Este tutorial mostra as noções básicas de como criar uma relação de dados mestre/detalhes em uma planilha e armazenar em cache um DataSet. Estas são algumas tarefas que podem vir a seguir:

- Implante a solução. Para obter mais informações, consulte [implantar uma solução do Office](../vsto/deploying-an-office-solution.md)

## <a name="see-also"></a>Consulte também
- [Associar dados a controles em soluções do Office](../vsto/binding-data-to-controls-in-office-solutions.md)
- [Dados em soluções do Office](../vsto/data-in-office-solutions.md)
- [Dados de cache](../vsto/caching-data.md)
- [Visão geral de itens de host e controles de host](../vsto/host-items-and-host-controls-overview.md)
