---
title: Criando páginas de opções | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- managed package framework, creating Tools Options pages
- Tools Options pages [Visual Studio SDK], creating using managed package framework
ms.assetid: 1bf11fec-dece-4943-8053-6de1483c43eb
caps.latest.revision: 30
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 076c4934fe4f81bd56edc70356ecdcc1101456e8
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51760324"
---
# <a name="creating-options-pages"></a>Criando páginas de opções
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

No [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] estrutura de pacote gerenciado, as classes derivadas de <xref:Microsoft.VisualStudio.Shell.DialogPage> estender a [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] IDE adicionando **opções** páginas sob o **ferramentas** menu.  
  
 Um objeto que implementa um determinado **opção de ferramentas** página estiver associada a VSPackages específicos pelo <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> objeto.  
  
 Porque o ambiente instancia o objeto que implementa um determinado **opções de ferramentas** página quando a página específica é exibida pelo IDE:  
  
-   Um **opção ferramentas** página deve ser implementada em seu próprio objeto e não no objeto que implementa um VSPackage.  
  
-   Um objeto não é possível implementar várias **opções de ferramentas** páginas.  
  
## <a name="registering-as-a-tools-options-page-provider"></a>Registrar-se como um provedor de página de opções de ferramentas  
 Uma configuração de usuário de suporte de VSPackage através de **opções de ferramentas** páginas indica os objetos que fornece esses **opções de ferramentas** páginas por meio da aplicação de instâncias de <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> aplicada para o <xref:Microsoft.VisualStudio.Shell.Package>implementação.  
  
 Deve haver uma instância do <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> para cada <xref:Microsoft.VisualStudio.Shell.DialogPage>-derivado do tipo que implementa um **opções de ferramentas** página.  
  
 Cada instância do <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> usa o tipo que implementa o **opções de ferramentas** página, cadeias de caracteres que contêm a categoria e subcategoria usado para identificar um **opções de ferramentas** página e recurso informações para registrar o tipo que o fornecimento de um **opções de ferramentas** página.  
  
## <a name="persisting-tools-options-page-state"></a>Manter estado da página Opções de ferramentas  
 Se um **opções de ferramentas** implementação de página é registrada com o suporte de automação habilitado, a IDE persiste o estado da página, juntamente com todos os outros **opções de ferramentas** páginas.  
  
 Um VSPackage pode gerenciar sua própria persistência usando <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute>. Apenas um ou outro método de persistência deve ser usado.  
  
## <a name="implementing-dialogpage-class"></a>A implementação da classe de DialogPage  
 Um objeto que fornece a implementação de um VSPackage de um <xref:Microsoft.VisualStudio.Shell.DialogPage>-tipo derivado pode tirar proveito dos recursos herdados a seguir:  
  
- Uma janela de interface de usuário padrão.  
  
- Um padrão disponível do mecanismo de persistência ambos se <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> é aplicado à classe, ou se o <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute.SupportsProfiles%2A> estiver definida como `true` para o <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> que é aplicado à classe.  
  
- Suporte de automação.  
  
  O requisito mínimo para um objeto que implementa um **opções de ferramentas** página usando <xref:Microsoft.VisualStudio.Shell.DialogPage> é a adição de propriedades públicas.  
  
  Se a classe registrada corretamente como um **opções de ferramentas** página provedor, em seguida, suas propriedades públicas estão disponíveis na **opções** seção o **ferramentas** menu na forma de um grade de propriedade.  
  
  Todos esses recursos padrão podem ser substituídos. Por exemplo, para criar um usuário mais sofisticado interface exige apenas substituir a implementação padrão de <xref:Microsoft.VisualStudio.Shell.DialogPage.Window%2A>.  
  
## <a name="example"></a>Exemplo  
 O que se segue é uma implementação simples "hello world" de uma página de opções. Adicionando o seguinte código a um projeto padrão criado pelo modelo do pacote Visual Studio com o **comando de Menu** opção selecionada adequadamente demonstrará a funcionalidade da página de opção.  
  
### <a name="description"></a>Descrição  
 A classe a seguir define uma página de opções de mínimo "hello world". Quando aberto, o usuário pode definir o público `HelloWorld` propriedade em uma grade de propriedade.  
  
### <a name="code"></a>Código  
 [!code-csharp[UI_UserSettings_ToolsOptionPages#11](../../snippets/csharp/VS_Snippets_VSSDK/ui_usersettings_toolsoptionpages/cs/class1.cs#11)]
 [!code-vb[UI_UserSettings_ToolsOptionPages#11](../../snippets/visualbasic/VS_Snippets_VSSDK/ui_usersettings_toolsoptionpages/vb/class1.vb#11)]  
  
### <a name="description"></a>Descrição  
 Aplicar o seguinte atributo à classe de pacote disponibiliza as opções de página quando o pacote for carregado. Os números são arbitrárias IDs de recurso para a categoria e a página e o valor booliano no final Especifica se a página dá suporte à automação.  
  
### <a name="code"></a>Código  
 [!code-csharp[UI_UserSettings_ToolsOptionPages#07](../../snippets/csharp/VS_Snippets_VSSDK/ui_usersettings_toolsoptionpages/cs/uiusersettingstoolsoptionspagespackage.cs#07)]
 [!code-vb[UI_UserSettings_ToolsOptionPages#07](../../snippets/visualbasic/VS_Snippets_VSSDK/ui_usersettings_toolsoptionpages/vb/uiusersettingstoolsoptionspagespackage.vb#07)]  
  
### <a name="description"></a>Descrição  
 O manipulador de eventos a seguir exibe um resultado, dependendo do valor da propriedade definida na página de opções. Ele usa o <xref:Microsoft.VisualStudio.Shell.Package.GetDialogPage%2A> método com o resultado explicitamente convertido no tipo de página de opção personalizada para acessar as propriedades expostas pela página.  
  
 No caso de um projeto gerado pelo modelo do pacote, chame essa função do `MenuItemCallback` função para anexá-lo para o comando padrão é adicionado para o **ferramentas** menu.  
  
### <a name="code"></a>Código  
 [!code-csharp[UI_UserSettings_ToolsOptionPages#08](../../snippets/csharp/VS_Snippets_VSSDK/ui_usersettings_toolsoptionpages/cs/uiusersettingstoolsoptionspagespackage.cs#08)]
 [!code-vb[UI_UserSettings_ToolsOptionPages#08](../../snippets/visualbasic/VS_Snippets_VSSDK/ui_usersettings_toolsoptionpages/vb/uiusersettingstoolsoptionspagespackage.vb#08)]  
  
## <a name="see-also"></a>Consulte também  
 [Opções e configurações de usuário de extensão](../../extensibility/extending-user-settings-and-options.md)   
 [Suporte à automação para páginas de opções](../../extensibility/internals/automation-support-for-options-pages.md)

