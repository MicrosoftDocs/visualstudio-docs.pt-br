---
title: Como gerenciar vários threads no código gerenciado | Microsoft Docs
description: Saiba como gerenciar vários threads no código se a extensão gerenciada do VSPackage chamar métodos assíncronos ou tiver operações fora do thread Visual Studio interface do usuário.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 59730063-cc29-4dae-baff-2234ad8d0c8f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 39319b748dd41c6936e7b70e20243202452fae67
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112903080"
---
# <a name="how-to-manage-multiple-threads-in-managed-code"></a>Como gerenciar vários threads em código gerenciado
Se você tiver uma extensão gerenciada do VSPackage que chama métodos assíncronos ou tem operações que são executadas em threads diferentes do thread de interface do usuário do Visual Studio, siga as diretrizes fornecidas abaixo. Você pode manter o thread da interface do usuário responsivo porque ele não precisa aguardar a conclusão do trabalho em outro thread. Você pode tornar seu código mais eficiente, porque você não tem threads extras que levam espaço na pilha e pode torná-lo mais confiável e fácil de depurar porque evita deadlocks e código sem resposta.

 Em geral, você pode alternar do thread da interface do usuário para um thread diferente ou vice-versa. Quando o método retorna, o thread atual é o thread do qual foi originalmente chamado.

> [!IMPORTANT]
> As diretrizes a seguir usam as APIs no <xref:Microsoft.VisualStudio.Threading> namespace, em particular, a <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory> classe . As APIs neste namespace são novas no [!INCLUDE[vs_dev12](../extensibility/includes/vs_dev12_md.md)] . Você pode obter uma instância de um <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory> da <xref:Microsoft.VisualStudio.Shell.ThreadHelper> propriedade `ThreadHelper.JoinableTaskFactory` .

## <a name="switch-from-the-ui-thread-to-a-background-thread"></a>Alternar do thread da interface do usuário para um thread em segundo plano

1. Se você estiver no thread da interface do usuário e quiser fazer um trabalho assíncrono em um thread em segundo plano, use `Task.Run()` :

    ```csharp
    await Task.Run(async delegate{
        // Now you're on a separate thread.
    });
    // Now you're back on the UI thread.

    ```

2. Se você estiver no thread da interface do usuário e quiser bloquear de forma síncrona enquanto estiver executando o trabalho em um thread em segundo plano, use a propriedade <xref:System.Threading.Tasks.TaskScheduler> `TaskScheduler.Default` dentro de <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.Run%2A> :

    ```csharp
    // using Microsoft.VisualStudio.Threading;
    ThreadHelper.JoinableTaskFactory.Run(async delegate {
        await TaskScheduler.Default;
        // You're now on a separate thread.
        DoSomethingSynchronous();
        await OrSomethingAsynchronous();
    });
    ```

## <a name="switch-from-a-background-thread-to-the-ui-thread"></a>Alternar de um thread em segundo plano para o thread de interface do usuário

1. Se você estiver em um thread em segundo plano e quiser fazer algo no thread da interface do usuário, use <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.SwitchToMainThreadAsync%2A> :

    ```csharp
    // Switch to main thread
    await ThreadHelper.JoinableTaskFactory.SwitchToMainThreadAsync();
    ```

     Você pode usar o <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.SwitchToMainThreadAsync%2A> método para alternar para o thread da interface do usuário. Esse método posta uma mensagem no thread da interface do usuário com a continuação do método assíncrono atual e também se comunica com o restante da estrutura de threading para definir a prioridade correta e evitar deadlocks.

     Se o método de thread em segundo plano não for assíncrono e você não puder torná-lo assíncrono, você ainda poderá usar a sintaxe para alternar para o thread da interface do usuário, envolvendo seu trabalho com , como `await` <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.Run%2A> neste exemplo:

    ```csharp
    ThreadHelper.JoinableTaskFactory.Run(async delegate {
        // Switch to main thread
        await ThreadHelper.JoinableTaskFactory.SwitchToMainThreadAsync();
        // Do your work on the main thread here.
    });
    ```
