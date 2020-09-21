---
title: 'Como: abrir editores específicos do projeto | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- project types, opening a project-specific editor
- editors [Visual Studio SDK], opening project-specific editors
- projects [Visual Studio SDK], opening folders
ms.assetid: 83e56d39-c97b-4c6b-86d6-3ffbec97e8d1
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2439a07f63b8da854ca8dc331d26e30f49503257
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "90838681"
---
# <a name="how-to-open-project-specific-editors"></a>Como abrir editores específicos a um projeto
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Se um arquivo de item que está sendo aberto por um projeto estiver associado intrinsecamente ao editor específico desse projeto, o projeto deverá abrir o arquivo usando um editor específico do projeto. Não é possível delegar o arquivo para o mecanismo do IDE para selecionar um editor. Por exemplo, em vez de usar um editor de bitmap padrão, você pode usar essa opção de editor específica do projeto para especificar um editor de bitmap específico que reconheça as informações no arquivo que é exclusivo para seu projeto.  
  
 O IDE chama o <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A> método quando determina que um arquivo deve ser aberto por um projeto específico. Para obter mais informações, consulte [exibindo arquivos usando o comando abrir arquivo](../extensibility/internals/displaying-files-by-using-the-open-file-command.md). Use as diretrizes a seguir para implementar o `OpenItem` método para que o projeto Abra um arquivo usando um editor específico do projeto.  
  
### <a name="to-implement-the-openitem-method-with-a-project-specific-editor"></a>Para implementar o método OpenItem com um editor específico de projeto  
  
1. Chame o <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.FindAndLockDocument%2A> método (RDT_EditLock) para determinar se o arquivo (objeto de dados de documento) já está aberto.  
  
    > [!NOTE]
    > Para obter mais informações sobre dados de documentos e objetos de exibição de documentos, consulte [dados de documentos e exibição de documentos em editores personalizados](../extensibility/document-data-and-document-view-in-custom-editors.md).  
  
2. Se o arquivo já estiver aberto, reponha o arquivo chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.IsDocumentOpen%2A> método e especificando um valor de IDO_ActivateIfOpen para o `grfIDO` parâmetro.  
  
     Se o arquivo estiver aberto e o documento pertencer a um projeto que não seja o projeto de chamada, um aviso será exibido para o usuário que o editor que está sendo aberto é de outro projeto. A janela de arquivo é, então, na superfície.  
  
3. Se o buffer de texto (objeto de dados de documento) já estiver aberto e você quiser anexar outra exibição a ele, você será responsável por conectar essa exibição. A abordagem recomendada para instanciar uma exibição (objeto de exibição de documento) do projeto é a seguinte:  
  
    1. Chame `QueryService` no <xref:Microsoft.VisualStudio.Shell.Interop.SLocalRegistry> serviço para obter um ponteiro para a <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2> interface.  
  
    2. Chame o <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2.CreateInstance%2A> método para criar uma instância da classe de exibição de documento.  
  
4. Chame o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.CreateDocumentWindow%2A> método, especificando o objeto de exibição de documento.  
  
     Esse método sites o objeto de exibição de documento em uma janela de documento.  
  
5. Execute as chamadas apropriadas para os <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat.InitNew%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat.Load%2A> métodos ou.  
  
     Neste ponto, a exibição deve ser totalmente inicializada e pronta para ser aberta.  
  
6. Chame o <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.Show%2A> método para mostrar e abrir o modo de exibição.  
  
## <a name="see-also"></a>Consulte Também  
 [Abrindo e salvando itens de projeto](../extensibility/internals/opening-and-saving-project-items.md)   
 [Como: abrir editores padrão](../extensibility/how-to-open-standard-editors.md)   
 [Como abrir editores para documentos abertos](../extensibility/how-to-open-editors-for-open-documents.md)
