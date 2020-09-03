---
title: Visual Basic IntelliSense
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.Basic.IntelliSense
helpviewer_keywords:
- IntelliSense [Visual Basic]
- IntelliSense [Visual Studio], Visual Basic
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 118de9ec05bcd5c56376376619bea0c5148d36ab
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "75594182"
---
# <a name="intellisense-for-visual-basic-code-files"></a>IntelliSense para arquivos de código do Visual Basic

O editor de código-fonte do Visual Basic oferece os seguintes recursos de IntelliSense:

## <a name="syntax-tips"></a>Dicas de sintaxe

Dicas de sintaxe são exibidas na sintaxe da instrução que você está digitando. Isso é útil para instruções de como [Declare](/dotnet/visual-basic/language-reference/statements/declare-statement).

## <a name="automatic-completion"></a>Conclusão automática

- Conclusão em várias palavras-chave

     Por exemplo, se você digitar `goto` e um espaço, o IntelliSense exibirá uma lista dos rótulos definidos em um menu suspenso. Outras palavras-chave com suporte incluem `Exit`, `Implements`, `Option` e `Declare`.

- Conclusão em `Enum` e `Boolean`

    Quando uma instrução fizer referência a um membro de uma enumeração, o IntelliSense exibirá uma lista dos membros de `Enum`. Quando uma instrução fizer referência a um `Boolean`, o IntelliSense exibirá um menu suspenso de verdadeiro ou falso.

A conclusão pode ser desativada por padrão desmarcando **Listar membros automaticamente** na página de propriedades **Geral** na pasta **Visual Basic**.

Você pode invocar manualmente a conclusão invocando membros da lista, palavra completa **Alt**ou + **seta para a direita**Alt. Para obter mais informações, confira [Usar o IntelliSense](../ide/using-intellisense.md).

## <a name="intellisense-in-zone"></a>IntelliSense por Zona

O IntelliSense por Zona ajuda desenvolvedores de Visual Basic que precisam implantar aplicativos por meio de [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] e que estão restritos a configurações de confiança parcial. Este recurso:

- Permite escolher as permissões com que o aplicativo será executado.

- Exibe APIs na Zona escolhida como disponíveis em Listar Membros e exibe APIs que requerem permissões adicionais como não disponíveis.

Para obter mais informações, consulte [Segurança de acesso do código para aplicativos ClickOnce](../deployment/code-access-security-for-clickonce-applications.md).

## <a name="filtered-completion-lists"></a>Listas de preenchimento filtradas

No Visual Basic, as listas de conclusão do IntelliSense têm dois controles de guia localizados na parte inferior das listas. A guia **Comum**, que é selecionada por padrão, exibe itens que são usados com maior frequência para completar a instrução que você está escrevendo. A guia **Todos** exibe todos os itens disponíveis para preenchimento automático, incluindo aqueles que também estão na guia **Comum**.

## <a name="see-also"></a>Confira também

- [Usar o IntelliSense](../ide/using-intellisense.md)
