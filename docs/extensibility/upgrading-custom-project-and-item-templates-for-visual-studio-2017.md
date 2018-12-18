---
title: Atualizando o projeto personalizados e modelos de Item para Visual Studio de 2017 | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
ms.assetid: ad02477b-e101-4f32-aeb7-292bf95d5c2f
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: af60281e7211e7b16e86200c02aef791d26da274
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31143472"
---
# <a name="upgrading-custom-project-and-item-templates-for-visual-studio-2017"></a>Atualizando modelos de Item para Visual Studio de 2017 e projeto personalizados

A partir do Visual Studio de 2017, o Visual Studio descobre modelos de projeto e item que foram instalados de forma diferente de versões anteriores do Visual Studio por um .vsix ou um arquivo. msi. Se você possui extensões que usam modelos de item ou projeto personalizados, você precisa atualizar suas extensões. Este tópico explica o que você deve fazer.

Esta alteração afeta apenas de 2017 Visual Studio. Ele não afeta as versões anteriores do Visual Studio.

Se você quiser criar um modelo de projeto ou item como parte de uma extensão do VSIX, consulte [criando personalizar modelos de projeto e Item](../extensibility/creating-custom-project-and-item-templates.md).

## <a name="template-scanning"></a>Verificação de modelo

Em versões anteriores do Visual Studio, **devenv /setup** ou **/installvstemplates devenv** verificados no disco local para localizar modelos de projeto e item. A partir do Visual Studio de 2017, a verificação é executada apenas para o local de nível de usuário. O local de nível de usuário padrão é **%USERPROFILE%\Documents\\< versão do Visual Studio\>\Templates\\**. Esse local é usado para modelos gerados pelo **projeto** > **exportar modelos...**  comando, se o **importar automaticamente o modelo no Visual Studio** opção é selecionada no assistente.

Para outros locais (não-usuário), você deve incluir um arquivo de manifest(.vstman) que especifica o local e outras características do modelo. O arquivo .vstman é gerado junto com o arquivo. vstemplate usado para modelos. Se você instalar a extensão usando um .vsix, você pode fazer isso através da recompilação a extensão no Visual Studio de 2017. Mas se você usar um arquivo. msi, você precisa fazer as alterações manualmente. Para obter uma lista do que você precisa para fazer essas alterações, consulte **atualizações para extensões instaladas com um. MSI** mais adiante neste tópico.  
  
## <a name="how-to-update-a-vsix-extension-with-project-or-item-templates"></a>Como atualizar uma extensão do VSIX com modelos de Item ou projeto  

1.  Abra a solução no Visual Studio de 2017. Você será solicitado a atualizar o código. Clique em **OK**.  
  
2.  Após a conclusão da atualização, talvez seja necessário alterar a versão do destino da instalação. No projeto VSIX, abra o arquivo source.extension.vsixmanifest e selecione o **instalar destinos** guia. Se o **versão intervalo** campo é **[14.0]**, clique em **editar** e altere-o para incluir 2017 do Visual Studio. Por exemplo, você pode definir **[14.0,15.0]** para instalar a extensão do Visual Studio 2015 ou Visual Studio de 2017, ou em **[15.0]** para instalá-lo para apenas de 2017 Visual Studio.  
  
3.  Recompile o código.  
  
4.  Feche o Visual Studio.  
  
5.  Instale o VSIX.  
  
6.  Você pode testar a atualização, faça o seguinte:  
  
    1.  Verificação de alteração de arquivo é ativado pela seguinte chave do registro:  
  
         **reg adicionar hklm\software\microsoft\visualstudio\15.0\VSTemplate /v DisableTemplateScanning /t REG_DWORD /d 1 /reg:32**  
  
    2.  Depois que você adicionou a chave, execute **/installvstemplates devenv**.  
  
    3.  Reabra o Visual Studio. Você deve encontrar o modelo no local esperado.  
  
    > [!NOTE]
    >  Os modelos de projeto de extensibilidade do Visual Studio não estão disponíveis quando a chave do registro está presente. Você deve excluir a chave do registro (e execute novamente **/installvstemplates devenv**) para usá-los.  
  
## <a name="other-recommendations-for-deploying-project-and-item-templates"></a>Outras recomendações para implantação de modelos de projeto e Item  
  
-   Evite usar arquivos de modelo compactado. Compactado arquivos precisam ser descompactado para recuperar o conteúdo e recursos de modelo, assim eles estarão costlier usar. Em vez disso, você deve implantar modelos de projeto e item como arquivos individuais em seu próprio diretório para acelerar a inicialização do modelo. Para as extensões de VSIX, tarefas de build do SDK serão descompactados automaticamente qualquer modelo compactado ao criar o arquivo VSIX.  
  
-   Evite usar entradas de ID de recurso do pacote para o nome do modelo, a descrição, o ícone ou a visualização para evitar cargas de assembly desnecessárias de recursos durante a descoberta do modelo. Em vez disso, você pode usar manifestos localizados para criar uma entrada de modelo para cada localidade, que usa nomes localizados ou propriedades.  
  
-   Se você estiver incluindo modelos como itens de arquivo, geração de manifesto não pode fornecer os resultados esperados. Nesse caso, você precisará adicionar um manifesto gerado manualmente para o projeto do VSIX.  
  
## <a name="file-changes-in-project-and-item-templates"></a>Alterações de arquivo no projeto e modelos de Item  
Vamos mostrar os pontos de diferença entre o Visual Studio 2015 e as versões do Visual Studio de 2017 dos arquivos de modelo, para que você possa criar novos arquivos corretamente.  
  
 Aqui está o arquivo. vstemplate de projeto de padrão criado pelo Visual Studio 2015:  
  
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
  
 Aqui está o arquivo .vstman (você pode encontrá-lo no diretório de manifesto do projeto VSIX) que resultaram de recriação do projeto VSIX:  
  
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
  
 As informações fornecidas pelo [TemplateData](../extensibility/templatedata-element-visual-studio-templates.md) elemento permanece o mesmo. O  **\<VSTemplateContainer >** elemento aponta para o arquivo. vstemplate para o modelo associado.  
  
 Aqui está o arquivo. vstemplate de item de padrão criado pelo Visual Studio 2015:  
  
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
  
 Aqui está o arquivo .vstman (você pode encontrá-lo no diretório de manifesto do projeto VSIX) que resultaram de recriação do projeto VSIX:  
  
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
  
 As informações fornecidas pelo  **\<TemplateData >** elemento permanece o mesmo. O  **\<VSTemplateContainer >** elemento aponta para o arquivo. vstemplate para o modelo associado  
  
 Para obter mais informações sobre os diferentes elementos do arquivo .vstman, consulte [Visual Studio Template manifesto Schema Reference](../extensibility/visual-studio-template-manifest-schema-reference.md).  
  
## <a name="upgrades-for-extensions-installed-with-an-msi"></a>Atualizações para as extensões instaladas com um. MSI

Algumas extensões de MSI implantar modelos locais comuns do modelo, como o seguinte:

- **\<Diretório de instalação do Visual Studio > \Common7\IDE\\< ProjectTemplates/ItemTemplates >**

- **\<Diretório de instalação do Visual Studio > \Common7\IDE\Extensions\\< ExtensionName\>\\< projeto/ItemTemplates >**

Se sua extensão executa uma implantação de MSI, você precisa gerar o manifesto do modelo manualmente e certifique-se de que ele está incluído na configuração da extensão. Compare os exemplos de .vstman listados acima e [Visual Studio Template manifesto Schema Reference](../extensibility/visual-studio-template-manifest-schema-reference.md).

Você deve criar manifestos separados para modelos de projeto e item, e eles devem apontar para o modelo diretório raiz conforme especificado acima. Crie um manifesto por extensão e a localidade.

## <a name="see-also"></a>Consulte também

[Solucionando problemas de descoberta do modelo](troubleshooting-template-discovery.md)  
[Criando modelos personalizados de projeto e item](creating-custom-project-and-item-templates.md)