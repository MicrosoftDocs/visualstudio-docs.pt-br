---
title: Função CvInitProvider | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- cvmarkers/CvInitProvider
helpviewer_keywords:
- CvInitProvider method
ms.assetid: ba1863ad-e35f-4d34-a2f2-5e68957d1915
caps.latest.revision: 8
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a41e7fe1a6da619e926301b0e1a9b99803fc6d67
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51798294"
---
# <a name="cvinitprovider-function"></a>Função CvInitProvider
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Inicializa o provedor de marcador. Deve ser chamado antes das outras funções do SDK da Visualização Simultânea.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT CvInitProvider(  
   _In_ const GUID* pGuid,  
   _Out_ PCV_PROVIDER* ppProvider  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pGuid`  
 GUID do provedor. Não pode ser NULL.  
  
 `ppProvider`  
 Endereço de uma variável de saída que armazenará o contexto de provedor. Não pode ser NULL.  
  
## <a name="return-value"></a>Valor de retorno  
 S_OK quando o provedor é inicializado com êxito ou código de erro no caso de erros. Use as macros SUCCEEDED/FAILED para verificar a condição de erro.  
  
## <a name="requirements"></a>Requisitos  
 **Cabeçalho:** cvmarkers.h  
  
## <a name="see-also"></a>Consulte também  
 [Referência de biblioteca C++](../profiling/cpp-library-reference.md)



