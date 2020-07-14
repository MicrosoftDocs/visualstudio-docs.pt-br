---
title: Criar modelos de multiprojeto
ms.date: 04/17/2019
ms.topic: how-to
helpviewer_keywords:
- Visual Studio templates, creating multi-project
- project templates, multi-project
- multi-project templates
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: b71af98c7d72e0b3a510f3968f3d0770cd5401df
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85284406"
---
# <a name="how-to-create-multi-project-templates"></a>Como criar modelos multiprojetos

Os modelos de vários projetos atuam como contêineres para dois ou mais projetos. Quando você cria um projeto baseado em um modelo multiprojetos, todos os projetos no modelo são adicionados à solução.

Um modelo de vários projetos tem dois ou mais modelos de projeto e um modelo raiz do tipo **Project**.

Os modelos multiprojetos comportam-se de forma diferente dos modelos de projeto único. Eles têm as seguintes características exclusivas:

- Nomes não podem ser atribuídos a projetos individuais em um modelo multiprojetos quando o modelo é usado para criar um projeto. Em vez disso, use o atributo **ProjectName** no elemento **ProjectTemplateLink** do arquivo *vstemplate* para especificar um nome para cada projeto.

- Os modelos multiprojetos podem conter projetos de diferentes linguagens, mas o modelo inteiro em si só pode ser colocado em uma única categoria. Especifique a categoria de modelo no elemento **ProjectType** do arquivo *vstemplate*.

Um modelo de vários projetos deve incluir os seguintes itens, compactados em um arquivo *. zip* :

- Um arquivo *vstemplate* raiz para todo o modelo de vários projetos. Esse arquivo *vstemplate* raiz contém metadados que são exibidos na caixa de diálogo em que você cria um projeto. Ela também especifica onde encontrar os arquivos *vstemplate* para os projetos no modelo. Esse arquivo deve estar localizado na raiz do arquivo *. zip* .

- Duas ou mais pastas que contêm os arquivos necessários para um modelo de projeto concluído. As pastas incluem todos os arquivos de código para o projeto e também um arquivo *vstemplate* para o projeto.

Por exemplo, um arquivo *. zip* de modelo multiprojeto que tem dois projetos pode ter os seguintes arquivos e diretórios:

- *MultiProjectTemplate.vstemplate*
- *\Project1\MyTemplate.vstemplate*
- *\Project1\Project1.vbproj*
- *\Project1\Class.vb*
- *\Project2\MyTemplate.vstemplate*
- *\Project2\Project2.vbproj*
- *\Project2\Class.vb*

O arquivo *vstemplate* raiz para um modelo de vários projetos difere de um modelo de projeto único das seguintes maneiras:

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

> [!TIP]
> Se você deseja que o modelo de multiprojetos apareça apenas na nova caixa de diálogo do projeto e não nos projetos individuais que ele contém, marque os modelos internos como [oculto](../extensibility/hidden-element-visual-studio-templates.md). Por exemplo:
>
> ```xml
> <VSTemplate Type="Project" ... >
>     <TemplateData>
>         ...
>         <Hidden>true</Hidden>
>     </TemplateData>
>     ...
> </VSTemplate>
> ```

## <a name="create-a-multi-project-template-from-an-existing-solution"></a>Criar um modelo multiprojetos usando uma solução existente

1. Crie uma solução e adicione dois ou mais projetos.

2. Personalize os projetos até que eles estejam prontos para serem exportados para um modelo.

   > [!TIP]
   > Se você estiver usando [parâmetros de modelo](template-parameters.md) e quiser se referir a variáveis do modelo pai, prefixe o nome do parâmetro com `ext_`. Por exemplo, `$ext_safeprojectname$`. Além disso, defina o atributo **CopyParameters** do elemento **ProjectTemplateLink** como **true**.
   >
   > ```xml
   > <ProjectTemplateLink ProjectName="MyProject" CopyParameters="true">...</ProjectTemplateLink>
   > ```

3. No menu **Projeto**, escolha **Exportar Modelo**.

   O **Assistente para Exportar Modelo** é aberto.

4. Na página **Escolher Tipo de Modelo**, selecione **Modelo de Projeto**. Selecione um dos projetos que você deseja exportar para um modelo e, em seguida, escolha **Avançar**. (Você repetirá essas etapas para cada projeto na solução.)

5. Na página **Selecionar Opções do Modelo**, insira um nome e uma descrição opcional, um ícone e uma imagem de exibição para o modelo. Escolha **Concluir**.

   O projeto é exportado para um arquivo *. zip* e colocado no local de saída especificado.

   > [!NOTE]
   > Cada projeto deve ser exportado para um modelo separadamente, portanto, repita as etapas anteriores para cada projeto na solução.

6. Crie um diretório para o modelo, com um subdiretório para cada projeto.

7. Extraia o conteúdo do arquivo *.zip* de cada projeto para o subdiretório correspondente que você criou.

8. No diretório base, crie um arquivo XML com uma extensão de arquivo *.vstemplate*. Esse arquivo contém os metadados do modelo multiprojetos. Consulte o exemplo a seguir para obter a estrutura do arquivo. Certifique-se de especificar o caminho relativo para o arquivo *vstemplate* de cada projeto.

9. Selecione todos os arquivos no diretório base e, no menu de contexto ou clique com o botão direito do mouse, escolha **Enviar para**  >  **pasta compactada (zipada)**.

   Esses arquivos e pastas estão compactados em um arquivo *.zip*.

10. Copie o arquivo *. zip* para o diretório de modelo de projeto do usuário. Por padrão, esse diretório é o *%USERPROFILE%\Documents\Visual Studio \<version\> \Templates\ProjectTemplates*.

11. No Visual Studio, escolha **arquivo**  >  **novo**  >  **projeto** e verifique se o modelo é exibido.

## <a name="two-project-example"></a>Exemplo de dois projetos

Este exemplo mostra um arquivo principal *vstemplate* raiz de vários projetos. Neste exemplo, o modelo tem dois projetos, **Meu Aplicativo do Windows** e **Minha Biblioteca de Classes**. O atributo **ProjectName** no elemento **ProjectTemplateLink** especifica o nome fornecido para o projeto.

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

## <a name="see-also"></a>Veja também

- [Criando modelos de projeto e item](../ide/creating-project-and-item-templates.md)
- [Como: criar modelos de projeto](../ide/how-to-create-project-templates.md)
- [Referência de esquema de modelo do Visual Studio (extensibilidade)](../extensibility/visual-studio-template-schema-reference.md)
- [Elemento SolutionFolder (modelos do Visual Studio)](../extensibility/solutionfolder-element-visual-studio-templates.md)
- [Elemento ProjectTemplateLink (modelos do Visual Studio)](../extensibility/projecttemplatelink-element-visual-studio-templates.md)
