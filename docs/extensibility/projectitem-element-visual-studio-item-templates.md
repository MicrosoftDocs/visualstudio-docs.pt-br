---
title: Elemento ProjectItem (modelos de item do Visual Studio) | Microsoft Docs
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#ProjectItem
helpviewer_keywords:
- <ProjectItem> element [Visual Studio item templates]
- ProjectItem element [Visual Studio item templates]
ms.assetid: 9ed94112-0c38-49df-b728-0dd2d0d1eb47
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 885d0fbb50204f23a30fa43c1ffad45c9d67f829
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85770724"
---
# <a name="projectitem-element-visual-studio-item-templates"></a>Elemento ProjectItem (modelos de item do Visual Studio)
Especifica um arquivo que está incluído no modelo de item.

> [!NOTE]
> O `ProjectItem` elemento aceita atributos diferentes, dependendo se o modelo é para um projeto ou um item. Este tópico explica o `ProjectItem` elemento para item. Para obter uma explicação do `ProjectItem` elemento para modelos de projeto, consulte [elemento ProjectItem (modelos de projeto do Visual Studio)](../extensibility/projectitem-element-visual-studio-project-templates.md).

 \<VSTemplate> \<TemplateContent>
 \<ProjectItem>

## <a name="syntax"></a>Sintaxe

```
<ProjectItem
    SubType="Form/Component/CustomControl/UserControl"
    CustomTool="string"
    ItemType="string"
    ReplaceParameters="true/false"
    TargetFileName="TargetFileName.ext">
        FileName.ext
</ProjectItem>
```

## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos

| Atributo | Descrição |
|---------------------| - |
| `SubType` | Atributo opcional.<br /><br /> Especifica o subtipo de um item em um modelo de item de vários arquivos. Esse valor é usado para determinar o editor que [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] será usado para abrir o item. |
| `CustomTool` | Atributo opcional.<br /><br /> Define o CustomTool para o item no arquivo de projeto. |
| `ItemType` | Atributo opcional.<br /><br /> Define o ItemType para o item no arquivo de projeto. |
| `ReplaceParameters` | Atributo opcional.<br /><br /> Um valor booliano que especifica se o item tem valores de parâmetro que devem ser substituídos quando um projeto é criado a partir do modelo. O valor padrão é `false`. |
| `TargetFileName` | Atributo opcional.<br /><br /> Especifica o nome do item que é criado a partir do modelo. Esse atributo é útil para usar a substituição de parâmetro para criar um nome de item. |

### <a name="child-elements"></a>Elementos filho
 Nenhum.

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[TemplateContent](../extensibility/templatecontent-element-visual-studio-templates.md)|Especifica o conteúdo do modelo.|

## <a name="text-value"></a>Valor de texto
 Um valor de texto é obrigatório.

 Um `string` que representa o nome de um arquivo no arquivo *. zip* de modelo.

## <a name="remarks"></a>Comentários
 `ProjectItem`é um filho opcional de `TemplateContent` .

 O `TargetFileName` atributo pode ser usado para renomear arquivos com parâmetros. Por exemplo, se o arquivo *MyFile. vb* existir no diretório raiz do arquivo *. zip* do modelo, mas você quiser que o arquivo seja nomeado com base no nome do arquivo fornecido pelo usuário na caixa de diálogo **Adicionar novo item** , você usaria o seguinte XML:

```xml
<ProjectItem TargetFileName="$fileinputname$.vb">MyFile.vb</ProjectItem>
```

 Quando um item for criado a partir desse modelo, o nome do arquivo será baseado no nome que o usuário inseriu na caixa de diálogo **Adicionar novo item** . Isso é útil ao criar modelos de item de vários arquivos. Para obter mais informações, consulte [como: criar modelos de item de vários arquivos](../ide/how-to-create-multi-file-item-templates.md) e [parâmetros de modelo](../ide/template-parameters.md).

## <a name="example"></a>Exemplo
 O exemplo a seguir ilustra os metadados para o modelo de item padrão para uma [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] classe.

```
<VSTemplate Type="Item" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>MyClass</Name>
        <Description>My custom C# class.</Description>
        <Icon>Icon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <DefaultName>MyClass.cs</DefaultName>
    </TemplateData>
    <TemplateContent>
        <ProjectItem ReplaceParameters="true">MyClass.cs</ProjectItem>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>Confira também
- [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)
- [Criando modelos de projeto e item](../ide/creating-project-and-item-templates.md)
- [Como criar modelos de item multiarquivos](../ide/how-to-create-multi-file-item-templates.md)
- [Parâmetros de modelo](../ide/template-parameters.md)
