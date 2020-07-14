---
title: Configurações de EditorConfig
ms.date: 08/01/2018
ms.topic: how-to
helpviewer_keywords:
- editorconfig [Visual Studio]
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: 30c2ce8a10a6a1001f8fb7c21ba7db7db7243fe4
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85770748"
---
# <a name="create-portable-custom-editor-settings-with-editorconfig"></a>Criar configurações do editor portátil e personalizado com o EditorConfig

Você pode adicionar um arquivo [EditorConfig](https://editorconfig.org/) ao seu projeto ou codebase para impor estilos de codificação consistentes para todos que trabalham na base de código. As configurações de EditorConfig têm precedência sobre as configurações do editor de texto global do Visual Studio. Isso significa que é possível personalizar cada base de código para usar as configurações de editor de texto específicas para esse projeto. Você ainda pode definir suas preferências pessoais editor na caixa de diálogo **Opções** do Visual Studio. Essas configurações se aplicam sempre que você estiver trabalhando em uma base de código sem um arquivo *. editorconfig* ou quando o arquivo *. editorconfig* não substituir uma configuração específica. Um exemplo de como essa preferência é o estilo de recuo&mdash;tabulações ou espaços.

As configurações do EditorConfig são compatíveis com vários editores de códigos e IDEs, incluindo o Visual Studio. Ele é um componente portátil que acompanha o seu código e pode impor estilos de codificação mesmo fora do Visual Studio.

::: moniker range=">=vs-2019"

Quando você adiciona um arquivo EditorConfig ao seu projeto no Visual Studio, novas linhas de código são formatadas de acordo com as configurações do EditorConfig. A formatação do código existente não será alterada, a menos que você execute um dos seguintes comandos:

 - [Limpeza de código](../ide/code-styles-and-code-cleanup.md) (**Ctrl** + **K**, **Ctrl** + **E**), que aplica qualquer configuração de espaço em branco, como estilo de recuo e configurações de estilo de código selecionadas, como classificar `using` diretivas.
 - **Editar** > **Avançado** > **Formate o documento** (ou **Ctrl** + **K**, **Ctrl** + **D** no perfil padrão), que aplica apenas as configurações de espaço em branco, como estilo de recuo.

 ::: moniker-end

::: moniker range="=vs-2017"

Quando você adiciona um arquivo EditorConfig ao seu projeto no Visual Studio, novas linhas de código são formatadas de acordo com as configurações do EditorConfig. A formatação do código existente não é alterada, a menos que você formate o documento (**edite**o documento de  >  **Advanced**  >  **formato** avançado ou **Ctrl** + **K**, **Ctrl** + **D** no perfil padrão). A formatação do documento afeta apenas as configurações de espaço em branco, como o estilo de recuo, a menos que você tenha configurado o documento de formato para [executar a limpeza de código adicional](../ide/code-styles-and-code-cleanup.md#apply-code-styles).

 ::: moniker-end

::: moniker range="vs-2017"

Você pode definir quais configurações do EditorConfig deseja que **Formatar Documento** aplique à [página de opções de **Formatação**](reference/options-text-editor-csharp-formatting.md#format-document-settings).

::: moniker-end

> [!NOTE]
> Este tópico aplica-se ao Visual Studio no Windows. Para o Visual Studio para Mac, confira [EditorConfig no Visual Studio para Mac](/visualstudio/mac/editorconfig).

## <a name="code-consistency"></a>Consistência do código

As configurações em arquivos EditorConfig permitem manter configurações e estilos de codificação consistentes em uma base de código, como estilo de recuo, largura de tabulação, caracteres de fim de linha, codificação e mais, independentemente do editor ou IDE usado. Por exemplo, ao codificar em C#, se sua codebase tiver uma Convenção para preferir que os recuos sempre consistam em cinco caracteres de espaço, os documentos usarão a codificação UTF-8 e cada linha sempre terminará com uma CR/LF, você poderá configurar um arquivo *. editorconfig* para fazer isso.

As convenções de codificação usadas em seus projetos pessoais podem ser diferentes das usadas nos projetos da sua equipe. Por exemplo, talvez você prefira que, quando estiver codificando, o recuo adicione um caractere de tabulação. No entanto, sua equipe pode preferir que o recuo adicione quatro caracteres de espaço em vez de um caractere de tabulação. Os arquivos EditorConfig resolvem esse problema permitindo que você tenha uma configuração para cada cenário.

Como as configurações estão contidas em um arquivo na base de código, elas viajam juntamente com essa base de código. Contanto que você abra o arquivo de código em um editor em conformidade com o EditorConfig, as configurações do editor de texto são implementadas. Para obter mais informações sobre arquivos EditorConfig, consulte o site [EditorConfig.org](https://editorconfig.org/).

> [!NOTE]
> As convenções definidas em um arquivo EditorConfig não podem ser aplicadas em um pipeline de CI/CD como erros ou avisos de build. Qualquer desvio de estilo aparece apenas no editor do Visual Studio e na **Lista de Erros**.

## <a name="supported-settings"></a>Configurações com suporte

O editor no Visual Studio é compatível com o conjunto principal de [propriedades do EditorConfig](https://editorconfig.org/#supported-properties):

- indent_style
- indent_size
- tab_width
- end\_of_line
- charset
- trim\_trailing_whitespace
- insert\_final_newline
- root

Há suporte para as configurações de editor do EditorConfig em todas as linguagens compatíveis com o Visual Studio, exceto para XML. Além disso, o EditorConfig dá suporte a convenções de [estilo de código](../ide/editorconfig-code-style-settings-reference.md) incluindo [linguagem](../ide/editorconfig-language-conventions.md), [formatação](../ide/editorconfig-formatting-conventions.md) e convenções de [nomenclatura](../ide/editorconfig-naming-conventions.md) para C# e Visual Basic.

## <a name="add-and-remove-editorconfig-files"></a>Adicionar e remover arquivos EditorConfig

Quando você adiciona um arquivo EditorConfig ao seu projeto ou base de código, as novas linhas de código que você escreve são formatadas de acordo com o arquivo EditorConfig. No entanto, a adição de um arquivo EditorConfig não converte os estilos existentes para os novos até que você formate o documento ou execute a [limpeza de código](../ide/code-styles-and-code-cleanup.md). Por exemplo, se você tiver recuos em seu arquivo formatados com tabulações e adicionar um arquivo EditorConfig com recuos com espaços, os caracteres de recuo não serão convertidos automaticamente em espaços. Ao Formatar o documento (**Editar**o documento de  >  **Advanced**  >  **formato** avançado ou **Ctrl** + **K**, **Ctrl** + **D**), as configurações de espaço em branco no arquivo EditorConfig são aplicadas a linhas de código existentes.

Se você remover um arquivo EditorConfig de seu projeto ou base de códigos e desejar que as novas linhas sejam formatadas de acordo com as configurações globais do editor, é preciso fechar e reabrir os arquivos de código abertos.

### <a name="add-an-editorconfig-file-to-a-project"></a>Adicionar um arquivo EditorConfig a um projeto

1. Abra um projeto ou uma solução no Visual Studio. Selecione o nó projeto ou solução, dependendo se suas configurações *. editorconfig* devem ser aplicadas a todos os projetos na solução ou apenas um. Você também pode selecionar uma pasta em seu projeto ou solução para adicionar o arquivo *. editorconfig* ao.

1. Na barra de menus, escolha **projeto**  >  **Adicionar novo item**ou pressione **Ctrl** + **Shift** + **A**.

   A caixa de diálogo **Adicionar Novo Item** é aberta.

1. Na caixa de pesquisa, pesquise **editorconfig**.

   Dois modelos de item de **Arquivo editorconfig** são mostrados nos resultados da pesquisa.

   ![Modelos de item do arquivo EditorConfig no Visual Studio](media/editorconfig-item-templates.png)

1. Selecione o modelo **Arquivo editorconfig (padrão)** para adicionar um arquivo EditorConfig pré-preenchido com duas opções principais do EditorConfig para tamanho e estilo de recuo. Ou selecione o modelo **Arquivo editorconfig (.NET)** para adicionar um arquivo EditorConfig pré-preenchido com [convenções de nomenclatura, formatação e estilo de código .NET](../ide/editorconfig-code-style-settings-reference.md).

   Um arquivo *. editorconfig* aparece em Gerenciador de soluções e é aberto no editor.

   ![Arquivo .editorconfig no Gerenciador de Soluções e editor](media/editorconfig-dotnet.png)

1. Edite o arquivo conforme o desejado.

### <a name="other-ways-to-add-an-editorconfig-file"></a>Outras formas de adicionar um arquivo EditorConfig

Há algumas outras maneiras de adicionar um arquivo EditorConfig ao seu projeto:

- O [recurso de inferência de código](/visualstudio/intellicode/code-style-inference) do IntelliCode para Visual Studio infere seus estilos de código com base no código existente. Ele cria um arquivo EditorConfig não vazio com suas preferências de estilo de código já definidas.

- A partir do Visual Studio 2019, você pode [gerar um arquivo EditorConfig com base em suas configurações de estilo de código](code-styles-and-code-cleanup.md#code-styles-in-editorconfig-files) em **Ferramentas** > **Opções**.

## <a name="file-hierarchy-and-precedence"></a>Precedência e hierarquia de arquivos

Quando você adiciona um arquivo *.editorconfig* a uma pasta em sua hierarquia de arquivos, as configurações se aplicam a todos os arquivos aplicáveis nesse nível e abaixo. Você também pode substituir as configurações de EditorConfig para um projeto específico, uma base de código ou parte de uma base de código, de modo que ele use convenções diferentes do que as outras partes da base de código. Isso pode ser útil quando você incorpora código de outro lugar e não quer alterar suas convenções.

Para substituir algumas ou todas as configurações de EditorConfig, adicione um arquivo *. EditorConfig* no nível da hierarquia de arquivos que você deseja aplicar a essas configurações substituídas. As novas configurações de arquivo do EditorConfig aplicam-se aos arquivos no mesmo nível e a todas as subpastas.

![Hierarquia do EditorConfig](../ide/media/vside_editorconfig_hierarchy.png)

Se você quiser substituir algumas, mas não todas, as configurações, especifique apenas essas configurações no arquivo *. editorconfig* . Somente as propriedades que você listar explicitamente no arquivo de nível inferior são substituídas. Outras configurações dos arquivos *. editorconfig* de nível superior continuam a ser aplicadas. Se você quiser garantir que _nenhuma_ configuração de _nenhum_ arquivo *. editorconfig* de nível superior seja aplicada a essa parte da base de código, adicione a ```root=true``` propriedade ao arquivo *. editorconfig* de nível inferior:

```ini
# top-most EditorConfig file
root = true
```

Os arquivos EditorConfig são lidos de cima para baixo. Se houver várias propriedades com o mesmo nome, a propriedade mais recente encontrada com esse nome terá precedência.

## <a name="edit-editorconfig-files"></a>Editar os arquivos EditorConfig

O Visual Studio ajuda a editar arquivos *.editorconfig* fornecendo listas de conclusão do IntelliSense.

![IntelliSense em um arquivo .editorconfig](media/editorconfig-intellisense-no-extension.png)

Depois de editar seu arquivo EditorConfig, será necessário recarregar seus arquivos de código para que as novas configurações entrem em vigor.

Se você editar vários arquivos *. editorconfig* , poderá encontrar a [extensão de serviço de idioma do editorconfig](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.EditorConfig) útil. Alguns dos recursos dessa extensão incluem realce de sintaxe, IntelliSense aprimorado, validação e formatação de código.

![IntelliSense com a extensão do serviço de linguagem do EditorConfig](media/editorconfig-intellisense.png)

## <a name="example"></a>Exemplo

O exemplo a seguir mostra o estado de recuo de um trecho de código C# antes e depois de adicionar um arquivo *. editorconfig* ao projeto. A configuração **Tabulações** na caixa de diálogo **Opções** do editor de texto do Visual Studio foi definida para produzir caracteres de espaço ao pressionar a tecla **Tab**.

![Configuração de tabulação do Editor de texto](../ide/media/vside_editorconfig_tabsetting.png)

Conforme esperado, pressionar a tecla **Tab** na próxima linha faz a linha recuar por meio da adição de quatro caracteres de espaço em branco.

![Codificar antes de usar o EditorConfig](../ide/media/vside_editorconfig_before.png)

Adicione um novo arquivo chamado *. editorconfig* ao projeto, com o conteúdo a seguir. A configuração `[*.cs]` significa que essa alteração se aplica somente a arquivos de código C# no projeto.

```ini
# Top-most EditorConfig file
root = true

# Tab indentation
[*.cs]
indent_style = tab
```

Agora, ao pressionar a tecla **TAB**, você obtém caracteres de tabulação em vez de espaços.

![A tecla Tab adiciona um caractere de tabulação](../ide/media/vside_editorconfig_tab.png)

## <a name="troubleshoot-editorconfig-settings"></a>Solução de problemas de configurações do EditorConfig

Se houver um arquivo do EditorConfig na estrutura do diretório no local do seu projeto ou acima desse local, o Visual Studio aplicará as configurações do editor nesse arquivo ao seu editor. Nesse caso, você verá a seguinte mensagem na barra de status:

   **"As preferências do usuário para esse tipo de arquivo foram substituídas pelas convenções de codificação desse projeto."**

Isso significa que, se qualquer configuração do editor em **ferramentas**  >  **Opções**  >  **Editor de texto** (como o tamanho do recuo e o estilo, o tamanho da guia ou as convenções de codificação) forem especificadas em um arquivo EditorConfig no projeto da estrutura de diretório, as convenções no arquivo EditorConfig substituirão as configurações em **Opções**. Você pode controlar esse comportamento ativando/desativando a opção **Seguir as convenções de codificação do projeto** em **Ferramentas** > **Opções** > **Editor de Texto**. Desmarcar a opção desliga o suporte do EditorConfig para Visual Studio.

![Opções de ferramentas – seguir as convenções de codificação do projeto](media/coding_conventions_option.png)

É possível encontrar arquivos *.editorconfig* em diretórios pai abrindo um prompt de comando e executando o seguinte comando na raiz do disco que contém seu projeto:

```Shell
dir .editorconfig /s
```

Você pode controlar o escopo de suas convenções EditorConfig definindo a ```root=true``` propriedade no arquivo *. EditorConfig* na raiz do seu repositório ou no diretório em que seu projeto reside. O Visual Studio procura um arquivo chamado *. editorconfig* no diretório do arquivo aberto e em cada diretório pai. A pesquisa termina quando atinge o filePath raiz ou se um arquivo *. editorconfig* com ```root=true``` é encontrado.

## <a name="see-also"></a>Confira também

- [Convenções de estilo de código do .NET](../ide/editorconfig-code-style-settings-reference.md)
- [Dando suporte ao EditorConfig para um serviço de linguagem](../extensibility/supporting-editorconfig.md)
- [EditorConfig.org](https://editorconfig.org/)
- [Recursos do editor de código](writing-code-in-the-code-and-text-editor.md)
- [EditorConfig (Visual Studio para Mac)](/visualstudio/mac/editorconfig)
