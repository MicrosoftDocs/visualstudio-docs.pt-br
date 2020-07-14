---
title: Depuração de modo misto para Python
description: Depure simultaneamente o C++ e o Python no Visual Studio, incluindo execução em etapas entre ambientes, exibição de valores e avaliação de expressões.
ms.date: 11/12/2018
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 953ff26a6094a9de9dcf974d5e4cb5a02aaa503f
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85533556"
---
# <a name="debug-python-and-c-together"></a>Depurar o Python e o C++ juntos

A maioria dos depuradores regulares do Python dão suporte apenas à depuração de código do Python. No entanto, na prática, o Python é usado em conjunto com C ou C++, em cenários que exigem alto desempenho ou a capacidade de invocar diretamente as APIs da plataforma. (Confira [Criar uma extensão do C++ para o Python](working-with-c-cpp-python-in-visual-studio.md) para obter um passo a passo.)

O Visual Studio fornece depuração integrada e simultânea de modo misto para Python e C/C++ nativo, desde que você selecione a opção **ferramentas de desenvolvimento nativo do Python** para a carga de trabalho de **desenvolvimento do Python** no instalador do Visual Studio.

> [!Note]
> A depuração de modo misto não está disponível nas Ferramentas Python para Visual Studio 1.x no Visual Studio 2015 e anteriores.

Os recursos de depuração de modo misto incluem o seguinte, conforme explicado neste artigo:

- Pilhas de chamada combinadas
- Etapa entre o Python e o código nativo
- Pontos de interrupção nos dois tipos de código
- Veja as representações de Python de objetos em quadros nativos e vice-versa
- Depuração dentro do contexto do projeto do Python ou C++

![Depuração de modo misto do Python no Visual Studio](media/mixed-mode-debugging.png)

|   |   |
|---|---|
| ![ícone de câmera para vídeo](../install/media/video-icon.png "Assistir a um vídeo") | Para obter uma introdução ao build, ao teste e à depuração de módulos nativos do C com o Visual Studio, assista ao vídeo [Deep Dive: Creating Native Modules](https://youtu.be/D9RlT06a1EI) (Aprofundamento: Criar módulos nativos) (youtube.com, 9min09s). O vídeo aplica-se para o Visual Studio 2015 e 2017. |

## <a name="enable-mixed-mode-debugging-in-a-python-project"></a>Habilitar a depuração de modo misto em um projeto do Python

1. Clique com o botão direito do mouse no projeto Python no **Gerenciador de soluções**, selecione **Propriedades**, selecione a guia **depurar** e, em seguida, selecione **Habilitar depuração de código nativo**. Essa opção habilita o modo misto em todas as sessões de depuração.

    ![Habilitando a depuração de código nativo](media/mixed-mode-debugging-enable-native.png)

    > [!Tip]
    > Quando você habilita a depuração de código nativo, a janela de saída do Python pode desaparecer imediatamente quando o programa é concluído sem fornecer a você a **tecla usual para continuar** pausar. Para forçar uma pausa, adicione a `-i` opção ao campo **executar**  >  **argumentos do intérprete** na guia **depurar** ao habilitar a depuração de código nativo. Esse argumento coloca o interpretador do Python no modo interativo após a conclusão do código e, nesse ponto, ele espera que você pressione **Ctrl** + **Z**  >  **Enter** para sair.

1. Ao anexar o depurador de modo misto a um processo existente (**depurar**  >  **anexar ao processo**), use o botão **selecionar** para abrir a caixa de diálogo **Selecionar tipo de código** . Em seguida, defina a opção **Depurar esses tipos de código** e selecione **Nativo** e **Python** na lista:

    ![Selecionando os tipos de código Nativo e do Python](media/mixed-mode-debugging-code-type.png)

    As configurações de tipo de código são persistentes, portanto, se você quiser desabilitar a depuração de modo misto ao anexar a um processo diferente mais tarde, limpe o tipo de código **Python** .

    É possível selecionar outros tipos de código além do **Nativo** ou em vez dele. Por exemplo, se um aplicativo gerenciado hospeda CPython, que por sua vez usa módulos de extensão nativos, e você deseja depurar todos os três, você pode verificar o **Python**, **nativo**e **gerenciado** em conjunto para uma experiência de depuração unificada, incluindo pilhas de chamadas combinadas e percorrendo entre todos os três tempos de execução.

1. Ao iniciar a depuração no modo misto pela primeira vez, você poderá ver uma caixa de diálogo **Símbolos Obrigatórios do Python** (confira [Símbolos para depuração de modo misto](debugging-symbols-for-mixed-mode-c-cpp-python.md)). Você precisa instalar símbolos apenas uma vez para qualquer ambiente do Python. Os símbolos serão incluídos automaticamente se você instalar o suporte do Python por meio do instalador do Visual Studio (Visual Studio 2017 e posterior).

1. Para tornar o código-fonte do Python padrão em si disponível durante a depuração, visite [https://www.python.org/downloads/source/](https://www.python.org/downloads/source/) , baixe o arquivo apropriado para sua versão e extraia-o para uma pasta. Em seguida, aponte o Visual Studio para arquivos específicos nessa pasta em qualquer ponto que for solicitado.

## <a name="enable-mixed-mode-debugging-in-a-cc-project"></a>Habilitar a depuração de modo misto em um projeto do C/C++

O Visual Studio (2017 versão 15.5 e posterior) é compatível com a depuração de modo misto em um projeto do C/C++ (por exemplo, ao [inserir Python em outro aplicativo, conforme a descrição em python.org](https://docs.python.org/3/extending/embedding.html)). Para habilitar a depuração de modo misto, configure o projeto C/C++ para iniciar a **Depuração do Python/Nativa**:

1. Clique com o botão direito do mouse no projeto C/C++ em **Gerenciador de soluções** e selecione **Propriedades**.
1. Selecione a guia **Depuração**, **Depuração Nativa/do Python** em **Depurador a ser iniciado** e **OK**.

    ![Selecionando o depurador do Python/Nativo em um projeto do C/C++](media/mixed-mode-debugging-select-cpp-debugger.png)

> [!Note]
> Se você não tiver a opção de selecionar a **depuração do Python/Native** , precisará primeiro instalar as **ferramentas de desenvolvimento nativo do Python** usando o instalador do vs. Você pode encontrá-lo como uma opção na carga de trabalho de desenvolvimento do Python. Para obter informações adicionais, consulte [como instalar o suporte do Python no Visual Studio no Windows](installing-python-support-in-visual-studio.md).

Usando esse método, fique ciente de que você não pode depurar o próprio inicializador do *py.exe*, pois ele gera um processo filho *python.exe* ao qual o depurador não será anexado. Caso deseje iniciar o *python.exe* diretamente com argumentos, altere a opção **Comando** nas propriedades **Depuração do Python/Nativa** (mostradas na imagem anterior) para especificar o caminho completo para *python.exe* e, em seguida, especifique os argumentos em **Argumentos do Comando**.

### <a name="attaching-the-mixed-mode-debugger"></a>Anexando o depurador de modo misto

Para todas as versões anteriores do Visual Studio, a depuração direta de modo misto é habilitada apenas ao iniciar um projeto do Python no Visual Studio, pois os projetos do C/C++ usam somente o depurador nativo. No entanto, você pode anexar o depurador separadamente:

1. Inicie o projeto C++ sem depuração (**Debug**  >  **Iniciar Depuração sem depuração** ou **Ctrl** + **F5**).
1. Selecione **depuração**  >  **anexar ao processo**. Na caixa de diálogo exibida, selecione o processo apropriado e, em seguida, use o botão **selecionar** para abrir a caixa de diálogo **Selecionar tipo de código** na qual você pode selecionar **python**:

    ![Selecionando Python como o tipo de depuração ao anexar um depurador](media/mixed-mode-debugging-attach-type.png)

1. Selecione **OK** para fechar essa caixa de diálogo, em seguida, **Anexar** para iniciar o depurador.
1. Talvez seja necessário introduzir uma pausa ou atraso adequado no aplicativo C++ para garantir que ele não chame o código Python que você deseja depurar antes que você tenha a chance de anexar o depurador.

## <a name="mixed-mode-specific-features"></a>Recursos específicos ao modo misto

- [Pilha de chamadas combinada](#combined-call-stack)
- [Etapa entre o Python e o código nativo](#step-between-python-and-native-code)
- [Exibição de valores PyObject no código nativo](#pyobject-values-view-in-native-code)
- [Exibição de valores Nativos no código do Python](#native-values-view-in-python-code)

### <a name="combined-call-stack"></a>Pilha de chamadas combinada

A janela **pilha de chamadas** mostra os quadros de pilha nativos e Python intercalados, com transições marcadas entre os dois:

![Pilha de chamadas combinada com a depuração de modo misto](media/mixed-mode-debugging-call-stack.png)

As transições serão exibidas como **[Código Externo]**, sem especificar a direção da transição, se a opção **Ferramentas** > **Opções** > **Depuração** > **Geral** > **Habilitar Apenas Meu Código** estiver definida.

Clicar duas vezes em um quadro de chamada o torna ativo e abre o código-fonte apropriado, se possível. Se o código-fonte não estiver disponível, o quadro ainda ficará ativo e as variáveis locais poderão ser inspecionadas.

### <a name="step-between-python-and-native-code"></a>Etapa entre o Python e o código nativo

Ao usar os comandos **Step Into** (**F11**) ou **Step Out** (**Shift** + **F11**), o depurador de modo misto manipula corretamente as alterações entre os tipos de código. Por exemplo, quando o Python chama um método de um tipo implementado no C, a intervenção em uma chamada a esse método é interrompida no início da função nativa que implementa o método. Da mesma forma, quando o código nativo chama uma função de API do Python, isso resulta na invocação do código do Python. Por exemplo, a intervenção em um `PyObject_CallObject` em um valor de função que foi originalmente definido no Python é interrompida no início da função do Python. Também há suporte para a intervenção do Python para nativo em funções nativas invocadas do Python por meio de [ctypes](https://docs.python.org/3/library/ctypes.html).

### <a name="pyobject-values-view-in-native-code"></a>Exibição de valores PyObject no código nativo

Quando um quadro nativo (C ou C++) estiver ativo, suas variáveis locais aparecerão **na janela locais** do depurador. Nos módulos de extensão nativos do Python, muitas dessas variáveis são do tipo `PyObject` (que é um typedef de `_object`) ou alguns outros tipos fundamentais do Python (consulte a lista abaixo). Na depuração de modo misto, esses valores apresentam um nó filho adicional rotulado **[exibição do Python]**. Quando expandido, esse nó mostra a representação do Python da variável, idêntica a que você veria se uma variável local referenciando o mesmo objeto estivesse presente em um quadro do Python. Os filhos desse nó são editáveis.

![Exibição do Python na janela Locais](media/mixed-mode-debugging-python-view.png)

Para desabilitar esse recurso, clique com o botão direito do mouse em qualquer lugar da janela **Locais** e ative/desative a opção de menu **Python** > **Mostrar Nós de Exibição do Python**:

![Habilitando a Exibição do Python na janela Locais](media/mixed-mode-debugging-enable-python-view.png)

Tipos C que mostram os nós **[modo de exibição Python]** (se habilitado):

- `PyObject`
- `PyVarObject`
- `PyTypeObject`
- `PyByteArrayObject`
- `PyBytesObject`
- `PyTupleObject`
- `PyListObject`
- `PyDictObject`
- `PySetObject`
- `PyIntObject`
- `PyLongObject`
- `PyFloatObject`
- `PyStringObject`
- `PyUnicodeObject`

**[Exibição do Python]** não aparece automaticamente para os tipos que você mesmo cria. Ao criar extensões para Python 3. x, essa falta geralmente não é um problema porque qualquer objeto tem, por fim `ob_base` , um campo de um dos tipos acima, o que faz com que **[exibição do Python]** apareça.

No entanto, para o Python 2.x, cada tipo de objeto normalmente declara seu cabeçalho como uma coleção de campos embutidos e não há nenhuma associação entre os tipos criados personalizados e `PyObject` no nível do sistema de tipos do código C/C++. Para habilitar nós da **[exibição do Python]** para esses tipos personalizados, edite o arquivo *PythonDkm.natvis* no [diretório de instalação das ferramentas Python](installing-python-support-in-visual-studio.md#install-locations) e adicione outro elemento ao XML do struct C ou da classe C++.

Uma opção alternativa (e melhor) é seguir o [PEP 3123](https://www.python.org/dev/peps/pep-3123/) e usar um campo `PyObject ob_base;` explícito em vez de `PyObject_HEAD`, embora isso nem sempre seja possível por motivos de compatibilidade com versões anteriores.

### <a name="native-values-view-in-python-code"></a>Exibição de valores Nativos no código do Python

Semelhante à seção anterior, você pode habilitar um **[modo de exibição C++]** para valores nativos na janela **locais** quando um quadro Python está ativo. Esse recurso não está habilitado por padrão; portanto, ative-o clicando com o botão direito do mouse na janela **Locais** e ativando/desativando a opção de menu **Python** > **Mostrar Nós de Exibição do C++**.

![Habilitando a Exibição do C++ na janela Locais](media/mixed-mode-debugging-enable-cpp-view.png)

O nó **[modo de exibição c++]** fornece uma representação da estrutura C/c++ subjacente para um valor, idêntico ao que você veria em um quadro nativo. Por exemplo, ele mostra uma instância de `_longobject` (para a qual `PyLongObject` é um typedef) de um inteiro longo do Python e tenta inferir tipos para as classes nativas criadas por conta própria. Os filhos desse nó são editáveis.

![Exibição do C++ na janela Locais](media/mixed-mode-debugging-cpp-view.png)

Se um campo filho de um objeto for do tipo `PyObject` , ou um dos outros tipos com suporte, ele terá um nó de representação **[modo de exibição do Python]** (se essas representações estiverem habilitadas), possibilitando a navegação de gráficos de objeto em que os links não são expostos diretamente para o Python.

Ao contrário de nós **[modo de exibição Python]** , que usam metadados de objeto Python para determinar o tipo do objeto, não há um mecanismo confiável semelhante para **[modo de exibição C++]**. Em termos gerais, considerando um valor do Python (ou seja, uma referência `PyObject`), não é possível determinar com confiança qual estrutura do C/C++ está dando suporte a ele. O depurador de modo misto tenta adivinhar esse tipo, observando vários campos do tipo de objeto (como o `PyTypeObject` referenciado por seu campo `ob_type`) que têm tipos de ponteiro de função. Se um desses ponteiros de função referenciar uma função que pode ser resolvida e essa função tiver um parâmetro `self` com um tipo mais específico que `PyObject*`, esse tipo será considerado como o tipo de suporte. Por exemplo, se `ob_type->tp_init` de um objeto especificado apontar para a seguinte função:

```c
static int FobObject_init(FobObject* self, PyObject* args, PyObject* kwds) {
    return 0;
}
```

o depurador poderá deduzir corretamente que o tipo C do objeto é `FobObject`. Se não for possível determinar um tipo mais preciso de `tp_init`, ele seguirá para outros campos. Se não for possível deduzir o tipo de qualquer um desses campos, o nó **[modo de exibição C++]** apresentará o objeto como uma `PyObject` instância.

Para obter sempre uma representação útil de tipos criados personalizados, é melhor registrar pelo menos uma função especial ao registrar o tipo e usar um parâmetro `self` fortemente tipado. A maioria dos tipos atende a esse requisito naturalmente; se não for o caso, geralmente, `tp_init` será a entrada mais conveniente a ser usada para essa finalidade. Uma implementação fictícia de `tp_init` de um tipo que está presente exclusivamente para habilitar a inferência de tipos do depurador pode apenas retornar zero imediatamente, como no exemplo de código acima.

## <a name="differences-from-standard-python-debugging"></a>Diferenças da depuração padrão do Python

O depurador de modo misto é diferente do [depurador padrão do Python](debugging-python-in-visual-studio.md), que introduz alguns recursos adicionais, mas que não contém algumas funcionalidades relacionadas ao Python:

- Recursos sem suporte: pontos de interrupção condicionais, janela **interativa de depuração** e depuração remota de plataforma cruzada.
- Janela **imediata** : está disponível, mas com um subconjunto limitado de sua funcionalidade, incluindo todas as limitações listadas aqui.
- Versões do Python com suporte: somente CPython 2.7 e 3.3+.
- Shell do Visual Studio: ao usar o Python com o Shell do Visual Studio (por exemplo, se ele tiver sido instalado por meio do instalador integrado), o Visual Studio não poderá abrir projetos do C++ e a experiência de edição para arquivos do C++ será apenas a de um editor de texto básico. No entanto, há suporte completo para a depuração do C/C++ e a depuração de modo misto no Shell com código-fonte, execução em etapas em código nativo e avaliação de expressão do C++ nas janelas do depurador.
- Exibindo e expandindo objetos: ao exibir objetos Python nas janelas de ferramentas **locais** e **assistir** ao depurador, o depurador de modo misto mostra apenas a estrutura dos objetos. Ele não avalia propriedades automaticamente nem mostra atributos computados. Para coleções, ele mostra apenas os elementos de tipos de coleção interna (`tuple`, `list`, `dict`, `set`). Os tipos de coleção personalizada não são visualizados como coleções, a menos que sejam herdados de algum tipo de coleção interna.
- Avaliação de expressão: consulte abaixo.

### <a name="expression-evaluation"></a>Avaliação de expressão

O depurador padrão do Python permite a avaliação de expressões de Python arbitrárias em **inspeção** e janelas **imediatas** quando o processo depurado é pausado em qualquer ponto do código, desde que ele não seja bloqueado em uma operação de e/s ou outra chamada de sistema semelhante. Na depuração de modo misto, as expressões arbitrárias podem ser avaliadas somente quando interrompidas no código do Python, depois de um ponto de interrupção ou intervindo no código. As expressões podem ser avaliadas apenas no thread em que o ponto de interrupção ou a operação de intervenção ocorreu.

Quando interrompida no código nativo ou no código do Python quando as condições acima não se aplicarem (por exemplo, após uma operação de depuração circular ou em um thread diferente), a avaliação da expressão é limitada ao acesso das variáveis locais e globais no escopo do quadro atualmente selecionado, ao acesso de seus campos e à indexação de tipos de coleção interna com literais. Por exemplo, a seguinte expressão pode ser avaliada em qualquer contexto (desde que todos os identificadores refiram-se a variáveis e a campos existentes dos tipos apropriados):

```python
foo.bar[0].baz['key']
```

O depurador de modo misto também resolve essas expressões de outra forma. Todas as operações de acesso a membro pesquisam somente os campos que fazem parte diretamente do objeto (como uma entrada em seu `__dict__` ou `__slots__`, ou um campo de um struct nativo que é exposto ao Python por meio de `tp_members`) e ignoram qualquer `__getattr__`, `__getattribute__` ou lógica do descritor. Da mesma forma, todas as operações de indexação ignoram `__getitem__` e acessam as estruturas de dados internas das coleções diretamente.

Para fins de consistência, esse esquema de resolução de nomes é usado para todas as expressões que correspondem às restrições de avaliação de expressão limitada, independentemente se as expressões arbitrárias são permitidas no ponto de interrupção atual. Para forçar a semântica correta do Python quando um avaliador completo está disponível, coloque a expressão entre parênteses:

```python
(foo.bar[0].baz['key'])
```
