---
title: EditorConfig
description: Usando um arquivo editorconfig para habilitar estilos de codificação de projeto consistentes no Visual Studio para Mac.
author: conceptdev
ms.author: crdun
ms.date: 05/06/2018
ms.topic: article
ms.technology: vs-ide-install
ms.assetid: 26A0DE31-2FBF-4E1B-99FB-083111AA1680
ms.openlocfilehash: d42103d17b64ee9b3fb2a0660017824490655808
ms.sourcegitcommit: 0a8ac5f2a685270d9ca79bb39d26fd90099bfa29
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51294013"
---
# <a name="creating-and-editing-a-custom-editorconfig-file"></a>Criando e editando um arquivo EditorConfig personalizado

No Visual Studio para Mac, você pode adicionar um arquivo [EditorConfig](http://editorconfig.org/) ao seu projeto ou solução para impor estilos de codificação consistente para todas as pessoas que trabalham na base de código. As configurações declaradas no arquivo EditorConfig têm precedência sobre as configurações do editor de texto globais do Visual Studio para Mac. Usar um arquivo do EditorConfig dentro de seu projeto ou base de código permite que você defina o estilo de codificação, as preferências e os avisos para seu projeto. Devido ao arquivo fazer parte de sua base de código, ele facilita para todos os usuários a adesão às práticas de codificação de um projeto, independentemente do IDE ou editor de código que eles usam.

Arquivos [EditorConfig](http://editorconfig.org/) são compatíveis com muitos editores de código e IDEs, incluindo o Visual Studio 2017.

## <a name="supported-settings"></a>Configurações com suporte

O editor no Visual Studio para Mac é compatível com o conjunto principal de [propriedades do EditorConfig](http://editorconfig.org/#supported-properties):

- `indent_style`
- `indent_size`
- `tab_width`
- `end_of_line`
- `charset`
- `trim_trailing_whitespace`
- `insert_final_newline`
- `root`

O EditorConfig também dá suporte a [convenções de codificação](/visualstudio/ide/editorconfig-code-style-settings-reference) em C#.

## <a name="add-an-editorconfig-file-to-a-project"></a>Adicionar um arquivo EditorConfig a um projeto

### <a name="adding-a-new-editorconfig-file"></a>Adicionando um novo arquivo EditorConfig

1. Abra seu projeto no Visual Studio para Mac. Selecione o nó de solução ou do projeto ao qual você deseja adicionar o arquivo EditorConfig. Adicionar o arquivo ao diretório da solução aplica as configurações de .editorconfig a todos os projetos na solução.

2. Clique com o botão direito do mouse no nó e selecione **Adicionar > Novo Arquivo** para abrir a caixa de diálogo **Novo Arquivo**:

    ![Itens de menu de conteúdo](media/editorconfig-image0.png)

3. Escolha **Diversos > Arquivo de Texto Vazio** e dê a ele um **Nome** `.editorconfig`. Pressione **Novo** para criar o arquivo e abri-lo no editor:

    ![Caixa de diálogo Novo Arquivo](media/editorconfig-image1.png)

    Adicionar o item no nível da solução automaticamente cria e aninha-o em uma pasta **Itens de Solução**:

    ![O item de solução é exibido no painel de soluções](media/editorconfig-image1a.png)

4. Edite o arquivo. Por exemplo:

    ```EditorConfig
    # This file is the top-most EditorConfig file
    root = true

    # All Files
    [*]
    indent_style = space
    indent_size = 8
    insert_final_newline = false
    trim_trailing_whitespace = false

    [*.cs]
    csharp_new_line_before_open_brace = none
    ```

4. As configurações do arquivo `.editorconfig` serão aplicadas a qualquer novo código que você escrever, mas o código existente talvez precise ser reformatado para ser consistente com as novas configurações. Para aplicar as configurações do arquivo `.editorconfig` a um arquivo de origem existente, abra o arquivo e escolha **Editar > Formatar > Formatar Documento** na barra de menus:

    ![Item de menu Formatar Documento](media/editorconfig-image2.png)

### <a name="adding-an-existing-editorconfig-file"></a>Adicionando um arquivo EditorConfig existente

Se estiver trabalhando com um projeto ou solução que já contém um arquivo `.editorconfig`, você não precisará fazer para aplicar as configurações. Novas linhas de código serão formatadas de acordo com as configurações de EditorConfig.

Talvez você queira reutilizar um arquivo `.editorconfig` existente em seu projeto. Para adicionar um arquivo existente, faça o seguinte:

1. Clique com o botão direito do mouse na pasta na qual você deseja adicionar e selecione **Adicionar > Adicionar Arquivos**.

2. Navegue até o diretório do arquivo necessário.

3. Arquivos começando com `.` (tais como `.editorconfig`) são arquivos ocultos no macOS, então pressione **Command + Shift + .** para tornar o arquivo `.editorconfig` visível.

4. Selecione o arquivo `.editorconfig` e clique em **Abrir**:

    ![janela adicionando um novo campo](media/editorconfig-image3b.png)

5. Quando vir a seguinte caixa de diálogo, selecione a opção **Copiar o arquivo para o diretório** e selecione **OK**:

    ![Opções da caixa de diálogo Adicionar arquivo à pasta](media/editorconfig-image3.png)

### <a name="reflecting-editorconfig-settings"></a>Refletindo as configurações de .editorconfig

Depois de adicionar um arquivo EditorConfig a sua base de código, qualquer novo código adicionado é formatado automaticamente de acordo com as configurações especificadas. O código existente não reflete automaticamente as configurações, a menos que você formate a base de código.

Para refletir as configurações do arquivo `.editorconfig`, selecione o nó da solução e escolha **Editar > Formatar > Formatar Documento** na barra de menus:

![Formatar documento na barra de menus](media/editorconfig-image3a.png)

## <a name="editing-an-editorconfig-file"></a>Editando um arquivo EditorConfig

Os arquivos EditorConfig usam um layout de arquivo simples para especificar as configurações, que é explicado abaixo usando um exemplo anterior:

```EditorConfig
# This file is the top-most EditorConfig file
root = true

# All Files
[*]
indent_style = space
indent_size = 4
insert_final_newline = false
trim_trailing_whitespace = false

[*.cs]
csharp_new_line_before_open_brace = none
```

Definir `root` como `true` sinalizará este arquivo como o arquivo principal da base de código e arquivos `.editorconfig` superiores no projeto serão ignorados, conforme explicado na seção [Substituir configurações de EditorConfig](#override-editorconfig-settings).

Cada seção é indicada por chaves (**[ ]**) e especifica informações sobre os tipos de arquivos a que as propriedades seguintes devem se referir.

No exemplo acima, algumas configurações são aplicadas a todos os arquivos no projeto e outras são adicionadas apenas a arquivos C#. As capturas de tela abaixo mostram antes e depois de as configurações `.editorconfig` serem aplicadas:

**Antes**:

![Antes das configurações de editorconfig serem aplicadas](media/editorconfig-image4.png)

**Depois**:

![após as configurações de editorconfig serem aplicadas](media/editorconfig-image5.png)

Para obter mais informações sobre as configurações de EditorConfig disponíveis, consulte o artigo [Configurações de convenção de codificação do .NET para o EditorConfig](/visualstudio/ide/editorconfig-code-style-settings-reference) e a seção [Propriedades com suporte](http://editorconfig.org/#supported-properties) na documentação oficial.

## <a name="override-editorconfig-settings"></a>Substituir as configurações de EditorConfig

É possível ter mais de um arquivo `.editorconfig` em cada solução. O Visual Studio para Mac lê arquivos `.editorconfig` de cima para baixo na solução, adicionando e substituindo configurações conforme realiza tal leitura. Isso significa que as configurações no `.editorconfig` _mais próximo_ ao arquivo que você está editando terão precedência. As configurações são obtidas do `.editorconfig` na mesma pasta (se houver), do `.editorconfig` na pasta pai (se houver), e assim por diante até que `root=true` seja encontrado.

Se você quiser garantir que _nenhuma_ configuração de nenhum arquivo `.editorconfig` de nível superior seja aplicada a essa parte da base de código, adicione a propriedade `root=true` ao topo do arquivo `.editorconfig` de nível inferior:

```EditorConfig
# top-most EditorConfig file
root = true
```

## <a name="see-also"></a>Consulte também

- [Criar configurações do editor personalizado com o EditorConfig (Visual Studio no Windows)](/visualstudio/ide/create-portable-custom-editor-options)