---
title: Opções, Editor de Texto, JavaScript, IntelliSense
ms.date: 10/29/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.JavaScript.Intellisense.References
- VS.ToolsOptionsPages.Text_Editor.JavaScript.Intellisense.General
- VS.ToolsOptionsPages.Text_Editor.TypeScript.IntelliSense.General
ms.assetid: b4a9816d-cf87-4dc6-a8d4-1591d6a48103
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 742d6394975b6920218579e1b4652bb2e99c479c
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50670774"
---
# <a name="options-text-editor-javascript-intellisense"></a>Opções, Editor de Texto, JavaScript, IntelliSense
Use a página **IntelliSense** da caixa de diálogo **Opções** para modificar as configurações que afetam o comportamento do IntelliSense para JavaScript. É possível acessar a página **IntelliSense** escolhendo **Ferramentas** > **Opções** na barra de menus e, em seguida, expandindo **Editor de texto** > **JavaScript** > **IntelliSense.**

[!INCLUDE[note_settings_general](../../data-tools/includes/note_settings_general_md.md)]

A página **IntelliSense** contém as seguintes seções:

## <a name="statement-completion"></a>Preenchimento de declaração
 Você pode usar essas opções para alterar o comportamento do preenchimento de declaração do IntelliSense.

### <a name="uielement-list"></a>Lista UIElement
 **Usar apenas Tab ou Enter para confirmar**

 Quando você marca essa caixa de seleção, o editor de código do JavaScript acrescenta instruções com itens selecionados na lista de conclusão somente após você escolher a tecla **Tab** ou **Enter**. Quando você desmarca essa caixa de seleção, outros caracteres, como ponto, vírgula, dois-pontos, parênteses de abertura e chave de abertura ({), também podem acrescentar instruções com os itens selecionados.

## <a name="references"></a>Referências
 Você pode usar essas opções para especificar os tipos de arquivo .js do IntelliSense que estão no escopo de diferentes tipos de projeto JavaScript. Geralmente, as referências do IntelliSense são usadas para oferecer suporte a objetos globais do IntelliSense. Também é possível usar essa página para definir a ordem de carregamento de scripts que devem ser carregados no tempo de execução e para adicionar arquivos de extensão do IntelliSense.

### <a name="uielement-list"></a>Lista UIElement
 **Grupos de referências**

 Essa opção especifica o tipo do grupo de referência. Há suporte para três grupos de referência:

 Você pode usar grupos de referência predefinidos para especificar se determinados arquivos .js do IntelliSense estão no escopo para diferentes projetos JavaScript. Quatro grupos de referência estão disponíveis:

- Implícitos (*versão* do Windows) para aplicativos [!INCLUDE[win8_appname_long](../../debugger/includes/win8_appname_long_md.md)] usando JavaScript. Os arquivos incluídos nesse grupo estão no escopo de cada arquivo .js aberto no Editor de Códigos para aplicativos do [!INCLUDE[win8_appname_long](../../debugger/includes/win8_appname_long_md.md)] que usam JavaScript.

- Implícito (Web), para projetos HTML5. Os arquivos incluídos nesse grupo estão no escopo de cada arquivo .js aberto no Editor de Códigos para esses tipos de projeto.

- Grupos de referência de atividade dedicada, para web workers HTML5. Os arquivos especificados nesse grupo estão no escopo de arquivos .js que têm uma referência explícita a um grupo de referência de atividade dedicada.

- Genérico, para outros tipos de projeto JavaScript.

**Arquivos incluídos**

Essa opção especifica a ordem na qual os arquivos são carregados no contexto do serviço de linguagem. Você pode configurar a ordem usando os botões **Remover**, **Subir** e **Descer**. Para que o IntelliSense funcione corretamente, um arquivo que depende de outro deve ser carregado depois do outro arquivo.

> [!CAUTION]
> Se um objeto for definido incondicionalmente em duas ou mais referências implícitas, a última referência nessa lista será usada para definir o objeto.


**Adicionar uma referência ao grupo**

Essa opção fornece uma maneira de adicionar arquivos .js extras do IntelliSense navegando até os arquivos apropriados.

**Baixar referências remotas (por exemplo, http://) para arquivos no projeto de arquivos diversos**

Quando essa caixa de seleção for marcada e se você tiver um arquivo JavaScript aberto fora do contexto de um projeto, o Visual Studio baixará os arquivos JavaScript remotos referenciados no arquivo com a finalidade de fornecer informações do IntelliSense. Se essa opção for selecionada, os arquivos serão baixados quando você incluí-los como uma referência no seu arquivo JavaScript.

> [!NOTE]
> Em projetos Web, os arquivos remotos referenciados no seu projeto são baixados por padrão.



## <a name="see-also"></a>Consulte também

- [JavaScript IntelliSense](../../ide/javascript-intellisense.md)