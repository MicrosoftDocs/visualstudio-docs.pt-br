---
title: Contexto de documento | Microsoft Docs
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
- debugging [Debugging SDK], contexts
ms.assetid: 8e8b5702-5c16-4988-953d-69dd807d8b84
caps.latest.revision: 11
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: c5753e2353b351f6aa4bd73c5aced3d4959b3cde
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51741187"
---
# <a name="document-context"></a>Contexto do documento
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Na [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] depuração, um **contexto de documento**:  
  
-   Representa uma posição em um arquivo de origem. Para os idiomas em que o arquivo de origem não pode estar presente, um contexto de documento identifica uma posição em um documento gerado normalmente pelo ambiente de tempo de execução. Por exemplo, um mecanismo de script pode gerar um documento de script. Para obter mais informações, consulte [posição do documento](../../extensibility/debugger/document-position.md).  
  
-   Descreve uma posição em um documento de origem que corresponde a um contexto de código. O manipulador de símbolo mapeia um contexto de código ao contexto da documentação, usando as informações geradas por um compilador ou interpretador.  
  
-   É implementado por uma [IDebugDocumentContext2](../../extensibility/debugger/reference/idebugdocumentcontext2.md) interface.  
  
## <a name="see-also"></a>Consulte também  
 [Contexto de código](../../extensibility/debugger/code-context.md)   
 [Provedor de símbolos](../../extensibility/debugger/symbol-provider.md)   
 [Interfaces de provedor de símbolos](../../extensibility/debugger/reference/symbol-provider-interfaces.md)   
 [Contextos do depurador](../../extensibility/debugger/debugger-contexts.md)

