---
title: XML da faixa de opções
description: Saiba como usar o item da faixa de opção (XML) se desejar personalizar a faixa de palavras de uma forma que não seja suportada pelo item da faixa de opção (Visual Designer).
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VSTO.Ribbon.RibbonXMLItem
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom Ribbon, XML
- customizing the Ribbon, XML
- Ribbon [Office development in Visual Studio], XML
- callback methods
- custom Ribbon, displaying
- custom Ribbon, defining behavior
- XML [Office development in Visual Studio], Ribbon
- customizing the Ribbon, defining behavior
- Ribbon [Office development in Visual Studio], customizing
- customizing the Ribbon, displaying
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: a84a0c21bba42263e7b4dad9ad9118f462389ad6
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107827494"
---
# <a name="ribbon-xml"></a>XML da faixa de opções
  O item da faixa de de (XML) permite que você personalize uma faixa de faixas usando XML. Use o item da faixa de opção (XML) se desejar personalizar a faixa de uma forma que não seja suportada pelo item da faixa de opção (Visual Designer). Para obter uma comparação do que você pode fazer com cada item, consulte [visão geral da faixa](../vsto/Ribbon-overview.md)de medida.

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

## <a name="add-a-ribbon-xml-item-to-a-project"></a>Adicionar um item da faixa (XML) a um projeto
 Você pode adicionar um item **da faixa (XML)** a qualquer projeto do Office na caixa de diálogo **Adicionar novo item** . O Visual Studio adiciona automaticamente os seguintes arquivos ao seu projeto:

- Um arquivo XML da faixa de faixas. Esse arquivo define a interface do usuário da faixa de para. Use esse arquivo para adicionar elementos de interface do usuário, como guias, grupos e controles. Para obter detalhes, consulte [referência de arquivo XML da faixa](#RibbonDescriptorFile) de visualização mais adiante neste tópico.

- Um arquivo de código da faixa de uma. Esse arquivo contém a *classe Ribbon*. Essa classe tem o nome que você especificou para o item **da faixa de para (XML)** na caixa de diálogo **Adicionar novo item** . Microsoft Office aplicativos usam uma instância dessa classe para carregar a faixa de Ribbon personalizada. Para obter detalhes, consulte [referência de classe da faixa](#RibbonExtensionClass) de medida mais adiante neste tópico.

  Por padrão, esses arquivos adicionam um grupo personalizado à guia **suplementos** na faixa de bits.

## <a name="display-the-custom-ribbon-in-a-microsoft-office-application"></a>Exibir a faixa de Ribbon personalizada em um aplicativo Microsoft Office
 Depois de adicionar um item **da faixa (XML)** ao seu projeto, você deve adicionar o código à classe **ThisAddIn**, **ThisWorkbook** ou **ThisDocument** que substitui o `CreateRibbonExtensibilityObject` método e retorna a classe XML da faixa de forma para o aplicativo do Office.

 O exemplo de código a seguir substitui o `CreateRibbonExtensibilityObject` método e retorna uma classe XML da faixa de opções chamada MyRibbon.

 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Ribbon_Custom_Tab_XML_O12/ThisAddIn.cs" id="Snippet1":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Ribbon_Custom_Tab_XML_O12/ThisAddIn.vb" id="Snippet1":::

## <a name="define-the-behavior-of-the-custom-ribbon"></a>Definir o comportamento da faixa de Ribbon personalizada
 Você pode responder às ações do usuário, como clicar em um botão na faixa de faixas, criando *métodos de retorno de chamada*. Os métodos de retorno de chamada são semelhantes a eventos nos controles Windows Forms, mas são identificados por um atributo no XML do elemento de interface do usuário. Você escreve métodos na classe Ribbon e um controle chama o método que tem o mesmo nome que o valor do atributo. Por exemplo, você pode criar um método de retorno de chamada que é chamado quando um usuário clica em um botão na faixa de faixas. Duas etapas são necessárias para criar um método de retorno de chamada:

- Atribua um atributo a um controle no arquivo XML da faixa de forma que identifica um método de retorno de chamada em seu código.

- Defina o método de retorno de chamada na classe Ribbon.

> [!NOTE]
> O Outlook requer uma etapa adicional. Para obter mais informações, consulte [personalizar uma faixa de visualização para o Outlook](../vsto/customizing-a-ribbon-for-outlook.md).

 Para obter instruções que demonstram como automatizar um aplicativo a partir da faixa de faixas, consulte [Walkthrough: criar uma guia personalizada usando o XML da faixa](../vsto/walkthrough-creating-a-custom-tab-by-using-ribbon-xml.md)de uma.

### <a name="assign-callback-methods-to-controls"></a>Atribuir métodos de retorno de chamada a controles
 Para atribuir um método de retorno de chamada a um controle no arquivo XML da faixa de tipos, adicione um atributo que especifica o tipo do método de retorno de chamada e o nome do método. Por exemplo, o elemento a seguir define um botão de alternância que tem um método de retorno de chamada **OnAction** chamado `OnToggleButton1` .

```xml
<toggleButton id="toggleButton1" onAction="OnToggleButton1" />
```

 **OnAction** é chamado quando o usuário executa a tarefa principal associada a um controle específico. Por exemplo, o método de retorno de chamada **OnAction** de um botão de alternância é chamado quando o usuário clica no botão.

 O método que você especificar no atributo pode ter qualquer nome. No entanto, ele deve corresponder ao nome do método que você definir no arquivo de código da faixa de forma.

 Há muitos tipos diferentes de métodos de retorno de chamada que você pode atribuir a controles de faixa de lista. Para obter uma lista completa dos métodos de retorno de chamada disponíveis para cada controle, consulte o artigo técnico [Personalizar a interface do usuário da faixa de Ribbon do Office (2007) para desenvolvedores (parte 3 de 3)](/previous-versions/office/developer/office-2007/aa722523(v=office.12)).

### <a name="define-callback-methods"></a><a name="CallBackMethods"></a> Definir métodos de retorno de chamada
 Defina seus métodos de retorno de chamada na classe Ribbon no arquivo de código da faixa de Ribbon. Um método de retorno de chamada tem vários requisitos:

- Ele deve ser declarado como público.

- Seu nome deve corresponder ao nome de um método de retorno de chamada que você atribuiu a um controle no arquivo XML da faixa de faixas.

- Sua assinatura deve corresponder à assinatura de um tipo de método de retorno de chamada que está disponível para o controle da faixa de tipos associado.

  Para obter uma lista completa das assinaturas do método de retorno de chamada para os controles da faixa de chamadas, consulte o artigo técnico [Personalizar a interface do usuário da faixa de forma do Office (2007) para desenvolvedores (parte 3 de 3)](/previous-versions/office/developer/office-2007/aa722523(v=office.12)). O Visual Studio não fornece suporte IntelliSense para métodos de retorno de chamada que você cria no arquivo de código da faixa de Ribbon. Se você criar um método de retorno de chamada que não corresponda a uma assinatura válida, o código será compilado, mas nada ocorrerá quando o usuário clicar no controle.

  Todos os métodos de retorno de chamada têm um <xref:Microsoft.Office.Core.IRibbonControl> parâmetro que representa o controle que chamou o método. Você pode usar esse parâmetro para reutilizar o mesmo método de retorno de chamada para vários controles. O exemplo de código a seguir demonstra um método de retorno de chamada **OnAction** que executa tarefas diferentes dependendo de qual controle o usuário clica.

  :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_RibbonOutlookBasic/Ribbon1.cs" id="Snippet2":::
  :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_RibbonOutlookBasic/Ribbon1.vb" id="Snippet2":::

## <a name="ribbon-xml-file-reference"></a><a name="RibbonDescriptorFile"></a> Referência de arquivo XML da faixa de Ribbon
 Você pode definir sua faixa de faixas personalizada adicionando elementos e atributos ao arquivo XML da faixa de faixas. Por padrão, o arquivo XML da faixa de opções contém o XML a seguir.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<customUI xmlns="http://schemas.microsoft.com/office/2006/01/customui" onLoad="OnLoad">
  <ribbon>
    <tabs>
      <tab idMso="TabAddIns">
        <group id="MyGroup"
               label="My Group">
        </group>
      </tab>
    </tabs>
  </ribbon>
</customUI>
```

 A tabela a seguir descreve os elementos padrão no arquivo XML da faixa de opções.

|Elemento|Descrição|
|-------------|-----------------|
|**customUI**|Representa a faixa de bits personalizada no projeto de suplemento do VSTO.|
|**3D**|Representa a faixa de faixas.|
|**temas**|Representa um conjunto de guias da faixa de faixas.|
|**abas**|Representa uma única guia da faixa de uma.|
|**grupo**|Representa um grupo de controles na guia faixa de faixas.|

 Esses elementos têm atributos que especificam a aparência e o comportamento da faixa de Ribbon personalizada. A tabela a seguir descreve os atributos padrão no arquivo XML da faixa de opções.

|Atributo|Elemento pai|Descrição|
|---------------|--------------------|-----------------|
|**Carregamento**|**customUI**|Identifica um método que é chamado quando o aplicativo carrega a faixa de faixas.|
|**idMso**|**abas**|Identifica uma guia interna a ser exibida na faixa de bits.|
|**id**|**grupo**|Identifica o grupo.|
|**label**|**grupo**|Especifica o texto que aparece no grupo.|

 Os elementos e atributos padrão no arquivo XML da faixa de lista são um pequeno subconjunto dos elementos e atributos que estão disponíveis. Para obter uma lista completa dos elementos e dos atributos disponíveis, consulte o artigo técnico [Personalizar a interface do usuário da faixa de Ribbon do Office (2007) para desenvolvedores (parte 2 de 3)](/previous-versions/office/developer/office-2007/aa338199(v=office.12)).

## <a name="ribbon-class-reference"></a><a name="RibbonExtensionClass"></a> Referência de classe da faixa de Ribbon
 O Visual Studio gera a classe Ribbon no arquivo de código da faixa de faixas. Adicione os métodos de retorno de chamada para controles na faixa de faixas para essa classe. Essa classe implementa a interface <xref:Microsoft.Office.Core.IRibbonExtensibility>.

 A tabela a seguir descreve os métodos padrão nesta classe.

|Método|Descrição|
|------------|-----------------|
|`GetCustomUI`|Retorna o conteúdo do arquivo XML da faixa de faixas. Microsoft Office aplicativos chamam esse método para obter uma cadeia de caracteres XML que define a interface do usuário de sua faixa de faixas personalizada. Este método implementa o método <xref:Microsoft.Office.Core.IRibbonExtensibility.GetCustomUI%2A>. **Observação:** `GetCustomUI` deve ser implementado somente para retornar o conteúdo do arquivo XML da faixa de faixas; Ele não deve ser usado para inicializar o suplemento do VSTO.   Em particular, você não deve tentar exibir caixas de diálogo ou outras janelas na sua `GetCustomUI` implementação. Caso contrário, a faixa de faixas personalizada pode não se comportar corretamente. Se você tiver que executar o código que inicializa o suplemento do VSTO, adicione o código ao `ThisAddIn_Startup` manipulador de eventos.|
|`OnLoad`|Atribui o <xref:Microsoft.Office.Core.IRibbonControl> parâmetro ao `Ribbon` campo. Microsoft Office aplicativos chamam esse método quando carregam a faixa de Ribbon personalizada. Você pode usar esse campo para atualizar dinamicamente a faixa de Ribbon personalizada. Para obter mais informações, consulte o artigo técnico [Personalizar a interface do usuário da faixa de forma do Office (2007) para desenvolvedores (parte 1 de 3)](/previous-versions/office/developer/office-2007/aa338202(v=office.12)).|
|`GetResourceText`|Chamado pelo `GetCustomUI` método para obter o conteúdo do arquivo XML da faixa de faixas.|

## <a name="see-also"></a>Consulte também
- [Visão geral da faixa de faixas](../vsto/ribbon-overview.md)
- [Walkthrough: criar uma guia personalizada usando o XML da faixa de uma](../vsto/walkthrough-creating-a-custom-tab-by-using-ribbon-xml.md)
- [Personalização da interface do usuário do Office](../vsto/office-ui-customization.md)
