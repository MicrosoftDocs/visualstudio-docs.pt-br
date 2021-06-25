---
title: Utilitário CreatePkgDef | Microsoft Docs
description: Saiba mais sobre o utilitário CreatePkgDef que leva um arquivo .dll para uma extensão Visual Studio como um parâmetro e cria um arquivo .pkgdef para acompanhar o arquivo .dll.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- package definition
- create pkgdef
- pkgdef
- createpkgdef
ms.assetid: c745cb76-47a6-49ff-9eed-16af0f748e35
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: bfbd4b42d9ceddd40e08c28926a59aecba719fe9
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898117"
---
# <a name="createpkgdef-utility"></a>Utilitário CreatePkgDef
Aceita um .dll para uma extensão Visual Studio como um parâmetro e cria um *arquivo .pkgdef* para acompanhar o *arquivo.dll* arquivo. O *arquivo .pkgdef* contém todas as informações que, de outra forma, seriam escritas no registro do sistema quando a extensão for instalada.

> [!NOTE]
> A maioria dos modelos de projeto incluídos no SDK do Visual Studio cria automaticamente arquivos *.pkgdef* como parte do processo de build. Este documento destina-se a aqueles que querem criar pacotes manualmente ou converter pacotes existentes para usar a implantação *.pkgdef.*

## <a name="syntax"></a>Sintaxe

```
CreatePkgDef /out=<FileName> [/codebase] [/assembly] <AssemblyPath>
```

## <a name="arguments"></a>Argumentos
**/out= &lt; FileName&gt;**\
Obrigatórios. Define o nome do arquivo *de saída .pkgdef* como &lt; &gt; FileName.

**/codebase**\
Opcional. Força o registro com o **utilitário CodeBase.**

**/assembly**\
Força o registro com o **utilitário Assembly.**

**&lt;Assemblypath&gt;**\
O caminho do arquivo *.dll* do qual você deseja gerar *o .pkgdef.*

## <a name="remarks"></a>Comentários
A implantação de extensão *usando arquivos .pkgdef* substitui os requisitos do Registro de versões anteriores do Visual Studio.

::: moniker range=">=vs-2019"

Os *arquivos .pkgdef* devem ser instalados em um dos seguintes locais:

- *%localappdata%\Microsoft\Visual Studio\16.0\Extensions\\*

- *%vsinstalldir%\Common7\IDE\Extensions\\*

Se a pasta de instalação for *%localappdata%\Microsoft\Visual Studio\16.0\Extensions, \\* a extensão será reconhecida pelo Visual Studio mas será desabilitada por padrão. O usuário pode habilitar a extensão usando **Gerenciar Extensões**.

Se a pasta de instalação for *%vsinstalldir%\Common7\IDE\Extensions, \\* a extensão será habilitada por padrão.

> [!NOTE]
> A **ferramenta Gerenciar Extensões** não pode ser usada para acessar uma extensão, a menos que ela seja instalada como parte de um pacote VSIX.

::: moniker-end

::: moniker range="vs-2017"

Os *arquivos .pkgdef* devem ser instalados em um dos seguintes locais:

- *%localappdata%\Microsoft\Visual Studio\15.0\Extensions\\*

- *%vsinstalldir%\Common7\IDE\Extensions\\*

Se a pasta de instalação for *%localappdata%\Microsoft\Visual Studio\15.0\Extensions \\*, a extensão será reconhecida pelo Visual Studio mas será desabilitada por padrão. O usuário pode habilitar a extensão usando **Extensões e Atualizações**.

Se a pasta de instalação for *%vsinstalldir%\Common7\IDE\Extensions, \\* a extensão será habilitada por padrão.

> [!NOTE]
> A **ferramenta Extensões e Atualizações** não pode ser usada para acessar uma extensão, a menos que ela seja instalada como parte de um pacote VSIX.

::: moniker-end

## <a name="see-also"></a>Confira também
- [Utilitário CreateExpInstance](../../extensibility/internals/createexpinstance-utility.md)
