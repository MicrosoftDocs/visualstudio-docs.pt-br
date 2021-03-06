---
title: Criar um projeto IA com base no código existente
description: Saiba como usar Visual Studio Tools for AI para colocar o código Python existente em um projeto do Visual Studio.
ms.custom: SEO-VS-2020
author: jillre
ms.author: jillfra
manager: jmartens
monikerRange: vs-2017
ms.date: 11/13/2017
ms.topic: how-to
ms.workload:
- multiple
ms.openlocfilehash: 7746d8dd39bb4400a7779ad43e489cf6e7475fb9
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99841621"
---
# <a name="create-an-ai-project-from-existing-code"></a>Criar um projeto IA com base no código existente

Depois de [instalar as Ferramentas do Visual Studio para IA](installation.md), é fácil colocar o código Python existente em um projeto do Visual Studio.

> [!Important]
> O processo descrito aqui não move ou copia os arquivos de origem. Se você quiser trabalhar com uma cópia, basta primeiro duplicar a pasta.

1. Inicie o Visual Studio e selecione **Arquivo > Novo > Projeto**.

2. Na caixa de diálogo **Novo projeto**, pesquise "**Ferramentas do IA**", selecione o modelo "**Do código Python Existente**", dê ao projeto um nome e um local e selecione **OK**.

   ![Novo Projeto com base em um Código Existente, etapa 1](media/create-project-existing/new-ai-project.png)

3. No assistente exibido, defina o caminho como seu código existente, defina um filtro para tipos de arquivo e especifique os caminhos de pesquisa que seu projeto requer. Em seguida, selecione **OK**. Se você não souber o que são caminhos de pesquisa, deixe esse campo em branco.

   ![Novo Projeto com base em um Código Existente, etapa 2](media/create-project-existing/azurebatch-newproject.png)

   Se o seu código existente fizer parte de um projeto do Azure Machine Learning, marque **É a pasta do Azure Machine Learning** para garantir a conversão bem-sucedida de importantes detalhes de configuração do Azure Machine Learning, como a conta de Experimentação, o Workspace, quais contextos computacionais a serem usados e mais.

4. Para definir um arquivo de inicialização, localize o arquivo no **Gerenciador de Soluções**, clique com o botão direito do mouse e selecione **Definir como Arquivo de Inicialização**.

5. Execute o programa pressionando **Ctrl** + **F5** ou selecionando **debug > iniciar sem depuração**.

> [!div class="nextstepaction"]
> [Tutorial: trabalhando com o Python no Visual Studio](../python/tutorial-working-with-python-in-visual-studio-step-00-installation.md)

## <a name="see-also"></a>Consulte também

- [Identificar manualmente um ambiente de Python existente](../python/managing-python-environments-in-visual-studio.md#manually-identify-an-existing-environment)
