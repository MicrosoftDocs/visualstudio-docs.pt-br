---
title: IDebugDocumentChecksum2::GetChecksumAndAlgorithmId | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- IDebugDocumentChecksum2::GetChecksumAndAlgorithmI
- GetChecksumAndAlgorithmI
ms.assetid: 25efef99-0ef3-4332-a752-607605fc6e67
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: fbb12f315bc0e83e14ad4a342443ed3207411dae
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49846376"
---
# <a name="idebugdocumentchecksum2getchecksumandalgorithmid"></a>IDebugDocumentChecksum2::GetChecksumAndAlgorithmId
Recupera o identificador de soma de verificação e o algoritmo de documento dado o número máximo de bytes a serem usados.  
  
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
  
#### <a name="parameters"></a>Parâmetros  
 `pRetVal`  
 [out] Identificador exclusivo para o algoritmo de soma de verificação.  
  
 `cMaxBytes`  
 [in] Número máximo de bytes a ser usado para a soma de verificação.  
  
 `pChecksum`  
 [out] Valor da soma de verificação.  
  
 `pcNumBytes`  
 [out] Número real de bytes usados para a soma de verificação.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir usa esse método para obter a soma de verificação e o algoritmo para um documento.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [IDebugDocumentChecksum2](../../../extensibility/debugger/reference/idebugdocumentchecksum2.md)