---
title: 'Walkthrough: criar um modelo usando controles de conteúdo'
description: Saiba como criar uma personalização em nível de documento que usa controles de conteúdo para criar conteúdo estruturado e reutilizável em um modelo do Microsoft Word.
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- building blocks [Office development in Visual Studio]
- Word [Office development in Visual Studio], creating documents
- content controls [Office development in Visual Studio], adding to documents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 7f78ca406d19461de7fa8e2a8c147b1003c9c852
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826961"
---
# <a name="walkthrough-create-a-template-by-using-content-controls"></a>Walkthrough: criar um modelo usando controles de conteúdo
  Este tutorial demonstra como criar uma personalização em nível de documento que usa controles de conteúdo para criar conteúdo estruturado e reutilizável em um modelo do Word Microsoft Office.

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 O Word permite que você crie uma coleção de partes de documentos reutilizáveis, chamadas de *blocos de construção*. Este tutorial mostra como criar duas tabelas como blocos de construção. Cada tabela contém vários controles de conteúdo que podem conter diferentes tipos de conteúdo, como texto sem formatação ou datas. Uma das tabelas contém informações sobre um funcionário e a outra tabela contém comentários do cliente.

 Depois de criar um documento a partir do modelo, você pode adicionar uma das tabelas ao documento usando vários <xref:Microsoft.Office.Tools.Word.BuildingBlockGalleryContentControl> objetos, que exibem os blocos de construção disponíveis no modelo.

 Este passo a passo ilustra as seguintes tarefas:

- Criar tabelas que contêm controles de conteúdo em um modelo do Word em tempo de design.

- Preencher um controle de conteúdo de caixa de combinação e um controle de conteúdo de lista suspensa programaticamente.

- Impedir que os usuários editem uma tabela especificada.

- Adicionar tabelas à coleção de blocos de construção de um modelo.

- Criar um controle de conteúdo que exibe os blocos de construção disponíveis no modelo.

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>Pré-requisitos
 Você precisará dos seguintes componentes para concluir este passo a passo:

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft Word.

## <a name="create-a-new-word-template-project"></a>Criar um novo projeto de modelo do Word
 Crie um modelo do Word para que os usuários possam criar suas próprias cópias facilmente.

### <a name="to-create-a-new-word-template-project"></a>Para criar um novo projeto de modelo do Word

1. Crie um projeto de modelo do Word com o nome **MyBuildingBlockTemplate**. No assistente, crie um novo documento na solução. Para obter mais informações, consulte [como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Abre o novo modelo do Word no designer e adiciona o projeto **MyBuildingBlockTemplate** ao **Gerenciador de soluções**.

## <a name="create-the-employee-table"></a>Criar a tabela Employee
 Crie uma tabela que contém quatro tipos diferentes de controles de conteúdo em que o usuário pode inserir informações sobre um funcionário.

### <a name="to-create-the-employee-table"></a>Para criar a tabela Employee

1. No modelo do Word hospedado no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Designer, na faixa de palavras, clique na guia **Inserir** .

2. No grupo **tabelas** , clique em **tabela** e insira uma tabela com duas colunas e quatro linhas.

3. Digite o texto na primeira coluna para que seja semelhante à seguinte coluna:

   ||
   |-|
   |**Nome do funcionário**|
   |**Hire Date**|
   |**Título**|
   |**Imagem**|

4. Clique na primeira célula na segunda coluna (ao lado do **nome do funcionário**).

5. Na faixa de faixas, clique na guia **desenvolvedor** .

   > [!NOTE]
   > Se a guia **desenvolvedor** não estiver visível, você deverá primeiro mostrá-la. Para obter mais informações, consulte [como: mostrar a guia Desenvolvedor na faixa de faixas](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md).

6. No grupo **controles** , clique no botão  de texto ![PlainTextContentControl](../vsto/media/plaintextcontrol.gif "PlainTextContentControl") para adicionar um <xref:Microsoft.Office.Tools.Word.PlainTextContentControl> à primeira célula.

7. Clique na segunda célula na segunda coluna (ao lado de **data de contratação**).

8. No grupo **controles** , clique no botão **seletor de data** ![DatePickerContentControl](../vsto/media/datepicker.gif "DatePickerContentControl") para adicionar um <xref:Microsoft.Office.Tools.Word.DatePickerContentControl> à segunda célula.

9. Clique na terceira célula na segunda coluna (ao lado de **título**).

10. No grupo **controles** , clique no botão da **caixa de combinação** ![ComboBoxContentControl](../vsto/media/combobox.gif "ComboBoxContentControl") para adicionar um <xref:Microsoft.Office.Tools.Word.ComboBoxContentControl> à terceira célula.

11. Clique na última célula na segunda coluna (ao lado de **imagem**).

12. No grupo **controles** , clique no botão **controle de conteúdo da imagem** ![PictureContentControl](../vsto/media/pictcontentcontrol.gif "PictureContentControl") para adicionar um <xref:Microsoft.Office.Tools.Word.PictureContentControl> à última célula.

## <a name="create-the-customer-feedback-table"></a>Criar a tabela de comentários do cliente
 Crie uma tabela que contenha três tipos diferentes de controles de conteúdo em que o usuário pode inserir informações de comentários do cliente.

### <a name="to-create-the-customer-feedback-table"></a>Para criar a tabela de comentários do cliente

1. No modelo do Word, clique na linha após a tabela Employee que você adicionou anteriormente e pressione **Enter** para adicionar um novo parágrafo.

2. Na faixa de faixas, clique na guia **Inserir** .

3. No grupo **tabelas** , clique em **tabela** e insira uma tabela com duas colunas e três linhas.

4. Digite o texto na primeira coluna para que seja semelhante à seguinte coluna:

   ||
   |-|
   |**Nome do Cliente**|
   |**Classificação de satisfação**|
   |**Comentários**|

5. Clique na primeira célula da segunda coluna (ao lado de **nome do cliente**).

6. Na faixa de faixas, clique na guia **desenvolvedor** .

7. No grupo **controles** , clique no botão  de texto ![PlainTextContentControl](../vsto/media/plaintextcontrol.gif "PlainTextContentControl") para adicionar um <xref:Microsoft.Office.Tools.Word.PlainTextContentControl> à primeira célula.

8. Clique na segunda célula da segunda coluna (ao lado da **classificação de satisfação**).

9. No grupo **controles** , clique no botão de **lista suspensa** ![DropDownListContentControl](../vsto/media/dropdownlist.gif "DropDownListContentControl") para adicionar um <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> à segunda célula.

10. Clique na última célula da segunda coluna (ao lado de **comentários**).

11. No grupo **controles** , clique no botão **Rich Text** ![RichTextContentControl](../vsto/media/richtextcontrol.gif "RichTextContentControl") para adicionar um <xref:Microsoft.Office.Tools.Word.RichTextContentControl> à última célula.

## <a name="populate-the-combo-box-and-drop-down-list-programmatically"></a>Preencher a caixa de combinação e a lista suspensa programaticamente
 Você pode inicializar os controles de conteúdo em tempo de design usando a janela **Propriedades** no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] . Você também pode inicializá-los em tempo de execução, o que permite que você defina seus Estados iniciais dinamicamente. Para esta explicação, use o código para popular as entradas no <xref:Microsoft.Office.Tools.Word.ComboBoxContentControl> e <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> no tempo de execução para que você possa ver como esses objetos funcionam.

### <a name="to-modify-the-ui-of-the-content-controls-programmatically"></a>Para modificar a interface do usuário dos controles de conteúdo programaticamente

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse em **ThisDocument. cs** ou **ThisDocument. vb** e clique em **Exibir código**.

2. Adicione o código a seguir à classe `ThisDocument` . Esse código declara vários objetos que você usará posteriormente neste passo a passos.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/ContentControlTemplateWalkthrough/ThisDocument.vb" id="Snippet1":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/ContentControlTemplateWalkthrough/ThisDocument.cs" id="Snippet1":::

3. Adicione o código a seguir ao `ThisDocument_Startup` método da `ThisDocument` classe. Esse código adiciona entradas ao <xref:Microsoft.Office.Tools.Word.ComboBoxContentControl> e <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> nas tabelas e define o texto do espaço reservado que é exibido em cada um desses controles antes de o usuário editá-los.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/ContentControlTemplateWalkthrough/ThisDocument.vb" id="Snippet2":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/ContentControlTemplateWalkthrough/ThisDocument.cs" id="Snippet2":::

## <a name="prevent-users-from-editing-the-employee-table"></a>Impedir que os usuários editem a tabela Employee
 Use o <xref:Microsoft.Office.Tools.Word.GroupContentControl> objeto declarado anteriormente para proteger a tabela Employee. Depois de proteger a tabela, os usuários ainda poderão editar os controles de conteúdo na tabela. No entanto, eles não podem editar texto na primeira coluna ou modificar a tabela de outras maneiras, como adicionar ou excluir linhas e colunas. Para obter mais informações sobre como usar um <xref:Microsoft.Office.Tools.Word.GroupContentControl> para proteger uma parte de um documento, consulte [controles de conteúdo](../vsto/content-controls.md).

### <a name="to-prevent-users-from-editing-the-employee-table"></a>Para impedir que os usuários editem a tabela Employee

1. Adicione o código a seguir ao `ThisDocument_Startup` método da `ThisDocument` classe, após o código que você adicionou na etapa anterior. Esse código impede que os usuários editem a tabela Employee colocando a tabela dentro do <xref:Microsoft.Office.Tools.Word.GroupContentControl> objeto que você declarou anteriormente.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/ContentControlTemplateWalkthrough/ThisDocument.vb" id="Snippet3":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/ContentControlTemplateWalkthrough/ThisDocument.cs" id="Snippet3":::

## <a name="add-the-tables-to-the-building-block-collection"></a>Adicionar as tabelas à coleção de blocos de construção
 Adicione as tabelas a uma coleção de blocos de construção de documento no modelo para que os usuários possam inserir as tabelas que você criou no documento. Para obter mais informações sobre blocos de construção de documento, consulte [controles de conteúdo](../vsto/content-controls.md).

### <a name="to-add-the-tables-to-the-building-blocks-in-the-template"></a>Para adicionar as tabelas aos blocos de construção no modelo

1. Adicione o código a seguir ao `ThisDocument_Startup` método da `ThisDocument` classe, após o código que você adicionou na etapa anterior. Esse código adiciona novos blocos de construção que contêm as tabelas à coleção Microsoft. Office. Interop. Word. BuildingBlockEntries, que contém todos os blocos de construção reutilizáveis no modelo. Os novos blocos de construção são definidos em uma nova categoria denominada **informações de funcionário e cliente** e recebem o tipo de bloco de construção `Microsoft.Office.Interop.Word.WdBuildingBlockTypes.wdTypeCustom1` .

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/ContentControlTemplateWalkthrough/ThisDocument.vb" id="Snippet4":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/ContentControlTemplateWalkthrough/ThisDocument.cs" id="Snippet4":::

2. Adicione o código a seguir ao `ThisDocument_Startup` método da `ThisDocument` classe, após o código que você adicionou na etapa anterior. Esse código exclui as tabelas do modelo. As tabelas não são mais necessárias, pois você as adicionou à galeria de blocos de construção reutilizáveis no modelo. O código coloca o documento primeiro em modo de design para que a tabela de funcionários protegida possa ser excluída.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/ContentControlTemplateWalkthrough/ThisDocument.vb" id="Snippet5":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/ContentControlTemplateWalkthrough/ThisDocument.cs" id="Snippet5":::

## <a name="create-a-content-control-that-displays-the-building-blocks"></a>Criar um controle de conteúdo que exibe os blocos de construção
 Crie um controle de conteúdo que forneça acesso aos blocos de construção (ou seja, as tabelas) que você criou anteriormente. Os usuários podem clicar nesse controle para adicionar as tabelas ao documento.

### <a name="to-create-a-content-control-that-displays-the-building-blocks"></a>Para criar um controle de conteúdo que exibe os blocos de construção

1. Adicione o código a seguir ao `ThisDocument_Startup` método da `ThisDocument` classe, após o código que você adicionou na etapa anterior. Esse código inicializa o <xref:Microsoft.Office.Tools.Word.BuildingBlockGalleryContentControl> objeto que você declarou anteriormente. O <xref:Microsoft.Office.Tools.Word.BuildingBlockGalleryContentControl> exibe todos os blocos de construção definidos na categoria **informações de funcionário e cliente** e que têm o tipo de bloco de construção `Microsoft.Office.Interop.Word.WdBuildingBlockTypes.wdTypeCustom1` .

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/ContentControlTemplateWalkthrough/ThisDocument.vb" id="Snippet6":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/ContentControlTemplateWalkthrough/ThisDocument.cs" id="Snippet6":::

## <a name="test-the-project"></a>Testar o projeto
 Os usuários podem clicar nos controles da Galeria de blocos de construção no documento para inserir a tabela de funcionários ou a tabela de comentários do cliente. Os usuários podem digitar ou selecionar respostas nos controles de conteúdo nas duas tabelas. Os usuários podem modificar outras partes da tabela de comentários do cliente, mas não devem ser capazes de modificar outras partes da tabela Employee.

### <a name="to-test-the-employee-table"></a>Para testar a tabela Employee

1. Pressione **F5** para executar o projeto.

2. Clique em **escolher seu primeiro bloco de construção** para exibir o primeiro controle de conteúdo da Galeria de blocos de construção.

3. Clique na seta suspensa ao lado do título **Galeria personalizada 1** no controle e selecione **tabela de funcionários**.

4. Clique na célula à direita da célula nome do **funcionário** e digite um nome.

     Verifique se você pode adicionar apenas texto a esta célula. O <xref:Microsoft.Office.Tools.Word.PlainTextContentControl> permite que os usuários adicionem apenas texto, e não outros tipos de conteúdo, como arte ou uma tabela.

5. Clique na célula à direita da célula data de **contratação** e selecione uma data no seletor de data.

6. Clique na célula à direita da célula de **título** e selecione um dos títulos de trabalho na caixa de combinação.

     Opcionalmente, digite o nome de um cargo que não esteja na lista. Isso é possível porque o <xref:Microsoft.Office.Tools.Word.ComboBoxContentControl> permite que os usuários selecionem em uma lista de entradas ou digitem suas próprias entradas.

7. Clique no ícone na célula à direita da célula da **imagem** e navegue até uma imagem para exibi-la.

8. Tente adicionar linhas ou colunas à tabela e tente excluir linhas e colunas da tabela. Verifique se você não pode modificar a tabela. O <xref:Microsoft.Office.Tools.Word.GroupContentControl> impede que você faça modificações.

### <a name="to-test-the-customer-feedback-table"></a>Para testar a tabela de comentários do cliente

1. Clique em **escolher seu segundo bloco de construção** para exibir o segundo controle de conteúdo da Galeria de blocos de construção.

2. Clique na seta suspensa ao lado do título **Galeria personalizada 1** no controle e selecione **tabela cliente**.

3. Clique na célula à direita da célula nome do **cliente** e digite um nome.

4. Clique na célula à direita da célula de **classificação de satisfação** e selecione uma das opções disponíveis.

     Verifique se você não pode digitar sua própria entrada. O <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> permite que os usuários selecionem apenas em uma lista de entradas.

5. Clique na célula à direita da célula **comentários** e digite alguns comentários.

     Opcionalmente, adicione algum conteúdo que não seja texto, como arte ou uma tabela inserida. Isso é possível porque o <xref:Microsoft.Office.Tools.Word.RichTextContentControl> permite que os usuários adicionem conteúdo que não seja texto.

6. Verifique se você pode adicionar linhas ou colunas à tabela, e se você pode excluir linhas e colunas da tabela. Isso é possível porque você não protegeu a tabela colocando-a em um <xref:Microsoft.Office.Tools.Word.GroupContentControl> .

7. Feche o modelo.

## <a name="next-steps"></a>Próximas etapas
 Você pode aprender mais sobre como usar controles de conteúdo deste tópico:

- Associar controles de conteúdo a partes do XML, também nomeadas como partes XML personalizadas, que são inseridas em um documento. Para obter mais informações, consulte [Walkthrough: associar controles de conteúdo a partes XML personalizadas](../vsto/walkthrough-binding-content-controls-to-custom-xml-parts.md).

## <a name="see-also"></a>Consulte também
- [Automatizar o Word usando objetos estendidos](../vsto/automating-word-by-using-extended-objects.md)
- [Controles de conteúdo](../vsto/content-controls.md)
- [Como: adicionar controles de conteúdo a documentos do Word](../vsto/how-to-add-content-controls-to-word-documents.md)
- [Como: proteger partes de documentos usando controles de conteúdo](../vsto/how-to-protect-parts-of-documents-by-using-content-controls.md)
- [Visão geral de itens de host e controles de host](../vsto/host-items-and-host-controls-overview.md)
- [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [Adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md)
