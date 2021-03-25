---
title: Opções e páginas de opções | Microsoft Docs
description: Saiba mais sobre o suporte para páginas de opções, que permitem alterar os valores das opções que determinam o estado de um VSPackage.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Tools Options pages [Visual Studio SDK], managed package framework support
- managed package framework, Tools Options pages support
- support, Tools Options pages
- Tools Options pages [Visual Studio SDK], layouts
- Tools Options pages [Visual Studio SDK], attributes
ms.assetid: e6c0e636-5ec3-450e-b395-fc4bb9d75918
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1b6c5810cd95b50a63f32cfaa6123e81e35a4be9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105063026"
---
# <a name="options-and-options-pages"></a>Opções e páginas de opções
Clicar em **Opções** no menu **ferramentas** abre a caixa de diálogo **Opções** . As opções nessa caixa de diálogo são chamadas coletivamente de páginas de opções. O controle de árvore no painel de navegação inclui categorias de opções e cada categoria tem páginas de opções. Quando você seleciona uma página, suas opções aparecem no painel direito. Essas páginas permitem que você altere os valores das opções que determinam o estado de um VSPackage.

## <a name="support-for-options-pages"></a>Suporte para páginas de opções
 A <xref:Microsoft.VisualStudio.Shell.Package> classe fornece suporte para a criação de categorias de opções páginas e opções. A <xref:Microsoft.VisualStudio.Shell.DialogPage> classe implementa uma página de opções.

 A implementação padrão do <xref:Microsoft.VisualStudio.Shell.DialogPage> oferece suas propriedades públicas para um usuário em uma grade genérica de propriedades. Você pode personalizar esse comportamento substituindo vários métodos na página para criar uma página de opções personalizadas que tenha sua própria interface do usuário. Para obter mais informações, consulte [criando uma página de opções](../../extensibility/creating-an-options-page.md).

 A <xref:Microsoft.VisualStudio.Shell.DialogPage> classe implementa <xref:Microsoft.VisualStudio.Shell.IProfileManager> , que fornece persistência para páginas de opções e também para configurações de usuário. As implementações padrão dos <xref:Microsoft.VisualStudio.Shell.IProfileManager.LoadSettingsFromStorage%2A> <xref:Microsoft.VisualStudio.Shell.IProfileManager.SaveSettingsToStorage%2A> métodos e mantêm as alterações de propriedade em uma seção de usuário do registro se a propriedade puder ser convertida em e de uma cadeia de caracteres.

## <a name="options-page-registry-path"></a>Caminho do registro da página de opções
 Por padrão, o caminho do registro das propriedades gerenciadas por uma página de opções é determinado pela combinação <xref:Microsoft.VisualStudio.Shell.Package.UserRegistryRoot%2A> , a palavra DialogPage e o nome do tipo da classe de página de opções. Por exemplo, uma classe de página de opções pode ser definida da seguinte maneira.

 [!code-csharp[VSSDKSupportForOptionsPages#1](../../extensibility/internals/codesnippet/CSharp/options-and-options-pages_1.cs)]
 [!code-vb[VSSDKSupportForOptionsPages#1](../../extensibility/internals/codesnippet/VisualBasic/options-and-options-pages_1.vb)]

 Se o <xref:Microsoft.VisualStudio.Shell.Package.UserRegistryRoot%2A> for HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0Exp, os pares nome da propriedade e valor serão subchaves de HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0Exp\DialogPage\Company.OptionsPage.OptionsPageGeneral.

 O caminho do registro da própria página de opções é determinado pela combinação <xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A> , a palavra, a ToolsOptionsPages e a categoria e o nome da página de opções. Por exemplo, se a página opções personalizadas tiver a categoria, as páginas de minha opção e o <xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A> for HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp, a página opções terá a chave do registro HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\ToolsOptionsPages\My Option Pages\Custom.

## <a name="toolsoptions-page-attributes-and-layout"></a>Layout e atributos de página de ferramentas/opções
 O <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> atributo determina o agrupamento de páginas de opções personalizadas em categorias na árvore de navegação da caixa de diálogo **Opções** . O <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> atributo associa uma página de opções com o VSPackage que fornece a interface. Considere o fragmento de código a seguir:

 [!code-csharp[VSSDKSupportForOptionsPages#2](../../extensibility/internals/codesnippet/CSharp/options-and-options-pages_2.cs)]
 [!code-vb[VSSDKSupportForOptionsPages#2](../../extensibility/internals/codesnippet/VisualBasic/options-and-options-pages_2.vb)]

 Isso declara que MyPackage fornece duas páginas de opções, OptionsPageGeneral e OptionsPageCustom. Na caixa de diálogo **Opções** , ambas as páginas de opções aparecem na categoria de **páginas minha opção** , como **geral** e **personalizada**, respectivamente.

## <a name="option-attributes-and-layout"></a>Layout e atributos de opção
 A interface do usuário (IU) que a página fornece determina a aparência das opções em uma página de opções personalizadas. O layout, a rotulagem e a descrição das opções em uma página de opções genéricas são determinados pelos seguintes atributos:

- <xref:System.ComponentModel.CategoryAttribute> determina a categoria da opção.

- <xref:System.ComponentModel.DisplayNameAttribute> determina o nome de exibição da opção.

- <xref:System.ComponentModel.DescriptionAttribute> determina a descrição da opção.

  > [!NOTE]
  > Atributos equivalentes, SRCategory, LocDisplayName e SRDescription, usam recursos de cadeia de caracteres para localização e são definidos no [exemplo de projeto gerenciado](/azure/devops/integrate/index).

  Considere o fragmento de código a seguir:

  [!code-csharp[VSSDKSupportForOptionsPages#3](../../extensibility/internals/codesnippet/CSharp/options-and-options-pages_3.cs)]
  [!code-vb[VSSDKSupportForOptionsPages#3](../../extensibility/internals/codesnippet/VisualBasic/options-and-options-pages_3.vb)]

  A opção OptionInteger aparece na página opções como **opção de inteiro** na categoria **minhas opções** . Se a opção estiver selecionada, a opção descrição, **meu inteiro** aparecerá na caixa Descrição.

## <a name="accessing-options-pages-from-another-vspackage"></a>Acessando páginas de opções de outro VSPackage
 Um VSPackage que hospeda e gerencia uma página de opções pode ser acessado por meio de programação de outro VSPackage usando o modelo de automação. Por exemplo, no código a seguir, um VSPackage é registrado como Hospedagem de uma página de opções.

 [!code-csharp[VSSDKSupportForOptionsPages#4](../../extensibility/internals/codesnippet/CSharp/options-and-options-pages_4.cs)]
 [!code-vb[VSSDKSupportForOptionsPages#4](../../extensibility/internals/codesnippet/VisualBasic/options-and-options-pages_4.vb)]

 O fragmento de código a seguir obtém o valor de OptionInteger de MyOptionPage:

 [!code-csharp[VSSDKSupportForOptionsPages#5](../../extensibility/internals/codesnippet/CSharp/options-and-options-pages_5.cs)]
 [!code-vb[VSSDKSupportForOptionsPages#5](../../extensibility/internals/codesnippet/VisualBasic/options-and-options-pages_5.vb)]

 Quando o <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> atributo registra uma página de opções, a página é registrada na chave AutomationProperties se o `SupportsAutomation` argumento do atributo for `true` . A automação examina essa entrada de registro para localizar o VSPackage associado e a automação, em seguida, acessa a propriedade por meio da página opções hospedadas, nesse caso, a página de grade.

 O caminho do registro da propriedade de automação é determinado pela combinação <xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A> , a palavra, a AutomationProperties e a categoria e o nome da página de opções. Por exemplo, se a página de opções tiver a categoria minha categoria, o nome da página de grade e o <xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A> , HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp, a propriedade de automação terá a chave do registro, HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\AutomationProperties\My Category\My Grid Page.

> [!NOTE]
> O nome canônico, minha página de grade Category.My, é o valor da subchave Name dessa chave.
