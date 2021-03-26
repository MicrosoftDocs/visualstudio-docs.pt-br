---
title: Service Essentials | Microsoft Docs
description: Saiba mais sobre os serviços, que são interfaces para o consumo de outro VSPackage. Os serviços em um VSPackage podem substituir serviços internos ou outros.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- services, essentials
ms.assetid: fbe84ad9-efe1-48b1-aba3-b50b90424d47
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 69e7e1c5b18019c4ff063ec504fc702f47f7e023
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105080821"
---
# <a name="service-essentials"></a>Conceitos básicos do serviço
Um serviço é um contrato entre duas VSPackages. Um VSPackage fornece um conjunto específico de interfaces para que outro VSPackage consuma. [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] é, em si, uma coleção de VSPackages que fornece serviços para outros VSPackages.

 Por exemplo, você pode usar o serviço SVsActivityLog para obter uma interface IVsActivityLog, que pode ser usada para gravar no log de atividades. Para obter mais informações, consulte [como: usar o log de atividades](../../extensibility/how-to-use-the-activity-log.md).

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] também fornece alguns serviços internos que não estão registrados. O VSPackages pode substituir serviços internos ou outros fornecendo uma substituição de serviço. Somente uma substituição de serviço é permitida para qualquer serviço.

 Os serviços não têm capacidade de descoberta. Portanto, você deve saber o identificador de serviço (SID) de um serviço que deseja consumir e deve saber quais interfaces ele fornece. A documentação de referência para o serviço fornece essas informações.

- VSPackages que fornecem serviços são chamados de provedores de serviços.

- Os serviços que são fornecidos a outros VSPackages são chamados de serviços globais.

- Os serviços que estão disponíveis somente para o VSPackage que os implementa, ou para qualquer objeto que ele cria, são chamados de serviços locais.

- Os serviços que substituem serviços internos ou serviços fornecidos por outros pacotes são chamados de substituições de serviço.

- Serviços, ou substituições de serviço, são carregados sob demanda, ou seja, o provedor de serviços é carregado quando o serviço que ele fornece é solicitado por outro VSPackage.

- Para dar suporte ao carregamento sob demanda, um provedor de serviços registra seus serviços globais com o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] . Para obter mais informações, consulte [como: fornecer um serviço](../../extensibility/how-to-provide-a-service.md).

- Depois de obter um serviço, use [QueryInterface](/cpp/atl/queryinterface) (código não gerenciado) ou conversão (código gerenciado) para obter a interface desejada, por exemplo:

  ```vb
  TryCast(GetService(GetType(SVsActivityLog)), IVsActivityLog)
  ```

  ```csharp
  GetService(typeof(SVsActivityLog)) as IVsActivityLog;
  ```

- O código gerenciado refere-se a um serviço por seu tipo, enquanto o código não gerenciado se refere a um serviço por seu GUID.

- Quando [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] o carrega um VSPackage, ele passa um provedor de serviços para o VSPackage para conceder o VSPackage acesso aos serviços globais. Isso é chamado de "Localizando" do VSPackage.

- VSPackages podem ser provedores de serviços para os objetos que criam. Por exemplo, um formulário pode enviar uma solicitação de um serviço de cores para seu quadro, que pode passar a solicitação para [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] .

- Os objetos gerenciados que estão profundamente aninhados, ou não site, podem chamar o <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> acesso direto aos serviços globais.

<a name="how-to-use-getglobalservice"></a>

## <a name="use-getglobalservice"></a>Usar GetGlobalService

Às vezes, talvez seja necessário obter um serviço de uma janela de ferramentas ou de um contêiner de controle que não tenha sido site, ou que tenha sido site com um provedor de serviços que não saiba sobre o serviço desejado. Por exemplo, talvez você queira gravar no log de atividades de dentro de um controle. Para obter mais informações sobre esses e outros cenários, consulte [como solucionar problemas de serviços](../../extensibility/how-to-troubleshoot-services.md).

Você pode obter a maioria dos serviços do Visual Studio chamando o <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> método estático.

<xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> o se baseia em um provedor de serviços em cache que é inicializado na primeira vez que qualquer VSPackage derivado do pacote é site. Você deve garantir que essa condição seja atendida ou esteja preparada para um serviço nulo.

Felizmente, <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> o funciona corretamente na maioria das vezes.

- Se um VSPackage fornecer um serviço conhecido apenas para outro VSPackage, o VSPackage solicitando o serviço será colocado no local antes que o VSPackage que fornece o serviço seja carregado.

- Se uma janela de ferramenta for criada por um VSPackage, o VSPackage será acessado antes que a janela de ferramentas seja criada.

- Se um contêiner de controle for hospedado por uma janela de ferramenta criada por um VSPackage, o VSPackage será armazenado no site antes do contêiner de controle ser criado.

### <a name="to-get-a-service-from-within-a-tool-window-or-control-container"></a>Para obter um serviço de dentro de uma janela de ferramentas ou contêiner de controle

- Insira este código no construtor, na janela de ferramentas ou no contêiner de controle:

    ```csharp
    IVsActivityLog log = Package.GetGlobalService(typeof(SVsActivityLog)) as IVsActivityLog;
        if (log == null) return;
    ```

    ```vb
    Dim log As IVsActivityLog = TryCast(Package.GetGlobalService(GetType(SVsActivityLog)), IVsActivityLog)
    If log Is Nothing Then
        Return
    End If
    ```

    Esse código obtém um serviço SVsActivityLog e o converte em uma interface IVsActivityLog, que pode ser usada para gravar no log de atividades. Para obter um exemplo, consulte [como: usar o log de atividades](../../extensibility/how-to-use-the-activity-log.md).

## <a name="see-also"></a>Confira também

- [Lista de serviços disponíveis](../../extensibility/internals/list-of-available-services.md)
- [Usando e fornecendo serviços](../../extensibility/using-and-providing-services.md)
- [Conversões cast e conversões de tipo](/dotnet/csharp/programming-guide/types/casting-and-type-conversions)
- [Transmissão](/cpp/cpp/casting)
