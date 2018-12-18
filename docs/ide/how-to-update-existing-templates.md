---
title: Atualizar modelos de projeto e de item existentes no Visual Studio
ms.date: 01/02/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- item templates, updating
- Visual Studio templates, updating
- project templates, updating
- updating templates [Visual Studio]
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: ddc360e6146678730d1844e4762ac3f6112a97d3
ms.sourcegitcommit: 0aafcfa08ef74f162af2e5079be77061d7885cac
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/01/2018
ms.locfileid: "34572560"
---
# <a name="how-to-update-existing-templates"></a>Como atualizar modelos existentes

Depois de criar um modelo e compactar os arquivos em um arquivo *.zip*, modifique o modelo. É possível fazer isso alterando manualmente os arquivos no modelo ou exportando um novo modelo de um projeto com base no modelo.

## <a name="using-the-export-template-wizard-to-update-an-existing-project-template"></a>Usando o Assistente para Exportar Modelo para atualizar um modelo de projeto existente

O Visual Studio fornece um **Assistente para Exportar Modelo** que pode ser usado para atualizar um modelo existente.

1. Abra a caixa de diálogo **Novo Projeto**, escolhendo **Arquivo** > **Novo** > **Projeto**.

1. Selecione o modelo que deseja atualizar, insira um nome e um local para o projeto e escolha **OK**.

1. Modifique o projeto no Visual Studio.

1. No menu **Projeto**, escolha **Exportar Modelo**.

    O **Assistente para Exportar Modelo** é aberto.

1. Siga os prompts no assistente para exportar o modelo como um arquivo *.zip*.

1. (Opcional) Para adicionar o modelo à caixa de diálogo **Novo Projeto**, coloque o arquivo *.zip* no seguinte diretório: *%USERPROFILE%\Documents\Visual Studio \<versão\>\Templates\ProjectTemplates*. Você precisará executar essa etapa se você não tiver selecionado a opção **Importar automaticamente o modelo no Visual Studio** no **Assistente para Exportar Modelo**.

1. Exclua o arquivo *.zip* de modelo antigo.

## <a name="manually-update-an-existing-template"></a>Atualizar manualmente um modelo existente

Você pode atualizar um modelo existente sem usar o **Assistente de Exportação de Modelo**, modificando os arquivos no arquivo *.zip* compactado.

### <a name="to-manually-update-an-existing-template"></a>Para atualizar manualmente um modelo existente

1. Localize o arquivo *.zip* que contém o modelo. Os modelos de projeto do usuário estão localizados em *%USERPROFILE%\Documents\Visual Studio \<versão\>\Templates\ProjectTemplates*.

1. Extraia o arquivo *.zip*.

1. Modifique ou exclua os arquivos de modelo atuais ou adicione novos arquivos ao modelo.

1. Abra, modifique e salve o arquivo XML *.vstemplate* para tratar o comportamento atualizado ou novos arquivos.

    Para obter mais informações sobre o esquema *.vstemplate*, consulte [Referência de esquema de modelo do Visual Studio (extensibilidade)](../extensibility/visual-studio-template-schema-reference.md). Para obter mais informações sobre o que você pode parametrizar nos arquivos de origem, consulte [Parâmetros do modelo](../ide/template-parameters.md).

1. Selecione os arquivos em seu modelo, clique no menu de contexto ou no menu acionado com o botão direito do mouse e escolha **Enviar para** > **Pasta compactada (zipada)**.

    Os arquivos selecionados são compactados em um arquivo *.zip*.

1. Coloque o novo arquivo *.zip* no mesmo diretório do antigo arquivo *.zip*.

1. Exclua os arquivos de modelo extraídos e o arquivo *.zip* de modelo antigo.

## <a name="see-also"></a>Consulte também

- [Personalizar modelos](../ide/customizing-project-and-item-templates.md)
- [Criar modelos de projeto e de item](../ide/creating-project-and-item-templates.md)
- [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)
- [Parâmetros de modelo](../ide/template-parameters.md)