---
title: Suporte do Assistente para projetos aninhados | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Add Item wizard
- nested projects, wizard support
- New Project wizard
ms.assetid: 1b496acc-b326-4cdb-bb48-e3b5c6f12e05
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 14e8a32db2542ae1729a7fdc87cc2ab32845f8ca
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31137489"
---
# <a name="wizard-support-for-nested-projects"></a>Suporte do Assistente para projetos aninhados
O IDE executa dois assistentes que o projeto pai para projetos aninhados pode implementar: o **novo projeto** assistente e o **Adicionar Item** assistente.  
  
 Se um usuário inicia o **novo projeto** assistente selecionando **Adicionar projeto** e clicando em **novo projeto** no menu arquivo ou selecionando **adicionar** e o botão direito do mouse **novo projeto** no Gerenciador de soluções, o IDE executa o **AddProject** comando e a implementação do projeto do pai o **AddProject**comando retorna ou um arquivo de projeto de modelo ou um arquivo de assistente (. vsz) que tem um conjunto de parâmetros de contexto.  
  
 Da mesma forma, a implementação do projeto de um pai de **AddItem** assistentes retorna um arquivo. vsz que tem um conjunto diferente de parâmetros de contexto.  
  
 Para obter mais informações sobre assistentes, consulte [Assistente (. Arquivo vsz)](../../extensibility/internals/wizard-dot-vsz-file.md), [parâmetros de contexto](../../extensibility/internals/context-parameters.md) e [registrar os modelos de projeto e Item](../../extensibility/internals/registering-project-and-item-templates.md).  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>   
 [Aninhar projetos](../../extensibility/internals/nesting-projects.md)