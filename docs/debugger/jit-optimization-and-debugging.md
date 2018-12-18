---
title: JIT otimização e depuração | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], optimized code
- optimized code, debugging
ms.assetid: 19bfabf3-1a2e-49dc-8819-a813982e86fd
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 9a9b18ab38c7c19fa5208d34439bd3133099e8bc
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
ms.locfileid: "31477349"
---
# <a name="jit-optimization-and-debugging"></a>Otimização e depuração JIT
**Como as otimizações funcionam no .NET:** se você está tentando depurar o código, é mais fácil quando que o código é **não** otimizado. Isso ocorre porque quando o código está otimizado, o compilador e o tempo de execução de fazem alterações para o código de CPU emitido para que ele é executado mais rapidamente, mas tem um mapeamento menos direto ao código-fonte original. Isso significa que depuradores são geralmente não é possível informar o valor de variáveis locais e a revisão de código e os pontos de interrupção podem não funcionar conforme o esperado.

Normalmente a configuração de compilação de versão cria código otimizado e a configuração de compilação de depuração não. O `Optimize` propriedade MSBuild controla se o compilador deve otimizar código.

No ecossistema do .NET, código esteja ativado de origem para instruções de CPU em um processo de duas etapas: primeiro, o compilador c# converte o texto digitado em um formato binário intermediário chamado MSIL e grava isso em arquivos. dll. Posteriormente, o tempo de execução do .NET converte este MSIL em instruções de CPU. As duas etapas podem otimizar até certo ponto, mas a segunda etapa executada pelo tempo de execução .NET executa as otimizações mais significativas.

**A opção 'Otimização Suppress JIT no carregamento do módulo (somente gerenciado)':** o depurador expõe uma opção que controla o que acontece quando uma DLL que é compilada com otimizações habilitadas carrega dentro do processo de destino. Se essa opção estiver desmarcada (o estado padrão), em seguida, quando o tempo de execução do .NET compila o código MSIL em código de CPU, ele deixa as otimizações habilitadas. Se a opção estiver marcada, o depurador solicita que otimizações desabilitada.

O **otimização Suppress JIT no carregamento do módulo (somente gerenciado)** opção pode ser encontrada no **geral** página sob o **depuração** nó no **opções** caixa de diálogo.

**Quando você marca essa opção:** marque essa opção quando você baixou as DLLs de outra origem, como um pacote do nuget, e você deseja depurar o código nessa DLL. Em ordem para este trabalho, você também deve localizar o arquivo de símbolo (. PDB) para essa DLL.

Se você só está interessado em depurar o código que você está criando localmente, convém deixar essa opção estiver desmarcada, como, em alguns casos, a habilitação dessa opção será significativamente mais lenta de depuração. Há dois motivos para isso lento:

* Código otimizado é executada mais rapidamente. Se você está desativando otimizações de muita código, o impacto no desempenho pode somar.
* Se você tiver Just My Code ativado, o depurador nem tente e carregar símbolos para DLLs que são otimizados. Localizar símbolos pode levar muito tempo.

**Limitações desta opção:** há duas situações em que essa opção será **não** funcionam:

1. Em situações em que você está anexando o depurador a um processo já em execução, essa opção não terá efeito nos módulos que já foram carregados no momento em que o depurador foi anexado.
2. Essa opção não tem nenhum efeito em DLLs que foram previamente compilado (também conhecidos como ngen'ed) para código nativo. No entanto, você pode desabilitar o uso do código compilado previamente iniciando o processo com o ambiente de que variável 'COMPlus_ZapDisable' definido como '1'.

## <a name="see-also"></a>Consulte também  
 [Depurando código gerenciado](../debugger/debugging-managed-code.md)   
 [Navegar pelo código com o depurador](../debugger/navigating-through-code-with-the-debugger.md)   
 [Anexar a processos em execução](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)   
 [Processo de execução gerenciada](/dotnet/standard/managed-execution-process)
