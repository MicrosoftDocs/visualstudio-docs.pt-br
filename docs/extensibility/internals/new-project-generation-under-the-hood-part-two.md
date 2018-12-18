---
title: 'Nova geração de projeto: Nos bastidores, parte 2 | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio], new project dialog
- projects [Visual Studio], new project generation
ms.assetid: 73ce91d8-0ab1-4a1f-bf12-4d3c49c01e13
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 38f2a4a84c6223c2e195c3d703f52d7fd5b18c86
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49837523"
---
# <a name="new-project-generation-under-the-hood-part-two"></a>Geração de novo projeto: nos bastidores, Parte dois
Na [nova geração de projeto: Under the Hood, parte 1](../../extensibility/internals/new-project-generation-under-the-hood-part-one.md) vimos como o **novo projeto** caixa de diálogo caixa é preenchida. Vamos supor que você selecionou uma **Visual c# Windows Application**, preenchido a **nome** e **local** caixas de texto e Okey clicado.  
  
## <a name="generating-the-solution-files"></a>Gerar os arquivos de solução  
 Escolher um modelo de aplicativo direciona [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] para descompactar e abrir o arquivo. vstemplate correspondente e para iniciar um modelo para interpretar os comandos XML neste arquivo. Esses comandos criam projetos e itens de projeto na solução nova ou existente.  
  
 O modelo desempacota os arquivos de origem, chamados de modelos de item, da mesma pasta. zip que contém o arquivo. vstemplate. O modelo copia esses arquivos para o novo projeto, personalizá-las adequadamente.  
  
### <a name="template-parameter-replacement"></a>Substituição de parâmetro de modelo  
 Quando o modelo copia um modelo de item para um novo projeto, ele substitui quaisquer parâmetros de modelo com cadeias de caracteres para personalizar o arquivo. Um parâmetro de modelo é um símbolo especial que é precedido e seguido por um sinal de cifrão, por exemplo, $ $date.  
  
 Vamos examinar um modelo de item de projeto comum. Extrair e examine o Program.cs na pasta Program Files\Microsoft Visual Studio 8\Common7\IDE\ProjectTemplates\CSharp\Windows\1033\WindowsApplication.zip.  
  
```  
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
  
 Se você criar um novo projeto de aplicativo do Windows chamado simples, o modelo substitui o `$safeprojectname$` parâmetro com o nome do projeto.  
  
```  
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
  
 Para ver uma lista completa dos parâmetros de modelo, consulte [Parâmetros de Modelo](../../ide/template-parameters.md).  
  
## <a name="a-look-inside-a-vstemplate-file"></a>Uma olhada dentro de um. Arquivo VSTemplate  
 Um arquivo. vstemplate básico tem este formato  
  
```  
<VSTemplate Version="2.0.0"     xmlns="http://schemas.microsoft.com/developer/vstemplate/2005"     Type="Project">  
    <TemplateData>  
    </TemplateData>  
    <TemplateContent>  
    </TemplateContent>  
</VSTemplate>  
```  
  
 Analisamos o \<TemplateData > seção de [nova geração de projeto: Under the Hood, parte 1](../../extensibility/internals/new-project-generation-under-the-hood-part-one.md). As marcas nesta seção são usadas para controlar a aparência do **novo projeto** caixa de diálogo.  
  
 As marcas no \<TemplateContent > seção controle a geração de novos projetos e itens de projeto. Aqui está o \<TemplateContent > seção do arquivo na pasta \Program Visual Studio 8\Common7\IDE\ProjectTemplates\CSharp\Windows\1033\WindowsApplication.zip cswindowsapplication.vstemplate.  
  
```  
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
  
 O \<Project > marca controla a geração de um projeto e o \<ProjectItem > marca controla a geração de um item de projeto. Se o parâmetro ReplaceParameters for true, o modelo irá personalizar todos os parâmetros de modelo no arquivo de projeto ou item. Nesse caso, todos os itens de projeto são personalizados, exceto para Settings.  
  
 O parâmetro de TargetFileName Especifica o nome e caminho relativo do arquivo resultante do projeto ou item. Isso permite que você crie uma estrutura de pastas para o seu projeto. Se você não especificar esse argumento, o item de projeto terá o mesmo nome que o modelo de item de projeto.  
  
 A estrutura de pasta de aplicativo Windows resultante tem esta aparência:  
  
 ![SimpleSolution](../../extensibility/internals/media/simplesolution.png "SimpleSolution")  
  
 O primeiro e único \<projeto > marca nas leituras de modelo:  
  
```  
<Project File="WindowsApplication.csproj" ReplaceParameters="true">  
```  
  
 Isso instrui o modelo novo projeto para criar o arquivo de projeto Simple.csproj copiando e personalizando o windowsapplication.csproj de item de modelo.  
  
### <a name="designers-and-references"></a>Designers e referências  
 Você pode ver no Gerenciador de soluções que a pasta de propriedades está presente e contém os arquivos esperados. Mas e quanto ao projeto referencia e dependências de arquivo de designer, como Resources.Designer.cs para Resources e Form1.Designer.cs para Form1.cs?  Eles são definidos no arquivo Simple.csproj quando ele é gerado.  
  
 Aqui está o \<ItemGroup > de Simple.csproj que cria as referências do projeto:  
  
```  
<ItemGroup>  
    <Reference Include="System" />  
    <Reference Include="System.Data" />  
    <Reference Include="System.Deployment" />  
    <Reference Include="System.Drawing" />  
    <Reference Include="System.Windows.Forms" />  
    <Reference Include="System.Xml" />  
</ItemGroup>  
```  
  
 Você pode ver que essas são as referências do seis projeto que aparecem no Gerenciador de soluções. Aqui está uma seção de outro \<ItemGroup >. Número de linhas de código ter sido excluído por motivos de clareza. Esta seção faz Settings.Designer.cs dependente do Settings:  
  
```  
<ItemGroup>  
    <Compile Include="Properties\Settings.Designer.cs">  
        <DependentUpon>Settings.settings</DependentUpon>  
    </Compile>  
</ItemGroup>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Nova geração de projeto: nos bastidores, parte 1](../../extensibility/internals/new-project-generation-under-the-hood-part-one.md)  
 [MSBuild](../../msbuild/msbuild.md)