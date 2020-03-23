---
title: Opções, Editor de Texto, Extensão de Arquivo
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.File_Extension
helpviewer_keywords:
- file extensions, associating to editor
- Editing Experience
- Options dialog box
- Editing Experience, selecting
ms.assetid: 05298fc5-fc4e-4bb2-b942-1f7d2dcdff0f
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3711a87d84e25fd6f790cee62ecb71b2b046d0be
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/18/2020
ms.locfileid: "75596197"
---
# <a name="options-text-editor-file-extension"></a>Opções, Editor de Texto, Extensão de Arquivo

A caixa de diálogo Opções permite especificar como todos os arquivos com determinadas extensões de arquivo serão manipulados pelo IDE (ambiente de desenvolvimento integrado) do Visual Studio. Para cada **Extensão** que inserir, você pode selecionar uma Experiência de Edição. Isso permite escolher o editor ou o designer do IDE no qual os documentos de um determinado tipo serão abertos. Para exibir essas opções, escolha **Opções** no menu **Ferramentas**, expanda o nó **Editor de Texto** e selecione **Extensão de Arquivo**.

Quando você selecionar uma opção "com codificação", uma caixa de diálogo será exibida sempre que você abrir um documento do tipo em questão que permitir selecionar um esquema de codificação para o documento. Isso pode ser útil se você estiver preparando versões dos documentos do projeto para uso em diferentes plataformas ou em diferentes linguagens de destino.

## <a name="uielement-list"></a>Lista de elementos de interface do usuário

**Extensão**

Digite a extensão de arquivo cuja Experiência de Edição no IDE você deseja definir.

**Editor**

Selecione o editor ou o designer do IDE em que documentos com essa extensão de arquivo serão abertos. Quando você selecionar uma opção "com codificação", uma caixa de diálogo será exibida sempre que você abrir um documento desse tipo que permite a seleção de um esquema de codificação.

**Adicionar**

Adiciona uma entrada que inclui a **Extensão** e a **Experiência de Edição** especificadas à Lista de extensões.

**Remover**

Exclui a entrada selecionada da Lista de Extensões.

**Lista de extensões**

Lista todas as extensões para as quais uma Experiência de Edição foi especificada.

**Mapear arquivos sem extensão para**

Selecione esta opção se você quiser especificar como arquivos sem extensão serão tratados pelo IDE.

**Opções de arquivos sem extensão**

Fornece a mesma lista que o **Editor**. Selecione o editor ou o designer do IDE em que documentos sem extensão de arquivo serão abertos.

## <a name="see-also"></a>Confira também

- [Como gerenciar modos do editor](../../ide/how-to-manage-editor-modes.md)
