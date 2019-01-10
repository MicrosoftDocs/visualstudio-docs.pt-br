---
title: -Edit (devenv.exe)
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.topic: reference
helpviewer_keywords:
- Devenv, /edit switch
- /Edit Devenv switch
ms.assetid: 02b3d6e7-a2b1-4d83-a747-aa8c2fb758b7
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 0ccbd3a693313b870378021e6404424cfb11f199
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2019
ms.locfileid: "53907982"
---
# <a name="edit-devenvexe"></a>/Edit (devenv.exe)
Abre o arquivo especificado em uma instância existente do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)].

## <a name="syntax"></a>Sintaxe

```cmd
Devenv /edit [file1[ file2]]
```

## <a name="arguments"></a>Arguments
 `file1`

 Opcional. O arquivo a ser aberto em uma instância existente do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]. Se nenhuma instância do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] existir, uma nova instância será criada com um layout de janela simplificado, e o `file1` será aberto na nova instância.

 `file2`

 Opcional. Um ou mais arquivos adicionais a serem abertos na instância existente do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)].

## <a name="remarks"></a>Comentários
 Se nenhum arquivo for especificado e se houver uma instância existente do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)], a instância existente do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] receberá o foco. Se nenhum arquivo for especificado e se não houver nenhuma instância existente do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)], uma nova instância do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] será criada com um layout de janela simplificado.

 Se a instância existente do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] estiver em um estado modal, por exemplo, se a [caixa de diálogo Opções](../../ide/reference/options-dialog-box-visual-studio.md) estiver aberta, o arquivo será aberto na instância existente quando [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] sair do estado modal.

## <a name="example"></a>Exemplo
 Esse exemplo abre o arquivo `MyFile.cs` em uma instância existente do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ou abre o arquivo em uma nova instância da [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] se ainda não existir nenhuma.

```cmd
devenv /edit MyFile.cs
```

## <a name="see-also"></a>Consulte também

- [Opções de linha de comando do Devenv](../../ide/reference/devenv-command-line-switches.md)