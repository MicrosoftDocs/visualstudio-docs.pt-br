---
title: Depuração de código gerenciado | Microsoft Docs
ms.date: 09/23/2019
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging managed code
- debugging ASP.NET Web applications, managed code
- managed code, debugging
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: c94de629026cfa1b78429aaf2209b81eead7da4f
ms.sourcegitcommit: ea182703e922c74725045afc251bcebac305068a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71211208"
---
# <a name="debug-managed-code-c-visual-basic-f-ccli"></a>Depurar código gerenciado (C#, Visual Basic, F#, C++/CLI)

Esta seção aborda problemas comuns de depuração e técnicas para aplicativos gerenciados ou aplicativos escritos em linguagens que se destinam à Common Language Runtime C#, como C++Visual Basic, e/CLI. As técnicas descritas aqui são técnicas de alto nível. [Introdução ao depurador](../debugger/debugger-feature-tour.md).

## <a name="in-this-section"></a>Nesta seção

[Mensagens de diagnóstico na Janela de Saída](../debugger/diagnostic-messages-in-the-output-window.md)\
Descreve as classes <xref:System.Diagnostics.Debug> e <xref:System.Diagnostics.Trace>, com as quais você pode escrever mensagens de tempo de execução para a janela **Saída**. Essas classes incluem métodos de saída que permitem a saída de informações sem interromper a execução e a saída de informações que também interrompem a execução se uma condição especificada falhar.

[Asserções em código gerenciado](../debugger/assertions-in-managed-code.md)\
Descreve asserções em código gerenciado, que testam condições que você especifica como argumentos para os métodos `Assert`. Além disso, este tópico fornece código de exemplo, informações sobre como usar os métodos de classe <xref:System.Diagnostics.Debug> e <xref:System.Diagnostics.Trace>, considerações sobre as versões de depuração e lançamento do código, efeitos colaterais, argumentos de declaração, personalização de comportamento de declaração e arquivos de configuração.

[Instruções Stop no Visual Basic](../debugger/stop-statements-in-visual-basic.md)\
Descreve a instrução `Stop`, que fornece uma alternativa para definir um ponto de interrupção. O código de exemplo também é fornecido, junto com comparações entre a instrução `Stop` e a instrução `End`, bem como a instrução `Stop` e `Assert`.

[Passo a passo: Depurando um formulário do Windows](../debugger/walkthrough-debugging-a-windows-form.md)\
Fornece instruções passo a passo para criar um Windows Form e depurar esse formulário. Um Windows Form, um componente padrão de um aplicativo gerenciado do Windows, é um dos aplicativos gerenciados mais comuns. Este passo a passo usa o Visual C # e o Visual Basic, mas as técnicas para criar um Windows Form com C++ geralmente são semelhantes.

[Depuração do método OnStart](../debugger/how-to-debug-the-onstart-method.md)\
Fornece exemplos de código para permitir que você depure o método `OnStart` de um serviço gerenciado do Windows. Para depurar o método `OnStart` de um serviço do Windows, você deverá adicionar algumas linhas de código para simular o serviço.

[Depuração de modo misto](../debugger/debugging-mixed-mode-applications.md)\
Discute aplicativos de modo misto de depuração. Isso significa qualquer aplicativo que combine código nativo com código gerenciado.

[Erro: A depuração não é possível porque um depurador de kernel está habilitado no sistema](../debugger/error-debugging-isn-t-possible-because-a-kernel-debugger-is-enabled-on-the-system.md)\
Descreve uma mensagem de erro que ocorre quando você tenta depurar o código gerenciado em um sistema [!INCLUDE[win7](../debugger/includes/win7_md.md)], [!INCLUDE[wiprlhext](../debugger/includes/wiprlhext_md.md)], [!INCLUDE[winxp](../code-quality/includes/winxp_md.md)], [!INCLUDE[Win2kFamily](../code-quality/includes/win2kfamily_md.md)] ou Windows NT que foi iniciado em modo de depuração.

[Otimização e depuração JIT](../debugger/jit-optimization-and-debugging.md)\
Descreve os efeitos da otimização JIT na depuração.

[Depuração de LINQ e DLINQ](../debugger/debugging-linq.md)\
Discute técnicas para depurar consultas LINQ.

[Passo a passo: Depurando um aplicativo paralelo](../debugger/walkthrough-debugging-a-parallel-application.md)\
Descreve como usar as janelas de ferramentas de **Tarefas Paralelas** e **Pilhas Paralelas** para depurar um aplicativo paralelo.

## <a name="related-sections"></a>Seções relacionadas

[IntelliTrace](../debugger/intellitrace.md)\
Localizar os bugs mais rápido e de maneira mais fácil registrando o histórico de execução do seu aplicativo com IntelliTrace. Retroceda e avance pelos eventos e pelas chamadas registrados para examinar o estado do aplicativo nos pontos-chave em tempo. Depure seu código sem definir muitos pontos de interrupção ou reiniciar o aplicativo com tanta frequência. Requer Visual Studio Enterprise.

[Rastreando e instrumentando aplicativos](/dotnet/framework/debug-trace-profile/tracing-and-instrumenting-applications)\
Descreve o rastreamento, uma maneira de monitorar a execução do aplicativo enquanto está em execução, e a instrumentação, que envolve a colocação de instruções de rastreamento em locais estratégicos em seu código. Este tópico também fornece links para uma introdução à instrumentação e ao rastreamento, alternâncias de rastreamento, ouvintes de rastreamento, código de rastreamento em um aplicativo, adição de instruções de rastreamento no código do aplicativo, e criando condicionalmente com <xref:System.Diagnostics.Debug> e <xref:System.Diagnostics.Trace>.

[/ASSEMBLYDEBUG](/cpp/build/reference/assemblydebug-add-debuggableattribute)\
Descreve uma opção do vinculador que adiciona <xref:System.Diagnostics.DebuggableAttribute> ao código escrito com C++. Esse atributo é necessário para usar os recursos de depuração como, por exemplo, anexar com C++.

[Como depurar aplicativos de serviço do Windows](/dotnet/framework/windows-services/how-to-debug-windows-service-applications)\
Fornece considerações para depurar aplicativos de serviço do Windows, incluindo configuração, anexação ao processo, depuração do código do método `OnStart` do serviço e o código no método principal, definindo pontos de interrupção e usando o Gerenciador de Controle de Serviços para iniciar, parar, pausar e retomar seu serviço.

[Depuração e criação de perfil](/dotnet/framework/debug-trace-profile/index)\
Discute a depuração de aplicativos do .NET Framework e os requisitos de configuração.

[Como depurar aplicativos de script e Web](/visualstudio/debugger/how-to-enable-debugging-for-aspnet-applications)\
Descreve os problemas comuns de depuração e técnicas que você pode encontrar ao depurar aplicativos de script e Web.

## <a name="see-also"></a>Consulte também

- [Passo a passo: Depurar controles de Windows Forms personalizados em tempo de design](/dotnet/framework/winforms/controls/walkthrough-debugging-custom-windows-forms-controls-at-design-time)
- [Segurança do depurador](../debugger/debugger-security.md)
- [Depurando no Visual Studio](../debugger/index.yml)
- [Introdução ao depurador](../debugger/debugger-feature-tour.md)