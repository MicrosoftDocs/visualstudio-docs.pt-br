---
title: Como usar o Boost.Test para C++
description: Use o Boost.Test para criar testes de unidade no Visual Studio.
ms.date: 01/29/2020
ms.topic: how-to
author: corob-msft
ms.author: corob
manager: markl
ms.workload:
- cplusplus
ms.openlocfilehash: 34c593469a586d1314c7ee52f3aeb3ab6faf334c
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85287266"
---
# <a name="how-to-use-boosttest-for-c-in-visual-studio"></a>Como usar o Boost.Test para C++ no Visual Studio

No Visual Studio 2017 e versões posteriores, o adaptador de teste Boost. Test é integrado ao IDE do Visual Studio. É um componente do desenvolvimento de **desktop com** carga de trabalho de C++.

![Adaptador de Teste para Boost.Test](media/cpp-boost-component.png)

Se você não tiver a carga de trabalho **Desenvolvimento para desktop com C++** instalada, abra o **Instalador do Visual Studio**. Selecione a carga de trabalho **Desenvolvimento para desktop com C++** e escolha o botão **Modificar**.

## <a name="install-boost"></a>Instalar o Boost

O Boost.Test exige o [Boost](https://www.boost.org/)! Se você não tiver o Boost instalado, recomendamos o uso do Gerenciador de pacotes do Vcpkg.

1. Siga as instruções em [Vcpkg: um Gerenciador de pacotes do C++ para Windows](/cpp/vcpkg) para instalar o Vcpkg (se você ainda não o tiver).

1. Instale a biblioteca Boost.Test dinâmica ou estática:

    - Execute `vcpkg install boost-test` para instalar a biblioteca Boost.Test dinâmica.

       -OU-

    - Execute `vcpkg install boost-test:x86-windows-static` para instalar a biblioteca Boost.Test estática.

1. Execute `vcpkg integrate install` para configurar o Visual Studio com a biblioteca e incluir caminhos para os cabeçalhos e os binários do Boost.

Você tem a opção de configurar seus testes em sua solução no Visual Studio: você pode incluir seu código de teste no projeto em teste, ou você pode criar um projeto de teste separado para seus testes. Ambas as opções têm vantagens e desvantagens.

## <a name="add-tests-inside-your-project"></a>Adicionar testes dentro do seu projeto

No Visual Studio 2017 versão 15,6 e posterior, você pode adicionar um modelo de item para testes em seu projeto. Tanto os testes quanto o seu código residem no mesmo projeto. Você precisará criar uma configuração de compilação separada para gerar uma compilação de teste. E você precisará manter os testes fora de suas compilações de depuração e de versão.

No Visual Studio 2017 versão 15.5, não há nenhum modelo de projeto de teste ou de item pré-configurado disponível para o Boost.Test. Use as instruções para criar e configurar um projeto de teste separado.

### <a name="create-a-boosttest-item"></a>Criar um item Boost. Test

1. Para criar um arquivo *. cpp* para seus testes, clique com o botão direito do mouse no nó do projeto em **Gerenciador de soluções** e escolha **Adicionar**  >  **novo item**.

1. Na caixa de diálogo **Adicionar novo item** , expanda **instalado**  >  **Visual C++**  >  **teste**. Selecione **Boost. Test**e, em seguida, escolha **Adicionar** para adicionar *Test. cpp* ao seu projeto.

   ![Modelo de item Boost.Test](media/boost_test_item_template.png)

O novo arquivo *Test. cpp* contém um exemplo de método de teste. Esse arquivo é onde você pode incluir seus próprios arquivos de cabeçalho e gravar testes para seu aplicativo.

O arquivo de teste também usa macros para definir uma nova `main` rotina para configurações de teste. Se você criar seu projeto agora, verá um erro LNK2005, como "_main já definido em Main. obj".

### <a name="create-and-update-build-configurations"></a>Criar e atualizar configurações de compilação

1. Para criar uma configuração de teste, na barra de menus, selecione **criar**  >  **Configuration Manager**. Na caixa de diálogo **Configuration Manager** , abra a lista suspensa em **configuração da solução ativa** e escolha **nova**. Na caixa de diálogo **nova configuração de solução** , insira um nome como "debug UnitTests". Em **copiar configurações de** selecionar **depuração**e, em seguida, escolha **OK**.

1. Exclua o código de teste de suas configurações de depuração e versão: em **Gerenciador de soluções**, clique com o botão direito do mouse em Test. cpp e selecione **Propriedades**. Na caixa de diálogo **páginas de propriedades** , selecione **todas as configurações** na lista suspensa **configuração** . Selecione **Propriedades de configuração**  >  **geral** e abra o menu suspenso da propriedade **de compilação excluído de** . Selecione **Sim**e, em seguida, escolha **aplicar** para salvar as alterações.

1. Para incluir o código de teste em sua configuração de UnitTests de depuração, na caixa de diálogo **páginas de propriedades** , selecione **depurar UnitTests** no menu suspenso **configuração** . Selecione **não** na propriedade **de compilação excluída de** e escolha **OK** para salvar as alterações.

1. Exclua o código principal de sua configuração de UnitTests de depuração. Em **Gerenciador de soluções**, clique com o botão direito do mouse no arquivo que contém sua `main` função e selecione **Propriedades**. Na caixa de diálogo **páginas de propriedades** , selecione **depurar UnitTests** no menu suspenso de **configuração** . Selecione **Propriedades de configuração**  >  **geral** e abra o menu suspenso da propriedade **de compilação excluído de** . Selecione **Sim**e escolha **OK** para salvar as alterações.

1. Defina a configuração da solução para **depurar UnitTests**e, em seguida, crie seu projeto para habilitar o **Gerenciador de testes** para descobrir o método.

Desde que o nome da configuração que você criar comece com as palavras "debug" ou "Release", o Boost correspondente. as bibliotecas de teste serão selecionadas automaticamente.

O modelo de item usa a variante de cabeçalho único do Boost.Test, mas você pode modificar o caminho #include a fim de usar a variante de biblioteca autônoma. Para saber mais, confira [Adicionar diretivas de inclusão](#add-include-directives).

## <a name="create-a-separate-test-project"></a>Criar um projeto de teste separado

Em muitos casos, é mais fácil usar um projeto separado para seus testes. Você não precisará criar uma configuração de teste especial para seu projeto. Ou exclua arquivos de teste de compilações de depuração e versão.

### <a name="to-create-a-separate-test-project"></a>Para criar um projeto de teste separado

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse no nó da solução e escolha **Adicionar** > **Novo Projeto**.

1. Na caixa de diálogo **Adicionar um novo projeto** , escolha **C++**, **Windows**e **console** nos menus suspensos de filtro. Selecione o modelo **aplicativo de console** e, em seguida, escolha **Avançar**.

1. Dê um nome ao projeto e escolha **Criar**.

1. Exclua a `main` função no arquivo *. cpp* .

1. Se você estiver usando a versão de cabeçalho único ou de biblioteca dinâmica de Boost. Test, vá para [Adicionar diretivas include](#add-include-directives). Se você estiver usando a versão da biblioteca estática, precisará fazer alguma configuração adicional:

   a. Para editar o arquivo de projeto, primeiro descarregue-o. No **Gerenciador de Soluções**, clique com o botão direito do mouse no nó do projeto e escolha **Descarregar Projeto**. Em seguida, clique com o botão direito do mouse no nó do projeto e escolha **Editar <name\>.vcxproj**.

   b. Adicione duas linhas no grupo de propriedades **Globais**, como é mostrado aqui:

    ```xml
    <PropertyGroup Label="Globals">
    ....
        <VcpkgTriplet>x86-windows-static</VcpkgTriplet>
        <VcpkgEnabled>true</VcpkgEnabled>
    </PropertyGroup>
    ```

   c. Salve e feche o arquivo * \* . vcxproj* e recarregue o projeto.

   d. Para abrir a **Páginas de Propriedades**, clique com o botão direito do mouse no nó do projeto e escolha **Propriedades**.

   e. Expanda geração de código **C/C++**  >  **Code Generation**e, em seguida, selecione **biblioteca de tempo de execução**. Selecione **/MTd** para depurar a biblioteca de runtime estática ou **/MT** para liberar a biblioteca de runtime estática.

   f. Expanda sistema **vinculador**  >  **System**. Verifique se **subsistema** está definido como **console**.

   g. Escolha **OK** para fechar as páginas de propriedades.

## <a name="add-include-directives"></a>Adicionar diretivas de inclusão

1. No arquivo test *. cpp* , adicione as diretivas necessárias `#include` para tornar os tipos e as funções do programa visíveis para o código de teste. Se você estiver usando um projeto de teste separado, normalmente, o programa estará em um nível irmão na hierarquia de pastas. Se você digitar `#include "../"`, uma janela do IntelliSense será exibida e permitirá que você selecione o caminho completo para o arquivo de cabeçalho.

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

Agora, você está pronto para escrever e executar testes do Boost. Consulte a [documentação do Boost Test library](https://www.boost.org/doc/libs/1_71_0/libs/test/doc/html/index.html) para obter informações sobre as macros de teste. Consulte [Executar testes de unidade com o Gerenciador de Testes](run-unit-tests-with-test-explorer.md) para saber mais sobre como descobrir, executar e agrupar testes usando o **Gerenciador de Testes**.

## <a name="see-also"></a>Veja também

- [Escrever testes de unidade para C/C++](writing-unit-tests-for-c-cpp.md)
