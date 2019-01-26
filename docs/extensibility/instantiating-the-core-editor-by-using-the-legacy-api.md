---
title: Criando uma instância o Editor principal usando a API herdada | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - instantiating editor
ms.assetid: dda23b18-96ef-43c6-b0dc-06d15cbe5cbb
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 292e30a094cd78954e48817324a44ebacda7a78a
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "54934528"
---
# <a name="instantiate-the-core-editor-by-using-the-legacy-api"></a>Criar uma instância o editor principal usando a API herdada
O editor é responsável por funções, como inserção, exclusão, copiar e colar de edição de texto. Ele combina essas funções com as funções fornecidas pelos serviços de linguagem, como coloração de texto, recuo e preenchimento de declaração do IntelliSense.  
  
 Você pode instanciar uma instância do editor de núcleo de uma das três maneiras:  
  
- Crie explicitamente uma instância do núcleo do editor em uma janela.  
  
- Fornecer uma fábrica de editor que retorna uma instância do editor de núcleo  
  
- Abra um arquivo da hierarquia do projeto.  
  
  As seções a seguir discutem como usar a API herdada para instanciar o editor.  
  
## <a name="explicitly-open-a-core-editor-instance"></a>Abrir explicitamente uma instância do editor de núcleo  
 Ao obter explicitamente uma instância do editor de núcleo:  
  
- Obter um <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> para manter o objeto de dados de documento que está sendo editado.  
  
- Criar uma representação de linha que é orientada a dados do objeto de documento com a criação de um <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines> da interface do <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> interface.  
  
- Definir <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines> como o objeto de dados de documento para uma instância da implementação padrão do <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow> interface, usando o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow.SetBuffer%2A> método.  
  
   Host de <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow> da instância em um <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> interface usando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.CreateToolWindow%2A> método.  
  
  Neste ponto, exibindo o <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> interface fornece uma janela que contém uma instância do editor de núcleo.  
  
  No entanto, isso não é uma instância muito útil, porque não têm teclas de atalho ou acesso a recursos avançados. Para obter acesso a recursos avançados e teclas de atalho:  
  
- Use o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer.SetLanguageServiceID%2A> método a ser associado a um serviço de linguagem e o objeto de dados de documento que usa o editor.  
  
- Crie suas próprias teclas de atalho ou usar o padrão do sistema, definindo o <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> objetos exibem as propriedades. Para fazer isso, chame o <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.SetGuidProperty%2A> método com o <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID> propriedade.  
  
   Para obter e usar teclas de atalho não padrão, gerá-los usando o *VSCT* arquivo. Para obter mais informações, consulte [arquivos de tabela (. VSCT) de comando do Visual Studio](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md).  
  
## <a name="how-to-use-an-editor-factory-to-obtain-the-core-editor"></a>Como usar uma fábrica de editor para obter o editor de núcleo  
 Ao implementar um editor de núcleo com uma fábrica de editor usando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> método, siga as etapas descritas na seção anterior para hospedar explicitamente uma <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow> usando uma <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> objeto de dados de documento, em um <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> objeto.  
  
 Para exibir o texto, obter um <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> interface do <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow> objeto e chame o <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> método.  
  
 Para fornecer um serviço de linguagem para o editor, chame o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer.SetLanguageServiceID%2A> método dentro de <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> método.  
  
 Para obter padrão de teclas de atalho, diferentemente da seção anterior, você usar o contexto do comando retornado pelo <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> método ao obter o editor principal do <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> método.  
  
 Se o <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> método retorna o mesmo comando GUID como o editor de texto, a instância do editor de núcleo obtém automaticamente o padrão teclas de atalho.  
  
 Para obter informações gerais, consulte [passo a passo: Criar um núcleo de editor e registrar um tipo de arquivo do editor](../extensibility/walkthrough-creating-a-core-editor-and-registering-an-editor-file-type.md).  
  
## <a name="see-also"></a>Consulte também  
 [Dentro do editor de núcleo](../extensibility/inside-the-core-editor.md)   
 [Abrir e salvar itens de projeto](../extensibility/internals/opening-and-saving-project-items.md)   
 [Passo a passo: Criar um editor de núcleo e registrar um tipo de arquivo do editor](../extensibility/walkthrough-creating-a-core-editor-and-registering-an-editor-file-type.md)