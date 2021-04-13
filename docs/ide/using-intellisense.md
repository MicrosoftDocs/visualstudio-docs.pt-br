---
title: Informações do parâmetro, listar membros e informações rápidas
description: 'Saiba como usar estes recursos do IntelliSense: listar Membros, informações de parâmetro, informações rápidas e palavra completa.'
ms.custom: SEO-VS-2020
ms.date: 05/25/2018
ms.topic: conceptual
f1_keywords:
- vc.tools.intellisense
helpviewer_keywords:
- Quick info
- Parameter info
- Complete word
- List members
- IntelliSense [Visual Studio]
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 0e6b984a9f885f137cf387837a242cc1207e45ae
ms.sourcegitcommit: 52b093e000334f53d87c6165d1418347e4f45dec
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/09/2021
ms.locfileid: "107221712"
---
# <a name="intellisense-in-visual-studio"></a>IntelliSense no Visual Studio

O IntelliSense é uma ajuda de preenchimento de código que inclui inúmeras funcionalidades: Listar Membros, Informações do Parâmetro, Informações Rápidas e Completar Palavra. Essas funcionalidades ajudam você a aprender mais sobre o código que está usando, a manter o acompanhamento dos parâmetros que está digitando e a adicionar chamadas a métodos e propriedades pressionando apenas algumas teclas.

Vários aspectos do IntelliSense são específicos do idioma. Para obter mais informações sobre o IntelliSense para diferentes idiomas, consulte os tópicos listados na seção [Consulte também](#see-also).

## <a name="list-members"></a>Listar Membros

Uma lista de membros válidos de um tipo (ou namespace) aparece depois que você digita um caractere disparador (por exemplo, um ponto (`.`) no código gerenciado ou `::` em C++). Se você continuar a digitar caracteres, a lista será filtrada para incluir somente os membros que começam com esses caracteres ou aqueles em que o início de *qualquer* palavra do nome começar com esses caracteres. O IntelliSense também realiza a correspondência de "palavras concatenadas", para que você possa digitar apenas a primeira letra de cada palavra concatenada no nome do membro para ver as correspondências.

Após selecionar um item, você poderá inseri-lo em seu código pressionando **Tab** ou inserindo um espaço. Se você selecionar um item e digitar um ponto, o item aparecerá seguido pelo ponto, que abrirá outra lista de membros. Ao selecionar um item, mas antes de inseri-lo, você obtém a Informação Rápida do item.

Na lista de membros, o ícone à esquerda representa o tipo do membro, como namespace, classe, função ou variável. Para obter uma lista de ícones, consulte [Modo de Exibição de Classe e ícones do Pesquisador de Objetos](../ide/class-view-and-object-browser-icons.md). A lista pode ser muito longa, de modo que você pode pressionar **PgUp** e **PgDn** para mover para cima ou para baixo na lista.

![Lista de membros do Visual Studio](../ide/media/vs2015_intellisense.png)

Você pode invocar o recurso **listar Membros** manualmente digitando **Ctrl** + **J**, escolhendo **Editar**  >    >  **membros da lista** do IntelliSense ou escolhendo o botão **listar Membros** na barra de ferramentas do editor. Quando é invocada em uma linha em branco ou fora de um escopo reconhecível, a lista exibe símbolos no namespace global.

Para desativar os membros da lista por padrão (para que ele não apareça, a menos que seja especificamente invocado), vá para **ferramentas**  >  **Opções**  >  **todos os idiomas** e desmarque **listar Membros automaticamente**. Se você deseja desligar Listar Membros somente para uma linguagem específica, vá para as configurações **Gerais** dessa linguagem.

Você também pode alterar para o modo de sugestão, no qual apenas o texto que você digita é inserido no código. Por exemplo, se você inserir um identificador que não está na lista e pressionar a **Guia**, no modo de preenchimento, a entrada poderá substituir o identificador digitado. Para alternar entre o modo de conclusão e o modo de sugestão, pressione **Ctrl** + **ALT** + **espaço** ou escolha **Editar**  >    >  **modo de conclusão de alternância** do IntelliSense.

## <a name="parameter-info"></a>Informações de Parâmetro

Informações de Parâmetro fornecem informações sobre o número, os nomes e os tipos de parâmetros exigidos por um método, um parâmetro de tipo genérico de atributo (em C#) ou um modelo (em C++).

O parâmetro em negrito indica o próximo parâmetro que é necessário à medida que você digita a função. Para funções sobrecarregadas, use as teclas de direção **Para Cima** e **Para Baixo** para exibir informações de parâmetro alternativas para as sobrecargas de função.

![Informações de Parâmetro](../ide/media/vs2015_param_info.png)

Quando você anota funções e parâmetros com comentários da Documentação XML, os comentários são exibidos como Informações do Parâmetro. Para obter mais informações, consulte [Fornecer comentários de código XML](reference/generate-xml-documentation-comments.md).

Você pode invocar manualmente informações de parâmetro escolhendo **Editar**  >  informações de  >  **parâmetro** do IntelliSense, pressionando **Ctrl** + **Shift** + **espaço** ou escolhendo o botão **informações do parâmetro** na barra de ferramentas do editor.

## <a name="quick-info"></a>Informação Rápida

Informação Rápida exibe a declaração completa de qualquer identificador no seu código.

![Informações rápidas sobre o Visual Studio](../ide/media/vs2015_quick_info.png)

Quando você seleciona um membro na caixa **Listar Membros**, as Informações Rápidas também são exibidas.

![Informações do parâmetro em um arquivo de código C&#35;](../ide/media/vs2015_paraminfo.png)

Você pode invocar manualmente informações rápidas escolhendo **Editar**  >    >  **informações rápidas** do IntelliSense, pressionando **Ctrl** + **K**, **Ctrl** + **I** ou escolhendo o botão **informações rápidas** na barra de ferramentas do editor.

Se uma função estiver sobrecarregada, o IntelliSense não poderá exibir informações de todos os formulários da sobrecarga.

Você pode ativar as informações rápidas para o código C++ navegando até **ferramentas**  >  **Opções**  >  **Editor de texto**  >  **C/C++**  >  **avançado** e definindo **informações rápidas automáticas** para `false` .

## <a name="complete-word"></a>Completar Palavra

Completar Palavra completa o restante de uma variável, um comando ou um nome de função uma vez que você tenha inserido caracteres suficientes para remover ambiguidades do termo. Você pode invocar a palavra completa escolhendo **Editar**  >  **IntelliSense**  >  **Complete Word**, pressionando **Ctrl** + **espaço** ou escolhendo o botão **concluir palavra** na barra de ferramentas do editor.

## <a name="intellisense-options"></a>Opções do IntelliSense

As opções do IntelliSense são ativadas por padrão. Para desativá-las, escolha **ferramentas**  >  **Opções**  >  **Editor de texto** e desmarque **informações de parâmetro** ou **membros de lista automática** se você não quiser o recurso membros da lista.

## <a name="intellisense-icons"></a>Ícones do IntelliSense
Os ícones no IntelliSense podem transmitir significado adicional com modificadores de ícone. Esses são estrelas, corações e cadeados sobrepostos ao ícone do objeto e que transmitem, respectivamente, os significados de protegido, interno ou privado.

|    ícone    |    Acessibilidade    |    Descrição    |
|------------|--------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|
| ![Modificador de ícone público](../ide/media/intellisensePublicNoModifier.png)       |    Classe pública    |    O acesso não é restrito.   |
| ![Modificador de ícone protegido](../ide/media/intellisenseProtectedModifier.png)       |    Classe protegida    |    O acesso é limitado à classe que os contém ou aos tipos derivados da classe que os contém.    |
| ![Modificador de ícone interno protegido](../ide/media/intellisenseProtectedInternalModifier.png)       |    Classe interna protegida    |    O acesso é limitado ao assembly atual ou aos tipos derivados da classe que os contém.    |
| ![Modificador de ícone interno](../ide/media/intellisenseInternalModifier.png)       |    Classe interna    |    O acesso é limitado ao assembly atual.    |
|![Modificador de ícone privado](../ide/media/intellisensePrivateModifier.png)        |    Classe privada    |    O acesso é limitado à classe que o contém ou a tipos derivados da classe que o contém no assembly atual. (Disponível desde o C# 7.2.)    |

## <a name="troubleshoot-intellisense&quot;></a>Solução de problemas do IntelliSense

As opções do IntelliSense podem não funcionar como você espera em alguns casos.

**O cursor está abaixo de um erro de código.** Talvez não seja possível usar o IntelliSense se uma função incompleta ou outro erro existirem no código acima do cursor, pois o IntelliSense talvez não possa analisar os elementos do código. Você pode resolver esse problema comentando o código aplicável.

**O cursor está em um comentário de código.** Não será possível usar o IntelliSense se o cursor estiver em um comentário no arquivo de origem.

**O cursor está em um literal de cadeia de caracteres.** Não será possível usar o IntelliSense se o cursor estiver entre aspas em um literal de cadeia de caracteres, como no exemplo a seguir:

```cpp
MessageBox( hWnd, &quot;String literal|")
```

**As opções automáticas estão desativadas.** Por padrão, o IntelliSense funciona automaticamente, mas é possível desabilitar isso. Mesmo se o preenchimento automático de declaração for desabilitado, é possível invocar um recurso IntelliSense.

## <a name="see-also"></a>Veja também

- [Visual Basic IntelliSense](../ide/visual-basic-specific-intellisense.md)
- [C# IntelliSense](../ide/visual-csharp-intellisense.md)
- [IntelliSense do Python](../python/editing-python-code-in-visual-studio.md#intellisense)
- [JavaScript IntelliSense](../ide/javascript-intellisense.md)
- [Escrever e refatorar o código (C++)](/cpp/ide/writing-and-refactoring-code-cpp)
- [Fornecer comentários de código XML](reference/generate-xml-documentation-comments.md)
