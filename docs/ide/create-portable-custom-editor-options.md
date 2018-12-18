---
title: Usando as configurações do EditorConfig no Visual Studio
ms.date: 08/01/2018
ms.topic: conceptual
helpviewer_keywords:
- editorconfig [Visual Studio]
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.openlocfilehash: 244312646de83e935dfa84cde4a9b793eb01a76f
ms.sourcegitcommit: bc43970c000f07c9cc2051f1264a9742943a9755
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51349709"
---
# <a name="create-portable-custom-editor-settings-with-editorconfig"></a>Criar configurações do editor portátil e personalizado com o EditorConfig

No Visual Studio de 2017, você pode adicionar um arquivo [EditorConfig](http://editorconfig.org/) ao seu projeto ou base de código para impor estilos de codificação consistente para todas as pessoas que trabalham na base de código. As configurações de EditorConfig têm precedência sobre as configurações do editor de texto global do Visual Studio. Isso significa que é possível personalizar cada base de código para usar as configurações de editor de texto específicas para esse projeto. Você ainda pode definir suas preferências pessoais editor na caixa de diálogo **Opções** do Visual Studio. Essas configurações serão aplicadas sempre que você estiver trabalhando em uma base de código sem um arquivo *.editorconfig* ou quando o arquivo *.editorconfig* não substituir determinada configuração. Um exemplo de como essa preferência é o estilo de recuo&mdash;tabulações ou espaços.

As configurações do EditorConfig são compatíveis com vários editores de códigos e IDEs, incluindo o Visual Studio. Ele é um componente portátil que acompanha o seu código e pode impor estilos de codificação mesmo fora do Visual Studio.

Quando você adiciona um arquivo EditorConfig ao projeto no Visual Studio, a formatação do código existente não é alterada, a menos que você formate o documento (**Editar** > **Avançado**  >  **Formatar Documento** ou **Ctrl**+**K**, **Ctrl**+**D** no perfil padrão). No entanto, novas linhas de código serão formatadas de acordo com as configurações do EditorConfig. Você pode definir quais configurações do EditorConfig deseja que **Formatar Documento** aplique à [página de opções de **Formatação**](reference/options-text-editor-csharp-formatting.md#format-document-settings).

> [!NOTE]
> Este tópico aplica-se ao Visual Studio no Windows. Para o Visual Studio para Mac, confira [EditorConfig no Visual Studio para Mac](/visualstudio/mac/editorconfig).

## <a name="coding-consistency"></a>Consistência de codificação

As configurações em arquivos EditorConfig permitem manter configurações e estilos de codificação consistentes em uma base de código, como estilo de recuo, largura de tabulação, caracteres de fim de linha, codificação e mais, independentemente do editor ou IDE usado. Por exemplo, ao codificar em C#, se sua base de código tiver uma convenção de preferir que os recuos sempre sejam compostos por cinco caracteres de espaço, que os documentos usem codificação UTF-8 e que cada linha sempre termine com uma CR/LF, será possível configurar um arquivo *.editorconfig* para fazer isso.

As convenções de codificação usadas em seus projetos pessoais podem ser diferentes das usadas nos projetos da sua equipe. Por exemplo, talvez você prefira que, quando estiver codificando, o recuo adicione um caractere de tabulação. No entanto, sua equipe pode preferir que o recuo adicione quatro caracteres de espaço em vez de um caractere de tabulação. Os arquivos EditorConfig resolvem esse problema permitindo que você tenha uma configuração para cada cenário.

Como as configurações estão contidas em um arquivo na base de código, elas viajam juntamente com essa base de código. Contanto que você abra o arquivo de código em um editor em conformidade com o EditorConfig, as configurações do editor de texto são implementadas. Para obter mais informações sobre arquivos EditorConfig, consulte o site [EditorConfig.org](http://editorconfig.org/).

> [!NOTE]
> As convenções definidas em um arquivo EditorConfig não podem ser aplicadas em um pipeline de CI/CD como erros ou avisos de build. Qualquer desvio de estilo aparece apenas no editor do Visual Studio e na **Lista de Erros**.

## <a name="supported-settings"></a>Configurações com suporte

O editor no Visual Studio é compatível com o conjunto principal de [propriedades do EditorConfig](http://editorconfig.org/#supported-properties):

- indent_style
- indent_size
- tab_width
- end\_of_line
- charset
- trim\_trailing_whitespace
- insert\_final_newline
- raiz

Há suporte para as configurações de editor do EditorConfig em todas as linguagens compatíveis com o Visual Studio, exceto para XML. Além disso, o EditorConfig dá suporte ao [estilo de código](../ide/editorconfig-code-style-settings-reference.md) e convenções de [nomenclatura](../ide/editorconfig-naming-conventions.md) para C# e Visual Basic.

## <a name="adding-and-removing-editorconfig-files"></a>Adicionando e removendo arquivos EditorConfig

Adicionar um arquivo EditorConfig ao seu projeto ou base de código não converte os estilos existentes em novos. Por exemplo, se você tiver recuos em seu arquivo formatados com tabulações e adicionar um arquivo EditorConfig com recuos com espaços, os caracteres de recuo não serão convertidos automaticamente em espaços. No entanto, novas linhas de código serão formatadas de acordo com o arquivo EditorConfig. Além disso, se você formatar o documento (**Editar** > **Avançado** > **Formatar Documento** ou **Ctrl**+**K**, **Ctrl**+**D**), as configurações no arquivo EditorConfig serão aplicadas às linhas de código existentes.

Se você remover um arquivo EditorConfig do seu projeto ou da base de código, será necessário fechar e reabrir os arquivos de código aberto a serem revertidos para as configurações globais do editor para novas linhas de código.

### <a name="to-add-an-editorconfig-file-to-a-project-or-solution"></a>Para adicionar um arquivo EditorConfig em um projeto ou uma solução

1. Abra um projeto ou uma solução no Visual Studio. Selecione o nó do projeto ou da solução, dependendo se as configurações de *.editorconfig* tiverem que ser aplicadas a todos os projetos na solução ou a apenas um. Também é possível selecionar uma pasta no projeto ou na solução para adicionar o arquivo *.editorconfig*.

1. Na barra de menus, escolha **Projeto** > **Adicionar Novo Item** ou pressione **Ctrl**+**Shift**+**A**.

   A caixa de diálogo **Adicionar Novo Item** é aberta.

1. Nas categorias à esquerda, escolha **Geral** e, em seguida, escolha o modelo **Arquivo de Texto**. Na caixa de texto **Nome**, insira `.editorconfig` e, em seguida, escolha **Adicionar**.

   Um arquivo *.editorconfig* aparece no Gerenciador de Soluções e é aberto no editor.

   ![Arquivo .editorconfig no Gerenciador de Soluções](media/editorconfig-in-solution-explorer.png)

1. Edite o arquivo conforme o desejado, por exemplo:

   ```EditorConfig
   root = true

   [*.{cs,vb}]
   indent_size = 4
   trim_trailing_whitespace = true

   [*.cs]
   csharp_new_line_before_open_brace = methods
   ```

### <a name="other-ways-to-add-an-editorconfig-file"></a>Outras formas de adicionar um arquivo EditorConfig

Há algumas outras maneiras de adicionar um arquivo EditorConfig ao seu projeto:

- Instale a [extensão do serviço de linguagem do EditorConfig](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.EditorConfig) para adicionar mais facilmente um arquivo *.editorconfig* vazio ao seu projeto. Depois de instalar essa extensão, basta escolher **Adicionar** > **Arquivo .editorconfig** no menu de contexto ou no menu acionado com o botão direito do mouse do nó da solução, do nó do projeto ou de qualquer pasta no **Gerenciador de Soluções**. Essa extensão também melhora a experiência de edição do arquivo *.editorconfig*.

   ![Adicionar o arquivo .editorconfig com extensão](media/editorconfig-extension-add.png)

- Experimente a [extensão do IntelliCode](/visualstudio/intellicode/intellicode-visual-studio). Essa extensão experimental infere os estilos de código a partir do código existente e, em seguida, cria um arquivo *.editorconfig* não vazio com suas preferências de estilo de código já definidas.

## <a name="override-editorconfig-settings"></a>Substituir as configurações do EditorConfig

Quando você adiciona um arquivo *.editorconfig* a uma pasta em sua hierarquia de arquivos, as configurações se aplicam a todos os arquivos aplicáveis nesse nível e abaixo. Você também pode substituir as configurações de EditorConfig para um projeto específico, uma base de código ou parte de uma base de código, de modo que ele use convenções diferentes do que as outras partes da base de código. Isso pode ser útil quando você incorpora código de outro lugar e não quer alterar suas convenções.

Para substituir algumas ou todas as configurações do EditorConfig, adicione um arquivo *.editorconfig* no nível da hierarquia de arquivos em que você deseja aplicar essas configurações substituídas. As novas configurações de arquivo do EditorConfig aplicam-se aos arquivos no mesmo nível e a todas as subpastas.

![Hierarquia do EditorConfig](../ide/media/vside_editorconfig_hierarchy.png)

Se você quiser substituir algumas, mas não todas as configurações, especifique essas configurações no arquivo *.editorconfig*. Somente as propriedades que você listar explicitamente no arquivo de nível inferior são substituídas. As outras configurações de arquivos .*.editorconfig* de nível superior continuam sendo aplicadas. Se você quiser garantir que _nenhuma_ configuração de _nenhum_ arquivo *.editorconfig* de nível superior seja aplicada a essa parte da base de código, adicione a propriedade ```root=true``` ao arquivo *.editorconfig* de nível inferior:

```EditorConfig
# top-most EditorConfig file
root = true
```

Os arquivos do EditorConfig são lidos de cima para baixo e os arquivos do EditorConfig mais próximos são lidos por último. As convenções de seções do EditorConfig correspondentes são aplicadas na ordem em que foram lidas, portanto as convenções dos arquivos mais próximos têm precedência.

## <a name="editing-editorconfig-files"></a>Editando arquivos EditorConfig

O Visual Studio ajuda a editar arquivos *.editorconfig* fornecendo listas de conclusão do IntelliSense.

![IntelliSense em um arquivo .editorconfig](media/editorconfig-intellisense-no-extension.png)

Depois de editar seu arquivo EditorConfig, será necessário recarregar seus arquivos de código para que as novas configurações entrem em vigor.

Se você edita vários arquivos *.editorconfig*, a [Extensão do Serviço de Linguagem do EditorConfig](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.EditorConfig) pode ser útil. Alguns dos recursos dessa extensão incluem realce de sintaxe, IntelliSense aprimorado, validação e formatação de código.

![IntelliSense com a extensão do serviço de linguagem do EditorConfig](media/editorconfig-intellisense.png)

## <a name="example"></a>Exemplo

O exemplo a seguir mostra o estado de recuo de um snippet de código C# antes e depois de adicionar um arquivo *.editorconfig* ao projeto. A configuração **Tabulações** na caixa de diálogo **Opções** do editor de texto do Visual Studio foi definida para produzir caracteres de espaço ao pressionar a tecla **Tab**.

![Configuração de tabulação do Editor de texto](../ide/media/vside_editorconfig_tabsetting.png)

Conforme esperado, pressionar a tecla **Tab** na próxima linha faz a linha recuar por meio da adição de quatro caracteres de espaço em branco.

![Codificar antes de usar o EditorConfig](../ide/media/vside_editorconfig_before.png)

Adicione um novo arquivo chamado *.editorconfig* ao projeto, com o conteúdo a seguir. A configuração `[*.cs]` significa que essa alteração se aplica somente a arquivos de código C# no projeto.

```EditorConfig
# Top-most EditorConfig file
root = true

# Tab indentation
[*.cs]
indent_style = tab
```

Agora, ao pressionar a tecla **TAB**, você obtém caracteres de tabulação em vez de espaços.

![A tecla Tab adiciona um caractere de tabulação](../ide/media/vside_editorconfig_tab.png)

## <a name="troubleshooting-editorconfig-settings"></a>Solução de problemas de configurações do EditorConfig

Se houver um arquivo do EditorConfig na estrutura do diretório no local do seu projeto ou acima desse local, o Visual Studio aplicará as configurações do editor nesse arquivo ao seu editor. Nesse caso, você verá a seguinte mensagem na barra de status:

   **"As preferências do usuário para esse tipo de arquivo foram substituídas pelas convenções de codificação desse projeto."**

Isso significa que, se as configurações do editor em **Ferramentas** > **Opções** > **Editor de Texto** (como tamanho e estilo do recuo, tamanho da tabulação ou convenções de codificação) forem especificadas em um arquivo EditorConfig no projeto ou acima dele na estrutura de diretório, as convenções no arquivo EditorConfig substituirão as configurações em **Opções**. Você pode controlar esse comportamento ativando/desativando a opção **Seguir as convenções de codificação do projeto** em **Ferramentas** > **Opções** > **Editor de Texto**. Desmarcar a opção desliga o suporte do EditorConfig para Visual Studio.

![Opções de ferramentas – seguir as convenções de codificação do projeto](media/coding_conventions_option.png)

É possível encontrar arquivos *.editorconfig* em diretórios pai abrindo um prompt de comando e executando o seguinte comando na raiz do disco que contém seu projeto:

```Shell
dir .editorconfig /s
```

Você pode controlar o escopo das convenções do EditorConfig configurando a propriedade ```root=true``` no arquivo *.editorconfig* na raiz do seu repositório ou no diretório em que o projeto reside. O Visual Studio procurará um arquivo chamado *.editorconfig* no diretório do arquivo aberto e em todos os diretórios pai. A pesquisa terminará quando atingir o caminho do arquivo raiz ou se um arquivo *.editorconfig* com ```root=true``` for encontrado.

## <a name="see-also"></a>Consulte também

- [Convenções de estilo de código do .NET](../ide/editorconfig-code-style-settings-reference.md)
- [Convenções de Nomenclatura do .NET](../ide/editorconfig-naming-conventions.md)
- [Dando suporte ao EditorConfig para um serviço de linguagem](../extensibility/supporting-editorconfig.md)
- [EditorConfig.org](http://editorconfig.org/)
- [Recursos do Editor de Códigos](writing-code-in-the-code-and-text-editor.md)
- [EditorConfig (Visual Studio para Mac)](/visualstudio/mac/editorconfig)