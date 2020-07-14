---
title: Como usar o Google Test para C++
description: Use o Google Test para criar testes de unidade do C++ no Visual Studio.
ms.date: 05/06/2017
ms.topic: how-to
ms.author: corob
manager: markl
ms.workload:
- cplusplus
author: corob-msft
ms.openlocfilehash: bf4db1c01fc79d32f7e498c265b74dec34f67e48
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85287240"
---
# <a name="how-to-use-google-test-for-c-in-visual-studio"></a>Como usar o Google Test para C++ no Visual Studio

No Visual Studio 2017 e versões posteriores, o Google Test está integrado ao IDE do Visual Studio como componente padrão da carga de trabalho **Desenvolvimento de área de trabalho com o C++**. Para verificar se ele está instalado no seu computador, abra o Instalador do Visual Studio e localize o Google Test na lista de componentes de carga de trabalho:

![Instalar o Google Test](media/cpp-google-component.png)

::: moniker range="vs-2019"

## <a name="add-a-google-test-project-in-visual-studio-2019"></a>Adicionar um projeto do Google Test no Visual Studio 2019

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse no nó da solução e escolha **Adicionar** > **Novo projeto**.
2. Defina **Linguagem de programação** como **C++** e digite **teste** na caixa de pesquisa. Na lista de resultados, escolha **Projeto do Google Test**.
3. Dê um nome ao projeto de teste e clique em **OK**.

![Novo projeto do Google Test](media/vs-2019/cpp-gtest-new-project-vs2019.png)

::: moniker-end

::: moniker range="vs-2017"

## <a name="add-a-google-test-project-in-visual-studio-2017"></a>Adicionar um projeto do Google Test no Visual Studio 2017

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse no nó da solução e escolha **Adicionar** > **Novo projeto**.
2. No painel esquerdo, escolha **Visual C++** > **Teste** e, em seguida, escolha **Projeto do Google Test** no painel central.
3. Dê um nome ao projeto de teste e clique em **OK**.

![Novo projeto do Google Test](media/cpp-gtest-new-project.png)

::: moniker-end

## <a name="configure-the-test-project"></a>Configurar o projeto de teste

Na caixa de diálogo **Configuração do Projeto de Teste** exibida, escolha o projeto que deseja testar. Ao escolher um projeto, o Visual Studio adiciona uma referência ao projeto selecionado. Se nenhum projeto for escolhido, então, será necessário adicionar as referências manualmente ao(s) projeto(s) que você deseja testar. Ao escolher entre a vinculação estática e dinâmica para os binários do Google Test, as considerações são as mesmas de qualquer programa do C++. Para saber mais, consulte [DLLs no Visual C++](/cpp/build/dlls-in-visual-cpp).

![Configurar projeto do Google Test](media/cpp-gtest-config.png)

## <a name="set-additional-options"></a>Definir opções adicionais

No menu principal, escolha **ferramentas**  >  **Opções**  >  **adaptador de teste para Google Test** para definir opções adicionais. Consulte a documentação do Google Test para saber mais sobre essas configurações.

![Configurações de projeto do Google Test](media/cpp-gtest-settings.png)

## <a name="add-include-directives"></a>Adicionar diretivas de inclusão

No arquivo test *. cpp* , adicione as diretivas necessárias `#include` para tornar os tipos e as funções do programa visíveis para o código de teste. Normalmente, o programa está um nível acima na hierarquia de pastas. Se você digitar `#include "../"`, uma janela do IntelliSense será exibida e permitirá que você selecione o caminho completo para o arquivo de cabeçalho.

![Adicionar diretivas de #inclusão](media/cpp-gtest-includes.png)

## <a name="write-and-run-tests"></a>Gravar e executar testes

Agora, você está pronto para gravar e executar testes no Google Test. Consulte o [Google Test primer](https://github.com/google/googletest/blob/master/googletest/docs/primer.md) para obter informações sobre as macros de teste. Consulte [Executar testes de unidade com o Gerenciador de Testes](run-unit-tests-with-test-explorer.md) para saber mais sobre como descobrir, executar e agrupar testes usando o **Gerenciador de Testes**.

## <a name="see-also"></a>Veja também

[Escrever testes de unidade para C/C++](writing-unit-tests-for-c-cpp.md)
