---
title: Funções de gancho de relatório | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.hooks
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- hooks, report
- _CrtDbgReport function
- debugger, report hook functions
- memory allocation, debug heap
- debugging [C++], hook functions
- _CrtSetReportHook function
- report hook functions
ms.assetid: 1854bca7-d7eb-4502-89bf-b1ee64cb50ef
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 97d39a171d812915a1cf3c1c6450c73098067949
ms.sourcegitcommit: 1ab675a872848c81a44d6b4bd3a49958fe673c56
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2018
ms.locfileid: "44284192"
---
# <a name="report-hook-functions"></a>Funções de gancho do relatório
Uma função de gancho de relatório, instalada usando [crtsetreporthook](/cpp/c-runtime-library/reference/crtsetreporthook), é chamado toda vez [crtdbgreport](/cpp/c-runtime-library/reference/crtdbgreport-crtdbgreportw) gera um relatório de depuração. Você pode usá-la, entre outras coisas, para filtrar relatórios com foco em tipos de alocações específicos. Uma função de gancho de relatório deve ter um protótipo como o seguinte:  
  
```cpp
int YourReportHook(int nRptType, char *szMsg, int *retVal);  
```  
  
 O ponteiro que você passa para **crtsetreporthook** é do tipo **crt_report_hook**, conforme definido em CRTDBG. H:  
  
```cpp
typedef int (__cdecl *_CRT_REPORT_HOOK)(int, char *, int *);  
```  
  
 Quando a biblioteca de tempo de execução chama sua função de gancho, o *nRptType* argumento contém a categoria do relatório (**_CRT_WARN**, **crt_error**, ou **_CRT Macros Assert**), *szMsg* contém um ponteiro para uma cadeia de caracteres de mensagem de relatório completamente montado, e *retVal* Especifica se `_CrtDbgReport` devem continuar em execução normal Depois de gerar o relatório ou inicie o depurador. (Um *retVal* valor igual a zero continua a execução, um valor de 1 inicia o depurador.)  
  
 Se o gancho tratar a mensagem em questão completamente, para que nenhum relatório adicional seja necessária, ele deverá retornar **verdadeira**. Se ele retornar **falsos**, `_CrtDbgReport` relatará a mensagem normalmente.  
  
## <a name="see-also"></a>Consulte também  
 [Gravação da função de gancho de depuração](../debugger/debug-hook-function-writing.md)   
 [Exemplo de crt_dbg2](https://github.com/Microsoft/VCSamples/tree/master/VC2010Samples/crt/crt_dbg2)
