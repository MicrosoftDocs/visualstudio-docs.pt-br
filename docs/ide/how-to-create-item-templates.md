---
title: Criar modelos de item para o Visual Studio
ms.date: 01/02/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- item templates [Visual Studio], creating
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 342b7ebd17280c47296fae43c6541a5e969ad5f3
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31954656"
---
# <a name="how-to-create-item-templates"></a>Como criar modelos de item

Este artigo mostra como criar um modelo de item usando o **Assistente de Exportação de Modelo**. Se seu modelo for composto por em vários arquivos, consulte [Como criar modelos de item de vários arquivos](../ide/how-to-create-multi-file-item-templates.md).

## <a name="to-add-a-user-item-template-to-the-add-new-item-dialog-box"></a>Para adicionar um modelo de item de usuário para a caixa de diálogo Adicionar Novo Item

1. Crie ou abra um projeto no Visual Studio.

1. Adicione um item ao projeto e modifique-o caso desejar.

1. Modifique o arquivo de código para indicar em que ponto a substituição de parâmetro deve ocorrer. Para obter mais informações, consulte [Como substituir parâmetros em um modelo](../ide/how-to-substitute-parameters-in-a-template.md).

1. No menu **Projeto**, escolha **Exportar Modelo**.

1. Na página **Escolher Tipo de Modelo**, escolha **Modelo de Item**, selecione o projeto que contém o item e, em seguida, escolha **Avançar**.

1. Na página **Selecionar Item para Exportar**, escolha o item para o qual você deseja criar um modelo e, em seguida, escolha **Avançar**.

1. Na página **Selecionar Referências de Item**, selecione as referências de assembly a serem incluídas no modelo e, em seguida, escolha **Avançar**.

1. Na página **Selecionar Opções do Modelo**, insira o nome do modelo e a descrição opcional, um ícone e uma imagem de exibição e, em seguida, escolha **Concluir**.

    Os arquivos do modelo são adicionados a um arquivo *.zip* e copiados no diretório que você especificou na caixa de diálogo. O local padrão é *%USERPROFILE%\Documents\Visual Studio \<versão\>\My Exported Templates*.

1. Se você não tiver selecionado a opção **Importar automaticamente o modelo no Visual Studio** no **Assistente de Exportação de Modelo**, localize o modelo exportado. Em seguida, copie-o para o diretório de modelo de item do usuário. O local padrão é *%USERPROFILE%\Documents\Visual Studio \<versão\>\Templates\ItemTemplates*.

1. Feche o Visual Studio e, em seguida, o reabra.

1. Crie um novo projeto ou abra um projeto existente e, em seguida, escolha **Projeto** > **Adicionar Novo Item** ou pressione **Ctrl**+**Shift**+**A**.

   O modelo de item aparece na caixa de diálogo **Adicionar Novo Item**. Se você adicionou uma descrição no **Assistente para Exportar Modelo**, a descrição será exibida no lado direito da caixa de diálogo.

## <a name="to-enable-the-item-template-to-be-used-in-a-universal-windows-app-project"></a>Para habilitar o modelo de item a ser usado em um projeto de aplicativo universal do Windows

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

## <a name="to-enable-templates-for-specific-project-subtypes"></a>Para habilitar os modelos para subtipos de projeto específicos

Você pode especificar que o modelo deve aparecer apenas para determinados subtipos do projeto, como Windows, Office, banco de dados ou Web.

1. Localize o elemento `ProjectType` no arquivo *.vstemplate* para o modelo de item.

1. Adicione um elemento [ProjectSubType](../extensibility/projectsubtype-element-visual-studio-templates.md) imediatamente após o elemento `ProjectType`.

1. Defina o valor de texto do elemento para um dos seguintes valores:

    - Windows
    - Office
    - Banco de Dados
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

## <a name="to-manually-create-an-item-template-without-using-the-export-template-wizard"></a>Para criar manualmente um modelo de item sem usar o assistente Exportar Modelo

Em alguns casos, convém criar um modelo de item manualmente, desde o início.

1. Crie um projeto e um item de projeto.

1. Modifique o item de projeto até que ele esteja pronto para ser salvo como um modelo.

1. Modifique o arquivo de código para indicar o ponto em que a substituição de parâmetro deve ocorrer, caso ela ocorra em algum ponto. Para saber mais sobre substituição de parâmetro, confira [Como substituir parâmetros em um modelo.](../ide/how-to-substitute-parameters-in-a-template.md)

1. Crie um arquivo XML e salve-o com uma extensão de arquivo *.vstemplate* no mesmo diretório que o arquivo de item de projeto.

1. Edite o arquivo XML *.vstemplate* para fornecer metadados do modelo de item. Para obter mais informações, consulte [Referência de esquema de modelo (extensibilidade)](../extensibility/visual-studio-template-schema-reference.md) e o exemplo na seção anterior.

1. Salve o arquivo *.vstemplate* e feche-o.

1. No **Windows Explorer**, selecione os arquivos que você deseja incluir no modelo. Clique com o botão direito do mouse na seleção e escolha **Enviar para** > **Pasta compactada (zipada)**. Os arquivos selecionados são compactados em um arquivo *.zip*.

1. Copie o arquivo *.zip* e cole-o no local do modelo de item do usuário. No Visual Studio de 2017, o diretório padrão é *%USERPROFILE%\Documents\Visual Studio 2017\Templates\ItemTemplates*. Para obter mais informações, consulte [Como localizar e organizar modelos de projeto e de item](../ide/how-to-locate-and-organize-project-and-item-templates.md).

## <a name="see-also"></a>Consulte também

- [Criar modelos de projeto e de item](../ide/creating-project-and-item-templates.md)
- [Como criar modelos de item multiarquivos](../ide/how-to-create-multi-file-item-templates.md)
- [Referência de esquema de modelo do Visual Studio (extensibilidade)](../extensibility/visual-studio-template-schema-reference.md)
