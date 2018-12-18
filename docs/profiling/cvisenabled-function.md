---
title: Função CvIsEnabled | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- cvmarkers/CvIsEnabledEx
- cvmarkers/CvIsEnabled
helpviewer_keywords:
- CvIsEnabled method
- CvIsEnabledEx method
ms.assetid: 2e4fea6d-758d-4150-8744-6102a1d58c1c
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 1555703c92695090a3c8ac7b04e7a35dadcd7627
ms.sourcegitcommit: 58052c29fc61c9a1ca55a64a63a7fdcde34668a4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34749194"
---
# <a name="cvisenabled-function"></a>Função CvIsEnabled
Determina se uma sessão habilitou o provedor ETW especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```C  
HRESULT CvIsEnabled(  
   _In_ PCV_PROVIDER pProvider  
);  
HRESULT CvIsEnabledEx(  
   _In_ PCV_PROVIDER pProvider,  
   _In_ CV_IMPORTANCE level,  
   _In_ int category  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `category`  
 Categoria.  
  
 `level`  
 Nível de importância.  
  
 `pProvider`  
 Objeto de provedor válido. Não pode ser NULL.  
  
## <a name="return-value"></a>Valor retornado  
 S_OK se o provedor estiver habilitado no momento. S_FALSE se o provedor estiver desabilitado no momento. Código de erro em caso de erros. Use a macro FAILED para verificar a condição de erro e depois verifique se S_OK/S_FALSE.  
  
## <a name="requirements"></a>Requisitos  
 **Cabeçalho:** *cvmarkers.h*  
  
## <a name="see-also"></a>Consulte também  
 [Referência de biblioteca C++](../profiling/cpp-library-reference.md)