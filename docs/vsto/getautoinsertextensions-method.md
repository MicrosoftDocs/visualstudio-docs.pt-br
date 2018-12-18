---
title: Método GetAutoInsertExtensions
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 7e3e0fda420682e4f33c0d22a3e9c8caa920895b
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "35670105"
---
# <a name="getautoinsertextensions-method"></a>Método GetAutoInsertExtensions
  Obtém informações sobre os aplicativos do Office que serão inseridos automaticamente durante a depuração.  
  
 Este método está reservado para uso futuro.  
  
## <a name="syntax"></a>Sintaxe  
  
```csharp
HRESULT GetAutoInsertExtensions(  
    [out, retval] SAFEARRAY(BSTR)* psaExtensionNames  
);  
```  
  
### <a name="parameters"></a>Parâmetros  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|*psaExtensionNames*|Os nomes de extensão dos aplicativos para Office.|  
  
## <a name="return-value"></a>Valor retornado  
 Um valor HRESULT que indica se o método concluída com êxito.  
  
## <a name="remarks"></a>Comentários  
 Cada aplicativo do Office a ser inserido é retornado como um nome de extensão de aplicativo do Office, que corresponde a um valor em **HKEY_CURRENT_USER\Software\Microsoft\Office\WEF\Developer**. O host deve pesquisar esses valores no registro e, em seguida, inserir automaticamente as extensões.  
  
  