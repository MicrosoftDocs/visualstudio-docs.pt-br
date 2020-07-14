---
title: Elemento ProjectItem (modelos de projeto do Visual Studio) | Microsoft Docs
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#ProjectItem
helpviewer_keywords:
- ProjectItem element [Visual Studio project templates]
- <ProjectItem> element [Visual Studio project templates]
ms.assetid: 82879fbe-7756-42cd-9a07-c10edf5b4673
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 943f50823892e3cd942709bdcd4556b65c006b58
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85770306"
---
# <a name="projectitem-element-visual-studio-project-templates"></a>Elemento ProjectItem (modelos de projeto do Visual Studio)
Especifica um arquivo que está incluído no modelo de projeto.

> [!NOTE]
> O `ProjectItem` elemento aceita atributos diferentes, dependendo se o modelo é para um projeto ou um item. Este tópico explica o `ProjectItem` elemento para modelos de projeto. Para obter uma explicação do `ProjectItem` elemento para modelos de item, consulte [elemento ProjectItem (modelos de item do Visual Studio)](../extensibility/projectitem-element-visual-studio-item-templates.md).

 \<VSTemplate> \<TemplateContent>
 \<Project>
 \<ProjectItem>

## <a name="syntax"></a>Sintaxe

```
<ProjectItem
    TargetFileName="TargetFileName.ext"
    ReplaceParameters="true/false"
    OpenInEditor="true/false"
    OpenInWebBrowser="true/false"
    OpenInHelpBrowser="true/false"
    OpenOrder="Value">
        FileName.ext
</ProjectItem>
```

## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos

| Atributo | Descrição |
|---------------------| - |
| `TargetFileName` | Atributo opcional.<br /><br /> Especifica o nome e o caminho do item de projeto quando um projeto é criado a partir do modelo. Esse atributo é útil para criar uma estrutura de diretório diferente da estrutura de diretório no arquivo template *. zip* ou para usar a substituição de parâmetro para criar um nome de item. |
| `ReplaceParameters` | Atributo opcional.<br /><br /> Um valor booliano que especifica se o item tem valores de parâmetro que devem ser substituídos quando um projeto é criado a partir do modelo. O valor padrão é `false`. |
| `OpenInEditor` | Atributo opcional.<br /><br /> Um valor booliano que especifica se o item deve ser aberto em seu respectivo editor em [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] quando um projeto é criado a partir do modelo.<br /><br /> Os `OpenInWebBrowser` `OpenInHelpBrowser` atributos e são ignorados em um item com um `OpenInEditor` valor de `true` .<br /><br /> O valor padrão é `false`. |
| `OpenInWebBrowser` | Atributo opcional.<br /><br /> Um valor booliano que especifica se o item deve ser aberto no navegador da Web quando um projeto é criado a partir do modelo.<br /><br /> Somente arquivos HTML e arquivos de texto que são locais para o projeto podem ser abertos no navegador da Web. Não é possível abrir URLs externas com este atributo.<br /><br /> O valor padrão é `false`. |
| `OpenInHelpBrowser` | Atributo opcional.<br /><br /> Um valor booliano que especifica se o item deve ser aberto no Visualizador da ajuda quando um projeto é criado a partir do modelo.<br /><br /> Somente arquivos HTML e arquivos de texto que são locais para o projeto podem ser abertos no navegador da ajuda. Não é possível abrir URLs externas com este atributo.<br /><br /> O valor padrão é `false`. |
| `OpenOrder` | Atributo opcional.<br /><br /> Especifica um valor numérico que representa a ordem em que os itens serão abertos em seus respectivos editores. Todos os valores devem ser múltiplos de 10. Os itens com `OpenOrder` valores mais altos são abertos primeiro. |

### <a name="child-elements"></a>Elementos filho
 Nenhum.

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[Projeto](../extensibility/project-element-visual-studio-templates.md)|Especifica os arquivos ou diretórios a serem adicionados ao projeto.|

## <a name="text-value"></a>Valor de texto
 Um valor de texto é obrigatório.

 Um `string` que representa o nome ou o caminho para um arquivo no arquivo template *. zip* .

## <a name="remarks"></a>Comentários
 `ProjectItem`é um filho opcional de `Project` .

 O `TargetFileName` atributo pode ser usado para criar uma estrutura de diretório diferente da estrutura de diretório no arquivo template *. zip* . Por exemplo, se o arquivo *MyFile. vb* existir na raiz do arquivo *. zip* do modelo, mas você quiser que o arquivo seja colocado em um diretório chamado *CustomFiles* em todos os projetos criados a partir do modelo, você usaria o seguinte XML:

```xml
<ProjectItem TargetFileName="CustomFiles\MyFile.vb">MyFile.vb</ProjectItem>
```

 O `TargetFileName` atributo também pode ser usado para renomear arquivos que contêm caracteres internacionais em seus nomes de arquivo. Por exemplo, um arquivo *. zip* de modelo não pode conter nomes de arquivo com caracteres Unicode, portanto, o arquivo deve ser renomeado para que possa ser compactado em um arquivo *. zip* . O `TargetFileName` atributo pode ser usado para definir o nome do arquivo de volta para o nome de arquivo Unicode original.

 O `TargetFileName` atributo também pode ser usado para renomear arquivos com parâmetros. O procedimento a seguir explica como renomear o arquivo *MyFile. vb*, que existe no diretório raiz do arquivo template *. zip* , para um nome de arquivo com base no nome do projeto.

### <a name="to-rename-files-with-parameters"></a>Para renomear arquivos com parâmetros

1. Use o seguinte XML no arquivo *. vstemplate* :

   ```xml
   <ProjectItem TargetFileName="$safeprojectname$.vb">MyFile.vb</ProjectItem>
   ```

2. Abra o arquivo de projeto (*. vbproj* para um [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] projeto) em um editor de texto ou [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] .

3. Localize a linha no arquivo de projeto que se assemelha ao seguinte XML:

   ```xml
   <Compile Include="MyFile.vb">
   ```

4. Substitua a linha de código pelo seguinte XML:

   ```xml
   <Compile Include="$safeprojectname$.vb">
   ```

    Quando um projeto é criado com base nesse modelo, o nome do arquivo será baseado no nome que o usuário inseriu na caixa de diálogo **novo projeto** , com todos os caracteres e espaços não seguros removidos. Para obter mais informações, consulte [parâmetros de modelo](../ide/template-parameters.md).

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra os metadados de um modelo de projeto para um [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] aplicativo.

```
<VSTemplate Type="Project" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>My template</Name>
        <Description>A basic starter kit</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
    </TemplateData>
    <TemplateContent>
        <Project File="MyStarterKit.csproj">
            <ProjectItem ReplaceParameters="true">Form1.cs<ProjectItem>
            <ProjectItem>Form1.Designer.cs</ProjectItem>
            <ProjectItem>Program.cs</ProjectItem>
            <ProjectItem>Properties\AssemblyInfo.cs</ProjectItem>
            <ProjectItem>Properties\Resources.resx</ProjectItem>
            <ProjectItem>Properties\Resources.Designer.cs</ProjectItem>
            <ProjectItem>Properties\Settings.settings</ProjectItem>
            <ProjectItem>Properties\Settings.Designer.cs</ProjectItem>
        </Project>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>Confira também
- [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)
- [Criar modelos de projeto e de item](../ide/creating-project-and-item-templates.md)
- [Parâmetros de modelo](../ide/template-parameters.md)
- [Elemento ProjectItem (modelos de item do Visual Studio)](../extensibility/projectitem-element-visual-studio-item-templates.md)
