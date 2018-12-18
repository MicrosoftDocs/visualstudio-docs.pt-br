---
title: 'Como: fornecer um serviço assíncrono do Visual Studio | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0448274c-d3d2-4e12-9d11-8aca78a1f3f5
caps.latest.revision: 11
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 4833fcef561bcc7c81a8c19fd5c4a1fcb2f7ccea
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51767628"
---
# <a name="how-to-provide-an-asynchronous-visual-studio-service"></a>Como: fornecer um serviço assíncrono do Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Se você quiser obter um serviço sem bloquear o thread de interface do usuário, você deve criar um serviço assíncrono e carregar o pacote em um thread em segundo plano. Para essa finalidade, você pode usar um <xref:Microsoft.VisualStudio.Shell.AsyncPackage> em vez de um <xref:Microsoft.VisualStudio.Shell.Package>e adicione o serviço com os métodos assíncronos especial do pacote assíncrono  
  
 Para obter informações sobre o fornecimento de serviços síncronos do Visual Studio, consulte [como: fornecer um serviço](../extensibility/how-to-provide-a-service.md).  
  
## <a name="implementing-an-asynchronous-service"></a>Implementando um serviço assíncrono  
  
1.  Crie um projeto VSIX (**arquivo / novo / projeto / Visual c# / extensibilidade / VSIX Project**). Nomeie o projeto **TestAsync**.  
  
2.  Adicione um VSPackage ao projeto. Selecione o nó do projeto na **Gerenciador de soluções** e clique em **Add / novo item / itens do Visual c# / extensibilidade / pacote do Visual Studio**. Nomeie esse arquivo **TestAsyncPackage.cs**.  
  
3.  No TestAsyncPackage.cs, altere o pacote para herdar de AsyncPackage em vez de pacote:  
  
    ```csharp  
    public sealed class TestAsyncPackage : AsyncPackage  
    ```  
  
4.  Para implementar um serviço, você precisa criar três tipos:  
  
    -   Uma interface que descreve o serviço. Muitas dessas interfaces estão vazias, ou seja, eles têm sem métodos.  
  
    -   Uma interface que descreve a interface de serviço. Essa interface inclui os métodos a serem implementados.  
  
    -   Uma classe que implementa o serviço e a interface de serviço.  
  
5.  O exemplo a seguir mostra uma implementação muito básica dos três tipos. O construtor da classe de serviço deve definir o provedor de serviços. Neste exemplo vamos apenas adicionar o serviço para o arquivo de código do pacote.  
  
6.  Adicione as seguintes instruções using ao arquivo de pacote:  
  
    ```csharp  
    using System.Threading;  
    using System.Threading.Tasks;  
    using System.Runtime.CompilerServices;  
    using System.IO;  
    ```  
  
7.  Aqui está a implementação de serviço assíncrona. Observe que você precisa definir o provedor de serviço assíncrono em vez do provedor de serviço síncronas no construtor:  
  
    ```  
    public class TextWriterService : STextWriterService, ITextWriterService  
    {  
        private Microsoft.VisualStudio.Shell.IAsyncServiceProvider serviceProvider;  
        public TextWriterService(Microsoft.VisualStudio.Shell.IAsyncServiceProvider provider)  
        {  
            serviceProvider = provider;  
        }  
        public async System.Threading.Tasks.Task WriteLineAsync(string path, string line)  
        {  
            StreamWriter writer = new StreamWriter(path);  
            await writer.WriteLineAsync(line);  
            writer.Close();  
        }  
        public TaskAwaiter GetAwaiter()  
        {  
            return new TaskAwaiter();  
        }  
    }  
    public interface STextWriterService  
    {  
    }  
    public interface ITextWriterService   
    {  
        System.Threading.Tasks.Task WriteLineAsync(string path, string line);  
        TaskAwaiter GetAwaiter();  
    }  
    ```  
  
## <a name="registering-a-service"></a>Registrar um serviço  
 Para registrar um serviço, adicione o <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute> ao pacote que fornece o serviço. Há duas diferenças ao registrar um serviço síncrono:  
  
- Se você realiza o carregamento automático de pacote, você deve adicionar o <xref:Microsoft.VisualStudio.Shell.PackageAutoLoadFlags> valor BackgroundLoad ao atributo. Para obter mais informações sobre os VSPackages realiza o carregamento automático, consulte [carregar VSPackages](../extensibility/loading-vspackages.md).  
  
- Você deve adicionar o **AllowsBackgroundLoading = true** campo para o <xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute>. Para obter mais informações sobre o PackageRegistrationAttribute, consulte [Registrando e Cancelando o registro de VSPackages](../extensibility/registering-and-unregistering-vspackages.md).  
  
  Aqui está um exemplo de um AsyncPackage com um registro de serviço assíncrono::  
  
```csharp  
[ProvideService((typeof(STextWriterService)), IsAsyncQueryable = true)]  
[ProvideAutoLoad(UIContextGuids80.SolutionExists, PackageAutoLoadFlags.BackgroundLoad)]  
[PackageRegistration(UseManagedResourcesOnly = true, AllowsBackgroundLoading = true)]   
[Guid(TestAsyncPackage.PackageGuidString)]  
public sealed class TestAsyncPackage : AsyncPackage  
{. . . }  
```  
  
## <a name="adding-a-service"></a>Adição de um serviço  
  
1.  No TestAsyncPackage.cs, remova os `Initialize()` método e substituição de `InitializeAsync()` método. Adicionar o serviço e adicione um método de retorno de chamada para criar os serviços. Aqui está um exemplo do inicializador assíncrono adicionando um serviço:  
  
    ```  
    protected override async System.Threading.Tasks.Task InitializeAsync(CancellationToken cancellationToken, IProgress<ServiceProgressData> progress)  
    {  
        this.AddService(typeof(STextWriterService), CreateService);  
  
        await base.InitializeAsync(cancellationToken, progress);  
    }  
  
    ```  
  
2.  Adicione uma referência ao Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll.  
  
3.  Implemente o método de retorno de chamada como um método assíncrono que cria e retorna o serviço.  
  
    ```csharp  
    public async System.Threading.Tasks.Task<object> CreateService(IAsyncServiceContainer container, CancellationToken cancellationToken, Type serviceType)  
    {  
        STextWriterService service = null;  
        await System.Threading.Tasks.Task.Run(() => {  
                    service = new TextWriterService(this);  
             });  
  
        return service;  
    }  
  
    ```  
  
## <a name="using-a-service"></a>Usando um serviço  
 Agora você pode obter o serviço e usar seus métodos.  
  
1.  Vamos mostrar isso no inicializador, mas você pode obter o serviço em qualquer lugar que deseja usar o serviço.  
  
    ```csharp  
    protected override async System.Threading.Tasks.Task InitializeAsync(CancellationToken cancellationToken, IProgress<ServiceProgressData> progress)  
    {  
        this.AddService(typeof(STextWriterService), CreateService);  
  
        ITextWriterService textService = await this.GetServiceAsync(typeof(STextWriterService)) as ITextWriterService;  
  
        await writer.WriteLineAsync(<userpath>), "this is a test");  
  
        await base.InitializeAsync(cancellationToken, progress);  
    }  
  
    ```  
  
     Não se esqueça de alterar  *\<userpath >* para um nome de arquivo e caminho que faça sentido em seu computador!  
  
2.  Compile e execute o código. Quando for exibida a instância experimental do Visual Studio, abra uma solução. Isso faz com que o AsyncPackage para autoload. Quando o inicializador de execução, você deve encontrar um arquivo no local especificado por você.  
  
## <a name="using-an-asynchronous-service-in-a-command-handler"></a>Usando um serviço assíncrono em um manipulador de comandos  
 Aqui está um exemplo de como usar um serviço assíncrono em um comando de menu. Você pode usar o procedimento mostrado aqui para usar o serviço em outros métodos não assíncronas.  
  
1.  Adicione um comando de menu ao seu projeto. (Na **Gerenciador de soluções**, selecione o nó do projeto, clique com botão direito e selecione **Add / Novo Item / extensibilidade personalizada de comando /**.) Nomeie o arquivo de comando **TestAsyncCommand.cs.**  
  
2.  O modelo de comando personalizado adiciona novamente o `Initialize()` método ao arquivo TestAsyncPackage.cs para inicializar o comando. No método Initialize (), copie a linha que inicializa o comando. Ele deve ter esta aparência:  
  
    ```  
    TestAsyncCommand.Initialize(this);  
    ```  
  
     Mover esta linha para o `InitializeAsync()` método no arquivo AsyncPackageForService.cs. Uma vez que isso está em uma inicialização assíncrona, você deve alternar para o thread principal antes de você inicializa o comando usando <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.SwitchToMainThreadAsync%2A>. Agora, ele deve ser assim:  
  
    ```csharp  
  
    protected override async System.Threading.Tasks.Task InitializeAsync(CancellationToken cancellationToken, IProgress<ServiceProgressData> progress)  
    {  
        await ThreadHelper.JoinableTaskFactory.SwitchToMainThreadAsync();  
        TestAsyncCommand.Initialize(this);    
  
        this.AddService(typeof(STextWriterService), CreateService);  
  
        ITextWriterService textService =   
           await this.GetServiceAsync(typeof(STextWriterService)) as ITextWriterService;  
  
        await writer.WriteLineAsync((<userpath>, "this is a test");  
  
        await base.InitializeAsync(cancellationToken, progress);  
    }  
  
    ```  
  
3.  Excluir o `Initialize()` método.  
  
4.  No arquivo TestAsyncCommand.cs, localize o `MenuItemCallback()` método. Exclua o corpo do método.  
  
5.  Adicionar uma instrução using:  
  
    ```  
    using System.IO;  
    ```  
  
6.  Adicionar um método assíncrono chamado `GetAsyncService()`, que obtém o serviço e usa seus métodos:  
  
    ```csharp  
    private async System.Threading.Tasks.Task GetAsyncService()  
    {  
        ITextWriterService textService =   
           this.ServiceProvider.GetService(typeof(STextWriterService))  
              as ITextWriterService;  
        // don’t forget to change <userpath> to a local path  
        await writer.WriteLineAsync((<userpath>),"this is a test");  
       }  
  
    ```  
  
7.  Chamar esse método a partir de `MenuItemCallback()` método:  
  
    ```  
    private void MenuItemCallback(object sender, EventArgs e)  
    {  
        GetAsyncService();  
    }  
  
    ```  
  
8.  Compile a solução e inicie a depuração. Quando for exibida a instância experimental do Visual Studio, vá para o **ferramentas** menu e procure o **TestAsyncCommand invocar** item de menu. Quando você clica nele, o TextWriterService grava o arquivo especificado. (Você não precisa abrir uma solução, porque também invoca o comando faz com que o pacote a ser carregado.)  
  
## <a name="see-also"></a>Consulte também  
 [Usar e fornecer serviços](../extensibility/using-and-providing-services.md)

