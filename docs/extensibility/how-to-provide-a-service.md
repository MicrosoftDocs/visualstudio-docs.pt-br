---
title: 'Como: fornecer um serviço | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- services, providing
ms.assetid: 12bc1f12-47b1-44f6-b8db-862aa88d50d1
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 2408eace3ecea447c9b49ff17c729e3f4661b5d6
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49942539"
---
# <a name="how-to-provide-a-service"></a>Como: fornecer um serviço
Um VSPackage pode fornecer serviços que outros VSPackages pode usar. Para fornecer um serviço, um VSPackage deve registrar o serviço com o Visual Studio e adicione o serviço.  
  
 O <xref:Microsoft.VisualStudio.Shell.Package> classe implementa ambos <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> e <xref:System.ComponentModel.Design.IServiceContainer>. <xref:System.ComponentModel.Design.IServiceContainer> contém métodos de retorno de chamada que fornecem serviços sob demanda.  
  
 Para obter mais informações sobre serviços, consulte [essentials do serviço](../extensibility/internals/service-essentials.md) .  
  
> [!NOTE]
>  Quando um VSPackage está prestes a ser descarregado, o Visual Studio aguarda até que todas as solicitações para serviços que fornece um VSPackage foram entregues. Ele não permite novas solicitações para esses serviços. Você não deve chamar explicitamente o <xref:Microsoft.VisualStudio.Shell.Interop.IProfferService.RevokeService%2A> método revogar um serviço quando o descarregamento.  
  
## <a name="implement-a-service"></a>Implementar um serviço  
  
1. Crie um projeto VSIX (**arquivo** > **New** > **projeto** > **Visual C#**  >  **Extensibilidade** > **projeto VSIX**).  
  
2. Adicione um VSPackage ao projeto. Selecione o nó do projeto na **Gerenciador de soluções** e clique em **Add** > **novo item** > **Visual C# itens**  >  **Extensibilidade** > **pacote do Visual Studio**.  
  
3. Para implementar um serviço, você precisa criar três tipos:  
  
   - Uma interface que descreve o serviço. Muitas dessas interfaces estão vazias, ou seja, eles têm sem métodos.  
  
   - Uma interface que descreve a interface de serviço. Essa interface inclui os métodos a serem implementados.  
  
   - Uma classe que implementa o serviço e a interface de serviço.  
  
     O exemplo a seguir mostra uma implementação básica dos três tipos. O construtor da classe de serviço deve definir o provedor de serviços.  
  
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
  
### <a name="register-a-service"></a>Registrar um serviço  
  
1.  Para registrar um serviço, adicione o <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute> o VSPackage que fornece o serviço. Veja um exemplo:  
  
    ```csharp  
    [ProvideService(typeof(SMyService))]  
    [PackageRegistration(UseManagedResourcesOnly = true)]  
    [Guid(VSPackage1.PackageGuidString)]  
    public sealed class VSPackage1 : Package  
    {. . . }  
    ```  
  
     Este atributo registra `SMyService` com o Visual Studio.  
  
    > [!NOTE]
    >  Para registrar um serviço que substitui outro serviço com o mesmo nome, use o <xref:Microsoft.VisualStudio.Shell.ProvideServiceOverrideAttribute>. Observe que a substituição de um serviço somente uma é permitida.  
  
### <a name="add-a-service"></a>Adicionar um serviço  
  
1.  No inicializador de VSPackage, adicione o serviço e adicione um método de retorno de chamada para criar os serviços. Aqui está a alteração a fazer o <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> método:  
  
    ```csharp  
    protected override void Initialize()  
    {  
        ServiceCreatorCallback callback =new ServiceCreatorCallback(CreateService);  
  
        ((IServiceContainer)this).AddService(typeof(SMyService), callback);  
    . . .  
    }  
    ```  
  
2.  Implemente o método de retorno de chamada, que deve criar e retornar o serviço ou nulo se ela não pode ser criada.  
  
    ```csharp  
    private object CreateService(IServiceContainer container, Type serviceType)  
    {  
        if (typeof(SMyService) == serviceType)  
            return new MyService(this);  
        return null;  
    }  
    ```  
  
    > [!NOTE]
    >  Visual Studio pode rejeitar uma solicitação para fornecer um serviço. Ele faz isso, se outro VSPackage já fornece o serviço.  
  
3.  Agora você pode obter o serviço e usar seus métodos. O exemplo a seguir mostra o uso do serviço no inicializador, mas você pode obter o serviço em qualquer lugar que deseja usar o serviço.  
  
    ```csharp  
    protected override void Initialize()  
    {  
        ServiceCreatorCallback callback =new ServiceCreatorCallback(CreateService);  
  
        ((IServiceContainer)this).AddService(typeof(SMyService), callback);  
  
        MyService myService = (MyService) this.GetService(typeof(SMyService));  
        myService.Hello();  
        string helloString = myService.Goodbye();  
  
        base.Initialize();  
    }  
    ```  
  
     O valor de `helloString` deve ser "Hello".  
  
## <a name="see-also"></a>Consulte também  
 [Como: obter um serviço](../extensibility/how-to-get-a-service.md)   
 [Use e forneça serviços](../extensibility/using-and-providing-services.md)   
 [Fundamentos do serviço](../extensibility/internals/service-essentials.md)
