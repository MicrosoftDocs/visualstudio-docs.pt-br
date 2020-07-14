---
title: Atualizar modelos de item de projeto existentes
ms.date: 01/02/2018
ms.topic: how-to
helpviewer_keywords:
- item templates, updating
- Visual Studio templates, updating
- project templates, updating
- updating templates [Visual Studio]
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: d5d9726ecbf3cb7c403f682aadb197a26b0dc26b
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85283912"
---
# <a name="how-to-update-existing-templates"></a>Como atualizar modelos existentes

Depois de criar um modelo e compactar os arquivos em um arquivo *.zip*, modifique o modelo. É possível fazer isso alterando manualmente os arquivos no modelo ou exportando um novo modelo de um projeto com base no modelo.

## <a name="use-the-export-template-wizard"></a>Use o Assistente para Exportar Modelo

O Visual Studio fornece um **Assistente de modelo de exportação** que pode ser usado para atualizar um modelo existente:

1. Escolha **arquivo**  >  **novo**  >  **projeto** na barra de menus.

1. Selecione o modelo que você deseja atualizar e continue seguindo as etapas para criar o projeto.

1. Modifique o projeto no Visual Studio. Por exemplo, altere o tipo de saída ou adicione um novo arquivo ao projeto.

1. No menu **Projeto**, escolha **Exportar Modelo**.

    O **Assistente para Exportar Modelo** é aberto.

1. Siga os prompts no assistente para exportar o modelo como um arquivo *.zip*.

1. Adicional Coloque o arquivo *. zip* no seguinte diretório: *%USERPROFILE%\Documents\Visual Studio \<version\> \Templates\ProjectTemplates* para torná-lo disponível para seleção. Você precisará executar essa etapa se você não tiver selecionado a opção **Importar automaticamente o modelo no Visual Studio** no **Assistente para Exportar Modelo**.

1. Exclua o arquivo *.zip* de modelo antigo.

## <a name="manually-update-an-existing-template"></a>Atualizar manualmente um modelo existente

Você pode atualizar um modelo existente sem usar o **Assistente de Exportação de Modelo**, modificando os arquivos no arquivo *.zip* compactado.

### <a name="to-manually-update-an-existing-template"></a>Para atualizar manualmente um modelo existente

1. Localize o arquivo *.zip* que contém o modelo. Os modelos de projeto de usuário estão localizados em *%USERPROFILE%\Documents\Visual Studio \<version\> \Templates\ProjectTemplates*.

1. Extraia o arquivo *. zip* .

1. Modifique ou exclua os arquivos de modelo atuais ou adicione novos arquivos ao modelo.

1. Abra, modifique e salve o arquivo XML *.vstemplate* para tratar o comportamento atualizado ou novos arquivos.

    Para obter mais informações sobre o esquema *. vstemplate* , consulte [extensibilidade (referência de esquema de modelo) do Visual Studio](../extensibility/visual-studio-template-schema-reference.md). Para obter mais informações sobre o que você pode parametrizar nos arquivos de origem, consulte [parâmetros de modelo](../ide/template-parameters.md).

1. Selecione os arquivos em seu modelo e, no menu de contexto ou clique com o botão direito do mouse, e escolha **Enviar para**  >  **pasta compactada (zipada)**.

    Os arquivos que você selecionou são compactados em um arquivo *. zip* .

1. Coloque o novo arquivo *.zip* no mesmo diretório do antigo arquivo *.zip*.

1. Exclua os arquivos de modelo extraídos e o arquivo *.zip* de modelo antigo.

## <a name="see-also"></a>Veja também

- [Personalizar modelos](../ide/customizing-project-and-item-templates.md)
- [Criar modelos de projeto e de item](../ide/creating-project-and-item-templates.md)
- [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)
- [Parâmetros de modelo](../ide/template-parameters.md)
