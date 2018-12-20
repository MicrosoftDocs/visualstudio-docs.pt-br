---
title: Como caminhos de pesquisa de Python são aplicados
description: O Visual Studio fornece um meio mais específico para especificar caminhos de pesquisa para ambientes e projetos para evitar o uso de variáveis em todo o sistema.
ms.date: 11/12/2018
ms.prod: visual-studio-dev15
ms.technology: vs-python
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: douge
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: e3e6bd1ce14e1803e48a476246e3cfb8858286bb
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53051523"
---
# <a name="how-visual-studio-uses-python-search-paths"></a>Como o Visual Studio usa caminhos de pesquisa de Python

Com o uso típico do Python, a variável de ambiente `PYTHONPATH` (ou `IRONPYTHONPATH`, etc.) fornece o caminho de pesquisa padrão para arquivos de módulo. Ou seja, quando você usa uma instrução `from <name> import...` ou `import <name>`, o Python pesquisa os seguintes locais, nessa ordem, por um nome correspondente:

1. Módulos internos do Python.
1. A pasta que contém o código do Python que você está executando.
1. O "caminho de pesquisa do módulo", conforme definido pela variável de ambiente aplicável. (Consulte [O caminho de pesquisa do módulo](https://docs.python.org/2/tutorial/modules.html#the-module-search-path) e [Variáveis de ambiente](https://docs.python.org/2/using/cmdline.html#envvar-PYTHONPATH) na documentação básica do Python.)

No entanto, o Visual Studio ignora a variável de ambiente do caminho de pesquisa, mesmo quando ela tiver sido configurada para todo o sistema. Na verdade, ela é precisamente ignorada *porque* é definida para todo o sistema e, portanto, gera algumas perguntas que não podem ser respondidas automaticamente: Os módulos referenciados são destinados ao Python 2.7 ou ao Python 3.6+? Eles substituirão os módulos da biblioteca padrão? O desenvolvedor está ciente desse comportamento ou essa é uma tentativa de sequestro mal-intencionada?

Dessa forma, o Visual Studio fornece um meio para especificar caminhos de pesquisa diretamente nos projetos e ambientes. O código que você executa ou depura no Visual Studio recebe os caminhos de pesquisa no valor de `PYTHONPATH` (e outras variáveis equivalentes). Ao adicionar caminhos de pesquisa, o Visual Studio inspeciona as bibliotecas nessas localizações e compila bancos de dados do IntelliSense para elas quando necessário (Visual Studio 2017 versão 15.5 e anterior; a criação do banco de dados pode demorar algum tempo, dependendo do número de bibliotecas).

Para adicionar um caminho de pesquisa, acesse **Gerenciador de Soluções**, expanda o nó do projeto, clique com o botão direito do mouse em **Caminhos de Pesquisa**, selecione **Adicionar Pasta ao Caminho de Pesquisa**:

![Comando Adicionar Pasta ao Caminho de Pesquisa em Caminhos de Pesquisa no Gerenciador de Soluções](media/search-paths-command.png)

Esse comando exibe um navegador no qual você pode selecionar a pasta a ser incluída.

Se a variável de ambiente `PYTHONPATH` já incluir as pastas que você deseja, use **Adicionar PYTHONPATH aos Caminhos de Pesquisa** como um atalho conveniente.

Depois que as pastas forem adicionadas aos caminhos de pesquisa, o Visual Studio usará esses caminhos para qualquer ambiente associado ao projeto. (Você poderá ver erros se o ambiente tiver base no Python 3, e você tentar adicionar um caminho de pesquisa aos módulos do Python 2.7.)

Os arquivos com uma extensão *.zip* ou *.egg* também podem ser adicionados como caminhos de pesquisa selecionando **Adicionar Arquivo Morto Zip ao Caminho de Pesquisa**. Assim como ocorre com pastas, o conteúdo desses arquivos é examinado e disponibilizado para o IntelliSense.

## <a name="see-also"></a>Consulte também

- [Gerenciar ambientes do Python no Visual Studio](managing-python-environments-in-visual-studio.md)
- [Selecionar um intérprete para um projeto](selecting-a-python-environment-for-a-project.md)
- [Usar requirements.txt para dependências](managing-required-packages-with-requirements-txt.md)
- [Referência à janela Ambientes do Python](python-environments-window-tab-reference.md)
