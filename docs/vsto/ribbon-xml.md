---
title: XML da faixa de opções
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
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
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: e5502ed118bf5b8bf622f18fd777889127e12aab
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50672438"
---
# <a name="ribbon-xml"></a>XML da faixa de opções
  O item da faixa de opções (XML) permite que você personalize uma faixa de opções usando XML. Use o item de faixa de opções (XML), se você quiser personalizar a faixa de opções de forma que não é compatível com o item da faixa de opções (Visual Designer). Para obter uma comparação do que você pode fazer com cada item, consulte [visão geral da faixa de opções](../vsto/Ribbon-overview.md).  
  
 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]  
  
## <a name="add-a-ribbon-xml-item-to-a-project"></a>Adicionar um item da faixa de opções (XML) a um projeto  
 Você pode adicionar um **da faixa de opções (XML)** item a qualquer projeto do Office da **Adicionar Novo Item** caixa de diálogo. Visual Studio adiciona automaticamente os arquivos a seguir ao seu projeto:  
  
- Um arquivo XML de faixa de opções. Esse arquivo define a interface do usuário da faixa de opções (IU). Use esse arquivo para adicionar elementos de interface do usuário, como guias, grupos e controles. Para obter detalhes, consulte [referência do arquivo XML de faixa de opções](#RibbonDescriptorFile) mais adiante neste tópico.  
  
- Um arquivo de código da faixa de opções. Esse arquivo contém o *faixa de opções classe*. Essa classe tem o nome que você especificou para o **da faixa de opções (XML)** item o **Adicionar Novo Item** caixa de diálogo. Aplicativos do Microsoft Office usam uma instância dessa classe para carregar a faixa de opções personalizada. Para obter detalhes, consulte [referência de classe da faixa de opções](#RibbonExtensionClass) mais adiante neste tópico.  
  
  Por padrão, esses arquivos de adicionar um grupo personalizado para o **Add-Ins** guia na faixa de opções.  
  
## <a name="display-the-custom-ribbon-in-a-microsoft-office-application"></a>Exibir a faixa de opções personalizada em um aplicativo do Microsoft Office  
 Depois de adicionar um **da faixa de opções (XML)** item ao seu projeto, você deve adicionar código para o **ThisAddin**, **ThisWorkbook**, ou **ThisDocument** classe que substitui o `CreateRibbonExtensibilityObject` método e retorna o XML da faixa de opções de classe para o aplicativo do Office.  
  
 O seguinte código de exemplo substitui o `CreateRibbonExtensibilityObject` MyRibbon nomeado de classe do método e retorna um XML de faixa de opções.  
  
 [!code-csharp[Trin_Ribbon_Custom_Tab_XML#1](../vsto/codesnippet/CSharp/Trin_Ribbon_Custom_Tab_XML_O12/ThisAddIn.cs#1)]
 [!code-vb[Trin_Ribbon_Custom_Tab_XML#1](../vsto/codesnippet/VisualBasic/Trin_Ribbon_Custom_Tab_XML_O12/ThisAddIn.vb#1)]  
  
## <a name="define-the-behavior-of-the-custom-ribbon"></a>Definir o comportamento da faixa de opções personalizada  
 Você pode responder a ações do usuário, como clicar em um botão na faixa de opções, criando *métodos de retorno de chamada*. Métodos de retorno de chamada são semelhantes a eventos em controles dos Windows Forms, mas eles são identificados por um atributo no XML do elemento de interface do usuário. Escrever métodos na classe da faixa de opções, e um controle chama o método que tem o mesmo nome que o valor do atributo. Por exemplo, você pode criar um método de retorno de chamada que é chamado quando um usuário clica em um botão na faixa de opções. Duas etapas são necessárias para criar um método de retorno de chamada:  
  
-   Atribua um atributo a um controle no arquivo XML de faixa de opções que identifica um método de retorno de chamada em seu código.  
  
-   Defina o método de retorno de chamada na classe da faixa de opções.  
  
> [!NOTE]  
>  O Outlook requer uma etapa adicional. Para obter mais informações, consulte [personalizar uma faixa de opções para Outlook](../vsto/customizing-a-ribbon-for-outlook.md).  
  
 Para um passo a passo que demonstra como automatizar um aplicativo da faixa de opções, consulte [instruções passo a passo: criar uma guia personalizada usando o XML da faixa de opções](../vsto/walkthrough-creating-a-custom-tab-by-using-ribbon-xml.md).  
  
### <a name="assign-callback-methods-to-controls"></a>Atribuir métodos de retorno de chamada para controles  
 Para atribuir um método de retorno de chamada a um controle no arquivo XML de faixa de opções, adicione um atributo que especifica o tipo do método de retorno de chamada e o nome do método. Por exemplo, o elemento a seguir define um botão de alternância que tem um **onAction** método de retorno de chamada chamado `OnToggleButton1`.  
  
```xml  
<toggleButton id="toggleButton1" onAction="OnToggleButton1" />  
```  
  
 **onAction** é chamado quando o usuário executa a tarefa principal associada a um controle específico. Por exemplo, o **onAction** método de retorno de chamada de um botão de alternância é chamado quando o usuário clica no botão.  
  
 O método que você especificar no atributo pode ter qualquer nome. No entanto, ele deve corresponder ao nome do método que você define no arquivo de código da faixa de opções.  
  
 Há muitos tipos diferentes de métodos de retorno de chamada que você pode atribuir aos controles da faixa de opções. Para obter uma lista completa dos métodos de retorno de chamada disponíveis para cada controle, consulte o artigo técnico [personalizar a interface do usuário da faixa de opções do Office (2007) para desenvolvedores (parte 3 de 3)](/previous-versions/office/developer/office-2007/aa722523(v=office.12)).  
  
###  <a name="CallBackMethods"></a> Definir métodos de retorno de chamada  
 Defina seus métodos de retorno de chamada na classe da faixa de opções no arquivo de código da faixa de opções. Um método de retorno de chamada tem vários requisitos:  
  
- Ele deve ser declarado como público.  
  
- Seu nome deve corresponder ao nome de um método de retorno de chamada que é atribuída a um controle no arquivo XML de faixa de opções.  
  
- Sua assinatura deve corresponder à assinatura de um tipo de método de retorno de chamada que está disponível para o controle associado de faixa de opções.  
  
  Para obter uma lista completa das assinaturas de método de retorno de chamada para controles da faixa de opções, consulte o artigo técnico [personalizar a interface do usuário da faixa de opções do Office (2007) para desenvolvedores (parte 3 de 3)](/previous-versions/office/developer/office-2007/aa722523(v=office.12)). Visual Studio não fornece suporte ao IntelliSense para os métodos de retorno de chamada que você criar no arquivo de código da faixa de opções. Se você criar um método de retorno de chamada que não corresponde a uma assinatura válida, o código será compilado, mas nada ocorrerá quando o usuário clica no controle.  
  
  Todos os métodos de retorno de chamada tem um <xref:Microsoft.Office.Core.IRibbonControl> parâmetro que representa o controle que chamou o método. Você pode usar esse parâmetro para reutilizar o mesmo método de retorno de chamada para vários controles. O exemplo de código a seguir demonstra uma **onAction** método de retorno de chamada que executa tarefas diferentes, dependendo de qual controle o usuário clica.  
  
  [!code-csharp[Trin_RibbonOutlookBasic#2](../vsto/codesnippet/CSharp/Trin_RibbonOutlookBasic/Ribbon1.cs#2)]
  [!code-vb[Trin_RibbonOutlookBasic#2](../vsto/codesnippet/VisualBasic/Trin_RibbonOutlookBasic/Ribbon1.vb#2)]  
  
##  <a name="RibbonDescriptorFile"></a> Referência do arquivo XML da faixa de opções  
 Você pode definir sua faixa de opções personalizada pela adição de elementos e atributos para o arquivo XML de faixa de opções. Por padrão, o arquivo XML de faixa de opções contém o XML a seguir.  
  
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
  
 A tabela a seguir descreve os elementos padrão no arquivo XML de faixa de opções.  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|**customUI**|Representa a faixa de opções personalizada no projeto de suplemento do VSTO.|  
|**Faixa de opções**|Representa a faixa de opções.|  
|**Guias**|Representa um conjunto de guias da faixa de opções.|  
|**tab**|Representa uma única guia de faixa de opções.|  
|**group**|Representa um grupo de controles na guia da faixa de opções.|  
  
 Esses elementos têm atributos que especificam a aparência e comportamento da faixa de opções personalizada. A tabela a seguir descreve os atributos padrão no arquivo XML de faixa de opções.  
  
|Atributo|Elemento pai|Descrição|  
|---------------|--------------------|-----------------|  
|**onLoad**|**customUI**|Identifica um método que é chamado quando o aplicativo carrega a faixa de opções.|  
|**idMso**|**tab**|Identifica uma guia interna para exibir na faixa de opções.|  
|**id**|**group**|Identifica o grupo.|  
|**label**|**group**|Especifica o texto que aparece no grupo.|  
  
 Os atributos no arquivo XML de faixa de opções e elementos de padrão são um pequeno subconjunto de elementos e atributos que estão disponíveis. Para obter uma lista completa dos atributos e elementos disponíveis, consulte o artigo técnico [personalizar a interface do usuário da faixa de opções do Office (2007) para desenvolvedores (parte 2 de 3)](/previous-versions/office/developer/office-2007/aa338199(v=office.12)).  
  
##  <a name="RibbonExtensionClass"></a> Referência de classe da faixa de opções  
 Visual Studio gera a classe da faixa de opções no arquivo de código da faixa de opções. Adicione os métodos de retorno de chamada para controles da faixa de opções para essa classe. Essa classe implementa o <xref:Microsoft.Office.Core.IRibbonExtensibility> interface.  
  
 A tabela a seguir descreve os métodos padrão nessa classe.  
  
|Método|Descrição|  
|------------|-----------------|  
|`GetCustomUI`|Retorna o conteúdo do arquivo XML de faixa de opções. Aplicativos do Microsoft Office chamam esse método para obter uma cadeia de caracteres XML que define a interface do usuário da sua faixa de opções personalizada. Este método implementa o método <xref:Microsoft.Office.Core.IRibbonExtensibility.GetCustomUI%2A>. **Observação:** `GetCustomUI` devem ser implementadas apenas para retornar o conteúdo do arquivo XML de faixa de opções; ele não deve ser usado para inicializar o suplemento do VSTO. Em particular, você não deve tentar exibir caixas de diálogo ou outras janelas no seu `GetCustomUI` implementação. Caso contrário, a faixa de opções personalizada pode não se comportar corretamente. Se for preciso executar o código que inicializa o suplemento do VSTO, adicione o código para o `ThisAddIn_Startup` manipulador de eventos.|  
|`OnLoad`|Atribui a <xref:Microsoft.Office.Core.IRibbonControl> parâmetro para o `Ribbon` campo. Aplicativos do Microsoft Office chamam esse método quando eles são carregados a faixa de opções personalizada. Você pode usar este campo para atualizar dinamicamente a faixa de opções personalizada. Para obter mais informações, consulte o artigo técnico [personalizar a interface do usuário da faixa de opções do Office (2007) para desenvolvedores (parte 1 de 3)](/previous-versions/office/developer/office-2007/aa338202(v=office.12)).|  
|`GetResourceText`|Chamado pelo `GetCustomUI` método para obter o conteúdo do arquivo XML de faixa de opções.|  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral da faixa de opções](../vsto/ribbon-overview.md)   
 [Passo a passo: Criar uma guia personalizada usando o XML da faixa de opções](../vsto/walkthrough-creating-a-custom-tab-by-using-ribbon-xml.md)   
 [Personalização da interface do usuário do Office](../vsto/office-ui-customization.md)  
  
  