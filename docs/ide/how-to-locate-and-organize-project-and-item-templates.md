---
title: Organizar modelos no Visual Studio
ms.date: 01/02/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- project templates [Visual Studio], locations
- item templates [Visual Studio], locations
- template locations [Visual Studio]
- Visual Studio templates, organizing
- templates [Visual Studio], organizing
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 65d4940e7a7969fe28fe115ec7ef42cfdc645c9a
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31948724"
---
# <a name="how-to-locate-and-organize-project-and-item-templates"></a>Como localizar e organizar modelos de projeto e de item

Os arquivos de modelo devem ser colocados em um local que o Visual Studio reconheça, para que os modelos apareçam nas caixas de diálogo **Novo Projeto** e **Adicionar Novo Item**. Você também pode criar subcategorias personalizadas no local do modelo de usuário e as categorias são mostradas nas caixas de diálogo **Novo Projeto** e **Adicionar Novo Item**.

## <a name="locate-templates"></a>Localizar modelos

Os modelos instalados e os modelos do usuário são armazenados em dois locais diferentes.

### <a name="user-templates"></a>Modelos do usuário

Se você adicionar um arquivo compactado (*.zip*) que inclua um arquivo *.vstemplate* no diretório de modelos do usuário, o modelo aparecerá na caixa de diálogo **Novo Projeto** ou **Adicionar Novo Item**. Por padrão, os modelos do usuário estão localizados em:

- *%USERPROFILE%\Documents\Visual Studio \<Versão\>\Templates\ProjectTemplates*

- *%USERPROFILE%\Documents\Visual Studio \<Versão\>\Templates\ItemTemplates*

Por exemplo, o seguinte diretório contém modelos de projeto do usuário para C#:

- *C:\Users\UserName\Documents\Visual Studio 2017\Templates\ProjectTemplates\Visual C#*

> [!TIP]
> Você pode definir o local dos modelos do usuário em **Ferramentas** > **Opções** > **Projetos e Soluções** > **Locais**.

### <a name="installed-templates"></a>Modelos instalados

Por padrão, os modelos instalados com o Visual Studio estão localizados em:

- *\\<VisualStudioInstallationDirectory\>\Common7\IDE\ItemTemplates\\<Linguagem de programação\>\\<Locale ID>*

- *\\<VisualStudioInstallationDirectory\>\Common7\IDE\ProjectTemplates\\<Linguagem de programação\>\\<Locale ID>*

Por exemplo, o diretório a seguir contém os modelos de item do Visual Basic para inglês (LCID 1033):

- *C:\\<VisualStudioInstallationDirectory\>\Common7\IDE\ItemTemplates\VisualBasic\1033*

## <a name="organize-templates"></a>Organizar modelos

As categorias nas caixas de diálogo **Novo Projeto** e **Adicionar Novo Item** refletem as estruturas de diretório que existem nos locais dos modelos instalados e dos modelos do usuário. Os modelos do usuário podem ser organizados em suas próprias categorias adicionando novas pastas ao diretório do modelo do usuário. As caixas de diálogo **Novo Projeto** e **Adicionar Novo Item** mostram alterações feitas nas categorias de modelo do usuário.

> [!NOTE]
> Você não pode criar uma nova categoria no nível da linguagem de programação. Novas categorias podem ser criadas apenas dentro de cada linguagem.

### <a name="to-create-new-user-project-template-categories"></a>Para criar novas categorias de modelo de projeto do usuário

1. Crie uma pasta na pasta de linguagem de programação no diretório de modelo de projeto do usuário. Por exemplo, para estabelecer uma categoria **HelloWorld** para modelos de projeto C#, crie o seguinte diretório:

    - *\%USERPROFILE%\Documents\Visual Studio \<Versão\>\Templates\ProjectTemplates\Visual C#\HelloWorld\*

1. Coloque todos os modelos dessa categoria na nova pasta.

1. No menu **Arquivo**, escolha **Novo** > **Projeto**.

   A categoria **HelloWorld** aparece na caixa de diálogo **Novo Projeto** em **Instalado** > **Visual C#**.

### <a name="to-create-new-user-item-template-categories"></a>Para criar novas categorias de modelo de item do usuário

1. Crie uma pasta na pasta de linguagem de programação no diretório de modelo de item do usuário. Por exemplo, para estabelecer uma categoria **HelloWorld** para modelos de item C#, crie o seguinte diretório:

    - *\%USERPROFILE%\Documents\Visual Studio \<Versão\>\Templates\ItemTemplates\Visual C#\HelloWorld\*

1. Coloque todos os modelos dessa categoria na nova pasta.

1. Crie um projeto ou abra um projeto existente. Em seguida, no menu **Projeto**, escolha **Adicionar Novo Item**.

   A categoria **HelloWorld** aparece na caixa de diálogo **Adicionar Novo Item** em **Instalado** > **Itens do Visual C#**.

### <a name="display-templates-in-parent-categories"></a>Exibir modelos em categorias pai

Você pode habilitar modelos em subcategorias a serem exibidos em suas categorias pai usando o elemento `NumberOfParentCategoriesToRollUp` no arquivo *.vstemplate*. Essas etapas são as mesmas para modelos de projeto e modelos de item.

#### <a name="to-display-templates-in-parent-categories"></a>Para exibir modelos em categorias pai

1. Localize o arquivo *.zip* que contém o modelo.

1. Extraia o arquivo *.zip*.

1. Abra o arquivo *.vstemplate* no Visual Studio.

1. No elemento `TemplateData`, adicione um elemento `NumberOfParentCategoriesToRollUp`. Por exemplo, o código a seguir torna o modelo visível na categoria pai, mas não superior.

    ```xml
    <TemplateData>
        ...
        <NumberOfParentCategoriesToRollUp>
            1
        </NumberOfParentCategoriesToRollUp>
        ...
    </TemplateData>
    ```

1. Salve e feche o arquivo *.vstemplate*.

1. Selecione os arquivos em seu modelo, clique com o botão direito do mouse na seleção e escolha **Enviar para** > **Pasta compactada (zipada)**.

   Os arquivos são compactados em um arquivo *.zip*.

1. Exclua os arquivos de modelo extraídos e o arquivo *.zip* de modelo antigo.

1. Coloque o novo arquivo *.zip* no diretório que tinha o arquivo *.zip* excluído.

## <a name="see-also"></a>Consulte também

- [Personalizar modelos](../ide/customizing-project-and-item-templates.md)
- [Referência de esquema de modelo do Visual Studio (extensibilidade)](../extensibility/visual-studio-template-schema-reference.md)
- [NumberOfParentCategoriesToRollUp (modelos do Visual Studio)](../extensibility/numberofparentcategoriestorollup-visual-studio-templates.md)
- [Como criar modelos de projeto](../ide/how-to-create-project-templates.md)
- [Como criar modelos de item](../ide/how-to-create-item-templates.md)