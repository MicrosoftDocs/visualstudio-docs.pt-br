---
title: Macros para relatórios | Microsoft Docs
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
- vs.debug.macros
dev_langs:
- FSharp
- VB
- CSharp
- C++
- C++
helpviewer_keywords:
- macros, CRT reporting macros
- macros, debugging with
- _RPTFn macro
- CRT, reporting macros
- debugging [CRT], reporting macros
- _RPTn macro
ms.assetid: f2085314-a3a8-4caf-a5a4-2af9ad5aad05
caps.latest.revision: 18
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: dc2a5226b3d6f512d2c2f89d9fef2a80eef34340
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51758450"
---
# <a name="macros-for-reporting"></a>Macros para relatórios
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode usar o **rptn**, e **rptfn** macros, definidas em CRTDBG. H, para substituir o uso de `printf` instruções para depuração. Essas macros desaparecem automaticamente na sua versão de compilação quando **Debug** não estiver definido, portanto, não há nenhuma necessidade de incluí-los em **#ifdef**s.  
  
|Macro|Descrição|  
|-----------|-----------------|  
|**_RPT0**, **_RPT1**, **_RPT2**, **_RPT3**, **_RPT4**|Gera uma cadeia de caracteres de mensagem e zero a quatro argumentos. Para _RPT1 até **_RPT4**, a cadeia de caracteres de mensagem serve como uma cadeia de caracteres de formatação de estilo printf para os argumentos.|  
|**_RPTF0**, **_RPTF1**, **, _RPTF2**, **_RPTF4**|Mesmo que **rptn** , mas essas macros também o número de linha e de nome de arquivo onde se encontra a macro de saída.|  
  
 Considere o exemplo a seguir:  
  
```  
#ifdef _DEBUG  
    if ( someVar > MAX_SOMEVAR )  
        printf( "OVERFLOW! In NameOfThisFunc( ),  
               someVar=%d, otherVar=%d.\n",  
               someVar, otherVar );  
#endif  
```  
  
 Esse código gera os valores de `someVar` e `otherVar` à **stdout**. Você pode usar a seguinte chamada para `_RPTF2` para reportar os mesmos valores e, além disso, o nome de arquivo e o número de linha:  
  
```  
if (someVar > MAX_SOMEVAR) _RPTF2(_CRT_WARN, "In NameOfThisFunc( ), someVar= %d, otherVar= %d\n", someVar, otherVar );  
```  
  
 Se você achar que um aplicativo específico precisa de um relatório de depuração que as macros fornecidas com a biblioteca em tempo de execução C não fornecem, poderá escrever uma macro criada especificamente para se adaptar a seus próprios requisitos. Em um dos arquivos de cabeçalho, por exemplo, você pode incluir código como o seguinte para definir uma macro chamada **ALERT_IF2**:  
  
```  
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
  
 Uma chamada para **ALERT_IF2** poderia executar todas as funções da **printf** código no início deste tópico:  
  
```  
ALERT_IF2(someVar > MAX_SOMEVAR, "OVERFLOW! In NameOfThisFunc( ),   
someVar=%d, otherVar=%d.\n", someVar, otherVar );  
```  
  
 Como uma macro personalizada pode ser alterada facilmente para reportar mais ou menos informações para os destinos diferentes (dependendo do que é mais conveniente), essa abordagem pode ser útil principalmente à medida que seus requisitos de depuração evoluem.  
  
## <a name="see-also"></a>Consulte também  
 [Técnicas de depuração CRT](../debugger/crt-debugging-techniques.md)



