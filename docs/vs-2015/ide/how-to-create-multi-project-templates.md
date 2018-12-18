---
title: Como criar modelos multiprojeto | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Visual Studio templates, creating multi-project templates
- project templates, creating multi-project templates
- multi-project templates
ms.assetid: 8c7f7065-137e-40ad-868d-37e007270efd
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: eee52a4f77c7d3a07b237f01877c5cba30e53900
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49950843"
---
# <a name="how-to-create-multi-project-templates"></a>Como criar modelos multiprojeto
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Os modelos de vários projetos atuam como contêineres para dois ou mais projetos. Quando um projeto baseado em um modelo multiprojeto é criado com base na caixa de diálogo **Novo Projeto**, todo projeto no modelo é adicionado à solução.  
  
 Um modelo multiprojeto deve incluir os itens a seguir, compactados em um arquivo .zip:  
  
- Um arquivo .vstemplate raiz para todo o modelo multiprojeto. Esse arquivo .vstemplate raiz contém os metadados que a caixa de diálogo **Novo Projeto** exibe e especifica onde localizar os arquivos .vstemplate para os projetos nesse modelo. Esse arquivo deve estar localizado na raiz do arquivo .zip.  
  
- Uma ou mais pastas que contêm os arquivos necessários para um modelo de projeto completo. Isso inclui todos os arquivos de código do projeto e um arquivo .vstemplate do projeto.  
  
  Por exemplo, um arquivo .zip de modelo multiprojeto com dois projetos poderia ter os seguintes arquivos e diretórios:  
  
  MultiProjectTemplate.vstemplate  
  
  \Project1\Project1.vstemplate  
  
  \Project1\Project1.vbproj  
  
  \Project1\Class.vb  
  
  \Project2\Project2.vstemplate  
  
  \Project2\Project2.vbproj  
  
  \Project2\Class.vb  
  
  O arquivo .vstemplate raiz para um modelo multiprojeto difere de um modelo de projeto único das seguintes maneiras:  
  
- O atributo `Type` do elemento `VSTemplate` contém o valor `ProjectGroup`. Por exemplo:  
  
  ```  
  <VSTemplate Version="2.0.0" Type="ProjectGroup"  
      xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">  
  ```  
  
- O elemento `TemplateContent` contém um elemento `ProjectCollection` que tem um ou mais elementos `ProjectTemplateLink` que definem os caminhos para os arquivos .vstemplate dos projetos incluídos. Por exemplo:  
  
  ```  
  <TemplateContent>  
      <ProjectCollection>  
          <ProjectTemplateLink>  
              Project1\Project1.vstemplate  
          </ProjectTemplateLink>  
          <ProjectTemplateLink>  
              Project2\Project2.vstemplate  
          </ProjectTemplateLink>  
      </ProjectCollection>  
  </TemplateContent>  
  ```  
  
  Modelos multiprojeto também se comportam de maneira diferente dos modelos normais. Modelos multiprojeto têm as seguintes características exclusivas:  
  
- Projetos individuais em um modelo multiprojeto não podem ter nomes atribuídos pela caixa de diálogo **Novo Projeto**. Em vez disso, use o atributo `ProjectName` no elemento `ProjectTemplateLink` para especificar o nome de cada projeto. Para obter mais informações, consulte o primeiro exemplo na seção a seguir.  
  
- Modelos multiprojeto podem conter projetos escritos em diferentes linguagens, mas o próprio modelo inteiro só pode ser colocado em uma categoria usando o elemento `ProjectType`.  
  
### <a name="to-create-a-multi-project-template"></a>Para criar um modelo multiprojeto  
  
1.  Crie os projetos a serem incluídos no modelo multiprojeto.  
  
2.  Crie arquivos .vstemplate para cada projeto. Para obter mais informações, consulte [Como criar modelos de projeto](../ide/how-to-create-project-templates.md).  
  
3.  Crie um arquivo .vstemplate raiz para conter os metadados do modelo multiprojeto. Para obter mais informações, consulte o primeiro exemplo na seção a seguir.  
  
4.  Selecione os arquivos e pastas a serem incluídos em seu modelo, clique com o botão direito do mouse na seleção, clique em **Enviar Para** e, em seguida, clique em **Pasta Compactada (Zipada)**. Esses arquivos e pastas estão compactados em um arquivo .zip.  
  
5.  Coloque o arquivo de modelo .zip no diretório de modelo de projeto [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. Por padrão, esse diretório é \Meus Documentos\Visual Studio *Versão*\Templates\ProjectTemplates\\.  
  
## <a name="example"></a>Exemplo  
 Esse exemplo mostra um arquivo .vstemplate raiz multiprojeto básico. Neste exemplo, o modelo contém dois projetos, `My Windows Application` e `My Class Library`. O atributo `ProjectName` no elemento `ProjectTemplateLink` define o nome do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para atribuir este projeto. Se o atributo `ProjectName` não existir, o nome do arquivo .vstemplate é usado como o nome do projeto.  
  
```  
<VSTemplate Version="2.0.0" Type="ProjectGroup"  
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
            <ProjectTemplateLink ProjectName="My Class Library">  
                ClassLib\MyTemplate.vstemplate  
            </ProjectTemplateLink>  
        </ProjectCollection>  
    </TemplateContent>  
</VSTemplate>  
```  
  
## <a name="example"></a>Exemplo  
 Esse exemplo usa o elemento `SolutionFolder` para dividir os projetos em dois grupos, `Math Classes` e `Graphics Classes`. O modelo contém quatro projetos, dois dos quais são colocados em cada pasta de solução.  
  
```  
<VSTemplate Version="2.0.0" Type="ProjectGroup"  
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">  
    <TemplateData>  
        <Name>Multi-Project Template Sample</Name>  
        <Description>An example of a multi-project template</Description>  
        <Icon>Icon.ico</Icon>  
        <ProjectType>VisualBasic</ProjectType>  
    </TemplateData>  
    <TemplateContent>  
        <ProjectCollection>  
            <SolutionFolder Name="Math Classes">  
                <ProjectTemplateLink ProjectName="MathClassLib1">  
                    MathClassLib1\MyTemplate.vstemplate  
                </ProjectTemplateLink>  
                <ProjectTemplateLink ProjectName="MathClassLib2">  
                    MathClassLib2\MyTemplate.vstemplate  
                </ProjectTemplateLink>  
            </SolutionFolder>  
            <SolutionFolder Name="Graphics Classes">  
                <ProjectTemplateLink ProjectName="GraphicsClassLib1">  
                    GraphicsClassLib1\MyTemplate.vstemplate  
                </ProjectTemplateLink>  
                <ProjectTemplateLink ProjectName="GraphicsClassLib2">  
                    GraphicsClassLib2\MyTemplate.vstemplate  
                </ProjectTemplateLink>  
            </SolutionFolder>  
        </ProjectCollection>  
    </TemplateContent>  
</VSTemplate>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Criando modelos de projeto e de item](../ide/creating-project-and-item-templates.md)   
 [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)   
 [Como criar modelos de projeto](../ide/how-to-create-project-templates.md)   
 [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)   
 [Elemento SolutionFolder (modelos do Visual Studio)](../extensibility/solutionfolder-element-visual-studio-templates.md)   
 [Elemento ProjectTemplateLink (modelos do Visual Studio)](../extensibility/projecttemplatelink-element-visual-studio-templates.md)



