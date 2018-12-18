---
title: IDebugProperty2::GetExtendedInfo | Microsoft Docs
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
- IDebugProperty2::GetExtendedInfo
helpviewer_keywords:
- IDebugProperty2::GetExtendedInfo
ms.assetid: 0c9c0b2b-7540-4424-adb5-fce7aa37a026
caps.latest.revision: 11
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 9f6fd711a70c050a6f490a27a56eb860c84de867
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51726957"
---
# <a name="idebugproperty2getextendedinfo"></a>IDebugProperty2::GetExtendedInfo
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Obtém informações estendidas de propriedade.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
HRESULT GetExtendedInfo (   
   REFGUID* guidExtendedInfo,  
   VARIANT* pExtendedInfo  
);  
```  
  
```csharp  
int GetExtendedInfo (   
   ref Guid guidExtendedInfo,  
   out object pExtendedInfo  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `guidExtendedInfo`  
 [in] GUID que determina o tipo de informações estendidas a serem recuperados. Consulte os comentários para obter detalhes.  
  
 `pExtendedInfo`  
 [out] Retorna um `VARIANT` (C++) ou o objeto (C#) que pode ser usado para recuperar as informações de propriedade estendida. Por exemplo, esse parâmetro pode retornar um `IUnknown` interface que pode ser consultado para uma [IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md) interface. Consulte os comentários para obter detalhes.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retornará o código de erro. Retorna `S_GETEXTENDEDINFO_NO_EXTENDEDINFO` se não houver nenhuma informação estendida para recuperar.  
  
## <a name="remarks"></a>Comentários  
 Este método existe para fins de recuperação de informações que não se prestam a que está sendo recuperado por meio da chamada a [GetPropertyInfo](../../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) método.  
  
 Os GUIDs seguintes normalmente são reconhecidos por este método (os valores GUID são especificados para c#, pois o nome não está disponível em qualquer assembly). GUIDs adicionais podem ser criados para uso interno.  
  
|Nome|GUID|Descrição|  
|----------|----------|-----------------|  
|guidDocument|{3f98de84-fee9-11d0-b47f-00a0244a1dd2}|Retorna um `IUnknown` interface para o documento. Normalmente, o [IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md) interface pode ser obtida deste `IUnknown` interface.|  
|guidCodeContext|{e2fc65e-56ce - 11d 1-b528-00aax004a8797}|Retorna um `IUnknown` interface para o contexto do documento. Normalmente, o [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md) interface pode ser obtida deste `IUnknown` interface.|  
|guidCustomViewerSupported|{d9c9da31-ffbe-4eeb-9186-23121e3c088c}|Retorna uma cadeia de caracteres que contém o CLSID de um visualizador personalizado, costuma ser implementado por um avaliador de expressão.|  
|guidExtendedInfoSlot|{6df235ad-82c6-4292-9c97-7389770bc42f}|Retorna um número de 32 bits que representa o número de slot desejado se esta propriedade representa um endereço local do código gerenciado.|  
|guidExtendedInfoSignature|{b5fb6d46-f805-417f-96a3-8ba737073ffd}|Retorna uma cadeia de caracteres que contém a assinatura da variável associada ao objeto de propriedade.|  
  
## <a name="see-also"></a>Consulte também  
 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)   
 [IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md)   
 [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)

