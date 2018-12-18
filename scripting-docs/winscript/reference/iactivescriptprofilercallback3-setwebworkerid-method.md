---
title: Método IActiveScriptProfilerCallback3::SetWebWorkerId | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 47744746-1276-441e-ab60-2a78f550e8e2
caps.latest.revision: 3
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 426767b8d4d23964d6bfaa7102ee53b550e7ab9b
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24724606"
---
# <a name="iactivescriptprofilercallback3setwebworkerid-method"></a>Método IActiveScriptProfilerCallback3::SetWebWorkerId
Notifica o criador de perfil sobre a ID do trabalho a ser usado para esta sessão de criação de perfil. Se a função não está em execução no contexto da página, esse método não é invocado. O valor de `webWorkerId` aumenta em incrementos de 1 para cada funcionário, começando em 1. Os valores de ID não devem ser estável, além de uma sessão e correspondem somente à ordem em que os trabalhadores são criados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT SetWebWorkerId([in] DWORD webWorkerId);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `webWorkerId`  
 A ID do trabalho da web.  
  
## <a name="return-value"></a>Valor de retorno  
 O valor de retorno desse método é ignorado pelo mecanismo de script.