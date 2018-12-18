---
title: As fábricas de editor | Microsoft Docs
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
- editors [Visual Studio SDK], legacy - editor factories
ms.assetid: cf4e8164-3546-441d-b465-e8a836ae7216
caps.latest.revision: 21
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 74ea8d296db643e74654f9016c1f5bff4f34c6d8
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51809448"
---
# <a name="editor-factories"></a>Fábricas de editor
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Uma fábrica de editor cria objetos do editor e coloca-os em um quadro de janela conhecido como uma exibição física. Ele cria os dados de documentos e objetos de exibição de documento que são necessários para criar editores e designers. Uma fábrica de editor é necessário para criar o editor principal do Visual Studio e qualquer editor padrão. Um editor personalizado também pode ser criado com uma fábrica de editor.  
  
 Criar uma fábrica de editor Implementando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory> interface. O exemplo a seguir ilustra como implementar <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory> para criar uma fábrica de editor:  
  
 [!code-csharp[VSSDKEditorFactories#1](../snippets/csharp/VS_Snippets_VSSDK/vssdkeditorfactories/cs/vssdkeditorfactoriespackage.cs#1)]
 [!code-vb[VSSDKEditorFactories#1](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkeditorfactories/vb/vssdkeditorfactoriespackage.vb#1)]  
  
 Um editor é carregado na primeira vez que você abrir um tipo de arquivo tratado pelo editor. Você pode optar por abrir um editor específico ou o editor padrão. Se você selecionar o editor padrão, o ambiente de desenvolvimento integrado (IDE) determina o editor correto para abrir e, em seguida, abre-lo. Para obter mais informações, consulte [determinar qual Editor abre um arquivo em um projeto](../extensibility/internals/determining-which-editor-opens-a-file-in-a-project.md).  
  
## <a name="registering-editor-factories"></a>Registrar fábricas de Editor  
 Antes de usar um editor que você criou, primeiro você deve registrar informações sobre ele, incluindo as extensões de arquivo, que ele pode manipular.  
  
 Se o VSPackage é escrito em código gerenciado, você pode usar o método de estrutura de pacote gerenciado (MPF) <xref:Microsoft.VisualStudio.Shell.Package.RegisterEditorFactory%2A> para registrar a fábrica do editor, após o VSPackage é carregado. Se o VSPackage é escrito em código não gerenciado, você deve registrar sua fábrica de editor usando o <xref:Microsoft.VisualStudio.Shell.Interop.SVsRegisterEditors> service.  
  
### <a name="registering-an-editor-factory-by-using-managed-code"></a>Registrar uma fábrica de Editor usando código gerenciado  
 Você deve registrar sua fábrica de editor no VSPackage o `Initialize` método. Primeiro chamar `base.Initialize`e, em seguida, chame <xref:Microsoft.VisualStudio.Shell.Package.RegisterEditorFactory%2A> para cada fábrica de editor  
  
 No código gerenciado, não é necessário cancelar o registro de uma fábrica de editor, pois o VSPackage tratará disso para você. Além disso, se sua fábrica de editor implementa <xref:System.IDisposable>, ele é descartado automaticamente quando ele é cancelado.  
  
### <a name="registering-an-editor-factory-by-using-unmanaged-code"></a>Registrando uma fábrica de editor usando código não gerenciado  
 No <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A> implementação para o seu pacote do editor, use o `QueryService` método a ser chamado `SVsRegisterEditors`. Isso retorna um ponteiro para <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterEditors>. Chame o <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterEditors.RegisterEditor%2A> método, passando a sua implementação do <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory> interface. Você deve mplementar <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory> em uma classe separada.  
  
## <a name="the-editor-factory-registration-process"></a>O processo de registro de fábrica de Editor  
 O seguinte processo ocorre quando o Visual Studio carregará seu editor usando sua fábrica de editor:  
  
1.  O [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] chamadas do sistema de projeto <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>.  
  
2.  Esse método retorna a fábrica do editor. Atrasos Visual do Studio carregar o pacote do editor, no entanto, até que um sistema de projeto precisa, na verdade, o editor.  
  
3.  Quando um sistema de projeto requer o editor, o Visual Studio chama <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A>, um método especializado que retorna o modo de exibição de documento e o documento de objetos de dados.  
  
4.  Se chama pelo Visual Studio para sua fábrica de editor usando <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> retornar um objeto de dados de documento e um objeto de exibição de documento, o Visual Studio, em seguida, cria a janela do documento, coloca o objeto de exibição de documento nele e faz uma entrada no documento em execução tabela (RDT) para o objeto de dados do documento.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory>   
 [Tabela de documentos em execução](../extensibility/internals/running-document-table.md)

