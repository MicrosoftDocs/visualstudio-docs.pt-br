---
title: Criando modelos de item multiarquivos para o Visual Studio
ms.date: 01/02/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio templates, creating multi-file item templates
- multi-file item templates
- item templates, creating multi-file item templates
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 0ba36e666daf7940971dff587aa483d62f97b6a9
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31942150"
---
# <a name="how-to-create-multi-file-item-templates"></a>Como criar modelos de item multiarquivos

Os modelos de item podem especificar apenas um item, mas, algumas vezes, o item é composto por vários arquivos. Por exemplo, um modelo de item do Windows Forms requer os três arquivos a seguir:

- Um arquivo que contém o código para o formulário

- Um arquivo que contém as informações do designer de formulário

- Um arquivo que contém os recursos inseridos para o formulário

Os modelos de item multiarquivos exigem parâmetros para garantir que as extensões de arquivo corretas sejam usadas quando o item é criado. Se você criar um modelo de item multiarquivos usando o **Assistente para Exportar Modelo**, esses parâmetros serão gerados automaticamente e nenhuma outra edição será necessária.

## <a name="to-create-a-multi-file-item-template-by-using-the-export-template-wizard"></a>Para criar um modelo de item multiarquivos usando o Assistente para Exportar Modelo

Você pode criar um modelo de item multiarquivos da mesma maneira que se cria um modelo de item de arquivo único. Consulte [Como criar modelos de item](../ide/how-to-create-item-templates.md). Na página **Selecionar Item para Exportar** do assistente, selecione o arquivo que contém os arquivos dependentes (por exemplo, um arquivo de formato do Windows Forms). O assistente inclui automaticamente todos os arquivos dependentes, como arquivos de recursos e do designer, no modelo.

## <a name="to-manually-create-a-multi-file-item-template"></a>Para criar manualmente um modelo de item de vários arquivos

1. Crie o modelo de item da mesma forma em que você criaria manualmente um modelo de item de arquivo único, mas inclua cada arquivo que constitui o item multiarquivos.

1. No arquivo XML *.vstemplate*, adicione um elemento `ProjectItem` a cada arquivo individual e, em seguida, adicione um atributo `TargetFileName` a este elemento. Defina os valores do atributo `TargetFileName` como *$fileinputname$.ExtensãoDeArquivo*, em que *ExtensãoDeArquivo* é a extensão de arquivo do arquivo que está sendo incluído no modelo. Por exemplo:

    ```xml
    <ProjectItem TargetFileName="$fileinputname$.vb">
        Form1.vb
    </ProjectItem>
    <ProjectItem TargetFileName="$fileinputname$.Designer.vb">
        Form1.Designer.vb
    </ProjectItem>
    <ProjectItem TargetFileName="$fileinputname$.resx">
        Form1.resx
    </ProjectItem>
    ```

     > [!NOTE]
     > Quando um item derivado deste modelo for adicionado a um projeto, os nomes de arquivo serão derivados do nome que o usuário inserir na caixa de diálogo **Adicionar Novo Item**.

1. Selecione os arquivos a serem incluídos em seu modelo, clique com o botão direito do mouse na seleção e escolha **Enviar para** > **Pasta compactada (zipada)**.

   Os arquivos selecionados são compactados em um arquivo *.zip*.

1. Copie o arquivo *.zip* para o local do modelo de item do usuário. Por padrão, o diretório é *%USERPROFILE%\Documents\Visual Studio \<Versão\>\Templates\ItemTemplates*. Para obter mais informações, consulte [Como localizar e organizar modelos](../ide/how-to-locate-and-organize-project-and-item-templates.md).

1. Feche o Visual Studio e, em seguida, o reabra.

1. Crie um novo projeto ou abra um projeto existente e, em seguida, escolha **Projeto** > **Adicionar Novo Item** ou pressione **Ctrl**+**Shift**+**A**.

   O modelo de item multiarquivos aparece na caixa de diálogo **Adicionar Novo Item**.

## <a name="example"></a>Exemplo

O exemplo a seguir mostra um modelo do Windows Forms. Quando um item é criado com base nesse modelo, os nomes dos três arquivos criados corresponderá ao nome inserido na caixa de diálogo **Adicionar Novo Item**.

```xml
<VSTemplate Version="2.0.0" Type="Item"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>Multi-file Item Template</Name>
        <Icon>Icon.ico</Icon>
        <Description>An example of a multi-file item template</Description>
        <ProjectType>VisualBasic</ProjectType>
    </TemplateData>
    <TemplateContent>
        <ProjectItem TargetFileName="$fileinputname$.vb" SubType="Form">
            Form1.vb
        </ProjectItem>
        <ProjectItem TargetFileName="$fileinputname$.Designer.vb">
            Form1.Designer.vb
        </ProjectItem>
        <ProjectItem TargetFileName="$fileinputname$.resx">
            Form1.resx
        </ProjectItem>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>Consulte também

- [Criar modelos de projeto e de item](../ide/creating-project-and-item-templates.md)
- [Como criar modelos de item](../ide/how-to-create-item-templates.md)
- [Parâmetros de modelo](../ide/template-parameters.md)
- [Como substituir parâmetros em um modelo](../ide/how-to-substitute-parameters-in-a-template.md)