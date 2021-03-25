---
title: 'Nova geração de projeto: nos bastidores, parte dois | Microsoft Docs'
description: Veja detalhadamente o que acontece no IDE (ambiente de desenvolvimento integrado) do Visual Studio enquanto você cria seu próprio tipo de projeto (parte 2 de 2).
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio], new project dialog
- projects [Visual Studio], new project generation
ms.assetid: 73ce91d8-0ab1-4a1f-bf12-4d3c49c01e13
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e391ad66c9925dc68997ff610dc5d1556ddf09b2
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105063078"
---
# <a name="new-project-generation-under-the-hood-part-two"></a>Geração de novo projeto: Bastidores, parte dois

Em [nova geração de projeto: nos bastidores, parte 1](../../extensibility/internals/new-project-generation-under-the-hood-part-one.md) vimos como a caixa de diálogo **novo projeto** é populada. Vamos supor que você selecionou um **aplicativo do Windows em Visual C#**, preencheu as caixas de texto **nome** e **local** e clicou em OK.

## <a name="generating-the-solution-files"></a>Gerando os arquivos da solução
 Escolher um modelo de aplicativo direciona [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] para descompactar e abrir o arquivo. vstemplate correspondente e iniciar um modelo para interpretar os comandos XML nesse arquivo. Esses comandos criam projetos e itens de projeto na solução nova ou existente.

 O modelo desempacota os arquivos de origem, chamados de modelos de item, da mesma pasta. zip que contém o arquivo. vstemplate. O modelo copia esses arquivos para o novo projeto, personalizando-os adequadamente.

### <a name="template-parameter-replacement"></a>Substituição de parâmetro de modelo
 Quando o modelo copia um modelo de item para um novo projeto, ele substitui todos os parâmetros de modelo por cadeias de caracteres para personalizar o arquivo. Um parâmetro de modelo é um token especial que é precedido e seguido por um cifrão, por exemplo, $date $.

 Vamos examinar um modelo de item de projeto típico. Extraia e examine Program. cs na pasta Program Files\Microsoft Visual Studio 8\Common7\IDE\ProjectTemplates\CSharp\Windows\1033\WindowsApplication.zip.

```csharp
using System;
using System.Collections.Generic;
using System.Windows.Forms;

namespace $safeprojectname$
{
    static class Program
    {
        // source code deleted here for brevity
    }
}
```

Se você criar um novo projeto de aplicativo do Windows chamado Simple, o modelo substituirá o `$safeprojectname$` parâmetro pelo nome do projeto.

```csharp
using System;
using System.Collections.Generic;
using System.Windows.Forms;

namespace Simple
{
    static class Program
    {
        // source code deleted here for brevity
    }
}
```

 Para obter uma lista completa de parâmetros de modelo, consulte [parâmetros de modelo](../../ide/template-parameters.md).

## <a name="a-look-inside-a-vstemplate-file"></a>Uma olhada dentro de um. Arquivo VSTemplate
 Um arquivo. vstemplate básico tem esse formato

```xml
<VSTemplate Version="2.0.0"     xmlns="http://schemas.microsoft.com/developer/vstemplate/2005"     Type="Project">
    <TemplateData>
    </TemplateData>
    <TemplateContent>
    </TemplateContent>
</VSTemplate>
```

 Examinamos a \<TemplateData> seção na [nova geração do projeto: nos bastidores, Part One](../../extensibility/internals/new-project-generation-under-the-hood-part-one.md). As marcas nesta seção são usadas para controlar a aparência da caixa de diálogo **novo projeto** .

 As marcas na \<TemplateContent> seção controlam a geração de novos projetos e itens de projeto. Aqui está a \<TemplateContent> seção do arquivo cswindowsapplication. vstemplate na pasta \Program Files\Microsoft Visual Studio 8\Common7\IDE\ProjectTemplates\CSharp\Windows\1033\WindowsApplication.zip.

```xml
<TemplateContent>
  <Project File="WindowsApplication.csproj" ReplaceParameters="true">
    <ProjectItem ReplaceParameters="true"
      TargetFileName="Properties\AssemblyInfo.cs">
      AssemblyInfo.cs
    </ProjectItem>
    <ProjectItem TargetFileName="Properties\Resources.resx">
      Resources.resx
    </ProjectItem>
    <ProjectItem ReplaceParameters="true"       TargetFileName="Properties\Resources.Designer.cs">
      Resources.Designer.cs
    </ProjectItem>
    <ProjectItem TargetFileName="Properties\Settings.settings">
      Settings.settings
    </ProjectItem>
    <ProjectItem ReplaceParameters="true"       TargetFileName="Properties\Settings.Designer.cs">
      Settings.Designer.cs
    </ProjectItem>
    <ProjectItem ReplaceParameters="true" OpenInEditor="true">
      Form1.cs
    </ProjectItem>
    <ProjectItem ReplaceParameters="true">
      Form1.Designer.cs
    </ProjectItem>
    <ProjectItem ReplaceParameters="true">
      Program.cs
    </ProjectItem>
  </Project>
</TemplateContent>
```

 A \<Project> marca controla a geração de um projeto e a \<ProjectItem> marca controla a geração de um item de projeto. Se o parâmetro ReplaceParameters for true, o modelo personalizará todos os parâmetros de modelo no arquivo ou item de projeto. Nesse caso, todos os itens de projeto são personalizados, exceto para Settings. Settings.

 O parâmetro TargetFileName especifica o nome e o caminho relativo do arquivo ou item de projeto resultante. Isso permite que você crie uma estrutura de pastas para seu projeto. Se você não especificar esse argumento, o item de projeto terá o mesmo nome que o modelo de item de projeto.

 A estrutura resultante da pasta do aplicativo do Windows tem esta aparência:

 ![Captura de tela da estrutura de pastas de aplicativos do Windows para a solução ' simples ' no Gerenciador de Soluções do Visual Studio.](../../extensibility/internals/media/simplesolution.png)

 A primeira e única \<Project> marca no modelo lê:

```xml
<Project File="WindowsApplication.csproj" ReplaceParameters="true">
```

 Isso instrui o novo modelo de projeto a criar o arquivo de projeto simples. csproj copiando e personalizando o item de modelo WindowsApplication. csproj.

### <a name="designers-and-references"></a>Designers e referências
 Você pode ver na Gerenciador de Soluções que a pasta Propriedades está presente e contém os arquivos esperados. Mas e as referências de projeto e as dependências de arquivo de designer, como Resources. designer. cs a Resources. resx e Form1. designer. cs como Form1. cs?  Eles são configurados no arquivo. csproj simples quando ele é gerado.

 Aqui está o \<ItemGroup> de Simple. csproj que cria as referências do projeto:

```xml
<ItemGroup>
    <Reference Include="System" />
    <Reference Include="System.Data" />
    <Reference Include="System.Deployment" />
    <Reference Include="System.Drawing" />
    <Reference Include="System.Windows.Forms" />
    <Reference Include="System.Xml" />
</ItemGroup>
```

 Você pode ver que essas são as seis referências de projeto que aparecem na Gerenciador de Soluções. Aqui está uma seção de outra \<ItemGroup> . Muitas linhas de código foram excluídas para fins de clareza. Esta seção torna o Settings. designer. cs dependente de Settings. Settings:

```xml
<ItemGroup>
    <Compile Include="Properties\Settings.Designer.cs">
        <DependentUpon>Settings.settings</DependentUpon>
    </Compile>
</ItemGroup>
```

## <a name="see-also"></a>Confira também

- [Geração de novo projeto: Bastidores, parte um](../../extensibility/internals/new-project-generation-under-the-hood-part-one.md)
- [MSBuild](../../msbuild/msbuild.md)
