---
title: Atualizar modelos de projeto e item personalizados para o Visual Studio 2017
titleSuffix: ''
description: Saiba como atualizar seu projeto personalizado e modelo de item de versões anteriores do SDK do Visual Studio para uso com o Visual Studio 2017 e versões posteriores.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: ad02477b-e101-4f32-aeb7-292bf95d5c2f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: 8442e24bf971b8a2a0bcf5baeeb397e4646ba766
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060270"
---
# <a name="upgrade-custom-project-and-item-templates-for-visual-studio-2017"></a>Atualizar Modelos de Projeto e Item para Visual Studio personalizado 2017

A partir do Visual Studio 2017, o Visual Studio descobre modelos de projeto e item que foram instalados por um. vsix ou um. msi de uma maneira diferente para versões anteriores do Visual Studio. Se você possui extensões que usam modelos de projeto ou item personalizados, você precisa atualizar suas extensões. Este artigo explica o que você deve fazer.

Essa alteração afeta apenas o Visual Studio 2017. Ele não afeta as versões anteriores do Visual Studio.

Se você quiser criar um modelo de projeto ou item como parte de uma extensão do VSIX, consulte [criando projetos personalizados e modelos de item](../extensibility/creating-custom-project-and-item-templates.md).

## <a name="template-scanning"></a>Verificação de modelo

Nas versões anteriores do Visual Studio, **devenv/setup** ou **devenv/InstallVSTemplates** verificou o disco local para localizar modelos de projeto e item. A partir do Visual Studio 2017, a verificação é executada somente para o local no nível do usuário. O local de nível de usuário padrão é **%USERPROFILE%\Documents \\<Visual Studio \> versão \\ \Templates**. Esse local é usado para modelos gerados pelo comando exportar modelos de **projeto**  >  **...** , se a opção **importar automaticamente o modelo para o Visual Studio** estiver selecionada no assistente.

Para outros locais (não de usuário), você deve incluir um arquivo de manifesto (. vstman) que especifica o local e outras características do modelo. O arquivo. vstman é gerado junto com o arquivo. vstemplate usado para modelos. Se você instalar a extensão usando um. vsix, poderá fazer isso recompilando a extensão no Visual Studio 2017. Mas se você usar um. msi, precisará fazer as alterações manualmente. Para obter uma lista do que você precisa fazer para fazer essas alterações, consulte  **atualizações para extensões instaladas com um. MSI** mais adiante nesta página.

## <a name="how-to-update-a-vsix-extension-with-project-or-item-templates"></a>Como atualizar uma extensão do VSIX com modelos de projeto ou item

1. Abra a solução no Visual Studio 2017. Você será solicitado a atualizar o código. Clique em **OK**.

2. Após a conclusão da atualização, talvez seja necessário alterar a versão do destino de instalação. No projeto VSIX, abra o arquivo Source. Extension. vsixmanifest e selecione a guia **instalar destinos** . Se o campo **intervalo de versão** for **[14,0]**, clique em **Editar** e altere-o para incluir o Visual Studio 2017. Por exemplo, você pode defini-lo como **[14.0, 15.0]** para instalar a extensão para o visual Studio 2015 ou o visual Studio 2017 ou para **[15,0]** para instalá-lo no apenas Visual Studio 2017.

3. Recompile o código.

4. Feche o Visual Studio.

5. Instale o VSIX.

6. Você pode testar a atualização fazendo o seguinte:

    1. A alteração de verificação de arquivo é ativada pela seguinte chave do registro:

         **REG add hklm\software\microsoft\visualstudio\15.0\VSTemplate/v DisableTemplateScanning/t REG_DWORD/d 1/Reg: 32**

    2. Depois de adicionar a chave, execute **devenv/InstallVSTemplates**.

    3. Reabra o Visual Studio. Você deve encontrar seu modelo no local esperado.

    > [!NOTE]
    > Os modelos de projeto de extensibilidade do Visual Studio não estão disponíveis quando a chave do registro está presente. Você deve excluir a chave do registro (e executar novamente **devenv/InstallVSTemplates**) para usá-las.

## <a name="other-recommendations-for-deploying-project-and-item-templates"></a>Outras recomendações para implantar modelos de projeto e item

- Evite usar arquivos de modelo compactados. Os arquivos de modelo zipados precisam ser descompactados para recuperar recursos e conteúdo, portanto, eles serão mais carasdos a usar. Em vez disso, você deve implantar modelos de projeto e item como arquivos individuais em seu próprio diretório para acelerar a inicialização do modelo. Para as extensões do VSIX, as tarefas de compilação do SDK descompactam automaticamente qualquer modelo compactado ao criar o arquivo VSIX.

- Evite usar entradas de ID de pacote/recurso para o nome do modelo, a descrição, o ícone ou a visualização para evitar cargas desnecessárias de assembly de recursos durante a descoberta de modelo. Em vez disso, você pode usar manifestos localizados para criar uma entrada de modelo para cada localidade, que usa nomes ou propriedades localizadas.

- Se você estiver incluindo modelos como itens de arquivo, a geração de manifesto pode não fornecer os resultados esperados. Nesse caso, você precisará adicionar um manifesto gerado manualmente ao projeto VSIX.

## <a name="file-changes-in-project-and-item-templates"></a>Alterações de arquivo em modelos de projeto e item
Mostramos os pontos de diferença entre as versões do Visual Studio 2015 e do Visual Studio 2017 dos arquivos de modelo, para que você possa criar os novos arquivos corretamente.

 Este é o arquivo. vstemplate de projeto padrão criado pelo Visual Studio 2015:

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

 Aqui está o arquivo. vstman (você pode encontrá-lo no diretório de manifesto do projeto VSIX) que resultou da recriação do projeto VSIX:

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

 As informações fornecidas pelo elemento [TemplateData](../extensibility/templatedata-element-visual-studio-templates.md) permanecem as mesmas. O **\<VSTemplateContainer>** elemento aponta para o arquivo. vstemplate para o modelo associado.

 Este é o arquivo. vstemplate de item padrão criado pelo Visual Studio 2015:

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

 Aqui está o arquivo. vstman (você pode encontrá-lo no diretório de manifesto do projeto VSIX) que resultou da recriação do projeto VSIX:

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

 As informações fornecidas pelo **\<TemplateData>** elemento permanecem as mesmas. O **\<VSTemplateContainer>** elemento aponta para o arquivo. vstemplate para o modelo associado

 Para obter mais informações sobre os diferentes elementos do arquivo. vstman, consulte [referência de esquema de manifesto de modelo do Visual Studio](../extensibility/visual-studio-template-manifest-schema-reference.md).

## <a name="upgrades-for-extensions-installed-with-an-msi"></a>Atualizações para extensões instaladas com um. MSI

Algumas extensões baseadas em MSI implantam modelos em locais de modelo comuns, como os seguintes diretórios:

- **\<Visual Studio installation directory>\Common7\IDE \\<ProjectTemplates/meus modelos\>**

- **\<Visual Studio installation directory>\Common7\IDE\Extensions \\<extensionname \> \\<projeto/modelos\>**

Se sua extensão executar uma implantação baseada em MSI, você precisará gerar o manifesto do modelo manualmente e verificar se ele está incluído na configuração da extensão. Compare os exemplos de. vstman listados acima e a [referência de esquema de manifesto de modelo do Visual Studio](../extensibility/visual-studio-template-manifest-schema-reference.md).

Crie manifestos separados para modelos de projeto e item, e eles devem apontar para o diretório de modelo raiz, conforme especificado acima. Crie um manifesto por extensão e localidade.

## <a name="see-also"></a>Confira também

- [Solução de problemas de descoberta de modelo](troubleshooting-template-discovery.md)
- [Criando modelos personalizados de projeto e item](creating-custom-project-and-item-templates.md)
