---
title: Gerenciamento de titular de bloqueio de documentos | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - document locking
ms.assetid: fa1ce513-eb7d-42bc-b6e8-cb2433d051d5
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 45b41227e5bcacbd5f0705bb46b0cacf01a46ab7
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49897024"
---
# <a name="document-lock-holder-management"></a>Gerenciamento de titular de bloqueio de documento
A tabela de documento (RDT) em execução mantém uma contagem de documentos abertos e todos eles têm os bloqueios de edição. Você pode colocar um bloqueio de edição em um documento no RDT quando é editado por meio de programação em segundo plano sem que o usuário ver um documento aberto em uma janela do documento. Essa funcionalidade é frequentemente usada pelos designers que modificar vários arquivos através de uma interface gráfica do usuário.  
  
## <a name="document-lock-holder-scenarios"></a>Cenários de titular de bloqueio de documento  
  
### <a name="file-a-has-a-dependence-on-file-b"></a>Arquivo de "a" tem uma dependência no arquivo "b"  
 Considere uma situação em que você implementar um editor padrão "A" de tipo de arquivo "a" e cada arquivo do tipo "a" tem uma referência a (ou a dependência de) um arquivo do tipo "b". Existe um editor padrão "B" para arquivos do tipo "b". Quando o editor de "A" abre o arquivo "r" recupera a referência para o arquivo correspondente "b". O arquivo "b" não é exibido, mas o editor "A" pode modificá-lo. Editor de "A" obtém uma referência aos dados de documento do arquivo de "b" do <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.FindAndLockDocument%2A> método e também mantém um bloqueio de edição no arquivo "b". Depois que o editor "A" é feito modificando o arquivo "b", você pode diminuir o bloqueio de edição contar com o arquivo "b" chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.UnlockDocument%2A> método. Você pode omitir essa etapa se você tivesse chamado de <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.FindAndLockDocument%2A> método com o parâmetro `dwRDTLockType` definido como <xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS>.  
  
### <a name="file-b-is-opened-by-a-different-editor"></a>O arquivo "b" é aberto por um outro editor  
 No caso em que o arquivo "b" já está aberto por editor "B", quando o editor de "A" tenta abri-lo, há dois cenários separados para lidar com:  
  
- Se o arquivo "b" está aberto em um editor compatível, você deve ter A"editor" registrar um bloqueio de edição de documento no arquivo "b" usando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.RegisterDocumentLockHolder%2A> método. Depois que o seu editor de "A" é feito modificando arquivos "b", cancelar o registro do documento editar bloqueio usando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.UnregisterDocumentLockHolder%2A> método.  
  
- Se o arquivo "b" está aberto em um modo incompatível, você pode deixar que a tentativa abertura de arquivo "b" por "A" falha, ou você pode permitir que o modo de exibição associado ao editor "A" parcialmente abre e exibe uma mensagem de erro apropriado de editor. A mensagem de erro deve instruir o usuário fechar o arquivo "b" no editor incompatível e, em seguida, abra novamente o arquivo usando o "a" editor "A". Você também pode implementar o [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] método <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable2.QueryCloseRunningDocument%2A> para avisar o usuário fechar o arquivo "b" que é aberto no editor incompatível. Se o usuário fechar o arquivo "b", a abertura do arquivo de "a" no editor "A" continuará normalmente.  
  
## <a name="additional-document-edit-lock-considerations"></a>Considerações de bloqueio de edição de documentos adicionais  
 Você obterá um comportamento diferente, se o editor de "A" é o único editor que tem um documento de editar o bloqueio no arquivo "b" do que o editor "B" também contém um documento editar bloqueio no arquivo "b". Na [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)], **Designer de classe** é um exemplo de um designer visual que não mantém um bloqueio de editar o arquivo de código associado. Ou seja, se o usuário tem um diagrama de classe abrir no modo de exibição de design e o arquivo de código associado abertos simultaneamente, e se o usuário modifica o arquivo de código, mas não salvar as alterações, as alterações também serão perdidas ao arquivo de diagrama (. CD) de classe. Se o **Designer de classe** tem o documento apenas editar bloqueio no arquivo de código, o usuário não será solicitado a salvar as alterações ao fechar o arquivo de código. O IDE pede ao usuário para salvar as alterações somente depois que o usuário fecha o **Designer de classe**. As alterações salvas são refletidas em ambos os arquivos. Se ambos os **Designer de classe** e o editor de arquivo de código mantidos bloqueios de edição de documento no arquivo de código, em seguida, o usuário é solicitado a salvar ao fechar o arquivo de código ou o formulário. Nesse ponto, as alterações salvas são refletidas no formulário e o arquivo de código. Para obter mais informações sobre diagramas de classe, consulte [trabalhar com diagramas de classe (Designer de classe)](../ide/working-with-class-diagrams-class-designer.md).  
  
 Observe que se você precisar colocar um bloqueio de edição em um documento para um não-editor, você deve implementar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder> interface.  
  
 Muitas vezes um interface do usuário designer que modifica os arquivos de código por meio de programação faz alterações em mais de um arquivo. Nesses casos, o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell2.SaveItemsViaDlg%2A> método manipula o salvamento de um ou mais documentos por meio das **você deseja salvar as alterações aos seguintes itens?** caixa de diálogo.  
  
## <a name="see-also"></a>Consulte também  
 [tabela de documento em execução](../extensibility/internals/running-document-table.md)   
 [Tabela de documento em execução e persistência](../extensibility/internals/persistence-and-the-running-document-table.md)