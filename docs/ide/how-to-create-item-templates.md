---
title: Criar modelos de item
ms.date: 01/02/2018
ms.topic: how-to
helpviewer_keywords:
- item templates [Visual Studio], creating
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: 0a0d4122d36c0946b6c1c98ef0f1523ce35751a6
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85284471"
---
# <a name="how-to-create-item-templates"></a>Como criar modelos de item

Este artigo mostra como criar um modelo de item usando o **Assistente de Exportação de Modelo**. Se seu modelo for composto por em vários arquivos, consulte [Como criar modelos de item de vários arquivos](../ide/how-to-create-multi-file-item-templates.md).

## <a name="add-an-item-template-to-the-add-new-item-dialog-box"></a>Adicione um modelo de item à caixa de diálogo Adicionar Novo Item

1. Crie ou abra um projeto no Visual Studio.

1. Adicione um item ao projeto e modifique-o caso desejar.

1. Modifique o arquivo de código para indicar em que ponto a substituição de parâmetro deve ocorrer. Para obter mais informações, consulte [Como substituir parâmetros em um modelo](../ide/how-to-substitute-parameters-in-a-template.md).

1. No menu **Projeto**, escolha **Exportar Modelo**.

1. Na página **Escolher Tipo de Modelo**, escolha **Modelo de Item**, selecione o projeto que contém o item e, em seguida, escolha **Avançar**.

1. Na página **Selecionar Item para Exportar**, escolha o item para o qual você deseja criar um modelo e, em seguida, escolha **Avançar**.

1. Na página **Selecionar Referências de Item**, selecione as referências de assembly a serem incluídas no modelo e, em seguida, escolha **Avançar**.

1. Na página **Selecionar Opções do Modelo**, insira o nome do modelo e a descrição opcional, um ícone e uma imagem de exibição e, em seguida, escolha **Concluir**.

    Os arquivos do modelo são adicionados a um arquivo *.zip* e copiados no diretório que você especificou na caixa de diálogo. O local padrão é o *%USERPROFILE%\Documents\Visual Studio \<version\> \Meus modelos exportados*.

1. Se você não tiver selecionado a opção **Importar automaticamente o modelo no Visual Studio** no **Assistente de Exportação de Modelo**, localize o modelo exportado. Em seguida, copie-o para o diretório de modelo de item do usuário. O local padrão é o *%USERPROFILE%\Documents\Visual Studio \<version\> \Templates\ItemTemplates*.

1. Feche o Visual Studio e, em seguida, o reabra.

1. Crie um novo projeto ou abra um projeto existente e, em seguida, escolha **projeto**  >  **Adicionar novo item** ou pressione **Ctrl** + **Shift** + **a**.

   O modelo de item aparece na caixa de diálogo **Adicionar Novo Item**. Se você adicionou uma descrição no **Assistente para Exportar Modelo**, a descrição será exibida no lado direito da caixa de diálogo.

## <a name="enable-the-item-template-to-be-used-in-a-universal-windows-app-project"></a>Habilitar o modelo de item a ser usado em um projeto de Aplicativo Universal do Windows

O assistente faz grande parte do trabalho de criar um modelo básico, mas, em muitos casos, será necessário modificar manualmente o arquivo *.vstemplate* depois de exportar o modelo. Por exemplo, se quiser que o item apareça na caixa de diálogo **Adicionar Novo Item** de um projeto de aplicativo universal do Windows, será necessário executar algumas etapas adicionais.

1. Siga as etapas na seção anterior para exportar um modelo de item.

1. Extraia o arquivo *.zip* que foi criado e abra o arquivo *.vstemplate* no Visual Studio.

1. Para um projeto universal C# do Windows, adicione o seguinte XML no elemento `<TemplateData>`:

   ```xml
   <TemplateID>Microsoft.CSharp.Class</TemplateID>
   ```

1. No Visual Studio, salve o arquivo *.vstemplate* e feche-o.

1. Copie e cole o arquivo *.vstemplate* novamente no arquivo *.zip*.

     Se a caixa de diálogo **Copiar Arquivo** for exibida, escolha a opção **Copiar e Substituir**.

Agora você pode adicionar um item com base neste modelo em um projeto universal do Windows usando a caixa de diálogo **Adicionar Novo Item**.

## <a name="enable-templates-for-specific-project-subtypes"></a>Habilitar os modelos para subtipos de projeto específicos

Você pode especificar que o modelo deve aparecer apenas para determinados subtipos do projeto, como Windows, Office, banco de dados ou Web.

1. Localize o elemento `ProjectType` no arquivo *.vstemplate* para o modelo de item.

1. Adicione um elemento [ProjectSubType](../extensibility/projectsubtype-element-visual-studio-templates.md) imediatamente após o elemento `ProjectType`.

1. Defina o valor de texto do elemento para um dos seguintes valores:

    - Windows
    - Office
    - Banco de dados
    - Web

Por exemplo: `<ProjectSubType>Database</ProjectSubType>`.

O exemplo a seguir mostra um modelo de item para projetos do **Office**.

```xml
<VSTemplate Version="2.0.0" Type="Item" Version="2.0.0">
   <TemplateData>
      <Name>Class</Name>
      <Description>An empty class file</Description>
      <Icon>Class.ico</Icon>
      <ProjectType>CSharp</ProjectType>
      <ProjectSubType>Office</ProjectSubType>
      <DefaultName>Class.cs</DefaultName>
   </TemplateData>
   <TemplateContent>
      <ProjectItem>Class1.cs</ProjectItem>
   </TemplateContent>
</VSTemplate>
```

## <a name="manually-create-an-item-template"></a>Criar manualmente um modelo de item

Em alguns casos, convém criar um modelo de item manualmente, desde o início.

1. Crie um projeto e um item de projeto.

2. Modifique o item de projeto até que ele esteja pronto para ser salvo como um modelo.

3. Modifique o arquivo de código para indicar o ponto em que a substituição de parâmetro deve ocorrer, caso ela ocorra em algum ponto. Para saber mais sobre substituição de parâmetro, confira [Como substituir parâmetros em um modelo.](../ide/how-to-substitute-parameters-in-a-template.md)

4. Crie um arquivo XML e salve-o com uma extensão de arquivo *.vstemplate* no mesmo diretório que o arquivo de item de projeto.

5. Edite o arquivo XML *.vstemplate* para fornecer metadados do modelo de item. Para obter mais informações, consulte [Referência de esquema de modelo (extensibilidade)](../extensibility/visual-studio-template-schema-reference.md) e o exemplo na seção anterior.

6. Salve o arquivo *.vstemplate* e feche-o.

7. No **Windows Explorer**, selecione os arquivos que você deseja incluir no modelo. Clique com o botão direito do mouse na seleção e escolha **Enviar para**  >  **pasta compactada (zipada)**. Os arquivos que você selecionou são compactados em um arquivo *. zip* .

::: moniker range="vs-2017"

8. Copie o arquivo *.zip* e cole-o no local do modelo de item do usuário. O diretório padrão é *%USERPROFILE%\Documents\Visual Studio 2017\Templates\ItemTemplates*. Para obter mais informações, consulte [Como localizar e organizar modelos de projeto e de item](../ide/how-to-locate-and-organize-project-and-item-templates.md).

::: moniker-end

::: moniker range=">=vs-2019"

8. Copie o arquivo *.zip* e cole-o no local do modelo de item do usuário. O diretório padrão é *%USERPROFILE%\Documents\Visual Studio 2019\Templates\ItemTemplates*. Para obter mais informações, consulte [Como localizar e organizar modelos de projeto e de item](../ide/how-to-locate-and-organize-project-and-item-templates.md).

::: moniker-end

## <a name="see-also"></a>Veja também

- [Criar modelos de projeto e de item](../ide/creating-project-and-item-templates.md)
- [Como criar modelos de item multiarquivos](../ide/how-to-create-multi-file-item-templates.md)
- [Referência de esquema de modelo do Visual Studio (extensibilidade)](../extensibility/visual-studio-template-schema-reference.md)
