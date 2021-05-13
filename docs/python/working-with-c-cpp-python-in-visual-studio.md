---
title: Escrever extensões do C++ para o Python
description: Um passo a passo da criação de uma extensão em C++ para Python usando Visual Studio, CPython e PyBind11, incluindo uma depuração de modo misto.
ms.date: 05/11/2021
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 866b588b8b46477b397cda92076780d1955cfa83
ms.sourcegitcommit: 9cb0097c33755a3e5cbadde3b0a6e9e76cee727d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/13/2021
ms.locfileid: "109848299"
---
# <a name="create-a-c-extension-for-python"></a>Criar uma extensão do C++ para o Python

Os módulos escritos em C++ (ou em C) são geralmente usados para estender as funcionalidades de um interpretador do Python, bem como para permitir o acesso a funcionalidades de baixo nível do sistema operacional. Há três tipos de módulos principais:

- Módulos de acelerador: como o Python é uma linguagem interpretada, algumas partes do código podem ser escritas em C++ para um desempenho mais alto.
- Módulos de wrapper: expõem interfaces C/C++ existentes para o código Python ou expõem uma API mais "Pythonic" fácil de usar do Python.
- Módulos de acesso do sistema de baixo nível: criados para acessar recursos de nível inferior do runtime, do sistema operacional ou `CPython` do hardware subjacente.

Este artigo explica como criar um módulo de extensão C++ para que compute uma tangente hiperbólica e a `CPython` chama do código Python. A rotina é implementada primeiro em Python para demonstrar o ganho de desempenho relativo da implementação da mesma rotina em C++.

Este artigo também demonstra duas maneiras de disponibilizar o C++ para Python:

- As `CPython` extensões padrão, conforme descrito na [documentação do Python](https://docs.python.org/3/c-api/)
- [PyBind11](https://github.com/pybind/pybind11), que é recomendado para C++ 11 devido à sua simplicidade.

O exemplo completo deste passo a passo pode ser encontrado em [python-samples-vs-cpp-extension](https://github.com/Microsoft/python-sample-vs-cpp-extension) (GitHub).

## <a name="prerequisites"></a>Pré-requisitos

- Visual Studio 2017 ou posterior com a carga de trabalho desenvolvimento do **Python** instalada, incluindo as ferramentas de desenvolvimento nativo do **Python,** que traz a carga de trabalho do C++ e os modelos de ferramentas necessários para extensões nativas.

    ![Selecionando a opção de ferramentas de desenvolvimento nativo do Python](media/cpp-install-native.png)

    > [!Tip]
    > A instalação da carga de trabalho **Aplicativos de ciência de dados e análise** também inclui o Python e a opção **Ferramentas nativas de desenvolvimento em Python** por padrão.

Para obter mais informações sobre opções de instalação, consulte [Instalar o suporte do Python para Visual Studio](installing-python-support-in-visual-studio.md). Se você instalar o Python separadamente, selecione **Baixar símbolos de depuração** em Opções **Avançadas** em seu instalador. Essa opção é necessária para usar a depuração de modo misto entre o código Python e o código nativo.

## <a name="create-the-python-application"></a>Criar o aplicativo do Python

1. Crie um novo projeto python no Visual Studio **selecionando Arquivo**  >  **Novo**  >  **Projeto**. Pesquise "Python", selecione o modelo aplicativo **Python,** dê a ele um nome e um local de sua escolha e selecione **OK.**

1. No arquivo *.py* do projeto, colar o código a seguir (ou insira-o manualmente para experimentar alguns dos recursos [de edição do Python).](editing-python-code-in-visual-studio.md) Esse código calcula uma tangente hiperbólica sem usar a biblioteca matemática e é o que aceleraremos com extensões nativas.

    > [!Tip]
    > Escreva seu código em Python puro antes de reescrever em C++. Dessa forma, você pode verificar com mais facilidade se o código nativo está correto

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

1. Execute o programa usando **Depurar**  >  **Iniciar sem Depuração** (**Ctrl** + **F5**) para ver os resultados. Você pode ajustar a variável `COUNT` para alterar o tempo que os parâmetros de comparação levam para serem executados. Para a finalidade deste passo a passo, defina a contagem de forma que cada parâmetro de comparação leve cerca de dois segundos.

> [!TIP]
> Ao executar parâmetros de comparação, sempre use **Depurar** Iniciar sem Depuração para evitar a sobrecarga incorrida ao executar o código no Visual Studio  >   depurador.

## <a name="create-the-core-c-projects"></a>Criar os projetos principais de C++

Siga as instruções nesta seção para criar dois projetos de C++ idênticos chamados "superfastcode" e "superfastcode2". Posteriormente, você usará duas abordagens diferentes em cada projeto para expor o código C++ ao Python.

1. Clique com o botão direito do mouse na solução em **Gerenciador de Soluções** e escolha **Adicionar** > **Novo Projeto**. Uma solução do Visual Studio pode conter os projetos Python e C++ juntos (essa é uma das vantagens de usar o Visual Studio para Python).

1. Pesquise por "C++", selecione **Projeto vazio**, especifique o nome "superfastcode" ("superfastcode2" para o segundo projeto) e selecione **OK**.

    > [!Tip]
    > Com as **ferramentas de desenvolvimento nativo do Python** instaladas no Visual Studio, você poderá começar em vez disso com o modelo **Módulo de Extensão do Python**, que tem grande parte do que está descrito abaixo já implementado. No entanto, para este passo a passo, começar com um projeto vazio demonstra o build do módulo de extensão passo a passo. Depois de entender o processo, o modelo faz com que você economize tempo ao escrever suas próprias extensões.

1. Crie um arquivo do C++ no novo projeto clicando com o botão direito do mouse no nó **Arquivos de Origem**, escolha **Adicionar** > **Novo Item**, escolha **Arquivo do C++**, forneça a ele o nome `module.cpp` e marque **OK**.

    > [!Important]
    > Um arquivo com a extensão *.cpp* é necessário para ativar as páginas de propriedade C++ nas etapas a seguir.

1. Se você estiver usando um tempo de execução do Python de 64 bits, ative a configuração **x64** usando o menu suspenso na barra de ferramentas principal. Para um tempo de execução do Python de 32 bits, ative a configuração do **Win32** .

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto C++ e escolha **Propriedades**. O valor de **configuração** deve estar **ativo (depuração)** e a **plataforma** estará **ativa (x64)** ou **ativa (Win32)** , dependendo da sua seleção na etapa anterior.

    > [!Tip]
    > Para seus próprios projetos, você desejará configurar as configurações de depuração e de versão. Aqui, apenas configuramos a configuração de depuração e a definimos para usar uma compilação de *versão* do `CPython` , que desabilita alguns recursos de depuração do tempo de execução do C++, incluindo asserções. O uso `CPython` de binários de *depuração* ( `python_d.exe` ) exigirá configurações diferentes.

1. Defina as propriedades específicas, conforme descrito na tabela a seguir e, em seguida, selecione **OK**.
    ::: moniker range=">=vs-2019"
    | Tab | Propriedade | Valor |
    | --- | --- | --- |
    | **Geral** | **Geral** > **Nome de Destino** | Especifique o nome do módulo ao qual você deseja se referir do Python nas instruções `from...import`. Você pode usar esse mesmo nome em C++ ao definir o módulo para Python. Se você quiser usar o nome do projeto como o nome do módulo, deixe o valor padrão de **$(ProjectName)**. |
    | | **Avançado** > **Extensão do arquivo de destino** | **.pyd** |
    | | **Padrões do Projeto** > **Tipo de Configuração** | **Biblioteca Dinâmica (.dll)** |
    | **C/C++** > **Geral** | **Diretórios de Inclusão Adicionais** | Adicione a pasta *include* do Python conforme apropriado para sua instalação, por exemplo, `c:\Python36\include`.  |
    | **C/C++** > **Pré-processador** | **Definições do Pré-processador** | **Apenas CPython**: adicione `Py_LIMITED_API;` no início da cadeia de caracteres (inclusive o ponto e vírgula). Essa definição restringe algumas das funções que podem ser chamadas do Python e torna o código mais portável entre diferentes versões do Python. Se você estiver trabalhando com PyBind11, não adicione essa definição, caso contrário, verá erros de build. |
    | **C/C++** > **Geração de Código** | **Biblioteca de Runtime** | **DLL com multi-thread (/MD)** (confira Aviso abaixo) |
    | **Vinculador** > **Geral** | **Diretórios de Biblioteca Adicionais** | Adicione a pasta *libs* do Python que contém arquivos *.lib* conforme apropriado para sua instalação, por exemplo, `c:\Python36\libs`. (Lembre-se de apontar para a pasta *libs* que contém arquivos *.lib* e *não* para a pasta *Lib* que contém arquivos *.py*.) |
    ::: moniker-end
    ::: moniker range="=vs-2017"
    | Tab | Propriedade | Valor |
    | --- | --- | --- |
    | **Geral** | **Geral** > **Nome de Destino** | Especifique o nome do módulo ao qual você deseja se referir do Python nas instruções `from...import`. Você pode usar esse mesmo nome em C++ ao definir o módulo para Python. Se você quiser usar o nome do projeto como o nome do módulo, deixe o valor padrão de **$(ProjectName)**. Para `python_d.exe` , adicione `_d` ao final do nome. |
    | | **Geral** > **Extensão de Destino** | **.pyd** |
    | | **Padrões do Projeto** > **Tipo de Configuração** | **Biblioteca Dinâmica (.dll)** |
    | **C/C++** > **Geral** | **Diretórios de Inclusão Adicionais** | Adicione a pasta *include* do Python conforme apropriado para sua instalação, por exemplo, `c:\Python36\include`.  |
    | **C/C++** > **Pré-processador** | **Definições do Pré-processador** | Se estiver presente, altere o valor de **_DEBUG** para **NDEBUG**, para corresponder à versão de não depuração de `CPython` . (Ao usar `python_d.exe` , deixe isso inalterado.) |
    | **C/C++** > **Geração de Código** | **Biblioteca de Runtime** | **DLL multithreaded (/MD)** para corresponder à versão de não depuração de `CPython` . (Ao usar `python_d.exe` , deixe isso inalterado.) |
    | **Vinculador** > **Geral** | **Diretórios de Biblioteca Adicionais** | Adicione a pasta *libs* do Python que contém arquivos *.lib* conforme apropriado para sua instalação, por exemplo, `c:\Python36\libs`. (Lembre-se de apontar para a pasta *libs* que contém arquivos *.lib* e *não* para a pasta *Lib* que contém arquivos *.py*.) |
    ::: moniker-end
    
    > [!Tip]
    > Se a guia C/C++ não for exibida nas propriedades do projeto, isso indicará que o projeto não contém nenhum arquivo que ele identifica como arquivos de origem do C/C++. Essa condição poderá ocorrer se você criar um arquivo de origem sem uma extensão *.c* ou *.cpp*. Por exemplo, se você acidentalmente inseriu `module.coo` em vez de `module.cpp` na caixa de diálogo novo item anteriormente, o Visual Studio criará o arquivo, mas não definirá o tipo de arquivo como "C/c + Code", que é o que ativa a guia de propriedades C/C++. Essa identificação indesejada permanece o caso, mesmo se você renomear o arquivo com `.cpp` . Para configurar o tipo de arquivo corretamente, clique com o botão direito do mouse no arquivo no **Gerenciador de Soluções**, escolha **Propriedades** e, em seguida, defina **Tipo de Arquivo** como **Código C/C++**.

1. Clique com o botão direito do mouse no projeto C++ e selecione **Compilar** para testar suas configurações ( **depuração** e **versão**). Os arquivos *.pyd* estão localizados na pasta **solução** em **Depurar** e **Versão**, não na própria pasta do projeto do C++.

1. Adicione o seguinte código ao arquivo *module.cpp* do projeto do C++:

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

1. Se ainda não tiver feito isso, repita as etapas acima para criar um segundo projeto denominado "superfastcode2" com conteúdo idêntico.

## <a name="convert-the-c-projects-to-extensions-for-python"></a>Converter os projetos de C++ em uma extensão para Python

Para transformar a DLL C++ em uma extensão para Python, primeiro você precisa modificar os métodos exportados para interagir com tipos Python. Em seguida, será necessário adicionar uma função que exporte o módulo, juntamente com as definições dos métodos do módulo.

As seções a seguir explicam como executar essas etapas usando as `CPython` extensões e PyBind11.

### <a name="cpython-extensions"></a>Extensões de CPython

Para obter mais informações sobre o que é mostrado nesta seção, consulte o [manual de referência da API do Python/C](https://docs.python.org/3/c-api/index.html) e especialmente [objetos de módulo](https://docs.python.org/3/c-api/module.html) no Python.org (Lembre-se de selecionar sua versão do Python no controle suspenso no canto superior direito para exibir a documentação correta).

1. Na parte superior de *module.cpp*, inclua *Python.h*:

    ```cpp
    #include <Python.h>
    ```

1. Modifique o método `tanh_impl` para aceitar e retornar tipos Python (um `PyObject*`, que é):

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

1. Adicionar uma estrutura que define o módulo da maneira como você deseja fazer referência a ele em seu código Python, especificamente ao usar a instrução `from...import`. (Faça isso corresponder ao valor nas propriedades do projeto em Propriedades **de Configuração**  >  **Geral**  >  **Nome de destino**.) No exemplo a seguir, o nome do módulo "superfastcode" significa que você pode usar em Python, porque `from superfastcode import fast_tanh` `fast_tanh` é definido em `superfastcode_methods` . (Os nomes de arquivo internos para o projeto C++, como *module.cpp,* são inconsequentes.)

    ```cpp
    static PyModuleDef superfastcode_module = {
        PyModuleDef_HEAD_INIT,
        "superfastcode",                        // Module name to use with Python import statements
        "Provides some functions, but faster",  // Module description
        0,
        superfastcode_methods                   // Structure that defines the methods of the module
    };
    ```

1. Adicione um método que o Python chama ao carregar o módulo, que deve ser chamado , em que module-name corresponde exatamente à propriedade Nome de Destino Geral do projeto `PyInit_<module-name>` &lt; &gt; C++   >  (ou seja, corresponde ao nome de arquivo *do .pyd* criado pelo projeto).

    ```cpp
    PyMODINIT_FUNC PyInit_superfastcode() {
        return PyModule_Create(&superfastcode_module);
    }
    ```

1. Compile o projeto C++ novamente para verificar seu código. Se encontrar erros, confira a seção [Solução de problemas](#troubleshooting) abaixo.

### <a name="pybind11"></a>PyBind11

Se tiver concluído as etapas na seção anterior, você certamente observou que usou muito código com texto clichê para criar as estruturas de módulo necessárias para o código C++. O PyBind11 simplifica o processo por meio de macros em um arquivo de cabeçalho de C++ que alcançam o mesmo resultado com muito menos código. Para obter informações de contexto sobre o que é mostrado nesta seção, confira [PyBind11 basics](https://github.com/pybind/pybind11/blob/master/docs/basics.rst) (Noções básicas de PyBind11) (github.com).

1. Instale o PyBind11 usando pip: `pip install pybind11` ou `py -m pip install pybind11`. (Como alternativa, você pode instalar usando a janela Ambientes do Python e, em seguida, usar seu comando "Abrir no PowerShell" para a próxima etapa.)

1. No mesmo terminal, execute `python -m pybind11 --includes` ou `py -m pybind11 --includes` . Isso imprimirá uma lista de caminhos que você deve adicionar à propriedade Diretórios de Inclusão Adicionais Gerais **C/C++** do seu projeto (removendo o  >    >   `-I` prefixo, se presente).

1. Na parte superior de um *novo module.cpp*, que não inclui nenhuma das alterações da seção anterior, inclua *pybind11.h*:

    ```cpp
    #include <pybind11/pybind11.h>
    ```

1. Na parte inferior de *module.cpp*, use a macro `PYBIND11_MODULE` para definir o ponto de entrada da função de C++:

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

1. Crie o projeto C++ para verificar seu código. Se encontrar erros, confira a seção de solução de problemas a seguir.

### <a name="troubleshooting"></a>Solução de problemas

A compilação do módulo de C++ pode falhar pelos seguintes motivos:

- Não é possível localizar *Python.h* (**E1696: não é possível abrir o arquivo de software livre "Python.h"** e/ou **C1083: não é possível abrir o arquivo de inclusão: "Python.h": o arquivo ou diretório não existe**), verifique se o caminho em **C/C++** > **Geral** > **Diretórios de Inclusão Adicionais** nas propriedades do projeto aponta para a pasta *include* da instalação do Python. Veja a etapa 6 em [Criar o projeto principal do C++](#create-the-core-c-projects).

- Não é possível localizar bibliotecas do Python: verifique se o caminho em Diretórios de Biblioteca Adicionais Gerais do **Linker** nas propriedades do projeto aponta para a pasta libs da  >    >   *instalação do* Python. Veja a etapa 6 em [Criar o projeto principal do C++](#create-the-core-c-projects).

- Erros do vinculador relacionadas à arquitetura de destino: altere a arquitetura do projeto de destino C++ para corresponder à instalação do Python. Por exemplo, se você estiver direcionando **o Win32** com o projeto C++, mas sua instalação do Python for de 64 bits, altere o projeto C++ para **x64**.

## <a name="test-the-code-and-compare-the-results"></a>Testar o código e comparar os resultados

Agora que você tem as DLLs estruturadas como extensões de Python, é possível consultá-las por meio do projeto do Python, importar o módulo e usar seus métodos.

### <a name="make-the-dll-available-to-python"></a>Disponibilizar a DLL para o Python

Há duas maneiras de disponibilizar a DLL para o Python.

O primeiro método funcionará se o projeto Python e o projeto C++ estiverem na mesma solução. Vá para **Gerenciador de Soluções**, clique com o botão **direito** do mouse no nó Referências em seu projeto Python e selecione Adicionar **Referência**. Na caixa de diálogo que é exibida, selecione a guia **Projetos**, selecione os projetos **superfastcode** e **superfastcode2** e, em seguida, selecione **OK**.

![Adicionando uma referência ao projeto superfastcode](media/cpp-add-reference.png)

O método alternativo, descrito nas etapas a seguir, instala o módulo em seu ambiente python, disponibilizando-o para outros projetos do Python também. Visite o [ **projeto setuptools** para](https://setuptools.readthedocs.io/) obter uma documentação mais completa.

1. Crie um arquivo chamado *setup.py* em seu projeto de C++ clicando com o botão direito do mouse no projeto e selecionando **Adicionar** > **Novo Item**. Em seguida, escolha **Arquivo do C++ (.cpp)**, nomeie o arquivo como `setup.py` e escolha **OK** (nomear o arquivo com a extensão *.py* faz com que o Visual Studio o reconheça como Python, apesar do uso do modelo do C++). Quando o arquivo for exibido no editor, cole o seguinte código nele conforme for adequado ao método de extensão:

    **`CPython` extensões (projeto superfastcode):**

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

    **`PyBind11` (projeto superfastcode2):**

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

1. Crie um segundo arquivo chamado *pyproject. toml* no projeto C++ e cole o código a seguir nele.

    ```toml
    [build-system]
    requires = ["setuptools", "wheel", "pybind11"]
    build-backend = "setuptools.build_meta"
    ```

1. Para criar a extensão, clique com o botão direito do mouse na guia abrir *pyproject. toml* e selecione "Copiar caminho completo" (excluiremos o nome de *pyproject. toml* do caminho antes de usá-lo).

1. Em Gerenciador de Soluções, clique com o botão direito do mouse no ambiente ativo do Python e selecione *gerenciar pacotes do Python*.

    > [!Tip]
    > Se você já tiver instalado o pacote, verá-o listado aqui. Clique no "X" para desinstalá-lo antes de continuar.

1. Cole o caminho copiado na caixa de pesquisa e exclua-o `pyproject.toml` do final. Em seguida, pressione ENTER para instalar a partir desse diretório.

    > [!Tip]
    > Se a instalação falhar devido a um erro de permissão, adicione `--user` e tente o comando novamente.


### <a name="call-the-dll-from-python"></a>Chamar a DLL no Python

Após disponibilizar a DLL para o Python conforme descrito na seção anterior, você poderá chamar as funções `superfastcode.fast_tanh` e `superfastcode2.fast_tanh2` do código Python e comparar seu desempenho com a implementação do Python:

1. Adicione as seguintes linhas ao arquivo *.py* para chamar métodos exportados das DLLs e exibir suas saídas:

    ```python
    from superfastcode import fast_tanh
    test(lambda d: [fast_tanh(x) for x in d], '[fast_tanh(x) for x in d] (CPython C++ extension)')

    from superfastcode2 import fast_tanh2
    test(lambda d: [fast_tanh2(x) for x in d], '[fast_tanh2(x) for x in d] (PyBind11 C++ extension)')
    ```

1. Execute o programa Python (**depuração**  >  **Iniciar sem depuração** ou **Ctrl** + **F5**) e observe que as rotinas do C++ são executadas aproximadamente cinco a vinte vezes mais rápido do que a implementação do Python. A saída típica aparecerá como se segue:

    ```output
    Running benchmarks with COUNT = 500000
    [tanh(x) for x in d] (Python implementation) took 0.758 seconds

    [fast_tanh(x) for x in d] (CPython C++ extension) took 0.076 seconds

    [fast_tanh2(x) for x in d] (PyBind11 C++ extension) took 0.204 seconds
    ```

    Se o comando **Iniciar sem depuração** estiver desabilitado, clique com o botão direito do mouse no projeto Python no **Gerenciador de soluções** e selecione **definir como projeto de inicialização**.

1. Tente aumentar a variável `COUNT` para que as diferenças sejam mais evidentes. Uma compilação de **depuração** do módulo C++ também é executada mais lentamente do que uma compilação de **versão** porque a compilação de **depuração** é menos otimizada e contém várias verificações de erro. Sinta-se à vontade para alternar entre essas configurações para comparação (mas lembre-se de voltar e atualizar as propriedades anteriores para a configuração de **versão** ).

Na saída, você pode ver que a extensão PyBind11 não é tão rápida quanto a `CPython` extensão, embora ela deva ser significativamente mais rápida do que a implementação pura do Python. Essa diferença é basicamente porque usamos a `METH_O` chamada, que não dá suporte a vários parâmetros, nomes de parâmetros ou argumentos de palavras-chave. PyBind11 gera um código ligeiramente mais complexo para fornecer uma interface mais semelhante ao Python para chamadores, mas como o código de teste chama a função 500.000 vezes, os resultados podem ampliar muito essa sobrecarga!

Podemos reduzir ainda mais a sobrecarga movendo o `for` loop para o código nativo. Isso envolveria o uso [do protocolo iterador](https://docs.python.org/c-api/iter.html) (ou o tipo de PyBind11 para o parâmetro de função `py::iterable` ) para processar cada [](https://pybind11.readthedocs.io/en/stable/advanced/functions.html#python-objects-as-args)elemento. Remover as transições repetidas entre Python e C++ é uma maneira eficaz de reduzir o tempo gasto para processar a sequência.

### <a name="troubleshooting"></a>Solução de problemas

Se você receber um ao tentar importar seu módulo, é provável que um `ImportError` dos seguintes problemas seja a causa:

* Ao compilar por meio de uma referência de projeto, verifique se as propriedades do projeto do C++ corresponderão ao ambiente python ativado para seu projeto python, especialmente os diretórios Incluir e Biblioteca.

* Verifique se o arquivo de saída é chamado `superfastcode.pyd` . Um nome ou extensão diferente impedirá que ele seja importado.

* Se você instalou seu módulo usando o *arquivo setup.py,* verifique se você fez a correção do comando *pip* no ambiente do Python ativado para seu projeto python. Expandir o ambiente python em Gerenciador de Soluções deve mostrar uma entrada para `superfastcode` .

## <a name="debug-the-c-code"></a>Depurar o código C++

O Visual Studio é compatível com a depuração de código de Python e C++ juntos. Esta seção explica o processo usando o projeto **superfastcode**. As etapas são as mesmas para o projeto **superfastcode2**.

1. Clique com o botão direito do mouse no projeto Python, no **Gerenciador de Soluções**, escolha **Propriedades**, marque a guia **Depuração** e, em seguida, a opção **Depurar** > **Habilitar depuração de código nativo**.

    > [!Tip]
    > Quando você habilita a depuração de código nativo, a janela de saída do Python pode desaparecer imediatamente quando o programa for concluído sem lhe dar o normal Pressione qualquer tecla para **continuar pausando.** Para forçar uma pausa, adicione a opção ao campo Executar Argumentos do Interpretador na guia `-i`   >   **Depurar** ao habilitar a depuração de código nativo. Esse argumento coloca o interpretador do Python no modo interativo após a finalização do código, momento em que ele espera que você pressione **Ctrl** + **Z**  >  **Enter** para sair. (Como alternativa, se você não se importar em modificar o código do Python, poderá adicionar as instruções `import os` e `os.system("pause")` ao final do programa. Esse código duplicará o prompt de pausa original.)

1. Selecione **Arquivo**  >  **Salvar** para salvar as alterações de propriedade.

1. De definir a configuração de build **como Depurar** na barra de Visual Studio ferramentas.

    ![Definir a configuração de build como Depuração](media/cpp-set-debug.png)

1. Como o código geralmente demora mais para ser executado no depurador, talvez seja interessante alterar a variável `COUNT` no seu arquivo *.py* para um valor que seja cerca de cinco vezes menor (por exemplo, altere-o de `500000` para `100000`).

1. No código do C++, defina um ponto de interrupção na primeira linha do método `tanh_impl` e, em seguida, inicie o depurador (**F5** ou **Depurar** > **Iniciar Depuração**). O depurador para quando esse código é chamado. Se o ponto de interrupção não for atingido, verifique se a configuração está definida como **depurar** e se você salvou o projeto (o que não acontece automaticamente ao iniciar o depurador).

    ![Parando em um ponto de interrupção no código C++](media/cpp-debugging.png)

1. Neste ponto, você poderá executar o código C++ em etapas, examinar variáveis e assim por diante. Esses recursos são detalhados em [Depurar C++ e Python juntos](debugging-mixed-mode-c-cpp-python-in-visual-studio.md).

## <a name="alternative-approaches"></a>Abordagens alternativas

Há uma variedade de meios para criar extensões Python, conforme descrito na tabela a seguir. As duas primeiras entradas para o `CPython` e `PyBind11` o que já foram discutidas neste artigo.

| Abordagem | Vintage | Usuários representantes | 
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

O exemplo completo deste passo a passo pode ser encontrado em [python-samples-vs-cpp-extension](https://github.com/Microsoft/python-sample-vs-cpp-extension) (GitHub).
