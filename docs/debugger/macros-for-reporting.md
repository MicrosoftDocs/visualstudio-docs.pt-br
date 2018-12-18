---
title: Macros para relatórios | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.macros
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- macros, CRT reporting macros
- macros, debugging with
- _RPTFn macro
- CRT, reporting macros
- debugging [CRT], reporting macros
- _RPTn macro
ms.assetid: f2085314-a3a8-4caf-a5a4-2af9ad5aad05
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 57b254323fac5d670cd44399cd8d22c9530c4510
ms.sourcegitcommit: 0bf2aff6abe485e3fe940f5344a62a885ad7f44e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2018
ms.locfileid: "37056596"
---
# <a name="macros-for-reporting"></a>Macros para relatórios
Para depuração, você pode usar o **rptn** e **rptfn** macros, definidas em CRTDBG. H, para substituir o uso de `printf` instruções. Você não precisa inclose-los no **#ifdef**s, porque eles desaparecem automaticamente na sua versão de compilação quando **Debug** não está definido.  
  
|Macro|Descrição|  
|-----------|-----------------|  
|**_RPT0**, **_RPT1**, **_RPT2**, **_RPT3**, **_RPT4**|Gera uma cadeia de caracteres de mensagem e zero a quatro argumentos. Para _RPT1 até **_RPT4**, a cadeia de caracteres de mensagem serve como uma cadeia de caracteres de formatação de estilo printf para os argumentos.|  
|**_RPTF0**, **_RPTF1**, **_RPTF2**, **_RPTF4**|Mesmo que **rptn**, mas essas macros também o número de linha e de nome de arquivo onde se encontra a macro de saída.|  
  
 Considere o exemplo a seguir:  
  
```cpp
#ifdef _DEBUG  
    if ( someVar > MAX_SOMEVAR )  
        printf( "OVERFLOW! In NameOfThisFunc( ),  
               someVar=%d, otherVar=%d.\n",  
               someVar, otherVar );  
#endif  
```  
  
 Esse código gera os valores de `someVar` e `otherVar` à **stdout**. Você pode usar a seguinte chamada para `_RPTF2` para reportar os mesmos valores e, além disso, o nome de arquivo e o número de linha:  
  
```cpp
if (someVar > MAX_SOMEVAR) _RPTF2(_CRT_WARN, "In NameOfThisFunc( ), someVar= %d, otherVar= %d\n", someVar, otherVar );  
```  
  
Você pode achar que um aplicativo específico precisa depurar relatórios que não forneçam as macros fornecidas com a biblioteca de tempo de execução C. Nesses casos, você pode escrever uma macro criada especificamente para atender às suas próprias necessidades. Em um dos arquivos de cabeçalho, por exemplo, você pode incluir código como o seguinte para definir uma macro chamada **ALERT_IF2**:  
  
```cpp
#ifndef _DEBUG                  /* For RELEASE builds */  
#define  ALERT_IF2(expr, msg, arg1, arg2)  do {} while (0)  
#else                           /* For DEBUG builds   */  
#define  ALERT_IF2(expr, msg, arg1, arg2) \  
    do { \  
        if ((expr) && \  
            (1 == _CrtDbgReport(_CRT_ERROR, \  
                __FILE__, __LINE__, msg, arg1, arg2))) \  
            _CrtDbgBreak( ); \  
    } while (0)  
#endif  
```  
  
 Uma chamada para **ALERT_IF2** poderia fazer todas as funções da **printf** código:  
  
```cpp
ALERT_IF2(someVar > MAX_SOMEVAR, "OVERFLOW! In NameOfThisFunc( ),   
someVar=%d, otherVar=%d.\n", someVar, otherVar );  
```  
  
 Você pode alterar facilmente uma macro personalizada para relatar informações para diferentes destinos de mais ou menos. Essa abordagem é particularmente útil conforme suas necessidades de depuração evoluem.  
  
## <a name="see-also"></a>Consulte também  
 [Técnicas de depuração CRT](../debugger/crt-debugging-techniques.md)
