---
title: 'Como: fornecer um serviço assíncrono do Visual Studio | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 0448274c-d3d2-4e12-9d11-8aca78a1f3f5
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: c022f1a039aacee3599dd680adfa92a9404b34b8
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49915666"
---
# <a name="how-to-provide-an-asynchronous-visual-studio-service"></a>Como: fornecer um serviço assíncrono do Visual Studio
Se você quiser obter um serviço sem bloquear o thread de interface do usuário, você deve criar um serviço assíncrono e carregar o pacote em um thread em segundo plano. Para essa finalidade, você pode usar um <xref:Microsoft.VisualStudio.Shell.AsyncPackage> em vez de um <xref:Microsoft.VisualStudio.Shell.Package>e adicione o serviço com os métodos assíncronos especial do pacote assíncrono.
  
 Para obter informações sobre o fornecimento de serviços síncronos do Visual Studio, consulte [como: fornecer um serviço](../extensibility/how-to-provide-a-service.md).  
  
## <a name="implement-an-asynchronous-service"></a>Implementar um serviço assíncrono  
  
1.  Crie um projeto VSIX (**arquivo** > **New** > **projeto** > **Visual C#**  >  **Extensibilidade** > **projeto VSIX**). Nomeie o projeto **TestAsync**.  
  
2.  Adicione um VSPackage ao projeto. Selecione o nó do projeto na **Gerenciador de soluções** e clique em **Add** > **novo item** > **Visual C# itens**  >  **Extensibilidade** > **pacote do Visual Studio**. Nomeie esse arquivo *TestAsyncPackage.cs*.  
  
3.  Na *TestAsyncPackage.cs*, alterar o pacote do qual herdar `AsyncPackage` em vez de `Package`:  
  
    ```csharp  
    public sealed class TestAsyncPackage : AsyncPackage  
    ```  
  
4.  Para implementar um serviço, você precisa criar três tipos:  
  
    -   Uma interface que identifica o serviço. Muitas dessas interfaces estão vazias, ou seja, eles têm nenhum método que elas sejam usadas apenas para consultar o serviço.
  
    -   Uma interface que descreve a interface de serviço. Essa interface inclui os métodos a serem implementados.  
  
    -   Uma classe que implementa o serviço e a interface de serviço.  
  
5.  O exemplo a seguir mostra uma implementação muito básica dos três tipos. O construtor da classe de serviço deve definir o provedor de serviços. Neste exemplo vamos apenas adicionar o serviço para o arquivo de código do pacote.  
  
6.  Adicione as seguintes instruções using ao arquivo de pacote:  
  
    ```csharp  
    using System.Threading;  
    using System.Threading.Tasks;  
    using System.Runtime.CompilerServices;  
    using System.IO;
    using Microsoft.VisualStudio.Threading;
    using IAsyncServiceProvider = Microsoft.VisualStudio.Shell.IAsyncServiceProvider;
    using Task = System.Threading.Tasks.Task;
    ```  
  
7.  Aqui está a implementação de serviço assíncrona. Observe que você precisa definir o provedor de serviço assíncrono em vez do provedor de serviço síncronas no construtor:  
  
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

            await this.JoinableTaskFactory.SwitchToMainThreadAsync(cancellationToken);               
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
 Para registrar um serviço, adicione o <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute> ao pacote que fornece o serviço. Diferentes para registrar um serviço síncrono, você precisa certificar-se de pacote e de serviço dá suporte a async ao carregar:
  
- Você deve adicionar o **AllowsBackgroundLoading = true** campo para o <xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute> para garantir que o pacote pode ser inicializado de forma assíncrona para obter mais informações sobre o PackageRegistrationAttribute, consulte [registrar e Cancelar o registro de VSPackages](../extensibility/registering-and-unregistering-vspackages.md).  
  
- Você deve adicionar o **IsAsyncQueryable = true** campo para o <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute> para garantir que a instância de serviço pode ser inicializada de forma assíncrona.

  Aqui está um exemplo de um `AsyncPackage` com um registro de serviço assíncrona:
  
```csharp  
[ProvideService((typeof(STextWriterService)), IsAsyncQueryable = true)]  
[ProvideAutoLoad(UIContextGuids80.SolutionExists, PackageAutoLoadFlags.BackgroundLoad)]  
[PackageRegistration(UseManagedResourcesOnly = true, AllowsBackgroundLoading = true)]   
[Guid(TestAsyncPackage.PackageGuidString)]  
public sealed class TestAsyncPackage : AsyncPackage  
{. . . }  
```  
  
## <a name="add-a-service"></a>Adicionar um serviço  
  
1.  Na *TestAsyncPackage.cs*, remova o `Initialize()` método e substituição de `InitializeAsync()` método. Adicionar o serviço e adicione um método de retorno de chamada para criar os serviços. Aqui está um exemplo do inicializador assíncrono adicionando um serviço:  
  
    ```csharp
    protected override async Task InitializeAsync(CancellationToken cancellationToken, IProgress<ServiceProgressData> progress)  
    {  
        await base.InitializeAsync(cancellationToken, progress);  
        this.AddService(typeof(STextWriterService), CreateTextWriterService);
    }  
  
    ```  
  
2.  Adicione uma referência ao *Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll*.  
  
3.  Implemente o método de retorno de chamada como um método assíncrono que cria e retorna o serviço.  
  
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
  
1.  Vamos mostrar isso no inicializador, mas você pode obter o serviço em qualquer lugar que deseja usar o serviço.  
  
    ```csharp  
    protected override async System.Threading.Tasks.Task InitializeAsync(CancellationToken cancellationToken, IProgress<ServiceProgressData> progress)  
    {  
        await base.InitializeAsync(cancellationToken, progress);  
        this.AddService(typeof(STextWriterService), CreateTextWriterService);  
  
        ITextWriterService textService = await this.GetServiceAsync(typeof(STextWriterService)) as ITextWriterService;  
  
        await textService.WriteLineAsync(<userpath>), "this is a test");  
    }  
  
    ```  
  
     Não se esqueça de alterar  *\<userpath >* para um nome de arquivo e caminho que faça sentido em seu computador!  
  
2.  Compile e execute o código. Quando for exibida a instância experimental do Visual Studio, abra uma solução. Isso faz com que o `AsyncPackage` para autoload. Quando o inicializador de execução, você deve encontrar um arquivo no local especificado por você.  
  
## <a name="use-an-asynchronous-service-in-a-command-handler"></a>Usar um serviço assíncrono em um manipulador de comando  
 Aqui está um exemplo de como usar um serviço assíncrono em um comando de menu. Você pode usar o procedimento mostrado aqui para usar o serviço em outros métodos não assíncronas.  
  
1.  Adicione um comando de menu ao seu projeto. (Na **Gerenciador de soluções**, selecione o nó do projeto, clique com botão direito e selecione **Add** > **Novo Item**  >   **Extensibilidade** > **comando personalizado**.) Nomeie o arquivo de comando *TestAsyncCommand.cs*.  
  
2.  O modelo de comando personalizado adiciona novamente as `Initialize()` método para o *TestAsyncPackage.cs* arquivo a fim de inicializar o comando. No `Initialize()` método, copie a linha que inicializa o comando. Ele deve ter esta aparência:  
  
    ```csharp
    TestAsyncCommand.Initialize(this);  
    ```  
  
     Mover esta linha para o `InitializeAsync()` método na *AsyncPackageForService.cs* arquivo. Uma vez que isso está em uma inicialização assíncrona, você deve alternar para o thread principal antes de você inicializa o comando usando <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.SwitchToMainThreadAsync%2A>. Agora, ele deve ser assim:  
  
    ```csharp  
  
    protected override async System.Threading.Tasks.Task InitializeAsync(CancellationToken cancellationToken, IProgress<ServiceProgressData> progress)  
    {  
        await base.InitializeAsync(cancellationToken, progress);  
        this.AddService(typeof(STextWriterService), CreateTextWriterService);  

        ITextWriterService textService =   
           await this.GetServiceAsync(typeof(STextWriterService)) as ITextWriterService;  
  
        await textService.WriteLineAsync((<userpath>, "this is a test");  
  
        await this.JoinableTaskFactory.SwitchToMainThreadAsync(cancellationToken);  
        TestAsyncCommand.Initialize(this);
    }  
  
    ```  
  
3.  Excluir o `Initialize()` método.  
  
4.  No *TestAsyncCommand.cs* do arquivo, localize o `MenuItemCallback()` método. Exclua o corpo do método.  
  
5.  Adicionar uma instrução using:  
  
    ```csharp 
    using System.IO;  
    ```  
  
6.  Adicionar um método assíncrono chamado `UseTextWriterAsync()`, que obtém o serviço e usa seus métodos:  
  
    ```csharp  
    private async System.Threading.Tasks.Task UseTextWriterAsync()  
    {  
        // Query text writer service asynchronously to avoid a blocking call.
        ITextWriterService textService =   
           await AsyncServiceProvider.GlobalProvider.GetServiceAsync(typeof(STextWriterService))  
              as ITextWriterService;  

        // don't forget to change <userpath> to a local path  
        await textService.WriteLineAsync((<userpath>),"this is a test");  
       }  
  
    ```  
  
7.  Chamar esse método a partir de `MenuItemCallback()` método:  
  
    ```csharp
    private void MenuItemCallback(object sender, EventArgs e)  
    {  
        UseTextWriterAsync();  
    }  
  
    ```  
  
8.  Compile a solução e inicie a depuração. Quando for exibida a instância experimental do Visual Studio, vá para o **ferramentas** menu e procure o **TestAsyncCommand invocar** item de menu. Quando você clica nele, o TextWriterService grava o arquivo especificado. (Você não precisa abrir uma solução, porque também invoca o comando faz com que o pacote a ser carregado.)  
  
## <a name="see-also"></a>Consulte também  
 [Use e forneça serviços](../extensibility/using-and-providing-services.md)
