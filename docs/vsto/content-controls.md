---
title: Controles de conteúdo
description: Aprenda controles de conteúdo e como os controles de conteúdo fornecem uma maneira de criar documentos e modelos.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VST.Toolbox.DropDownListContentControl
- VST.Toolbox.RichTextContentControl
- VST.Toolbox.PlainTextContentControl
- VST.Toolbox.ComboBoxContentControl
- VST.Toolbox.CCBuildingBlockGalleryContentControl
- VST.Toolbox.DatePickerContentControl
- VST.Toolbox.PictureContentControl
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- document building blocks [Office development in Visual Studio]
- restricted permissions [Office development in Visual Studio]
- ComboBoxContentControl class
- PictureContentControl class
- PlainTextContentControl class
- Office documents [Office development in Visual Studio], restricted permissions
- RichTextContentControl class
- content controls [Office development in Visual Studio]
- building block gallery [Office development in Visual Studio]
- controls [Office development in Visual Studio], content controls
- GroupContentControl class
- documents [Office development in Visual Studio], restricted permissions
- DropDownListContentControl class
- DatePickerContentControl class
- data binding [Office development in Visual Studio], content controls
- content controls [Office development in Visual Studio], about content controls
- custom XML parts, content controls
- templates [Office development in Visual Studio], content controls
- BuildingBlockGalleryContentControl class
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: b0d55daba4dee07454a31fcb6fc5fa210e8bcc34
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825050"
---
# <a name="content-controls"></a>Controles de conteúdo
  Os controles de conteúdo fornecem uma maneira de criar documentos e modelos que tenham estes recursos:

- Uma interface do usuário que tem entrada controlada como um formulário.

- Restrições que impedem que os usuários editem seções protegidas do documento ou modelo. Para obter mais informações, consulte [proteger partes de documentos usando controles de conteúdo](#Protection).

- Associação de dados a uma fonte de dados. Para obter mais informações, consulte [associar dados a controles de conteúdo](#DataBinding).

  [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

  ![link para vídeo](../vsto/media/playvideo.gif "link para vídeo") Para ver uma demonstração de vídeo relacionada, consulte [associar dados a controles de conteúdo do Word 2007 usando o ferramentas do Visual Studio para o sistema do Office (3,0)](/previous-versions/office/developer/office-2007/bb967663(v=office.12)).

## <a name="overview-of-content-controls"></a>Visão geral dos controles de conteúdo
 Os controles de conteúdo fornecem uma interface de usuário que é otimizada para entrada e impressão do usuário. Quando você adiciona um controle de conteúdo a um documento, o controle é identificado por uma borda, um título e um texto temporário que pode fornecer instruções ao usuário. A borda e o título do controle não aparecem nas versões impressas do documento.

 Por exemplo, se você quiser que o usuário insira uma data em uma seção do documento, poderá adicionar um controle de conteúdo do seletor de data ao documento. Quando os usuários clicam no controle, a interface do usuário do seletor de data padrão é exibida. Você também pode definir as propriedades do controle para definir o calendário regional que é exibido e especificar o formato de data. Depois que o usuário escolher uma data, a interface do usuário do controle será ocultada e somente a data aparecerá se o usuário imprimir o documento.

 Os controles de conteúdo também ajudam você a fazer o seguinte:

- Impedir que os usuários editem ou excluam partes de um documento. Isso será útil se você tiver informações em um documento ou modelo que os usuários devem ser capazes de ler, mas não editar, ou se você quiser que os usuários possam editar controles de conteúdo, mas não excluí-los.

- Associar partes de um documento ou modelo aos dados. Você pode associar controles de conteúdo a campos de banco de dados, objetos gerenciados nos [!INCLUDE[dnprdnshort](../sharepoint/includes/dnprdnshort-md.md)] elementos XML, que são armazenados no documento e em outras fontes.

  Em projetos de nível de documento, você pode adicionar controles de conteúdo ao seu documento em tempo de design ou em tempo de execução. Em projetos de suplemento do VSTO, você pode adicionar controles de conteúdo a qualquer documento aberto em tempo de execução. Para obter mais informações, consulte [como: adicionar controles de conteúdo a documentos do Word](../vsto/how-to-add-content-controls-to-word-documents.md).

> [!NOTE]
> Você pode usar controles de conteúdo somente em documentos que são salvos no formato XML aberto. Você não pode usar controles de conteúdo em documentos que são salvos no formato de documento do Word 97-2003 (*. doc*).

## <a name="types-of-content-controls"></a>Tipos de controles de conteúdo
 Há nove tipos diferentes de controles de conteúdo que você pode adicionar a documentos. A maioria dos controles de conteúdo tem um tipo correspondente no <xref:Microsoft.Office.Tools.Word> namespace. Você também pode usar um genérico <xref:Microsoft.Office.Tools.Word.ContentControl> , que pode representar qualquer um dos controles de conteúdo disponíveis. Para obter instruções que demonstram como usar cada um dos controles de conteúdo disponíveis, consulte [Walkthrough: criar um modelo usando controles de conteúdo](../vsto/walkthrough-creating-a-template-by-using-content-controls.md).

### <a name="build-block-gallery"></a>Galeria de blocos de compilação
 Uma galeria de blocos de construção permite que os usuários selecionem em uma lista de *blocos de construção de documento* para inserir em um documento. Um bloco de construção de documento é uma parte do conteúdo que foi criado para ser usado várias vezes, como uma folha de rosto comum, uma tabela formatada ou um cabeçalho. Para obter mais informações, consulte o <xref:Microsoft.Office.Tools.Word.BuildingBlockGalleryContentControl> tipo. Para obter mais informações sobre blocos de construção, consulte [What ' s New for Developers in Word 2007](/previous-versions/office/developer/office-2007/bb266218(v=office.12)).

### <a name="check-box"></a>Caixa de seleção
 Uma caixa de seleção fornece uma interface do usuário que representa um estado binário: selecionada ou desmarcada.

 Ao contrário dos outros tipos de controles de conteúdo, o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] não fornece um tipo específico que representa um controle de conteúdo de caixa de seleção. Em outras palavras, não há nenhum `CheckBoxContentControl` tipo. No entanto, você ainda pode criar um controle de conteúdo de caixa de seleção adicionando um genérico <xref:Microsoft.Office.Tools.Word.ContentControl> a um documento programaticamente. Para obter mais informações, consulte [controles de conteúdo da caixa de seleção em projetos do Word](#checkbox).

### <a name="combo-box"></a>Caixa de combinação
 Uma caixa de combinação exibe uma lista de itens que os usuários podem selecionar. Ao contrário de uma lista suspensa, a caixa de combinação permite que os usuários adicionem seus próprios itens. Para obter mais informações, consulte o <xref:Microsoft.Office.Tools.Word.ComboBoxContentControl> tipo.

### <a name="date-picker"></a>Seletor de data
 Um seletor de data fornece uma interface do usuário de calendário para selecionar uma data. O calendário é exibido quando o usuário final clica na seta suspensa no controle. Você pode usar calendários regionais e diferentes formatos de data. Para obter mais informações, consulte o <xref:Microsoft.Office.Tools.Word.DatePickerContentControl> tipo.

### <a name="drop-down-list"></a>Lista suspensa
 Uma lista suspensa exibe uma lista de itens que os usuários podem selecionar. Ao contrário de uma caixa de combinação, a lista suspensa não permite que os usuários adicionem ou editem itens. Para obter mais informações, consulte o <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> tipo.

### <a name="group"></a>Grupo
 Um controle de grupo define uma região protegida de um documento que os usuários não podem editar ou excluir. Um controle de grupo pode conter qualquer item de documento, como texto, tabelas, elementos gráficos e outros controles de conteúdo. Para obter mais informações, consulte o <xref:Microsoft.Office.Tools.Word.GroupContentControl> tipo.

### <a name="picture"></a>Picture
 Um controle de imagem exibe uma imagem. Você pode especificar a imagem em tempo de design ou em tempo de execução, ou os usuários podem clicar nesse controle para selecionar uma imagem a ser inserida no documento. Para obter mais informações, consulte o <xref:Microsoft.Office.Tools.Word.PictureContentControl> tipo.

### <a name="rich-text"></a>Rich Text
 Um controle Rich Text contém texto ou outros itens, como tabelas, imagens ou outros controles de conteúdo. Para obter mais informações, consulte o <xref:Microsoft.Office.Tools.Word.RichTextContentControl> tipo.

### <a name="plain-text"></a>Texto sem formatação
 Um controle de texto sem formatação contém texto. Um controle de texto sem formatação não pode conter outros itens, como tabelas, imagens ou outros controles de conteúdo. Além disso, todo o texto em um controle de texto sem formatação tem a mesma formatação. Por exemplo, se você colocar em itálico uma palavra de uma frase que esteja em um controle de texto sem formatação, todo o texto dentro do controle ficará em itálico. Para obter mais informações, consulte o <xref:Microsoft.Office.Tools.Word.PlainTextContentControl> tipo.

### <a name="generic-content-control"></a>Controle de conteúdo genérico
 Um controle de conteúdo genérico é um <xref:Microsoft.Office.Tools.Word.ContentControl> objeto que pode representar qualquer um dos tipos de controles de conteúdo disponíveis. Você pode alterar um <xref:Microsoft.Office.Tools.Word.ContentControl> objeto para se comportar como um tipo diferente de controle de conteúdo usando a <xref:Microsoft.Office.Tools.Word.ContentControl.Type%2A> propriedade. Por exemplo, se você criar um <xref:Microsoft.Office.Tools.Word.ContentControl> objeto que representa um controle de texto sem formatação, poderá alterá-lo em tempo de execução para que ele se comporta como uma caixa de combinação.

 Você pode criar <xref:Microsoft.Office.Tools.Word.ContentControl> objetos somente em tempo de execução, não no tempo de design. Para obter mais informações, consulte [como: adicionar controles de conteúdo a documentos do Word](../vsto/how-to-add-content-controls-to-word-documents.md).

## <a name="common-features-of-content-controls"></a>Recursos comuns de controles de conteúdo
 A maioria dos controles de conteúdo compartilham um conjunto de membros que você pode usar para executar tarefas comuns. A tabela a seguir descreve algumas das tarefas que você pode executar usando esses membros.

|Para esta tarefa:|Faça o seguinte:|
|--------------------|--------------|
|Obter ou definir o texto que é exibido no controle.|Use a propriedade **Text** . **Observação:**  Os <xref:Microsoft.Office.Tools.Word.PictureContentControl> <xref:Microsoft.Office.Tools.Word.ContentControl> tipos e não têm essa propriedade.|
|Obter ou definir o texto temporário que é exibido no controle até que um usuário edite o controle, o controle é preenchido com dados de uma fonte de dados ou o conteúdo do controle é excluído.|Use a propriedade **PlaceholderText** . **Observação:**  O <xref:Microsoft.Office.Tools.Word.PictureContentControl> tipo não tem essa propriedade.|
|Obtém ou define o título que é exibido na borda do controle de conteúdo quando o usuário clica nele.|Use a propriedade **title** .|
|Remover o controle do documento automaticamente depois que o usuário editar o controle. (O texto no controle permanece no documento.)|Use a propriedade **temporária** .|
|Execute o código quando o usuário clicar no controle de conteúdo ou quando o cursor for movido para o controle de conteúdo programaticamente.|Manipule o <xref:Microsoft.Office.Tools.Word.ContentControlBase.Entering> evento do controle.|
|Executar código quando o usuário clicar fora do controle de conteúdo ou quando o cursor for movido para fora do controle de conteúdo programaticamente.|Manipule o <xref:Microsoft.Office.Tools.Word.ContentControlBase.Exiting> evento do controle.|
|Execute o código após o controle de conteúdo ser adicionado ao documento como resultado de uma operação refazer ou desfazer.|Manipule o <xref:Microsoft.Office.Tools.Word.ContentControlBase.Added> evento do controle.|
|Execute o código logo antes que o controle de conteúdo seja excluído do documento.|Manipule o <xref:Microsoft.Office.Tools.Word.ContentControlBase.Deleting> evento do controle.|

## <a name="protect-parts-of-documents-by-using-content-controls"></a><a name="Protection"></a> Proteger partes de documentos usando controles de conteúdo
 Ao proteger uma parte de um documento, você impede que os usuários alterem ou excluam o conteúdo dessa parte do documento. Há várias maneiras pelas quais você pode proteger partes de um documento usando controles de conteúdo.

 Se a área que você deseja proteger estiver dentro de um controle de conteúdo, você poderá usar as propriedades do controle de conteúdo para impedir que os usuários editem ou excluam o controle:

- A propriedade **LockContents** impede que os usuários editem o conteúdo.

- A propriedade **LockContentControl** impede que os usuários excluam o controle.

  Se a área que você deseja proteger não estiver dentro de um controle de conteúdo ou se desejar proteger uma área que contém controles de conteúdo e outros tipos de conteúdo, você poderá colocar a área inteira em um <xref:Microsoft.Office.Tools.Word.GroupContentControl> . Ao contrário de outros controles de conteúdo, um <xref:Microsoft.Office.Tools.Word.GroupContentControl> não fornece nenhuma interface do usuário visível para ele. Sua única finalidade é definir uma região que os usuários não podem editar.

> [!NOTE]
> Se você criar um <xref:Microsoft.Office.Tools.Word.GroupContentControl> que contenha controles de conteúdo inseridos, os controles de conteúdo inserido não serão protegidos automaticamente. Você deve usar a propriedade **LockContents** de cada controle incorporado para impedir que os usuários editem seu conteúdo.

 Para obter mais informações sobre como usar controles de conteúdo para proteger partes de documentos, consulte [como: proteger partes de documentos usando controles de conteúdo](../vsto/how-to-protect-parts-of-documents-by-using-content-controls.md).

## <a name="bind-data-to-content-controls"></a><a name="DataBinding"></a> Associar dados a controles de conteúdo
 Você pode exibir dados em documentos ligando um controle de conteúdo a uma fonte de dados. Quando a fonte de dados é atualizada, o controle de conteúdo reflete as alterações. Você também pode salvar as alterações de volta na fonte de dados.

 Os controles de conteúdo fornecem as seguintes opções de ligação de dados:

- Você pode associar os controles de conteúdo a campos de banco de dados ou objetos gerenciados usando o mesmo modelo de associação aos Windows Forms.

- Você pode associar controles de conteúdo a elementos em pedaços de XML (também chamados de *partes XML personalizadas*) inseridos no documento.

  Para obter uma visão geral da Associação de controles de host em soluções do Office para dados, consulte [associar dados a controles em soluções do Office](../vsto/binding-data-to-controls-in-office-solutions.md).

### <a name="use-the-windows-forms-data-binding-model"></a>Usar o modelo de associação de dados Windows Forms
 A maioria dos controles de conteúdo dá suporte ao modelo de vinculação de dados simples que o Windows Forms usa. Vinculação de dados simples significa que um controle está associado a um único elemento de dados, como um valor em uma coluna de uma tabela de dados. Para obter mais informações, consulte [vinculação de dados e Windows Forms](/dotnet/framework/winforms/data-binding-and-windows-forms).

 Em projetos de nível de documento, você pode associar dados a controles de conteúdo usando a janela **fontes de dados** no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] . Para obter mais informações sobre como adicionar controles de conteúdo vinculados a dados a documentos, consulte [como: popular documentos com dados de um banco](../vsto/how-to-populate-documents-with-data-from-a-database.md) e [como: preencher documentos com dados de objetos](../vsto/how-to-populate-documents-with-data-from-objects.md).

 A tabela a seguir lista os controles de conteúdo que você pode associar a cada tipo de dados na janela **fontes de dados** .

|Tipo de dados|Controle de conteúdo padrão|Outros controles de conteúdo que podem ser associados a este tipo de dados|
|---------------|-----------------------------|----------------------------------------------------------------|
|<xref:System.Boolean><br /><br /> <xref:System.Byte><br /><br /> <xref:System.Char><br /><br /> <xref:System.Double><br /><br /> <xref:System.Enum><br /><br /> <xref:System.Guid><br /><br /> <xref:System.Int16><br /><br /> <xref:System.Int32><br /><br /> <xref:System.Int64><br /><br /> <xref:System.SByte><br /><br /> <xref:System.Single><br /><br /> <xref:System.String><br /><br /> <xref:System.TimeSpan><br /><br /> <xref:System.UInt16><br /><br /> <xref:System.UInt32><br /><br /> <xref:System.UInt64>|<xref:Microsoft.Office.Tools.Word.PlainTextContentControl>|<xref:Microsoft.Office.Tools.Word.BuildingBlockGalleryContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.ComboBoxContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.DatePickerContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.RichTextContentControl>|
|<xref:System.DateTime>|<xref:Microsoft.Office.Tools.Word.DatePickerContentControl>|<xref:Microsoft.Office.Tools.Word.BuildingBlockGalleryContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.ComboBoxContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.PlainTextContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.RichTextContentControl>|
|<xref:System.Drawing.Image><br /><br /> Matriz <xref:System.Byte>|<xref:Microsoft.Office.Tools.Word.PictureContentControl>|Nenhum|

 Em projetos de suplemento no nível de documento e do VSTO, você pode associar um controle de conteúdo a uma fonte de dados programaticamente usando o <xref:System.Windows.Forms.ControlBindingsCollection.Add%2A> método da <xref:System.Windows.Forms.IBindableComponent.DataBindings%2A> Propriedade do controle. Se você fizer isso, passe o **texto** da cadeia de caracteres para o parâmetro *PropertyName* do <xref:System.Windows.Forms.ControlBindingsCollection.Add%2A> método. A propriedade **Text** é a propriedade de associação de dados padrão dos controles de conteúdo.

 Os controles de conteúdo também dão suporte à ligação de dados bidirecional, na qual as alterações no controle são atualizadas para a fonte de dados. Para obter mais informações, consulte [como: atualizar uma fonte de dados com dados de um controle de host](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md).

> [!NOTE]
> Os controles de conteúdo não dão suporte à associação de dados complexa. Se você associar um <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> ou <xref:Microsoft.Office.Tools.Word.ComboBoxContentControl> a uma fonte de dados usando o modelo de dados Windows Forms, os usuários verão apenas um único valor quando clicarem no controle. Se você quiser associar esses controles a um conjunto de valores de dados que os usuários podem escolher, você pode associar esses controles a elementos em uma parte XML personalizada.

### <a name="bind-content-controls-to-custom-xml-parts"></a>Associar controles de conteúdo a partes XML personalizadas
 Você pode associar alguns controles de conteúdo a elementos em partes XML personalizadas que são inseridas no documento. Para obter mais informações sobre partes XML personalizadas, consulte [visão geral de partes XML personalizadas](../vsto/custom-xml-parts-overview.md).

 Para associar um controle de conteúdo a um elemento em uma parte XML personalizada, use a propriedade **XMLMapping** do controle. O exemplo de código a seguir demonstra como associar um <xref:Microsoft.Office.Tools.Word.PlainTextContentControl> ao `Price` elemento sob o `Product` nó em uma parte XML personalizada que já foi adicionada ao documento.

```vb
plainTextContentControl1.XMLMapping.SetMapping("/Product/Price")
```

```csharp
plainTextContentControl1.XMLMapping.SetMapping("/Product/Price", String.Empty, null);
```

 Para obter instruções que demonstram como associar controles de conteúdo a partes XML personalizadas com mais detalhes, consulte [passo a passos: associar controles de conteúdo a partes XML personalizadas](../vsto/walkthrough-binding-content-controls-to-custom-xml-parts.md).

 Quando você associa um controle de conteúdo a uma parte XML personalizada, a ligação de dados bidirecional é habilitada automaticamente. Se um usuário editar texto no controle, os elementos XML correspondentes serão atualizados automaticamente. Da mesma forma, se os valores de elemento nas partes XML personalizadas forem alterados, os controles de conteúdo associados aos elementos XML exibirão os novos dados.

 Você pode associar os seguintes tipos de controles de conteúdo a partes XML personalizadas:

- <xref:Microsoft.Office.Tools.Word.ComboBoxContentControl>

- <xref:Microsoft.Office.Tools.Word.DatePickerContentControl>

- <xref:Microsoft.Office.Tools.Word.DropDownListContentControl>

- <xref:Microsoft.Office.Tools.Word.PictureContentControl>

- <xref:Microsoft.Office.Tools.Word.PlainTextContentControl>

### <a name="data-bind-events-for-content-controls"></a>Eventos de ligação de dados para controles de conteúdo
 Todos os controles de conteúdo fornecem um conjunto de eventos que você pode manipular para executar tarefas relacionadas a dados, como a validação de que o texto em um controle atende a certos critérios antes que a fonte de dados seja atualizada. A tabela a seguir lista os eventos de controle de conteúdo relacionados à vinculação de dados.

|Tarefa|Evento|
|----------|-----------|
|Executar código logo antes que o Word atualize automaticamente o texto em um controle de conteúdo que esteja associado a uma parte XML personalizada.|<xref:Microsoft.Office.Tools.Word.ContentControlBase.ContentUpdating>|
|Execute o código logo antes que o Word atualize automaticamente os dados em uma parte XML personalizada associada a um controle de conteúdo (ou seja, após o texto no controle de conteúdo ser alterado).|<xref:Microsoft.Office.Tools.Word.ContentControlBase.StoreUpdating>|
|Execute seu próprio código para validar o conteúdo do controle de acordo com os critérios personalizados.|<xref:Microsoft.Office.Tools.Word.ContentControlBase.Validating>|
|Execute o código depois que o conteúdo do controle tiver sido validado com êxito.|<xref:Microsoft.Office.Tools.Word.ContentControlBase.Validated>|

## <a name="limitations-of-content-controls"></a>Limitações de controles de conteúdo
 Quando você usa controles de conteúdo em seus projetos do Office, esteja ciente das limitações a seguir.

### <a name="behavior-differences-between-design-time-and-runtime"></a>Diferenças de comportamento entre o tempo de design e o tempo de execução
 Muitas das limitações que Microsoft Office palavras impostas sobre controles de conteúdo em tempo de execução não são impostas em tempo de design. Ao projetar a interface do usuário de uma solução em nível de documento no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] , lembre-se de modificar os controles de conteúdo apenas de maneiras com suporte em tempo de execução.

 Se você modificar um controle de conteúdo em tempo de design de forma que o controle não ofereça suporte em tempo de execução, o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Designer não o alertará sobre as alterações sem suporte. No entanto, quando você depurar ou executar o projeto, ou se salvar e reabrir o projeto, o Word exibirá uma mensagem de erro e solicitará permissão para reparar o documento. Quando você repara o documento, o Word remove todo o conteúdo sem suporte e a formatação do controle.

 Por exemplo, o Word não impede que você adicione uma tabela a um <xref:Microsoft.Office.Tools.Word.PlainTextContentControl> em tempo de design. No entanto, como <xref:Microsoft.Office.Tools.Word.PlainTextContentControl> os objetos não podem conter tabelas em tempo de execução, o Word exibirá uma mensagem de erro quando o documento for aberto.

 Observe também que muitas propriedades que definem o comportamento dos controles de conteúdo não têm nenhum efeito no tempo de design. Por exemplo, se você definir a propriedade **LockContents** de um controle de conteúdo como **true** no tempo de design, ainda poderá editar o texto no controle no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Designer. Essa propriedade só impede que os usuários editem o controle em tempo de execução.

### <a name="event-limitations"></a>Limitações de eventos
 Os controles de conteúdo não fornecem um evento que é gerado quando o usuário altera o texto ou outros itens no controle. Por exemplo, não há evento que é gerado quando um usuário seleciona um item diferente em um <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> ou <xref:Microsoft.Office.Tools.Word.ComboBoxContentControl> .

 Para determinar quando um usuário edita o conteúdo de um controle de conteúdo, você pode associar o controle a uma parte XML personalizada e, em seguida, manipular o <xref:Microsoft.Office.Tools.Word.ContentControlBase.StoreUpdating> evento. Esse evento é gerado quando o usuário altera o conteúdo de um controle associado a uma parte XML personalizada. Para obter instruções que demonstram como associar um controle de conteúdo a uma parte XML personalizada, consulte [passo a passos: associar controles de conteúdo a partes XML personalizadas](../vsto/walkthrough-binding-content-controls-to-custom-xml-parts.md).

### <a name="check-box-content-controls-in-word-projects"></a><a name="checkbox"></a> Controles de conteúdo da caixa de seleção em projetos do Word
 O Word 2010 introduziu um novo tipo de controle de conteúdo que representa uma caixa de seleção. No entanto, o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] não fornece um tipo de CheckBoxContentControl correspondente para você usar em projetos do Office. Para criar um controle de conteúdo de caixa de seleção em um [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] projeto do ou do Word 2010, use o <xref:Microsoft.Office.Tools.Word.ControlCollection.AddContentControl%2A> método para criar um <xref:Microsoft.Office.Tools.Word.ContentControl> objeto e passe o <xref:Microsoft.Office.Interop.Word.WdContentControlType.wdContentControlCheckBox> valor para o método para especificar um controle de conteúdo de caixa de seleção. O exemplo de código a seguir demonstra como fazer isso.

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_contentcontrolreference/checkbox.vb" id="Snippet800":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_wordcontentcontrolreference/checkbox.cs" id="Snippet800":::

## <a name="see-also"></a>Consulte também
- [Automatizar o Word usando objetos estendidos](../vsto/automating-word-by-using-extended-objects.md)
- [Como: adicionar controles de conteúdo a documentos do Word](../vsto/how-to-add-content-controls-to-word-documents.md)
- [Walkthrough: criar um modelo usando controles de conteúdo](../vsto/walkthrough-creating-a-template-by-using-content-controls.md)
- [Dados em soluções do Office](../vsto/data-in-office-solutions.md)
- [Associar dados a controles em soluções do Office](../vsto/binding-data-to-controls-in-office-solutions.md)
- [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
