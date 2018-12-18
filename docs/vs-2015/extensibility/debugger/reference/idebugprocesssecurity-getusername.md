---
title: IDebugProcessSecurity::GetUserName | Microsoft Docs
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
- IDebugProcessSecurity::GetUserName
ms.assetid: c73c60ac-da6e-45ae-8f04-95353a24ca3e
caps.latest.revision: 5
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 45e9bb46a26191c7722657033ece7d1e83867711
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51755937"
---
# <a name="idebugprocesssecuritygetusername"></a>IDebugProcessSecurity::GetUserName
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Obtém o nome de usuário do fornecedor de porta.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
HRESULT GetUserName(  
    BSTR *pbstrUserName  
);  
```  
  
```csharp  
int GetUserName (  
    string pbstrUserName  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pbstrUserName`  
 [out] Uma cadeia de caracteres que contém o nome de usuário.  
  
## <a name="return-value"></a>Valor de retorno  
 Se o método for bem-sucedido, ele retornará `S_OK`. Caso contrário, ele retornará um código de erro.  
  
## <a name="remarks"></a>Comentários  
 `GetUserName` Retorna o nome de usuário que é exibido na **nome de usuário** coluna o **anexar ao processo** caixa de diálogo. Para exibir o **anexar ao processo** caixa de diálogo, clique em **anexar ao processo** no **ferramentas** menu no [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] o ambiente de desenvolvimento integrado (IDE).  
  
## <a name="see-also"></a>Consulte também  
 [IDebugProcessSecurity](../../../extensibility/debugger/reference/idebugprocesssecurity.md)

