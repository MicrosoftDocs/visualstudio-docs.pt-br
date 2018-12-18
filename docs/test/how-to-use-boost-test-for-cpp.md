---
title: Como usar o Boost.Test para C++ no Visual Studio
ms.date: 01/29/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.topic: conceptual
author: mikeblome
ms.author: mblome
manager: douge
ms.workload:
- cplusplus
ms.openlocfilehash: eebefa7b4033de5acec313e241d13cddab7120fa
ms.sourcegitcommit: 495bba1d8029646653f99ad20df2f80faad8d58b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39380444"
---
# <a name="how-to-use-boosttest-for-c-in-visual-studio"></a>Como usar o Boost.Test para C++ no Visual Studio

No **Visual Studio 2017 versão 15.5** e posterior, o adaptador de teste Boost.Test está integrado ao IDE do Visual Studio como um componente da carga de trabalho **Desenvolvimento para desktop com C++**.

![Adaptador de Teste para Boost.Test](media/cpp-boost-component.png)

Se a carga de trabalho **Desenvolvimento para desktop com C++** não estiver instalada, abra o **Instalador do Visual Studio** e selecione **Modificar**. Selecione a carga de trabalho **Desenvolvimento para desktop com C++** e escolha o botão **Modificar**.

## <a name="install-boost"></a>Instalar o Boost

O Boost.Test exige o [Boost](http://www.boost.org/)! Se o Boost não estiver instalado, recomendamos o uso do gerenciador de pacotes Vcpkg.

1. Siga as instruções de [Vcpkg: um gerenciador de pacotes C++ para o Windows](/cpp/vcpkg) para instalar o vcpkg (caso ainda não o tenha).

1. Instale a biblioteca Boost.Test dinâmica ou estática:

    - Execute **vcpkg install boost-test** para instalar a biblioteca dinâmica Boost.Test.

       -OU-

    - Execute **vcpkg install boost-test:x86-windows-static** para instalar a biblioteca estática Boost.Test.

1. Execute **vcpkg integrate install** para configurar o Visual Studio com a biblioteca e incluir caminhos para os cabeçalhos e os binários do Boost.

## <a name="add-the-item-template-visual-studio-2017-version-156-and-later"></a>Adicionar o modelo de item (Visual Studio 2017 versão 15.6 e posterior)

1. Para criar um arquivo *.cpp* para os testes, no **Gerenciador de Soluções**, clique com o botão direito do mouse no nó do projeto e escolha **Adicionar Novo Item**.

   ![Modelo de item Boost.Test](media/boost_test_item_template.png)

1. O novo arquivo contém um método de teste de exemplo. Compile o projeto para habilitar o **Gerenciador de Testes** e descobrir o método.

O modelo de item usa a variante de cabeçalho único do Boost.Test, mas você pode modificar o caminho #include a fim de usar a variante de biblioteca autônoma. Para saber mais, confira [Adicionar diretivas de inclusão](#add-include-directives).

## <a name="create-a-test-project-visual-studio-2017-version-155"></a>Criar um projeto de teste (Visual Studio 2017 versão 15.5)

No Visual Studio 2017 versão 15.5, não há nenhum modelo de projeto de teste ou de item pré-configurado disponível para o Boost.Test. Portanto, é necessário criar e configurar um projeto de aplicativo de console para armazenar seus testes.

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse no nó da solução e escolha **Adicionar** > **Novo Projeto**.

1. No painel esquerdo, escolha **Visual C++** > **Windows Desktop** e, em seguida, selecione o modelo **Aplicativo de Console do Windows**.

1. Nomeie o projeto e escolha **OK**.

1. Exclua a função `main` do arquivo *.cpp*.

1. Se você estiver usando a versão da biblioteca de cabeçalho único ou dinâmica de Boost.Test, vá até [Adicionar diretivas de inclusão](#add-include-directives). Se você estiver usando a versão da biblioteca estática, será necessário realizar outras configurações:

   a. Para editar o arquivo de projeto, primeiro descarregue-o. No **Gerenciador de Soluções**, clique com o botão direito do mouse no nó do projeto e escolha **Descarregar Projeto**. Em seguida, clique com o botão direito do mouse no nó do projeto e escolha **Editar <name\>.vcxproj**.

   b. Adicione duas linhas no grupo de propriedades **Globais**, como é mostrado aqui:

    ```xml
    <PropertyGroup Label="Globals">
    ....
        <VcpkgTriplet>x86-windows-static</VcpkgTriplet>
        <VcpkgEnabled>true</VcpkgEnabled>
    </PropertyGroup>
    ```
   c. Salve e feche o arquivo *\*.vcxproj* e, em seguida, recarregue o projeto.

   d. Para abrir a **Páginas de Propriedades**, clique com o botão direito do mouse no nó do projeto e escolha **Propriedades**.

   d. Expanda **C/C++** > **Geração de Código** e, em seguida, selecione **Biblioteca em Tempo de Execução**. Selecione **/MTd** para depurar a biblioteca de tempo de execução estática ou **/MT** para liberar a biblioteca de tempo de execução estática.

   f. Expanda **Vinculador** > **Sistema**. Verifique se **Subsistema** está definido como **Console**.

   g. Escolha **OK** para fechar as páginas de propriedades.

## <a name="add-include-directives"></a>Adicionar diretivas de inclusão

1. No arquivo *.cpp* de teste, adicione as diretivas `#include` necessárias para que os tipos e as funções do programa fiquem visíveis para o código de teste. Normalmente, o programa está um nível acima na hierarquia de pastas. Se você digitar `#include "../"`, uma janela do IntelliSense será exibida e permitirá que você selecione o caminho completo para o arquivo de cabeçalho.

   ![Adicionar diretivas de #inclusão](media/cpp-gtest-includes.png)

   Você pode usar a biblioteca autônoma com:

   ```cpp
   #include <boost/test/unit_test.hpp>
   ```

   Ou, use a versão de cabeçalho único com:

   ```cpp
   #include <boost/test/included/unit_test.hpp>
   ```

   Em seguida, defina `BOOST_TEST_MODULE`.

O exemplo a seguir é suficiente para que o teste seja detectável no **Gerenciador de Testes**:

```cpp
#define BOOST_TEST_MODULE MyTest
#include <boost/test/included/unit_test.hpp\> //single-header
#include "../MyProgram/MyClass.h" // project being tested
#include <string>

BOOST_AUTO_TEST_CASE(my_boost_test)
{
    std::string expected_value = "Bill";

    // assume MyClass is defined in MyClass.h
    // and get_value() has public accessibility
    MyClass mc;
    BOOST_CHECK(expected_value == mc.get_value());
}
```

## <a name="write-and-run-tests"></a>Gravar e executar testes

Agora, você está pronto para escrever e executar testes do Boost. Confira a [documentação da Biblioteca do Boost Test](http://www.boost.org/doc/libs/release/libs/test/doc/html/index.html) para obter informações sobre as macros de teste. Consulte [Executar testes de unidade com o Gerenciador de Testes](run-unit-tests-with-test-explorer.md) para saber mais sobre como descobrir, executar e agrupar testes usando o **Gerenciador de Testes**.

## <a name="see-also"></a>Consulte também

- [Escrever testes de unidade para C/C++](writing-unit-tests-for-c-cpp.md)
