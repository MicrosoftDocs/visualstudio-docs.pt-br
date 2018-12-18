---
title: Considerações para descarregar e recarregar projetos de aninhados | Microsoft Docs
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
- nested projects, unloading and reloading
- projects [Visual Studio SDK], unloading and reloading nested
ms.assetid: 06c3427e-c874-45b1-b9af-f68610ed016c
caps.latest.revision: 13
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 28c5ba7dffecd73556a5f963c471910bb190f1db
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51756971"
---
# <a name="considerations-for-unloading-and-reloading-nested-projects"></a>Considerações para descarregar e recarregar projetos aninhados
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Quando você implementa os tipos de projeto aninhado, você deve executar etapas adicionais quando você descarrega e recarregar os projetos. Para notificar os ouvintes de eventos de solução corretamente, você deverá gerar corretamente os `OnBeforeUnloadProject` e `OnAfterLoadProject` eventos.  
  
 Um motivo que você deve criar esses eventos dessa maneira é que você não deseja que o controle do código fonte (SCC) para excluir os itens do servidor e, em seguida, adicioná-los de volta como algo novo se não houver um `Get` operação do SCC. Nesse caso, um novo arquivo seria carregado fora de SCC e você tem que descarregar e recarregar todos os arquivos, caso sejam diferentes. Chamadas de SCC `ReloadItem`. A implementação dessa chamada é excluir o projeto e recriá-la novamente com a implementação `IVsFireSolutionEvents` chamar `OnBeforeUnloadProject` e `OnAfterLoadProject`. Quando você executa essa implementação, o SCC é informado de que o projeto foi excluído e adicionado novamente temporariamente. Portanto, o SCC não funcionará no projeto como se o projeto foi realmente excluído do servidor e, em seguida, adicionado novamente.  
  
## <a name="reloading-projects"></a>Recarregar projetos  
 Para dar suporte a recarregamento de projetos aninhados, você deve implementar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.ReloadItem%2A> método. Em sua implementação de `ReloadItem`, feche os projetos aninhados e, em seguida, recriá-los.  
  
 Normalmente quando um projeto é recarregado, o IDE gera o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnBeforeUnloadProject%2A> e o `M:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterLoadProject(Microsoft.VisualStudio.Shell.Interop.IVsHierarchy,Microsoft.VisualStudio.Shell.Interop.IVsHierarchy)` eventos. No entanto, para projetos aninhados que serão excluídos e recarregados, o projeto pai inicia o processo, não do IDE. Como o projeto pai não gera eventos de solução, e o IDE não possui informações sobre a inicialização do processo, os eventos não são gerados.  
  
 Para lidar com esse processo, as chamadas de projeto pai `QueryInterface` sobre o <xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents> fora da interface a <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution> interface. `IVsFireSolutionEvents` tem funções que mandar o IDE para gerar o `OnBeforeUnloadProject` evento para descarregar o projeto aninhado e, em seguida, gerar o `OnAfterLoadProject` evento para recarregar o projeto mesmo.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3>   
 [Aninhar projetos](../../extensibility/internals/nesting-projects.md)

