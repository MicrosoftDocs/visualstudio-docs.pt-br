---
title: Criando páginas de opções | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- managed package framework, creating Tools Options pages
- Tools Options pages [Visual Studio SDK], creating using managed package framework
ms.assetid: 1bf11fec-dece-4943-8053-6de1483c43eb
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 236d9a0be82885bdf8040c97601429279e74dd15
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49949637"
---
# <a name="create-options-pages"></a>Criar páginas de opções
No [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] estrutura de pacote gerenciado, as classes derivadas de <xref:Microsoft.VisualStudio.Shell.DialogPage> estender a [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE adicionando **opções** páginas sob o **ferramentas** menu.  
  
 Um objeto que implementa um determinado **opção de ferramentas** página estiver associada a VSPackages específicos pelo <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> objeto.  
  
 Porque o ambiente instancia o objeto que implementa um determinado **opções de ferramentas** página quando a página específica é exibida pelo IDE:  
  
-   Um **opção ferramentas** página deve ser implementada em seu próprio objeto e não no objeto que implementa um VSPackage.  
  
-   Um objeto não é possível implementar várias **opções de ferramentas** páginas.  
  
## <a name="register-as-a-tools-options-page-provider"></a>Registrar como um provedor de página de opções de ferramentas  
 Uma configuração de usuário de suporte de VSPackage através de **opções de ferramentas** páginas indica os objetos que fornece esses **opções de ferramentas** páginas por meio da aplicação de instâncias de <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> aplicada para o <xref:Microsoft.VisualStudio.Shell.Package>implementação.  
  
 Deve haver uma instância do <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> para cada <xref:Microsoft.VisualStudio.Shell.DialogPage>-derivado do tipo que implementa um **opções de ferramentas** página.  
  
 Cada instância do <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> usa o tipo que implementa o **opções de ferramentas** página, cadeias de caracteres que contêm a categoria e subcategoria usado para identificar um **opções de ferramentas** página e recurso informações para registrar o tipo que o fornecimento de um **opções de ferramentas** página.  
  
## <a name="persist-tools-options-page-state"></a>Persistir o estado da página de opções de ferramentas  
 Se um **opções de ferramentas** implementação de página é registrada com o suporte de automação habilitado, a IDE persiste o estado da página, juntamente com todos os outros **opções de ferramentas** páginas.  
  
 Um VSPackage pode gerenciar sua própria persistência usando <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute>. Apenas um ou outro método de persistência deve ser usado.  
  
## <a name="implement-dialogpage-class"></a>Implementar classe DialogPage  
 Um objeto que fornece a implementação de um VSPackage de um <xref:Microsoft.VisualStudio.Shell.DialogPage>-tipo derivado pode tirar proveito dos recursos herdados a seguir:  
  
- Uma janela de interface de usuário padrão.  
  
- Um padrão disponível do mecanismo de persistência ambos se <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> é aplicado à classe, ou se o <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute.SupportsProfiles%2A> estiver definida como `true` para o <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> que é aplicado à classe.  
  
- Suporte de automação.  
  
  O requisito mínimo para um objeto que implementa um **opções de ferramentas** página usando <xref:Microsoft.VisualStudio.Shell.DialogPage> é a adição de propriedades públicas.  
  
  Se a classe registrada corretamente como um **opções de ferramentas** página provedor, em seguida, suas propriedades públicas estão disponíveis na **opções** seção o **ferramentas** menu na forma de um grade de propriedade.  
  
  Todos esses recursos padrão podem ser substituídos. Por exemplo, para criar um usuário mais sofisticado interface exige apenas substituir a implementação padrão de <xref:Microsoft.VisualStudio.Shell.DialogPage.Window%2A>.  
  
## <a name="example"></a>Exemplo  
 O que se segue é uma implementação simples "Hello world" de uma página de opções. Adicionando o seguinte código a um projeto padrão criado pelo modelo de pacote do Visual Studio com o **comando de Menu** opção selecionada adequadamente demonstrará a funcionalidade da página de opção.  
  
### <a name="description"></a>Descrição  
 A classe a seguir define uma página de opções de mínimo "Hello world". Quando aberto, o usuário pode definir o público `HelloWorld` propriedade em uma grade de propriedade.  
  
### <a name="code"></a>Código  
 [!code-csharp[UI_UserSettings_ToolsOptionPages#11](../../extensibility/internals/codesnippet/CSharp/creating-options-pages_1.cs)]
 [!code-vb[UI_UserSettings_ToolsOptionPages#11](../../extensibility/internals/codesnippet/VisualBasic/creating-options-pages_1.vb)]  
  
### <a name="description"></a>Descrição  
 Aplicar o seguinte atributo à classe de pacote disponibiliza as opções de página quando o pacote for carregado. Os números são arbitrárias IDs de recurso para a categoria e a página e o valor booliano no final Especifica se a página dá suporte à automação.  
  
### <a name="code"></a>Código  
 [!code-csharp[UI_UserSettings_ToolsOptionPages#07](../../extensibility/internals/codesnippet/CSharp/creating-options-pages_2.cs)]
 [!code-vb[UI_UserSettings_ToolsOptionPages#07](../../extensibility/internals/codesnippet/VisualBasic/creating-options-pages_2.vb)]  
  
### <a name="description"></a>Descrição  
 O manipulador de eventos a seguir exibe um resultado, dependendo do valor da propriedade definida na página de opções. Ele usa o <xref:Microsoft.VisualStudio.Shell.Package.GetDialogPage%2A> método com o resultado explicitamente convertido no tipo de página de opção personalizada para acessar as propriedades expostas pela página.  
  
 No caso de um projeto gerado pelo modelo do pacote, chame essa função do `MenuItemCallback` função para anexá-lo para o comando padrão é adicionado para o **ferramentas** menu.  
  
### <a name="code"></a>Código  
 [!code-csharp[UI_UserSettings_ToolsOptionPages#08](../../extensibility/internals/codesnippet/CSharp/creating-options-pages_3.cs)]
 [!code-vb[UI_UserSettings_ToolsOptionPages#08](../../extensibility/internals/codesnippet/VisualBasic/creating-options-pages_3.vb)]  
  
## <a name="see-also"></a>Consulte também  
 [Estender opções e configurações de usuário](../../extensibility/extending-user-settings-and-options.md)   
 [Suporte de automação para páginas de opções](../../extensibility/internals/automation-support-for-options-pages.md)