---
title: Selecionar e instalar interpretadores do Python
description: Uma lista completa de interpretadores do Python que têm suporte no Visual Studio com instruções breves sobre onde localizar os instaladores.
ms.date: 06/05/2019
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: fb1c657789e232307672d494710f330758780a67
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85540719"
---
# <a name="install-python-interpreters"></a>Instalar interpretadores do Python

Por padrão, a instalação da carga de trabalho de desenvolvimento do Python no Visual Studio 2017 e versões posteriores também instala o Python 3 (64 bits). Você pode optar por instalar as versões de 32 e 64 bits do Python 2 e do Python 3, juntamente com o Miniconda (Visual Studio 2019) ou o Anaconda 2/Anaconda 3 (Visual Studio 2017), conforme descrito em [Instalação](installing-python-support-in-visual-studio.md).

::: moniker range=">=vs-2019"
Como alternativa, você pode instalar interpretadores padrão do Python na caixa de diálogo **Adicionar Ambiente**. Selecione o comando **Adicionar Ambiente** na janela **Ambientes do Python** ou na barra de ferramentas Python, selecione a guia **Instalação do Python**, indique quais interpretadores instalar e selecione **Instalar**.
::: moniker-end

Você também pode instalar manualmente qualquer um dos interpretadores listados na tabela abaixo fora do instalador do Visual Studio. Por exemplo, se você instalar o Anaconda 3 antes de instalar o Visual Studio, não será necessário instalar novamente usando o instalador do Visual Studio. Você também pode instalar um interpretador manualmente se, por exemplo, houver uma versão mais recente disponível que ainda não aparece no instalador do Visual Studio.

::: moniker range=">=vs-2019"
> [!Note]
> O Visual Studio dá suporte ao Python versão 2.7, bem como à versão 3.5 e posterior. Embora seja possível usar o Visual Studio para editar código escrito em outras versões do Python, essas versões não são oficialmente aceitas, e recursos como o IntelliSense e a depuração podem não funcionar.
::: moniker-end

Para o **Visual Studio 2015 e anterior**, você deve instalar manualmente um dos interpretadores.

O Visual Studio (todas as versões) detecta automaticamente cada interpretador Python instalado e seu ambiente verificando o Registro, de acordo com o [PEP 514 – registro do Python no Registro do Windows](https://www.python.org/dev/peps/pep-0514/). Geralmente, as instalações do Python se encontram em **HKEY_LOCAL_MACHINE\SOFTWARE\Python** (32 bits) e **HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Python** (64 bits) e, em seguida, dentro de nós para a distribuição, como **PythonCore** (CPython) e **ContinuumAnalytics** (Anaconda).

Se o Visual Studio não detectar um ambiente instalado, consulte [Identificar manualmente um ambiente existente](managing-python-environments-in-visual-studio.md#manually-identify-an-existing-environment).

O Visual Studio mostra todos os ambientes conhecidos na janela [**Ambientes do Python**](managing-python-environments-in-visual-studio.md#the-python-environments-window) e detecta automaticamente as atualizações para os interpretadores existentes.

| Interpretador | Descrição |
| --- | --- |
| [CPython](https://www.python.org/) | O interpretador “nativo” e mais usado, disponível em versões de 32 e 64 bits (o recomendado é 32 bits). Inclui os últimos recursos de linguagem, a compatibilidade máxima com pacotes do Python, suporte de depuração completo e interoperabilidade com o [IPython](https://ipython.org/). Consulte também: devo [usar o Python 2 ou o Python 3?](https://wiki.python.org/moin/Python2orPython3). Observe que o Visual Studio 2015 e os anteriores não dão suporte ao Python 3.6 ou posteriores e podem gerar erros, como **Python versão 3.6 sem suporte**. Use o Python 3.5 ou anteriores. |
| [IronPython](https://github.com/IronLanguages/ironpython2) | Uma implementação do .NET do Python, disponível em versões de 32 e 64 bits, que fornece interoperabilidade do C#/F#/Visual Basic, acesso às APIs do .NET, depuração padrão do Python (mas não a depuração de modo misto do C++) e a depuração mista do IronPython/C#. No entanto, o IronPython não dá suporte a ambientes virtuais. |
| [Anaconda](https://www.continuum.io) | Uma plataforma aberta de ciência de dados do Python, além de incluir a última versão do CPython e a maioria dos pacotes difíceis de serem instalados. Recomendamos usá-la, caso você esteja indeciso sobre qual plataforma deverá usar. |
| [PyPy](https://www.pypy.org/) | Uma implementação JIT de rastreamento de alto desempenho do Python que é boa para programas de execução longa e situações em que é possível identificar problemas de desempenho, mas em que não é possível encontrar outras resoluções. Funciona com o Visual Studio, mas com suporte limitado para recursos de depuração avançados. |
| [Jython](https://www.jython.org/) | Uma implementação do Python na JVM (Máquina Virtual Java). Semelhante ao IronPython, o código em execução no Jython pode interagir com classes e bibliotecas Java, mas poderá não usar várias bibliotecas destinadas ao CPython. Funciona com o Visual Studio, mas com suporte limitado para recursos de depuração avançados. |

Para os desenvolvedores que desejam fornecer novas formas de detecção para ambientes do Python, consulte [Detecção para ambiente da PTVS](https://github.com/Microsoft/PTVS/wiki/Extensibility-Environments) (github.com).

## <a name="move-an-interpreter"></a>Mover um interpretador

Se você mover um interpretador existente para um novo local usando o sistema de arquivos, o Visual Studio não detectará automaticamente a alteração.

- Se você especificou originalmente o local do interpretador por meio da janela **Ambientes do Python**, edite o ambiente usando a guia **Configurar** nessa janela para identificar o novo local. Consulte [Identificar manualmente um ambiente existente](managing-python-environments-in-visual-studio.md#manually-identify-an-existing-environment).

- Se você instalou o interpretador usando um programa de instalação, use as etapas a seguir para reinstalar o interpretador no novo local:

  1. Restaure o interpretador do Python para o local original.
  2. Desinstale-o usando o instalador, que limpa as entradas do Registro.
  3. Reinstale o interpretador no local desejado.
  4. Reinicie o Visual Studio, que deve detectar automaticamente o novo local em vez de o local antigo.

Esse processo garante que as entradas do Registro que identificam o local do interpretador, usado pelo Visual Studio, sejam atualizadas corretamente. O uso de um instalador também lida com outros efeitos colaterais que possam existir.

## <a name="see-also"></a>Consulte também

- [Gerenciar ambientes do Python](managing-python-environments-in-visual-studio.md)
- [Selecionar um interpretador para um projeto](selecting-a-python-environment-for-a-project.md)
- [Usar requirements.txt para dependências](managing-required-packages-with-requirements-txt.md)
- [Caminhos de pesquisa](search-paths.md)
- [Referência da janela de ambientes do Python](python-environments-window-tab-reference.md)
