---
title: Elemento ProjectTemplateLink (modelos do Visual Studio) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-general
ms.topic: conceptual
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#ProjectTemplateLink
helpviewer_keywords:
- <ProjectTemplateLink> element [Visual Studio Templates]
- ProjectTemplateLink element [Visual Studio Templates]
ms.assetid: b0449111-8b48-45a1-a031-ea24b765e969
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: f0f2d810f2e6dff135230af71b10a823d22330e8
ms.sourcegitcommit: 9765b3fcf89375ca499afd9fc42cf4645b66a8a2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/20/2018
ms.locfileid: "46495967"
---
# <a name="projecttemplatelink-element-visual-studio-templates"></a>Elemento ProjectTemplateLink (modelos do Visual Studio)
Especifica o caminho para o *. vstemplate* arquivo de um projeto em um modelo multiprojeto.  
  
 \<VSTemplate >  
 \<TemplateContent >  
 \<ProjectCollection >  
 \<ProjectTemplateLink >  
-ou-  
\<VSTemplate >  
 \<TemplateContent >  
 \<ProjectCollection >  
 \<SolutionFolder >  
 \<ProjectTemplateLink >  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
<ProjectTemplateLink ProjectName="Name">  
    PathToTemplateFile  
</ProjectTemplateLink>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`ProjectName`|Atributo opcional.<br /><br /> Especifica o nome de cada projeto individual em um modelo de vários projetos. O **novo projeto** caixa de diálogo não é possível atribuir nomes a projetos individuais.|  
|`CopyParameters`|Permite que todas as variáveis no modelo de grupo principal sejam copiadas em cada um dos modelos vinculados.<br /><br /> Os parâmetros nos modelos vinculados têm um prefixo `"$ext_*$"`. Por exemplo, se no modelo de grupo pai o parâmetro `$projectname$` tem um valor **ExampleProject1**, quando o modelo vinculado obtém sua vez para ser executado, ele adquire um parâmetro `$ext_projectname$`, que é uma cópia do `$projectname$`parâmetro de modelo de grupo pai.<br /><br /> Isso permite que modelos vinculados compartilhem alguns parâmetros comuns, que podem ser convenientemente criados somente no modelo de grupo pai.<br /><br /> Esse atributo é opcional e padronizado automaticamente para `false` quando não é incluído.<br /><br /> Introduzido no Visual Studio 2013 Atualização 2. Para fazer referência a versão correta do produto, consulte [entregues no Visual Studio 2013 SDK atualização 2 de assemblies de referência](https://msdn.microsoft.com/library/42b65c3e-e42b-4c39-98c8-bea285f25ffb).|  
  
### <a name="child-elements"></a>Elementos filho  
 Nenhum.  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[ProjectCollection](../extensibility/projectcollection-element-visual-studio-templates.md)|Especifica a organização e o conteúdo de modelos de vários projetos.|  
|[SolutionFolder](../extensibility/solutionfolder-element-visual-studio-templates.md)|Agrupa projetos em modelos de vários projetos.|  
  
## <a name="text-value"></a>Valor de texto  
 Um valor de texto é obrigatório.  
  
 Esse texto Especifica o caminho para o *. vstemplate* arquivo do modelo.  
  
## <a name="remarks"></a>Comentários  
 Os modelos de vários projetos atuam como contêineres para dois ou mais projetos. O `ProjectTemplateLink` elemento é usado para especificar o local do *. vstemplate* arquivo para um dos projetos no modelo. O *. vstemplate* arquivo de um modelo multiprojeto contém um `ProjectTemplateLink` elemento para cada projeto no modelo. Para obter mais informações sobre modelos de vários projetos, consulte [como: criar modelos multiprojetos](../ide/how-to-create-multi-project-templates.md).  
  
## <a name="example"></a>Exemplo  
 Este exemplo mostra uma raiz multiprojeto simple *. vstemplate* arquivo. Neste exemplo, o modelo contém dois projetos, `My Windows Application` e `My Class Library`. O atributo `ProjectName` no elemento `ProjectTemplateLink` define o nome do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] para atribuir este projeto. Se o `ProjectName` atributo não existir, o nome da *. vstemplate* arquivo é usado como o nome do projeto.  
  
```  
<VSTemplate Version="3.0.0" Type="ProjectGroup"  
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">  
    <TemplateData>  
        <Name>Multi-Project Template Sample</Name>  
        <Description>An example of a multi-project template</Description>  
        <Icon>Icon.ico</Icon>  
        <ProjectType>VisualBasic</ProjectType>  
    </TemplateData>  
    <TemplateContent>  
        <ProjectCollection>  
            <ProjectTemplateLink ProjectName="My Windows Application">  
                WindowsApp\MyTemplate.vstemplate  
            </ProjectTemplateLink>  
            <ProjectTemplateLink ProjectName="My Class Library" CopyParameters="true">  
                ClassLib\MyTemplate.vstemplate  
            </ProjectTemplateLink>  
        </ProjectCollection>  
    </TemplateContent>  
</VSTemplate>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)   
 [Criar modelos de projeto e item](../ide/creating-project-and-item-templates.md)   
 [Como: criar modelos multiprojetos](../ide/how-to-create-multi-project-templates.md)