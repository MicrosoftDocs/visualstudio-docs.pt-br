---
title: IDebugGenericParamField::GetConstraints | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- IDebugGenericParamField::GetConstraints
- GetConstraints
ms.assetid: 86a78b5a-ee0f-4999-a0ba-919d3dc7d969
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: abed2d77156aac83b09bf5a0ba472b1887d15600
ms.sourcegitcommit: 845442e2b515c3ca1e4e47b46cc1cef4df4f08d8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/20/2019
ms.locfileid: "56450068"
---
# <a name="idebuggenericparamfieldgetconstraints"></a>IDebugGenericParamField::GetConstraints
Recupera as restrições que estão associadas esse parâmetro genérico.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetConstraints(
    ULONG32       cConstraints,
    IDebugField** ppConstraints,
    ULONG32*      pcConstraints
);
```

```csharp
int GetConstraints(
    uint              cConstraints,
    out IDebugField[] ppConstraints,
    ref uint          pcConstraints
);
```

#### <a name="parameters"></a>Parâmetros
`cConstraints`  
[in] Número de restrições.

`ppConstraints`  
[out] Retorna uma matriz que contém as restrições associadas a esse campo.

`pcConstraints`  
[no, out] Número de restrições no `ppConstraints` matriz.

## <a name="return-value"></a>Valor de retorno
Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.

## <a name="example"></a>Exemplo
O exemplo a seguir mostra como implementar esse método para um **CDebugGenericParamFieldType** objeto que expõe a [IDebugGenericParamField](../../../extensibility/debugger/reference/idebuggenericparamfield.md) interface.

```cpp
HRESULT CDebugGenericParamFieldType::GetConstraints(
    ULONG32 cConstraints,
    IDebugField** ppConstraints,
    ULONG32* pcConstraints)
{
    HRESULT hr = S_OK;
    CComPtr<IMetaDataImport> pMetadata;
    CComPtr<IMetaDataImport2> pMetadata2;
    mdGenericParamConstraint* rgParamConsts = NULL;
    HCORENUM hEnum = 0;
    ULONG cConst = 0;
    ULONG iConst;
    ULONG iConstOut = 0;

    METHOD_ENTRY( CDebugGenericParamFieldType::GetConstraints );

    IfFalseGo(ppConstraints && pcConstraints, E_INVALIDARG );
    *pcConstraints = 0;

    IfNullGo( rgParamConsts = new mdGenericParamConstraint[cConstraints], E_OUTOFMEMORY);

    IfFailGo( m_spSH->GetMetadata( m_idModule, &pMetadata ) );
    IfFailGo( pMetadata->QueryInterface(IID_IMetaDataImport2, (void**)&pMetadata2) );
    IfFailGo( pMetadata2->EnumGenericParamConstraints( &hEnum,
              m_tokParam,
              rgParamConsts,
              cConstraints,
              &cConst) );
    pMetadata->CloseEnum(hEnum);
    hEnum = NULL;

    for (iConst = 0; iConst < cConst; iConst++)
    {
        mdToken tokConst;

        IfFailGo( pMetadata2->GetGenericParamConstraintProps( rgParamConsts[iConst],
                  NULL,
                  &tokConst ) );
        switch (TypeFromToken(tokConst))
        {
            case mdtTypeRef:
                {
                    Module_ID mid;
                    mdTypeDef tokClass;

                    IfFailGo( CDebugClassFieldType::GetClassToken(m_spSH, m_idModule, tokConst, &mid, &tokClass) );
                    IfFailGo( m_spSH->CreateClassType( mid, tokClass, ppConstraints + iConstOut ) );
                    iConstOut++;
                    break;
                }
            case mdtTypeDef:
                {
                    IfFailGo( m_spSH->CreateClassType( m_idModule, tokConst, ppConstraints + iConstOut ) );
                    iConstOut++;
                    break;
                }
            case mdtTypeSpec:
                {
                    PCCOR_SIGNATURE pvSig;
                    ULONG cbSig;
                    DWORD cb = 0;
                    DWORD dwElementType;

                    IfFailGo( pMetadata2->GetTypeSpecFromToken( tokConst, &pvSig, &cbSig) );

                    cb += CorSigUncompressData(&(pvSig[cb]), &dwElementType);

                    IfFailGo( m_spSH->CreateType( pvSig, cbSig, m_idModule, mdMethodDefNil, m_pGenScope, ppConstraints + iConstOut ) );

                    iConstOut++;

                    break;
                }
            default:
                {
                    ASSERT(!"Bad constraint token");
                }
        }
    }

    *pcConstraints = iConstOut;

Error:

    METHOD_EXIT( CDebugGenericParamFieldType::GetConstraints, hr );

    DELETERG(rgParamConsts);

    return hr;
}
```

## <a name="see-also"></a>Consulte também
[IDebugGenericParamField](../../../extensibility/debugger/reference/idebuggenericparamfield.md)
