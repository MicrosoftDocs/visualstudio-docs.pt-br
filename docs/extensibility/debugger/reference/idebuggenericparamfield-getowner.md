---
title: IDebugGenericParamField::GetOwner | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- IDebugGenericParamField::GetOwner
ms.assetid: c7f6d166-a69e-40c4-bd0b-1a1fdf9aaacf
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 6ab96887c12d798bfc521519b444c164b6e661fc
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49937155"
---
# <a name="idebuggenericparamfieldgetowner"></a>IDebugGenericParamField::GetOwner
Recupera o proprietário do tipo ou método desse parâmetro genérico.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetOwner(  
   IDebugField** ppOwner  
);  
```  
  
```csharp  
int GetOwner(  
   out IDebugField ppOwner  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `ppOwner`  
 [out] Retorna o [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) objeto que possui esse parâmetro genérico.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra como implementar esse método para um **CDebugGenericParamFieldType** objeto que expõe a [IDebugGenericParamField](../../../extensibility/debugger/reference/idebuggenericparamfield.md) interface.  
  
```cpp  
HRESULT CDebugGenericParamFieldType::GetOwner(IDebugField** ppOwner)  
{  
    HRESULT hr = S_OK;  
    CComPtr<IMetaDataImport> pMetadata;  
  
    METHOD_ENTRY( CDebugGenericParamFieldType::GetOwner );  
  
    IfFalseGo(ppOwner, E_INVALIDARG );  
    *ppOwner = NULL;  
  
    IfFailGo( this->LoadProps() );  
    IfFailGo( m_spSH->GetMetadata( m_idModule, &pMetadata ) );  
  
    switch (TypeFromToken(m_tokOwner))  
    {  
        case mdtMethodDef:  
            {  
                mdTypeDef tokClass;  
                CComPtr<IDebugField> pClass;  
                CDEBUG_ADDRESS caddr;  
                CComPtr<IDebugContainerField> pContainer;  
  
                IfFailGo( pMetadata->GetMethodProps( m_tokOwner, &tokClass, NULL, 0, NULL, NULL, NULL, NULL, NULL, NULL ) );  
                IfFailGo( m_spSH->CreateClassType(m_idModule, tokClass, &pClass) );  
                IfFailGo( pClass->QueryInterface( &pContainer ) );  
                IfFailGo( caddr.InitializeMethod( m_idModule, tokClass, m_tokOwner, 0, 0 ) );  
                IfFailGo( m_spSH->CreateMethodSymbol( pContainer, caddr, FIELD_SYM_MEMBER, ppOwner ) );  
                break;  
            }  
        case mdtTypeDef:  
            {  
                IfFailGo( m_spSH->CreateClassType(m_idModule, m_tokOwner, ppOwner) );  
                break;  
            }  
        default:  
            {  
                ASSERT(!"Unexpected Owner type for Generic Param Field");  
                hr = E_FAIL;  
            }  
    }  
Error:  
  
    METHOD_EXIT( CDebugGenericParamFieldType::GetOwner, hr );  
    return hr;  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [IDebugGenericParamField](../../../extensibility/debugger/reference/idebuggenericparamfield.md)