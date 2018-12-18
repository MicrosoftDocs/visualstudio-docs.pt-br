---
title: Informações do parâmetro, listar membros e informações rápidas
ms.date: 05/25/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vc.tools.intellisense
helpviewer_keywords:
- Quick info
- Parameter info
- Complete word
- List members
- IntelliSense [Visual Studio]
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 5e00b43f1705079a86d511239d7b38119868d8f4
ms.sourcegitcommit: 58052c29fc61c9a1ca55a64a63a7fdcde34668a4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34748469"
---
# <a name="intellisense-in-visual-studio"></a>IntelliSense no Visual Studio

O IntelliSense é uma ajuda de preenchimento de código que inclui inúmeras funcionalidades: Listar Membros, Informações do Parâmetro, Informações Rápidas e Completar Palavra. Essas funcionalidades ajudam você a aprender mais sobre o código que está usando, a manter o acompanhamento dos parâmetros que está digitando e a adicionar chamadas a métodos e propriedades pressionando apenas algumas teclas.

Vários aspectos do IntelliSense são específicos do idioma. Para obter mais informações sobre o IntelliSense para diferentes idiomas, consulte os tópicos listados na seção [Consulte também](#see-also).

## <a name="list-members"></a>Listar Membros

Uma lista de membros válidos de um tipo (ou namespace) aparece depois que você digita um caractere disparador (por exemplo, um ponto (`.`) no código gerenciado ou `::` em C++). Se você continuar a digitar caracteres, a lista será filtrada para incluir somente os membros que começam com esses caracteres ou aqueles em que o início de *qualquer* palavra do nome começar com esses caracteres. O IntelliSense também realiza a correspondência de "palavras concatenadas", para que você possa digitar apenas a primeira letra de cada palavra concatenada no nome do membro para ver as correspondências.

Após selecionar um item, você poderá inseri-lo em seu código pressionando **Tab** ou inserindo um espaço. Se você selecionar um item e digitar um ponto, o item aparecerá seguido pelo ponto, que abrirá outra lista de membros. Ao selecionar um item, mas antes de inseri-lo, você obtém a Informação Rápida do item.

Na lista de membros, o ícone à esquerda representa o tipo do membro, como namespace, classe, função ou variável. Para obter uma lista de ícones, consulte [Modo de Exibição de Classe e ícones do Pesquisador de Objetos](../ide/class-view-and-object-browser-icons.md). A lista pode ser muito longa, de modo que você pode pressionar **PgUp** e **PgDn** para mover para cima ou para baixo na lista.

![Lista de membros do Visual Studio](../ide/media/vs2015_intellisense.png)

Invoque o recurso **Listar Membros** manualmente digitando **Ctrl**+**J**, escolhendo **Editar** > **IntelliSense** > **Listar Membros** ou escolhendo o botão **Listar Membros** na barra de ferramentas do editor. Quando é invocada em uma linha em branco ou fora de um escopo reconhecível, a lista exibe símbolos no namespace global.

Para desativar Listar Membros por padrão (para que ele não seja exibido, exceto se invocado especificamente), acesse **Ferramentas** > **Opções** > **Todas as linguagens** e desmarque **Listar membros automaticamente**. Se você deseja desligar Listar Membros somente para uma linguagem específica, vá para as configurações **Gerais** dessa linguagem.

Você também pode alterar para o modo de sugestão, no qual apenas o texto que você digita é inserido no código. Por exemplo, se você inserir um identificador que não está na lista e pressionar a **Guia**, no modo de preenchimento, a entrada poderá substituir o identificador digitado. Para alternar entre o modo de preenchimento e o modo de sugestão, pressione **Ctrl**+**Alt**+**Espaço** ou escolha **Editar** > **IntelliSense** > **Ativar/Desativar Modo de Preenchimento**.

## <a name="parameter-info"></a>Informações de Parâmetro

Informações de Parâmetro fornecem informações sobre o número, os nomes e os tipos de parâmetros exigidos por um método, um parâmetro de tipo genérico de atributo (em C#) ou um modelo (em C++).

O parâmetro em negrito indica o próximo parâmetro que é necessário à medida que você digita a função. Para funções sobrecarregadas, use as teclas de direção **Para Cima** e **Para Baixo** para exibir informações de parâmetro alternativas para as sobrecargas de função.

![Informações de Parâmetro](../ide/media/vs2015_param_info.png)

Quando você anota funções e parâmetros com comentários da Documentação XML, os comentários são exibidos como Informações do Parâmetro. Para obter mais informações, consulte [Fornecer comentários de código XML](../ide/supplying-xml-code-comments.md).

Invoque a opção Informações do Parâmetro manualmente escolhendo **Editar** > **IntelliSense** > **Informações do Parâmetro**, pressionando **Ctrl**+**Shift**+**Espaço** ou escolhendo o botão **Informações do Parâmetro** na barra de ferramentas do editor.

## <a name="quick-info"></a>Informação Rápida

Informação Rápida exibe a declaração completa de qualquer identificador no seu código.

![Informações rápidas sobre o Visual Studio](../ide/media/vs2015_quick_info.png)

Quando você seleciona um membro na caixa **Listar Membros**, as Informações Rápidas também são exibidas.

![Informações do parâmetro em um arquivo de código C&#35;](../ide/media/vs2015_paraminfo.png)

É possível invocar Informações Rápidas ao selecionar **Editar** > **IntelliSense** > **Informações Rápidas**, pressionar **Ctrl**+**I** ou escolher o botão **Informações Rápidas** na barra de ferramentas do editor.

Se uma função estiver sobrecarregada, o IntelliSense não poderá exibir informações de todos os formulários da sobrecarga.

É possível invocar desativar as informações rápidas para o código C++ ao navegar em **Ferramentas** > **Opções** > **Editor de Texto** > **C/C++** > **Avançado** e configurar as **Informações Rápidas Automáticas** para `false`.

## <a name="complete-word"></a>Completar Palavra

Completar Palavra completa o restante de uma variável, um comando ou um nome de função uma vez que você tenha inserido caracteres suficientes para remover ambiguidades do termo. É possível invocar Completar Palavra ao selecionar **Editar** > **IntelliSense** > **Completar Palavra**, pressionar **Ctrl**+**Espaço** ou ao escolher o botão **Completar Palavra** na barra de ferramentas do editor.

## <a name="intellisense-options"></a>Opções do IntelliSense

As opções do IntelliSense são ativadas por padrão. Para desativá-las, escolha **Ferramentas** > **Opções** > **Editor de Texto** e desmarque a seleção **Informações do parâmetro** ou **Listar membros automaticamente** se você não deseja o recurso Listar Membros.

## <a name="troubleshoot-intellisense"></a>Solução de problemas do IntelliSense

As opções do IntelliSense podem não funcionar como você espera em alguns casos.

**O cursor está abaixo de um erro de código.** Talvez não seja possível usar o IntelliSense se uma função incompleta ou outro erro existirem no código acima do cursor, pois o IntelliSense talvez não possa analisar os elementos do código. Você pode resolver esse problema comentando o código aplicável.

**O cursor está em um comentário de código.** Não será possível usar o IntelliSense se o cursor estiver em um comentário no arquivo de origem.

**O cursor está em um literal de cadeia de caracteres.** Não será possível usar o IntelliSense se o cursor estiver entre aspas em um literal de cadeia de caracteres, como no exemplo a seguir:

```cpp
MessageBox( hWnd, "String literal|")
```

**As opções automáticas estão desativadas.** Por padrão, o IntelliSense funciona automaticamente, mas é possível desabilitar isso. Mesmo se o preenchimento automático de declaração for desabilitado, é possível invocar um recurso IntelliSense.

## <a name="see-also"></a>Consulte também

- [IntelliSense do Visual Basic](../ide/visual-basic-specific-intellisense.md)
- [C# IntelliSense](../ide/visual-csharp-intellisense.md)
- [JavaScript IntelliSense](../ide/javascript-intellisense.md)
- [Escrever e refatorar o código (C++)](/cpp/ide/writing-and-refactoring-code-cpp)
- [Fornecer comentários de código XML](../ide/supplying-xml-code-comments.md)