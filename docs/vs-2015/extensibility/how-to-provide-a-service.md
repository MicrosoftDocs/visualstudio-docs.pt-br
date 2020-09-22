---
title: 'Como: fornecer um serviço | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- services, providing
ms.assetid: 12bc1f12-47b1-44f6-b8db-862aa88d50d1
caps.latest.revision: 23
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 565a8a91797c826b6419dc5a8488d7d3baf9cddc
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "90838450"
---
# <a name="how-to-provide-a-service"></a>Como fornecer um serviço
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Um VSPackage pode fornecer serviços que outros VSPackages podem usar. Para fornecer um serviço, um VSPackage deve registrar o serviço com o Visual Studio e adicionar o serviço.  
  
 A <xref:Microsoft.VisualStudio.Shell.Package> classe implementa <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> e <xref:System.ComponentModel.Design.IServiceContainer> . <xref:System.ComponentModel.Design.IServiceContainer> contém métodos de retorno de chamada que fornecem serviços sob demanda.  
  
 Para obter mais informações sobre serviços, consulte [Service Essentials](../extensibility/internals/service-essentials.md) .  
  
> [!NOTE]
> Quando um VSPackage está prestes a ser descarregado, o Visual Studio aguarda até que todas as solicitações de serviços que um VSPackage fornece tenham sido entregues. Ele não permite novas solicitações para esses serviços. Você não deve chamar explicitamente o <xref:Microsoft.VisualStudio.Shell.Interop.IProfferService.RevokeService%2A> método para revogar um serviço ao descarregar.  
  
#### <a name="implementing-a-service"></a>Implementando um serviço  
  
1. Crie um projeto VSIX (**arquivo/novo/projeto/Visual C#/extensiblity/projeto VSIX**).  
  
2. Adicione um VSPackage ao projeto. Selecione o nó do projeto na **Gerenciador de soluções** e clique em **Adicionar/novo item/Visual C# itens/extensibilidade/pacote do Visual Studio**.  
  
3. Para implementar um serviço, você precisa criar três tipos:  
  
   - Uma interface que descreve o serviço. Muitas dessas interfaces estão vazias, ou seja, não têm métodos.  
  
   - Uma interface que descreve a interface do serviço. Essa interface inclui os métodos a serem implementados.  
  
   - Uma classe que implementa o serviço e a interface de serviço.  
  
     O exemplo a seguir mostra uma implementação muito básica dos três tipos. O construtor da classe de serviço deve definir o provedor de serviços.  
  
   ```csharp  
   public class MyService : SMyService, IMyService  
   {  
       private Microsoft.VisualStudio.OLE.Interop.IServiceProvider serviceProvider;  
       private string myString;  
       public MyService(Microsoft.VisualStudio.OLE.Interop.IServiceProvider sp)  
       {  
           Trace.WriteLine(  
                  "Constructing a new instance of MyService");  
           serviceProvider = sp;  
       }  
       public void Hello()  
       {  
           myString = "hello";  
       }  
       public string Goodbye()  
       {  
          return "goodbye";  
       }  
   }  
   public interface SMyService  
   {  
   }  
   public interface IMyService  
   {  
       void Hello();  
       string Goodbye();  
   }  
  
   ```  
  
### <a name="registering-a-service"></a>Registrando um serviço  
  
1. Para registrar um serviço, adicione o <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute> ao VSPackage que fornece o serviço. Veja um exemplo:  
  
    ```csharp  
    [ProvideService(typeof(SMyService))]  
    [PackageRegistration(UseManagedResourcesOnly = true)]  
    [Guid(VSPackage1.PackageGuidString)]  
    public sealed class VSPackage1 : Package  
    {. . . }  
    ```  
  
     Esse atributo é registrado `SMyService` com o Visual Studio.  
  
    > [!NOTE]
    > Para registrar um serviço que substitui outro serviço com o mesmo nome, use o <xref:Microsoft.VisualStudio.Shell.ProvideServiceOverrideAttribute> . Observe que apenas uma substituição de um serviço é permitida.  
  
### <a name="adding-a-service"></a>Adicionando um serviço  
  
1. 1.  No inicializador VSPackage, adicione o serviço e adicione um método de retorno de chamada para criar os serviços. Aqui está a alteração a ser feita no <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> método:  
  
    ```csharp  
    protected override void Initialize()  
    {  
        ServiceCreatorCallback callback =new ServiceCreatorCallback(CreateService);  
  
        ((IServiceContainer)this).AddService(typeof(SMyService), callback);  
    . . .  
    }  
    ```  
  
2. Implemente o método de retorno de chamada, que deve criar e retornar o serviço, ou NULL se não puder ser criado.  
  
    ```  
    private object CreateService(IServiceContainer container, Type serviceType)  
    {  
        if (typeof(SMyService) == serviceType)  
            return new SMyService(this);  
        return null;  
    }  
    ```  
  
    > [!NOTE]
    > O Visual Studio pode rejeitar uma solicitação para fornecer um serviço. Ele faz isso se outro VSPackage já fornecer o serviço.  
  
3. Agora você pode obter o serviço e usar seus métodos. Mostraremos isso no inicializador, mas você poderá obter o serviço em qualquer lugar em que desejar usar o serviço.  
  
    ```csharp  
    protected override void Initialize()  
    {  
        ServiceCreatorCallback callback =new ServiceCreatorCallback(CreateService);  
  
        ((IServiceContainer)this).AddService(typeof(SMyService), callback);  
  
        MyService myService = (MyService) this.GetService(typeof(SMyService));  
        myService.Hello();  
        string helloString = myService.myString;  
  
        base.Initialize();  
    }  
    ```  
  
     O valor de `helloString` deve ser "Olá".  
  
## <a name="see-also"></a>Consulte Também  
 [Como: obter um serviço](../extensibility/how-to-get-a-service.md)   
 [Usando e fornecendo serviços](../extensibility/using-and-providing-services.md)   
 [Conceitos básicos do serviço](../extensibility/internals/service-essentials.md)
