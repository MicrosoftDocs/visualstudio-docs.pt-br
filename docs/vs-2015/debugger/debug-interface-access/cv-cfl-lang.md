---
title: CV_CFL_LANG | Microsoft Docs
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
- CV_CFL_LANG enumeration
ms.assetid: 4e8e0613-ad02-4de9-9f46-e4753c5b0251
caps.latest.revision: 16
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f6e2aa402d3f882d83525b180707653b97533e32
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51724794"
---
# <a name="cvcfllang"></a>CV_CFL_LANG
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Especifica a linguagem de código fonte do aplicativo ou módulo vinculado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
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
 CV_CFL_C  
 Idioma do aplicativo é C.  
  
 CV_CFL_CXX  
 Idioma do aplicativo é C++.  
  
 CV_CFL_FORTRAN  
 Idioma do aplicativo é FORTRAN.  
  
 CV_CFL_MASM  
 Idioma do aplicativo é Microsoft Macro Assembler.  
  
 CV_CFL_PASCAL  
 Idioma do aplicativo é Pascal.  
  
 CV_CFL_BASIC  
 Idioma do aplicativo é BASIC.  
  
 CV_CFL_COBOL  
 Idioma do aplicativo é COBOL.  
  
 CV_CFL_LINK  
 Aplicativo é um módulo geradas pelo vinculador.  
  
 CV_CFL_CVTRES  
 Aplicativo é um módulo de recurso convertido com a ferramenta CVTRES.  
  
 CV_CFL_CVTPGD  
 Aplicativo é um módulo POGO otimizado gerado com a ferramenta CVTPGD.  
  
 CV_CFL_CSHARP  
 Idioma do aplicativo é c#.  
  
 CV_CFL_VB  
 É o idioma do aplicativo Visual Basic.  
  
 CV_CFL_ILASM  
 Idioma do aplicativo é um assembly de linguagem intermediária (ou seja, o assembly do Common Language Runtime (CLR)).  
  
 CV_CFL_JAVA  
 Idioma do aplicativo é Java.  
  
 CV_CFL_JSCRIPT  
 Idioma do aplicativo é Jscript.  
  
 CV_CFL_MSIL  
 Idioma do aplicativo é um desconhecido MSIL Microsoft Intermediate Language (), possivelmente um resultado do uso de [/LTCG (geração de código Link-time)](http://msdn.microsoft.com/library/788c6f52-fdb8-40c2-90af-4026ea2cf2e2) alternar.  
  
 CV_CFL_HLSL  
 Idioma do aplicativo é a linguagem de sombreador de nível alto.  
  
## <a name="remarks"></a>Comentários  
 Os valores nesta enumeração são retornados por uma chamada para o [idiasymbol:: Get_language](../../debugger/debug-interface-access/idiasymbol-get-language.md) método.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: cvconst.h  
  
## <a name="see-also"></a>Consulte também  
 [Enumerações e estruturas](../../debugger/debug-interface-access/enumerations-and-structures.md)   
 [IDiaSymbol::get_language](../../debugger/debug-interface-access/idiasymbol-get-language.md)



