---
title: 'Como: usar o gerenciamento de desfazer vinculado | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - linked undo management
ms.assetid: af5cc22a-c9cf-45b1-a894-1022d563f3ca
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 255ad8de79b13a74816b2abd28281ac5de6f1932
ms.sourcegitcommit: 3dd15e019cba7d35dbabc1aa3bf55842a59f5278
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/19/2018
ms.locfileid: "46370556"
---
# <a name="how-to-use-linked-undo-management"></a>Como: usar vinculado gerenciamento de desfazer
Desfazer vinculado permite que o usuário simultaneamente, desfazer as mesmas edições em vários arquivos. Por exemplo, as alterações de texto simultâneas em vários arquivos de programa, como um arquivo de cabeçalho e um arquivo do Visual C++, é uma transação de desfazer vinculado. Capacidade de desfazer vinculado está incorporada a implementação do ambiente do Gerenciador de desfazer, e <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLinkedUndoTransactionManager> permite manipular esse recurso. Desfazer vinculado é implementado por uma unidade de desfazer pai que pode vincular as pilhas de desfazer separado juntos para ser tratado como uma unidade de desfazer. O procedimento para usar um Desfazer vinculado é detalhado na seção a seguir.  
  
## <a name="to-use-linked-undo"></a>Para usar um Desfazer vinculado  
  
1.  Chame `QueryService` na `SVsLinkedUndoManager` para obter um ponteiro para `IVsLinkedUndoTransactionManager`.  
  
2.  Criar a unidade de desfazer vinculado pai inicial chamando <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLinkedUndoTransactionManager.OpenLinkedUndo%2A>. Isso define o ponto de partida para um conjunto de pilhas de desfazer a ser agrupada em pilhas de desfazer vinculado. No `OpenLinkedUndo` método, você também precisará especificar se deseja que o desfazer vinculado ser estrito ou não restrito. Comportamento de desfazer vinculado não estrito significa que alguns dos documentos com irmãos de desfazer vinculado podem fechar e ainda, deixe o outro vinculado desfazer irmãos em suas pilhas. Comportamento estrito desfazer vinculado Especifica que todas as pilhas de irmão desfazer vinculado precisam ser desfeita juntos ou nenhum. Adicionar subsequentes vinculado pilhas de desfazer, chamando [IOleUndoManager::Add](/windows/desktop/api/ocidl/nf-ocidl-ioleundomanager-add) método.  
  
3.  Chamar <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLinkedUndoTransactionManager.CloseLinkedUndo%2A> reverter todas as unidades de desfazer vinculado como um.  
  
    > [!NOTE]
    >  Para implementar o gerenciamento de desfazer vinculado em um editor, adicione o gerenciamento de desfazer. Para obter mais informações sobre como implementar o gerenciamento de desfazer vinculado, consulte [como: implementar o gerenciamento de desfazer](../extensibility/how-to-implement-undo-management.md).  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompoundAction>   
 [IOleParentUndoUnit](/windows/desktop/api/ocidl/nn-ocidl-ioleparentundounit)   
 [IOleUndoUnit](/windows/desktop/api/ocidl/nn-ocidl-ioleundounit)   
 [Como: implementar o gerenciamento de desfazer](../extensibility/how-to-implement-undo-management.md)