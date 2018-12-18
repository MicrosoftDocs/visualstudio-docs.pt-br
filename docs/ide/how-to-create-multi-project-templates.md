---
title: Criar modelos multiprojetos para Visual Studio
ms.date: 01/02/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio templates, creating multi-project
- project templates, multi-project
- multi-project templates
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 24002512ec891866839ad3bd33590c3dfe966e99
ms.sourcegitcommit: e5a382de633156b85b292f35e3d740f817715d47
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38978379"
---
# <a name="how-to-create-multi-project-templates"></a>Como criar modelos multiprojetos

Os modelos de vários projetos atuam como contêineres para dois ou mais projetos. Quando você cria um projeto baseado em um modelo multiprojetos usando a caixa de diálogo **Novo Projeto**, todos os projetos no modelo são adicionados à solução.

Um modelo multiprojeto tem dois ou mais modelos de projeto e um modelo raiz do tipo **ProjectGroup**.

Os modelos multiprojetos comportam-se de forma diferente dos modelos de projeto único. Eles têm as seguintes características exclusivas:

- Os projetos individuais em um modelo multiprojetos não podem ter nomes atribuídos na caixa de diálogo **Novo Projeto**. Em vez disso, use o atributo **ProjectName** no elemento **ProjectTemplateLink** do arquivo *vstemplate* para especificar um nome para cada projeto.

- Os modelos multiprojetos podem conter projetos de diferentes linguagens, mas o modelo inteiro em si só pode ser colocado em uma única categoria. Especifique a categoria de modelo no elemento **ProjectType** do arquivo *vstemplate*.

Um modelo multiprojeto deve incluir os itens a seguir, compactados em um arquivo *.zip*:

- Um arquivo *vstemplate* raiz para todo o modelo multiprojeto. Esse arquivo *vstemplate* raiz contém metadados que a caixa de diálogo **Novo Projeto** exibe e especifica onde localizar os arquivos *vstemplate* dos projetos no modelo. Esse arquivo deve estar localizado na raiz do arquivo *.zip*.

- Duas ou mais pastas que contêm os arquivos necessários para um modelo de projeto concluído. As pastas incluem todos os arquivos de código do projeto e também um arquivo *vstemplate* do projeto.

Por exemplo, um arquivo *.zip* de modelo multiprojeto com dois projetos poderia ter os seguintes arquivos e diretórios:

- *MultiProjectTemplate.vstemplate*
- *\Project1\MyTemplate.vstemplate*
- *\Project1\Project1.vbproj*
- *\Project1\Class.vb*
- *\Project2\MyTemplate.vstemplate*
- *\Project2\Project2.vbproj*
- *\Project2\Class.vb*

O arquivo *vstemplate* raiz para um modelo multiprojeto difere de um modelo de projeto único das seguintes maneiras:

- O atributo **Type** do elemento **VSTemplate** tem o valor **ProjectGroup**, em vez de **Project**. Por exemplo:

    ```xml
    <VSTemplate Version="2.0.0" Type="ProjectGroup"
        xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    ```

- O elemento **TemplateContent** contém um elemento **ProjectCollection** que tem um ou mais elementos **ProjectTemplateLink** que definem os caminhos para os arquivos *vstemplate* dos projetos incluídos. Por exemplo:

    ```xml
    <TemplateContent>
        <ProjectCollection>
            <ProjectTemplateLink>
                Project1\MyTemplate.vstemplate
            </ProjectTemplateLink>
            <ProjectTemplateLink>
                Project2\MyTemplate.vstemplate
            </ProjectTemplateLink>
        </ProjectCollection>
    </TemplateContent>
    ```

## <a name="to-create-a-multi-project-template-from-an-existing-solution"></a>Para criar um modelo multiprojetos usando uma solução existente

1. Crie uma solução e adicione dois ou mais projetos.

1. Personalize os projetos até que eles estejam prontos para serem exportados para um modelo.

1. No menu **Projeto**, escolha **Exportar Modelo**.

   O **Assistente para Exportar Modelo** é aberto.

1. Na página **Escolher Tipo de Modelo**, selecione **Modelo de Projeto**. Selecione o projeto que você deseja exportar como um modelo e, em seguida, escolha **Avançar**.

1. Na página **Selecionar Opções do Modelo**, insira um nome e uma descrição opcional, um ícone e uma imagem de exibição para o modelo. Escolha **Concluir**.

   O projeto é exportado para um arquivo *.zip* e colocado no local de saída especificado.

   > [!NOTE]
   > Cada projeto deve ser exportado para um modelo separadamente, portanto, repita as etapas anteriores para cada projeto na solução.

1. Crie um diretório para o modelo, com um subdiretório para cada projeto.

1. Extraia o conteúdo do arquivo *.zip* de cada projeto para o subdiretório correspondente que você criou.

1. No diretório base, crie um arquivo XML com uma extensão de arquivo *.vstemplate*. Esse arquivo contém os metadados do modelo multiprojetos. Consulte o exemplo a seguir para obter a estrutura do arquivo. Certifique-se de especificar o caminho relativo para o arquivo *vstemplate* de cada projeto.

1. Selecione todos os arquivos no diretório base e, no menu de clique com o botão direito do mouse ou de contexto, escolha **Enviar para** > **Pasta compactada (zipada)**.

   Esses arquivos e pastas estão compactados em um arquivo *.zip*.

1. Copie o arquivo *.zip* no diretório do modelo de projeto do usuário. Por padrão, esse diretório é *%USERPROFILE%\Documents\Visual Studio \<versão\>\Templates\ProjectTemplates*.

1. No Visual Studio, abra a caixa de diálogo **Novo Projeto** e verifique se o modelo é exibido.

## <a name="two-project-example"></a>Exemplo de dois projetos

Esse exemplo mostra um arquivo *vstemplate* raiz multiprojeto básico. Neste exemplo, o modelo tem dois projetos, **Meu Aplicativo do Windows** e **Minha Biblioteca de Classes**. O atributo **ProjectName** no elemento **ProjectTemplateLink** especifica o nome fornecido para o projeto.

> [!TIP]
> Se o atributo **ProjectName** não for especificado, o nome do arquivo *vstemplate* será usado como o nome do projeto.

```xml
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

## <a name="example-with-solution-folders"></a>Exemplo com pastas de solução

Este exemplo usa o elemento **SolutionFolder** para dividir os projetos em dois grupos, **Math Classes** e **Graphics Classes**. O modelo tem quatro projetos, dois dos quais são colocados em cada pasta de solução.

```xml
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

- [Criando modelos de projeto e de item](../ide/creating-project-and-item-templates.md)
- [Como criar modelos de projeto](../ide/how-to-create-project-templates.md)
- [Referência de esquema de modelo do Visual Studio (extensibilidade)](../extensibility/visual-studio-template-schema-reference.md)
- [Elemento SolutionFolder (modelos do Visual Studio)](../extensibility/solutionfolder-element-visual-studio-templates.md)
- [Elemento ProjectTemplateLink (modelos do Visual Studio)](../extensibility/projecttemplatelink-element-visual-studio-templates.md)