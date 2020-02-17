---
title: Opções, Editor de Texto, C/C++, Experimental
ms.date: 08/02/2017
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.C/C++.Experimental
- VS.ToolsOptionsPages.Text_Editor.C%2FC%2B%2B.Experimental
- VS.ToolsOptionsPages.Text_Editor.C\C++.Experimental
author: corob-msft
ms.author: corob
manager: markl
ms.workload:
- cplusplus
ms.openlocfilehash: 7e239ad3d2091f334f18ec00a367fc47d5c21db3
ms.sourcegitcommit: 68f893f6e472df46f323db34a13a7034dccad25a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2020
ms.locfileid: "77278706"
---
# <a name="options-text-editor-cc-experimental"></a>Opções, Editor de Texto, C/C++, Experimental

Ao alterar essas opções, você pode alterar o comportamento relacionado ao IntelliSense e ao banco de dados de navegação quando estiver programando em C ou C++. Essas funcionalidades são realmente experimentais e podem ser modificadas ou removidas do Visual Studio em uma versão futura.

::: moniker range="vs-2017"

Este artigo descreve as opções no Visual Studio 2017. Para o Visual Studio 2015, selecione **2015** no seletor acima do sumário.

::: moniker-end

Para acessar esta página de propriedades, pressione **Ctrl**+**Q** para ativar a caixa de pesquisa e, em seguida, digite **experimental**. A Pesquisa encontra a página após as primeiras letras. Acesse-a também escolhendo **Ferramentas** > **Opções** e expandindo **Editor de Texto**, em seguida, **C/C++** e escolhendo **Experimental**.

Essas funcionalidades estão disponíveis em uma instalação do Visual Studio.

> [!NOTE]
> Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Consulte [Personalizar o IDE do Visual Studio](../../ide/personalizing-the-visual-studio-ide.md).

## <a name="enable-predictive-intellisense"></a>Habilitar IntelliSense Preditivo

O IntelliSense Preditivo limita o número de resultados exibidos na lista suspensa do IntelliSense para que você veja apenas os resultados relevantes no contexto. Por exemplo, se você digitar `int x =` e invocar a lista suspensa do IntelliSense, verá apenas inteiros ou funções que retornam inteiros. O IntelliSense Preditivo está desativado por padrão.

::: moniker range="vs-2017"

## <a name="enable-faster-project-load"></a>Habilitar carregamento de projeto mais rápido

No Visual Studio 2017 versão 15.3 em diante, essa funcionalidade é chamada **Habilitar Cache de Projeto** e foi movida para a página de propriedades [Configurações de Projeto do VC++](vcpp-project-settings-projects-and-solutions-options-dialog-box.md).

Essa opção permite que o Visual Studio coloque em cache os dados de projeto, para quando você abrir o projeto na próxima vez, ele pode carregar esses dados armazenados em cache em vez de recalcular dos arquivos de projeto. Usar dados armazenados em cache pode acelerar significativamente o tempo de carregamento do projeto.

::: moniker-end

## <a name="additional-features-in-the-visual-studio-marketplace"></a>Recursos adicionais no Visual Studio Marketplace

Você pode procurar outros recursos do editor de texto no [Visual Studio Marketplace](https://marketplace.visualstudio.com/search?target=VS&category=Tools&vsVersion=&subCategory=All&sortBy=Downloads). Um exemplo é [C++ Quick Fixes](https://marketplace.visualstudio.com/items?itemName=VisualCppDevLabs.CQuickFixes2017) (Correções Rápidas C++), que dá suporte ao seguinte:

- **Add missing #include (Adicionar #include ausente)** –sugere #include relevantes para símbolos desconhecidos no seu código

- **Add using namespace/Fully qualify symbol (Adicionar usando namespace/símbolo totalmente qualificado)** – semelhante ao item anterior, mas para namespaces

- **Add missing semicolon (adicionar ponto e vírgula ausente)**

- **Ajuda online** – pesquise mensagens de erro na ajuda online

- E muito mais...

## <a name="see-also"></a>Confira também

- [Configurando opções do editor específicas a um idioma](../../ide/reference/setting-language-specific-editor-options.md)
- [Refatoração em C++ (VC Blog)](https://devblogs.microsoft.com/cppblog/all-about-c-refactoring-in-visual-studio-2015-preview/
)
