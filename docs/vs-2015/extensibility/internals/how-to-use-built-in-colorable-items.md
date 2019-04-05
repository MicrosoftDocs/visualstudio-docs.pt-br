---
title: 'Como: Usar itens de coloração internos | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- colorable items
- language services, built-in colorable items
ms.assetid: 5e5f3436-6bad-4fd2-8823-6a30353ba648
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2546d9e9c864772bf1a2d3063e8ce4adc1cd7605
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "58926784"
---
# <a name="how-to-use-built-in-colorable-items"></a>Como: Usar itens internos que podem ser coloridos
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Antes de usar os itens de coloração internos, você deve primeiro sinalizar para o ambiente de desenvolvimento integrado (IDE) que você não está fornecendo seus próprios itens de coloração personalizados, que nesse caso, seria <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems> objetos. Você pode fazer isso definindo uma entrada de registro para o serviço de linguagem.  
  
### <a name="to-use-built-in-colorable-items"></a>Usar itens de coloração internos  
  
1.  Em HKEY_LOCAL_MACHINE\VisualStudio\\*x. y*\Languages\Language serviços\\*nome do idioma*, onde *x. y* é uma versão do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] e *nome do idioma* é o nome do seu idioma, crie um valor de entrada do Registro DWORD chamado `RequestStockColors`.  
  
2.  Defina o `RequestStockColors` valor de entrada do registro como 1.  
  
     Depois de criar a entrada de registro, seu colorizador <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> método pode usar os membros do <xref:Microsoft.VisualStudio.TextManager.Interop.DEFAULTITEMS> enumeração para preencher a matriz de atributos de cor para uso pelo editor.  
  
    > [!NOTE]
    >  Não defina essa entrada de registro se você estiver fornecendo itens de coloração personalizados. Para obter mais informações, consulte [itens de coloração personalizados](../../extensibility/internals/custom-colorable-items.md).  
  
## <a name="see-also"></a>Consulte também  
 [Coloração de sintaxe em editores personalizados](../../extensibility/syntax-coloring-in-custom-editors.md)   
 [Coloração de sintaxe em um serviço de linguagem herdado](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)   
 [Implementando a coloração de sintaxe](../../extensibility/internals/implementing-syntax-coloring.md)   
 [Itens de coloração personalizados](../../extensibility/internals/custom-colorable-items.md)   
 [Registrar um serviço de linguagem herdado](../../extensibility/internals/registering-a-legacy-language-service2.md)
