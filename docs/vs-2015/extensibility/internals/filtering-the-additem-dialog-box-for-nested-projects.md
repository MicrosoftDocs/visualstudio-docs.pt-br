---
title: A caixa de diálogo Adicionar item de filtragem para projetos aninhados | Microsoft Docs
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
- filtering, nested projects
- nested projects, AddItem dialog box filtering
ms.assetid: 5b3e352e-7f18-4f66-be16-b0ad55637ce5
caps.latest.revision: 13
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 363ba8e38ae2de445bd18bb9378d48aa4d824298
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51769768"
---
# <a name="filtering-the-additem-dialog-box-for-nested-projects"></a>Filtrando a caixa de diálogo AddItem para projetos aninhados
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Quando você exibe um **AddItem** caixa de diálogo para um projeto aninhado, o projeto pai pode controlar quais itens são exibidos na caixa de diálogo.  
  
 O <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2> interface lhe permite filtrar os nós que estarão em um **AddItem** caixa de diálogo. Quando o projeto filho exibe a **AddItem** caixa de diálogo, o pai pode implementar o `IVsFilterAddProjectItemDlg` interface e filtrar itens que seriam exibidos no projeto de seu filho.  
  
 Quando os projetos são agrupados por função em projetos pai específico, você pode implementar `IVsFilterAddProjectItemDlg` quando o usuário seleciona **Adicionar Item de projeto** no menu de atalho em um projeto aninhado. Implementando `IvsFilterAddProjectItemDlg displays` somente projeto itens ou específico a esse grupo de arquivos. Itens de projeto para outros grupos são filtradas fora da caixa de diálogo, mesmo se eles são armazenados no mesmo diretório.  
  
 Quando um usuário abre o **AddItem** filho, a implementação do projeto pai da caixa de diálogo de `IVsFilterAddProjectItemDlg` interface é chamado.  
  
 O `IVsFilterAddProjectItemDlg` interface também pode implementar a filtragem por categoria. Para obter mais informações, consulte [adicionando itens para as caixas de diálogo Adicionar Novo Item](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md) e [registrar modelos de projeto e Item](../../extensibility/internals/registering-project-and-item-templates.md).  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>   
 [Adição de itens para a adicionar novo Item caixas de diálogo](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)   
 [Registrar modelos de projeto e Item](../../extensibility/internals/registering-project-and-item-templates.md)   
 [Aninhar projetos](../../extensibility/internals/nesting-projects.md)

