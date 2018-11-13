---
title: -Command (devenv.exe)
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- Devenv, /command switch
- /command Devenv switch
ms.assetid: 13c20cd6-f09d-400a-8b7b-ecc266a32cef
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 1d6d2c5355fbce44bbb97a33e21ad623997ddceb
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50670800"
---
# <a name="command-devenvexe"></a>/Command (devenv.exe)
Executa o comando especificado depois de iniciar o IDE (ambiente de desenvolvimento integrado) do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)].

## <a name="syntax"></a>Sintaxe

```cmd
devenv /command CommandName
```

## <a name="arguments"></a>Arguments
 `CommandName` Necessário. O nome completo de um comando [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ou seu alias, colocado entre aspas duplas. Para obter mais informações sobre comandos e a sintaxe de aliases, consulte [Comandos do Visual Studio](../../ide/reference/visual-studio-commands.md).

## <a name="remarks"></a>Comentários
 Após a conclusão da inicialização, o IDE executa o comando nomeado. Se você usar essa opção, o IDE não mostrará a Página Inicial do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] na inicialização.

 Se um suplemento expor um comando, será possível usar essa opção para iniciar o suplemento por meio da linha de comando. Para obter mais informações, consulte [Como controlar suplementos usando o Gerenciador de Suplementos](https://msdn.microsoft.com/Library/4f60444a-cb48-4cdb-8df4-941f6419aeeb).

## <a name="example"></a>Exemplo
 Esse exemplo inicia [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] e executa a macro Abrir Arquivos Favoritos automaticamente.

```cmd
devenv /command "Macros.MyMacros.Module1.OpenFavoriteFiles"
```

## <a name="see-also"></a>Consulte também

- [Opções de linha de comando devenv](../../ide/reference/devenv-command-line-switches.md)
- [Aliases de comando do Visual Studio](../../ide/reference/visual-studio-command-aliases.md)