---
title: 'Walkthrough: Criando um editor personalizado | Microsoft Docs'
description: Saiba como o modelo de projeto VSPackage pode criar um editor personalizado simples em C++ usando este passo a passos.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], custom - create
ms.assetid: d090abb6-d99f-4083-a3db-cd16bf81ce7d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 79adcf719091619fe4c4eb62b1fe89ba3da388f5
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062012"
---
# <a name="walkthrough-create-a-custom-editor"></a>Walkthrough: criar um editor personalizado
O modelo de projeto VSPackage pode criar um editor personalizado simples em C++. O modelo de projeto VSPackage não dá mais suporte a projetos C# ou Visual Basic. Para obter mais informações, consulte [Visual Studio SDK](../extensibility/visual-studio-sdk.md).

## <a name="prerequisites"></a>Pré-requisitos
 Para seguir este passo a passos, você deve instalar o SDK do Visual Studio. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

## <a name="the-visual-studio-package-project-template"></a>O modelo de projeto de pacote do Visual Studio
 Você pode encontrar o modelo de projeto de pacote do Visual Studio na caixa de diálogo **novo projeto** na pasta **extensibilidade C++** .

### <a name="to-create-a-vspackage-using-the-visual-studio-package-template"></a>Para criar um VSPackage usando o modelo de pacote do Visual Studio

1. Crie um projeto com o modelo de pacote do Visual Studio.

2. Selecione a opção **editor personalizado** e clique em **Avançar**. A página **Opções do editor** é exibida.

3. Digite o nome do editor na caixa **nome do editor** . Digite a extensão de arquivo que você deseja associar ao editor na caixa extensão de **arquivo** . O editor está disponível para arquivos com esta extensão. A extensão de arquivo é registrada apenas para o Visual Studio, não para o Windows. Digite o nome de arquivo padrão para novos documentos criados com o editor na caixa **nome de arquivo padrão** .

4. Clique em **concluir** para criar o VSPackage na pasta que você especificou.

### <a name="to-test-your-custom-editor"></a>Para testar seu editor personalizado

1. No menu **arquivo** , aponte para **novo** e clique em **arquivo**.

2. No painel **modelos instalados** da caixa de diálogo **novo arquivo** , selecione o modelo de arquivo e o tipo de arquivo que você registrou.

3. Clique em **abrir** para exibir e editar o documento.

     O editor oferece suporte a operações de recortar e colar, localizar e substituir e abrir e carregar.

## <a name="see-also"></a>Confira também
- [VSPackages](../extensibility/internals/vspackages.md)
