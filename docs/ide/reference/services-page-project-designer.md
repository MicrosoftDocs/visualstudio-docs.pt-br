---
title: Página Serviços, Designer de Projeto
ms.date: 01/18/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- vb.ProjectPropertiesServices
helpviewer_keywords:
- Services page in Project Designer
- Project Designer, Services page
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: ba03b4aea25decef39983d203db12dfbedc516d9
ms.sourcegitcommit: 5b767247b3d819a99deb0dbce729a0562b9654ba
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/20/2018
ms.locfileid: "39177013"
---
# <a name="services-page-project-designer"></a>Página Serviços, Designer de Projeto

Os serviços de aplicativo cliente fornecem acesso simplificado ao logon, às funções e aos serviços de perfil do [!INCLUDE[ajax_current_short](../../ide/reference/includes/ajax_current_short_md.md)] por meio dos aplicativos Windows Forms e WPF (Windows Presentation Foundation). Você pode usar a página **Serviços** do **Designer de Projeto** para habilitar e configurar serviços de aplicativo cliente para seu projeto.

Com os serviços de aplicativo cliente, você pode usar um servidor centralizado para autenticar usuários, determinar a função ou as funções atribuídas a cada usuário e armazenar configurações de aplicativo por usuário que você pode compartilhar pela rede. Para obter mais informações, consulte [Serviços de aplicativo cliente](/dotnet/framework/common-client-technologies/client-application-services).

Para acessar a página **Serviços**, selecione um nó do projeto no **Gerenciador de Soluções** e, em seguida, clique em **Propriedades** no menu **Projeto**. Quando o **Designer de Projeto** for exibido, clique na guia **Serviços**.

## <a name="task-list"></a>Lista de Tarefas

[Como configurar serviços de aplicativo cliente](/dotnet/framework/common-client-technologies/how-to-configure-client-application-services)

## <a name="uielement-list"></a>Lista UIElement

 **Configuração**

 Esse controle não é editável nesta página. Para obter uma descrição desse controle, consulte [Página de compilação, Designer de Projeto (Visual Basic)](../../ide/reference/compile-page-project-designer-visual-basic.md) ou [Página de Build, Designer de Projeto (C#)](../../ide/reference/build-page-project-designer-csharp.md).

 **Plataforma**

 Esse controle não é editável nesta página. Para obter uma descrição desse controle, consulte [Página de compilação, Designer de Projeto (Visual Basic)](../../ide/reference/compile-page-project-designer-visual-basic.md) ou [Página de Build, Designer de Projeto (C#)](../../ide/reference/build-page-project-designer-csharp.md).

 **Habilitar serviços do aplicativo cliente**

 Selecione para habilitar serviços do aplicativo cliente. Você deve especificar locais de serviço na página **Serviços** para usar serviços de aplicativo cliente.

 **Usar a autenticação do Windows**

 Indica que o provedor de autenticação usará a autenticação baseada em Windows, ou seja, a identidade fornecida pelo sistema operacional Windows.

 **Usar autenticação de Formulários**

 Indica que o provedor de autenticação usará a autenticação de formulários. Isso significa que seu aplicativo deve fornecer uma interface do usuário para logon. Para obter mais informações, consulte [Como implementar o logon do usuário com os serviços de aplicativo cliente](/dotnet/framework/common-client-technologies/how-to-implement-user-login-with-client-application-services).

 **Local do serviço de autenticação**

 Utilizado somente com autenticação de formulários. Especifica o local do serviço de autenticação.

 **Opcional: provedor de credenciais**

 Utilizado somente com autenticação de formulários. Indica a implementação <xref:System.Web.ClientServices.Providers.IClientFormsAuthenticationCredentialsProvider> que o serviço de autenticação usará para exibir uma caixa de diálogo de logon quando o aplicativo chamar o método `static`<xref:System.Web.Security.Membership.ValidateUser%2A?displayProperty=fullName> e passar cadeias de caracteres vazias ou `null` para os parâmetros. Se deixar essa caixa em branco, você deverá passar um nome de usuário válido e uma senha para o método <xref:System.Web.Security.Membership.ValidateUser%2A?displayProperty=fullName>. Você deve especificar o provedor de credenciais como um nome de tipo qualificado pelo assembly. Para obter mais informações, consulte <xref:System.Type.AssemblyQualifiedName%2A?displayProperty=fullName> e [Assembly Names](/dotnet/framework/app-domains/assembly-names) (Nomes de assembly). Em sua forma mais simples, um nome de tipo qualificado pelo assembly é semelhante ao exemplo a seguir: `MyNamespace.MyLoginClass, MyAssembly`

 **Local do serviço de funções**

 Especifica o local do serviço de funções.

 **Local do serviço de configurações da Web**

 Especifica o local do serviço de perfil (configurações da Web).

 **Avançado**

 Abre [Configurações Avançadas para a Caixa de Diálogo Serviços](../../ide/reference/advanced-settings-for-services-dialog-box.md), que você pode usar para substituir o comportamento padrão. Por exemplo, você pode usar essa caixa de diálogo para especificar um banco de dados para armazenamento offline, em vez de usar o sistema de arquivos local. Para obter mais informações, consulte [Configurações Avançadas para a Caixa de Diálogo Serviços](../../ide/reference/advanced-settings-for-services-dialog-box.md).

## <a name="see-also"></a>Consulte também

- [Serviços de aplicativos cliente](/dotnet/framework/common-client-technologies/client-application-services)
- [Caixa de diálogo Configurações Avançadas para Serviços](../../ide/reference/advanced-settings-for-services-dialog-box.md)
- [Como configurar serviços de aplicativo cliente](/dotnet/framework/common-client-technologies/how-to-configure-client-application-services)
- [Página de Compilação, Designer de Projeto (Visual Basic)](../../ide/reference/compile-page-project-designer-visual-basic.md)
- [Página de Build, Designer de Projeto (C#)](../../ide/reference/build-page-project-designer-csharp.md)
