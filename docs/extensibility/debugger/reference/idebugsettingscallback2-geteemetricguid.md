---
title: IDebugSettingsCallback2::GetEEMetricGuid | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugSettingsCallback2::GetEEMetricGuid
ms.assetid: 3d70c19a-595d-44f1-a7b3-a0cf8f15e371
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f2bffa499d24bc38008982c990efd19205e95f6f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62869023"
---
# <a name="idebugsettingscallback2geteemetricguid"></a>IDebugSettingsCallback2::GetEEMetricGuid
Recupera o identificador exclusivo para uma métrica de avaliador de expressão dado seu nome.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetEEMetricGuid(
   REFGUID guidLang,
   REFGUID guidVendor,
   LPCWSTR pszMetric,
   GUID*   pguidValue
);
```

```csharp
HRESULT GetEEMetricGuid(
   ref Guid guidLang,
   ref Guid guidVendor,
   string   pszMetric,
   out Guid pguidValue
);
```

#### <a name="parameters"></a>Parâmetros
 `guidLang`

 [in] Identificador exclusivo da linguagem de programação.

 `guidVendor`

 [in] Identificador exclusivo do fornecedor.

 `pszMetric`

 [in] Nome da métrica.

 `pguidValue`

 [out] Retorna o identificador exclusivo da métrica.

## <a name="return-value"></a>Valor de retorno
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Consulte também
- [IDebugSettingsCallback2](../../../extensibility/debugger/reference/idebugsettingscallback2.md)