---
title: Suporte para propriedades de projeto e configuração | Microsoft Docs
description: Saiba como fornecer uma página de propriedades para seu próprio tipo de projeto no IDE do Visual Studio, que pode exibir o projeto e as propriedades estendidas de configuração.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project properties, supporting with Visual Studio SDK
- configuration properties, supporting with Visual Studio SDK
ms.assetid: 9fcfaa0f-7b41-4b68-82ec-7a151dca5d7e
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8d7e0065cf66f0d46680ab725537dbe4176928b1
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99953065"
---
# <a name="support-for-project-and-configuration-properties"></a>Suporte para propriedades do projeto e de configuração
A janela **Propriedades** no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ambiente de desenvolvimento integrado (IDE) pode exibir o projeto e as propriedades de configuração. Você pode fornecer uma página de propriedades para seu próprio tipo de projeto para que o usuário possa definir propriedades para seu aplicativo.

 Ao selecionar um nó de projeto no **Gerenciador de soluções** e, em seguida, clicar em **Propriedades** no menu **projeto** , você pode abrir uma caixa de diálogo que inclui propriedades de projeto e configuração. No [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] e no [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] , e os tipos de projeto derivados desses idiomas, essa caixa de diálogo aparece como uma página com guias na [caixa de diálogo geral, ambiente, opções](../../ide/reference/general-environment-options-dialog-box.md). Para obter mais informações, consulte [não em Build: passo a passos: expondo o projeto e as propriedades de configuração (C#)](/previous-versions/bb166517(v=vs.100)).

 A estrutura de pacote gerenciada para projetos (MPFProj) fornece classes auxiliares para criar e gerenciar o novo sistema de projeto. Você pode encontrar o código-fonte e as instruções de compilação em [MPF for projects-Visual Studio 2013](https://github.com/tunnelvisionlabs/MPFProj10).

## <a name="persistence-of-project-and-configuration-properties"></a>Persistência do projeto e das propriedades de configuração
 As propriedades de projeto e configuração são mantidas em um arquivo de projeto que tem qualquer extensão de nome de arquivo associada ao tipo de projeto, por exemplo,. csproj,. vbproj e. MyProj. Os projetos de linguagem normalmente usam um arquivo de modelo para gerar o arquivo de projeto. No entanto, há, na verdade, várias maneiras de associar modelos e tipos de projeto. Para obter mais informações, consulte [Descrição do diretório de modelos (. VSDir) arquivos](../../extensibility/internals/template-directory-description-dot-vsdir-files.md).

 As propriedades Project e Configuration são criadas adicionando itens ao arquivo de modelo. Essas propriedades ficam disponíveis para qualquer projeto criado usando o tipo de projeto que usa esse modelo. [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] os projetos e os MPFProj usam o esquema de [visão geral não está em compilação: MSBuild](/previous-versions/visualstudio/visual-studio-2008/ms171452(v=vs.90)) para arquivos de modelo. Esses arquivos têm uma seção PropertyGroup para cada configuração. As propriedades de projetos normalmente são mantidas na primeira seção PropertyGroup, que tem um argumento de configuração definido como uma cadeia de caracteres nula.

 O código a seguir mostra o início de um arquivo de projeto do MSBuild básico.

```
<Project MSBuildVersion="2.0" DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <PropertyGroup>
    <Configuration Condition=" '$(Configuration)' == '' ">Debug</Configuration>
    <Name>SomeProjectSix</Name>
    <SchemaVersion>2.0</SchemaVersion>
  </PropertyGroup>
  <PropertyGroup Condition=" '$(Configuration)' == 'Debug' ">
    <Optimize>false</Optimize>
  </PropertyGroup>
  <PropertyGroup Condition=" '$(Configuration)' == 'Release' ">
    <Optimize>true</Optimize>
```

 Neste arquivo de projeto, `<Name>` e `<SchemaVersion>` são propriedades do projeto, e `<Optimize>` é uma propriedade de configuração.

 É responsabilidade do projeto persistir o projeto e as propriedades de configuração do arquivo de projeto.

> [!NOTE]
> Um projeto pode otimizar a persistência mantendo apenas valores de propriedade que diferem de seus valores padrão.

## <a name="support-for-project-and-configuration-properties"></a>Suporte para propriedades do projeto e de configuração
 A `Microsoft.VisualStudio.Package.SettingsPage` classe implementa as páginas de propriedades de projeto e de configuração. A implementação padrão de `SettingsPage` oferece propriedades públicas para um usuário em uma grade de propriedades genérica. O `Microsoft.VisualStudio.Package.HierarchyNode.GetPropertyPageGuids` método seleciona classes derivadas de `SettingsPage` para grades de propriedades de projeto. O `Microsoft.VisualStudio.Package.ProjectNode.GetConfigPropertyPageGuids` método seleciona classes derivadas de `SettingsPage` para grades de propriedades de configuração. O tipo de projeto deve substituir esses métodos para selecionar as páginas de propriedades apropriadas.

 A `SettingsPage` classe e a `Microsoft.VisualStudio.Package.ProjectNode` classe oferecem esses métodos para persistir as propriedades de projeto e configuração:

- `Microsoft.VisualStudio.Package.ProjectNode.GetProjectProperty` e `Microsoft.VisualStudio.Package.ProjectNode.SetProjectProperty` manter as propriedades do projeto.

- `Microsoft.VisualStudio.Package.SettingsPage.GetConfigProperty` e `Microsoft.VisualStudio.Package.SettingsPage.SetConfigProperty` persiste as propriedades de configuração.

  > [!NOTE]
  > As implementações das `Microsoft.VisualStudio.Package.SettingsPage` `Microsoft.VisualStudio.Package.ProjectNode` classes e usam os `Microsoft.Build.BuildEngine` métodos (MSBuild) para obter e definir as propriedades de projeto e configuração do arquivo de projeto.

  A classe que você deriva `SettingsPage` deve implementar `Microsoft.VisualStudio.Package.SettingsPage.ApplyChanges` e `Microsoft.VisualStudio.Package.SettingsPage.BindProperties` manter as propriedades de projeto ou configuração do arquivo de projeto.

## <a name="provideobjectattribute-and-registry-path"></a>ProvideObjectAttribute e caminho do registro
 Classes derivadas de `SettingsPage` são projetadas para serem compartilhadas entre VSPackages. Para possibilitar que um VSPackage crie uma classe derivada de `SettingsPage` , adicione um `Microsoft.VisualStudio.Shell.ProvideObjectAttribute` a uma classe derivada de `Microsoft.VisualStudio.Shell.Package` .

 [!code-csharp[VSSDKSupportProjectConfigurationProperties#1](../../extensibility/internals/codesnippet/CSharp/support-for-project-and-configuration-properties_1.cs)]
 [!code-vb[VSSDKSupportProjectConfigurationProperties#1](../../extensibility/internals/codesnippet/VisualBasic/support-for-project-and-configuration-properties_1.vb)]

 O VSPackage ao qual o atributo está anexado não é importante. Quando um VSPackage é registrado com [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] , a ID de classe (CLSID) de qualquer objeto que pode ser criado é registrada para que uma chamada para <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry.CreateInstance%2A> possa criá-lo.

 O caminho do registro de um objeto que pode ser criado é determinado pela combinação da <xref:Microsoft.VisualStudio.Shell.Package.UserRegistryRoot%2A> palavra, do CLSID e do GUID do tipo de objeto. Se `MyProjectPropertyPage` a classe tiver um GUID de {3c693da2-5bca-49B3-bd95-ffe0a39dd723} e o UserRegistryRoot for HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0Exp, o caminho do registro será HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0Exp\CLSID\\ {3c693da2-5bca-49B3-bd95-ffe0a39dd723}.

## <a name="project-and-configuration-property-attributes-and-layout"></a>Layout e atributos de propriedade de configuração e projeto
 Os <xref:System.ComponentModel.CategoryAttribute> <xref:System.ComponentModel.DisplayNameAttribute> atributos,, e <xref:System.ComponentModel.DescriptionAttribute> determinam o layout, a rotulação e a descrição do projeto e das propriedades de configuração em uma página de propriedades genérica. Esses atributos determinam a categoria, o nome de exibição e a descrição da opção, respectivamente.

> [!NOTE]
> Atributos equivalentes, SRCategory, LocDisplayName e SRDescription, usam recursos de cadeia de caracteres para localização e são definidos em [MPF for projects-Visual Studio 2013](https://github.com/tunnelvisionlabs/MPFProj10).

 Considere o fragmento de código a seguir:

 [!code-vb[VSSDKSupportProjectConfigurationProperties#2](../../extensibility/internals/codesnippet/VisualBasic/support-for-project-and-configuration-properties_2.vb)]
 [!code-csharp[VSSDKSupportProjectConfigurationProperties#2](../../extensibility/internals/codesnippet/CSharp/support-for-project-and-configuration-properties_2.cs)]

 A `MyConfigProp` propriedade de configuração é exibida na página de propriedades de configuração como **minha propriedade** de configuração na categoria, **minha categoria**. Se a opção for selecionada, a descrição, **minha descrição**, aparecerá no painel Descrição.

## <a name="see-also"></a>Confira também
- [Adicionar e remover páginas de propriedade](../../extensibility/adding-and-removing-property-pages.md)
- [Projetos](../../extensibility/internals/projects.md)
- [Arquivos de descrição do diretório de modelo (.Vsdir)](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)