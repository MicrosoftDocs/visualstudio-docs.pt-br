---
title: -DoNotLoadProjects (devenv.exe)
description: Saiba como usar a opção de linha de comando DoNotLoadProjects devenv para abrir a solução especificada sem carregar nenhum projeto.
ms.custom: SEO-VS-2020
ms.date: 04/30/2019
ms.topic: reference
helpviewer_keywords:
- Devenv, /DoNotLoadProjects switch
- /DoNotLoadProjects Devenv switch
- DoNotLoadProjects Devenv switch
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: fb43d3a12e50d3f4a7af43721a5e93b769da28ea
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99907584"
---
# <a name="donotloadprojects-devenvexe"></a>/DoNotLoadProjects (devenv.exe)

**Novidades no Visual Studio 2019 versão 16.1**

Abre a solução especificada sem carregar projetos. Confira mais informações em [Soluções filtradas no Visual Studio](../filtered-solutions.md).

## <a name="syntax"></a>Sintaxe

```shell
devenv /DoNotLoadProjects SolutionName
```

## <a name="arguments"></a>Argumentos

*SolutionName*

Obrigatório. O caminho completo e o nome da solução a ser aberta.

## <a name="example"></a>Exemplo

O exemplo abre a solução MySln.sln sem carregar projetos.

```shell
devenv /donotloadprojects MySln.sln
```

## <a name="see-also"></a>Confira também

- [Soluções filtradas no Visual Studio](../filtered-solutions.md)
- [Opções de linha de comando do Devenv](../../ide/reference/devenv-command-line-switches.md)
