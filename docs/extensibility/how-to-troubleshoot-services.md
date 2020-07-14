---
title: 'Como: solucionar problemas de serviços | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: troubleshooting
helpviewer_keywords:
- services, troubleshooting
ms.assetid: 001551da-4847-4f59-a0b2-fcd327d7f5ca
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 588396f3f152222c4e79b03a1d733524a8ff3ca9
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905725"
---
# <a name="how-to-troubleshoot-services"></a>Como: solucionar problemas de serviços
Há vários problemas comuns que podem ocorrer quando você tenta obter um serviço:

- O serviço não está registrado no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] .

- O serviço é solicitado pelo tipo de interface e não pelo tipo de serviço.

- O VSPackage que solicita o serviço não foi local.

- O provedor de serviços errado é usado.

  Se o serviço solicitado não puder ser obtido, a chamada para <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> retornará NULL. Você sempre deve testar o valor nulo após solicitar um serviço:

```csharp
IVsActivityLog log =
    GetService(typeof(SVsActivityLog)) as IVsActivityLog;
if (log == null) return;
```

## <a name="to-troubleshoot-a-service"></a>Para solucionar problemas de um serviço

1. Examine o registro do sistema para ver se o serviço foi registrado corretamente. Para obter mais informações, consulte [como: fornecer um serviço](../extensibility/how-to-provide-a-service.md).

    O fragmento de arquivo *. reg* a seguir mostra como o serviço SVsTextManager pode ser registrado:

   ```
   [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\<version number>\Services\{F5E7E71D-1401-11d1-883B-0000F87579D2}]
   @="{F5E7E720-1401-11d1-883B-0000F87579D2}"
   "Name"="SVsTextManager"
   ```

    No exemplo acima, o número de versão é a versão do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] , como 12,0 ou 14,0, a chave {F5E7E71D-1401-11D1-883B-0000F87579D2} é o identificador de serviço (SID) do serviço, SVsTextManager e o valor padrão {F5E7E720-1401-11D1-883B-0000F87579D2} é o GUID do pacote do VSPackage do Gerenciador de texto, que fornece o serviço.

2. Use o tipo de serviço e não o tipo de interface ao chamar GetService. Ao solicitar um serviço do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] , <xref:Microsoft.VisualStudio.Shell.Package> o extrai o GUID do tipo. Um serviço não será encontrado se as seguintes condições existirem:

   1. Um tipo de interface é passado para GetService em vez do tipo de serviço.

   2. Nenhum GUID é explicitamente atribuído à interface. Portanto, o sistema cria um GUID padrão para um objeto, conforme necessário.

3. Certifique-se de que a VSPackage solicitando o serviço tenha sido site. [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]os sites VSPackage depois de construí-lo e antes de chamar <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> .

    Se você tiver um código em um Construtor VSPackage que precisa de um serviço, mova-o para o `Initialize` método.

4. Certifique-se de que você está usando o provedor de serviços correto.

    Nem todos os provedores de serviço são semelhantes. O provedor de serviços que [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] passa para uma janela de ferramentas difere do que ele passa para um VSPackage. O provedor de serviços da janela de ferramentas sabe <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> , mas não conhece <xref:Microsoft.VisualStudio.Shell.Interop.SVsRunningDocumentTable> . Você pode chamar <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> para obter um provedor de serviços VSPackage de dentro de uma janela de ferramentas.

    Se uma janela de ferramenta hospedar um controle de usuário ou qualquer outro contêiner de controle, o contêiner será site pelo modelo de componente do Windows e não terá acesso a nenhum [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] serviço. Você pode chamar <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> para obter um provedor de serviços VSPackage de dentro de um contêiner de controle.

## <a name="see-also"></a>Confira também
- [Lista de serviços disponíveis](../extensibility/internals/list-of-available-services.md)
- [Usar e fornecer serviços](../extensibility/using-and-providing-services.md)
- [Noções básicas do serviço](../extensibility/internals/service-essentials.md)
