---
title: Criar Designers e editores personalizados | Microsoft Docs
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
- designers [Visual Studio SDK]
- editors [Visual Studio SDK], custom
ms.assetid: b6a5e8b2-0ae1-4fc3-812d-09d40051b435
caps.latest.revision: 32
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 324284a6cac44c995d652cce2f2e82a4c13702c1
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51753258"
---
# <a name="creating-custom-editors-and-designers"></a>Criando designers e editores personalizados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O ambiente de desenvolvimento integrado (IDE) do Visual Studio pode hospedar diferentes tipos de editor:  
  
- O editor principal do Visual Studio  
  
- Editores personalizados  
  
- Editores externos  
  
- Designers  
  
  As informações a seguir ajuda a escolher o tipo de editor que você precisa.  
  
## <a name="types-of-editor"></a>Tipos de Editor  
 Para obter informações sobre o editor principal do Visual Studio, consulte [estender o Editor e os serviços de linguagem](../extensibility/extending-the-editor-and-language-services.md).  
  
##### <a name="custom-editors"></a>Editores personalizados  
 Um editor personalizado é aquele que foi projetado para funcionar em casos especializados. Por exemplo, você pode criar um editor cuja função é ler e gravar dados em um repositório específico, como um Microsoft Exchange server. Se você quiser um editor que funciona com o tipo de projeto ou se você quiser que um editor que tem apenas alguns comandos específicos, escolha um editor personalizado. No entanto, observe que os usuários não poderão usar um editor personalizado para editar padrão [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] projetos.  
  
 Um editor personalizado pode usar uma fábrica de editor e adicionar informações sobre o editor no registro. No entanto, o tipo de projeto associado com o editor personalizado pode instanciar o editor personalizado de outras maneiras.  
  
 Um editor personalizado pode usar a ativação in-loco ou incorporação simplificada para implementar uma exibição.  
  
##### <a name="external-editors"></a>Editores externos  
 Editores externos são editores que não estão integradas ao Visual Studio, como Microsoft Word, o bloco de notas ou Microsoft FrontPage. Se, por exemplo, você estiver passando o texto a ele, do VSPackage, você pode chamar tal um editor. Editores externos se registram e podem ser usados fora do Visual Studio. Quando você chamar um editor externo, e ele pode ser inserido em uma janela de host, ele aparece em uma janela no IDE. Caso contrário, em seguida, o IDE cria uma janela separada para ele.  
  
 O <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A> método define a prioridade do documento usando o <xref:Microsoft.VisualStudio.Shell.Interop.VSDOCUMENTPRIORITY> enumeração. Se o `DP_External` valor for especificado, o arquivo pode ser aberto por um editor externo.  
  
## <a name="editor-design-decisions"></a>Decisões de Design do Editor  
 As seguintes perguntas de design ajudará você a escolher o tipo de editor melhor adequado para seu aplicativo:  
  
-   O aplicativo salvará seus dados em arquivos ou não? Se ele salvará seus dados em arquivos, eles será em um formato padrão ou personalizado?  
  
     Se você usar um formato de arquivo padrão, outros tipos de projeto, além de seu projeto será capazes de abrir e ler/gravar dados para eles. Se você usar um formato de arquivo personalizado, no entanto, somente o tipo de projeto será capaz de abrir e ler/gravar dados para eles.  
  
     Se seu projeto usa arquivos, você deve personalizar o editor padrão. Se seu projeto não usa arquivos, mas em vez disso, usa itens em um banco de dados ou em outro repositório, você deve criar um editor personalizado.  
  
-   O editor de que precisa para hospedar controles ActiveX?  
  
     Se seu editor de hospedar controles ActiveX, em seguida, implementar um editor de ativação no local, conforme descrito na [ativação in-loco](../misc/in-place-activation.md). Se ele não hospedar controles ActiveX, em seguida, use um editor de incorporação simplificado, ou personalizar o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] editor padrão.  
  
-   Seu editor oferecerá suporte a vários modos de exibição? Se você quiser que os modos de exibição do seu editor fiquem visíveis ao mesmo tempo como o editor padrão, você deve suportar vários modos de exibição.  
  
     Se seu editor precisa dar suporte a vários modos de exibição, os dados de documentos e objetos de exibição de documento para o editor devem ser objetos separados. Para obter mais informações, consulte [que dão suporte a várias exibições de documento](../extensibility/supporting-multiple-document-views.md).  
  
     Se seu editor dá suporte a vários modos de exibição, você planeja usar o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] implementação do buffer de texto do editor de núcleo (<xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> objeto) para seu objeto de dados de documento? Ou seja, você deseja dar suporte a seu editor exibição lado a lado com o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] editor principal? A capacidade de fazer isso é a base do designer de formulários do...  
  
-   Se você precisa para hospedar um editor externo, pode editor ser incorporado dentro de [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]?  
  
     Se ele pode ser inserido, você deve criar uma janela de host para o editor externo e, em seguida, chame o <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A> método e defina o <xref:Microsoft.VisualStudio.Shell.Interop.VSDOCUMENTPRIORITY> valor de enumeração para `DP_External`. Se o editor não pode ser inserido, o IDE criará automaticamente uma janela separada para ele.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Passo a passo: Criar um editor personalizado](../extensibility/walkthrough-creating-a-custom-editor.md)  
 Explica como criar um editor personalizado.  
  
 [Passo a passo: Adicionar recursos a um editor personalizado](../extensibility/walkthrough-adding-features-to-a-custom-editor.md)  
 Explica como adicionar recursos a um editor personalizado.  
  
 [Inicialização do designer e configuração de metadados](../extensibility/designer-initialization-and-metadata-configuration.md)  
 Explica como inicializar um designer.  
  
 [Fornecer suporte à função desfazer para designers](../extensibility/supplying-undo-support-to-designers.md)  
 Explica como fornecer suporte à função desfazer para designers.  
  
 [Coloração de sintaxe em editores personalizados](../extensibility/syntax-coloring-in-custom-editors.md)  
 Explica a diferença entre cores no editor de núcleo e em editores personalizados de sintaxe.  
  
 [Dados de documentos e exibição de documentos em editores personalizados](../extensibility/document-data-and-document-view-in-custom-editors.md)  
 Explica como implementar dados de documentos e exibições de documento em editores personalizados.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Interfaces herdadas no editor](../extensibility/legacy-interfaces-in-the-editor.md)  
 Explica como acessar o editor de núcleo por meio da API herdada.  
  
 [Desenvolver um serviço de linguagem herdado](../extensibility/internals/developing-a-legacy-language-service.md)  
 Explica como implementar um serviço de linguagem.  
  
 [Estender outras partes do Visual Studio](../extensibility/extending-other-parts-of-visual-studio.md)  
 Explica como criar elementos de interface do usuário que correspondem ao restante do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory>

