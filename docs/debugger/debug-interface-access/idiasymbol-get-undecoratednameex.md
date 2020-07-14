---
title: IDiaSymbol::get_undecoratedNameEx | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_undecoratedNameEx method
ms.assetid: 579aed0b-c57d-41a1-a94a-3bf665fd4a9d
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 25942c76d8e568d6354c9a6a2b2c69c806cde352
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85461598"
---
# <a name="idiasymbolget_undecoratednameex"></a>IDiaSymbol::get_undecoratedNameEx
Recupera parte ou todo um nome não decorado para um nome de C++ decorado (vinculação).

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_undecoratedNameEx( 
   DWORD undecorateOptions,
   BSTR* pRetval
);
```

#### <a name="parameters"></a>Parâmetros
 `undecoratedOptions`

no Especifica uma combinação de sinalizadores que controlam o que é retornado. Consulte a seção comentários para obter os valores específicos e o que eles fazem.

 `pRetVal`

fora Retorna o nome não decorado para um nome decorado em C++.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` ou um código de erro.

> [!NOTE]
> Um valor de retorno de `S_FALSE` significa que a propriedade não está disponível para o símbolo.

## <a name="remarks"></a>Comentários
 O `undecorateOptions` pode ser uma combinação dos sinalizadores a seguir.

> [!NOTE]
> Os nomes dos sinalizadores não são definidos no DIA SDK, portanto, você precisa adicionar as declarações ao seu código ou usar os valores brutos.

|Sinalizador|Valor|Descrição|
|----------|-----------|-----------------|
|UNDNAME_COMPLETE|0x0000|Habilita a desdecoração completa.|
|UNDNAME_NO_LEADING_UNDERSCORES|0x0001|Remove os sublinhados à esquerda de palavras-chave estendidas da Microsoft.|
|UNDNAME_NO_MS_KEYWORDS|0x0002|Desabilita a expansão de palavras-chave estendidas da Microsoft.|
|UNDNAME_NO_FUNCTION_RETURNS|0x0004|Desabilita a expansão do tipo de retorno para a declaração principal.|
|UNDNAME_NO_ALLOCATION_MODEL|0x0008|Desabilita a expansão do modelo de declaração.|
|UNDNAME_NO_ALLOCATION_LANGUAGE|0x0010|Desabilita a expansão do especificador de linguagem de declaração.|
|UNDNAME_RESERVED1|0x0020|RESERVADO.|
|UNDNAME_RESERVED2|0x0040|RESERVADO.|
|UNDNAME_NO_THISTYPE|0x0060|Desabilita todos os modificadores no `this` tipo.|
|UNDNAME_NO_ACCESS_SPECIFIERS|0x0080|Desabilita a expansão de especificadores de acesso para membros.|
|UNDNAME_NO_THROW_SIGNATURES|0x0100|Desabilita a expansão de "Throw-Signatures" para funções e ponteiros para funções.|
|UNDNAME_NO_MEMBER_TYPE|0x0200|Desabilita a expansão de `static` Membros ou `virtual` .|
|UNDNAME_NO_RETURN_UDT_MODEL|0x0400|Desabilita a expansão do modelo da Microsoft para retornos de UDT.|
|UNDNAME_32_BIT_DECODE|0x0800|Não decora os nomes decorados de 32 bits.|
|UNDNAME_NAME_ONLY|0x1000|Obtém somente o nome da declaração principal; retorna apenas o nome [Scope::].  Expande parâmetros de modelo.|
|UNDNAME_TYPE_ONLY|0x2000|A entrada é apenas uma codificação de tipo; compõe um Declarador abstrato.|
|UNDNAME_HAVE_PARAMETERS|0x4000|Os parâmetros de modelo reais estão disponíveis.|
|UNDNAME_NO_ECSU|0x8000|Suprime enum/Class/struct/Union.|
|UNDNAME_NO_IDENT_CHAR_CHECK|0x10000|Suprime a verificação de caracteres de identificador válidos.|
|UNDNAME_NO_PTR64|0x20000|Não inclui ptr64 na saída.|

## <a name="see-also"></a>Veja também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)