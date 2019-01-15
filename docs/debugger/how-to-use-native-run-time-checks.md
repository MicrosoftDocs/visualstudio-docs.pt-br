---
title: 'Como: Usar verificações de tempo de execução nativas | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- c.runtime.errorchecks
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- /RTC compiler option [C++], /O compiler option
- run-time checks, native
- stack, pointer corruption
- stack pointers, corruption
- /O compiler option, /RTC option
- run-time errors, error checks
- O compiler option, /RTC option
- debugger, runtime errors
- variables [debugger], loss of data
- runtime_checks pragma
- variables [debugger], catching dependencies on uninitialized local variables
- run-time errors, debugging
- debugger, native run-time checks
- optimized build option
- RTC compiler option, /O compiler option
- native run-time checks
- run-time checks
- debugging arrays
- stack pointers
- arrays [Visual Studio], debugging
ms.assetid: dc7b2f1e-5ff6-42e0-89b3-dc9dead83ee1
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- cplusplus
ms.openlocfilehash: c5f71d6b201213b86caaf9d6e9761975493550a6
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2019
ms.locfileid: "53830950"
---
# <a name="how-to-use-native-run-time-checks"></a>Como: Usar verificações de tempo de execução nativas
No Visual C++, você pode usar nativos [runtime_checks](/cpp/preprocessor/runtime-checks) para capturar erros comuns de tempo de execução, como:  
  
- Dano do ponteiro de pilha.  
  
- Excesso de matrizes locais.  
  
- Dano de pilha.  
  
- Dependências em variáveis locais não inicializadas.  
  
- Perda de dados em uma atribuição para uma variável mais curta.  
  
  Se você usar **/RTC** com um otimizado (**/O**) criar um resultados de erro do compilador. Se você usar um pragma `runtime_checks` em uma construção otimizada, o pragma não terá nenhum efeito.  
  
  Quando você depurar um programa que tem as verificações de tempo de execução habilitadas, a ação padrão será para o programa parar e interromper no depurador quando ocorrer um erro em tempo de execução. Você pode alterar este comportamento padrão para qualquer verificação de tempo de execução. Para obter mais informações, consulte [Gerenciando exceções com o depurador](../debugger/managing-exceptions-with-the-debugger.md).  
  
  Os procedimentos a seguir descrevem como habilitar as verificações nativas de tempo de execução em uma compilação de depuração e como modificar o comportamento nativo de verificação de tempo de execução.  
  
  Outros tópicos desta seção fornecem informações sobre:  
  
- [Personalizando as verificações de tempo de execução com a biblioteca em tempo de execução C](../debugger/native-run-time-checks-customization.md)  
  
- [Usando verificações de tempo de execução sem a biblioteca em tempo de execução do C](../debugger/using-run-time-checks-without-the-c-run-time-library.md)  
  
### <a name="to-enable-native-run-time-checks-in-a-debug-build"></a>Para habilitar as verificações de tempo de execução nativas em uma compilação de depuração  
  
-   Use o **/RTC** opção e vincule com a versão de depuração de uma biblioteca de tempo de execução do C (/ MDd, por exemplo).  
  
### <a name="to-modify-native-run-time-check-behavior"></a>Para modificar o comportamento nativo de verificação de tempo de execução  
  
-   Use o pragma `runtime_checks`.  
  
## <a name="see-also"></a>Consulte também  
 [Depurando no Visual Studio](../debugger/index.md)  
 [Tour dos recursos do depurador](../debugger/debugger-feature-tour.md)   
 [runtime_checks](/cpp/preprocessor/runtime-checks)   
 [Verificação de erros em tempo de execução](/cpp/c-runtime-library/run-time-error-checking)