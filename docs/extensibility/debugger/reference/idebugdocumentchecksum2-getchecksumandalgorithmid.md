---
description: Recupera a soma de verificação do documento e o identificador do algoritmo de acordo com o número máximo de bytes a serem usados.
title: 'IDebugDocumentChecksum2:: GetChecksumAndAlgorithmId | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugDocumentChecksum2::GetChecksumAndAlgorithmI
- GetChecksumAndAlgorithmI
ms.assetid: 25efef99-0ef3-4332-a752-607605fc6e67
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: af1d3718fd4976ea2c26d284f9257b52cc233e67
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105066770"
---
# <a name="idebugdocumentchecksum2getchecksumandalgorithmid"></a>IDebugDocumentChecksum2::GetChecksumAndAlgorithmId
Recupera a soma de verificação do documento e o identificador do algoritmo de acordo com o número máximo de bytes a serem usados.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetChecksumAndAlgorithmId(
    GUID  *pRetVal,
    ULONG cMaxBytes,
    BYTE  *pChecksum,
    ULONG *pcNumBytes
);
```

```csharp
public int GetChecksumAndAlgorithmId(
    out Guid pRetVal,
    uint     cMaxBytes,
    out byte pChecksum,
    out uint pcNumBytes
);
```

## <a name="parameters"></a>Parâmetros
`pRetVal`\
fora Identificador exclusivo para o algoritmo de soma de verificação.

`cMaxBytes`\
no Número máximo de bytes a serem usados para a soma de verificação.

`pChecksum`\
fora Valor da soma de verificação.

`pcNumBytes`\
fora Número real de bytes usados para a soma de verificação.

## <a name="return-value"></a>Valor Retornado
Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="example"></a>Exemplo
O exemplo a seguir usa esse método para obter a soma de verificação e o algoritmo de um documento.

```cpp
HRESULT CDebugCodeContext::GetDocumentChecksumAndAlgorithmId(GUID *pguidAlgorithm, BYTE **ppChecksum, ULONG *pcNumBytes)
{
    HRESULT hRes = E_FAIL;

    *ppChecksum = NULL;
    *pcNumBytes = 0;

    CComPtr<IDebugDocumentContext2> pDocContext;

    hRes = this->GetDocumentContext(&pDocContext);

    if ( HREVAL(S_OK, hRes) )
    {
        CComQIPtr<IDebugDocumentChecksum2> pDocChecksum(pDocContext);

        if ( pDocChecksum != NULL )
        {
            // Figure out the size of the checksum buffer required
            ULONG cNumBytes = 0;

            hRes = pDocChecksum->GetChecksumAndAlgorithmId(pguidAlgorithm, 0, NULL, &cNumBytes);

            if ( S_OK == hRes )
            {
                // check to see if we got back valid values
                if ( cNumBytes && GUID_NULL != (*pguidAlgorithm) )
                {
                    // Alloc space for the checksum data
                    BYTE *pChecksum = (BYTE*) CoTaskMemAlloc(cNumBytes);

                    if ( pChecksum )
                    {
                        // Get the buffer containing the checksum info
                        hRes = pDocChecksum->GetChecksumAndAlgorithmId(pguidAlgorithm, cNumBytes, pChecksum, &cNumBytes);

                        if ( HREVAL(S_OK, hRes) )
                        {
                            *ppChecksum = pChecksum;
                            *pcNumBytes = cNumBytes;
                        }
                        else
                        {
                            CoTaskMemFree(pChecksum);
                        }
                    }
                    else
                        hRes = E_OUTOFMEMORY;
                }
                else
                    hRes = S_FALSE; // lang doesn't support checksums
            }
            else
                hRes = S_FALSE; // failed to work out checksum info
        }
        else
            hRes = S_FALSE; // SH doesn't support checksums
    }

    return ( hRes );
}
```

## <a name="see-also"></a>Confira também
- [IDebugDocumentChecksum2](../../../extensibility/debugger/reference/idebugdocumentchecksum2.md)
