---
title: 'Como: Use Pesquisa em Designer de Fluxo de Trabalho'
ms.date: 11/04/2016
ms.topic: conceptual
ms.prod: visual-studio-dev15
ms.technology: vs-workflow-designer
ms.assetid: f42d3115-2ed2-4941-8f1e-92dac41c30fa
ms.author: gewarren
manager: douge
ms.workload:
- multiple
author: gewarren
ms.openlocfilehash: ecf4839cec08e9ffb0419aebcff9da145214b117
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49943057"
---
# <a name="how-to-use-search-in-the-workflow-designer"></a>Como: Use Pesquisa em Designer de Fluxo de Trabalho

Para facilitar a criação de fluxos de trabalho maiores e mais complexos, você pode pesquisar dentro do Designer de fluxo de trabalho para localizar itens por palavra-chave. Observe que o designer não suporta substitui.

## <a name="quick-find"></a>Localização Rápida

Localização rápida localiza o seguinte no designer:

-   Propriedades de objetos de <xref:System.Activities.Activity> , de objetos, <xref:System.Activities.Statements.FlowNode> de objetos <xref:System.Activities.Statements.State> , das transições, e outros itens personalizados de controle de fluxo.

-   Variáveis

-   Arguments

-   Expressões

### <a name="use-quick-find"></a>Usar a localização rápida

1. Com o designer de fluxo de trabalho aberto, pressione **Ctrl + F**, ou selecione **editar** > **localizar e substituir** > **localização rápida**.

2. Insira o termo de pesquisa para o **localizar** caixa de texto e clique em **Localizar próximo**.

3. O termo de pesquisa está localizado no fluxo de trabalho atual. A imagem a seguir mostra um nome de exibição de atividade que está sendo localizado no designer:

   ![Resultado de pesquisa no designer de fluxo de trabalho](../workflow-designer/media/designersearch.png)

## <a name="find-in-files"></a>Localizar nos arquivos

Localizar em arquivos localiza cadeias de caracteres em arquivos de fluxo de trabalho, incluindo arquivos XAML.

### <a name="use-find-in-files"></a>Usar Localizar em arquivos

1.  No Visual Studio, pressione **Ctrl**+**Shift**+**F**, ou selecione **editar**  >   **Localizar e substituir** > **localizar nos arquivos**.

2.  Inserir o item de pesquisa para o **localizar** caixa de texto e clique em **Localizar tudo**.

3.  O resultado de alterações é mostrado na **localizar o resultado** modo de exibição. Clicar duas vezes em um item de resultado navegará para a atividade que contém a correspondência no designer de fluxo de trabalho.