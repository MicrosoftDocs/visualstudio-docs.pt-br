---
title: A caixa de diálogo Adicionar item de filtragem para projetos aninhados | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- filtering, nested projects
- nested projects, AddItem dialog box filtering
ms.assetid: 5b3e352e-7f18-4f66-be16-b0ad55637ce5
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 61a51c69857f9bd8f5b2ad84448b0170b809c18a
ms.sourcegitcommit: 1c2ed640512ba613b3bbbc9ce348e28be6ca3e45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39497073"
---
# <a name="filter-the-additem-dialog-box-for-nested-projects"></a>Filtrar a caixa de diálogo AddItem para projetos aninhados
Quando você exibe um **AddItem** caixa de diálogo para um projeto aninhado, o projeto pai pode controlar quais itens são exibidos na caixa de diálogo.  
  
 O <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2> interface lhe permite filtrar os nós que estarão em um **AddItem** caixa de diálogo. Quando o projeto filho exibe a **AddItem** caixa de diálogo, o pai pode implementar o `IVsFilterAddProjectItemDlg` interface e filtrar itens que seriam exibidos no projeto de seu filho.  
  
 Quando os projetos são agrupados por função em projetos pai específico, você pode implementar `IVsFilterAddProjectItemDlg` quando o usuário seleciona **Adicionar Item de projeto** no menu de atalho em um projeto aninhado. Implementando `IvsFilterAddProjectItemDlg displays` somente projeto itens ou específico a esse grupo de arquivos. Itens de projeto para outros grupos são filtradas fora da caixa de diálogo, mesmo se eles são armazenados no mesmo diretório.  
  
 Quando um usuário abre o **AddItem** filho, a implementação do projeto pai da caixa de diálogo de `IVsFilterAddProjectItemDlg` interface é chamado.  
  
 O `IVsFilterAddProjectItemDlg` interface também pode implementar a filtragem por categoria. Para obter mais informações, consulte [adicionar itens à caixa de diálogo Adicionar Novo Item](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md) e [registrar modelos de projeto e item](../../extensibility/internals/registering-project-and-item-templates.md).  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>   
 [Adicionar itens à caixa de diálogo Adicionar Novo Item](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)   
 [Registrar os modelos de projeto e de item](../../extensibility/internals/registering-project-and-item-templates.md)   
 [Projetos de aninhamento](../../extensibility/internals/nesting-projects.md)