---
title: Gerenciamento de titular de bloqueio de documentos | Microsoft Docs
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
- editors [Visual Studio SDK], custom - document locking
ms.assetid: fa1ce513-eb7d-42bc-b6e8-cb2433d051d5
caps.latest.revision: 22
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 8eaeb8529f570db112bf43813fe20339f3bca7c2
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51786295"
---
# <a name="document-lock-holder-management"></a>Gerenciamento de proprietário de bloqueio de documento
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A tabela de documento em execução (RDT) mantém uma contagem de documentos abertos e todos eles têm os bloqueios de edição. Você pode colocar um bloqueio de edição em um documento no RDT quando é editado por meio de programação em segundo plano sem que o usuário ver um documento aberto em uma janela do documento. Essa funcionalidade é frequentemente usada pelos designers que modificar vários arquivos através de uma interface gráfica do usuário.  
  
## <a name="document-lock-holder-scenarios"></a>Cenários de titular de bloqueio de documento  
  
### <a name="file-a-has-a-dependence-on-file-b"></a>Arquivo de "a" uma dependência no arquivo tem "b"  
 Considere uma situação em que você implementar um editor padrão "A" de tipo de arquivo "a" e cada arquivo do tipo "a" tem uma referência a (ou a dependência de) um arquivo do tipo "b". Existe um editor padrão "B" para arquivos do tipo "b". Quando o editor de "A" abre o arquivo "r" recupera a referência para o arquivo correspondente "b". O arquivo "b" não é exibido, mas o editor "A" pode modificá-lo. Editor de "A" obtém uma referência aos dados de documento do arquivo de "b" do <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.FindAndLockDocument%2A> método e também mantém um bloqueio de edição no arquivo "b". Depois que o editor "A" é feito modificando o arquivo "b", você pode diminuir o bloqueio de edição contar com o arquivo "b" chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.UnlockDocument%2A> método. Você pode omitir essa etapa se você tivesse chamado de <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.FindAndLockDocument%2A> método com o parâmetro `dwRDTLockType` definido como <xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS>.  
  
### <a name="file-b-is-opened-by-a-different-editor"></a>O arquivo "b" é aberto por um outro Editor  
 No caso em que o arquivo "b" já está aberto por editor "B", quando o editor de "A" tenta abri-lo, há dois cenários separados para lidar com:  
  
-   Se o arquivo "b" está aberto em um editor compatível, você deve ter A"editor" registrar um bloqueio de edição de documento no arquivo "b" usando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.RegisterDocumentLockHolder%2A> método. Depois que o seu editor de "A" é feito modificando arquivos "b", cancelar o registro do documento editar bloqueio usando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.UnregisterDocumentLockHolder%2A> método.  
  
-   Se o arquivo "b" está aberto em um modo incompatível, você pode deixar que a tentativa abertura de arquivo "b" por "A" falha, ou você pode permitir que o modo de exibição associado ao editor "A" parcialmente abre e exibe uma mensagem de erro apropriado de editor. A mensagem de erro deve instruir o usuário fechar o arquivo "b" no editor incompatível e, em seguida, abra novamente o arquivo usando o "a" editor "A". Você também pode implementar o [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] método <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable2.QueryCloseRunningDocument%2A> para avisar o usuário fechar o arquivo "b" que é aberto no editor incompatível. Se o usuário fechar o arquivo "b", a abertura do arquivo de "a" no editor "A" continuará normalmente.  
  
## <a name="additional-document-edit-lock-considerations"></a>Considerações de bloqueio de edição de documentos adicionais  
 Você obterá um comportamento diferente, se o editor de "A" é o único editor que tem um documento de editar o bloqueio no arquivo "b" do que o editor "B" também contém um documento editar bloqueio no arquivo "b". Na [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], **Designer de classe** é um exemplo de um designer visual que não mantém um bloqueio de editar o arquivo de código associado. Ou seja, se o usuário tem um diagrama de classe abrir no modo de exibição de design e o arquivo de código associado abertos simultaneamente, e se o usuário modifica o arquivo de código, mas não salvar as alterações, as alterações também serão perdidas ao arquivo de diagrama (. CD) de classe. Se o **Designer de classe** tem o documento apenas editar bloqueio no arquivo de código, o usuário não será solicitado a salvar as alterações ao fechar o arquivo de código. O IDE pede ao usuário para salvar as alterações somente depois que o usuário fecha o **Designer de classe**. As alterações salvas são refletidas em ambos os arquivos. Se ambos os **Designer de classe** e o editor de arquivo de código mantidos bloqueios de edição de documento no arquivo de código, em seguida, o usuário é solicitado a salvar ao fechar o arquivo de código ou o formulário. Nesse ponto, as alterações salvas são refletidas no formulário e o arquivo de código. Para obter mais informações sobre diagramas de classe, consulte [trabalhando com diagramas de classe (Designer de classe)](../ide/working-with-class-diagrams-class-designer.md).  
  
 Observe que se você precisar colocar um bloqueio de edição em um documento para um não-editor, você deve implementar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder> interface.  
  
 Muitas vezes um interface do usuário designer que modifica os arquivos de código por meio de programação faz alterações em mais de um arquivo. Nesses casos, o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell2.SaveItemsViaDlg%2A> método manipula o salvamento de um ou mais documentos por meio das **você deseja salvar as alterações aos seguintes itens?** caixa de diálogo.  
  
## <a name="see-also"></a>Consulte também  
 [Tabela de documento em execução](../extensibility/internals/running-document-table.md)   
 [Persistência e tabela de documento em execução](../extensibility/internals/persistence-and-the-running-document-table.md)

