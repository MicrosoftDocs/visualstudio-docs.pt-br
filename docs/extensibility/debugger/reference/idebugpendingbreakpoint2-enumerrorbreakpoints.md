---
description: Obtém uma lista de todos os pontos de interrupção de erro que resultaram desse ponto de interrupção pendente.
title: 'IDebugPendingBreakpoint2:: EnumErrorBreakpoints | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPendingBreakpoint2::EnumErrorBreakpoints
helpviewer_keywords:
- IDebugPendingBreakpoint2::EnumErrorBreakpoints method
- EnumErrorBreakpoints method
ms.assetid: 2f9a9720-c1ac-4430-8f28-200d85360452
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 664a64896244f58e98c9fd600b4fab71b5e9fe35
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102169802"
---
# <a name="idebugpendingbreakpoint2enumerrorbreakpoints"></a>IDebugPendingBreakpoint2::EnumErrorBreakpoints
Obtém uma lista de todos os pontos de interrupção de erro que resultaram desse ponto de interrupção pendente.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT EnumErrorBreakpoints( 
   BP_ERROR_TYPE                 bpErrorType,
   IEnumDebugErrorBreakpoints2** ppEnum
);
```

```csharp
int EnumErrorBreakpoints( 
   enum_BP_ERROR_TYPE              bpErrorType,
   out IEnumDebugErrorBreakpoints2 ppEnum
);
```

## <a name="parameters"></a>Parâmetros
`bpErrorType`\
no Uma combinação de valores da enumeração [BP_ERROR_TYPE](../../../extensibility/debugger/reference/bp-error-type.md) que seleciona o tipo de erros a serem enumerados.

`ppEnum`\
fora Retorna um objeto [IEnumDebugErrorBreakpoints2](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2.md) que contém uma lista de objetos [IDebugErrorBreakpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md) .

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro. Retorna `E_BP_DELETED` se o ponto de interrupção foi excluído.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra como implementar esse método para um `CPendingBreakpoint` objeto simples que expõe a interface [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md) .

```cpp
HRESULT CPendingBreakpoint::EnumErrorBreakpoints(
   BP_ERROR_TYPE bpErrorType,
   IEnumDebugErrorBreakpoints2** ppEnum)
{
   HRESULT hr;

   // Verify that the passed IEnumDebugErrorBreakpoints2 interface pointer
   // is valid.
   if (ppEnum)
   {
      // Verify that the pending breakpoint has not been deleted. If
      // deleted, then return hr = E_BP_DELETED.
      if (m_state.state != PBPS_DELETED)
      {
         // Verify that this error is not a warning.
         // All errors supported by this DE are errors, not warnings.
         if (IsFlagSet(bpErrorType, BPET_TYPE_ERROR) && m_pErrorBP)
         {
            // Get the error breakpoint.
            CComPtr<IDebugErrorBreakpoint2> spErrorBP;
            hr = m_pErrorBP->QueryInterface(&spErrorBP);
            assert(hr == S_OK);
            if (hr == S_OK)
            {
               // Create the error breakpoint enumerator.
               CComObject<CEnumDebugErrorBreakpoints>* pErrorEnum;
               hr = CComObject<CEnumDebugErrorBreakpoints>::CreateInstance(&pErrorEnum);
               assert(hr == S_OK);
               if (hr == S_OK)
               {
                  // Initialize the enumerator of error breakpoints with
                  // the IDebugErrorBreakpoint2 information.
                  IDebugErrorBreakpoint2* rgpErrorBP[] = { spErrorBP.p };
                  hr = pErrorEnum->Init(rgpErrorBP, &(rgpErrorBP[1]), NULL, AtlFlagCopy);
                  if (hr == S_OK)
                  {
                     // Verify that the passed IEnumDebugErrorBreakpoints2
                     // interface can be queried by the created
                     // CEnumDebugErrorBreakpoints object.
                     hr = pErrorEnum->QueryInterface(ppEnum);
                     assert(hr == S_OK);
                  }

                  // Otherwise, delete the CEnumDebugErrorBreakpoints
                  // object.
                  if (FAILED(hr))
                  {
                     delete pErrorEnum;
                  }
               }
            }
         }
         else
         {
            hr = S_FALSE;
         }
      }
      else
      {
         hr = E_BP_DELETED;
      }
   }
   else
   {
      hr = E_INVALIDARG;
   }

   return hr;
}
```

## <a name="see-also"></a>Confira também
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
- [BP_ERROR_TYPE](../../../extensibility/debugger/reference/bp-error-type.md)
- [IEnumDebugErrorBreakpoints2](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2.md)
- [IDebugErrorBreakpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)
