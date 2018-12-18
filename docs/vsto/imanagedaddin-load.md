---
title: IManagedAddin::Load
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords: ''
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: d1ea659d59e780beba3949e7cae363affa312c17
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "35670746"
---
# <a name="imanagedaddinload"></a>IManagedAddin::Load
  Chamado quando um gerenciado VSTO suplemento é carregado.  
  
## <a name="syntax"></a>Sintaxe  
  
```csharp
HRESULT Load([in] BSTR bstrManifestURL,   
             [in] IDispatch *pdispApplication);  
```  
  
### <a name="parameters"></a>Parâmetros  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|*bstrManifestURL*|O caminho completo do manifesto para o suplemento do VSTO.|  
|*pdispApplication*|Um ponteiro para um que representa o aplicativo host que está carregando o suplemento do VSTO IDispatch.|  
  
## <a name="return-value"></a>Valor de retorno  
 Um valor HRESULT que indica se o método concluída com êxito.  
  
## <a name="remarks"></a>Comentários  
 Um manifesto é um arquivo (normalmente, um arquivo XML) que fornece informações que são usadas para ajudar a carregar o suplemento do VSTO. Por exemplo, um manifesto pode especificar o local do assembly do suplemento do VSTO e a classe de ponto de entrada para criar uma instância quando o suplemento do VSTO é carregado.  
  
 O *bstrManifestURL* parâmetro contém o valor da `Manifest` entrada sob o **HKEY_CURRENT_USER\Software\Microsoft\Office\\_\<nome do aplicativo >_ \Addins\\_\<ID do suplemento >_**  chave do registro para o suplemento do VSTO. Para obter mais informações, consulte [interface IManagedAddin](../vsto/imanagedaddin-interface.md).  
  
 Implemente a [IManagedAddIn::Load](../vsto/imanagedaddin-load.md) método para executar tarefas como configurar a política de segurança e de domínio de aplicativo para o suplemento VSTO que está sendo carregado.  
  
## <a name="see-also"></a>Consulte também  
 [Interface IManagedAddin](../vsto/imanagedaddin-interface.md)   
 [IManagedAddin::Unload](../vsto/imanagedaddin-unload.md)  
  
  