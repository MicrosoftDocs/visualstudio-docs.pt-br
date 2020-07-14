---
title: 'Como: usar AsyncPackage para carregar VSPackages em segundo plano | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: dedf0173-197e-4258-ae5a-807eb3abc952
author: acangialosi
ms.author: anthc
ms.workload:
- vssdk
ms.openlocfilehash: 7727d53c84ab876fe6616c8ec5d438033216481e
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905597"
---
# <a name="how-to-use-asyncpackage-to-load-vspackages-in-the-background"></a>Como: usar AsyncPackage para carregar VSPackages em segundo plano
Carregar e inicializar um pacote do VS pode resultar em e/s de disco. Se essa e/s ocorrer no thread da interface do usuário, isso pode levar a problemas de capacidade de resposta. Para resolver isso, o Visual Studio 2015 introduziu a <xref:Microsoft.VisualStudio.Shell.AsyncPackage> classe que habilita o carregamento do pacote em um thread em segundo plano.

## <a name="create-an-asyncpackage"></a>Criar um AsyncPackage
 Você pode começar criando um projeto VSIX (**arquivo**  >  **novo**projeto de  >  **Project**  >  VSIX de extensibilidade do**Visual C#**  >  **Extensibility**  >  **VSIX Project**) e adicionando um VSPackage ao projeto (clique com o botão direito do mouse no projeto e **adicione**  >  **novo item**  >  **C# item**  >  **extensibilidade**  >  **Visual Studio Package**). Você pode criar seus serviços e adicionar esses serviços ao seu pacote.

1. Derive o pacote de <xref:Microsoft.VisualStudio.Shell.AsyncPackage> .

2. Se você estiver fornecendo serviços cuja consulta pode fazer com que o pacote seja carregado:

    Para indicar ao Visual Studio que seu pacote é seguro para carregamento em segundo plano e para aceitar esse comportamento, você <xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute> deve definir a propriedade **AllowsBackgroundLoading** como true no construtor de atributo.

   ```csharp
   [PackageRegistration(UseManagedResourcesOnly = true, AllowsBackgroundLoading = true)]

   ```

    Para indicar ao Visual Studio que é seguro instanciar seu serviço em um thread em segundo plano, você deve definir a <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttributeBase.IsAsyncQueryable%2A> propriedade como true no <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute> Construtor.

   ```csharp
   [ProvideService(typeof(SMyTestService), IsAsyncQueryable = true)]

   ```

3. Se você estiver carregando por meio de contextos de interface do usuário, deverá especificar **PackageAutoLoadFlags. BackgroundLoad** para o <xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute> ou o valor (0x2) nos sinalizadores gravados como o valor da entrada de carga automática do pacote.

   ```csharp
   [ProvideAutoLoad(UIContextGuid, PackageAutoLoadFlags.BackgroundLoad)]

   ```

4. Se você tiver o trabalho de inicialização assíncrona para fazer, você deve substituir <xref:Microsoft.VisualStudio.Shell.AsyncPackage.InitializeAsync%2A> . Remova o `Initialize()` método fornecido pelo modelo VSIX. (O `Initialize()` método em **AsyncPackage** é lacrado). Você pode usar qualquer um dos <xref:Microsoft.VisualStudio.Shell.AsyncPackage.AddService%2A> métodos para adicionar serviços assíncronos ao seu pacote.

    Observação: para chamar `base.InitializeAsync()` , você pode alterar o código-fonte para:

   ```csharp
   await base.InitializeAsync(cancellationToken, progress);
   ```

5. Você deve tomar cuidado para não fazer RPCs (chamada de procedimento remoto) do seu código de inicialização assíncrona (em **InitializeAsync**). Isso pode ocorrer quando você chama <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> direta ou indiretamente.  Quando são necessárias cargas de sincronização, o thread da interface do usuário bloqueará o uso do <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory> . O modelo de bloqueio padrão desabilita RPCs. Isso significa que se você tentar usar um RPC a partir de suas tarefas assíncronas, você será deadlock se o thread da interface do usuário estiver aguardando o carregamento do seu pacote. A alternativa geral é empacotar seu código para o thread da interface do usuário, se necessário, usando algo como **alocador de tarefas de junção** <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.SwitchToMainThreadAsync%2A> ou algum outro mecanismo que não use um RPC.  Não use **ThreadHelper. Generic. Invoke** ou, geralmente, bloqueie o thread de chamada aguardando para chegar ao thread da interface do usuário.

    Observação: você deve evitar usar **GetService** ou **QueryService** em seu `InitializeAsync` método. Se você precisar usá-los, precisará mudar para o thread da interface do usuário primeiro. A alternativa é usar <xref:Microsoft.VisualStudio.Shell.AsyncServiceProvider.GetServiceAsync%2A> de seu **AsyncPackage** (convertendo-o para <xref:Microsoft.VisualStudio.Shell.Interop.IAsyncServiceProvider> .)

   C#: criar um AsyncPackage:

```csharp
[PackageRegistration(UseManagedResourcesOnly = true, AllowsBackgroundLoading = true)]
[ProvideService(typeof(SMyTestService), IsAsyncQueryable = true)]
public sealed class TestPackage : AsyncPackage
{
    protected override Task InitializeAsync(System.Threading.CancellationToken cancellationToken, IProgress<ServiceProgressData> progress)
    {
        this.AddService(typeof(SMyTestService), CreateService, true);
        return Task.FromResult<object>(null);
    }
}
```

## <a name="convert-an-existing-vspackage-to-asyncpackage"></a>Converter um VSPackage existente em AsyncPackage
 A maior parte do trabalho é a mesma que criar um novo **AsyncPackage**. Siga as etapas 1 a 5 acima. Você também precisa tomar cuidado adicional com as seguintes recomendações:

1. Lembre-se de remover a `Initialize` substituição que você tinha em seu pacote.

2. Evitar deadlocks: pode haver RPCs ocultas em seu código. que agora acontece em um thread em segundo plano. Certifique-se de que, se você estiver fazendo um RPC (por exemplo, **GetService**), será necessário (1) alternar para o thread principal ou (2) usar a versão assíncrona da API, se existir uma (por exemplo, **GetServiceAsync**).

3. Não alterne entre threads com muita frequência. Tente localizar o trabalho que pode ocorrer em um thread em segundo plano para reduzir o tempo de carregamento.

## <a name="querying-services-from-asyncpackage"></a>Consultando serviços do AsyncPackage
 Um **AsyncPackage** pode ou não ser carregado de forma assíncrona, dependendo do chamador. Por exemplo,

- Se o chamador chamou **GetService** ou **QueryService** (ambas as APIs síncronas) ou

- Se o chamador chamou **IVsShell:: LoadPackage** (ou **IVsShell5:: LoadPackageWithContext**) ou

- A carga é disparada por um contexto de interface do usuário, mas você não especificou que o mecanismo de contexto da interface do usuário pode carregá-lo assincronamente

  em seguida, o pacote será carregado de forma síncrona.

  Seu pacote ainda tem uma oportunidade (em sua fase de inicialização assíncrona) para fazer o trabalho fora do thread da interface do usuário, embora o thread da interface do usuário seja bloqueado para a conclusão desse trabalho. Se o chamador usar **IAsyncServiceProvider** para consultar de forma assíncrona o serviço, a carga e a inicialização serão feitas de forma assíncrona, supondo que não bloqueiem imediatamente o objeto de tarefa resultante.

  C#: como consultar o serviço de forma assíncrona:

```csharp
using Microsoft.VisualStudio.Shell;
using Microsoft.VisualStudio.Shell.Interop;

IAsyncServiceProvider asyncServiceProvider = Package.GetService(typeof(SAsyncServiceProvider)) as IAsyncServiceProvider;
IMyTestService testService = await asyncServiceProvider.GetServiceAsync(typeof(SMyTestService)) as IMyTestService;
```
