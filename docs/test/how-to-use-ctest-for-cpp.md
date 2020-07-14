---
title: Como usar o CTest para C++
ms.date: 01/23/2020
ms.topic: how-to
ms.author: corob
manager: jillfra
ms.workload:
- cplusplus
author: corob-msft
ms.openlocfilehash: c429c9e676ead54bb9f168e3220bf2d4791fac63
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85287227"
---
# <a name="how-to-use-ctest-for-c-in-visual-studio-2017-and-later"></a>Como usar o CTest para C++ no Visual Studio 2017 e posterior

O CMake (que inclui o CTest) está integrado por padrão ao IDE do Visual Studio como um componente da carga de trabalho **Desenvolvimento para desktop com C++**. Se você precisar instalá-lo em seu computador, abra o programa Instalador do Visual Studio, clique no botão **Desenvolvimento de área de trabalho com o C++** e clique em **Modificar**. Selecione as **ferramentas CMake de C++ para Windows** na lista de componentes de carga de trabalho.

## <a name="to-write-tests"></a>Para escrever testes

O suporte de CMake no Visual Studio não envolve o sistema de projetos do Visual Studio. Portanto, você grava e configura testes CTest exatamente como faria em qualquer ambiente CMake. Use o `enable_testing()` comando para habilitar o teste e o `add_test()` `gtest_discover_tests()` comando ou para adicionar um novo teste. Para saber mais sobre o CTest, consulte a [documentação do cmake](https://gitlab.kitware.com/cmake/community/wikis/doc/ctest/Testing-With-CTest). 

Para saber mais sobre como usar o CMake no Visual Studio, confira [Projetos CMake no Visual Studio](/cpp/build/cmake-projects-in-visual-studio).

## <a name="to-run-tests"></a>Para executar testes

O CTest é totalmente integrado ao **Gerenciador de Testes** e também dá suporte às estruturas de teste de unidade Google e Boost. Essas estruturas estão incluídas por padrão como componentes na carga de trabalho **Desenvolvimento para desktop com C++**. No entanto, se você estiver atualizando um projeto de uma versão anterior do Visual Studio, talvez seja necessário instalar essas estruturas usando o programa Instalador do Visual Studio.

A ilustração a seguir mostra os resultados de uma execução de CTest usando a estrutura do Google Test:

![CTest com o Google Test Framework no Visual Studio](media/ctest-test-explorer.png)

Se você estiver usando CTest, mas não os adaptadores do Google ou Boost, verá resultados no nível de CTest em vez do nível de método de teste individual. Você pode depurar e percorrer executáveis apenas de CTest, mas os rastreamentos de pilha em testes individuais não têm suporte.

## <a name="see-also"></a>Veja também

- [Escrever testes de unidade para C/C++](writing-unit-tests-for-c-cpp.md)
