---
title: Comandos | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Visual Studio, commands
- commands, Visual Studio
- command syntax
ms.assetid: 76ffa394-ee89-4629-aba9-1a62b72e6cc1
caps.latest.revision: 23
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 91c04ad161e17ac2932ca8e75ddadfc1c2879785
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53053098"
---
# <a name="visual-studio-commands"></a>Comandos do Visual Studio
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]


Os comandos do Visual Studio permitem invocar um comando na janela **Comando**, janela **Imediato** ou na caixa **Localizar/Comando**. Em cada caso, o sinal maior que (`>`) é usado para indicar que um comando deve ser seguido em vez de uma operação de pesquisa ou de depuração.

 É possível encontrar uma lista completa de comandos e sua sintaxe na caixa de diálogo **Teclado, Opções de Ambiente**.

 O caractere de escape para comandos do Visual Studio é um caractere de circunflexo (^), que significa que o caractere imediatamente depois dele é interpretado literalmente, em vez de interpretado como um caractere de controle. Isso pode ser usado para inserir aspas retas ("), espaços, barras iniciais, acentos circunflexos ou quaisquer outros caracteres literais em um parâmetro ou valor de opção, com a exceção de nomes de opção. Por exemplo,

```
>Edit.Find ^^t /regex
```

 Um acento circunflexo funciona da mesma forma tanto dentro quanto fora das aspas. Se um acento circunflexo for o último caractere na linha, ele será ignorado.

 Em versões localizadas do IDE, os nomes de comando podem ser inseridos na linguagem nativa do IDE ou em inglês. Por exemplo, é possível digitar `File.NewFile` ou `Fichier.NouveauFichier` no IDE francês para executar o mesmo comando.

 Muitos comandos têm aliases. Para obter uma lista de aliases de comando, consulte [Aliases de comando do Visual Studio](../../ide/reference/visual-studio-command-aliases.md).

 Os comandos a seguir têm argumentos e/ou opções.

|Nome do comando|Descrição|
|------------------|-----------------|
|[Add Existing Item](../../ide/reference/add-existing-item-command.md)|Adiciona um arquivo existente à solução atual e abre-o.|
|[Add Existing Project](../../ide/reference/add-existing-project-command.md)|Adiciona um projeto existente à solução atual.|
|[Add New Item](../../ide/reference/add-new-item-command.md)|Adiciona um novo item de solução, como um .htm, .css, .txt ou conjunto de quadros à solução atual e a abre.|
|[Alias](../../ide/reference/alias-command.md)|Cria um novo alias para um comando completo, comando e argumentos completos ou até mesmo outro alias.|
|[Evaluate Statement](../../ide/reference/evaluate-statement-command.md)|Avalia e exibe a instrução fornecida.|
|[Find](../../ide/reference/find-command.md)|Pesquisa arquivos usando um subconjunto das opções disponíveis no controle **Localizar e Substituir**.|
|[Localizar em Arquivos](../../ide/reference/find-in-files-command.md)|Pesquisa arquivos usando um subconjunto das opções disponíveis em [Localizar e Substituir](../../ide/find-in-files.md).|
|[Ir para](../../ide/reference/go-to-command.md)|Move o cursor para a linha especificada.|
|[List Call Stack](../../ide/reference/list-call-stack-command.md)|Exibe a pilha de chamadas atual.|
|[List Disassembly](../../ide/reference/list-disassembly-command.md)|Inicia o processo de depuração e permite que você especifique como os erros são tratados.|
|[List Memory](../../ide/reference/list-memory-command.md)|Exibe o conteúdo do intervalo de memória especificado.|
|[List Modules](../../ide/reference/list-modules-command.md)|Lista os módulos do processo atual.|
|[List Registers](../../ide/reference/list-registers-command.md)|Exibe uma lista de registros.|
|[List Source](../../ide/reference/list-source-command.md)|Exibe as linhas de código-fonte especificadas.|
|[List Threads](../../ide/reference/list-threads-command.md)|Exibe uma lista dos threads no programa atual.|
|[Log Command Window Output](../../ide/reference/log-command-window-output-command.md)|Copia todas as entradas e saídas da janela Comando para um arquivo.|
|[New File](../../ide/reference/new-file-command.md)|Cria um novo arquivo e o adiciona ao projeto atualmente selecionado.|
|[Open File](../../ide/reference/open-file-command.md)|Abre um arquivo existente e permite que você especifique um editor.|
|[Open Project](../../ide/reference/open-project-command.md)|Abre um projeto existente e permite que você o adicione à solução atual.|
|[Open Solution](../../ide/reference/open-solution-command.md)|Abre uma solução existente.|
|[Imprimir](../../ide/reference/print-command.md)|Avalia a expressão e exibe os resultados ou o texto especificado.|
|[Comando Quick Watch](../../ide/reference/quick-watch-command.md)|Exibe o texto selecionado ou especificado no campo **Expressão** da caixa de diálogo **Inspeção Rápida**.|
|[Replace](../../ide/reference/replace-command.md)|Substitui texto em arquivos usando um subconjunto das opções disponíveis no controle **Localizar e Substituir**.|
|[Substituir nos Arquivos](../../ide/reference/replace-in-files-command.md)|Substitui texto em arquivos usando um subconjunto das opções disponíveis em [Substituir nos Arquivos](../../ide/replace-in-files.md).|
|[Set Current Stack Frame](../../ide/reference/set-current-stack-frame-command.md)|Permite que você exiba um registro de ativação específico.|
|[Set Current Thread](../../ide/reference/set-current-thread-command.md)|Permite que você exiba um thread específico.|
|[Set Radix](../../ide/reference/set-radix-command.md)|Determina o número de bytes a ser exibido.|
|[Shell](../../ide/reference/shell-command.md)|Inicia programas de dentro do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] como se o comando tivesse sido executado no prompt de comando.|
|[Comando ShowWebBrowser](../../ide/reference/showwebbrowser-command.md)|Exibe a URL especificada em uma janela de navegador da Web, tanto dentro do IDE (ambiente de desenvolvimento integrado) ou externa ao IDE.|
|[Iniciar](../../ide/reference/start-command.md)|Inicia o processo de depuração e permite que você especifique como os erros são tratados.|
|[Path](../../ide/reference/symbol-path-command.md)|Define a lista de diretórios para o depurador pesquisar símbolos.|
|[Toggle Breakpoint](../../ide/reference/toggle-breakpoint-command.md)|Ativa ou desativa o ponto de interrupção dependendo de seu estado atual, no local atual do arquivo.|
|[Comando Watch](../../ide/reference/watch-command.md)|Cria e abre uma instância especificada de uma janela **Inspeção**.|

## <a name="see-also"></a>Consulte também
 [Janela de comando](../../ide/reference/command-window.md) [caixa Localizar/comando](../../ide/find-command-box.md) [Aliases de comando do Visual Studio](../../ide/reference/visual-studio-command-aliases.md)
