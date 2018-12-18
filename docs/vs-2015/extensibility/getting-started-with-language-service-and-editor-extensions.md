---
title: Introdução ao serviço de linguagem e as extensões do Editor | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- editors [Visual Studio SDK], new - extensions
ms.assetid: 6b151891-c06d-40b1-9867-42298caa8492
caps.latest.revision: 22
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: f09056d184256e2d62387af08c61186c6ff57c02
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51735207"
---
# <a name="getting-started-with-language-service-and-editor-extensions"></a>Introdução ao serviço de linguagem e às extensões do editor
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode usar as extensões do editor para adicionar recursos de serviço de linguagem, como a estrutura de tópicos, correspondência de chaves, IntelliSense e as lâmpadas para sua própria linguagem de programação ou a qualquer tipo de conteúdo. Você também pode personalizar a aparência e comportamento do editor do Visual Studio, por exemplo texto coloração, margens, adornos e outros elementos visuais. Você também pode definir seu próprio tipo de conteúdo e especificar a aparência e comportamento dos modos de exibição de texto no qual o conteúdo será exibido.  
  
 Para começar a escrever as extensões do editor, use os modelos de projeto do editor que são instalados como parte do SDK do Visual Studio. O SDK do Visual Studio é um conjunto para download de ferramentas que tornam mais fácil desenvolver extensões do Visual Studio, usando os VSPackages ou usando o Managed Extensibility Framework (MEF).  
  
> [!NOTE]
>  Para obter mais informações sobre o SDK do Visual Studio, consulte [SDK do Visual Studio](../extensibility/visual-studio-sdk.md).  
  
 É recomendável que você Aprenda sobre os seguintes conceitos e tecnologias antes de escrever suas próprias extensões de editor.  
  
## <a name="the-windows-presentation-foundation-wpf-and-editor-extensions"></a>O Windows Presentation Foundation (WPF) e as extensões do Editor  
 Interface de usuário de editor do Visual Studio (interface do usuário) é implementado usando o Windows Presentation Foundation (WPF). O WPF fornece uma experiência visual e um modelo de programação consistente que separa os aspectos visuais do código da lógica de negócios. Quando você cria as extensões do editor, você pode usar vários elementos do WPF e recursos. Para obter mais informações, consulte [Windows Presentation Foundation](http://msdn.microsoft.com/library/f667bd15-2134-41e9-b4af-5ced6fafab5d).  
  
## <a name="the-managed-extensibility-framework-mef-and-editor-extensions"></a>O Managed Extensibility Framework (MEF) e as extensões do Editor  
 Editor do Visual Studio usa o MEF Managed Extensibility Framework () para gerenciar seus componentes e extensões. O MEF também permite que os desenvolvedores mais facilmente criar extensões para um aplicativo host como o Visual Studio. Nessa estrutura, você pode define uma extensão de acordo com um contrato MEF e exportá-lo como uma parte do componente de MEF. O aplicativo host gerencia as partes do componente, localizá-los, registrando-os e certificando-se de que eles são aplicados ao contexto correto.  
  
> [!NOTE]
>  Para obter mais informações sobre o MEF no editor, consulte [Managed Extensibility Framework no Editor de](../extensibility/managed-extensibility-framework-in-the-editor.md).  
  
## <a name="visual-studio-editor-extension-points-and-extensions"></a>Pontos de extensão de Editor do Visual Studio e extensões  
 Pontos de extensão do editor são partes do componente de MEF que você pode personalizar e estender. Em alguns casos você pode estender o ponto de extensão implementando uma interface e exportá-lo junto com os metadados corretos. Em outros casos basta declarar uma extensão e exportá-lo como um tipo específico.  
  
 A seguir está alguns dos tipos básicos de extensões do editor:  
  
- Margens e barras de rolagem  
  
- Marcas  
  
- Adornos  
  
- Opções  
  
- IntelliSense  
  
  Para obter mais informações sobre pontos de extensão de editor, consulte [serviço de linguagem e pontos de extensão de Editor](../extensibility/language-service-and-editor-extension-points.md).  
  
## <a name="deploying-editor-extensions"></a>Implantando extensões de Editor  
 No Visual Studio, você pode implantar as extensões do editor, adicionando um arquivo de metadados chamado vsixmanifest à solução, compilar a solução e, em seguida, adicionando uma cópia dos arquivos binários e o manifesto em uma pasta que é conhecida para o Visual Studio. O arquivo de manifesto define as informações básicas sobre a extensão (por exemplo, nome, autor, versão e tipo de conteúdo). Para obter mais informações sobre o arquivo de manifesto do VSIX e como implantar extensões, consulte [envio extensões do Visual Studio](../extensibility/shipping-visual-studio-extensions.md).  
  
 Quando você instala uma extensão em um computador, incluem os binários e o manifesto em uma subpasta da pasta que é conhecida como Visual Studio.  
  
> [!WARNING]
>  Você não precisa se preocupar sobre os detalhes de manifestos e locais de implantação, se você usar um dos modelos de extensibilidade de editor que estão incluídos no Visual Studio. Os modelos contêm tudo o que é necessário para registrar e implantar uma extensão.  
  
## <a name="running-extensions-in-the-experimental-instance"></a>Execução de extensões na instância Experimental  
 Você pode isolar sua versão de trabalho do Visual Studio enquanto você estiver desenvolvendo uma extensão ao implantá-lo na seguinte pasta experimental (no Windows Vista e Windows 7):  
  
 *% LOCALAPPDATA %* \VisualStudio\10.0Exp\Extensions\\*empresa*\\*ExtensionID*  
  
 em que *% LOCALAPPDATA %* é o nome do usuário conectado *empresa* é o nome da empresa que possui a extensão, e *ExtensionID* é a ID da extensão.  
  
 Quando você implanta uma extensão para o local experimental, ele é executado no modo de depuração. Uma segunda instância do Visual Studio é iniciada e é denominada **Microsoft Visual Studio - instância Experimental**.  
  
## <a name="managing-extensions"></a>Gerenciamento de extensões  
 Extensões para Visual Studio são listadas na **extensões e atualizações** (sobre o **ferramentas** menu). Se você estiver testando uma extensão na instância experimental, ele é listado no **extensões e atualizações** na instância experimental, mas não está listado na instância de desenvolvimento.  
  
 Para obter mais informações, consulte [Localizando e usando extensões do Visual Studio](../ide/finding-and-using-visual-studio-extensions.md).  
  
## <a name="using-templates-to-create-editor-extensions"></a>Usando modelos para criar extensões de Editor  
 Você pode usar o editor de modelos para criar extensões MEF que personalizam classificadores, adornos e margens. Há modelos para projetos c# e Visual Basic. Para obter mais informações, consulte [criar uma extensão com um modelo de Item Editor](../extensibility/creating-an-extension-with-an-editor-item-template.md).  
  
 Você também pode usar o modelo de projeto de VSIX para criar extensões. Esse modelo fornece apenas os elementos que são necessárias para implantar qualquer tipo de extensão e incluir o arquivo vsixmanifest, as referências de assembly necessárias e um arquivo de projeto que inclui as tarefas de compilação que permitem que você implantar o extensão. Para obter mais informações, consulte [modelo de projeto do VSIX](../extensibility/vsix-project-template.md).  
  
 Você também pode criar editor de componentes do MEF de uma extensão do pacote do Visual Studio. Consulte as instruções a seguir para obter detalhes:  
  
-   [Passo a passo: Usar um comando de Shell com uma extensão do editor](../extensibility/walkthrough-using-a-shell-command-with-an-editor-extension.md)  
  
-   [Passo a passo: Usar uma chave de atalho com uma extensão do editor](../extensibility/walkthrough-using-a-shortcut-key-with-an-editor-extension.md)  
  
## <a name="see-also"></a>Consulte também  
 [Serviço de linguagem e pontos de extensão do editor](../extensibility/language-service-and-editor-extension-points.md)

