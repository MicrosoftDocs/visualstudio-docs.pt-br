---
title: Uso da biblioteca de depuração CRT | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- c.debug.runtime
dev_langs:
- FSharp
- VB
- CSharp
- C++
- C++
helpviewer_keywords:
- /DEBUG linker option [C++]
- crtdbg.h file
- debug library
- MDd compiler option [C++]
- libraries, CRT debug library
- MTd compiler option [C++]
- LDd compiler function [C++]
- /MTd compiler option [C++]
- /MDd compiler option [C++]
- debugging [CRT], CRT debug library
- DEBUG linker option [C++]
- /LDd compiler function [C++]
ms.assetid: 464de16b-4215-4787-9bfa-921aaff9d9f4
caps.latest.revision: 19
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c6bba5b9c1b9d65c867176ac72c0641fac4cd286
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51817640"
---
# <a name="crt-debug-library-use"></a>Uso da biblioteca de depuração CRT
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A biblioteca em tempo de execução C fornece amplo suporte à depuração. Para usar uma das bibliotecas de depuração do CRT, você deve vincular com [/Debug](http://msdn.microsoft.com/library/1af389ae-3f8b-4d76-a087-1cdf861e9103) e compile com **/MDd**, **/MTd**, ou **/LDd**.  
  
## <a name="remarks"></a>Comentários  
 As definições e macros principais de depuração de CRT podem ser encontradas no arquivo de cabeçalho CRTDBG.h.  
  
 As funções em bibliotecas de depuração de CRT são compiladas com informações de depuração ([/Z7, /Zd, /Zi, /ZI (formato de informações de depuração)](http://msdn.microsoft.com/library/ce9fa7e1-0c9b-47e3-98ea-26d1a16257c8)) e sem otimização. Algumas funções contêm asserções para verificar os parâmetros passados a elas, e o código-fonte será fornecido. Com esse código-fonte, você pode acessar funções de CRT para confirmar se as funções estão funcionando conforme o esperado e verificar se há parâmetros incorretos ou estados de memória. (Qualquer tecnologia de CRT é proprietária e não fornece código-fonte para tratamento de exceções, ponto flutuante e algumas outras rotinas.)  
  
 Quando você instalar o Visual C++, terá a opção de instalar o código-fonte da biblioteca em tempo de execução C no disco rígido. Se você não instalar o código-fonte, precisará do CD-ROM para acessar as funções de CRT.  
  
 Para obter mais informações sobre as várias bibliotecas de tempo de execução, você pode usar, consulte [bibliotecas de tempo de execução C](http://msdn.microsoft.com/library/a889fd39-807d-48f2-807f-81492612463f).  
  
## <a name="see-also"></a>Consulte também  
 [Técnicas de depuração CRT](../debugger/crt-debugging-techniques.md)   
 [/MD, /MT, /LD (usar biblioteca de tempo de execução)](http://msdn.microsoft.com/library/cf7ed652-dc3a-49b3-aab9-ad60e5395579)



