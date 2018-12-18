---
title: Visão geral da faixa de opções
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- customizing the Ribbon, multiple Ribbons
- Ribbon [Office development in Visual Studio], about Ribbon
- toolbars [Office development in Visual Studio], Ribbon
- Ribbon [Office development in Visual Studio]
- Ribbon [Office development in Visual Studio], multiple Ribbons
- toolbars [Office development in Visual Studio]
- custom Ribbon, multiple Ribbons
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 51de8b5fbc4e21b4dabaf34f526b85f0b98623db
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49846350"
---
# <a name="ribbon-overview"></a>Visão geral da faixa de opções
  A faixa de opções é uma maneira de organizar os comandos relacionados para que eles são mais fáceis de encontrar. Comandos são exibidos como controles da faixa de opções. Controles são organizados em *grupos* ao longo de uma faixa horizontal na borda superior da janela do aplicativo. Grupos relacionados são organizados em guias.  
  
 Agora, a maioria dos recursos que foram acessados por meio de menus e barras de ferramentas em versões anteriores do Microsoft Office system pode ser acessada por meio da faixa de opções. Para obter mais informações, consulte o artigo técnico [visão geral do desenvolvedor da interface do usuário para o 2007 Microsoft Office system](http://go.microsoft.com/fwlink/?LinkID=70860).  
  
 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]  
  
## <a name="customize-the-microsoft-office-ribbon"></a>Personalizar a faixa de opções do Microsoft Office  
 Para personalizar a faixa de opções, adicione um dos seguintes itens de faixa de opções ao seu projeto do Office:  
  
- **Faixa de opções (Visual Designer)**  
  
- **Faixa de opções (XML)**  
  
  Por exemplo, para personalizar a faixa de opções do Excel, adicione um item da faixa de opções para um projeto de suplemento do VSTO do Excel.  
  
### <a name="ribbon-visual-designer-item"></a>Item da faixa de opções (Visual Designer)  
 O **faixa de opções (Visual Designer)** item fornece ferramentas avançadas que tornam mais fácil para você projetar e desenvolver uma faixa de opções personalizada. Use o **faixa de opções (Visual Designer)** item para personalizar a faixa de opções das seguintes maneiras:  
  
- Adicione guias personalizadas ou internas para uma faixa de opções.  
  
- Adicione grupos personalizados a uma guia interna ou personalizada.  
  
  > [!NOTE]  
  >  Uma guia interna ou grupo é aquele que já existe na faixa de opções de um aplicativo do Microsoft Office. Por exemplo, o **dados** guia é uma guia interna no Excel. O **conexões** é um grupo interno sobre o **dados** guia.  
  
- Adicione controles personalizados a um grupo personalizado.  
  
- Adicione controles personalizados para o modo de exibição Backstage.  
  
  Para obter mais informações sobre como personalizar uma faixa de opções usando o **faixa de opções (Visual Designer)** item, consulte [designer de faixa de opções](../vsto/ribbon-designer.md).  
  
### <a name="ribbon-xml-item"></a>Item da faixa de opções (XML)  
 Use o **da faixa de opções (XML)** item se você quiser personalizar a faixa de opções de forma que não é compatível com o **faixa de opções (Visual Designer)** item. Use o **da faixa de opções (XML)** item para personalizar a faixa de opções das seguintes maneiras:  
  
- Adicione *internos* grupos para uma guia personalizada ou uma guia interna.  
  
- Adicione controles internos para um grupo personalizado.  
  
- Adicione código personalizado para substituir os manipuladores de eventos de controles internos.  
  
- Personalize a barra de ferramentas de acesso rápido.  
  
- Compartilhar uma personalização da faixa de opções entre o suplemento do VSTO usando uma ID de qualificado.  
  
  Para obter mais informações sobre como personalizar a faixa de opções usando o **da faixa de opções (XML)** item, consulte [XML da faixa de opções](../vsto/ribbon-xml.md).  
  
## <a name="export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml"></a>Exportar uma faixa de opções do Designer da faixa de opções para o XML da faixa de opções  
 Se você criar uma faixa de opções usando o Designer de faixa de opções e, em seguida, decidir que deseja personalizar a faixa de opções de maneiras que o **faixa de opções (Visual Designer)** item não dá suporte, você pode exportar a faixa de opções para XML.  
  
 Visual Studio cria automaticamente um **da faixa de opções (XML)** de item e preenche o arquivo XML de faixa de opções com elementos e atributos para cada controle na faixa de opções.  
  
 Nem todas as propriedades que estão na **propriedades** janela do Designer da faixa de opções são transferidos para o arquivo XML de faixa de opções.  Por exemplo, o Visual Studio não exporta o valor da **imagem** ou **texto** propriedade. Isso ocorre porque você deve criar um método de retorno de chamada no arquivo de código da faixa de opções do projeto exportado para atribuir uma imagem ou definir o texto de um controle. Visual Studio gera automaticamente os métodos de retorno de chamada como parte do processo de exportação.  
  
 Além disso, quaisquer valores de propriedade padrão inalterado não aparecem no arquivo XML de faixa de opções resultante.  
  
 Para obter mais informações sobre como exportar a faixa de opções para XML, consulte [como: exportar uma faixa de opções do Designer da faixa de opções para o XML da faixa de opções](../vsto/how-to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml.md).  
  
### <a name="update-the-code"></a>Atualize o código  
 Um novo arquivo de código da faixa de opções é adicionado ao **Gerenciador de soluções**. Esse arquivo contém a classe XML da faixa de opções. Você deve criar métodos de retorno de chamada no `Ribbon Callbacks` região dessa classe para manipular ações do usuário, como clicar em um botão. Mover seu código de manipuladores de eventos para esses métodos de retorno de chamada e modifique o código para trabalhar com a extensibilidade da faixa de opções (RibbonX) modelo de programação. Para obter mais informações, consulte [XML da faixa de opções](../vsto/ribbon-xml.md).  
  
 Você também deve adicionar código para o `ThisAddIn`, `ThisWorkbook`, ou `ThisDocument` classe que substitui o `CreateRibbonExtensibilityObject` método e retorna o XML da faixa de opções de classe para o aplicativo do Office.  
  
 Para obter mais informações, consulte [XML da faixa de opções](../vsto/ribbon-xml.md).  
  
## <a name="add-multiple-ribbon-items-to-a-project"></a>Adicionar vários itens de faixa de opções para um projeto  
 Você pode adicionar mais de um item da faixa de opções para um único projeto. Isso é útil se você quiser executar qualquer uma das seguintes tarefas:  
  
-   Criar faixas de opções do Outlook *inspetores*. Para obter mais informações, consulte [personalizar uma faixa de opções para Outlook](../vsto/customizing-a-ribbon-for-outlook.md).  
  
    > [!NOTE]  
    >  Um Inspector é uma janela que é aberta quando os usuários executam determinadas tarefas, como a criação de uma mensagem de email.  
  
-   Selecione quais da faixa de opções para exibir no tempo de execução.  
  
### <a name="select-which-ribbons-to-display-at-runtime"></a>Selecione quais faixas de opções para exibir no tempo de execução  
 Como um projeto pode conter mais de uma faixa de opções, você pode selecionar quais da faixa de opções para exibir no tempo de execução.  
  
 Para selecionar uma faixa de opções para exibir no tempo de execução, substituir os `CreateRibbonExtensibilityObject` método na `ThisAddin`, `ThisWorkbook`, ou `ThisDocument` classe do seu projeto e o retorno de faixa de opções que você deseja exibir. O exemplo a seguir verifica o valor de um campo denominado `myCondition` e retorna a faixa de opções apropriada.  
  
> [!NOTE]  
>  A sintaxe usada neste exemplo retorna uma faixa de opções que foi criada usando o **faixa de opções (Visual Designer)** item. A sintaxe para retornar uma faixa de opções é criada usando um **da faixa de opções (XML)** item é um pouco diferente. Para obter mais informações sobre como retornar um **da faixa de opções (XML)** item, consulte [XML da faixa de opções](../vsto/ribbon-xml.md).  
  
 Adicione o seguinte código:  
  
 [!code-vb[Trin_Ribbon_Choose_Ribbon#1](../vsto/codesnippet/VisualBasic/trin_Ribbon_choose_Ribbon_4/ThisWorkbook.vb#1)]
 [!code-csharp[Trin_Ribbon_Choose_Ribbon#1](../vsto/codesnippet/CSharp/trin_Ribbon_choose_Ribbon_4/ThisWorkbook.cs#1)]  
  
### <a name="related-topics"></a>Tópicos relacionados  
  
|Título|Descrição|  
|-----------|-----------------|  
|[Como: Introdução à personalização da faixa de opções](../vsto/how-to-get-started-customizing-the-ribbon.md)|Mostra como personalizar a faixa de opções de um aplicativo do Microsoft Office, adicione uma **faixa de opções (Visual Designer)** ou **da faixa de opções (XML)** item a um projeto do Office.|  
|[Designer de faixa de opções](../vsto/ribbon-designer.md)|Descreve como você pode usar o Designer de faixa de opções para adicionar guias personalizadas, grupos e controles à faixa de opções de um aplicativo do Microsoft Office.|  
|[Passo a passo: Criar uma guia personalizada usando o Designer de faixa de opções](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)|Mostra como criar uma guia de faixa de opções personalizada usando o Designer de faixa de opções. Você pode usar o Designer de faixa de opções para adicionar e posicionar os controles da guia personalizada.|  
|[Visão geral do modelo de objeto da faixa de opções](../vsto/ribbon-object-model-overview.md)|Fornece uma visão geral do modelo de objeto com rigidez de tipos que você pode usar para obter e definir as propriedades de controles da faixa de opções em tempo de execução.|  
|[Explicação passo a passo: Os controles em uma faixa de opções em tempo de execução de atualização](../vsto/walkthrough-updating-the-controls-on-a-ribbon-at-run-time.md)|Demonstra como usar o modelo de objeto da faixa de opções para atualizar os controles em uma faixa de opções, depois que a faixa de opções é carregada no aplicativo do Office.|  
|[Personalizar uma faixa de opções do Outlook](../vsto/customizing-a-ribbon-for-outlook.md)|Fornece orientação para personalizar a faixa de opções no Microsoft Office Outlook.|  
|[Personalizar uma faixa de opções para InfoPath](../vsto/customizing-a-ribbon-for-infopath.md)|Fornece orientação para personalizar a faixa de opções no Microsoft Office InfoPath.|  
|[Acesso a faixa de opções em tempo de execução](../vsto/accessing-the-ribbon-at-run-time.md)|Mostra como mostrar, ocultar e modificar a faixa de opções e permitir que os usuários executar o código de controles em um painel de tarefas personalizado, o painel de ações ou a região de formulário do Outlook.|  
|[Como: alterar a posição de uma guia na faixa de opções](../vsto/how-to-change-the-position-of-a-tab-on-the-ribbon.md)|Mostra como alterar a ordem das guias em uma faixa de opções.|  
|[Como: personalizar uma guia interna](../vsto/how-to-customize-a-built-in-tab.md)|Mostra como adicionar grupos e controles a uma guia interna.|  
|[Como: adicionar controles ao modo de exibição Backstage](../vsto/how-to-add-controls-to-the-backstage-view.md)|Mostra como adicionar controles ao menu que é aberta quando você clica o **arquivo**.|  
|[Como: adicionar um iniciador da caixa de diálogo a um grupo de faixa de opções](../vsto/how-to-add-a-dialog-box-launcher-to-a-ribbon-group.md)|Mostra para adicionar um iniciador da caixa de diálogo a qualquer grupo em uma faixa de opções.|  
|[Como: exportar uma faixa de opções do Designer da faixa de opções para o XML da faixa de opções](../vsto/how-to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml.md)|Mostra como personalizar a faixa de opções de maneiras avançadas exportando a faixa de opções do designer para XML da faixa de opções.|  
|[XML da faixa de opções](../vsto/ribbon-xml.md)|Explica como você pode personalizar uma faixa de opções usando XML da faixa de opções.|  
|[Passo a passo: Criar uma guia personalizada usando o Designer de faixa de opções](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)|Demonstra como criar uma guia de faixa de opções personalizada usando o **da faixa de opções (XML)** item.|  
  
  