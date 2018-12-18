---
title: 'Idiasymbol:: Get_undecoratednameex | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_undecoratedNameEx method
ms.assetid: 579aed0b-c57d-41a1-a94a-3bf665fd4a9d
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: de8eb57e8b1e31be835163e67fa12e3cd6556892
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49930655"
---
# <a name="idiasymbolgetundecoratednameex"></a>IDiaSymbol::get_undecoratedNameEx
Recupera parte ou todo um nome não decorado para um C++ decoradas nome (ligação).  
  
## <a name="syntax"></a>Sintaxe  
  
```C++  
HRESULT get_undecoratedNameEx(   
   DWORD undecorateOptions,  
   BSTR* pRetval  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `undecoratedOptions`  
 [in] Especifica uma combinação de sinalizadores que controlam o que é retornado. Consulte a seção comentários para os valores específicos e o que fazer.  
  
 `pRetVal`  
 [out] Retorna o que nome decorado do nome não decorado para um C++.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna `S_FALSE` ou um código de erro.  
  
> [!NOTE]
>  Um valor de retorno `S_FALSE` significa que a propriedade não está disponível para o símbolo.  
  
## <a name="remarks"></a>Comentários  
 O `undecorateOptions` pode ser uma combinação dos sinalizadores a seguir.  
  
> [!NOTE]
>  Os nomes de sinalizador não são definidos no DIA SDK, portanto, você precisa adicionar as declarações em seu código ou usar os valores brutos.  
  
|Sinalizador|Valor|Descrição|  
|----------|-----------|-----------------|  
|UNDNAME_COMPLETE|0x0000|Habilita completo undecoration.|  
|UNDNAME_NO_LEADING_UNDERSCORES|0x0001|Remove o sublinhados à esquerda da Microsoft estendido palavras-chave.|  
|UNDNAME_NO_MS_KEYWORDS|0x0002|Desabilita expansão de estendidas de palavras-chave da Microsoft.|  
|UNDNAME_NO_FUNCTION_RETURNS|0x0004|Desabilita expansão do tipo de retorno para a declaração primário.|  
|UNDNAME_NO_ALLOCATION_MODEL|0x0008|Desabilita a expansão do modelo de declaração.|  
|UNDNAME_NO_ALLOCATION_LANGUAGE|0x0010|Desabilita expansão do especificador de linguagem de declaração.|  
|UNDNAME_RESERVED1|0x0020|RESERVADO.|  
|UNDNAME_RESERVED2|0x0040|RESERVADO.|  
|UNDNAME_NO_THISTYPE|0x0060|Desabilita todos os modificadores no `this` tipo.|  
|UNDNAME_NO_ACCESS_SPECIFIERS|0x0080|Desabilita expansão dos especificadores de acesso para membros.|  
|UNDNAME_NO_THROW_SIGNATURES|0x0100|Desabilita expansão de "throw-assinaturas" para funções e ponteiros para funções.|  
|UNDNAME_NO_MEMBER_TYPE|0x0200|Desabilita expansão dos `static` ou `virtual` membros.|  
|UNDNAME_NO_RETURN_UDT_MODEL|0x0400|Desabilita expansão do modelo da Microsoft para retorna UDT.|  
|UNDNAME_32_BIT_DECODE|0x0800|Undecorates nomes decorados de 32 bits.|  
|UNDNAME_NAME_ONLY|0x1000|Obtém somente o nome de declaração primário; Retorna apenas [escopo::] nome.  Expande os parâmetros de modelo.|  
|UNDNAME_TYPE_ONLY|0x2000|A entrada é apenas um tipo de codificação; compõe um declarador abstrato.|  
|UNDNAME_HAVE_PARAMETERS|0x4000|Os parâmetros de modelo real estão disponíveis.|  
|UNDNAME_NO_ECSU|0x8000|Suprime enum/classe/struct/union.|  
|UNDNAME_NO_IDENT_CHAR_CHECK|0x10000|Suprime a verificação de caracteres de identificador válido.|  
|UNDNAME_NO_PTR64|0x20000|Não inclui ptr64 na saída.|  
  
## <a name="see-also"></a>Consulte também  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)