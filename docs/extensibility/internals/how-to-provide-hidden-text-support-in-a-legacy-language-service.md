---
title: 'Como: fornecer suporte a texto oculto em um serviço de linguagem herdado | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- hidden text, supporting
- editors [Visual Studio SDK], hidden text
- language services, implementing hidden text regions
ms.assetid: 1c1dce9f-bbe2-4fc3-a736-5f78a237f4cc
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: d368caaa9b65f6f9ab8b12c1f49994e3bfe16670
ms.sourcegitcommit: 206e738fc45ff8ec4ddac2dd484e5be37192cfbd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39511954"
---
# <a name="how-to-provide-hidden-text-support-in-a-legacy-language-service"></a>Como: texto oculto de fornecer suporte a um serviço de linguagem herdado
Você pode criar regiões de texto oculto além das regiões de estrutura de tópicos. Regiões de texto oculta podem ser controlado pelo cliente ou controlado pelo editor e são usados para ocultar uma região de texto completo. O editor exibe uma região oculta como linhas horizontais. Um exemplo disso é o **somente Script** exibição no editor de HTML.  
  
  
## <a name="to-implement-a-hidden-text-region"></a>Para implementar uma região de texto oculto  
  
1.  Chame `QueryService` para <xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager>.  
  
     Isso retorna um ponteiro para <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager>.  
  
2.  Chamar <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.GetHiddenTextSession%2A>, passando um ponteiro para um buffer de texto especificado. Isso determina se o texto oculto já existe uma sessão para o buffer.  
  
3.  Se já existir um, então você não precisará criar um e um ponteiro para existente <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession> objeto é retornado. Use esse ponteiro para enumerar e criar regiões de texto oculto. Caso contrário, chame <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.CreateHiddenTextSession%2A> para criar uma sessão para o buffer de texto oculto.  
  
     Um ponteiro para o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession> objeto é retornado.  
  
    > [!NOTE]
    >  Quando você chama `CreateHiddenTextSession`, você pode especificar um cliente do texto oculto (ou seja, <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextClient>). O cliente do texto oculto notifica quando o texto oculto ou estrutura de tópicos é expandida ou recolhida pelo usuário.  
  
4.  Chame <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession.AddHiddenRegions%2A> para adicionar um ou mais nova da estrutura de tópicos regiões ao mesmo tempo, especificando as seguintes informações na `reHidReg` (<xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion>) parâmetro:  
  
    1.  Especifique um valor de `hrtConcealed` no `iType` membro o <xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion> estrutura para indicar que você está criando uma região oculta, em vez de uma região de estrutura de tópicos.  
  
        > [!NOTE]
        >  Quando regiões escondidos estiverem ocultas, o editor exibe automaticamente linhas ao redor das regiões ocultas para indicar sua presença.  
  
    2.  Especifique se a região é controlado pelo cliente ou controlado de editor do `dwBehavior` os membros a <xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion> estrutura. Sua implementação de estrutura de tópicos inteligente pode conter uma mistura de estrutura de tópicos do editor-controlado pelo cliente e regiões de texto oculto.