---
title: O que há de novo no SDK do Visual Studio 2019 | Microsoft Docs
description: O SDK do Visual Studio os recursos novos e atualizados para o Visual Studio 2019, incluindo aprimoramentos de registro do editor.
ms.custom: SEO-VS-2020
ms.date: 03/29/2019
ms.topic: conceptual
ms.assetid: 4a07607b-0c87-4866-acd8-6d68358d6a47
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2d8e08136eb142e5e72c08e23860bf94f01dc87c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105061895"
---
# <a name="whats-new-in-the-visual-studio-2019-sdk"></a>Novidades do SDK do Visual Studio 2019

O SDK do Visual Studio tem os seguintes recursos novos e atualizados para o Visual Studio 2019.

## <a name="synchronously-autoloaded-extensions-warning"></a>Aviso de extensões autocarregadas de forma síncrona

Agora, os usuários verão um aviso se qualquer uma de suas extensões instaladas for carregada de forma síncrona na inicialização. Você pode saber mais sobre o aviso em [extensões autocarregadas](synchronously-autoloaded-extensions.md)de forma síncrona.

## <a name="single-unified-visual-studio-sdk"></a>SDK único e unificado do Visual Studio

Agora você pode obter todos os ativos do SDK do Visual Studio por meio de um único pacote NuGet [Microsoft. VisualStudio. SDK](https://www.nuget.org/packages/microsoft.visualstudio.sdk).

## <a name="editor-registration-enhancements"></a>Aprimoramentos no registro do editor

Desde sua criação, o Visual Studio tem suporte para o registro de editor personalizado, em que um editor pode declarar sua afinidade para extensões específicas (por exemplo,. XAML e. rc), ou que seja adequado para qualquer extensão (. *). A partir do Visual Studio 2019 versão 16,1, ampliamos o suporte para o registro do editor.

### <a name="filenames"></a>Nomes de arquivos

Além de, ou em vez de, registrar o suporte para uma extensão de arquivo específica, um editor pode registrar que oferece suporte a nomes de arquivos específicos aplicando o novo `ProvideEditorFilename` atributo ao pacote do editor.

Por exemplo, um editor que dá suporte a todos os arquivos. JSON aplica esse `ProvideEditorExtension` atributo ao seu pacote:

```cs
[ProvideEditorExtension(typeof(MyEditor), ".json", MyEditor.Priority)]
```

A partir do 16,1, se o myediter der suporte apenas a alguns arquivos. JSON conhecidos, ele poderá aplicar esses `ProvideEditorFilename` atributos ao pacote:

```cs
[ProvideEditorFilename(typeof(MyEditor), "particular.json", MyEditor.Priority)]
[ProvideEditorFilename(typeof(MyEditor), "special.json",    MyEditor.Priority)]
```

### <a name="uicontexts"></a>UIContexts

Um editor pode registrar um ou mais UIContexts que representam quando ele está habilitado. UIContexts são registrados pela aplicação de uma ou mais instâncias do `ProvideEditorUIContextAttribute` ao pacote que registra o editor.

Se um editor tiver registrado UIContexts:

- Se pelo menos um de seus UIContexts registrados estiver ativo quando um arquivo com a extensão fornecida for aberto, o editor será incluído na pesquisa do editor.
- Se nenhuma das UIContexts registradas estiver ativa, o editor não será incluído na pesquisa do editor.

Se um editor não registrar nenhum UIContexts, ele sempre será incluído na pesquisa do editor para essa extensão.

Por exemplo, se um editor estiver disponível apenas quando um projeto C# estiver aberto, ele poderá declarar essa afinidade aplicando um `ProvideEditorUIContext` atributo:

```cs
[ProvideEditorUIContext(typeof(MyEditor), KnownUIContexts.CSharpProjectContext)]
```
