---
title: Como definir uma zona de segurança para um aplicativo ClickOnce | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, security settings
- code access security, ClickOnce applications
- security zones, ClickOnce applications
ms.assetid: d3dac454-518a-44d7-a76e-ccb7b9c3a150
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 51515339c24ea8a0507c47d0399cde9e423f71a0
ms.sourcegitcommit: 3f491903e0c10db9a3f3fc0940f7b587fcbf9530
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85382127"
---
# <a name="how-to-set-a-security-zone-for-a-clickonce-application"></a>Como definir uma zona de segurança para um aplicativo ClickOnce
Ao definir permissões de segurança de acesso de código para um aplicativo ClickOnce, você precisa começar com um conjunto base de permissões na página **segurança** do **Designer de projeto**.

 Na maioria dos casos, você também pode escolher a zona da **Internet** que contém um conjunto limitado de permissões ou a zona **da intranet local** que contém um conjunto maior de permissões. Se seu aplicativo exigir permissões personalizadas, você poderá fazer isso escolhendo a zona de segurança **personalizada** . Para obter mais informações sobre como definir permissões personalizadas, consulte [como: definir permissões personalizadas para um aplicativo ClickOnce](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md).

### <a name="to-set-a-security-zone"></a>Para definir uma zona de segurança

1. Com um projeto selecionado no **Gerenciador de Soluções**, no menu **Projeto**, clique em **Propriedades**.

2. Clique na guia **Segurança**.

3. Marque a caixa de seleção **Habilitar configurações de segurança do ClickOnce** .

4. Selecione o botão de opção **este é um aplicativo de confiança parcial** .

     Os controles na seção de **permissões de segurança do ClickOnce** estão habilitados.

5. Na lista suspensa zona em que **seu aplicativo será instalado** , selecione uma zona de segurança.

## <a name="see-also"></a>Veja também
- [Como definir permissões personalizadas em um aplicativo ClickOnce](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)
- [Proteger aplicativos ClickOnce](../deployment/securing-clickonce-applications.md)
- [Segurança de acesso do código para aplicativos ClickOnce](../deployment/code-access-security-for-clickonce-applications.md)
