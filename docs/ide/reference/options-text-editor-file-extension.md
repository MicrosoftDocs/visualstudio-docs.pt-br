---
title: Opções, Editor de Texto, Extensão de Arquivo
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.File_Extension
helpviewer_keywords:
- file extensions, associating to editor
- Editing Experience
- Options dialog box
- Editing Experience, selecting
ms.assetid: 05298fc5-fc4e-4bb2-b942-1f7d2dcdff0f
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 05fce2fd1735e1bed7f528467a1c32f399a9ce22
ms.sourcegitcommit: dd839de3aa24ed7cd69f676293648c6c59c6560a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52389034"
---
# <a name="options-text-editor-file-extension"></a>Opções, Editor de Texto, Extensão de Arquivo

A caixa de diálogo Opções permite especificar como todos os arquivos com determinadas extensões de arquivo serão manipulados pelo IDE (ambiente de desenvolvimento integrado) do Visual Studio. Para cada **Extensão** que inserir, você pode selecionar uma Experiência de Edição. Isso permite escolher o editor ou o designer do IDE no qual os documentos de um determinado tipo serão abertos. Para exibir essas opções, escolha **Opções** no menu **Ferramentas**, expanda o nó **Editor de Texto** e selecione **Extensão de Arquivo**.

Quando você selecionar uma opção "com codificação", uma caixa de diálogo será exibida sempre que você abrir um documento do tipo em questão que permitir selecionar um esquema de codificação para o documento. Isso pode ser útil se você estiver preparando versões dos documentos do projeto para uso em diferentes plataformas ou em diferentes linguagens de destino.

## <a name="uielement-list"></a>Lista UIElement

**Extensão**

Digite a extensão de arquivo cuja Experiência de Edição no IDE você deseja definir.

**Editor**

 Selecione o editor ou o designer do IDE em que documentos com essa extensão de arquivo serão abertos. Quando você selecionar uma opção "com codificação", uma caixa de diálogo será exibida sempre que você abrir um documento desse tipo que permite a seleção de um esquema de codificação.

**Adicionar**

Adiciona uma entrada que inclui a **Extensão** e a **Experiência de Edição** especificadas à Lista de extensões.

**Removerr**

Exclui a entrada selecionada da Lista de Extensões.

**Lista de extensões**

Lista todas as extensões para as quais uma Experiência de Edição foi especificada.

**Mapear arquivos sem extensão para**

Selecione esta opção se você quiser especificar como arquivos sem extensão serão tratados pelo IDE.

**Opções de arquivos sem extensão**

Fornece a mesma lista que o **Editor**. Selecione o editor ou o designer do IDE em que documentos sem extensão de arquivo serão abertos.

## <a name="see-also"></a>Consulte também

- [Como gerenciar modos do editor](../../ide/how-to-manage-editor-modes.md)