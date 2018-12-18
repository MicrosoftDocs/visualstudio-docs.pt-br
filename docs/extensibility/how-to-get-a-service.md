---
title: 'Como: obter um serviço | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- services, consuming
ms.assetid: 1f000020-8fb7-4e39-8e1e-2e38c7fec3d4
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: b7b28f018ba92ad2ab8a266311ac2e71fd910440
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49951373"
---
# <a name="how-to-get-a-service"></a>Como: obter um serviço
Muitas vezes você precisa obter os serviços do Visual Studio para acessar recursos diferentes. Em geral, um serviço do Visual Studio fornece uma ou mais interfaces que você pode usar. Você pode obter a maioria dos serviços de um VSPackage.  
  
 Qualquer VSPackage que deriva de <xref:Microsoft.VisualStudio.Shell.Package> e que localizado corretamente pode pedir para qualquer serviço global. Porque o `Package` classe implementa <xref:System.IServiceProvider>, qualquer VSPackage que deriva de `Package` também é um provedor de serviços.  
  
 Quando o Visual Studio carrega uma <xref:Microsoft.VisualStudio.Shell.Package>, ele passa um <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> do objeto para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A> método durante a inicialização. Isso é chamado *localização* VSPackage. O `Package` classe encapsula esse provedor de serviços e fornece o <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> método para obter serviços.  
  
## <a name="getting-a-service-from-an-initialized-vspackage"></a>Obtendo um serviço de um VSPackage inicializado  
  
1. Cada extensão do Visual Studio inicia com um projeto de implantação do VSIX que conterá os ativos de extensão. Criar uma [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] projeto do VSIX chamado `GetServiceExtension`. Você pode encontrar o modelo de projeto VSIX na **novo projeto** diálogo sob **Visual c#** > **extensibilidade**.  
  
2. Agora, adicione um modelo de item de comando personalizado chamado **GetServiceCommand**. No **Adicionar Novo Item** caixa de diálogo, vá para **Visual c#** > **extensibilidade** e selecione **comando personalizado**. No **nome** campo na parte inferior da janela, altere o nome do arquivo de comando para *GetServiceCommand.cs*. Para obter mais informações sobre como criar um comando personalizado, [criar uma extensão com um comando de menu](../extensibility/creating-an-extension-with-a-menu-command.md)  
  
3. Na *GetServiceCommand.cs*, remova o corpo de `MenuItemCommand` método e adicione o seguinte código:  
  
   ```csharp  
   IVsActivityLog activityLog = ServiceProvider.GetService(typeof(SVsActivityLog)) as IVsActivityLog;  
   if (activityLog == null) return;  
   System.Windows.Forms.MessageBox.Show("Found the activity log service.");  
  
   ```  
  
    Esse código obtém um serviço SVsActivityLog e converte-o para um <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog> interface, que pode ser usado para gravar no log de atividade. Por exemplo, consulte [como: usar o log de atividades](../extensibility/how-to-use-the-activity-log.md).  
  
4. Compile o projeto e comece a depuração. A instância experimental é exibida.  
  
5. No **ferramentas** menu da instância experimental, localizar o **GetServiceCommand invocar** botão. Quando você clica nesse botão, você deve ver uma caixa de mensagem que diz **encontrar o serviço de log de atividade.**  
  
## <a name="getting-a-service-from-a-tool-window-or-control-container"></a>Obtendo um serviço de um contêiner de controle ou janela de ferramenta  
 Às vezes, você precisará obter um serviço de uma janela de ferramenta ou controle de contêiner que não tenha sido colocado no local, caso contrário, foi colocado no local com um provedor de serviço que não sabe sobre o serviço que você deseja. Por exemplo, você talvez queira gravar no log de atividade de dentro de um controle.  
  
 Estático <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> método se baseia em um provedor de serviços em cache que é inicializado na primeira vez que qualquer VSPackage derivado de <xref:Microsoft.VisualStudio.Shell.Package> é colocado no local.  
  
 Como o construtor de VSPackage é chamado antes do VSPackage é colocado no local, serviços globais são normalmente indisponíveis a partir do construtor de VSPackage. Ver [como: solucionar problemas de serviços](../extensibility/how-to-troubleshoot-services.md) para uma solução alternativa.  
  
 Aqui está um exemplo da forma de obter um serviço em uma janela de ferramenta ou outro elemento não VSPackage.  
  
```csharp  
IVsActivityLog log = Package.GetGlobalService(typeof(SVsActivityLog)) as IVsActivityLog;  
if (log == null) return;  
```  
  
## <a name="getting-a-service-from-the-dte-object"></a>Introdução a um serviço do objeto DTE  
 Você também pode obter serviços de <xref:EnvDTE.DTEClass> objeto. No entanto, você deve obter o objeto DTE como um serviço de um VSPackage ou chamando estático <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> método.  
  
 Implementa o objeto DTE <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>, que pode ser usado para consultar um serviço usando <xref:Microsoft.VisualStudio.Shell.ServiceProvider.GetService%2A>.  
  
 Eis como obter um serviço do objeto DTE.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Como: fornecer um serviço](../extensibility/how-to-provide-a-service.md)   
 [Use e forneça serviços](../extensibility/using-and-providing-services.md)   
 [Fundamentos do serviço](../extensibility/internals/service-essentials.md)