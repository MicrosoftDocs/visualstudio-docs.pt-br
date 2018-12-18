---
title: Como alterar o diretório de saída do build
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-compile
ms.topic: conceptual
helpviewer_keywords:
- output directory, changing
ms.assetid: a8333c89-afb2-4b1d-b2e2-9146da852402
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: aebb4603d32f61c2d4b50355a550a1a932336962
ms.sourcegitcommit: 495bba1d8029646653f99ad20df2f80faad8d58b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39379683"
---
# <a name="how-to-change-the-build-output-directory"></a>Como alterar o diretório de saída do build

Você pode especificar o local de saída por configuração (para depuração, versão ou ambas) gerada pelo projeto.

> [!NOTE]
> Se você tiver um projeto de **Instalação**, consulte a observação no final deste artigo.

## <a name="change-the-build-output-directory"></a>Alterar o diretório de saída do build

1.  Na barra de menus, escolha **Projeto** > **\<Appname> Propriedades**. Clique também com o botão direito do mouse no nó do projeto no **Gerenciador de Soluções** e selecione **Propriedades**.

2.  Se você tiver um projeto do Visual Basic, selecione a guia **Compilar**. Se você tiver um projeto em C#, selecione a guia **Build**. Se você tiver um projeto C++ ou um projeto de JavaScript, selecione a guia **Geral**.

3.  Na lista suspensa de configuração na parte superior, escolha a configuração cujo local do arquivo de saída você deseja alterar (depuração, versão ou todos).

     Localize a entrada do caminho de saída (**Caminho de saída do build** no Visual Basic, **Diretório de saída** no Visual C++, **Caminho de saída** no JavaScript e C#). Especifique um novo diretório de saída de build em relação ao diretório do projeto.

> [!NOTE]
> Em um Projeto de Instalação, a caixa **Nome do arquivo de saída** muda apenas o local do arquivo *Setup.exe*, não o local dos arquivos de projeto. Para obter mais informações, consulte **Caixa de diálogo Build, Propriedades de Configuração, Propriedades do Projeto de Implantação**.

## <a name="see-also"></a>Consulte também

- [Página de build, Designer de Projeto (C#)](../ide/reference/build-page-project-designer-csharp.md)
- [Página de propriedades gerais (projeto)](/cpp/ide/general-property-page-project)
- [Compilação e build](../ide/compiling-and-building-in-visual-studio.md)