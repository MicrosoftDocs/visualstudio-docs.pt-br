---
title: Como definir permissões personalizadas para um aplicativo ClickOnce | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce applications, permissions
- permissions, ClickOnce applications
ms.assetid: 660459ca-ef73-44a8-b323-610001f63b93
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 17cd398468bd1640e50f6a58004905cfdf6c2ff0
ms.sourcegitcommit: 3f491903e0c10db9a3f3fc0940f7b587fcbf9530
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85382140"
---
# <a name="how-to-set-custom-permissions-for-a-clickonce-application"></a>Como definir permissões personalizadas para um aplicativo ClickOnce
Você pode implantar um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo que usa permissões padrão para a Internet ou zonas de intranet local. Como alternativa, você pode criar uma zona personalizada para as permissões específicas que o aplicativo precisa. Você pode fazer isso Personalizando as permissões de segurança na página **segurança** do designer de **projeto**.

### <a name="to-customize-a-permission"></a>Para personalizar uma permissão

1. Com um projeto selecionado no **Gerenciador de soluções**, no menu **projeto** , clique em **Propriedades**.

2. Clique na guia **Segurança**.

3. Marque a caixa de seleção **Habilitar configurações de segurança do ClickOnce** .

4. Selecione o botão de opção **este é um aplicativo de confiança parcial** .

     Os controles na seção de **permissões de segurança do ClickOnce** estão habilitados.

5. Na lista suspensa a zona em que **seu aplicativo será instalado** , clique em **(personalizado)**.

6. Clique em **Editar permissões XML**.

     O arquivo *app. manifest* é aberto no editor de XML.

7. Antes do `</applicationRequestMinimum>` elemento, adicione o código XML para permissões que seu aplicativo requer.

    > [!NOTE]
    > Você pode usar o `ToXml` método de um conjunto de permissões para gerar o código XML para o manifesto do aplicativo. Por exemplo, para gerar o XML para o <xref:System.Security.Permissions.EnvironmentPermission> conjunto de permissões, chame o <xref:System.Security.Permissions.EnvironmentPermission.ToXml%2A> método.

## <a name="see-also"></a>Veja também
- [Proteger aplicativos ClickOnce](../deployment/securing-clickonce-applications.md)
- [Segurança de acesso do código para aplicativos ClickOnce](../deployment/code-access-security-for-clickonce-applications.md)
