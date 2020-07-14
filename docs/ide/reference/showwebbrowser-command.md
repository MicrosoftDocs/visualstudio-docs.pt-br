---
title: Comando ShowWebBrowser
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- view.showwebbrowser
helpviewer_keywords:
- ShowWebBrowser command
- View.ShowWebBrowser command
ms.assetid: c6a4fbd6-8e9d-45cc-8b2f-93990d065e78
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f8266a7c70544d8a320658fcd8b9f5ad249162fe
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85769567"
---
# <a name="showwebbrowser-command"></a>Comando ShowWebBrowser

Exibe a URL especificada em uma janela de navegador da Web, tanto dentro do IDE (ambiente de desenvolvimento integrado) ou externa ao IDE.

## <a name="syntax"></a>Sintaxe

```cmd
View.ShowWebBrowser URL [/new][/ext]
```

## <a name="arguments"></a>Argumentos
`URL`

Obrigatórios. URL (Uniform Resource Locator) do site da Web.

## <a name="switches"></a>Opções
/new

Opcional. Especifica que a página é exibida em uma nova instância do navegador da Web.

/ext

Opcional. Especifica que a página é exibida no navegador da Web padrão fora do IDE.

## <a name="remarks"></a>Comentários
O alias do comando **ShowWebBrowser** é **navegue** ou **nav**.

## <a name="example"></a>Exemplo
O exemplo a seguir exibe a home page do Microsoft Docs em um navegador da Web fora do IDE. Se uma instância do navegador da Web já estiver aberta, ela será usada; caso contrário, uma nova instância será iniciada.

```cmd
>View.ShowWebBrowser https://docs.microsoft.com /ext
```

## <a name="see-also"></a>Confira também

- [Comandos do Visual Studio](../../ide/reference/visual-studio-commands.md)
- [Janela de comando](../../ide/reference/command-window.md)
- [Caixa Localizar/comando](../../ide/find-command-box.md)
- [Aliases de comando do Visual Studio](../../ide/reference/visual-studio-command-aliases.md)