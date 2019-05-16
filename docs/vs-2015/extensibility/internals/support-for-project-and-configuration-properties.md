---
title: Suporte para o projeto e propriedades de configuração | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- project properties, supporting with Visual Studio SDK
- configuration properties, suppporting with Visual Studio SDK
ms.assetid: 9fcfaa0f-7b41-4b68-82ec-7a151dca5d7e
caps.latest.revision: 26
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ae770d36c0f030a060eccfe86bc3939dad9622d8
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65691878"
---
# <a name="support-for-project-and-configuration-properties"></a>Suporte para propriedades do projeto e de configuração
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

O **propriedades** janela no [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] o ambiente de desenvolvimento integrado (IDE) pode exibir propriedades do projeto e configuração. Você pode fornecer uma página de propriedades para seu próprio tipo de projeto para que o usuário pode definir propriedades de seu aplicativo.  
  
 Selecionando um nó do projeto no **Gerenciador de soluções** e, em seguida, clicando em **propriedades** sobre o **projeto** menu, você pode abrir uma caixa de diálogo que inclui o projeto e a configuração Propriedades. Na [!INCLUDE[csprcs](../../includes/csprcs-md.md)] e [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]e tipos derivados desses idiomas, essa caixa de diálogo é exibida como uma página com guias do projeto do [geral, ambiente, caixa de diálogo Opções](../../ide/reference/general-environment-options-dialog-box.md). Para obter mais informações, consulte [não está em compilação: Passo a passo: Expondo propriedades de configuração (c#) e de projeto](https://msdn.microsoft.com/d850d63b-25e2-4505-9f3d-eb038d7c1d0e).  
  
 A estrutura de pacote gerenciado para projetos (MPFProj) fornece classes auxiliares para criar e gerenciar o novo sistema de projeto. Você pode encontrar a fonte de instruções de código e compilação em [MPF de projetos – Visual Studio 2013](http://mpfproj12.codeplex.com/).  
  
## <a name="persistence-of-project-and-configuration-properties"></a>Persistência de projeto e propriedades de configuração  
 Propriedades do projeto e configuração são mantidas em um arquivo de projeto que tem uma extensão de nome de arquivo associado ao tipo de projeto, por exemplo,. csproj,. vbproj e .myproj. Projetos de linguagem normalmente usam um arquivo de modelo para gerar o arquivo de projeto. No entanto, há, na verdade, de várias maneiras para associar modelos e tipos de projeto. Para obter mais informações, consulte [NIB: Modelos do Visual Studio](https://msdn.microsoft.com/141fccaa-d68f-4155-822b-27f35dd94041) e [descrição do diretório de modelo (. Os arquivos de Vsdir)](../../extensibility/internals/template-directory-description-dot-vsdir-files.md).  
  
 Propriedades do projeto e configuração são criadas com a adição de itens para o arquivo de modelo. Essas propriedades, em seguida, estão disponíveis para qualquer projeto criado usando o tipo de projeto que usa esse modelo. [!INCLUDE[csprcs](../../includes/csprcs-md.md)] projetos e o MPFProj ambos usam o [não está em compilação: Visão geral do MSBuild](https://msdn.microsoft.com/b588fd73-a45b-4706-908f-cc131bccfbde) esquema para arquivos de modelo. Esses arquivos têm uma seção PropertyGroup para cada configuração. Propriedades de projetos normalmente são persistidas na primeira seção PropertyGroup, que tem um argumento de configuração definida como uma cadeia de caracteres nula.  
  
 O código a seguir mostra o início de um arquivo de projeto básico do MSBuild.  
  
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
  
 Nesse arquivo de projeto, `<Name>` e `<SchemaVersion>` são as propriedades do projeto e `<Optimize>` é uma propriedade de configuração.  
  
 É responsabilidade do projeto para persistir as propriedades do projeto e a configuração do arquivo de projeto.  
  
> [!NOTE]
> Um projeto pode otimizar persistência persistentes somente valores de propriedade que são diferentes dos seus valores padrão.  
  
## <a name="support-for-project-and-configuration-properties"></a>Suporte para propriedades do projeto e de configuração  
 O `Microsoft.VisualStudio.Package.SettingsPage` classe implementa as páginas de propriedades de projeto e a configuração. A implementação padrão de `SettingsPage` oferece propriedades públicas para um usuário em uma grade de propriedade genérica. O `Microsoft.VisualStudio.Package.HierarchyNode.GetPropertyPageGuids` método seleciona classes derivadas de `SettingsPage` para grades de propriedades do projeto. O `Microsoft.VisualStudio.Package.ProjectNode.GetConfigPropertyPageGuids` método seleciona classes derivadas de `SettingsPage` para grades de propriedades de configuração. O tipo de projeto deve substituir esses métodos para selecionar as páginas de propriedades apropriadas.  
  
 O `SettingsPage` classe e o `Microsoft.VisualStudio.Package.ProjectNode` classe oferecer esses métodos para persistir as propriedades do projeto e configuração:  
  
- `Microsoft.VisualStudio.Package.ProjectNode.GetProjectProperty` e `Microsoft.VisualStudio.Package.ProjectNode.SetProjectProperty` persistir as propriedades do projeto.  
  
- `Microsoft.VisualStudio.Package.SettingsPage.GetConfigProperty` e `Microsoft.VisualStudio.Package.SettingsPage.SetConfigProperty` persistir as propriedades de configuração.  
  
  > [!NOTE]
  > As implementações do `Microsoft.VisualStudio.Package.SettingsPage` e `Microsoft.VisualStudio.Package.ProjectNode` classes usam o `Microsoft.Build.BuildEngine` métodos (MSBuild) para obter e definir propriedades do projeto e configuração do arquivo de projeto.  
  
  A classe derivar de `SettingsPage` deve implementar `Microsoft.VisualStudio.Package.SettingsPage.ApplyChanges` e `Microsoft.VisualStudio.Package.SettingsPage.BindProperties` para persistir as propriedades do projeto ou a configuração do arquivo de projeto.  
  
## <a name="provideobjectattribute-and-registry-path"></a>ProvideObjectAttribute e o caminho do registro  
 As classes derivadas de `SettingsPage` são projetados para ser compartilhado entre os VSPackages. Para tornar possível para criar uma classe derivada de um VSPackage `SettingsPage`, adicione uma `Microsoft.VisualStudio.Shell.ProvideObjectAttribute` para uma classe derivada de `Microsoft.VisualStudio.Shell.Package`.  
  
 [!code-csharp[VSSDKSupportProjectConfigurationProperties#1](../../snippets/csharp/VS_Snippets_VSSDK/vssdksupportprojectconfigurationproperties/cs/vssdksupportprojectconfigurationpropertiespackage.cs#1)]
 [!code-vb[VSSDKSupportProjectConfigurationProperties#1](../../snippets/visualbasic/VS_Snippets_VSSDK/vssdksupportprojectconfigurationproperties/vb/vssdksupportprojectconfigurationpropertiespackage.vb#1)]  
  
 O VSPackage para o qual o atributo é anexado não é importante. Quando um VSPackage é registrado com [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], a id de classe (CLSID) de qualquer objeto que pode ser criado é registrada para que uma chamada para <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry.CreateInstance%2A> pode criá-lo.  
  
 O caminho do registro de um objeto que pode ser criado é determinado pela combinação <xref:Microsoft.VisualStudio.Shell.Package.UserRegistryRoot%2A>, o word, CLSID e o guid do tipo de objeto. Se `MyProjectPropertyPage` classe tem um guid de {3c693da2-5bca-49b3-bd95-ffe0a39dd723} e o UserRegistryRoot for HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0Exp, o caminho do registro seria HKEY_CURRENT_USER\Software\Microsoft\VisualStudio \8.0Exp\CLSID\\{3c693da2-5bca-49b3-bd95-ffe0a39dd723}.  
  
## <a name="project-and-configuration-property-attributes-and-layout"></a>Projeto e atributos de propriedade de configuração e o Layout  
 O <xref:System.ComponentModel.CategoryAttribute>, <xref:System.ComponentModel.DisplayNameAttribute>, e <xref:System.ComponentModel.DescriptionAttribute> atributos determinam o layout, rotulagem e a descrição das propriedades de projeto e configuração em uma página de propriedades genérico. Esses atributos determinar a categoria, nome de exibição e descrição da opção, respectivamente.  
  
> [!NOTE]
> Atributos equivalentes, SRCategory, LocDisplayName e SRDescription, usar os recursos de cadeia de caracteres para localização e são definidos no [MPF de projetos – Visual Studio 2013](http://mpfproj12.codeplex.com/).  
  
 Considere o fragmento de código a seguir:  
  
 [!code-csharp[VSSDKSupportProjectConfigurationProperties#2](../../snippets/csharp/VS_Snippets_VSSDK/vssdksupportprojectconfigurationproperties/cs/myprojectpropertypage.cs#2)]
 [!code-vb[VSSDKSupportProjectConfigurationProperties#2](../../snippets/visualbasic/VS_Snippets_VSSDK/vssdksupportprojectconfigurationproperties/vb/myprojectpropertypage.vb#2)]  
  
 O `MyConfigProp` propriedade configuração aparece na página de propriedades de configuração como **propriedade de configuração My** na categoria de **My Category**. Se a opção for selecionada, a descrição **minha descrição**, aparece no painel de descrição.  
  
## <a name="see-also"></a>Consulte também  
 [Não está em compilação: Passo a passo: Expondo o projeto e propriedades de configuração (c#)](https://msdn.microsoft.com/d850d63b-25e2-4505-9f3d-eb038d7c1d0e)   
 [Adicionando e removendo páginas de propriedades](../../extensibility/adding-and-removing-property-pages.md)   
 [Estado de VSPackage](../../misc/vspackage-state.md)   
 [Projetos](../../extensibility/internals/projects.md)   
 [NIB: Modelos do Visual Studio](https://msdn.microsoft.com/141fccaa-d68f-4155-822b-27f35dd94041)   
 [Arquivos de descrição do diretório do modelo (.Vsdir)](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)
