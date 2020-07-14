---
title: Escrever extensões do C++ para o Python
description: Um passo a passo da criação de uma extensão em C++ para Python usando Visual Studio, CPython e PyBind11, incluindo uma depuração de modo misto.
ms.date: 11/19/2018
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 0871361d25131b493838bac12945a64a19a0f173
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85543722"
---
# <a name="create-a-c-extension-for-python"></a>Criar uma extensão do C++ para o Python

Os módulos escritos em C++ (ou em C) são geralmente usados para estender as funcionalidades de um interpretador do Python, bem como para permitir o acesso a funcionalidades de baixo nível do sistema operacional. Há três tipos de módulos principais:

- Módulos de acelerador: como o Python é uma linguagem interpretada, algumas partes do código podem ser escritas em C++ para um desempenho mais alto.
- Módulos de wrapper: expõem interfaces C/C++ existentes para o código Python ou expõem uma API mais "Pythonic" fácil de usar do Python.
- Módulos de acesso de baixo nível do sistema: criados para acessar os recursos de baixo nível do runtime CPython, do sistema operacional ou do hardware subjacente.

Este artigo explica como criar um módulo de extensão C++ para CPython que calcula uma tangente hiperbólica e faz uma chamada a ela do código Python. A rotina é implementada primeiro em Python para demonstrar o ganho de desempenho relativo da implementação da mesma rotina em C++.

Este artigo também demonstra duas maneiras de disponibilizar o C++ para Python:

- As extensões padrão de CPython, conforme descrito na [Documentação do Python](https://docs.python.org/3/c-api/)
- [PyBind11](https://github.com/pybind/pybind11), que é recomendado para C++ 11 devido à sua simplicidade.

Há uma comparação entre esses e outros meios em [abordagens alternativas](#alternative-approaches) no final deste artigo.

O exemplo completo deste passo a passo pode ser encontrado em [python-samples-vs-cpp-extension](https://github.com/Microsoft/python-sample-vs-cpp-extension) (GitHub).

## <a name="prerequisites"></a>Pré-requisitos

- Visual Studio 2017 ou posterior com as cargas de trabalho **Desenvolvimento para Desktop com C++** e **Desenvolvimento do Python** instaladas com as opções padrão.
- Na carga de trabalho **Desenvolvimento Python**, marque também a caixa à direita para **Ferramentas de desenvolvimento nativo em Python**. Essa opção define a maior parte da configuração descrita neste artigo. (Essa opção também inclui a carga de trabalho do C++ automaticamente.)

    ![Selecionando a opção de ferramentas de desenvolvimento nativo do Python](media/cpp-install-native.png)

    > [!Tip]
    > A instalação da carga de trabalho **Aplicativos de ciência de dados e análise** também inclui o Python e a opção **Ferramentas nativas de desenvolvimento em Python** por padrão.

Para obter mais informações, confira [Instalar o suporte para Python para Visual Studio](installing-python-support-in-visual-studio.md), incluindo o uso de outras versões do Visual Studio. Se você instalar o Python separadamente, lembre-se de selecionar **Baixar símbolos de depuração** e **Baixar binários de depuração** em **Opções Avançadas** no instalador. Essa opção garante que você terá as bibliotecas de depuração necessárias disponíveis se optar por fazer um build de depuração.

## <a name="create-the-python-application"></a>Criar o aplicativo do Python

1. Crie um novo projeto Python no Visual Studio selecionando **arquivo**  >  **novo**  >  **projeto**. Pesquise "Python", selecione o modelo **Aplicativo Python**, atribua a ele um nome e um local adequados e selecione **OK**.

1. O trabalho com C++ exige o uso de um interpretador de Python de 32 bits (Python 3.6 ou superior recomendado). Na janela **Gerenciador de Soluções** do Visual Studio, expanda o nó do projeto, depois o nó **Ambientes do Python**. Se você não encontrar um ambiente de 32 bits como o padrão (em negrito ou rotulado com **padrão global**), siga as instruções em [Escolher um ambiente de Python para um projeto](selecting-a-python-environment-for-a-project.md). Se você não encontrar um interpretador de 32 bits instalado, confira [Instalar interpretadores do Python](installing-python-interpreters.md).

1. No arquivo *.py* do projeto, cole o código a seguir que submeterá a benchmark o cálculo de uma tangente hiperbólica (implementada sem o uso da biblioteca de matemática para facilitar a comparação). Fique à vontade para inserir o código manualmente para experimentar alguns [recursos de edição do Python](editing-python-code-in-visual-studio.md).

    ```python
    from itertools import islice
    from random import random
    from time import perf_counter

    COUNT = 500000  # Change this value depending on the speed of your computer
    DATA = list(islice(iter(lambda: (random() - 0.5) * 3.0, None), COUNT))

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

1. Execute o programa usando **depurar**  >  **Iniciar sem depuração** (**Ctrl** + **F5**) para ver os resultados. Você pode ajustar a variável `COUNT` para alterar o tempo que os parâmetros de comparação levam para serem executados. Para a finalidade deste passo a passo, defina a contagem de forma que cada parâmetro de comparação leve cerca de dois segundos.

> [!TIP]
> Ao executar parâmetros de comparação, sempre use **debug**  >  **Start sem Debugging** para evitar a sobrecarga incorrida ao executar o código no depurador do Visual Studio.

## <a name="create-the-core-c-projects"></a>Criar os projetos principais de C++

Siga as instruções nesta seção para criar dois projetos de C++ idênticos chamados "superfastcode" e "superfastcode2". Posteriormente, você usará em cada projeto formas diferentes de expor o código C++ para Python.

1. Verifique se a variável de ambiente `PYTHONHOME` está definida para o interpretador do Python que você deseja usar. Os projetos do C++ no Visual Studio dependem dessa variável para localizar os arquivos, como *python.h*, que são usados ao criar uma extensão do Python.

1. Clique com o botão direito do mouse na solução em **Gerenciador de Soluções** e escolha **Adicionar** > **Novo Projeto**. Uma solução do Visual Studio pode conter os projetos Python e C++ juntos (essa é uma das vantagens de usar o Visual Studio para Python).

1. Pesquise por "C++", selecione **Projeto vazio**, especifique o nome "superfastcode" ("superfastcode2" para o segundo projeto) e selecione **OK**.

    > [!Tip]
    > Com as **ferramentas de desenvolvimento nativo do Python** instaladas no Visual Studio, você poderá começar em vez disso com o modelo **Módulo de Extensão do Python**, que tem grande parte do que está descrito abaixo já implementado. No entanto, para este passo a passo, começar com um projeto vazio demonstra o build do módulo de extensão passo a passo. Depois de entender o processo, o modelo faz com que você economize tempo ao escrever suas próprias extensões.

1. Crie um arquivo do C++ no novo projeto clicando com o botão direito do mouse no nó **Arquivos de Origem**, escolha **Adicionar** > **Novo Item**, escolha **Arquivo do C++**, forneça a ele o nome `module.cpp` e marque **OK**.

    > [!Important]
    > Um arquivo com a extensão *.cpp* é necessário para ativar as páginas de propriedade C++ nas etapas a seguir.

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto C++ e escolha **Propriedades**.

1. Na parte superior da caixa de diálogo **Páginas de Propriedades** exibida, defina **Configuração** para **Todas as Configurações** e **Plataforma** para **Win32**.

1. Defina as propriedades específicas, conforme descrito na tabela a seguir e, em seguida, selecione **OK**.

    | Tab | Propriedade | Valor |
    | --- | --- | --- |
    | **Geral** | **Geral**  >  **Nome do destino** | Especifique o nome do módulo ao qual você deseja se referir do Python nas instruções `from...import`. Você pode usar esse mesmo nome em C++ ao definir o módulo para Python. Se você quiser usar o nome do projeto como o nome do módulo, deixe o valor padrão de **$(ProjectName)**. |
    | | **Geral**  >  **Extensão de destino** | **.pyd** |
    | | **Padrões**  >  do projeto **Tipo de configuração** | **Biblioteca Dinâmica (.dll)** |
    | **C/C++**  >  **Geral** | **Diretórios de Inclusão Adicionais** | Adicione a pasta *include* do Python conforme apropriado para sua instalação, por exemplo, `c:\Python36\include`.  |
    | **C/C++**  >  **Pré-processador** | **Definições do Pré-processador** | **Apenas CPython**: adicione `Py_LIMITED_API;` no início da cadeia de caracteres (inclusive o ponto e vírgula). Essa definição restringe algumas das funções que podem ser chamadas do Python e torna o código mais portável entre diferentes versões do Python. Se você estiver trabalhando com PyBind11, não adicione essa definição, caso contrário, verá erros de build. |
    | **C/C++**  >  **Geração de código** | **Biblioteca de Runtime ** | **DLL com multi-thread (/MD)** (confira Aviso abaixo) |
    | **Vinculador**  >  **Geral** | **Diretórios de Biblioteca Adicionais** | Adicione a pasta *libs* do Python que contém arquivos *.lib* conforme apropriado para sua instalação, por exemplo, `c:\Python36\libs`. (Lembre-se de apontar para a pasta *libs* que contém arquivos *.lib* e *não* para a pasta *Lib* que contém arquivos *.py*.) |

    > [!Tip]
    > Se a guia C/C++ não for exibida nas propriedades do projeto, isso indicará que o projeto não contém nenhum arquivo que ele identifica como arquivos de origem do C/C++. Essa condição poderá ocorrer se você criar um arquivo de origem sem uma extensão *.c* ou *.cpp*. Por exemplo, se você acidentalmente inseriu `module.coo` em vez de `module.cpp` na caixa de diálogo novo item anteriormente, o Visual Studio criará o arquivo, mas não definirá o tipo de arquivo como "C/c + Code", que é o que ativa a guia de propriedades C/C++. Essa identificação indesejada permanece o caso, mesmo se você renomear o arquivo com `.cpp` . Para configurar o tipo de arquivo corretamente, clique com o botão direito do mouse no arquivo no **Gerenciador de Soluções**, escolha **Propriedades** e, em seguida, defina **Tipo de Arquivo** como **Código C/C++**.

    > [!Warning]
    > Sempre defina a opção de biblioteca de tempo de execução de código do **C/C++**  >  **Code Generation**  >  **Runtime Library** como **/MD (DLL de vários threads)**, mesmo para uma configuração de depuração, porque essa configuração é a qual os binários do Python sem depuração são compilados. Com o CPython, se você definir a opção **/MDD (DLL de depuração multi-threaded)** , a criação de uma configuração de **depuração** produzirá o erro **C1189: Py_LIMITED_API é incompatível com Py_DEBUG, Py_TRACE_REFS e Py_REF_DEBUG**. Além disso, se você remover `Py_LIMITED_API` (que é necessário com CPython, mas não em PyBind11) para evitar o erro de build, o Python falhará ao tentar importar o módulo. (A falha ocorre na chamada da DLL a `PyModule_Create`, conforme descrito adiante, com a mensagem de saída **Erro fatal do Python: PyThreadState_Get: nenhum thread atual**.)
    >
    > A opção/MDd é usada para criar os binários de depuração do Python (como *python_d.exe*), mas selecioná-lo para uma DLL de extensão ainda causa o erro de compilação com `Py_LIMITED_API` .

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

As seções a seguir explicam como executar essas etapas usando o PyBind11 e as extensões de CPython.

### <a name="cpython-extensions"></a>Extensões de CPython

Para obter informações sobre o que é mostrado nesta seção para Python 3.x, consulte o [Manual de Referência de API do Python/C](https://docs.python.org/3/c-api/index.html) e especialmente os [Objetos de Módulo](https://docs.python.org/3/c-api/module.html) em python.org (Lembre-se de selecionar a versão do Python do controle suspenso no canto superior direito para exibir a documentação correta).

Se você estiver trabalhando com o Python 2.7, consulte em vez disso [Extending Python 2.7 with C or C++ (Estender o Python 2.7 com C ou C++)](https://docs.python.org/2.7/extending/extending.html) e [Porting Extension Modules to Python 3 (Fazer a portabilidade de módulos de extensão para Python 3)](https://docs.python.org/2.7/howto/cporting.html) (python.org).

1. Na parte superior de *module.cpp*, inclua *Python.h*:

    ```cpp
    #include <Python.h>
    ```

1. Modifique o método `tanh_impl` para aceitar e retornar tipos Python (um `PyOjbect*`, que é):

    ```cpp
    PyObject* tanh_impl(PyObject *, PyObject* o) {
        double x = PyFloat_AsDouble(o);
        double tanh_x = sinh_impl(x) / cosh_impl(x);
        return PyFloat_FromDouble(tanh_x);
    }
    ```

1. Adicione uma estrutura que define como a função `tanh_impl` do C++ é apresentada ao Python:

    ```cpp
    static PyMethodDef superfastcode_methods[] = {
        // The first property is the name exposed to Python, fast_tanh, the second is the C++
        // function name that contains the implementation.
        { "fast_tanh", (PyCFunction)tanh_impl, METH_O, nullptr },

        // Terminate the array with an object containing nulls.
        { nullptr, nullptr, 0, nullptr }
    };
    ```

1. Adicionar uma estrutura que define o módulo da maneira como você deseja fazer referência a ele em seu código Python, especificamente ao usar a instrução `from...import`. (Faça isso corresponde ao valor nas propriedades do projeto em **Propriedades**  >  de configuração **Geral**  >  **Nome de destino**.) No exemplo a seguir, o nome do módulo "superfastcode" significa que você pode usar `from superfastcode import fast_tanh` no Python, porque `fast_tanh` está definido em `superfastcode_methods` . (Os nomes de FileNames internos ao projeto C++, como *Module. cpp*, são irrelevantes.)

    ```cpp
    static PyModuleDef superfastcode_module = {
        PyModuleDef_HEAD_INIT,
        "superfastcode",                        // Module name to use with Python import statements
        "Provides some functions, but faster",  // Module description
        0,
        superfastcode_methods                   // Structure that defines the methods of the module
    };
    ```

1. Adicione um método que o Python chama quando carrega o módulo, que deve ser nomeado `PyInit_<module-name>` , em que &lt; nome do módulo &gt; corresponde exatamente à propriedade de nome de destino **geral**do projeto C++  >  **Target Name** (ou seja, corresponde ao nome de arquivo do *. PYD* compilado pelo projeto).

    ```cpp
    PyMODINIT_FUNC PyInit_superfastcode() {
        return PyModule_Create(&superfastcode_module);
    }
    ```

1. Defina a configuração de destino como **liberar** e compilar o projeto C++ novamente para verificar seu código. Se encontrar erros, confira a seção [Solução de problemas](#troubleshooting) abaixo.

### <a name="pybind11"></a>PyBind11

Se tiver concluído as etapas na seção anterior, você certamente observou que usou muito código com texto clichê para criar as estruturas de módulo necessárias para o código C++. O PyBind11 simplifica o processo por meio de macros em um arquivo de cabeçalho de C++ que alcançam o mesmo resultado com muito menos código. Para obter informações de contexto sobre o que é mostrado nesta seção, confira [PyBind11 basics](https://github.com/pybind/pybind11/blob/master/docs/basics.rst) (Noções básicas de PyBind11) (github.com).

1. Instale o PyBind11 usando pip: `pip install pybind11` ou `py -m pip install pybind11`.

1. Na parte superior de *module.cpp*, inclua *pybind11.h*:

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

1. Defina a configuração de destino como **Versão** e crie o projeto C++ para verificar o código. Se encontrar erros, confira a seção de solução de problemas a seguir.

### <a name="troubleshooting"></a>Solução de problemas

A compilação do módulo de C++ pode falhar pelos seguintes motivos:

- Não é possível localizar *Python.h* (**E1696: não é possível abrir o arquivo de software livre "Python.h"** e/ou **C1083: não é possível abrir o arquivo de inclusão: "Python.h": o arquivo ou diretório não existe**), verifique se o caminho em **C/C++** > **Geral** > **Diretórios de Inclusão Adicionais** nas propriedades do projeto aponta para a pasta *include* da instalação do Python. Veja a etapa 6 em [Criar o projeto principal do C++](#create-the-core-c-projects).

- Não é possível localizar bibliotecas Python: Verifique se o caminho **Linker**em diretórios de  >  **General**  >  **biblioteca adicionais** gerais do vinculador nas propriedades do projeto aponta para a pasta *bibliotecas* da sua instalação do Python. Veja a etapa 6 em [Criar o projeto principal do C++](#create-the-core-c-projects).

- Erros do vinculador relacionadas à arquitetura de destino: altere a arquitetura do projeto de destino C++ para corresponder à instalação do Python. Por exemplo, se você tiver como alvo x64 com o projeto C++, mas a instalação do Python for x86, altere o projeto C++ para ter como destino x86.

## <a name="test-the-code-and-compare-the-results"></a>Testar o código e comparar os resultados

Agora que você tem as DLLs estruturadas como extensões de Python, é possível consultá-las por meio do projeto do Python, importar o módulo e usar seus métodos.

### <a name="make-the-dll-available-to-python"></a>Disponibilizar a DLL para o Python

Há duas maneiras de disponibilizar a DLL para o Python.

O primeiro método funcionará se o projeto Python e o projeto C++ estiverem na mesma solução. Vá para **Gerenciador de soluções**, clique com o botão direito do mouse no nó **referências** em seu projeto Python e selecione **Adicionar referência**. Na caixa de diálogo que é exibida, selecione a guia **Projetos**, selecione os projetos **superfastcode** e **superfastcode2** e, em seguida, selecione **OK**.

![Adicionando uma referência ao projeto superfastcode](media/cpp-add-reference.png)

O método alternativo, descrito nas etapas a seguir, instala o módulo no ambiente Python global, tornando-o disponível para outros projetos Python também. (Fazer isso normalmente requer que você atualize o banco de dados de preenchimento do IntelliSense para esse ambiente no Visual Studio 2017 versão 15.5 e anterior. A atualização também é necessária ao remover o módulo do ambiente.)

1. Se estiver usando o Visual Studio 2017 ou posterior, execute o instalador do Visual Studio, escolha **Modificar** e escolha **Componentes Individuais** > **Compiladores, ferramentas de build e runtimes** > **conjunto de ferramentas do Visual C++ 2015.3 v140**. Essa etapa é necessária porque o Python (para o Windows) foi criado com o Visual Studio 2015 (versão 14.0) e espera que essas ferramentas estejam disponíveis durante o build de uma extensão por meio do método descrito aqui. (Observe que talvez seja necessário instalar uma versão de 32 bits do Python e direcionar a DLL para o Win32 e não para o x64).

1. Crie um arquivo chamado *setup.py* em seu projeto de C++ clicando com o botão direito do mouse no projeto e selecionando **Adicionar** > **Novo Item**. Em seguida, escolha **Arquivo do C++ (.cpp)**, nomeie o arquivo como `setup.py` e escolha **OK** (nomear o arquivo com a extensão *.py* faz com que o Visual Studio o reconheça como Python, apesar do uso do modelo do C++). Quando o arquivo for exibido no editor, cole o seguinte código nele conforme for adequado ao método de extensão:

    **Extensões de CPython (projeto superfastcode):**

    ```python
    from distutils.core import setup, Extension, DEBUG

    sfc_module = Extension('superfastcode', sources = ['module.cpp'])

    setup(name = 'superfastcode', version = '1.0',
        description = 'Python Package with superfastcode C++ extension',
        ext_modules = [sfc_module]
        )
    ```

    Consulte [criando Python.org (extensões C e C++](https://docs.python.org/3/extending/building.html) ) para obter a documentação sobre este script.

    **PyBind11 (projeto superfastcode2):**

    ```python
    import os, sys

    from distutils.core import setup, Extension
    from distutils import sysconfig

    cpp_args = ['-std=c++11', '-stdlib=libc++', '-mmacosx-version-min=10.7']

    sfc_module = Extension(
        'superfastcode2', sources = ['module.cpp'],
        include_dirs=['pybind11/include'],
        language='c++',
        extra_compile_args = cpp_args,
        )

    setup(
        name = 'superfastcode2',
        version = '1.0',
        description = 'Python package with superfastcode2 C++ extension (PyBind11)',
        ext_modules = [sfc_module],
    )
    ```

1. O código *setup.py* instrui o Python a compilar a extensão usando o conjunto de ferramentas do C++ no Visual Studio 2015, quando usado na linha de comando. Abra um prompt de comandos com privilégios elevados, navegue até a pasta que contém o projeto C++ (ou seja, a pasta que contém *setup.py*) e digite o seguinte comando:

    ```command
    pip install .
    ```

    ou:

    ```command
    py -m pip install .
    ```

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

1. Tente aumentar a variável `COUNT` para que as diferenças sejam mais evidentes. Uma compilação de **depuração** do módulo C++ também é executada mais lentamente do que uma compilação de **versão** porque a compilação de **depuração** é menos otimizada e contém várias verificações de erro. Fique à vontade para alternar entre essas configurações para comparação.

> [!NOTE]
> Na saída, você pode ver que a extensão PyBind11 não é tão rápida quanto a extensão CPython, embora ainda seja significativamente mais rápida que a implementação direta de Python. A diferença se deve a uma pequena quantidade de sobrecarga por chamada que o PyBind11 introduz para tornar sua interface de C++ consideravelmente mais simples. Essa diferença por chamada é bastante irrelevante: como o código de teste chama as funções de extensão 500.000 vezes, os resultados que você vê aqui amplificam bastante essa sobrecarga! Normalmente, uma função de C++ faz muito mais trabalho do que os métodos `fast_tanh[2]` triviais usados aqui e, nesse caso, a sobrecarga não é importante. No entanto, se você estiver implementando métodos que podem ser chamados milhares de vezes por segundo, usar a abordagem de CPython poderá resultar em um desempenho melhor do que no caso do PyBind11.

## <a name="debug-the-c-code"></a>Depurar o código C++

O Visual Studio é compatível com a depuração de código de Python e C++ juntos. Esta seção explica o processo usando o projeto **superfastcode**. As etapas são as mesmas para o projeto **superfastcode2**.

1. Clique com o botão direito do mouse no projeto Python, no **Gerenciador de Soluções**, escolha **Propriedades**, marque a guia **Depuração** e, em seguida, a opção **Depurar** > **Habilitar depuração de código nativo**.

    > [!Tip]
    > Quando você habilita a depuração de código nativo, a janela de saída do Python pode desaparecer imediatamente quando o programa é concluído sem fornecer a você a **tecla usual para continuar** pausar. Para forçar uma pausa, adicione a `-i` opção ao campo **executar**  >  **argumentos do intérprete** na guia **depurar** ao habilitar a depuração de código nativo. Esse argumento coloca o interpretador do Python no modo interativo após a conclusão do código e, nesse ponto, ele espera que você pressione **Ctrl** + **Z**  >  **Enter** para sair. (Como alternativa, se você não se importar em modificar o código do Python, poderá adicionar as instruções `import os` e `os.system("pause")` ao final do programa. Esse código duplicará o prompt de pausa original.)

1. Selecione **arquivo**  >  **salvar** para salvar as alterações de propriedade.

1. Defina a configuração de compilação a ser **depurada** na barra de ferramentas do Visual Studio.

    ![Definir a configuração de build como Depuração](media/cpp-set-debug.png)

1. Como o código geralmente demora mais para ser executado no depurador, talvez seja interessante alterar a variável `COUNT` no seu arquivo *.py* para um valor que seja cerca de cinco vezes menor (por exemplo, altere-o de `500000` para `100000`).

1. No código do C++, defina um ponto de interrupção na primeira linha do método `tanh_impl` e, em seguida, inicie o depurador (**F5** ou **Depurar** > **Iniciar Depuração**). O depurador para quando esse código é chamado. Se o ponto de interrupção não for atingido, verifique se a configuração está definida como **depurar** e se você salvou o projeto (o que não acontece automaticamente ao iniciar o depurador).

    ![Parando em um ponto de interrupção no código C++](media/cpp-debugging.png)

1. Neste ponto, você poderá executar o código C++ em etapas, examinar variáveis e assim por diante. Esses recursos são detalhados em [Depurar C++ e Python juntos](debugging-mixed-mode-c-cpp-python-in-visual-studio.md).

## <a name="alternative-approaches"></a>Abordagens alternativas

Há uma variedade de meios para criar extensões Python, conforme descrito na tabela a seguir. As duas primeiras entradas para CPython e PyBind11 já foram discutidas neste artigo.

| Abordagem | Vintage | Usuários representantes | Vantagens | Desvantagens |
| --- | --- | --- | --- | --- |
| Módulos de extensão do C/C++ para o CPython | 1991 | Biblioteca Padrão | [Tutoriais e documentação abrangente](https://docs.python.org/3/c-api/). Controle total. | Compilação, portabilidade, gerenciamento de referências. Profundo conhecimento sobre o C. |
| [PyBind11](https://github.com/pybind/pybind11) (recomendado para C++) | 2015 |  | Biblioteca leve, somente cabeçalho para a criação de associações de Python de código C++ existente. Poucas dependências. Compatibilidade de PyPy. | Mais novo, menos maduro. Uso intensivo de recursos C++ 11. Lista curta de compiladores compatíveis (o Visual Studio está incluído). |
| Cython (recomendado para C) | 2007 | [gevent](https://www.gevent.org/), [kivy](https://kivy.org/) | Semelhante ao Python. Altamente maduro. Alto desempenho. | Compilação, nova sintaxe, nova cadeia de ferramentas. |
| [Boost.Python](https://www.boost.org/doc/libs/1_66_0/libs/python/doc/html/index.html) | 2002 | | Funciona com praticamente qualquer compilador C++. | Pacote grande e complexo de bibliotecas; contém várias soluções alternativas para compiladores antigos. |
| ctypes | 2003 | [oscrypto](https://github.com/wbond/oscrypto) | Sem compilação, ampla disponibilidade. | O acesso e a mutação de estruturas do C são complicados e sujeitos a erros. |
| SWIG | 1996 | [crfsuite](http://www.chokkan.org/software/crfsuite/) | Gere associações para várias linguagens de uma só vez. | Sobrecarga excessiva se o Python for o único destino. |
| cffi | 2013 | [cryptography](https://cryptography.io/en/latest/), [pypy](https://pypy.org/) | Facilidade de integração, compatibilidade com o PyPy. | Mais novo, menos maduro. |
| [cppyy](https://cppyy.readthedocs.io/en/latest/) | 2017 | | Semelhante ao cffi usando C++. | Mais recente, pode ter alguns problemas com o VS 2017. |

## <a name="see-also"></a>Confira também

O exemplo completo deste passo a passo pode ser encontrado em [python-samples-vs-cpp-extension](https://github.com/Microsoft/python-sample-vs-cpp-extension) (GitHub).
