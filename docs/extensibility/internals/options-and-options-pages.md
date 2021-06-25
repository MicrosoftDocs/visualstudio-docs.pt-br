---
title: Opções e páginas de opções | Microsoft Docs
description: Saiba mais sobre o suporte para páginas de opções, que permitem alterar os valores das opções que determinam o estado de um VSPackage.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
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
ms.openlocfilehash: ea05e894c0bfca077f1256c35e6fbe5c58bc91ea
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899882"
---
# <a name="options-and-options-pages"></a>Opções e páginas de opções
Clicar em **Opções** no menu **Ferramentas** abre a **caixa de diálogo** Opções. As opções nessa caixa de diálogo são coletivamente conhecidas como páginas de opções. O controle de árvore no painel de navegação inclui categorias de opções e cada categoria tem páginas de opções. Quando você seleciona uma página, suas opções aparecem no painel direito. Essas páginas permitem alterar os valores das opções que determinam o estado de um VSPackage.

## <a name="support-for-options-pages"></a>Suporte para páginas de opções
 A <xref:Microsoft.VisualStudio.Shell.Package> classe fornece suporte para a criação de páginas de opções e categorias de opções. A <xref:Microsoft.VisualStudio.Shell.DialogPage> classe implementa uma página de opções.

 A implementação padrão de <xref:Microsoft.VisualStudio.Shell.DialogPage> oferece suas propriedades públicas a um usuário em uma grade genérica de propriedades. Você pode personalizar esse comportamento substituindo vários métodos na página para criar uma página de opções personalizadas que tenha sua própria interface do usuário. Para obter mais informações, consulte [Criando uma página Opções](../../extensibility/creating-an-options-page.md).

 A <xref:Microsoft.VisualStudio.Shell.DialogPage> classe implementa , que fornece persistência para páginas de opções e também para <xref:Microsoft.VisualStudio.Shell.IProfileManager> configurações do usuário. As implementações padrão dos métodos e persistem alterações de propriedade em uma seção de usuário do Registro se a propriedade puder ser convertida de e para <xref:Microsoft.VisualStudio.Shell.IProfileManager.LoadSettingsFromStorage%2A> <xref:Microsoft.VisualStudio.Shell.IProfileManager.SaveSettingsToStorage%2A> uma cadeia de caracteres.

## <a name="options-page-registry-path"></a>Caminho do Registro de Página de Opções
 Por padrão, o caminho do Registro das propriedades gerenciadas por uma página de opções é determinado combinando , a palavra DialogPage e o nome do tipo da classe <xref:Microsoft.VisualStudio.Shell.Package.UserRegistryRoot%2A> de página options. Por exemplo, uma classe de página de opções pode ser definida da seguinte forma.

 :::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/vssdksupportforoptionspages/cs/vssdksupportforoptionspagespackage.cs" id="Snippet1":::
 :::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/vssdksupportforoptionspages/vb/vssdksupportforoptionspagespackage.vb" id="Snippet1":::

 Se o for HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0Exp, os pares nome e valor da propriedade <xref:Microsoft.VisualStudio.Shell.Package.UserRegistryRoot%2A> serão subkeys de HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0Exp\DialogPage\Company.OptionsPage.OptionsPageGeneral.

 O caminho do Registro da página de opções em si é determinado combinando , a palavra ToolsOptionsPages e o nome e a categoria da página <xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A> de opções. Por exemplo, se a página Opções personalizadas tiver a categoria Minhas Páginas de Opção e o for HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp, a página de opções terá a chave do <xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A> Registro, HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\ToolsOptionsPages\My Option Pages\Custom.

## <a name="toolsoptions-page-attributes-and-layout"></a>Atributos e layout da página Ferramentas/Opções
 O <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> atributo determina o agrupamento de páginas de opções personalizadas em categorias na árvore de navegação da caixa de **diálogo** Opções. O <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> atributo associa uma página de opções ao VSPackage que fornece a interface . Considere o fragmento de código a seguir:

:::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/vssdksupportforoptionspages/cs/vssdksupportforoptionspagespackage.cs" id="Snippet2":::
:::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/vssdksupportforoptionspages/vb/vssdksupportforoptionspagespackage.vb" id="Snippet2":::

 Isso declara que MyPackage fornece duas páginas de opções, OptionsPageGeneral e OptionsPageCustom. Na caixa **de diálogo** Opções, as duas páginas de opções aparecem na categoria Minhas Páginas **de Opção** como **Geral** **e Personalizada,** respectivamente.

## <a name="option-attributes-and-layout"></a>Atributos de opção e layout
 A interface do usuário que a página fornece determina a aparência das opções em uma página de opções personalizadas. O layout, a rotulagem e a descrição das opções em uma página de opções genéricas são determinados pelos seguintes atributos:

- <xref:System.ComponentModel.CategoryAttribute> determina a categoria da opção.

- <xref:System.ComponentModel.DisplayNameAttribute> determina o nome de exibição da opção.

- <xref:System.ComponentModel.DescriptionAttribute> determina a descrição da opção.

  > [!NOTE]
  > Atributos equivalentes, SRCategory, LocDisplayName e SRDescription, usam recursos de cadeia de caracteres para localização e são definidos no [exemplo de projeto gerenciado](/azure/devops/integrate/index).

  Considere o fragmento de código a seguir:

  :::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/vssdksupportforoptionspages/cs/optionspagecustom.cs" id="Snippet3":::
  :::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/vssdksupportforoptionspages/vb/optionspagegeneral.vb" id="Snippet3":::

  A opção OptionInteger aparece na página de opções como **Opção De Inteiro** na categoria **Minhas** Opções. Se a opção estiver selecionada, a descrição, **Opção Meu inteiro**, aparecerá na caixa de descrição.

## <a name="accessing-options-pages-from-another-vspackage"></a>Acessando páginas de opções de outro VSPackage
 Um VSPackage que hospeda e gerencia uma página de opções pode ser acessado programaticamente de outro VSPackage usando o modelo de automação. Por exemplo, no código a seguir, um VSPackage é registrado como hospedando uma página de opção.

 :::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/vssdksupportforoptionspages/cs/vssdksupportforoptionspagespackage.cs" id="Snippet4":::
 :::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/vssdksupportforoptionspages/vb/vssdksupportforoptionspagespackage.vb" id="Snippet4":::

 O fragmento de código a seguir obtém o valor de OptionInteger de MyOptionPage:

 :::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/vssdksupportforoptionspages/cs/vssdksupportforoptionspagespackage.cs" id="Snippet5":::
 :::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/vssdksupportforoptionspages/vb/vssdksupportforoptionspagespackage.vb" id="Snippet5":::

 Quando o atributo registra uma página de opções, a página é registrada na chave AutomationProperties se o <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> argumento do atributo for `SupportsAutomation` `true` . A automação examina essa entrada do Registro para encontrar o VSPackage associado e, em seguida, a automação acessa a propriedade por meio da página de opções hospedadas, nesse caso, Página Minha Grade.

 O caminho do Registro da propriedade de automação é determinado combinando , a palavra, AutomationProperties e a categoria e o nome da página <xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A> de opções. Por exemplo, se a página de opções tiver a categoria Minha Categoria, o nome da Minha Página da Grade e o , HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp, a propriedade de automação terá a chave do <xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A> Registro, HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\AutomationProperties\My Category\My Grid Page.

> [!NOTE]
> O nome canônico, My Category.My Grid Page, é o valor da sub-chave Nome dessa chave.
