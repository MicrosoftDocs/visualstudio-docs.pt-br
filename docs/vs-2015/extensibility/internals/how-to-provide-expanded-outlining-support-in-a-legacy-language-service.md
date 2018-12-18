---
title: 'Como: fornecer suporte expandido de estrutura de tópicos em um serviço de linguagem herdado | Microsoft Docs'
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
- editors [Visual Studio SDK], outlining support
- language services, supporting outlining
- outlining, supporting
ms.assetid: df759e89-8193-418c-8038-6626304d387b
caps.latest.revision: 17
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 56d125cdfc3cbdbbc880e1e8a98136eb20e07df1
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51774205"
---
# <a name="how-to-provide-expanded-outlining-support-in-a-legacy-language-service"></a>Como: fornecer suporte expandido de estrutura de tópicos em um serviço de linguagem herdado
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Há duas opções para estender a estrutura de tópicos de suporte para seu idioma além do suporte a **recolher para definições de** comando. Você pode adicionar regiões controlado pelo editor de estrutura de tópicos e adicionar regiões de estrutura de tópicos controlado pelo cliente.  
  
## <a name="adding-editor-controlled-outline-regions"></a>Adicionar regiões controlado pelo Editor de estrutura de tópicos  
 Use essa abordagem para criar uma região de estrutura de tópicos e, em seguida, permitir que o editor para manipular se a região é expandida, recolhido e assim por diante. As duas opções para fornecer suporte de estrutura de tópicos, essa opção é menos eficiente. Para essa opção, você deve criar uma nova região de estrutura de tópicos em um intervalo especificado de texto usando <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession.AddOutlineRegions%2A>. Depois que essa região é criado, seu comportamento é controlado pelo editor. Use o procedimento a seguir para implementar regiões controlado pelo editor.  
  
#### <a name="to-implement-an-editor-controlled-outline-region"></a>Para implementar uma região controlado pelo editor de estrutura de tópicos  
  
1.  Chamar `QueryService` para <xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager>  
  
     Isso retorna um ponteiro para <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager>.  
  
2.  Chamar <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.GetHiddenTextSession%2A>, passando um ponteiro para um buffer de texto especificado. Isso retorna um ponteiro para o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession> objeto para o buffer.  
  
3.  Chame <xref:System.Runtime.InteropServices.Marshal.QueryInterface%2A> na <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession> de um ponteiro para <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession>.  
  
4.  Chamar <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession.AddOutlineRegions%2A> para adicionar um ou mais novas regiões de estrutura de tópicos por vez.  
  
     Esse método permite que você especifique o intervalo de texto para a estrutura de tópicos, se as regiões de estrutura de tópicos existentes são removidos ou preservadas, e se a região de estrutura de tópicos é expandida ou recolhida por padrão.  
  
## <a name="adding-client-controlled-outline-regions"></a>Adicionar regiões de estrutura de tópicos controlado pelo cliente  
 Use essa abordagem para implementar controlado pelo cliente (ou inteligente) de estrutura de tópicos do tipo usado pelas [!INCLUDE[csprcs](../../includes/csprcs-md.md)] e [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] serviços de linguagem. Um serviço de linguagem que gerencia sua própria estrutura de tópicos monitora o conteúdo do buffer de texto para ser destruída antigo regiões de estrutura de tópicos quando eles se torna inválido e criar novas regiões de estrutura de tópicos, conforme necessário.  
  
#### <a name="to-implement-a-client-controlled-outline-region"></a>Para implementar uma região de estrutura de tópicos controlado pelo cliente  
  
1.  Chame `QueryService` para <xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager>. Isso retorna um ponteiro para <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager>.  
  
2.  Chamar <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.GetHiddenTextSession%2A>, passando um ponteiro para um buffer de texto especificado. Isso determina se o texto oculto já existe uma sessão para o buffer.  
  
3.  Se o texto já existe uma sessão, então você não precisará criar um e um ponteiro para existente <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession> objeto é retornado. Use esse ponteiro para enumerar e criar regiões de estrutura de tópicos. Caso contrário, chame <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.CreateHiddenTextSession%2A> para criar uma sessão para o buffer de texto oculto. Um ponteiro para o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession> objeto é retornado.  
  
    > [!NOTE]
    >  Quando você chama <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.CreateHiddenTextSession%2A>, você pode especificar um cliente do texto oculto (ou seja, um <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextClient> objeto). Esse cliente notifica você quando um texto oculto ou região de estrutura de tópicos é expandida ou recolhida pelo usuário.  
  
4.  Chamar <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession.AddHiddenRegions%2A> estrutura) parâmetro: Especifique um valor de <xref:Microsoft.VisualStudio.TextManager.Interop.HIDDEN_REGION_TYPE> na `iType` membro o <xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion> estrutura para indicar que você está criando uma região de estrutura de tópicos, em vez de uma região oculta. Especifique se a região é controlado pelo cliente ou controlado de editor do `dwBehavior` membro o <xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion> estrutura. Sua implementação de estrutura de tópicos inteligente pode conter uma mistura de regiões de estrutura de tópicos de editor-controlado pelo cliente. Especificar o texto do banner é exibido quando a sua região de estrutura de tópicos é recolhida, como "...", além de `pszBanner` membro do <xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion> estrutura. Texto da faixa do editor padrão para uma região oculta é ""....

