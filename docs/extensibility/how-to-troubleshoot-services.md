---
title: 'Como: solucionar problemas de serviços | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- services, troubleshooting
ms.assetid: 001551da-4847-4f59-a0b2-fcd327d7f5ca
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 3d2e1e59b5d2bd1210511b355676407a1368143f
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49834208"
---
# <a name="how-to-troubleshoot-services"></a>Como: solucionar problemas de serviços
Há vários problemas comuns que podem ocorrer ao tentar obter um serviço:  
  
- O serviço não está registrado com [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)].  
  
- O serviço for solicitado pelo tipo de interface e não pelo tipo de serviço.  
  
- O VSPackage solicitando o serviço não tem sido colocado no local.  
  
- O provedor de serviço errado é usado.  
  
  Se o serviço solicitado não pode ser obtida, a chamada para <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> retorna null. Você deve sempre testar Null após a solicitação em um serviço:  
  
```csharp  
IVsActivityLog log =   
    GetService(typeof(SVsActivityLog)) as IVsActivityLog;  
if (log == null) return;  
```  
  
## <a name="to-troubleshoot-a-service"></a>Para solucionar problemas de um serviço  
  
1. Examine o registro do sistema para ver se o serviço foi registrado corretamente. Para obter mais informações, consulte [como: fornecer um serviço](../extensibility/how-to-provide-a-service.md).  
  
    O seguinte *. reg* fragmento do arquivo mostra como o serviço SVsTextManager pode ser registrado:  
  
   ```  
   [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\<version number>\Services\{F5E7E71D-1401-11d1-883B-0000F87579D2}]  
   @="{F5E7E720-1401-11d1-883B-0000F87579D2}"  
   "Name"="SVsTextManager"  
   ```  
  
    No exemplo acima, o número de versão é a versão do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)], tais como 12.0 ou 14.0, a chave {F5E7E71D-1401-11d1-883B-0000F87579D2} é o identificador de serviço (SID) do serviço, SVsTextManager e a {de valor padrão F5E7E720-1401-11D1-883B-0000F87579D2} é o GUID do Gerenciador de texto VSPackage, que fornece o serviço do pacote.  
  
2. Use o tipo de serviço e não o tipo de interface ao chamar GetService. Ao solicitar um serviço do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)], <xref:Microsoft.VisualStudio.Shell.Package> extrai a GUID do tipo. Um serviço não será encontrado se existem as seguintes condições:  
  
   1.  Um tipo de interface é passado para GetService em vez do tipo de serviço.  
  
   2.  Nenhum GUID for explicitamente atribuído à interface. Portanto, o sistema cria um GUID padrão para um objeto, conforme necessário.  
  
3. Certifique-se de que o VSPackage solicitando o serviço foi colocado no local. [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] sites a um VSPackage após construí-la e antes de chamar <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A>.  
  
    Se você tiver código em um construtor de VSPackage que precisa de um serviço, mova-o para o `Initialize` método.  
  
4. Certifique-se de que você está usando o provedor de serviço correto.  
  
    Nem todos os provedores de serviço são iguais. O provedor de serviços que [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] passa para uma janela de ferramentas é diferente daquele que ele passa a um VSPackage. O provedor de serviços de janela da ferramenta conhece <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection>, mas não sabe sobre <xref:Microsoft.VisualStudio.Shell.Interop.SVsRunningDocumentTable>. Você pode chamar <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> para obter um provedor de serviços de VSPackage de dentro de uma janela de ferramenta.  
  
    Se uma janela de ferramentas hospeda um controle de usuário ou qualquer outro contêiner de controle, o contêiner será colocado no local pelo modelo de componente do Windows e não terá acesso a qualquer [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] serviços. Você pode chamar <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> para obter um provedor de serviços de VSPackage dentro de um contêiner de controle.  
  
## <a name="see-also"></a>Consulte também  
 [Lista de serviços disponíveis](../extensibility/internals/list-of-available-services.md)   
 [Use e forneça serviços](../extensibility/using-and-providing-services.md)   
 [Fundamentos do serviço](../extensibility/internals/service-essentials.md)