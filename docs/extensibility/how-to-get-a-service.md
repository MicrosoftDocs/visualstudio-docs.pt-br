---
title: 'Como: obter um serviço | Microsoft Docs'
ms.date: 3/16/2019
ms.topic: how-to
helpviewer_keywords:
- services, consuming
ms.assetid: 1f000020-8fb7-4e39-8e1e-2e38c7fec3d4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a401103112096a1089b59ba3733d19480f93e891
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905824"
---
# <a name="how-to-get-a-service"></a>Como: obter um serviço

Geralmente, você precisa obter os serviços do Visual Studio para acessar recursos diferentes. Em geral, um serviço do Visual Studio fornece uma ou mais interfaces que você pode usar. Você pode obter a maioria dos serviços de um VSPackage.

Qualquer VSPackage que deriva de <xref:Microsoft.VisualStudio.Shell.Package> e que tenha sido corretamente no local pode solicitar qualquer serviço global. Como a `Package` classe implementa <xref:System.IServiceProvider> , qualquer VSPackage que deriva de `Package` também é um provedor de serviços.

Quando o Visual Studio carrega um <xref:Microsoft.VisualStudio.Shell.Package> , ele passa um <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> objeto para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A> método durante a inicialização. Isso é chamado *localizando* VSPackage. A `Package` classe encapsula esse provedor de serviços e fornece o <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> método para obter serviços.

## <a name="getting-a-service-from-an-initialized-vspackage"></a>Obtendo um serviço de um VSPackage inicializado

1. Cada extensão do Visual Studio começa com um projeto de implantação VSIX, que conterá os ativos de extensão. Crie um [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] projeto VSIX denominado `GetServiceExtension` . Você pode encontrar o modelo de projeto VSIX na caixa de diálogo **novo projeto** pesquisando por "VSIX".

2. Agora, adicione um modelo de item de comando personalizado chamado **GetServiceCommand**. Na caixa de diálogo **Adicionar novo item** , vá para extensibilidade do **Visual C#**  >  **Extensibility** e selecione **comando personalizado**. No campo **nome** na parte inferior da janela, altere o nome do arquivo de comando para *GetServiceCommand.cs*. Para obter mais informações sobre como criar um comando personalizado, [crie uma extensão com um comando de menu](../extensibility/creating-an-extension-with-a-menu-command.md)

3. No *GetServiceCommand.cs*, remova o corpo do `MenuItemCommand` método e adicione o seguinte código:

   ```csharp
   IVsActivityLog activityLog = ServiceProvider.GetService(typeof(SVsActivityLog)) as IVsActivityLog;
   if (activityLog == null) return;
   System.Windows.Forms.MessageBox.Show("Found the activity log service.");

   ```

    Esse código obtém um serviço SVsActivityLog e o converte em uma <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog> interface, que pode ser usada para gravar no log de atividades. Para obter um exemplo, consulte [como: usar o log de atividades](../extensibility/how-to-use-the-activity-log.md).

4. Compile o projeto e comece a depuração. A instância experimental é exibida.

5. No menu **ferramentas** da instância experimental, localize o botão **invocar GetServiceCommand** . Ao clicar nesse botão, você deverá ver uma caixa de mensagem que diz **encontrar o serviço log de atividades.**

## <a name="getting-a-service-from-a-tool-window-or-control-container"></a>Obtendo um serviço de uma janela de ferramentas ou de um contêiner de controle

Às vezes, talvez seja necessário obter um serviço de uma janela de ferramentas ou de um contêiner de controle que não tenha sido site, ou que tenha sido site com um provedor de serviços que não saiba sobre o serviço desejado. Por exemplo, talvez você queira gravar no log de atividades de dentro de um controle.

O <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> método estático depende de um provedor de serviços em cache que é inicializado na primeira vez que qualquer VSPackage derivado de é colocado no <xref:Microsoft.VisualStudio.Shell.Package> site.

Como o Construtor VSPackage é chamado antes de o VSPackage ser site, os serviços globais normalmente não estão disponíveis no Construtor VSPackage. Consulte [como solucionar problemas de serviços](../extensibility/how-to-troubleshoot-services.md) para obter uma solução alternativa.

Aqui está um exemplo de como obter um serviço em uma janela de ferramentas ou outro elemento não VSPackage.

```csharp
IVsActivityLog log = Package.GetGlobalService(typeof(SVsActivityLog)) as IVsActivityLog;
if (log == null) return;
```

## <a name="getting-a-service-from-the-dte-object"></a>Obtendo um serviço do objeto DTE

Você também pode obter serviços do <xref:EnvDTE.DTEClass> objeto. No entanto, você deve obter o objeto DTE como um serviço de um VSPackage ou chamando o <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> método estático.

O objeto DTE implementa <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> , que você pode usar para consultar um serviço usando o <xref:Microsoft.VisualStudio.Shell.ServiceProvider.GetService%2A> .

Veja como obter um serviço do objeto DTE.

```csharp
// Start with the DTE object, for example: 
// using EnvDTE;
// DTE dte = (DTE)GetService(typeof(DTE));

ServiceProvider sp = new ServiceProvider((Microsoft.VisualStudio.OLE.Interop.IServiceProvider)dte);
if (sp != null)
{
    IVsActivityLog log = sp.GetService(typeof(SVsActivityLog)) as IVsActivityLog;
    if (log != null)
    {
        System.Windows.Forms.MessageBox.Show("Found the activity log service.");
    }
}
```

## <a name="see-also"></a>Confira também

- [Como: fornecer um serviço](../extensibility/how-to-provide-a-service.md)
- [Usar e fornecer serviços](../extensibility/using-and-providing-services.md)
- [Noções básicas do serviço](../extensibility/internals/service-essentials.md)
