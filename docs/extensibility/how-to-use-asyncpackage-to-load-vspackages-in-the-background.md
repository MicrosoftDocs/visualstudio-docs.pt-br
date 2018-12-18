---
title: 'Como: usar AsyncPackage para carregar VSPackages em segundo plano | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.topic: conceptual
ms.technology: vs-ide-sdk
ms.assetid: dedf0173-197e-4258-ae5a-807eb3abc952
author: gregvanl
ms.author: gregvanl
ms.workload:
- vssdk
ms.openlocfilehash: 1afd0199401159ace6ccc34bf3f32aa564cf195f
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49828514"
---
# <a name="how-to-use-asyncpackage-to-load-vspackages-in-the-background"></a>Como: usar AsyncPackage para carregar VSPackages em segundo plano
Carregar e inicializar um VS package podem resultar em e/s de disco. Se tal e/s acontece no thread da interface do usuário, ele pode levar a problemas de capacidade de resposta. Para resolver isso, o Visual Studio 2015 apresentou a <xref:Microsoft.VisualStudio.Shell.AsyncPackage> classe que habilita o carregamento do pacote em um thread em segundo plano.  
  
## <a name="create-an-asyncpackage"></a>Criar um AsyncPackage  
 Você pode começar criando um projeto VSIX (**arquivo** > **New** > **projeto** > **Visual C#**   >  **Extensibilidade** > **projeto VSIX**) e a adição de um VSPackage ao projeto (clique com botão direito no projeto e **adicionar**  >  **Novo Item**  >   **C# item** > **extensibilidade**  >   **Pacote do Visual Studio**). Em seguida, você pode criar seus serviços e adicionar esses serviços ao seu pacote.  
  
1. Derivar o pacote de <xref:Microsoft.VisualStudio.Shell.AsyncPackage>.  
  
2. Se você estiver fornecendo serviços cuja consulta pode fazer com que o pacote a ser carregado:  
  
    Para indicar para o Visual Studio que o pacote é seguro para carregamento em segundo plano e para aceitar esse comportamento, sua <xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute> deve definir **AllowsBackgroundLoading** propriedade como true no construtor de atributo.  
  
   ```csharp  
   [PackageRegistration(UseManagedResourcesOnly = true, AllowsBackgroundLoading = true)]  
  
   ```  
  
    Para indicar para o Visual Studio que é seguro instanciar seu serviço em um thread em segundo plano, você deve definir a <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttributeBase.IsAsyncQueryable%2A> propriedade como true no <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute> construtor.  
  
   ```csharp  
   [ProvideService(typeof(SMyTestService), IsAsyncQueryable = true)]  
  
   ```  
  
3. Se você estiver carregando por meio de contextos de interface do usuário, você deve especificar **PackageAutoLoadFlags.BackgroundLoad** para o <xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute> ou o valor (0x2) para os sinalizadores escrito como o valor da entrada de carga automático do seu pacote.  
  
   ```csharp  
   [ProvideAutoLoad(UIContextGuid, PackageAutoLoadFlags.BackgroundLoad)]  
  
   ```  
  
4. Se você tiver a inicialização assíncrona de trabalho, você deve substituir <xref:Microsoft.VisualStudio.Shell.AsyncPackage.InitializeAsync%2A>. Remover o `Initialize()` método fornecido pelo modelo do VSIX. (O `Initialize()` método no **AsyncPackage** está lacrado). Você pode usar qualquer um do <xref:Microsoft.VisualStudio.Shell.AsyncPackage.AddService%2A> métodos para adicionar serviços assíncronos ao seu pacote.  
  
    Observação: Para chamar `base.InitializeAsync()`, você pode alterar seu código-fonte para:  
  
   ```csharp  
   await base.InitializeAsync(cancellationToken, progress);  
   ```  
  
5. Você deve tomar cuidado para não ter RPCs (chamada de procedimento remoto) do seu código de inicialização assíncrona (em **InitializeAsync**). Elas podem ocorrer quando você chama <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> direta ou indiretamente.  Quando as cargas de sincronização são necessárias, o thread de interface do usuário bloqueará o uso <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory>. O modelo de bloqueio padrão desabilita RPCs. Isso significa que, se você tentar usar uma RPC de suas tarefas assíncronas, enfrentarão deadlock se o thread de interface do usuário é esperar que o pacote a ser carregado. A alternativa geral é realizar marshaling de seu código para o thread de interface do usuário se for necessário usar algo como **fábrica de tarefas permite junções**do <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.SwitchToMainThreadAsync%2A> ou algum outro mecanismo que não usa um RPC.  Não use **ThreadHelper.Generic.Invoke** ou geralmente bloquear o thread de chamada aguarda para obter o thread de interface do usuário.  
  
    Observação: Você deve evitar usar **GetService** ou **QueryService** em seu `InitializeAsync` método. Se você tiver de usá-los, você precisará alternar para o thread de interface do usuário pela primeira vez. A alternativa é usar <xref:Microsoft.VisualStudio.Shell.AsyncServiceProvider.GetServiceAsync%2A> de seu **AsyncPackage** (convertendo-o para <xref:Microsoft.VisualStudio.Shell.Interop.IAsyncServiceProvider>.)  
  
   C#: Crie um AsyncPackage:  
  
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
 A maioria do trabalho é o mesmo que criar um novo **AsyncPackage**. Siga as etapas 1 a 5 acima. Você também precisará tomar muito cuidado com as seguintes recomendações:  
  
1.  Lembre-se de remover o `Initialize` tinha em seu pacote de substituição.  
  
2.  Evitar deadlocks: pode haver oculto RPCs em seu código. Agora, que ocorrem em um thread em segundo plano. Certifique-se de que se você estiver fazendo uma RPC (por exemplo, **GetService**), você precisa para qualquer comutador (1) para o thread principal ou (2) use a versão assíncrona da API se um existe (por exemplo, **GetServiceAsync**).  
  
3.  Não alterne entre threads com muita frequência. Tente localizar o trabalho que pode ocorrer em um thread em segundo plano para reduzir o tempo de carregamento.  
  
## <a name="querying-services-from-asyncpackage"></a>Consultando serviços de AsyncPackage  
 Uma **AsyncPackage** podem ou não carregar assincronamente, dependendo do chamador. Por exemplo,  
  
- Se o chamador chamado **GetService** ou **QueryService** (ambas as APIs síncronas) ou  
  
- Se o chamador chamado **IVsShell::LoadPackage** (ou **IVsShell5::LoadPackageWithContext**) ou  
  
- O carregamento é disparado por um contexto de interface do usuário, mas você não especificou que o mecanismo de contexto da interface do usuário pode carregar você de forma assíncrona  
  
  em seguida, seu pacote será carregado de forma síncrona.  
  
  Seu pacote ainda tem uma oportunidade (em sua fase de inicialização assíncrona) para fazer o trabalho fora do thread de interface do usuário, embora o thread de interface do usuário será bloqueado para a conclusão de que o do trabalho. Se o chamador usa **IAsyncServiceProvider** para consultar assincronamente para seu serviço, em seguida, de carga e de inicialização serão feitos assincronamente supondo que eles não bloqueiam imediatamente no objeto de tarefa resultante.  
  
  C#: Como consultar o serviço de forma assíncrona:  
  
```csharp  
using Microsoft.VisualStudio.Shell;   
using Microsoft.VisualStudio.Shell.Interop;   
  
IAsyncServiceProvider asyncServiceProvider = Package.GetService(typeof(SAsyncServiceProvider)) as IAsyncServiceProvider;   
IMyTestService testService = await asyncServiceProvider.GetServiceAsync(typeof(SMyTestService)) as IMyTestService;  
```
  
