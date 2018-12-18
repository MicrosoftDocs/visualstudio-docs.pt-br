---
title: IApplicationDebuggerUI::BringDocumentContextToTop | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IApplicationDebuggerUI.BringDocumentContextToTop
apilocation:
- scrobj.dll
helpviewer_keywords:
- IApplicationDebuggerUI::BringDocumentContextToTop
ms.assetid: 7844217d-658b-42af-8d10-2714f4eded20
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 2fab017ab286957cf2c4be35832b1db877b339bd
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24725276"
---
# <a name="iapplicationdebuggeruibringdocumentcontexttotop"></a>IApplicationDebuggerUI::BringDocumentContextToTop
Coloca a janela que contém o contexto do documento fornecido na parte superior na interface de usuário do depurador e rolar a janela para o contexto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT BringDocumentContextToTop(  
   IDebugDocumentContext*  pddc  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pddc`  
 [in] Contexto de documento para colocar no início na interface de usuário do depurador.  
  
## <a name="return-value"></a>Valor de retorno  
 O método retorna um `HRESULT`. Os possíveis valores incluem, mas sem limitação, aqueles na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`S_OK`|O método foi bem-sucedido.|  
|`E_INVALIDARG`|O contexto especificado pelos `pddc` não é conhecido.|  
  
## <a name="remarks"></a>Comentários  
 Este método coloca a janela que contém o contexto do documento fornecido na parte superior na interface de usuário do depurador e rola a janela para o contexto.  
  
## <a name="see-also"></a>Consulte também  
 [IApplicationDebuggerUI Interface](../../winscript/reference/iapplicationdebuggerui-interface.md)