---
title: Fornecer suporte em um serviço de linguagem da estrutura de tópicos | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], outlining support
- language services, supporting outlining
- outlining, supporting
ms.assetid: df759e89-8193-418c-8038-6626304d387b
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 31ae8a6aeba28fbe90e68305f2b48021b4327c26
ms.sourcegitcommit: 206e738fc45ff8ec4ddac2dd484e5be37192cfbd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39511373"
---
# <a name="how-to-provide-expanded-outlining-support-in-a-legacy-language-service"></a>Como: fornecer suporte expandido de estrutura de tópicos em um serviço de linguagem herdado
Há duas opções para estender a estrutura de tópicos de suporte para seu idioma além do suporte a **recolher para definições de** comando. Você pode adicionar regiões controlado pelo editor de estrutura de tópicos e adicionar regiões de estrutura de tópicos controlado pelo cliente.  
  
## <a name="adding-editor-controlled-outline-regions"></a>Adicionar regiões controlado pelo editor de estrutura de tópicos  
 Use essa abordagem para criar uma região de estrutura de tópicos e, em seguida, permitir que o editor para manipular se a região é expandida, recolhido e assim por diante. As duas opções para fornecer suporte de estrutura de tópicos, essa opção é menos eficiente. Para essa opção, você deve criar uma nova região de estrutura de tópicos em um intervalo especificado de texto usando <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession.AddOutlineRegions%2A>. Depois que essa região é criado, seu comportamento é controlado pelo editor. Use o procedimento a seguir para implementar regiões controlado pelo editor.  
  
### <a name="to-implement-an-editor-controlled-outline-region"></a>Para implementar uma região controlado pelo editor de estrutura de tópicos  
  
1.  Chamar `QueryService` para <xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager>  
  
     Isso retorna um ponteiro para <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager>.  
  
2.  Chamar <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.GetHiddenTextSession%2A>, passando um ponteiro para um buffer de texto especificado. Isso retorna um ponteiro para o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession> objeto para o buffer.  
  
3.  Chame <xref:System.Runtime.InteropServices.Marshal.QueryInterface%2A> na <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession> de um ponteiro para <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession>.  
  
4.  Chamar <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession.AddOutlineRegions%2A> para adicionar um ou mais novas regiões de estrutura de tópicos por vez.  
  
     Esse método permite que você especifique o intervalo de texto para a estrutura de tópicos, se as regiões de estrutura de tópicos existentes são removidos ou preservadas, e se a região de estrutura de tópicos é expandida ou recolhida por padrão.  
  
## <a name="add-client-controlled-outline-regions"></a>Adicionar regiões de estrutura de tópicos controlado pelo cliente  
 Use essa abordagem para implementar controlado pelo cliente (ou inteligente) de estrutura de tópicos do tipo usado pelas [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] e [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] serviços de linguagem. Um serviço de linguagem que gerencia sua própria estrutura de tópicos monitora o conteúdo do buffer de texto para ser destruída antigo regiões de estrutura de tópicos quando eles se tornam inválidos e criar novas regiões de estrutura de tópicos, conforme necessário.  
  
### <a name="to-implement-a-client-controlled-outline-region"></a>Para implementar uma região de estrutura de tópicos controlado pelo cliente  
  
1.  Chame `QueryService` para <xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager>. Isso retorna um ponteiro para <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager>.  
  
2.  Chamar <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.GetHiddenTextSession%2A>, passando um ponteiro para um buffer de texto especificado. Isso determina se o texto oculto já existe uma sessão para o buffer.  
  
3.  Se o texto já existe uma sessão, então você não precisará criar um e um ponteiro para existente <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession> objeto é retornado. Use esse ponteiro para enumerar e criar regiões de estrutura de tópicos. Caso contrário, chame <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.CreateHiddenTextSession%2A> para criar uma sessão para o buffer de texto oculto. Um ponteiro para o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession> objeto é retornado.  
  
    > [!NOTE]
    >  Quando você chama <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.CreateHiddenTextSession%2A>, você pode especificar um cliente do texto oculto (ou seja, um <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextClient> objeto). Esse cliente notifica você quando um texto oculto ou região de estrutura de tópicos é expandida ou recolhida pelo usuário.  
  
4.  Chamar <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession.AddHiddenRegions%2A> estrutura) parâmetro: Especifique um valor de <xref:Microsoft.VisualStudio.TextManager.Interop.HIDDEN_REGION_TYPE> na `iType` membro o <xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion> estrutura para indicar que você está criando uma região de estrutura de tópicos, em vez de uma região oculta. Especifique se a região é controlado pelo cliente ou controlado de editor do `dwBehavior` membro o <xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion> estrutura. Sua implementação de estrutura de tópicos inteligente pode conter uma mistura de regiões de estrutura de tópicos de editor-controlado pelo cliente. Especificar o texto do banner é exibido quando a sua região de estrutura de tópicos é recolhida, como "...", além de `pszBanner` membro do <xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion> estrutura. Texto da faixa do editor padrão para uma região oculta é ""....