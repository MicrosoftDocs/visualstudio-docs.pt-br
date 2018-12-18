---
title: 'Idiadatasource:: Loadandvalidatedatafrompdb | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- C++
helpviewer_keywords:
- IDiaDataSource::loadAndValidateDataFromPdb method
ms.assetid: d66712dd-6c24-4192-919a-cce262066f0e
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: efd5641083bded6729a7c2c698b5a1164a280118
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51767686"
---
# <a name="idiadatasourceloadandvalidatedatafrompdb"></a>IDiaDataSource::loadAndValidateDataFromPdb
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Abre e verifica se o arquivo de banco de dados (. PDB) de programa corresponde as informações de assinatura fornecidas e prepara o arquivo. PDB como uma fonte de dados de depuração.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
HRESULT loadAndValidateDataFromPdb (   
   LPCOLESTR pdbPath,  
   GUID*     pcsig70,  
   DWORD     sig,  
   DWORD     age  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pdbPath`  
 [in] O caminho para o arquivo. PDB.  
  
 `pcsig70`  
 [in] A assinatura GUID para verificar em relação à assinatura do arquivo. PDB. Arquivos apenas. PDB [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)] e versões posteriores possuem assinaturas GUID.  
  
 `sig`  
 [in] A assinatura de 32 bits para verificar em relação à assinatura do arquivo. PDB.  
  
 `age`  
 [in] Valor de idade para verificar. A idade não necessariamente corresponde a qualquer valor de tempo conhecido, ele é usado para determinar se um arquivo. PDB está fora de sincronia com um arquivo .exe correspondente.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro. A tabela a seguir mostra os possíveis valores retornados para esse método.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|E_PDB_NOT_FOUND|Falha ao abrir o arquivo ou o arquivo tem um formato inválido.|  
|E_PDB_FORMAT|Tentativa de acessar um arquivo com um formato obsoleto.|  
|E_PDB_INVALID_SIG|Assinatura não corresponde.|  
|E_PDB_INVALID_AGE|Não corresponde a idade.|  
|E_INVALIDARG|Parâmetro inválido.|  
|E_UNEXPECTED|A fonte de dados já foi preparada.|  
  
## <a name="remarks"></a>Comentários  
 Um arquivo. PDB contém valores de assinatura e idade. Esses valores são replicados no arquivo. dll ou. .exe que corresponde ao arquivo. PDB. Antes de preparar a fonte de dados, esse método verifica a assinatura e a idade do arquivo. PDB chamado coincidir com os valores fornecidos.  
  
 Para carregar um arquivo. PDB sem validação, use o [idiadatasource:: Loaddatafrompdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md) método.  
  
 Para obter acesso para o processo de carregamento de dados (por meio de um mecanismo de retorno de chamada), use o [idiadatasource:: Loaddataforexe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md) método.  
  
 Para carregar um arquivo. PDB diretamente da memória, use o [idiadatasource:: Loaddatafromistream](../../debugger/debug-interface-access/idiadatasource-loaddatafromistream.md) método.  
  
## <a name="example"></a>Exemplo  
  
```cpp#  
IDiaDataSource* pSource;  // Previously created data source.  
DEFINE_GUID(expectedGUIDSignature,0x1234,0x5678,0x01,0x02,0x03,0x04,0x05,0x06,0x07,0x08);  
DWORD expectedFileSignature = 0x12345678;  
DWORD expectedAge           = 128;  
  
HRESULT hr;  
hr = pSource->loadAndValidateDataFromPdb( L"yprog.pdb",  
                                          &expectedGUIDSignature,  
                                          expectedFileSignature,  
                                          expectedAge);  
if (FAILED(hr))  
{  
    // Report an error  
}  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)   
 [Idiadatasource:: Loaddataforexe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)   
 [Idiadatasource:: Loaddatafrompdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md)   
 [IDiaDataSource::loadDataFromIStream](../../debugger/debug-interface-access/idiadatasource-loaddatafromistream.md)



