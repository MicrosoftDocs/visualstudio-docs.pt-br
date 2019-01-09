---
title: Comando Adicionar Projeto Existente
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.topic: reference
f1_keywords:
- file.addexistingproject
helpviewer_keywords:
- Add Existing Project command
- File.AddExistingProject
ms.assetid: 71cf3e31-c76b-405b-ad6a-1b1bc654bd40
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 2a5b0579037d31cf88de32f4fabda531d92c1b61
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2019
ms.locfileid: "53880449"
---
# <a name="add-existing-project-command"></a>Comando Adicionar Projeto Existente
Adiciona um projeto existente à solução atual.

## <a name="syntax"></a>Sintaxe

```cmd
File.AddExistingProject filename
```

## <a name="arguments"></a>Arguments
 `filename` Opcional. O caminho completo e nome do projeto, com a extensão, do projeto a adicionar à solução.

 Se o argumento `filename` incluir espaços, ele deverá ficar entre aspas.

 Se nenhum nome de arquivo for especificado, o comando abrirá a caixa de diálogo de arquivo para que o usuário possa escolher um projeto.

## <a name="remarks"></a>Comentários
 O preenchimento automático tenta localizar o caminho e o nome do arquivo corretos enquanto você digita.

## <a name="example"></a>Exemplo
 Este exemplo adiciona o projeto [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)], TestProject1, à solução atual.

```cmd
>File.AddExistingProject "c:\visual studio projects\TestProject1.vbproj"
```

## <a name="see-also"></a>Consulte também

- [Comandos do Visual Studio](../../ide/reference/visual-studio-commands.md)
- [Janela Comando](../../ide/reference/command-window.md)
- [Caixa Localizar/Comando](../../ide/find-command-box.md)
- [Aliases de comando do Visual Studio](../../ide/reference/visual-studio-command-aliases.md)