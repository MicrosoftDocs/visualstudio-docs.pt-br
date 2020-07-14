---
title: 'Como: fornecer um serviço assíncrono do Visual Studio | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 0448274c-d3d2-4e12-9d11-8aca78a1f3f5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ad178bf93e49c3d695c1ebd0a5d4f6b151175953
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905733"
---
# <a name="how-to-provide-an-asynchronous-visual-studio-service"></a>Como: fornecer um serviço assíncrono do Visual Studio
Se você quiser obter um serviço sem bloquear o thread da interface do usuário, deverá criar um serviço assíncrono e carregar o pacote em um thread em segundo plano. Para essa finalidade, você pode usar um <xref:Microsoft.VisualStudio.Shell.AsyncPackage> em vez de um <xref:Microsoft.VisualStudio.Shell.Package> e adicionar o serviço com os métodos assíncronos especiais do pacote assíncrono.

 Para obter informações sobre como fornecer serviços síncronos do Visual Studio, consulte [como fornecer um serviço](../extensibility/how-to-provide-a-service.md).

## <a name="implement-an-asynchronous-service"></a>Implementar um serviço assíncrono

1. Crie um projeto VSIX (**arquivo**  >  **novo**  >  **projeto**  >  **Visual C#**  >  **extensiblity**  >  **VSIX Project**). Nomeie o projeto **TestAsync**.

2. Adicione um VSPackage ao projeto. Selecione o nó do projeto na **Gerenciador de soluções** e clique em **Adicionar**  >  **novo item**  >  **Visual C# itens**  >  **extensibilidade**  >  **Visual Studio pacote**. Nomeie esse arquivo *TestAsyncPackage.cs*.

3. Em *TestAsyncPackage.cs*, altere o pacote para herdar de `AsyncPackage` em vez de `Package` :

    ```csharp
    public sealed class TestAsyncPackage : AsyncPackage
    ```

4. Para implementar um serviço, você precisa criar três tipos:

    - Uma interface que identifica o serviço. Muitas dessas interfaces estão vazias, ou seja, não têm métodos, pois são usadas apenas para consultar o serviço.

    - Uma interface que descreve a interface do serviço. Essa interface inclui os métodos a serem implementados.

    - Uma classe que implementa o serviço e a interface de serviço.

5. O exemplo a seguir mostra uma implementação muito básica dos três tipos. O construtor da classe de serviço deve definir o provedor de serviços. Neste exemplo, vamos apenas adicionar o serviço ao arquivo de código do pacote.

6. Adicione as seguintes diretivas using ao arquivo de pacote:

    ```csharp
    using System.Threading;
    using System.Threading.Tasks;
    using System.Runtime.CompilerServices;
    using System.IO;
    using Microsoft.VisualStudio.Threading;
    using IAsyncServiceProvider = Microsoft.VisualStudio.Shell.IAsyncServiceProvider;
    using Task = System.Threading.Tasks.Task;
    ```

7. Aqui está a implementação do serviço assíncrono. Observe que você precisa definir o provedor de serviços assíncrono em vez do provedor de serviços síncrono no construtor:

    ```csharp
    public class TextWriterService : STextWriterService, ITextWriterService
    {
        private IAsyncServiceProvider asyncServiceProvider;

        public TextWriterService(IAsyncServiceProvider provider)
        {
            // constructor should only be used for simple initialization
            // any usage of Visual Studio service, expensive background operations should happen in the
            // asynchronous InitializeAsync method for best performance
            asyncServiceProvider = provider;
        }

        public async Task InitializeAsync(CancellationToken cancellationToken)
        {
            await TaskScheduler.Default;
            // do background operations that involve IO or other async methods

            await ThreadHelper.JoinableTaskFactory.SwitchToMainThreadAsync(cancellationToken);
            // query Visual Studio services on main thread unless they are documented as free threaded explicitly.
            // The reason for this is the final cast to service interface (such as IVsShell) may involve COM operations to add/release references.

            IVsShell vsShell = this.asyncServiceProvider.GetServiceAsync(typeof(SVsShell)) as IVsShell;
            // use Visual Studio services to continue initialization
        }

        public async Task WriteLineAsync(string path, string line)
        {
            StreamWriter writer = new StreamWriter(path);
            await writer.WriteLineAsync(line);
            writer.Close();
        }
    }

    public interface STextWriterService
    {
    }

    public interface ITextWriterService
    {
        System.Threading.Tasks.Task WriteLineAsync(string path, string line);
    }
    ```

## <a name="register-a-service"></a>Registrar um serviço
 Para registrar um serviço, adicione o <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute> ao pacote que fornece o serviço. Diferente para registrar um serviço síncrono, você precisa garantir que o pacote e o serviço ofereçam suporte ao carregamento assíncrono:

- Você deve adicionar o campo **AllowsBackgroundLoading = true** ao <xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute> para garantir que o pacote possa ser inicializado de forma assíncrona para obter mais informações sobre o PackageRegistrationAttribute, consulte [registrar e cancelar o registro de VSPackages](../extensibility/registering-and-unregistering-vspackages.md).

- Você deve adicionar o campo **IsAsyncQueryable = true** ao <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute> para garantir que a instância de serviço possa ser inicializada de forma assíncrona.

  Aqui está um exemplo de um `AsyncPackage` com um registro de serviço assíncrono:

```csharp
[ProvideService((typeof(STextWriterService)), IsAsyncQueryable = true)]
[ProvideAutoLoad(UIContextGuids80.SolutionExists, PackageAutoLoadFlags.BackgroundLoad)]
[PackageRegistration(UseManagedResourcesOnly = true, AllowsBackgroundLoading = true)]
[Guid(TestAsyncPackage.PackageGuidString)]
public sealed class TestAsyncPackage : AsyncPackage
{. . . }
```

## <a name="add-a-service"></a>Adicionar um serviço

1. No *TestAsyncPackage.cs*, remova o `Initialize()` método e substitua o `InitializeAsync()` método. Adicione o serviço e adicione um método de retorno de chamada para criar os serviços. Aqui está um exemplo do inicializador assíncrono adicionando um serviço:

    ```csharp
    protected override async Task InitializeAsync(CancellationToken cancellationToken, IProgress<ServiceProgressData> progress)
    {
        await base.InitializeAsync(cancellationToken, progress);
        this.AddService(typeof(STextWriterService), CreateTextWriterService);
    }

    ```
    Para tornar esse serviço visível fora deste pacote, defina o valor do sinalizador Promote como *verdadeiro* como o último parâmetro:`this.AddService(typeof(STextWriterService), CreateTextWriterService, true);`

2. Adicione uma referência a *Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll*.

3. Implemente o método de retorno de chamada como um método assíncrono que cria e retorna o serviço.

    ```csharp
    public async Task<object> CreateTextWriterService(IAsyncServiceContainer container, CancellationToken cancellationToken, Type serviceType)
    {
        TextWriterService service = new TextWriterService(this);
        await service.InitializeAsync(cancellationToken);
        return service;
    }

    ```

## <a name="use-a-service"></a>Usar um serviço
 Agora você pode obter o serviço e usar seus métodos.

1. Mostraremos isso no inicializador, mas você poderá obter o serviço em qualquer lugar em que desejar usar o serviço.

    ```csharp
    protected override async System.Threading.Tasks.Task InitializeAsync(CancellationToken cancellationToken, IProgress<ServiceProgressData> progress)
    {
        await base.InitializeAsync(cancellationToken, progress);
        this.AddService(typeof(STextWriterService), CreateTextWriterService);

        ITextWriterService textService = await this.GetServiceAsync(typeof(STextWriterService)) as ITextWriterService;
        string userpath = @"C:\MyDir\MyFile.txt";
        await textService.WriteLineAsync(userpath, "this is a test");
    }

    ```

     Não se esqueça de alterar `userpath` para um nome de arquivo e caminho que faça sentido em seu computador!

2. Compile e execute o código. Quando a instância experimental do Visual Studio for exibida, abra uma solução. Isso faz com que o `AsyncPackage` seja o para AutoLoad. Quando o inicializador tiver sido executado, você deverá encontrar um arquivo no local especificado.

## <a name="use-an-asynchronous-service-in-a-command-handler"></a>Usar um serviço assíncrono em um manipulador de comandos
 Aqui está um exemplo de como usar um serviço assíncrono em um comando de menu. Você pode usar o procedimento mostrado aqui para usar o serviço em outros métodos não assíncronos.

1. Adicione um comando de menu ao seu projeto. (No **Gerenciador de soluções**, selecione o nó do projeto, clique com o botão direito do mouse e selecione **Adicionar**  >  **Novo item**  >  **Extensibilidade**  >  do **Comando personalizado**.) Nomeie o arquivo de comando *TestAsyncCommand.cs*.

2. O modelo de comando personalizado adiciona novamente o `Initialize()` método ao arquivo *TestAsyncPackage.cs* para inicializar o comando. No `Initialize()` método, copie a linha que inicializa o comando. O resultado deve ser assim:

    ```csharp
    TestAsyncCommand.Initialize(this);
    ```

     Mova essa linha para o `InitializeAsync()` método no arquivo *AsyncPackageForService.cs* . Como isso está em uma inicialização assíncrona, você deve alternar para o thread principal antes de inicializar o comando usando <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.SwitchToMainThreadAsync%2A> . Agora, ele deve ser assim:

    ```csharp

    protected override async System.Threading.Tasks.Task InitializeAsync(CancellationToken cancellationToken, IProgress<ServiceProgressData> progress)
    {
        await base.InitializeAsync(cancellationToken, progress);
        this.AddService(typeof(STextWriterService), CreateTextWriterService);

        ITextWriterService textService =
           await this.GetServiceAsync(typeof(STextWriterService)) as ITextWriterService;
        
        string userpath = @"C:\MyDir\MyFile.txt";
        await textService.WriteLineAsync(userpath, "this is a test");

        await this.JoinableTaskFactory.SwitchToMainThreadAsync(cancellationToken);
        TestAsyncCommand.Initialize(this);
    }

    ```

3. Exclua o `Initialize()` método.

4. No arquivo *TestAsyncCommand.cs* , localize o `MenuItemCallback()` método. Exclua o corpo do método.

5. Adicione uma diretiva using:

    ```csharp
    using System.IO;
    ```

6. Adicione um método assíncrono chamado `UseTextWriterAsync()` , que obtém o serviço e usa seus métodos:

    ```csharp
    private async System.Threading.Tasks.Task UseTextWriterAsync()
    {
        // Query text writer service asynchronously to avoid a blocking call.
        ITextWriterService textService =
           await AsyncServiceProvider.GlobalProvider.GetServiceAsync(typeof(STextWriterService))
              as ITextWriterService;

        string userpath = @"C:\MyDir\MyFile.txt";
        await textService.WriteLineAsync(userpath, "this is a test");
       }

    ```

7. Chame esse método do `MenuItemCallback()` método:

    ```csharp
    private void MenuItemCallback(object sender, EventArgs e)
    {
        UseTextWriterAsync();
    }

    ```

8. Compile a solução e inicie a depuração. Quando a instância experimental do Visual Studio for exibida, vá para o menu **ferramentas** e procure o item de menu **invocar TestAsyncCommand** . Quando você clica nele, o TextWriterService grava no arquivo especificado. (Você não precisa abrir uma solução, pois invocar o comando também faz com que o pacote seja carregado.)

## <a name="see-also"></a>Confira também
- [Usar e fornecer serviços](../extensibility/using-and-providing-services.md)
