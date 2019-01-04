---
title: 'Como: Usar itens de coloração internos | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- colorable items
- language services, built-in colorable items
ms.assetid: 5e5f3436-6bad-4fd2-8823-6a30353ba648
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: f0884ecd265522b2b0f2a222e12cb01c34c7e8c3
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2019
ms.locfileid: "53947290"
---
# <a name="how-to-use-built-in-colorable-items"></a>Como: Usar itens de coloração internos
Antes de usar os itens de coloração internos, você deve primeiro sinalizar para o ambiente de desenvolvimento integrado (IDE) que você não está fornecendo seus próprios itens de coloração personalizados, que nesse caso, seria <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems> objetos. Você pode fazer isso definindo uma entrada de registro para o serviço de linguagem.  
  
## <a name="to-use-built-in-colorable-items"></a>Usar itens de coloração internos  
  
1. Sob **HKEY_LOCAL_MACHINE\VisualStudio\\< x. y > Serviços de \Languages\Language\\< nome do idioma\>**, onde \<x. y > é uma versão de [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] e \<Nome do idioma > é o nome do seu idioma, crie um valor de entrada de Registro DWORD denominado **RequestStockColors**.  
  
2. Defina as **RequestStockColors** valor de entrada de registro para *1*.  
  
    Depois de criar a entrada de registro, seu colorizador <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> método pode usar os membros do <xref:Microsoft.VisualStudio.TextManager.Interop.DEFAULTITEMS> enumeração para preencher a matriz de atributos de cor para uso pelo editor.  
  
   > [!NOTE]
   >  Não defina essa entrada de registro se você estiver fornecendo itens de coloração personalizados. Para obter mais informações, consulte [itens de coloração personalizados](../../extensibility/internals/custom-colorable-items.md).  
  
## <a name="see-also"></a>Consulte também  
 [Coloração de sintaxe em editores personalizados](../../extensibility/syntax-coloring-in-custom-editors.md)   
 [Coloração de sintaxe em um serviço de linguagem herdado](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)   
 [Implementando a coloração de sintaxe](../../extensibility/internals/implementing-syntax-coloring.md)   
 [Itens de coloração personalizados](../../extensibility/internals/custom-colorable-items.md)   
 [Registrar um serviço de linguagem herdado](../../extensibility/internals/registering-a-legacy-language-service2.md)