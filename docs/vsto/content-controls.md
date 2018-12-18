---
title: Controles de conteúdo
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
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
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 924f31ac38219453ae96fd573d968b18ce19c913
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50672893"
---
# <a name="content-controls"></a>Controles de conteúdo
  Controles de conteúdo fornecem uma maneira para você aos documentos de design e modelos que têm esses recursos:  
  
- Uma interface de usuário (IU) que tem uma entrada controlada como um formulário.  
  
- Restrições que impedem que os usuários editem seções protegidas do documento ou modelo. Para obter mais informações, consulte [proteger partes de documentos usando controles de conteúdo](#Protection).  
  
- Associação de dados para uma fonte de dados. Para obter mais informações, consulte [associar dados a controles de conteúdo](#DataBinding).  
  
  [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]  
  
  ![link para vídeo](../vsto/media/playvideo.gif "link para vídeo") para uma demonstração em vídeo relacionada, consulte [usando o Visual Studio Tools para o Office system (3.0) de controles de conteúdo de associar dados ao Word 2007](http://go.microsoft.com/fwlink/?LinkId=136785).  
  
## <a name="overview-of-content-controls"></a>Visão geral dos controles de conteúdo  
 Controles de conteúdo fornecem uma interface do usuário que é otimizado para ambos os usuário de entrada e de impressão. Quando você adiciona um controle de conteúdo a um documento, o controle é identificado por uma borda, um título e texto temporário que pode fornecer instruções ao usuário. A borda e o título do controle não aparecem nas versões impressas do documento.  
  
 Por exemplo, se você quiser que o usuário insira uma data em uma seção do documento, você pode adicionar um controle de conteúdo de seletor de data para o documento. Quando os usuários clicam no controle, o seletor de data padrão da interface do usuário é exibida. Você também pode definir propriedades do controle para definir o calendário regional que é exibido e especificar o formato de data. Depois que o usuário escolhe uma data, a interface do usuário do controle está oculto e somente a data é exibida se o usuário imprime o documento.  
  
 Controles de conteúdo também ajudam você a fazer o seguinte:  
  
- Impedir que usuários editando ou excluindo partes de um documento. Isso é útil se você tiver informações em um documento ou modelo que os usuários devem ser capazes de ler, mas não editar, ou se você quiser que os usuários possam editar controles de conteúdo, mas não excluí-los.  
  
- Associe partes de um documento ou modelo de dados. Você pode associar controles de conteúdo para os campos de banco de dados, objetos gerenciados no [!INCLUDE[dnprdnshort](../sharepoint/includes/dnprdnshort-md.md)], elementos XML que são armazenados no documento e outras fontes de dados.  
  
  Em projetos de nível de documento, você pode adicionar controles de conteúdo ao documento em tempo de design ou em tempo de execução. Em projetos de suplemento do VSTO, você pode adicionar controles de conteúdo para qualquer documento aberto no tempo de execução. Para obter mais informações, consulte [como: adicionar controles content a documentos do Word](../vsto/how-to-add-content-controls-to-word-documents.md).  
  
> [!NOTE]  
>  Você pode usar controles de conteúdo somente em documentos que são salvos no formato Open XML. Você não pode usar controles de conteúdo em documentos que são salvas no documento do Word 97-2003 (*. doc*) formato.  
  
## <a name="types-of-content-controls"></a>Tipos de controles de conteúdo  
 Há nove tipos diferentes de controles de conteúdo que você pode adicionar aos documentos. A maioria dos controles de conteúdo tem um tipo correspondente <xref:Microsoft.Office.Tools.Word> namespace. Você também pode usar um genérico <xref:Microsoft.Office.Tools.Word.ContentControl>, que pode representar qualquer um dos controles de conteúdo disponíveis. Para um passo a passo que demonstra como usar cada um dos controles de conteúdo disponíveis, consulte [instruções passo a passo: criar um modelo usando os controles de conteúdo](../vsto/walkthrough-creating-a-template-by-using-content-controls.md).  
  
### <a name="build-block-gallery"></a>Criar galeria de blocos  
 Uma galeria de blocos de construção permite que os usuários selecionem de uma lista dos *blocos de construção de documento* para inserir em um documento. Um bloco de construção de documento é uma parte do conteúdo que foi criado para ser usada várias vezes, como um cabeçalho, uma tabela formatada ou uma folha de rosto comuns. Para obter mais informações, consulte o <xref:Microsoft.Office.Tools.Word.BuildingBlockGalleryContentControl> tipo. Para obter mais informações sobre blocos de construção, consulte [quais são as novidades para desenvolvedores no Word 2007](/previous-versions/office/developer/office-2007/bb266218(v=office.12)).  
  
### <a name="check-box"></a>Caixa de seleção  
 Uma caixa de seleção fornece uma interface do usuário que representa um estado binário: marcada ou desmarcada.  
  
 Ao contrário de outros tipos de controles de conteúdo, o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] não fornece um tipo específico que representa um controle de conteúdo da caixa de seleção. Em outras palavras, não há nenhum `CheckBoxContentControl` tipo. No entanto, você ainda pode criar um controle de conteúdo da caixa de seleção, adicionando um genérico <xref:Microsoft.Office.Tools.Word.ContentControl> a um documento por meio de programação. Para obter mais informações, consulte [controles de conteúdo da caixa de seleção em projetos do Word](#checkbox).  
  
### <a name="combo-box"></a>Caixa de combinação  
 Uma caixa de combinação exibe uma lista de itens que os usuários podem selecionar. Ao contrário de uma lista suspensa, caixa de combinação permite que os usuários adicionem seus próprios itens. Para obter mais informações, consulte o <xref:Microsoft.Office.Tools.Word.ComboBoxContentControl> tipo.  
  
### <a name="date-picker"></a>seletor de data  
 Um seletor de data fornece um interface do usuário de calendário para selecionar uma data. O calendário é exibido quando o usuário final clica na seta suspensa no controle. Você pode usar regionais calendários e formatos de data diferentes. Para obter mais informações, consulte o <xref:Microsoft.Office.Tools.Word.DatePickerContentControl> tipo.  
  
### <a name="drop-down-list"></a>Lista suspensa  
 Uma lista suspensa exibe uma lista de itens que os usuários podem selecionar. Ao contrário de uma caixa de combinação, a lista suspensa não permite que os usuários adicionar ou editar itens. Para obter mais informações, consulte o <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> tipo.  
  
### <a name="group"></a>Grupo  
 Um controle de grupo define uma região protegida de um documento que os usuários não podem editar ou excluir. Um controle de grupo pode conter qualquer item do documento, como texto, tabelas, gráficos e outros controles de conteúdo. Para obter mais informações, consulte o <xref:Microsoft.Office.Tools.Word.GroupContentControl> tipo.  
  
### <a name="picture"></a>Imagem  
 Um controle de imagem exibe uma imagem. Você pode especificar a imagem em tempo de design ou tempo de execução, ou os usuários podem clicar nesse controle para selecionar uma imagem a ser inserido no documento. Para obter mais informações, consulte o <xref:Microsoft.Office.Tools.Word.PictureContentControl> tipo.  
  
### <a name="rich-text"></a>Texto rico  
 Um controle rich text contém texto ou outros itens, como tabelas, imagens ou outros controles de conteúdo. Para obter mais informações, consulte o <xref:Microsoft.Office.Tools.Word.RichTextContentControl> tipo.  
  
### <a name="plain-text"></a>Texto sem formatação  
 Um controle de texto sem formatação contém texto. Um controle de texto sem formatação não pode conter outros itens, como tabelas, imagens ou outros controles de conteúdo. Além disso, todo o texto em um controle de texto sem formatação tem a mesma formatação. Por exemplo, se você aplicar itálico uma palavra de uma sentença que está em um controle de texto sem formatação, todo o texto dentro do controle está em itálico. Para obter mais informações, consulte o <xref:Microsoft.Office.Tools.Word.PlainTextContentControl> tipo.  
  
### <a name="generic-content-control"></a>Controle de conteúdo genérico  
 Um controle de conteúdo genérico é um <xref:Microsoft.Office.Tools.Word.ContentControl> objeto que pode representar qualquer um dos tipos de controles de conteúdo disponíveis. Você pode alterar uma <xref:Microsoft.Office.Tools.Word.ContentControl> objeto se comportar como um tipo diferente de controle de conteúdo usando o <xref:Microsoft.Office.Tools.Word.ContentControl.Type%2A> propriedade. Por exemplo, se você criar um <xref:Microsoft.Office.Tools.Word.ContentControl> do objeto que representa o controle de um texto sem formatação, você pode alterá-lo em tempo de execução para que ele se comporta como uma caixa de combinação.  
  
 Você pode criar <xref:Microsoft.Office.Tools.Word.ContentControl> objetos somente no tempo de execução, não em tempo de design. Para obter mais informações, consulte [como: adicionar controles content a documentos do Word](../vsto/how-to-add-content-controls-to-word-documents.md).  
  
## <a name="common-features-of-content-controls"></a>Recursos comuns de controles de conteúdo  
 Controles de conteúdo mais compartilham um conjunto de membros que você pode usar para executar tarefas comuns. A tabela a seguir descreve algumas das tarefas que podem ser executadas com o uso desses membros.  
  
|Para essa tarefa:|Faça o seguinte:|  
|--------------------|--------------|  
|Obtém ou define o texto que é exibido no controle.|Use o **texto** propriedade. **Observação:** as <xref:Microsoft.Office.Tools.Word.PictureContentControl> e <xref:Microsoft.Office.Tools.Word.ContentControl> tipos não têm essa propriedade.|  
|Obtém ou define o texto temporário que é exibido no controle até que um usuário edita o controle, o controle é preenchido com dados de uma fonte de dados ou o conteúdo do controle é excluído.|Use o **PlaceholderText** propriedade. **Observação:** o <xref:Microsoft.Office.Tools.Word.PictureContentControl> tipo não tem essa propriedade.|  
|Obtém ou define o título exibido na borda do controle de conteúdo quando o usuário clica nele.|Use o **título** propriedade.|  
|Remova o controle de documento automaticamente depois que o usuário edita o controle. (O texto no controle permanece no documento.)|Use o **temporário** propriedade.|  
|Execute código quando o usuário clica no controle de conteúdo, ou quando o cursor é movido programaticamente para o controle de conteúdo.|Manipular o <xref:Microsoft.Office.Tools.Word.ContentControlBase.Entering> evento do controle.|  
|Execute código quando o usuário clica fora do controle de conteúdo, ou quando o cursor é movido programaticamente fora do controle de conteúdo.|Manipular o <xref:Microsoft.Office.Tools.Word.ContentControlBase.Exiting> evento do controle.|  
|Executar código após o controle de conteúdo é adicionado ao documento como resultado de uma operação de refazer ou desfazer a operação.|Manipular o <xref:Microsoft.Office.Tools.Word.ContentControlBase.Added> evento do controle.|  
|Execute código antes do controle de conteúdo é excluído do documento.|Manipular o <xref:Microsoft.Office.Tools.Word.ContentControlBase.Deleting> evento do controle.|  
  
##  <a name="Protection"></a> Proteger partes de documentos usando controles de conteúdo  
 Quando você protege uma parte de um documento, você impedir usuários de alterar ou excluir o conteúdo nessa parte do documento. Há várias maneiras que você pode proteger partes de um documento usando controles de conteúdo.  
  
 Se a área que você deseja proteger estiver dentro de um controle de conteúdo, você pode usar as propriedades do controle de conteúdo para impedir que os usuários de editar ou excluir o controle:  
  
- O **LockContents** propriedade impede que os usuários editem o conteúdo.  
  
- O **LockContentControl** propriedade impede que os usuários a exclusão do controle.  
  
  Se a área que você deseja proteger não está dentro de um controle de conteúdo, ou se você quiser proteger uma área que contém controles de conteúdo e outros tipos de conteúdo, você pode colocar toda a área em um <xref:Microsoft.Office.Tools.Word.GroupContentControl>. Ao contrário de outros controles de conteúdo, um <xref:Microsoft.Office.Tools.Word.GroupContentControl> não fornece nenhuma interface do usuário que é visível para o usuário. Sua única finalidade é definir uma região que os usuários não podem editar.  
  
> [!NOTE]  
>  Se você criar um <xref:Microsoft.Office.Tools.Word.GroupContentControl> que contém os controles de conteúdo incorporados, os controles de conteúdo inseridos não são protegidos automaticamente. Você deve usar o **LockContents** incorporado de propriedade de cada controle para impedir que usuários editem seu conteúdo.  
  
 Para obter mais informações sobre como usar controles de conteúdo para proteger partes de documentos, consulte [como: proteger partes de documentos usando controles de conteúdo](../vsto/how-to-protect-parts-of-documents-by-using-content-controls.md).  
  
##  <a name="DataBinding"></a> Associar dados a controles de conteúdo  
 Você pode exibir dados em documentos, associando um controle de conteúdo a uma fonte de dados. Quando a fonte de dados é atualizada, o controle de conteúdo reflete as alterações. Você também pode salvar as alterações de volta para a fonte de dados.  
  
 Controles de conteúdo fornecem as seguintes opções de associação de dados:  
  
- Você pode associar controles de conteúdo aos campos de banco de dados ou objetos gerenciados, usando o mesmo modelo de associação de dados como o Windows Forms.  
  
- Você pode associar controles de conteúdo a elementos em partes de XML (também denominada *partes XML personalizadas*) que são inseridos no documento.  
  
  Para uma visão geral de associar controles de host em soluções do Office a dados, consulte [ligar dados a controles em soluções do Office](../vsto/binding-data-to-controls-in-office-solutions.md).  
  
### <a name="use-the-windows-forms-data-binding-model"></a>Use o modelo de vinculação de dados do Windows Forms  
 Suportam a controles de conteúdo mais o modelo de vinculação de dados simples que usa o Windows Forms. Associação de dados simples significa que um controle é associado a um elemento de dados, como um valor em uma coluna de uma tabela de dados. Para obter mais informações, consulte [vinculação de dados e o Windows Forms](/dotnet/framework/winforms/data-binding-and-windows-forms).  
  
 Em projetos de nível de documento, você pode associar dados a controles de conteúdo usando o **fontes de dados** janela no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]. Para obter mais informações sobre como adicionar controles de conteúdo associado a dados a documentos, consulte [como: preencher documentos com dados de um banco de dados](../vsto/how-to-populate-documents-with-data-from-a-database.md) e [como: preencher documentos com dados de objetos](../vsto/how-to-populate-documents-with-data-from-objects.md).  
  
 A tabela a seguir lista os controles de conteúdo que você pode associar a cada tipo de dados do **fontes de dados** janela.  
  
|Tipo de dados|Controle de conteúdo padrão|Outros controles de conteúdo que podem ser associados a esse tipo de dados|  
|---------------|-----------------------------|----------------------------------------------------------------|  
|<xref:System.Boolean><br /><br /> <xref:System.Byte><br /><br /> <xref:System.Char><br /><br /> <xref:System.Double><br /><br /> <xref:System.Enum><br /><br /> <xref:System.Guid><br /><br /> <xref:System.Int16><br /><br /> <xref:System.Int32><br /><br /> <xref:System.Int64><br /><br /> <xref:System.SByte><br /><br /> <xref:System.Single><br /><br /> <xref:System.String><br /><br /> <xref:System.TimeSpan><br /><br /> <xref:System.UInt16><br /><br /> <xref:System.UInt32><br /><br /> <xref:System.UInt64>|<xref:Microsoft.Office.Tools.Word.PlainTextContentControl>|<xref:Microsoft.Office.Tools.Word.BuildingBlockGalleryContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.ComboBoxContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.DatePickerContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.RichTextContentControl>|  
|<xref:System.DateTime>|<xref:Microsoft.Office.Tools.Word.DatePickerContentControl>|<xref:Microsoft.Office.Tools.Word.BuildingBlockGalleryContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.ComboBoxContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.PlainTextContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.RichTextContentControl>|  
|<xref:System.Drawing.Image><br /><br /> Matriz <xref:System.Byte>|<xref:Microsoft.Office.Tools.Word.PictureContentControl>|Nenhum|  
  
 No nível de documento e projetos de suplemento do VSTO, você pode associar um controle de conteúdo a uma fonte de dados programaticamente, usando o <xref:System.Windows.Forms.ControlBindingsCollection.Add%2A> método da <xref:System.Windows.Forms.IBindableComponent.DataBindings%2A> propriedade do controle. Se você fizer isso, passe a cadeia de caracteres **texto** para o *propertyName* parâmetro do <xref:System.Windows.Forms.ControlBindingsCollection.Add%2A> método. O **texto** propriedade é a propriedade de associação de dados padrão de controles de conteúdo.  
  
 Controles de conteúdo também dão suporte a associação de dados bidirecional, em que as alterações no controle são atualizadas para a fonte de dados. Para obter mais informações, consulte [como: atualizar uma fonte de dados com dados de um controle de host](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md).  
  
> [!NOTE]  
>  Controles de conteúdo não dão suporte a vinculação de dados complexos. Se você associar um <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> ou <xref:Microsoft.Office.Tools.Word.ComboBoxContentControl> a uma fonte de dados usando o modelo de dados do Windows Forms, os usuários verão apenas um único valor quando eles clicam no controle. Se você quiser vincular esses controles a um conjunto de valores de dados que os usuários podem escolher, você pode vincular esses controles aos elementos em uma parte XML personalizada.  
  
### <a name="bind-content-controls-to-custom-xml-parts"></a>Associar controles de conteúdo a partes XML personalizadas  
 Você pode associar alguns controles de conteúdo a elementos em partes XML personalizadas que são inseridos no documento. Para obter mais informações sobre partes XML personalizadas, consulte [visão geral de partes XML personalizadas](../vsto/custom-xml-parts-overview.md).  
  
 Para associar um controle de conteúdo para um elemento em uma parte XML personalizada, use o **XMLMapping** propriedade do controle. O exemplo de código a seguir demonstra como associar um <xref:Microsoft.Office.Tools.Word.PlainTextContentControl> para o `Price` elemento sob o `Product` nó em uma parte XML personalizada que já foi adicionada ao documento.  
  
```vb  
plainTextContentControl1.XMLMapping.SetMapping("/Product/Price")  
```  
  
```csharp  
plainTextContentControl1.XMLMapping.SetMapping("/Product/Price", String.Empty, null);  
```  
  
 Para um passo a passo que demonstra como associar controles de conteúdo a partes XML personalizadas em mais detalhes, consulte [instruções passo a passo: associar controles de conteúdo a partes XML personalizadas](../vsto/walkthrough-binding-content-controls-to-custom-xml-parts.md).  
  
 Quando você associa um controle de conteúdo para uma parte XML personalizada, associação de dados bidirecional é habilitada automaticamente. Se um usuário edita o texto do controle, os elementos XML correspondentes são atualizados automaticamente. Da mesma forma, se os valores de elemento em que as partes XML personalizadas são alterados, os controles de conteúdo que são associados aos elementos XML exibirá os novos dados.  
  
 Você pode vincular os seguintes tipos de controles de conteúdo a partes XML personalizadas:  
  
-   <xref:Microsoft.Office.Tools.Word.ComboBoxContentControl>  
  
-   <xref:Microsoft.Office.Tools.Word.DatePickerContentControl>  
  
-   <xref:Microsoft.Office.Tools.Word.DropDownListContentControl>  
  
-   <xref:Microsoft.Office.Tools.Word.PictureContentControl>  
  
-   <xref:Microsoft.Office.Tools.Word.PlainTextContentControl>  
  
### <a name="data-bind-events-for-content-controls"></a>Associar dados de eventos para controles de conteúdo  
 Todos os controles de conteúdo fornecem um conjunto de eventos que você pode manipular para executar tarefas relacionadas a dados, como validar que o texto em um controle atende a certos critérios antes de atualizar a fonte de dados. A tabela a seguir lista os eventos de controle de conteúdo relacionados à associação de dados.  
  
|Tarefa|evento|  
|----------|-----------|  
|Execute código antes que o Word automaticamente atualiza o texto em um controle de conteúdo que está associado a uma parte XML personalizada.|<xref:Microsoft.Office.Tools.Word.ContentControlBase.ContentUpdating>|  
|Executar código imediatamente antes que o Word atualiza automaticamente os dados em uma parte XML personalizada que está associado a um conteúdo de controle (ou seja, depois que o texto no controle de conteúdo é alterado).|<xref:Microsoft.Office.Tools.Word.ContentControlBase.StoreUpdating>|  
|Execute seu próprio código para validar o conteúdo do controle de acordo com critérios personalizados.|<xref:Microsoft.Office.Tools.Word.ContentControlBase.Validating>|  
|Execute código depois que o conteúdo do controle foi validado com êxito.|<xref:Microsoft.Office.Tools.Word.ContentControlBase.Validated>|  
  
## <a name="limitations-of-content-controls"></a>Limitações de controles de conteúdo  
 Ao usar controles de conteúdo em seus projetos do Office, esteja ciente das limitações a seguir.  
  
### <a name="behavior-differences-between-design-time-and-runtime"></a>Diferenças de comportamento entre o tempo de design e tempo de execução  
 Muitas das limitações que o Microsoft Office Word impõe em controles de conteúdo em tempo de execução não são impostas em tempo de design. Ao projetar a interface do usuário de uma solução de nível de documento em [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)], certifique-se de modificar controles de conteúdo somente de maneiras que têm suporte em tempo de execução.  
  
 Se você modificar um controle de conteúdo em tempo de design de forma que o controle não dá suporte em tempo de execução, o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] designer não alertará você sobre as alterações sem suporte. No entanto, quando você depura ou executa o projeto, ou se você salvar e, em seguida, reabra o projeto, o Word exibirá um erro mensagem e solicite permissão para reparar o documento. Quando você repara o documento, o Word remove conteúdo tudo sem suporte e a formatação do controle.  
  
 Por exemplo, palavra não impede que você adicionar uma tabela para um <xref:Microsoft.Office.Tools.Word.PlainTextContentControl> em tempo de design. No entanto, porque <xref:Microsoft.Office.Tools.Word.PlainTextContentControl> objetos não podem conter tabelas em tempo de execução, o Word exibirá uma mensagem de erro quando o documento é aberto.  
  
 Observe também que muitas propriedades que definem o comportamento de controles de conteúdo não têm nenhum efeito em tempo de design. Por exemplo, se você definir o **LockContents** propriedade de um controle de conteúdo **verdadeiro** em tempo de design, você ainda pode editar o texto do controle no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] designer. Essa propriedade só impede que os usuários o controle de edição em tempo de execução.  
  
### <a name="event-limitations"></a>Limitações de evento  
 Controles de conteúdo não fornecem um evento que é gerado quando o usuário altera o texto ou outros itens no controle. Por exemplo, não há nenhum evento que é gerado quando um usuário seleciona um item diferente em uma <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> ou <xref:Microsoft.Office.Tools.Word.ComboBoxContentControl>.  
  
 Para determinar quando um usuário edita o conteúdo de um controle de conteúdo, você pode associar o controle a uma parte XML personalizada e, em seguida, manipular o <xref:Microsoft.Office.Tools.Word.ContentControlBase.StoreUpdating> eventos. Esse evento é gerado quando o usuário altera o conteúdo de um controle que está associado a uma parte XML personalizada. Para um passo a passo que demonstra como associar um controle de conteúdo a uma parte XML personalizada, consulte [instruções passo a passo: associar controles de conteúdo a partes XML personalizadas](../vsto/walkthrough-binding-content-controls-to-custom-xml-parts.md).  
  
###  <a name="checkbox"></a> Controles de conteúdo da caixa de seleção em projetos do Word  
 Word 2010 introduziu um novo tipo de controle de conteúdo que representa uma caixa de seleção. No entanto, o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] não fornece um tipo correspondente de CheckBoxContentControl para uso em projetos do Office. Para criar um controle de caixa de seleção de conteúdo em um [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] ou um projeto do Word 2010, use o <xref:Microsoft.Office.Tools.Word.ControlCollection.AddContentControl%2A> método para criar um <xref:Microsoft.Office.Tools.Word.ContentControl> do objeto e passe o <xref:Microsoft.Office.Interop.Word.WdContentControlType.wdContentControlCheckBox> valor para o método para especificar um controle de conteúdo da caixa de seleção. O exemplo de código a seguir demonstra como fazer isso.  
  
 [!code-vb[Trin_ContentControlReference#800](../vsto/codesnippet/VisualBasic/trin_contentcontrolreference/checkbox.vb#800)]
 [!code-csharp[Trin_ContentControlReference#800](../vsto/codesnippet/CSharp/trin_wordcontentcontrolreference/checkbox.cs#800)]  
  
## <a name="see-also"></a>Consulte também  
 [Automatizar o Word usando objetos estendidos](../vsto/automating-word-by-using-extended-objects.md)   
 [Como: adicionar controles content a documentos do Word](../vsto/how-to-add-content-controls-to-word-documents.md)   
 [Passo a passo: Criar um modelo usando os controles de conteúdo](../vsto/walkthrough-creating-a-template-by-using-content-controls.md)   
 [Dados em soluções do Office](../vsto/data-in-office-solutions.md)   
 [Associar dados a controles em soluções do Office](../vsto/binding-data-to-controls-in-office-solutions.md)   
 [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)  
