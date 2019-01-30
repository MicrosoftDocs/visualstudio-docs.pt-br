---
title: Como usar o CTest para C++
ms.date: 11/07/2017
ms.prod: visual-studio-dev15
ms.topic: conceptual
ms.author: mblome
manager: jillfra
ms.workload:
- cplusplus
author: mikeblome
ms.openlocfilehash: 51338b594819fc8b162498b0bbcf2ac0ad9dc662
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "54930713"
---
# <a name="how-to-use-ctest-for-c-in-visual-studio"></a>Como usar o CTest para C++ no Visual Studio

O CMake (que inclui o CTest) está integrado por padrão ao IDE do Visual Studio como um componente da carga de trabalho **Desenvolvimento para desktop com C++**. Caso precise instalá-lo no computador, abra o programa Instalador do Visual Studio, clique no botão **Modificar** e, em seguida, marque [Ferramentas CMake para Visual C++](/cpp/ide/cmake-tools-for-visual-cpp) na lista de componentes de carga de trabalho.

## <a name="to-write-tests"></a>Para escrever testes

O suporte de CMake no Visual Studio não envolve o sistema de projetos do Visual Studio. Portanto, você grava e configura testes CTest exatamente como faria em qualquer ambiente CMake. Para obter mais informações sobre o uso do CMake no Visual Studio, confira [Ferramentas CMake para Visual C++](/cpp/ide/cmake-tools-for-visual-cpp).

## <a name="to-run-tests-visual-studio-2017-version-156"></a>Para executar testes (Visual Studio 2017 versão 15.6)

No Visual Studio 2017 versão 15.6, o CTest é totalmente integrado ao **Gerenciador de Testes** e também oferece suporte a estruturas de teste de unidade do Google e Boost. Essas estruturas estão incluídas por padrão como componentes na carga de trabalho **Desenvolvimento para desktop com C++**. No entanto, se você estiver atualizando um projeto de uma versão anterior do Visual Studio, talvez seja necessário instalar essas estruturas usando o programa Instalador do Visual Studio.

A ilustração a seguir mostra os resultados de uma execução de CTest usando a estrutura do Google Test:

![CTest com a Estrutura do Google Test no VS2017 15.6](media/ctest-test-explorer.png)

Se você estiver usando CTest, mas não os adaptadores do Google ou Boost, verá resultados no nível de CTest em vez do nível de método de teste individual. Você pode depurar e percorrer executáveis apenas de CTest, mas os rastreamentos de pilha em testes individuais não têm suporte.

## <a name="to-run-tests-visual-studio-2017-version-155"></a>Para executar testes (Visual Studio 2017 versão 15.5)

No **Visual Studio 2017 versão 15.5**, o CTest não está integrado ao **Gerenciador de Testes**. É possível executar os testes pelo menu principal CMake ou pelo menu do clique com o botão direito em um arquivo *CMakeLists.txt* no **Gerenciador de Soluções**. Os resultados de teste são direcionados para a **Janela de Saída** do Visual Studio.

![Executar testes de CTest no VS2017 15.5](media/cpp-cmake-run-tests.png)

## <a name="see-also"></a>Consulte também

[Escrever testes de unidade para C/C++](writing-unit-tests-for-c-cpp.md)