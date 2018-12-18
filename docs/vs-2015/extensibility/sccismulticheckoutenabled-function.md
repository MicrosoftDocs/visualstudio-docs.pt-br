---
title: Função SccIsMultiCheckoutEnabled | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- SccIsMultiCheckoutEnabled
helpviewer_keywords:
- SccIsMultiCheckoutEnabled function
ms.assetid: 6721639d-e475-4766-81b5-ee40a280fc70
caps.latest.revision: 14
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: e449ab110b4087f2c7e997b92d66f62f7bd780f8
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51769413"
---
# <a name="sccismulticheckoutenabled-function"></a>Função SccIsMultiCheckoutEnabled
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Essa função verifica se o plug-in de controle do código-fonte permite vários check-outs em um arquivo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
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

