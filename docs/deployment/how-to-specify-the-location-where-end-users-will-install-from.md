---
title: Como especificar o local para onde os usuários finais serão instalados | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications [ClickOnce], specifying an installation URL
- URLs, specifying an installation URL
- installation, specifying installation an URL
- Installation URL property
ms.assetid: 04a804bf-ed55-4a7a-a1e6-f63ed99c0276
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 993c654ccd16f2d51d86a46a716edd611ae154dd
ms.sourcegitcommit: bf2e9d4ff38bf5b62b8af3da1e6a183beb899809
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/22/2020
ms.locfileid: "77557606"
---
# <a name="how-to-specify-the-location-where-end-users-will-install-from"></a>Como especificar o local de onde os usuários finais instalarão
Ao publicar um aplicativo [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)], o local em que os usuários acessam baixar e instalar o aplicativo não é necessariamente o local onde você publicará o aplicativo inicialmente. Por exemplo, em algumas organizações, um desenvolvedor pode publicar um aplicativo em um servidor de preparo e, em seguida, um administrador moveria o aplicativo para um servidor Web.

Nesse caso, você pode usar a propriedade `Installation URL` para especificar o servidor Web onde os usuários vão baixar o aplicativo. Isso é necessário para que o manifesto do aplicativo saiba onde procurar atualizações.

A propriedade `Installation URL` pode ser definida na página **publicar** do designer de **projeto**.

> [!NOTE]
> A propriedade `Installation URL` também pode ser definida usando o **PublishWizard**. Para obter mais informações, consulte [como publicar um aplicativo ClickOnce usando o assistente de publicação](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md).

### <a name="to-specify-an-installation-url"></a>Para especificar uma URL de instalação

1. Com um projeto selecionado no **Gerenciador de Soluções**, no menu **Projeto**, clique em **Propriedades**.

2. Clique na guia **Publicar**.

3. No campo URL de instalação, insira o local de instalação usando uma URL totalmente qualificada usando o formato `https://www.contoso.com/ApplicationName`ou um caminho UNC usando o formato `\Server\ApplicationName`.

## <a name="see-also"></a>Consulte também
- [Como especificar para onde o Visual Studio copia os arquivos](../deployment/how-to-specify-where-visual-studio-copies-the-files.md)
- [Publicando aplicativos ClickOnce](../deployment/publishing-clickonce-applications.md)
- [Como publicar um aplicativo ClickOnce usando o Assistente de Publicação](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)