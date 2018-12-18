---
title: Usando um arquivo requirements.txt para gerenciar requisitos do pacote
description: Um arquivo requirements.txt descreve as dependências de um projeto. Se você receber um projeto que contém um arquivo requirements.txt, você pode instalar facilmente essas dependências em uma única etapa.
ms.date: 10/29/2018
ms.prod: visual-studio-dev15
ms.technology: vs-python
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: douge
ms.workload:
- python
- data-science
ms.openlocfilehash: 49f87ff5836188d6fefb80feac94b27902de7968
ms.sourcegitcommit: d462dd10746624ad139f1db04edd501e7737d51e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50218396"
---
# <a name="manage-required-packages-with-requirementstxt"></a>Gerenciar os pacotes necessários com requirements.txt

Se você compartilha um projeto com outras pessoas, usa um sistema de build ou planeja copiar o projeto para qualquer outra localização em que precise restaurar um ambiente, você precisa especificar os pacotes externos exigidos pelo projeto. A abordagem recomendada é usar um [arquivo requirements.txt](http://pip.readthedocs.org/en/latest/user_guide.html#requirements-files) (readthedocs.org) que contém uma lista de comandos do PIP que instala as versões necessárias dos pacotes dependentes. O comando mais comum é `pip freeze > requirements.txt`, que registra a lista atual de pacotes de um ambiente no *requirements.txt*.

Tecnicamente, qualquer nome de arquivo pode ser usado para acompanhar os requisitos (usando `-r <full path to file>` durante a instalação de um pacote), mas o Visual Studio fornece suporte específico para *requirements.txt*:

- Se você carregou um projeto que contém *requirements.txt* e deseja instalar todos os pacotes listados nesse arquivo, expanda o nó **Ambientes de Python** no **Gerenciador de Soluções** e clique com o botão direito do mouse em um nó de ambiente e selecione **Instalar de requirements.txt**:

    ![Instalar de requirements.txt](media/environments-requirements-txt-install.png)

- Se já tiver todos os pacotes necessários instalados em um ambiente, será possível clicar com o botão direito do mouse nesse ambiente, no **Gerenciador de Soluções** e escolher **Gerar requirements.txt** para criar o arquivo necessário. Se o arquivo já existir, será exibido um prompt para como atualizá-lo:

    ![Opções de atualização de requirements.txt](media/environments-requirements-txt-replace.png)

  - **Substituir todo o arquivo** remove todos os itens, comentários e opções existentes.
  - **Atualizar as entradas existentes** detecta os requisitos do pacote e atualiza os especificadores de versão para que eles correspondam à versão instalada.
  - **Atualizar e adicionar entradas** atualiza todos os requisitos encontrados e adiciona todos os outros pacotes ao final do arquivo.

Como os arquivos *requirements.txt* se destinam a congelar os requisitos do ambiente, todos os pacotes instalados são escritos com versões precisas. Usar versões precisas garante que você possa reproduzir facilmente seu ambiente em outra máquina. Os pacotes serão incluídos, mesmo se eles foram instalados com um intervalo de versão, como uma dependência de outro pacote ou com um instalador que não seja o PIP.

Se um pacote não puder ser instalado pelo PIP e for exibido em um arquivo *requirements.txt*, toda a instalação falhará. Nesse caso, edite manualmente o arquivo para excluir esse pacote ou use as [opções do PIP](https://pip.readthedocs.org/en/latest/reference/pip_install.html#requirements-file-format) para se referir a uma versão instalável do pacote. Por exemplo, você pode preferir usar [`pip wheel`](https://pip.readthedocs.org/en/latest/reference/pip_wheel.html) para compilar uma dependência e adicionar a opção `--find-links <path>` ao *requirements.txt*:

```output
C:\Project>pip wheel azure
Downloading/unpacking azure
    Running setup.py (path:C:\Project\env\build\azure\setup.py) egg_info for package azure

Building wheels for collected packages: azure
    Running setup.py bdist_wheel for azure
    Destination directory: c:\project\wheelhouse
Successfully built azure
Cleaning up...

C:\Project>type requirements.txt
--find-links wheelhouse
--no-index
azure==0.8.0

C:\Project>pip install -r requirements.txt -v
Downloading/unpacking azure==0.8.0 (from -r requirements.txt (line 3))
    Local files found: C:/Project/wheelhouse/azure-0.8.0-py3-none-any.whl
Installing collected packages: azure
Successfully installed azure
Cleaning up...
    Removing temporary dir C:\Project\env\build...
```

## <a name="see-also"></a>Consulte também

- [Gerenciar ambientes do Python no Visual Studio](managing-python-environments-in-visual-studio.md)
- [Selecionar um intérprete para um projeto](selecting-a-python-environment-for-a-project.md)
- [Caminhos de pesquisa](search-paths.md)
- [Referência à janela Ambientes do Python](python-environments-window-tab-reference.md)
