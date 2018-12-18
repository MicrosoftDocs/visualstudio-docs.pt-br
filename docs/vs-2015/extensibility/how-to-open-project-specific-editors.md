---
title: 'Como: abrir editores específicos do projeto | Microsoft Docs'
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
- project types, opening a project-specific editor
- editors [Visual Studio SDK], opening project-specific editors
- projects [Visual Studio SDK], opening folders
ms.assetid: 83e56d39-c97b-4c6b-86d6-3ffbec97e8d1
caps.latest.revision: 14
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 52d1fda1c3a1c2e8aac116c52afc8bf6738e23ea
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51817666"
---
# <a name="how-to-open-project-specific-editors"></a>Como: abrir editores específicos do projeto
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Se um arquivo de item que está sendo aberto por um projeto é intrinsecamente associado ao editor específico para o projeto, o projeto deve abrir o arquivo usando um editor específico do projeto. O arquivo não pode ser delegado para baixo para o mecanismo do IDE para a seleção de um editor. Por exemplo, em vez de usar um editor de bitmap padrão, você pode usar essa opção do editor específicas a um projeto para especificar um editor de bitmap específico que reconhece as informações no arquivo que é exclusivo ao seu projeto.  
  
 As chamadas IDE a <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A> método quando ele determina se um arquivo deve ser aberto por um projeto específico. Para obter mais informações, consulte [exibindo arquivos usando o comando Abrir do arquivo](../extensibility/internals/displaying-files-by-using-the-open-file-command.md). Use as seguintes diretrizes para implementar o `OpenItem` método para que seu projeto a abrir um arquivo usando um editor específico do projeto.  
  
### <a name="to-implement-the-openitem-method-with-a-project-specific-editor"></a>Para implementar o método OpenItem com um editor específico do projeto  
  
1.  Chamar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.FindAndLockDocument%2A> método (RDT_EditLock) para determinar se o arquivo (objeto de dados de documento) já está aberto.  
  
    > [!NOTE]
    >  Para obter mais informações sobre dados de documentos e objetos de exibição de documento, consulte [dados de documentos e exibição de documentos em editores personalizados](../extensibility/document-data-and-document-view-in-custom-editors.md).  
  
2.  Se o arquivo já estiver aberto, repavimentar o arquivo chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.IsDocumentOpen%2A> método e especificando um valor de IDO_ActivateIfOpen para o `grfIDO` parâmetro.  
  
     Se o arquivo está aberto e o documento pertencente a um projeto que não seja o projeto de chamada, um aviso será exibido para o usuário que o editor que está sendo aberto é de outro projeto. A janela de arquivo, em seguida, é exibida.  
  
3.  Se o buffer de texto (objeto de dados de documento) já está aberto e você deseja anexar outro modo de exibição a ele, você é responsável por esse modo de exibição de gancho. A abordagem recomendada para criar uma instância de um modo de exibição (objeto de exibição de documento) do projeto, é o seguinte:  
  
    1.  Chame `QueryService` sobre o <xref:Microsoft.VisualStudio.Shell.Interop.SLocalRegistry> service para obter um ponteiro para o <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2> interface.  
  
    2.  Chamar o <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2.CreateInstance%2A> método para criar uma instância da classe de exibição do documento.  
  
4.  Chamar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.CreateDocumentWindow%2A> método, especificando seu objeto de exibição de documento.  
  
     Esse método sites o objeto de exibição de documento em uma janela do documento.  
  
5.  Executar as chamadas apropriadas para qualquer um de <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat.InitNew%2A> ou o <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat.Load%2A> métodos.  
  
     Neste ponto, o modo de exibição deve ser totalmente inicializado e está pronto para ser aberto.  
  
6.  Chamar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.Show%2A> método para mostrar e abrir o modo de exibição.  
  
## <a name="see-also"></a>Consulte também  
 [Abrir e salvar itens de projeto](../extensibility/internals/opening-and-saving-project-items.md)   
 [Como: abrir editores padrão](../extensibility/how-to-open-standard-editors.md)   
 [Como abrir editores para documentos abertos](../extensibility/how-to-open-editors-for-open-documents.md)

