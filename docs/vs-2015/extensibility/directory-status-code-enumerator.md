---
title: Enumerador de código de Status de diretório | Microsoft Docs
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
- directory status code enumerator
- source control plug-ins, directory status enumeration
ms.assetid: 616026b5-f529-40ef-90c1-1836e116d797
caps.latest.revision: 14
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 6a23bef10dda57d761ce7f07c3b87808b021830c
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51766672"
---
# <a name="directory-status-code-enumerator"></a>Enumerador de código de status do diretório
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O `SccDirStatus` enumerador contém valores constantes nomeados que especificam o estado de um diretório no sistema de controle de origem. Essa enumeração é usada pelo [SccDirQueryInfo](../extensibility/sccdirqueryinfo-function.md). Essa foi introduzida na versão 1.2 do que a API de plug-in de controle do código-fonte.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
enum SccDirStatus {  
   SCC_DIRSTATUS_INVALID       = -1L,  
   SCC_DIRSTATUS_NOTCONTROLLED = 0x0000L,  
   SCC_DIRSTATUS_CONTROLLED    = 0x0001L,  
   SCC_DIRSTATUS_EMPTYPROJ     = 0x0002L  
};  
```  
  
## <a name="members"></a>Membros  
 SCC_DIRSTATUS_INVALID  
 Não foi possível obter o status; Não confie nele.  
  
 SCC_DIRSTATUS_NOTCONTROLLED  
 Diretório não está sob controle do código-fonte.  
  
 SCC_DIRSTATUS_CONTROLLED  
 Diretório está sob controle de origem.  
  
 SCC_DIRSTATUS_EMPTYPROJ  
 Projeto correspondente a esse diretório está vazio.  
  
## <a name="see-also"></a>Consulte também  
 [Plug-ins de controle de origem](../extensibility/source-control-plug-ins.md)   
 [SccDirQueryInfo](../extensibility/sccdirqueryinfo-function.md)

