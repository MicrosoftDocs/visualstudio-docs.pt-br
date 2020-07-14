---
title: Como salvar e abrir arquivos com codificação
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- Unicode, bidirectional language support
- files, encoding
- bidirectional language support, encoded files
- file encoding, bidirectional languages
ms.assetid: cb52b732-b395-4ba1-a3ef-104b3942a12a
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 72496e842841b2c55833075e890da4b7088cb489
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85284159"
---
# <a name="how-to-save-and-open-files-with-encoding"></a>Como salvar e abrir arquivos com codificação

Salve arquivos com uma codificação de caracteres específica para dar suporte a idiomas bidirecionais. Também é possível especificar uma codificação ao abrir um arquivo, para que o Visual Studio exiba o arquivo corretamente.

## <a name="to-save-a-file-with-encoding"></a>Para salvar um arquivo com codificação

1. No menu **Arquivo**, escolha **Salvar Arquivo Como** e clique no botão suspenso ao lado do botão **Salvar**.

     A caixa de diálogo **Opções de Salvamento Avançadas** é exibida.

2. Em **Codificação**, selecione a codificação a ser usada para o arquivo.

3. Opcionalmente, em **Terminações de linha**, selecione o formato para caracteres de final de linha.

     Essa opção é útil se você pretende trocar o arquivo com usuários de outro sistema operacional.

     Se deseja trabalhar com um arquivo que você sabe que está codificado de uma maneira específica, é possível informar ao Visual Studio para usar essa codificação ao abrir o arquivo. O método usado dependerá se o arquivo faz parte do projeto.

## <a name="to-open-an-encoded-file-that-is-part-of-a-project"></a>Para abrir um arquivo codificado que faz parte de um projeto

1. Em **Gerenciador de Soluções**, clique com o botão direito do mouse no arquivo e escolha **Abrir Com**.

2. Na caixa de diálogo **Abrir Com**, escolha o editor com o qual o arquivo será aberto.

     Muitos editores do Visual Studio, como o editor de formulários, detectarão a codificação automaticamente e abrirão o arquivo de forma adequada. Se você escolher um editor que permite escolher uma codificação, a caixa de diálogo **Codificação** será exibida.

3. Na caixa de diálogo **Codificação**, selecione a codificação que o editor deverá usar.

## <a name="to-open-an-encoded-file-that-is-not-part-of-a-project"></a>Para abrir um arquivo codificado que não faz parte de um projeto

1. No menu **Arquivo**, aponte para **Abrir**, escolha **Arquivo** ou **Arquivo da Web** e, em seguida, selecione o arquivo a ser aberto.

2. Clique no botão suspenso ao lado do botão **Abrir** e escolha **Abrir Com**.

3. Siga as Etapas 2 e 3 do procedimento anterior.

## <a name="see-also"></a>Veja também

- [Codificação e quebras de linha](encodings-and-line-breaks.md)
- [Codificação e globalização do Windows Forms](/dotnet/framework/winforms/advanced/encoding-and-windows-forms-globalization)
- [Globalizar e localizar aplicativos](../ide/globalizing-and-localizing-applications.md)
