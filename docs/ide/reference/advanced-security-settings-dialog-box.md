---
title: Caixa de diálogo Configurações de Segurança Avançadas
ms.date: 06/27/2018
ms.technology: vs-ide-deployment
ms.topic: reference
f1_keywords:
- vs.err.debug_in_zone_no_hostproc
helpviewer_keywords:
- Advanced Security Settings dialog box
ms.assetid: 2e7aefe9-6d20-4f3e-b257-aee1ebcc6f5d
author: Mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5d34d1b16f36c90f4200a091050d1646fc563d33
ms.sourcegitcommit: 9e15138a34532b222e80f6b42b1a9de7b2fe0175
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85419075"
---
# <a name="advanced-security-settings-dialog-box"></a>Caixa de diálogo Configurações de Segurança Avançadas

Essa caixa de diálogo permite especificar configurações de segurança relacionadas à depuração na zona.

![Caixa de diálogo Configurações de Segurança Avançada no Visual Studio](../media/advanced-security-settings.png)

Para acessar essa caixa de diálogo, selecione um nó do projeto no **Gerenciador de Soluções** e, no menu **Projeto**, clique em **Propriedades**. Quando o **Designer de projeto** for exibido, clique na guia **segurança** . Na página **segurança** , selecione **Habilitar configurações de segurança do ClickOnce**, clique em **este é um aplicativo de confiança parcial**e, em seguida, clique em **avançado**.

## <a name="uielement-list"></a>Lista de elementos de interface do usuário

**Conceder ao aplicativo acesso ao site de origem**

Se você marcar esta caixa de seleção, o aplicativo poderá acessar o site da Web ou o compartilhamento do servidor no qual ele é publicado. Por padrão, essa opção é selecionada.

**Depurar este aplicativo como se ele tivesse sido baixado da seguinte URL**

Se você precisar permitir que o aplicativo acesse o site ou o compartilhamento do servidor correspondente à **URL de Instalação** especificada na página **Publicar**, insira a URL aqui. Essa opção está disponível apenas quando **Conceder ao aplicativo acesso ao site de origem** está selecionado.

## <a name="see-also"></a>Veja também

- [Página Segurança, Designer de Projeto](../../ide/reference/security-page-project-designer.md)
