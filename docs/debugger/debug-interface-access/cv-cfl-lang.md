---
title: CV_CFL_LANG | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- CV_CFL_LANG enumeration
ms.assetid: 4e8e0613-ad02-4de9-9f46-e4753c5b0251
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ac8910ebe012e1edbaa6c26695027214db4e66c2
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85462130"
---
# <a name="cv_cfl_lang"></a>CV_CFL_LANG
Especifica o idioma do código-fonte do aplicativo ou módulo vinculado.

## <a name="syntax"></a>Syntax

```C++
typedef enum CV_CFL_LANG {
    CV_CFL_C       = 0x00,
    CV_CFL_CXX     = 0x01,
    CV_CFL_FORTRAN = 0x02,
    CV_CFL_MASM    = 0x03,
    CV_CFL_PASCAL  = 0x04,
    CV_CFL_BASIC   = 0x05,
    CV_CFL_COBOL   = 0x06,
    CV_CFL_LINK    = 0x07,
    CV_CFL_CVTRES  = 0x08,
    CV_CFL_CVTPGD  = 0x09,
    CV_CFL_CSHARP  = 0x0A,
    CV_CFL_VB      = 0x0B,
    CV_CFL_ILASM   = 0x0C,
    CV_CFL_JAVA    = 0x0D,
    CV_CFL_JSCRIPT = 0x0E,
    CV_CFL_MSIL    = 0x0F,
    CV_CFL_HLSL    = 0x10
} CV_CFL_LANG;
```

## <a name="elements"></a>Elementos
CV_CFL_C idioma do aplicativo é C.

CV_CFL_CXX idioma do aplicativo é C++.

CV_CFL_FORTRAN linguagem de aplicativo é a FORTRAN.

CV_CFL_MASM idioma do aplicativo é o Microsoft Macro Assembler.

CV_CFL_PASCAL idioma do aplicativo é Pascal.

CV_CFL_BASIC idioma do aplicativo é básico.

CV_CFL_COBOL idioma do aplicativo é COBOL.

CV_CFL_LINK aplicativo é um módulo gerado pelo vinculador.

CV_CFL_CVTRES aplicativo é um módulo de recurso convertido com a ferramenta CVTRES.

CV_CFL_CVTPGD aplicativo é um módulo de POGO otimizado gerado com a ferramenta CVTPGD.

CV_CFL_CSHARP idioma do aplicativo é C#.

CV_CFL_VB idioma do aplicativo é Visual Basic.

CV_CFL_ILASM idioma do aplicativo é um assembly de linguagem intermediária (ou seja, assembly CLR).

CV_CFL_JAVA idioma do aplicativo é Java.

CV_CFL_JSCRIPT idioma do aplicativo é JScript.

CV_CFL_MSIL linguagem de aplicativo é uma MSIL (Microsoft Intermediate Language) desconhecida, possivelmente um resultado do uso da opção [/LTCG (geração de código de tempo de vinculação)](/cpp/build/reference/ltcg-link-time-code-generation) .

CV_CFL_HLSL idioma do aplicativo é uma linguagem de sombreamento de alto nível.

## <a name="remarks"></a>Comentários
Os valores nessa enumeração são retornados por uma chamada para o método [IDiaSymbol:: get_language](../../debugger/debug-interface-access/idiasymbol-get-language.md) .

## <a name="requirements"></a>Requisitos
Cabeçalho: cvconst. h

## <a name="see-also"></a>Veja também
- [Enumerações e estruturas](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaSymbol::get_language](../../debugger/debug-interface-access/idiasymbol-get-language.md)
