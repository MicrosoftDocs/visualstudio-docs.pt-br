---
title: Atualizar modelos de projeto e item personalizados para Visual Studio 2017
titleSuffix: ''
description: Saiba como atualizar seu projeto personalizado e modelo de item de versões anteriores do SDK do Visual Studio para uso com o Visual Studio 2017 e versões posteriores.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: ad02477b-e101-4f32-aeb7-292bf95d5c2f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: 0d07af0a00ab840df8a9af437bcddc427f606948
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112903054"
---
# <a name="upgrade-custom-project-and-item-templates-for-visual-studio-2017"></a>Atualizar o Modelos de Projeto e Item para Visual Studio 2017

A partir do Visual Studio 2017, o Visual Studio descobre modelos de projeto e item que foram instalados por um .vsix ou um .msi de uma maneira diferente das versões anteriores do Visual Studio. Se você tiver extensões que usam modelos de item ou projeto personalizados, será necessário atualizar suas extensões. Este artigo explica o que você deve fazer.

Essa alteração afeta apenas Visual Studio 2017. Ele não afeta as versões anteriores do Visual Studio.

Se você quiser criar um modelo de projeto ou item como parte de uma extensão do VSIX, consulte Criando modelos de projeto e [item personalizados.](../extensibility/creating-custom-project-and-item-templates.md)

## <a name="template-scanning"></a>Verificação de modelo

Nas versões anteriores do Visual Studio, **devenv /setup** ou **devenv /installvstemplates** digitalizado o disco local para encontrar modelos de projeto e item. A partir Visual Studio 2017, a verificação é executada apenas para o local no nível do usuário. O local padrão no nível do usuário é **%USERPROFILE%\Documents \\<Visual Studio versão \> \Templates \\**. Esse local será usado para modelos gerados pelo comando **Modelos** de Exportação de  >  **Projeto...** se a opção Importar automaticamente o modelo para Visual Studio for selecionada no assistente. 

Para outros locais (não usuário), você deve incluir um arquivo manifest(.vstman) que especifica o local e outras características do modelo. O arquivo .vstman é gerado junto com o arquivo .vstemplate usado para modelos. Se você instalar sua extensão usando um .vsix, poderá fazer isso recompilando a extensão no Visual Studio 2017. Mas se você usar um .msi, precisará fazer as alterações manualmente. Para ver uma lista do que você precisa fazer para fazer essas alterações, consulte  **Upgrades for Extensions Installed** with an .MSIlater nesta página.

## <a name="how-to-update-a-vsix-extension-with-project-or-item-templates"></a>Como atualizar uma extensão vsix com modelos de projeto ou item

1. Abra a solução no Visual Studio 2017. Você será solicitado a atualizar o código. Clique em **OK**.

2. Após a conclusão da atualização, talvez seja necessário alterar a versão do destino de instalação. No projeto VSIX, abra o arquivo source.extension.vsixmanifest e selecione a **guia Instalar Destinos.** Se o **campo Intervalo de** Versão for **[14.0]**, clique em **Editar** e altere-o para incluir Visual Studio 2017. Por exemplo, você pode defini-la como **[14.0,15.0]** para instalar a extensão no Visual Studio 2015 ou Visual Studio 2017 ou **para [15.0]** para instalá-la apenas no Visual Studio 2017.

3. Recompile o código.

4. Feche o Visual Studio.

5. Instale o VSIX.

6. Você pode testar a atualização fazendo o seguinte:

    1. A alteração de verificação de arquivo é ativada pela seguinte chave do Registro:

         **reg add hklm\software\microsoft\visualstudio\15.0\VSTemplate /v DisableTemplateScanning /t REG_DWORD /d 1 /reg:32**

    2. Depois de adicionar a chave, execute **devenv /installvstemplates**.

    3. Reabra Visual Studio. Você deve encontrar seu modelo no local esperado.

    > [!NOTE]
    > Os Visual Studio de projeto de extensibilidade não estão disponíveis quando a chave do Registro está presente. Você deve excluir a chave do Registro (e rerun **devenv /installvstemplates**) para usá-las.

## <a name="other-recommendations-for-deploying-project-and-item-templates"></a>Outras recomendações para implantar modelos de projeto e item

- Evite usar arquivos de modelo recortados. Os arquivos de modelo compactados precisam ser descompactados para recuperar recursos e conteúdo, portanto, eles serão mais oneros de usar. Em vez disso, você deve implantar modelos de projeto e item como arquivos individuais em seu próprio diretório para acelerar a inicialização do modelo. Para extensões VSIX, as tarefas de build do SDK descompocarão automaticamente qualquer modelo recortado durante a criação do arquivo VSIX.

- Evite usar entradas de ID de pacote/recurso para o nome do modelo, a descrição, o ícone ou a versão prévia para evitar cargas desnecessárias de assembly de recursos durante a descoberta do modelo. Em vez disso, você pode usar manifestos localizados para criar uma entrada de modelo para cada localidade, que usa nomes ou propriedades localizados.

- Se você estiver incluindo modelos como itens de arquivo, a geração de manifesto poderá não lhe dar os resultados esperados. Nesse caso, você terá que adicionar um manifesto gerado manualmente ao projeto VSIX.

## <a name="file-changes-in-project-and-item-templates"></a>Alterações de arquivo em modelos de projeto e item
Mostramos os pontos de diferença entre as versões Visual Studio 2015 e Visual Studio 2017 dos arquivos de modelo, para que você possa criar os novos arquivos corretamente.

 Este é o arquivo .vstemplate do projeto padrão criado pelo Visual Studio 2015:

```xml
<?xml version="1.0" encoding="utf-8"?>
<VSTemplate Version="3.0.0" Type="Project" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" xmlns:sdk="http://schemas.microsoft.com/developer/vstemplate-sdkextension/2010">
  <TemplateData>
    <Name>ProjectTemplate1</Name>
    <Description>ProjectTemplate1</Description>
    <Icon>ProjectTemplate1.ico</Icon>
    <ProjectType>CSharp</ProjectType>
    <RequiredFrameworkVersion>2.0</RequiredFrameworkVersion>
    <SortOrder>1000</SortOrder>
    <TemplateID>05b79cc9-2146-4716-a8e5-7e085cdd2221</TemplateID>
    <CreateNewFolder>true</CreateNewFolder>
    <DefaultName>ProjectTemplate1</DefaultName>
    <ProvideDefaultName>true</ProvideDefaultName>
  </TemplateData>
  <TemplateContent>
    <Project File="ProjectTemplate.csproj" ReplaceParameters="true">
      <ProjectItem ReplaceParameters="true" TargetFileName="Properties\AssemblyInfo.cs">AssemblyInfo.cs</ProjectItem>
      <ProjectItem ReplaceParameters="true" OpenInEditor="true">Class1.cs</ProjectItem>
    </Project>
  </TemplateContent>
</VSTemplate>

```

 Este é o arquivo .vstman (você pode encontrá-lo no diretório de manifesto do projeto VSIX) que resultou na recriação do projeto VSIX:

```xml
<VSTemplateManifest Version="1.0" Locale="1033" xmlns="http://schemas.microsoft.com/developer/vstemplatemanifest/2015">
  <VSTemplateContainer TemplateType="Project">
    <RelativePathOnDisk>CSharp\1033\ProjectTemplate1</RelativePathOnDisk>
    <TemplateFileName>ProjectTemplate1.vstemplate</TemplateFileName>
    <VSTemplateHeader>
      <TemplateData xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
        <Name>ProjectTemplate1</Name>
        <Description>ProjectTemplate1</Description>
        <Icon>ProjectTemplate1.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <RequiredFrameworkVersion>2.0</RequiredFrameworkVersion>
        <SortOrder>1000</SortOrder>
        <TemplateID>05b79cc9-2146-4716-a8e5-7e085cdd2221</TemplateID>
        <CreateNewFolder>true</CreateNewFolder>
        <DefaultName>ProjectTemplate1</DefaultName>
        <ProvideDefaultName>true</ProvideDefaultName>
      </TemplateData>
    </VSTemplateHeader>
  </VSTemplateContainer>
</VSTemplateManifest>

```

 As informações fornecidas pelo [elemento TemplateData](../extensibility/templatedata-element-visual-studio-templates.md) permanecem as mesmas. O **\<VSTemplateContainer>** elemento aponta para o arquivo .vstemplate para o modelo associado.

 Este é o arquivo .vstemplate do item padrão criado pelo Visual Studio 2015:

```xml
<?xml version="1.0" encoding="utf-8"?>
<VSTemplate Version="3.0.0" Type="Item" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" xmlns:sdk="http://schemas.microsoft.com/developer/vstemplate-sdkextension/2010">
  <TemplateData>
    <Name>ItemTemplate1</Name>
    <Description>ItemTemplate1</Description>
    <Icon>ItemTemplate1.ico</Icon>
    <TemplateID>bfeadf8e-a251-4109-b605-516b88e38c8d</TemplateID>
    <ProjectType>CSharp</ProjectType>
    <RequiredFrameworkVersion>2.0</RequiredFrameworkVersion>
    <NumberOfParentCategoriesToRollUp>1</NumberOfParentCategoriesToRollUp>
    <DefaultName>Class.cs</DefaultName>
  </TemplateData>
  <TemplateContent>
    <References>
      <Reference>
        <Assembly>System</Assembly>
      </Reference>
    </References>
    <ProjectItem ReplaceParameters="true">Class.cs</ProjectItem>
  </TemplateContent>
</VSTemplate>

```

 Este é o arquivo .vstman (você pode encontrá-lo no diretório de manifesto do projeto VSIX) que resultou na recriação do projeto VSIX:

```xml
<VSTemplateManifest Version="1.0" Locale="1033" xmlns="http://schemas.microsoft.com/developer/vstemplatemanifest/2015">
  <VSTemplateContainer TemplateType="Item">
    <RelativePathOnDisk>CSharp\1033\ItemTemplate1</RelativePathOnDisk>
    <TemplateFileName>ItemTemplate1.vstemplate</TemplateFileName>
    <VSTemplateHeader>
      <TemplateData xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
        <Name>ItemTemplate1</Name>
        <Description>ItemTemplate1</Description>
        <Icon>ItemTemplate1.ico</Icon>
        <TemplateID>bfeadf8e-a251-4109-b605-516b88e38c8d</TemplateID>
        <ProjectType>CSharp</ProjectType>
        <RequiredFrameworkVersion>2.0</RequiredFrameworkVersion>
        <NumberOfParentCategoriesToRollUp>1</NumberOfParentCategoriesToRollUp>
        <DefaultName>Class.cs</DefaultName>
      </TemplateData>
    </VSTemplateHeader>
  </VSTemplateContainer>
</VSTemplateManifest>
```

 As informações fornecidas pelo **\<TemplateData>** elemento permanecem as mesmas. O **\<VSTemplateContainer>** elemento aponta para o arquivo .vstemplate para o modelo associado

 Para obter mais informações sobre os diferentes elementos do arquivo .vstman, [consulte referência Visual Studio esquema de manifesto do modelo.](../extensibility/visual-studio-template-manifest-schema-reference.md)

## <a name="upgrades-for-extensions-installed-with-an-msi"></a>Atualizações para extensões instaladas com um .MSI

Algumas extensões baseadas em MSI implantam modelos em locais de modelo comuns, como os seguintes diretórios:

- **\<Visual Studio installation directory>\Common7\IDE \\<ProjectTemplates/ItemTemplates\>**

- **\<Visual Studio installation directory>\Common7\IDE\Extensions \\<ExtensionName \> \\<Project/ItemTemplates\>**

Se sua extensão executar uma implantação baseada em MSI, você precisará gerar o manifesto do modelo manualmente e garantir que ele seja incluído na configuração da extensão. Compare os exemplos do .vstman listados acima e a [referência Visual Studio esquema de manifesto do modelo.](../extensibility/visual-studio-template-manifest-schema-reference.md)

Crie manifestos separados para modelos de projeto e item e eles devem apontar para o diretório de modelo raiz, conforme especificado acima. Crie um manifesto por extensão e localidade.

## <a name="see-also"></a>Confira também

- [Solução de problemas de descoberta de modelo](troubleshooting-template-discovery.md)
- [Criando modelos de projeto e item personalizados](creating-custom-project-and-item-templates.md)
