---
title: SetThreadCount | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: msbuild
ms.topic: reference
apiname:
- SetThreadCount
apilocation:
- filetracker.dll
apitype: COM
helpviewer_keywords:
- SetThreadCount
ms.assetid: 335335a5-8ca0-4e18-95f5-62aa6a691386
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 9cc9a1ae5f7fb51981f3cebc4d6fa658f614de6d
ms.sourcegitcommit: 0e5289414d90a314ca0d560c0c3fe9c88cb2217c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2018
ms.locfileid: "39151834"
---
# <a name="setthreadcount"></a>SetThreadCount
Define a contagem de thread global e atribui valores para o thread atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```cmd  
HRESULT WINAPI SetThreadCount(int threadCount);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 [in] `threadCount`  
 O número máximo de threads.  
  
## <a name="return-value"></a>Valor retornado  
 Um **HRESULT** com o conjunto de bit **SUCCEEDED** se a contagem de thread foi atualizada.  
  
## <a name="requirements"></a>Requisitos  
 **Cabeçalho:** *FileTracker.h*