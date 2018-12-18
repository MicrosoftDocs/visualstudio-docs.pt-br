---
title: Opções e páginas de opções | Microsoft Docs
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
- Tools Options pages [Visual Studio SDK], managed package framework support
- managed package framework, Tools Options pages support
- support, Tools Options pages
- Tools Options pages [Visual Studio SDK], layouts
- Tools Options pages [Visual Studio SDK], attributes
ms.assetid: e6c0e636-5ec3-450e-b395-fc4bb9d75918
caps.latest.revision: 35
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 005aeceb328a24c8c90994b6b274dbddc6b874f8
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51783266"
---
# <a name="options-and-options-pages"></a>Opções e páginas de opções
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Clicando em **opções** sobre o **ferramentas** menu é aberto o **opções** caixa de diálogo. As opções na caixa de diálogo são coletivamente chamadas de páginas de opções. O controle de árvore no painel de navegação inclui as categorias de opções, e cada categoria tem páginas de opções. Quando você seleciona uma página, suas opções aparecem no painel direito. Essas páginas permitem que você altere os valores das opções que determinam o estado de um VSPackage.  
  
## <a name="support-for-options-pages"></a>Suporte para páginas de opções  
 O <xref:Microsoft.VisualStudio.Shell.Package> classe oferece suporte para a criação de páginas de opções e as categorias de opções. O <xref:Microsoft.VisualStudio.Shell.DialogPage> classe implementa uma página de opções.  
  
 A implementação padrão de <xref:Microsoft.VisualStudio.Shell.DialogPage> oferece suas propriedades públicas para um usuário em uma grade genérico de propriedades. Você pode personalizar esse comportamento, substituindo os vários métodos de página para criar uma página de opções personalizada que tem sua própria interface do usuário (IU). Para obter mais informações, consulte [criando uma página de opções](../../extensibility/creating-an-options-page.md).  
  
 O <xref:Microsoft.VisualStudio.Shell.DialogPage> implementos de classe <xref:Microsoft.VisualStudio.Shell.IProfileManager>, que fornece a persistência para páginas de opções e também para as configurações do usuário. As implementações padrão do <xref:Microsoft.VisualStudio.Shell.IProfileManager.LoadSettingsFromStorage%2A> e <xref:Microsoft.VisualStudio.Shell.IProfileManager.SaveSettingsToStorage%2A> métodos persistirem as alterações de propriedade em uma seção do usuário do registro se a propriedade pode ser convertida em uma cadeia de caracteres.  
  
## <a name="options-page-registry-path"></a>Caminho do registro de página de opções  
 Por padrão, o caminho do registro das propriedades gerenciadas por uma página de opções é determinado pela combinação <xref:Microsoft.VisualStudio.Shell.Package.UserRegistryRoot%2A>, a palavra DialogPage e o nome do tipo da classe de página de opções. Por exemplo, uma classe de página de opções pode ser definida da seguinte maneira.  
  
 [!code-csharp[VSSDKSupportForOptionsPages#1](../../snippets/csharp/VS_Snippets_VSSDK/vssdksupportforoptionspages/cs/vssdksupportforoptionspagespackage.cs#1)]
 [!code-vb[VSSDKSupportForOptionsPages#1](../../snippets/visualbasic/VS_Snippets_VSSDK/vssdksupportforoptionspages/vb/vssdksupportforoptionspagespackage.vb#1)]  
  
 Se o <xref:Microsoft.VisualStudio.Shell.Package.UserRegistryRoot%2A> é HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0Exp, em seguida, os pares de nome e valor de propriedade são subchaves do HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0Exp\DialogPage\ Company.OptionsPage.OptionsPageGeneral.  
  
 O caminho do registro da página de opções em si é determinado pela combinação <xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A>, o word, ToolsOptionsPages e as opções de página de categoria e o nome. Por exemplo, se a página de opções personalizada tenha a categoria, minhas páginas de opção e o <xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A> é HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp, em seguida, a página de opções tem a chave do registro, hkey_local_machine\software\microsoft\. VisualStudio\8.0Exp\ToolsOptionsPages\My Pages\Custom de opção.  
  
## <a name="toolsoptions-page-attributes-and-layout"></a>Atributos de página e o Layout de ferramentas/opções  
 O <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> atributo determina o agrupamento de páginas de opções personalizadas em categorias na árvore de navegação do **opções** caixa de diálogo. O <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> atributo associa uma página de opções com o VSPackage que fornece a interface. Considere o fragmento de código a seguir:  
  
 [!code-csharp[VSSDKSupportForOptionsPages#2](../../snippets/csharp/VS_Snippets_VSSDK/vssdksupportforoptionspages/cs/vssdksupportforoptionspagespackage.cs#2)]
 [!code-vb[VSSDKSupportForOptionsPages#2](../../snippets/visualbasic/VS_Snippets_VSSDK/vssdksupportforoptionspages/vb/vssdksupportforoptionspagespackage.vb#2)]  
  
 Isso declara que MyPackage fornece duas páginas de opções, OptionsPageGeneral e OptionsPageCustom. No **opções** caixa de diálogo, ambas as páginas de opções aparecem na **minhas páginas de opção** categoria como **geral** e **personalizado**, respectivamente.  
  
## <a name="option-attributes-and-layout"></a>Atributos de opção e Layout  
 A interface do usuário (IU) que fornece a página determina a aparência das opções em uma página de opções personalizadas. O layout, rotulagem e a descrição das opções em uma página de opções genéricas são determinados pelos seguintes atributos:  
  
- <xref:System.ComponentModel.CategoryAttribute> Determina a categoria da opção.  
  
- <xref:System.ComponentModel.DisplayNameAttribute> Determina o nome de exibição da opção.  
  
- <xref:System.ComponentModel.DescriptionAttribute> Determina a descrição da opção.  
  
  > [!NOTE]
  >  Atributos equivalentes, SRCategory, LocDisplayName e SRDescription, usar os recursos de cadeia de caracteres para localização e são definidos na [exemplo de projeto gerenciado](http://go.microsoft.com/fwlink/?LinkId=122774).  
  
  Considere o fragmento de código a seguir:  
  
  [!code-csharp[VSSDKSupportForOptionsPages#3](../../snippets/csharp/VS_Snippets_VSSDK/vssdksupportforoptionspages/cs/optionspagecustom.cs#3)]
  [!code-vb[VSSDKSupportForOptionsPages#3](../../snippets/visualbasic/VS_Snippets_VSSDK/vssdksupportforoptionspages/vb/optionspagegeneral.vb#3)]  
  
  A opção OptionInteger aparece na página de opções como **opção de número inteiro** no **minhas opções** categoria. Se a opção for selecionada, a descrição **minha opção inteiro**, aparece na caixa de descrição.  
  
## <a name="accessing-options-pages-from-another-vspackage"></a>Acessando páginas de opções de VSPackage outro  
 Um VSPackage que hospeda e gerencia uma página de opções pode ser acessado por meio de programação de VSPackage outro usando o modelo de automação. Por exemplo, no código a seguir um VSPackage é registrado como uma página de opção de hospedagem.  
  
 [!code-csharp[VSSDKSupportForOptionsPages#4](../../snippets/csharp/VS_Snippets_VSSDK/vssdksupportforoptionspages/cs/vssdksupportforoptionspagespackage.cs#4)]
 [!code-vb[VSSDKSupportForOptionsPages#4](../../snippets/visualbasic/VS_Snippets_VSSDK/vssdksupportforoptionspages/vb/vssdksupportforoptionspagespackage.vb#4)]  
  
 O fragmento de código a seguir obtém o valor de OptionInteger de MyOptionPage:  
  
 [!code-csharp[VSSDKSupportForOptionsPages#5](../../snippets/csharp/VS_Snippets_VSSDK/vssdksupportforoptionspages/cs/vssdksupportforoptionspagespackage.cs#5)]
 [!code-vb[VSSDKSupportForOptionsPages#5](../../snippets/visualbasic/VS_Snippets_VSSDK/vssdksupportforoptionspages/vb/vssdksupportforoptionspagespackage.vb#5)]  
  
 Quando o <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> atributo registra uma página de opções, a página está registrada sob a chave de AutomationProperties se o `SupportsAutomation` argumento do atributo é `true`. Automação examina esta entrada de registro para encontrar o VSPackage associado e automação e em seguida, acessa a propriedade por meio da página de opções hospedado, nesse caso, minha página de grade.  
  
 O caminho do registro da propriedade de automação é determinado pela combinação <xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A>, o word, AutomationProperties e as opções de página de categoria e o nome. Por exemplo, se a página de opções tem a categoria My Category, o nome de minha página de grade e o <xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A>, HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp e, em seguida, a propriedade de automação tem a chave do registro, HKEY_LOCAL_MACHINE\SOFTWARE\ Página de grade Category\My Microsoft\VisualStudio\8.0Exp\AutomationProperties\My.  
  
> [!NOTE]
>  O nome canônico, minha página de grade Category.My, é o valor da subchave nome dessa chave.

