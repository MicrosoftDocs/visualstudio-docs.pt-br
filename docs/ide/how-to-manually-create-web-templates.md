---
title: Criar modelos da Web para Visual Studio
ms.date: 01/02/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio templates, Web
- templates [Visual Studio], Web
- Web templates [Visual Studio]
- project templates [Visual Studio], Web
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 4ec63f231698bfa4c5a1360d21908aa2a4e2649e
ms.sourcegitcommit: 6a955a2d179cd0e137942389f940d9fcbbe125de
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51607452"
---
# <a name="how-to-manually-create-web-templates"></a>Como criar manualmente modelos da Web

Criar um modelo de Web é diferente de criar outros tipos de modelos. Como modelos de projeto Web aparecem na caixa de diálogo **Adicionar Novo Site** e itens de projetos da Web são categorizados por linguagem de programação, o arquivo *vstemplate* deve especificar o modelo como um modelo de Web e identificar a linguagem de programação.

> [!NOTE]
> Os modelos da Web devem conter um arquivo vazio *.webproj* que deve ser referenciado no arquivo *vstemplate* no atributo `File` do elemento `Project`. Embora os projetos Web não exijam um arquivo de projeto *.proj*, é necessário criar esse arquivo de stub para que o modelo da Web funcione corretamente.

## <a name="to-manually-create-a-web-template"></a>Para criar manualmente um modelo da Web

1. Crie um projeto Web.

2. Modifique ou exclua os arquivos no projeto ou adicione novos arquivos ao projeto.

3. Crie um arquivo XML e salve-o com uma extensão de nome de arquivo *vstemplate*, no mesmo diretório que o projeto. Não o adicione ao projeto no Visual Studio.

4. Edite o arquivo XML *vstemplate* para fornecer metadados do modelo de projeto. Para obter mais informações, consulte o [exemplo a seguir](#example).

5. Localize o elemento `ProjectType` no arquivo *vstemplate* e defina o valor de texto para `Web`.

6. Após o elemento `ProjectType`, adicione um elemento `ProjectSubType` e defina o valor de texto como a linguagem de programação do modelo. A linguagem de programação pode ter um dos seguintes valores:

   - CSharp
   - VisualBasic

     Por exemplo:

     ```xml
     <TemplateData>
       ...
       <ProjectType>Web</ProjectType>
       <ProjectSubType>CSharp</ProjectSubType>
       ...
     </TemplateData>
     ```

7. Selecione os arquivos em seu modelo (isso inclui o arquivo *vstemplate*), clique com o botão direito do mouse na seleção e escolha **Enviar para** > **Pasta compactada (zipada)**. Os arquivos são compactados em um arquivo *.zip*.

8. Coloque o arquivo de modelo *.zip* no diretório de modelo de projeto do Visual Studio. Por padrão, esse diretório é *%USERPROFILE%\Documents\Visual Studio \<Versão\>\ProjectTemplates*.

## <a name="example"></a>Exemplo

O exemplo a seguir mostra um arquivo *vstemplate* básico para um modelo de projeto Web:

```xml
<VSTemplate Version="2.0.0" Type="Project"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>MyWebProjecStarterKit</Name>
        <Description>A simple web template</Description>
        <Icon>icon.ico</Icon>
        <ProjectType>Web</ProjectType>
        <ProjectSubType>CSharp</ProjectSubType>
        <DefaultName>WebSite</DefaultName>
    </TemplateData>
    <TemplateContent>
        <Project File="WebApplication.webproj">
            <ProjectItem>icon.ico</ProjectItem>
            <ProjectItem OpenInEditor="true">Default.aspx</ProjectItem>
            <ProjectItem>Default.aspx.cs</ProjectItem>
        </Project>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>Consulte também

- [Criar modelos de projeto e de item](../ide/creating-project-and-item-templates.md)
- [Referência de esquema de modelo do Visual Studio (extensibilidade)](../extensibility/visual-studio-template-schema-reference.md)
