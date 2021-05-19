---
title: Escrever extensões do C++ para o Python
description: Este artigo explica como criar uma extensão C++ para Python usando Visual Studio, CPython e PyBind11, incluindo depuração de modo misto.
ms.date: 05/11/2021
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: ce80ab6647ffc1043bcc452c387abcbdb80a2def
ms.sourcegitcommit: 162be102d2c22a1c4ad2c447685abd28e0e85d15
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2021
ms.locfileid: "109973434"
---
# <a name="create-a-c-extension-for-python"></a>Criar uma extensão do C++ para o Python

Módulos escritos em C++ (ou C) normalmente são usados para estender as funcionalidades de um interpretador do Python. Eles também são usados para habilitar o acesso a recursos de sistema operacional de baixo nível. 

Os módulos vêm em três tipos principais:

- **Módulos de acelerador:** como o Python é uma linguagem interpretada, você pode escrever módulos de acelerador em C++ para um desempenho mais alto.
- **Módulos wrapper:** esses módulos expõem interfaces C/C++ existentes ao código Python ou expõem uma API mais "pythonic" fácil de usar do Python.
- **Módulos de** acesso ao sistema de baixo nível: você pode criar esses módulos para acessar recursos de nível inferior do runtime, do sistema operacional ou `CPython` do hardware subjacente.

Este artigo explica como criar um módulo de extensão do C++ para que compute uma tangente hiperbólica e a `CPython` chama do código Python. A rotina é implementada primeiro em Python para demonstrar o ganho de desempenho relativo da implementação da mesma rotina em C++.

O artigo também demonstra duas maneiras de disponibilizar a extensão C++ para Python:

- Use as `CPython` extensões padrão, conforme descrito na [documentação do Python](https://docs.python.org/3/c-api/).
- Use [PyBind11](https://github.com/pybind/pybind11), que recomendamos para C++11 devido à simplicidade.

Você encontrará o exemplo concluído deste passo a passo no GitHub em [python-samples-vs-cpp-extension.](https://github.com/Microsoft/python-sample-vs-cpp-extension)

## <a name="prerequisites"></a>Pré-requisitos

- Visual Studio 2017 ou posterior, com a carga de trabalho desenvolvimento do Python instalada. A carga de trabalho inclui as ferramentas de desenvolvimento nativo do Python, que trazem a carga de trabalho do C++ e os modelos de ferramentas necessários para extensões nativas.

    ![Captura de tela de uma lista de opções de desenvolvimento do Python, realçando a opção ferramentas de desenvolvimento nativas do Python.](media/cpp-install-native.png)

    > [!NOTE]
    > Quando você instala a carga **de trabalho Ciência** de dados e aplicativos analíticos, a opção Python e as ferramentas de desenvolvimento nativo do **Python** são instaladas por padrão.

Para obter mais informações sobre as opções de instalação, consulte [Install Python support for Visual Studio](installing-python-support-in-visual-studio.md). Se você instalar o Python separadamente, certifique-se de selecionar **baixar símbolos de depuração** em **Opções avançadas** em seu instalador. Essa opção é necessária para que você use a depuração de modo misto entre o código Python e o código nativo.

## <a name="create-the-python-application"></a>Criar o aplicativo do Python

1. Crie um novo projeto Python no Visual Studio selecionando **arquivo**  >  **novo**  >  **projeto**. Procure **Python**, selecione o modelo de **aplicativo Python** , insira um nome e um local e, em seguida, selecione **OK**.

1. No arquivo *. py* do projeto, Cole o código a seguir. Para experimentar alguns dos [recursos de edição do Python](editing-python-code-in-visual-studio.md), tente inserir o código manualmente.  

   Esse código computa uma tangente hiperbólica sem usar a biblioteca de matemática e é isso que você vai acelerar com extensões nativas.

    > [!Tip]
    > Escreva seu código em Python puro antes de reescrevê-lo em C++. Dessa forma, você pode verificar mais facilmente para garantir que seu código nativo esteja correto.

    ```python
    from random import random
    from time import perf_counter

    COUNT = 500000  # Change this value depending on the speed of your computer
    DATA = [(random() - 0.5) * 3 for _ in range(COUNT)]

    e = 2.7182818284590452353602874713527

    def sinh(x):
        return (1 - (e ** (-2 * x))) / (2 * (e ** -x))

    def cosh(x):
        return (1 + (e ** (-2 * x))) / (2 * (e ** -x))

    def tanh(x):
        tanh_x = sinh(x) / cosh(x)
        return tanh_x

    def test(fn, name):
        start = perf_counter()
        result = fn(DATA)
        duration = perf_counter() - start
        print('{} took {:.3f} seconds\n\n'.format(name, duration))

        for d in result:
            assert -1 <= d <= 1, " incorrect values"

    if __name__ == "__main__":
        print('Running benchmarks with COUNT = {}'.format(COUNT))

        test(lambda d: [tanh(x) for x in d], '[tanh(x) for x in d] (Python implementation)')
    ```

1. Para exibir os resultados, execute o programa selecionando **depurar**  >  **Iniciar sem depuração** ou selecionando CTRL + F5. 

   Você pode ajustar a variável `COUNT` para alterar o tempo que os parâmetros de comparação levam para serem executados. Para a finalidade deste guia, defina a contagem para que o parâmetro de comparação leve cerca de dois segundos.

   > [!TIP]
   > Ao executar parâmetros de comparação, sempre use **debug**  >  **Start sem depuração**. Isso ajuda a evitar a sobrecarga que você incorrerá ao executar o código dentro do depurador do Visual Studio.

## <a name="create-the-core-c-projects"></a>Criar os projetos principais de C++

Siga as instruções nesta seção para criar dois projetos do C++ idênticos, *superfastcode* e *superfastcode2*. Posteriormente, você usará uma abordagem separada em cada projeto para expor o código C++ para Python.

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse na solução e selecione **Adicionar**  >  **novo projeto**. Uma solução do Visual Studio pode conter projetos Python e C++, que é uma das vantagens de usar o Visual Studio para Python.

1. Pesquise em **C++**, selecione **projeto vazio**, especifique **superfastcode** para o primeiro projeto ou **superfastcode2** para o segundo projeto e, em seguida, selecione **OK**.

    > [!Tip]
    > Como alternativa, com as ferramentas de desenvolvimento nativas do Python instaladas no Visual Studio, você pode começar com o modelo Módulo de Extensão do Python. O modelo tem muito do que está descrito aqui já em uso. 
    > 
    > No entanto, para este passo a passo, começar com um projeto vazio demonstra o build do módulo de extensão passo a passo. Depois de entender o processo, você pode usar o modelo para economizar tempo ao escrever suas próprias extensões.

1. Para criar um arquivo C++ no novo  projeto, clique com o botão direito do mouse no nó Arquivos de Origem e selecione   >  **Adicionar Novo Item**.

1. Selecione **Arquivo C++,** nomeia-o *module.cpp* e, em seguida, selecione **OK.**

    > [!Important]
    > Um arquivo com a extensão *.cpp* é necessário para ativar as páginas de propriedade C++ nas etapas a seguir.

1. Na barra de ferramentas principal, use o menu suspenso para fazer o seguinte:

   * Para um runtime do Python de 64 bits, ative a **configuração x64.** 
   * Para um runtime do Python de 32 bits, ative a **configuração do Win32.**

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto C++, selecione **Propriedades** e, em seguida, faça o seguinte: 

   a. Para **Configuração,** insira **Ativo (Depurar)**.  
   b. Para **Plataforma**, insira **Ativo (x64)** ou **Ativo (Win32),** dependendo da seleção na etapa anterior.

    > [!NOTE]
    > Ao criar seus próprios projetos, você vai querer configurar as configurações *de depuração* *e* versão. Nesta unidade, você está definindo apenas a configuração de depuração e definindo-a para usar um build de versão do CPython. Essa configuração desabilita alguns recursos de depuração do runtime do C++, incluindo declarações. O uso de binários de depuração do CPython (*python_d.exe*) requer configurações diferentes.

1. De acordo com as propriedades descritas na tabela a seguir:

    ::: moniker range=">=vs-2019"

    | Tab | Propriedade | Valor |
    | --- | --- | --- |
    | **Geral** | **Nome de destino** | Especifique o nome do módulo para fazer referência a ele do Python em `from...import` instruções . Você usa esse mesmo nome no código C++ ao definir o módulo para Python. Para usar o nome do projeto como o nome do módulo, deixe o valor padrão de **$\<ProjectName>** .  Para `python_d.exe` , adicione ao final do `_d` nome. |
    | | **Tipo de Configuração** | **Biblioteca Dinâmica (.dll)** |
    | | **Avançado** > **Extensão do arquivo de destino** | **.pyd** |
    | | **Padrões do Projeto** > **Tipo de Configuração** | **Biblioteca Dinâmica (.dll)** |
    | **C/C++** > **Geral** | **Diretórios de Inclusão Adicionais** | Adicione a pasta de *inclusão* do Python conforme apropriado para sua instalação (por exemplo, `c:\Python36\include` ).  |
    | **C/C++** > **Pré-processador** | **Definições do Pré-processador** | Se estiver presente, altere o valor de **_DEBUG** para **NDEBUG** para corresponder à versão de não depuração de CPython. Quando você estiver usando *python_d.exe*, deixe esse valor inalterado. |
    | **C/C++** > **Geração de Código** | **Biblioteca de Runtime** | **Dll de vários threads (/MD)** para corresponder à versão de não depuração de CPython. Quando você estiver usando *python_d.exe*, deixe esse valor como **dll de depuração multi-threaded (/MDD)**. |
    | **Vinculador** > **Geral** | **Diretórios de Biblioteca Adicionais** | Adicione a pasta Python *bibliotecas* que contém arquivos *. lib* , conforme apropriado para sua instalação (por exemplo, *c:\Python36\libs*). Certifique-se de apontar para a pasta *bibliotecas* que contém arquivos *. lib* , *e não* a pasta *lib* que contém arquivos *. py* . |
    | | |

    ::: moniker-end

    ::: moniker range="=vs-2017"

    | Tab | Propriedade | Valor |
    | --- | --- | --- |
    | **Geral** | **Geral** > **Nome de Destino** | Especifique o nome do módulo para referir-se a ele do Python em `from...import` instruções. Você usa esse mesmo nome no código C++ ao definir o módulo para Python. Para usar o nome do projeto como o nome do módulo, deixe o valor padrão de **$\<ProjectName>** . Para `python_d.exe` , adicione `_d` ao final do nome. |
    | | **Geral** > **Extensão de Destino** | **.pyd** |
    | | **Padrões do Projeto** > **Tipo de Configuração** | **Biblioteca Dinâmica (.dll)** |
    | **C/C++** > **Geral** | **Diretórios de Inclusão Adicionais** | Adicione a pasta de *inclusão* do Python, conforme apropriado para sua instalação (por exemplo, *c:\Python36\include*).  |
    | **C/C++** > **Pré-processador** | **Definições do Pré-processador** | Se estiver presente, altere o valor de **_DEBUG** para **NDEBUG** para corresponder à versão de não depuração do `CPython` . Quando você estiver usando `python_d.exe` , deixe esse valor inalterado. |
    | **C/C++** > **Geração de Código** | **Biblioteca de Runtime** | **DLL multithreaded (/MD)** para corresponder à versão de não depuração de `CPython` . Quando você estiver usando `python_d.exe` , deixe esse valor inalterado. |
    | **Vinculador** > **Geral** | **Diretórios de Biblioteca Adicionais** | Adicione a pasta Python *bibliotecas* que contém arquivos *. lib* , conforme apropriado para sua instalação (por exemplo, *c:\Python36\libs*). Certifique-se de apontar para a pasta *bibliotecas* que contém arquivos *. lib* , *e não* a pasta *lib* que contém arquivos *. py* . |
    | | |

    ::: moniker-end
    
    > [!NOTE]
    > Se a guia **C/C++** não for exibida nas propriedades do projeto, o projeto não conterá nenhum arquivo que ele identifica como arquivos de origem do C/c++. Essa condição poderá ocorrer se você criar um arquivo de origem sem uma *extensão de arquivo .c* ou *.cpp.* 
    > 
    > Por exemplo, se você acidentalmente tiver inserido *module.pdf em* vez de *module.cpp* anteriormente na caixa de diálogo novo item, o Visual Studio criará o arquivo, mas não definirá o tipo de arquivo como *Código C/C+,* o que ativará a guia de propriedades do C/C++. Esse erro de identificação permanecerá mesmo se você renomear o arquivo com uma *extensão de arquivo .cpp.* 
    > 
    > Para definir o tipo de arquivo corretamente, **Gerenciador de Soluções**, clique com o botão direito do mouse no arquivo e selecione **Propriedades**. Em seguida, **para Tipo de Arquivo,** selecione **Código C/C++.**

1. Selecione **OK**.

1. Para testar suas configurações *(depurar* e *liberar*), clique com o botão direito do mouse no projeto C++ e selecione **Criar**. 

   Você encontrará os arquivos *.pyd* na pasta da solução, em  *Depurar* e Liberar , não na própria pasta do projeto C++. 

1. No arquivo *module.cpp* do projeto C++, adicione o seguinte código:

    ```cpp
    #include <Windows.h>
    #include <cmath>

    const double e = 2.7182818284590452353602874713527;

    double sinh_impl(double x) {
        return (1 - pow(e, (-2 * x))) / (2 * pow(e, -x));
    }

    double cosh_impl(double x) {
        return (1 + pow(e, (-2 * x))) / (2 * pow(e, -x));
    }

    double tanh_impl(double x) {
        return sinh_impl(x) / cosh_impl(x);
    }
    ```

1. Compile o projeto do C++ novamente para confirmar se o código está correto.

1. Se você ainda não fez isso, repita as etapas anteriores para criar um segundo projeto chamado *superfastcode2* com uma configuração idêntica.

## <a name="convert-the-c-projects-to-extensions-for-python"></a>Converter os projetos de C++ em uma extensão para Python

Para tornar a DLL do C++ uma extensão para Python, primeiro modifique os métodos exportados para interagir com tipos do Python. Em seguida, será necessário adicionar uma função que exporte o módulo, juntamente com as definições dos métodos do módulo.

As seções a seguir explicam como executar essas etapas usando as extensões CPython e PyBind11.

### <a name="use-cpython-extensions"></a>Usar extensões do CPython

Para obter mais informações sobre o código mostrado nesta seção, consulte o Manual de Referência da [API do Python/C](https://docs.python.org/3/c-api/index.html) e, especialmente, a página [Objetos de](https://docs.python.org/3/c-api/module.html) Módulo. Certifique-se de selecionar sua versão do Python na lista de menus suspensos no canto superior direito.

1. Na parte superior do arquivo *module.cpp,* inclua *Python.h*:

    ```cpp
    #include <Python.h>
    ```

1. Modifique `tanh_impl` o método para aceitar e retornar tipos do Python (ou seja, um `PyObject*` ):

    ```cpp
    PyObject* tanh_impl(PyObject* /* unused module reference */, PyObject* o) {
        double x = PyFloat_AsDouble(o);
        double tanh_x = sinh_impl(x) / cosh_impl(x);
        return PyFloat_FromDouble(tanh_x);
    }
    ```

1. Adicione uma estrutura que define como a função `tanh_impl` do C++ é apresentada ao Python:

    ```cpp
    static PyMethodDef superfastcode_methods[] = {
        // The first property is the name exposed to Python, fast_tanh
        // The second is the C++ function with the implementation
        // METH_O means it takes a single PyObject argument
        { "fast_tanh", (PyCFunction)tanh_impl, METH_O, nullptr },

        // Terminate the array with an object containing nulls.
        { nullptr, nullptr, 0, nullptr }
    };
    ```

1. Adicione uma estrutura que define o módulo como você deseja fazer referência a ele em seu código Python, especificamente quando você usa a `from...import` instrução . 

   O nome que está sendo importado neste código deve corresponder ao valor nas propriedades do projeto em **Propriedades de configuração**  >  nome de  >  **destino** geral. 

   No exemplo a seguir, o `"superfastcode"` nome do módulo significa que você pode usar `from superfastcode import fast_tanh` no Python, porque `fast_tanh` está definido em `superfastcode_methods` . Nomes de arquivo internos ao projeto C++, como *Module. cpp*, são irrelevantes.

    ```cpp
    static PyModuleDef superfastcode_module = {
        PyModuleDef_HEAD_INIT,
        "superfastcode",                        // Module name to use with Python import statements
        "Provides some functions, but faster",  // Module description
        0,
        superfastcode_methods                   // Structure that defines the methods of the module
    };
    ```

1. Adicione um método que o Python chama quando carrega o módulo, que deve ser nomeado `PyInit_<module-name>` , onde *\<module-name>* corresponde exatamente à propriedade de nome de destino **geral** do projeto C++  >   . Ou seja, ele corresponde ao nome de arquivo do arquivo *. PYD* que é compilado pelo projeto.

    ```cpp
    PyMODINIT_FUNC PyInit_superfastcode() {
        return PyModule_Create(&superfastcode_module);
    }
    ```

1. Compile o projeto C++ novamente para verificar seu código. Se você encontrar erros, consulte a seção ["solução de problemas"](#troubleshoot-compiling-failures) .

### <a name="use-pybind11"></a>Usar PyBind11

Se tiver concluído as etapas na seção anterior, você certamente observou que usou muito código com texto clichê para criar as estruturas de módulo necessárias para o código C++. O PyBind11 simplifica o processo por meio de macros em um arquivo de cabeçalho C++ que realiza o mesmo resultado, mas com muito menos código. 

Para obter mais informações sobre o código nesta seção, consulte [noções básicas do PyBind11](https://github.com/pybind/pybind11/blob/master/docs/basics.rst).

1. Instale o PyBind11 usando Pip: `pip install pybind11` ou `py -m pip install pybind11` . 

   Como alternativa, você pode instalar o PyBind11 usando a janela ambientes Python e, em seguida, usar o comando **abrir no PowerShell** para a próxima etapa.

1. No mesmo terminal, execute `python -m pybind11 --includes` ou `py -m pybind11 --includes` . 

   Isso imprime uma lista de caminhos que você deve adicionar à propriedade de   >    >  **diretórios de inclusão adicionais** do C/C++ geral do projeto. Certifique-se de remover o `-I` prefixo, se ele estiver presente.

1. Na parte superior de um *Module. cpp* novo que não inclui nenhuma das alterações da seção anterior, inclua *pybind11. h*:

    ```cpp
    #include <pybind11/pybind11.h>
    ```

1. Na parte inferior de *Module. cpp*, use a `PYBIND11_MODULE` macro para definir o ponto de entrada para a função C++:

    ```cpp
    namespace py = pybind11;

    PYBIND11_MODULE(superfastcode2, m) {
        m.def("fast_tanh2", &tanh_impl, R"pbdoc(
            Compute a hyperbolic tangent of a single argument expressed in radians.
        )pbdoc");

    #ifdef VERSION_INFO
        m.attr("__version__") = VERSION_INFO;
    #else
        m.attr("__version__") = "dev";
    #endif
    }
    ```

1. Compile o projeto C++ para verificar seu código. Se você encontrar erros, consulte a próxima seção, "solucionar problemas de falhas de compilação" para obter soluções.

### <a name="troubleshoot-compiling-failures"></a>Solucionar problemas de falhas de compilação

O módulo C++ pode falhar ao compilar pelos seguintes motivos:

- Erro: Não é possível localizar *Python.h* (**E1696:** não é possível abrir o arquivo de software livre "Python.h" e/ou C1083: não é possível abrir o arquivo de **inclusão: "Python.h":** nenhum arquivo ou diretório desse tipo ) 

  Solução: verifique se o caminho em Diretórios de Inclusão Adicionais Gerais do **C/C++** nas propriedades do projeto aponta para a pasta de inclusão da instalação  >    >   *do* Python. Veja a etapa 6 em [Criar o projeto principal do C++](#create-the-core-c-projects).

- Erro: Não é possível localizar bibliotecas do Python 
 
   Solução: verifique se o caminho em Diretórios de Biblioteca Adicionais Gerais do **Linker** nas propriedades do projeto aponta para a pasta libs da  >    >   *instalação do* Python. Veja a etapa 6 em [Criar o projeto principal do C++](#create-the-core-c-projects).

- Erros do vinculador relacionados à arquitetura de destino
   
   Solução: altere a arquitetura do projeto do destino C++ para corresponder à da instalação do Python. Por exemplo, se você estiver direcionando o Win32 com o projeto C++, mas sua instalação do Python for de 64 bits, altere o projeto C++ para x64.

## <a name="test-the-code-and-compare-the-results"></a>Testar o código e comparar os resultados

Agora que você tem as DLLs estruturadas como extensões de Python, é possível consultá-las por meio do projeto do Python, importar o módulo e usar seus métodos.

### <a name="make-the-dll-available-to-python"></a>Disponibilizar a DLL para o Python

Você pode disponibilizar a DLL para o Python de várias maneiras. Aqui estão duas abordagens a considerar: 

* Esse primeiro método funcionará se o projeto Python e o projeto C++ estão na mesma solução. Faça o seguinte: 

   1. No **Gerenciador de Soluções**, clique com o botão direito do mouse **no** nó Referências em seu projeto python e selecione **Adicionar Referência**. 
   1. Na caixa de diálogo que é exibida, selecione a guia **Projetos**, selecione os projetos **superfastcode** e **superfastcode2** e, em seguida, selecione **OK**.

      ![Captura de tela mostrando como adicionar uma referência ao projeto "superfastcode".](media/cpp-add-reference.png)

* Um método alternativo instala o módulo em seu ambiente do Python, o que disponibiliza o módulo para outros projetos do Python também. Para obter mais informações, consulte a [ **documentação do projeto setuptools**](https://setuptools.readthedocs.io/). Faça o seguinte:

    1. Crie um arquivo chamado *setup.py* em seu projeto de C++ clicando com o botão direito do mouse no projeto e selecionando **Adicionar** > **Novo Item**. 
    
    1. Selecione **Arquivo C++ (.cpp),** nomeia o arquivo *setup.py* e, em seguida, selecione **OK.**
    
       Nomear o arquivo com a extensão *.py* faz com que Visual Studio-lo como um arquivo Python, apesar do uso do modelo de arquivo C++. 

       Quando o arquivo for exibido no editor, colar o seguinte código nele, conforme apropriado para o método de extensão:
    
        **Para `CPython` extensões (projeto superfastcode)**:
    
        ```python
        from setuptools import setup, Extension
    
        sfc_module = Extension('superfastcode', sources = ['module.cpp'])
    
        setup(
            name='superfastcode',
            version='1.0',
            description='Python Package with superfastcode C++ extension',
            ext_modules=[sfc_module]
        )
        ```
    
        **Para `PyBind11` (projeto superfastcode2)**:
    
        ```python
        from setuptools import setup, Extension
        import pybind11
    
        cpp_args = ['-std=c++11', '-stdlib=libc++', '-mmacosx-version-min=10.7']
    
        sfc_module = Extension(
            'superfastcode2',
            sources=['module.cpp'],
            include_dirs=[pybind11.get_include()],
            language='c++',
            extra_compile_args=cpp_args,
            )
    
        setup(
            name='superfastcode2',
            version='1.0',
            description='Python package with superfastcode2 C++ extension (PyBind11)',
            ext_modules=[sfc_module],
        )
        ```
    
    1. Crie um segundo arquivo chamado *pyproject. toml* no projeto C++ e cole o seguinte código nele:
    
        ```toml
        [build-system]
        requires = ["setuptools", "wheel", "pybind11"]
        build-backend = "setuptools.build_meta"
        ```
    
    1. Para criar a extensão, clique com o botão direito do mouse na guia abrir *pyproject. toml* e selecione **Copiar caminho completo**. Você excluirá o nome *pyproject. toml* do caminho antes de usá-lo.
    
    1. Em **Gerenciador de soluções**, clique com o botão direito do mouse no ambiente ativo do Python e selecione **gerenciar pacotes do Python**.
    
        > [!Tip]
        > Se você já tiver instalado o pacote, verá-o listado aqui. Antes de continuar, clique no **X** para desinstalá-lo.
    
    1. Na caixa de pesquisa, Cole o caminho copiado, exclua *pyproject. toml* do final e, em seguida, selecione Enter para instalar o módulo desse diretório.
    
        > [!Tip]
        > Se a instalação falhar devido a um erro de permissão, adicione *-* o ao final e tente o comando novamente.


### <a name="call-the-dll-from-python"></a>Chamar a DLL no Python

Depois de disponibilizar a DLL para o Python, conforme descrito na seção anterior, você pode chamar as `superfastcode.fast_tanh` funções e `superfastcode2.fast_tanh2` do código Python e comparar seu desempenho com a implementação do Python. Para chamar a DLL, faça o seguinte:

1. Adicione as seguintes linhas ao seu arquivo *. py* para chamar os métodos que foram exportados das DLLs e exibir suas saídas:

    ```python
    from superfastcode import fast_tanh
    test(lambda d: [fast_tanh(x) for x in d], '[fast_tanh(x) for x in d] (CPython C++ extension)')

    from superfastcode2 import fast_tanh2
    test(lambda d: [fast_tanh2(x) for x in d], '[fast_tanh2(x) for x in d] (PyBind11 C++ extension)')
    ```

1. Execute o programa Python selecionando **depurar**  >  **Iniciar sem depuração** ou selecionando CTRL + F5.

    > [!NOTE]
    > Se o comando **Iniciar sem depuração** estiver desabilitado, em **Gerenciador de soluções**, clique com o botão direito do mouse no projeto Python e selecione **definir como projeto de inicialização**.  

    Observe que as rotinas C++ executam aproximadamente cinco a vinte vezes mais rápido do que a implementação do Python. A saída típica aparecerá como se segue:

    ```output
    Running benchmarks with COUNT = 500000
    [tanh(x) for x in d] (Python implementation) took 0.758 seconds

    [fast_tanh(x) for x in d] (CPython C++ extension) took 0.076 seconds

    [fast_tanh2(x) for x in d] (PyBind11 C++ extension) took 0.204 seconds
    ```

1. Tente aumentar a variável `COUNT` para que as diferenças sejam mais evidentes. 

    Uma compilação de *depuração* do módulo C++ também é executada mais lentamente do que uma compilação de *versão* , pois a compilação de depuração é menos otimizada e contém várias verificações de erro. Sinta-se à vontade para alternar entre essas configurações para comparação, mas lembre-se de voltar e atualizar as propriedades que você definiu anteriormente para a configuração de versão.

Na saída, você pode ver que a extensão PyBind11 não é tão rápida quanto a extensão CPython, embora ela deva ser significativamente mais rápida do que a implementação pura do Python. Essa diferença é em grande parte porque você usou a chamada , que não dá suporte a vários parâmetros, nomes de `METH_O` parâmetros ou argumentos de palavras-chave. PyBind11 gera um código ligeiramente mais complexo para fornecer uma interface mais do tipo Python aos chamadores. Mas, como o código de teste chama a função 500.000 vezes, os resultados podem ampliar muito essa sobrecarga!

Você pode reduzir ainda mais a sobrecarga movendo o `for` loop para o código nativo. Essa abordagem envolveria o uso [do protocolo iterador](https://docs.python.org/c-api/iter.html) (ou o tipo PyBind11 para o parâmetro de função `py::iterable` ) para processar cada [](https://pybind11.readthedocs.io/en/stable/advanced/functions.html#python-objects-as-args)elemento. Remover as transições repetidas entre Python e C++ é uma maneira eficaz de reduzir o tempo necessário para processar a sequência.

### <a name="troubleshoot-importing-errors"></a>Solucionar problemas de erros de importação

Se você receber uma mensagem ao tentar importar seu módulo, poderá `ImportError` resolvê-lo de uma das seguintes maneiras:

* Ao compilar por meio de uma referência de projeto, verifique se as propriedades do projeto do  C++ corresponderão ao ambiente do Python ativado para seu projeto python, especialmente os diretórios Incluir e Biblioteca. 

* Verifique se o arquivo de saída é *chamado superfastcode.pyd*. Qualquer outro nome ou extensão impedirá que ele seja importado.

* Se você instalou seu módulo usando o *arquivo setup.py,* verifique se você fez a implantação do comando *pip* no ambiente do Python ativado para seu projeto python. Expandir o ambiente python em Gerenciador de Soluções deve exibir uma entrada para *superfastcode*.

## <a name="debug-the-c-code"></a>Depurar o código C++

O Visual Studio é compatível com a depuração de código de Python e C++ juntos. Nesta seção, você explica o processo usando o projeto *superfastcode.* O processo é o mesmo para o *projeto superfastcode2.*

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse no projeto Python, selecione **Propriedades**, selecione a guia **depurar** e, em seguida, selecione a opção **depurar**  >  **Habilitar depuração de código nativo** .

    > [!Tip]
    > Quando você habilita a depuração de código nativo, a janela saída do Python pode fechar imediatamente após o programa ser concluído sem fornecer a você a **tecla usual para continuar** pausar. 
    >
    > Solução: para forçar uma pausa depois de habilitar a depuração de código nativo, adicione a `-i` opção ao campo **executar**  >  **argumentos do intérprete** na guia **depurar** . Esse argumento coloca o interpretador do Python no modo interativo após a execução do código e, nesse ponto, ele espera que você selecione CTRL + Z e, em seguida, Enter para fechar a janela. 
    >
    > Como alternativa, se você não se importa para modificar seu código Python, você pode adicionar `import os` `os.system("pause")` instruções e no final do programa. Esse código duplica o prompt de pausa original.

1. Selecione **arquivo**  >  **salvar** para salvar as alterações de propriedade.

1. Na barra de ferramentas do Visual Studio, defina a configuração de compilação a ser **depurada**.

    ![Captura de tela da configuração de "depuração" na barra de ferramentas do Visual Studio.](media/cpp-set-debug.png)

1. Como o código geralmente leva mais tempo para ser executado no depurador, talvez você queira alterar a `COUNT` variável em seu arquivo *. py* para um valor que seja de cinco vezes menor do que o valor padrão. Por exemplo, altere-o de **500000** para **100000**.

1. Em seu código C++, defina um ponto de interrupção na primeira linha do `tanh_impl` método e, em seguida, inicie o depurador selecionando **F5** ou **debug**  >  **Iniciar Depuração**. 

    O depurador para quando o código do ponto de interrupção é chamado. Se o ponto de interrupção não for atingido, verifique se a configuração está definida como **depurar** e se você salvou o projeto, o que não acontece automaticamente quando você inicia o depurador.

    ![Captura de tela do código C++ que contém um ponto de interrupção.](media/cpp-debugging.png)

1. No ponto de interrupção, você pode percorrer o código C++, examinar variáveis e assim por diante. Para obter mais informações sobre esses recursos, consulte [Depurar Python e C++ juntos.](debugging-mixed-mode-c-cpp-python-in-visual-studio.md)

## <a name="alternative-approaches"></a>Abordagens alternativas

Você pode criar extensões do Python de várias maneiras, conforme descrito na tabela a seguir. As duas primeiras linhas, `CPython` e `PyBind11` , são discutidas neste artigo.

| Abordagem | Vintage | Usuários representativos | 
| --- | --- | --- |
| Módulos de extensão C/C++ para `CPython` | 1991 | Biblioteca Padrão | 
| [PyBind11](https://github.com/pybind/pybind11) (recomendado para C++) | 2015 |  |
| [Cython](https://cython.org) (recomendado para C) | 2007 | [gevent](https://www.gevent.org/), [kivy](https://kivy.org/) |
| [HPy](https://hpyproject.org/) | 2019 | |
| [mypyc](https://mypyc.readthedocs.io/) | 2017 | |
| ctypes | 2003 | [oscrypto](https://github.com/wbond/oscrypto) | 
| cffi | 2013 | [cryptography](https://cryptography.io/), [pypy](https://pypy.org/) |
| SWIG | 1996 | [crfsuite](http://www.chokkan.org/software/crfsuite/) | 
| [Boost.Python](https://www.boost.org/doc/libs/1_66_0/libs/python/doc/html/index.html) | 2002 | |
| [cppyy](https://cppyy.readthedocs.io/) | 2017 | |

## <a name="see-also"></a>Confira também

Você encontrará o exemplo concluído deste passo a passo no GitHub em [python-samples-vs-cpp-extension.](https://github.com/Microsoft/python-sample-vs-cpp-extension)
