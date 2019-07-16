---
title: OPTNAMECHANGEPFN | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- OPTNAMECHANGEPFN
helpviewer_keywords:
- OPTNAMECHANGEPFN callback function
ms.assetid: 147303f3-c7f1-438a-81b7-db891ea3d076
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4969dff811b6517c0274a35884703a9dc0c693cb
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "68194098"
---
# <a name="optnamechangepfn"></a>OPTNAMECHANGEPFN
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Essa é uma função de retorno de chamada especificada em uma chamada para o [SccSetOption](../extensibility/sccsetoption-function.md) (usando a opção `SCC_OPT_NAMECHANGEPFN`) e é usado para comunicar alterações de nome feitas pelo controle de fonte de plug-in voltar ao IDE.  
  
## <a name="signature"></a>Assinatura  
  
```cpp#  
typedef void (*OPTNAMECHANGEPFN)(  
   LPVOID pvCallerData,  
   LPCSTR pszOldName,  
   LPCSTR pszNewName  
);  
```  
  
## <a name="parameters"></a>Parâmetros  
 pvCallerData  
 [in] Valor de usuário especificado em uma chamada anterior para o [SccSetOption](../extensibility/sccsetoption-function.md) (usando a opção `SCC_OPT_USERDATA`).  
  
 pszOldName  
 [in] O nome original do arquivo.  
  
 pszNewName  
 [in] O nome do arquivo foi renomeado para.  
  
## <a name="return-value"></a>Valor de retorno  
 nenhuma.  
  
## <a name="remarks"></a>Comentários  
 Se um arquivo é renomeado durante uma operação de controle do código-fonte, o plug-in de controle do código-fonte pode notificar o IDE sobre a alteração de nome por meio desse retorno de chamada.  
  
 Se o IDE não dá suporte a esse retorno de chamada, ele não chamará o [SccSetOption](../extensibility/sccsetoption-function.md) especificá-lo. Se o plug-in não suporta esse retorno de chamada, ele retornará `SCC_E_OPNOTSUPPORTED` do `SccSetOption` quando o IDE tenta definir o retorno de chamada de função.  
  
## <a name="see-also"></a>Consulte também  
 [Funções de retorno de chamada implementadas pelo IDE](../extensibility/callback-functions-implemented-by-the-ide.md)   
 [SccSetOption](../extensibility/sccsetoption-function.md)
