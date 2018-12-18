---
title: Ativação in-loco | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-csharp
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- editors [Visual Studio SDK], custom - in-place view activation
ms.assetid: 7d316945-06e0-4d8e-ba3a-0ef96fc75399
caps.latest.revision: 26
manager: douge
ms.openlocfilehash: 5d8badf198d86e9643dbc6e98683dd3437d72f64
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49232187"
---
# <a name="in-place-activation"></a>Ativação in-loco
Se seu modo de exibição do editor hospeda ActiveX ou outros controles Active Directory, você deve implementar o modo de exibição do editor como um controle ActiveX ou como um objeto de dados de documento ativo usando o modelo de ativação no local.  
  
## <a name="support-for-menus-toolbars-and-commands"></a>Suporte para comandos, Menus e barras de ferramentas  
 Visual Studio permite a exibição do editor usar os menus e barras de ferramentas do IDE. Essas extensões são denominadas *componentes no local de OLE*. Para obter mais informações, consulte o <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponent> e <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentUIManager>.  
  
 Se você implementar um controle ActiveX, você pode hospedar outros objetos inseridos. Se você implementar um objeto de dados de documento, o quadro de janela restringe sua capacidade de usar controles ActiveX.  
  
> [!NOTE]
>  O <xref:Microsoft.VisualStudio.OLE.Interop.IOleDocument> e <xref:Microsoft.VisualStudio.OLE.Interop.IOleDocumentView> interfaces permitem que uma separação de dados e o modo de exibição. No entanto, o Visual Studio não oferece suporte a essa funcionalidade, e essas interfaces são usadas apenas para representar o objeto de exibição de documento.  
  
 Editores que usam o <xref:Microsoft.VisualStudio.Shell.Interop.SOleComponentUIManager> service pode fornecer menu, barra de ferramentas e integração de comando chamando os métodos do <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentUIManager> interface implementada pelo <xref:Microsoft.VisualStudio.Shell.Interop.SOleComponentUIManager> service. Editores também oferecem outras funcionalidades do Visual Studio, como acompanhamento da seleção e desfazer o gerenciamento. Para obter mais informações, consulte [criação personalizada editores e Designers](../extensibility/creating-custom-editors-and-designers.md).  
  
## <a name="objects-and-interfaces-used"></a>Objetos e Interfaces usadas  
 Os objetos que são usados para criar a ativação in-loco são mostrados na ilustração a seguir.  
  
 ![No&#45;Editor de ativação de colocar](../misc/media/vsinplaceactivationeditor.gif "vsInPlaceActivationEditor")  
Editor de ativação no local  
  
> [!NOTE]
>  Os objetos neste desenho, apenas o `CYourEditorFactory` objeto é necessária para criar um editor padrão. Se você estiver criando um editor personalizado, não é necessário implementar <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2> porque seu editor provavelmente terá seu próprio mecanismo de persistência privada. Para obter mais informações, consulte [criação personalizada editores e Designers](../extensibility/creating-custom-editors-and-designers.md).  
  
 Todas as interfaces que são implementadas para criar uma ativação in-loco editor são mostradas na única `CYourEditorDocument` objeto, mas essa configuração dá suporte apenas a uma única exibição de dados de documentos. Para obter mais informações sobre o suporte a vários modos de exibição de seus dados de documento, consulte [que dão suporte a várias exibições de documento](../extensibility/supporting-multiple-document-views.md).  
  
|Interface|Tipo de objeto|Use|  
|---------------|--------------------|---------|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponent>|Exibir|Permite que objetos de VSPackage in loco operar como componentes totalmente integradas do IDE, usando o <xref:Microsoft.VisualStudio.Shell.Interop.SOleComponentUIManager> service. Esse serviço integra os menus, barras de ferramentas e comandos do objeto ao IDE e emite notificações de alterações de estado.|  
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleObject>|Exibir|Principal meio pelo qual um objeto inserido fornece a funcionalidade básica para seu contêiner e se comunica com ele.|  
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleInPlaceActiveObject>|Exibir|Gerencia a ativação e desativação de objetos no local e determina o quanto do objeto no local deve estar visível.|  
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleInPlaceObject>|Exibir|Fornece um canal direto de comunicação entre um objeto no local, janela de quadro mais externo do aplicativo associado e a janela de documento no aplicativo que contém o objeto inserido.|  
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleDocument>|Exibir|Implementa um objeto ActiveX. Observe que os métodos de <xref:Microsoft.VisualStudio.OLE.Interop.IOleDocument> e `T:Microsoft.VisualStudio.OLE.Interop.IOleDocumentView` dados de documento separado e exibição não são usados no IDE.|  
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>|Exibir/dados|Permite que o objeto de dados de documento ou o objeto de exibição de documento ou ambos para participar da manipulação de comandos.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser>|Exibir|Permite atualizações da barra de status.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolboxUser>|Exibir|Permite adicionar itens à caixa de ferramentas.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsFileChangeEvents>|Dados|Envia notificação de alterações para o arquivo editado. (Essa interface é opcional.)|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>|Dados|Usado para habilitar o recurso Salvar como para um tipo de arquivo.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData>|Dados|Habilita a persistência para o documento. Para arquivos somente leitura, chame <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.SetDocDataReadOnly%2A> para fornecer o ícone de "bloqueio" que indica os arquivos somente leitura.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsDocDataFileChangeControl>|Dados|Determina se as alterações nos dados de documento devem ser ignoradas.|