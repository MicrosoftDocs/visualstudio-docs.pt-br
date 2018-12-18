---
title: Função SccIsMultiCheckoutEnabled | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- SccIsMultiCheckoutEnabled
helpviewer_keywords:
- SccIsMultiCheckoutEnabled function
ms.assetid: 6721639d-e475-4766-81b5-ee40a280fc70
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: e4a71f839c2129bcfb699188dec09b02b18d4cd1
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49920112"
---
# <a name="sccismulticheckoutenabled-function"></a>Função SccIsMultiCheckoutEnabled
Essa função verifica se o plug-in de controle do código-fonte permite vários check-outs em um arquivo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
SCCRTN SccIsMultiCheckoutEnabled(  
   LPVOID pContext,  
   LPBOOL pbMultiCheckout  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 pContext  
 [in] A estrutura de contexto de plug-in de controle de origem.  
  
 pbMultiCheckout  
 [out] Especifica se vários check-outs estão habilitadas para este projeto (diferente de zero significa que vários check-outs têm suporte).  
  
## <a name="return-value"></a>Valor de retorno  
 A implementação de plug-in de controle do código-fonte desta função deve retornar um dos seguintes valores:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SCC_OK|A verificação foi bem-sucedida.|  
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|Falha não específica.|  
  
## <a name="remarks"></a>Comentários  
 O IDE faz duas verificações para determinar se arquivos podem fazer check-out simultaneamente por mais de um usuário. Primeiro, o sistema de controle do código-fonte deve oferecer suporte a vários check-outs. O plug-in de controle de origem pode especificar esse recurso durante a inicialização, especificando o `SCC_CAP_MULTICHECKOUT`. Depois disso, como uma segunda verificação, o IDE chama essa função para determinar se o projeto atual dá suporte a vários check-outs. Se vários check-outs têm suporte para o projeto selecionado, a plug-in retorna um sucesso de código e definirá `pbMultiCheckout` como não zero (`TRUE`) ou `FALSE`.  
  
## <a name="see-also"></a>Consulte também  
 [Funções de API do plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)