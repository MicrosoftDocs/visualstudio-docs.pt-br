---
title: Visão geral da faixa de faixas
description: Saiba como a faixa de opção é uma maneira de organizar comandos relacionados para que eles sejam mais fáceis de localizar e como os comandos aparecem como controles na faixa de opção.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
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
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 8920c8a402b4566cf95bb74626171cca833d32de
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825544"
---
# <a name="ribbon-overview"></a>Visão geral da faixa de faixas
  A faixa de opção é uma maneira de organizar comandos relacionados para que eles sejam mais fáceis de localizar. Os comandos aparecem como controles na faixa de faixas. Os controles são organizados em *grupos* ao longo de uma faixa horizontal na borda superior de uma janela de aplicativo. Os grupos relacionados são organizados em guias.

 A maioria dos recursos que foram acessados usando menus e barras de ferramentas em versões anteriores do sistema de Microsoft Office agora pode ser acessada usando a faixa de faixas. Para obter mais informações, consulte o artigo técnico [visão geral do desenvolvedor da interface do usuário para o sistema de Microsoft Office de 2007](/previous-versions/office/developer/office-2007/aa338198(v=office.12)).

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

## <a name="customize-the-microsoft-office-ribbon"></a>Personalizar a faixa de Microsoft Office
 Para personalizar a faixa de opções, adicione um dos seguintes itens da faixa para o seu projeto do Office:

- **Faixa de visualização (Visual Designer)**

- **Faixa de Ribbon (XML)**

  Por exemplo, para personalizar a faixa de bits do Excel, adicione um item da faixa de medida a um projeto de suplemento do VSTO do Excel.

### <a name="ribbon-visual-designer-item"></a>Item da faixa de visualização (Visual Designer)
 O item **da faixa de visão (Visual Designer)** fornece ferramentas avançadas que facilitam o design e o desenvolvimento de uma faixa de Ribbon personalizada. Use o item **Ribbon (Visual Designer)** para personalizar a faixa de opções das seguintes maneiras:

- Adicione guias personalizadas ou internas a uma faixa de faixas.

- Adicione grupos personalizados a uma guia personalizada ou interna.

  > [!NOTE]
  > Uma guia ou grupo interno é aquele que já existe na faixa de bits de um aplicativo Microsoft Office. Por exemplo, a guia **dados** é uma guia interna no Excel. O grupo de **conexões** é um grupo interno na guia **dados** .

- Adicione controles personalizados a um grupo personalizado.

- Adicione controles personalizados à exibição de Backstage.

  Para obter mais informações sobre como personalizar uma faixa de faixas usando o item **Ribbon (Visual Designer)** , consulte [Designer de faixa](../vsto/ribbon-designer.md)de das.

### <a name="ribbon-xml-item"></a>Item da faixa (XML)
 Use o item **da faixa de opção (XML)** se desejar personalizar a faixa de uma forma que não seja suportada pelo item da faixa de opção **(Visual Designer)** . Use o item **da faixa de opções (XML)** para personalizar o Ribbon das seguintes maneiras:

- Adicione grupos *internos* a uma guia personalizada ou a uma guia interna.

- Adicione controles internos a um grupo personalizado.

- Adicione um código personalizado para substituir os manipuladores de eventos de controles internos.

- Personalize a barra de ferramentas de acesso rápido.

- Compartilhe uma personalização da faixa de bits entre o suplemento do VSTO usando uma ID qualificada.

  Para obter mais informações sobre como personalizar a faixa de faixas usando o item da faixa de visualização **(XML)** , consulte [XML da faixa](../vsto/ribbon-xml.md)de informações.

## <a name="export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml"></a>Exportar uma faixa de faixas do designer de faixa de das para XML da faixa de das
 Se você criar uma faixa de opções usando o designer de faixa e, em seguida, decidir que deseja personalizar o Ribbon de maneiras que o item **da faixa de opções (Visual Designer)** não oferece suporte, você poderá exportar a faixa para XML.

 O Visual Studio cria automaticamente um item **da faixa de visualização (XML)** e popula o arquivo XML da faixa de da Ribbon com elementos e atributos para cada controle na faixa de faixas.

 Nem todas as propriedades que estão na janela **Propriedades** do designer de faixa de faixas são transferidas para o arquivo XML da faixa de faixas.  Por exemplo, o Visual Studio não exporta o valor da **imagem** ou da propriedade de **texto** . Isso ocorre porque você deve criar um método de retorno de chamada no arquivo de código da faixa de medida do projeto exportado para atribuir uma imagem ou definir o texto de um controle. O Visual Studio não gera automaticamente métodos de retorno de chamada como parte do processo de exportação.

 Além disso, quaisquer valores de propriedade padrão inalterados não aparecem no arquivo XML da faixa de resultados resultante.

 Para obter mais informações sobre como exportar a faixa de faixas para o XML, consulte [como exportar uma faixa de forma do designer de faixa de das para XML da faixa de para](../vsto/how-to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml.md).

### <a name="update-the-code"></a>Atualizar o código
 Um novo arquivo de código da faixa de medida é adicionado ao **Gerenciador de soluções**. Esse arquivo contém a classe XML da faixa de faixas. Você deve criar métodos de retorno de chamada na `Ribbon Callbacks` região dessa classe para tratar as ações do usuário, como clicar em um botão. Mova seu código dos manipuladores de eventos para esses métodos de retorno de chamada e modifique o código para trabalhar com o modelo de programação do RibbonX (extensibilidade de faixa de medida). Para obter mais informações, consulte [Ribbon XML](../vsto/ribbon-xml.md).

 Você também deve adicionar o código à `ThisAddIn` `ThisWorkbook` classe, ou `ThisDocument` que substitui o `CreateRibbonExtensibilityObject` método e retorna a classe XML da faixa de forma para o aplicativo do Office.

 Para obter mais informações, consulte [Ribbon XML](../vsto/ribbon-xml.md).

## <a name="add-multiple-ribbon-items-to-a-project"></a>Adicionar vários itens da faixa de faixas a um projeto
 Você pode adicionar mais de um item da faixa de faixas a um único projeto. Isso será útil se você quiser executar uma das duas tarefas a seguir:

- Crie faixas de faixa para *inspetores* do Outlook. Para obter mais informações, consulte [personalizar uma faixa de visualização para o Outlook](../vsto/customizing-a-ribbon-for-outlook.md).

    > [!NOTE]
    > Um inspetor é uma janela que é aberta quando os usuários executam determinadas tarefas, como a criação de uma mensagem de email.

- Selecione a faixa de opções a ser exibida em tempo de execução.

### <a name="select-which-ribbons-to-display-at-run-time"></a>Selecione quais faixas de opções exibir em tempo de execução
 Como um projeto pode conter mais de uma faixa de opções, você pode selecionar qual faixa de opções exibir em tempo de execução.

 Para selecionar uma faixa de opções a ser exibida em tempo de execução, substitua o `CreateRibbonExtensibilityObject` método na `ThisAddin` `ThisWorkbook` classe, ou `ThisDocument` do seu projeto e retorne a faixa de opções que você deseja exibir. O exemplo a seguir verifica o valor de um campo chamado `myCondition` e retorna a faixa de opções apropriada.

> [!NOTE]
> A sintaxe usada neste exemplo retorna uma faixa de faixas que foi criada usando o item da **faixa de visualização (Visual Designer)** . A sintaxe para retornar uma faixa de forma que é criada usando um item **da faixa (XML)** é ligeiramente diferente. Para obter mais informações sobre como retornar um item **da faixa de forma (XML)** , consulte [XML da faixa](../vsto/ribbon-xml.md)de visualização.

 Adicione os códigos a seguir:

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_Ribbon_choose_Ribbon_4/ThisWorkbook.vb" id="Snippet1":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_Ribbon_choose_Ribbon_4/ThisWorkbook.cs" id="Snippet1":::

### <a name="related-topics"></a>Tópicos relacionados

|Título|Descrição|
|-----------|-----------------|
|[Como: começar a personalizar a faixa de faixas](../vsto/how-to-get-started-customizing-the-ribbon.md)|Mostra como personalizar a faixa de visualização de um aplicativo Microsoft Office, adicionar um item **da faixa de Ribbon (designer visual)** ou de **faixa (XML)** a um projeto do Office.|
|[Designer de faixa de das](../vsto/ribbon-designer.md)|Descreve como você pode usar o designer de faixa de faixas para adicionar guias, grupos e controles personalizados à faixa de faixas de um aplicativo Microsoft Office.|
|[Walkthrough: criar uma guia personalizada usando o designer de faixa de faixas](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)|Mostra como criar uma guia de faixa de forma personalizada usando o designer de faixa de faixas. Você pode usar o designer de faixa de faixas para adicionar e posicionar controles na guia personalizado.|
|[Visão geral do modelo de objeto Ribbon](../vsto/ribbon-object-model-overview.md)|Fornece uma visão geral do modelo de objeto fortemente tipado que você pode usar para obter e definir as propriedades dos controles da faixa de tipos em tempo de execução.|
|[Walkthrough: atualizar os controles em uma faixa de faixas em tempo de execução](../vsto/walkthrough-updating-the-controls-on-a-ribbon-at-run-time.md)|Demonstra como usar o modelo de objeto Ribbon para atualizar os controles em uma faixa de faixas depois que a faixa de faixas é carregada no aplicativo do Office.|
|[Personalizar uma faixa de faixas para o Outlook](../vsto/customizing-a-ribbon-for-outlook.md)|Fornece orientação para personalizar a faixa de faixas no Microsoft Office Outlook.|
|[Personalizar uma faixa de faixas para o InfoPath](../vsto/customizing-a-ribbon-for-infopath.md)|Fornece orientação para personalizar a faixa de faixas no Microsoft Office InfoPath.|
|[Acessar a faixa de faixas em tempo de execução](../vsto/accessing-the-ribbon-at-run-time.md)|Mostra como mostrar, ocultar e modificar a faixa de faixas e permitir que os usuários executem o código de controles em um painel de tarefas personalizado, no painel ações ou na região de formulário do Outlook.|
|[Como alterar a posição de uma guia na faixa de forma](../vsto/how-to-change-the-position-of-a-tab-on-the-ribbon.md)|Mostra como alterar a ordem das guias em uma faixa de faixas.|
|[Como: personalizar uma guia interna](../vsto/how-to-customize-a-built-in-tab.md)|Mostra como adicionar grupos e controles a uma guia interna.|
|[Como: adicionar controles ao modo de exibição de Backstage](../vsto/how-to-add-controls-to-the-backstage-view.md)|Mostra como adicionar controles ao menu que é aberto quando você clica no **arquivo**.|
|[Como: adicionar um iniciador de caixa de diálogo a um grupo de faixa de faixas](../vsto/how-to-add-a-dialog-box-launcher-to-a-ribbon-group.md)|Mostra para adicionar um iniciador de caixa de diálogo a qualquer grupo em uma faixa de faixas.|
|[Como exportar uma faixa de faixas do designer de faixa de das faixas para XML da faixa de modo](../vsto/how-to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml.md)|Mostra como personalizar a faixa de opções de maneiras avançadas exportando a faixa do designer para o XML da faixa.|
|[XML da faixa de opções](../vsto/ribbon-xml.md)|Explica como você pode personalizar uma faixa de modo usando o XML da faixa de uma.|
|[Walkthrough: criar uma guia personalizada usando o designer de faixa de faixas](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)|Demonstra como criar uma guia de faixa de forma personalizada usando o item da faixa de forma **(XML)** .|
