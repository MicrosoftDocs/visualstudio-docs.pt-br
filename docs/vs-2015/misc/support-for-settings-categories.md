---
title: Suporte para categorias de configurações | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-csharp
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- settings, supporting with Visual Studio SDK
- Visual Studio SDK, supporting settings
ms.assetid: 3bac375d-8bd5-41be-a8de-32eb33c5cfac
caps.latest.revision: 20
manager: douge
ms.openlocfilehash: 53abd3c9f35f16c2f2ae62e2c4f339a86477a8b3
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49244927"
---
# <a name="support-for-settings-categories"></a>Suporte para categorias de configurações
Uma categoria de configurações consiste em um grupo de opções que personalizam o ambiente de desenvolvimento integrado (IDE). Por exemplo, as configurações podem controlar o layout de [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] windows e o conteúdo dos menus. Para obter mais informações, consulte [Personalizando configurações de desenvolvimento no Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
 Sobre o **ferramentas** menu, clique em **Import and Export Settings** para iniciar o **Import and Export Settings Wizard**. O assistente oferece três opções: exportar, importar ou redefinir as configurações. Por exemplo, selecionando export, abre o **escolher configurações para exportar** página do assistente.  
  
 O controle de árvore no painel de navegação desta página lista as categorias. Uma categoria é um grupo de configurações relacionadas que aparecem como um "ponto de configurações personalizadas", ou seja, como uma caixa de seleção. Você pode usar essas caixas de seleção para selecionar as categorias para persistir em um arquivo .vsettings. O assistente permite que você nomeie o arquivo .vsettings e especifique seu caminho.  
  
> [!NOTE]
>  As configurações são salvos ou restauradas como uma categoria e nomes de configuração individuais não são exibidos no assistente.  
  
 A estrutura de pacote gerenciado (MPF) dá suporte à criação de categorias de configurações com um mínimo de código adicional.  
  
-   Criar um VSPackage para fornecer um contêiner para a categoria Subclassificando o <xref:Microsoft.VisualStudio.Shell.Package> classe.  
  
-   Criar a categoria em si, derivando-lo partir o <xref:Microsoft.VisualStudio.Shell.DialogPage> classe.  
  
-   Conectar-se os dois com o <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute>.  
  
## <a name="support-for-settings-categories"></a>Suporte para categorias de configurações  
 O <xref:Microsoft.VisualStudio.Shell.Package> classe oferece suporte para a criação de categorias. O <xref:Microsoft.VisualStudio.Shell.DialogPage> classe implementa uma categoria. A implementação padrão de <xref:Microsoft.VisualStudio.Shell.DialogPage> oferece suas propriedades públicas para um usuário como uma categoria. Para obter mais informações, consulte [criar uma categoria de configurações](../extensibility/creating-a-settings-category.md).  
  
 O <xref:Microsoft.VisualStudio.Shell.DialogPage> implementos de classe <xref:Microsoft.VisualStudio.Shell.IProfileManager>, que fornece a persistência para páginas de opções e configurações do usuário. O <xref:Microsoft.VisualStudio.Shell.IProfileManager.LoadSettingsFromXml%2A> e <xref:Microsoft.VisualStudio.Shell.IProfileManager.SaveSettingsToXml%2A> métodos persistirem as configurações em um. vssettings que do arquivo [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] fornece como um <xref:Microsoft.VisualStudio.Shell.Interop.IVsSettingsReader> ou <xref:Microsoft.VisualStudio.Shell.Interop.IVsSettingsWriter>, respectivamente. O <xref:Microsoft.VisualStudio.Shell.IProfileManager.ResetSettings%2A> método redefine as configurações para seus valores padrão.  
  
 O <xref:Microsoft.VisualStudio.Shell.DialogPage> classe fornece uma implementação do <xref:Microsoft.VisualStudio.Shell.DialogPage.LoadSettingsFromXml%2A> método que lê os pares nome-valor do xml do feed e usa a reflexão para descobrir as propriedades públicas no <xref:Microsoft.VisualStudio.Shell.DialogPage> classe derivada. As propriedades que têm nomes que coincidem com os pares nome-valor recebem os valores correspondentes.  
  
 A implementação padrão de <xref:Microsoft.VisualStudio.Shell.DialogPage.SaveSettingsToXml%2A> usa a reflexão para descobrir as propriedades públicas no <xref:Microsoft.VisualStudio.Shell.DialogPage> classe derivada e grava os valores e nomes de propriedade no feed XML como pares nome-valor.  
  
### <a name="settings-category-registry-path"></a>Caminho do registro de categoria de configurações  
 O caminho do registro da categoria de configurações é determinado pela combinação <xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A>, o word, UserSettings, a categoria de configurações e o nome do ponto de configurações personalizadas. Os nomes da categoria de configurações e o ponto de configurações personalizadas são Unidos e separados por um caractere de sublinhado para formar o nome canônico não localizado, que aparece no registro. Por exemplo, se a categoria de configurações é "My Category", as configurações personalizadas do ponto de nome "My Settings" e o ApplicationRegistryRoot HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp, a categoria de configurações tem a chave do registro, HKEY_LOCAL Configurações de Category_My MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\UserSettings\My.  
  
> [!NOTE]
>  O nome canônico não aparece em uma interface de usuário (IU). Ele é usado para associar um nome legível com a categoria de configurações, muito parecido com um identificador programático (ProgID).  
  
### <a name="settings-category-attribute"></a>Atributo de categoria de configurações  
 O <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> determina o mapeamento das categorias de pontos de configurações personalizadas em de **Import and Export Settings Wizard** associando uma categoria com o VSPackage que fornece a ele. Considere o fragmento de código a seguir:  
  
 [!code-csharp[VSSDKSupportForSettingsCategories#1](../snippets/csharp/VS_Snippets_VSSDK/vssdksupportforsettingscategories/cs/vssdksupportforsettingscategoriespackage.cs#1)]
 [!code-vb[VSSDKSupportForSettingsCategories#1](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksupportforsettingscategories/vb/vssdksupportforsettingscategoriespackage.vb#1)]  
  
 ID do recurso 106 é mapeado para "My Category", 107 para "Minhas configurações" e 108 para "Várias opções". Isso declara que `MyPackage` fornece a categoria, minhas configurações Category_My. A categoria é fornecida pelos `OptionsPageGeneral` classe, que deve implementar <xref:Microsoft.VisualStudio.Shell.IProfileManager>. As configurações nesta categoria são as propriedades públicas do `OptionsPageGeneral` classe.  
  
 No **Import and Export Settings Wizard**, o ponto de configurações com o nome, minhas configurações. Quando o ponto de configurações é selecionado, a descrição **várias opções**, será exibida. O nome do ponto de configurações e a descrição são retirados do recursos de cadeia de caracteres localizada.  
  
## <a name="see-also"></a>Consulte também  
 [Criando uma página de opções](../extensibility/creating-an-options-page.md)   
 [Exemplos de VSSDK](../misc/vssdk-samples.md)   
 [Estado de VSPackage](../misc/vspackage-state.md)   
 [Personalizando configurações de desenvolvimento no Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3)