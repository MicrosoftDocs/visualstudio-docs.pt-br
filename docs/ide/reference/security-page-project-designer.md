---
title: Página Segurança, Designer de Projeto
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- vb.ProjectPropertiesSecurity
- vb.XBAPProjectPropertiesSecurity
helpviewer_keywords:
- Project Designer, Security page
- Security page in Project Designer
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 75877dfd8620af9d3fdfecb5cfcb10761a739515
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31949573"
---
# <a name="security-page-project-designer"></a>Página Segurança, Designer de Projeto

A página **Segurança** do **Designer de Projeto** é usada para definir configurações de segurança de acesso do código para aplicativos implantados usando a implantação do [!INCLUDE[ndptecclick](../../deployment/includes/ndptecclick_md.md)]. Para obter mais informações, consulte [Segurança de acesso do código para aplicativos ClickOnce](../../deployment/code-access-security-for-clickonce-applications.md).

 Para acessar a página **Segurança**, clique em um nó do projeto no **Gerenciador de Soluções** e, em seguida, no menu **Projeto**, clique em **Propriedades**. Quando o **Designer de Projeto** for exibido, clique na guia **Segurança**.

## <a name="security-settings"></a>Configurações de segurança

 **Habilitar configurações de segurança do ClickOnce**

 Determina se as configurações de segurança estão habilitadas no tempo de design. Quando esta opção estiver desmarcada, todas as outras opções na página **Segurança** não ficarão disponíveis.

> [!NOTE]
> Quando você publica um aplicativo usando o assistente **Publicar**, essa opção fica habilitada automaticamente.


 Quando seleciona a opção, você tem a escolha de selecionar um de dois botões de opção: **Este é um aplicativo de confiança total** ou **Este é um aplicativo de confiança parcial**.

 Por padrão, para projetos de Aplicativo de navegador da Web do WPF, essa opção fica selecionada.

 Por padrão, para todos os outros tipos de projeto, a opção fica desmarcada.

 **Este é um aplicativo de confiança total**

 Se você selecionar essa opção, o aplicativo solicitará permissões de Confiança Total quando for instalado ou executado em um computador cliente. Evite usar a Confiança Total, se possível, porque o aplicativo receberá acesso irrestrito a recursos como o sistema de arquivos e o Registro.

 Por padrão, para projetos de Aplicativo de navegador da Web do WPF, essa opção fica definida como Confiança parcial.

 Por padrão, para todos os outros tipos de projeto, a opção fica definida como Confiança Total.

 **Este é um aplicativo de confiança parcial**

 Se você selecionar essa opção, o aplicativo solicitará permissões de Confiança parcial quando for instalado ou executado em um computador cliente. *Confiança parcial* significa que somente as ações permitidas de acordo com as permissões de segurança de acesso de código solicitadas serão executadas. Para obter mais informações sobre como configurar permissões de segurança, consulte [Segurança de acesso do código para aplicativos ClickOnce](../../deployment/code-access-security-for-clickonce-applications.md).

 Você pode especificar as configurações de segurança de Confiança parcial configurando as opções na área **Permissões de Segurança do ClickOnce**.

## <a name="clickonce-security-permissions"></a>Permissões de Segurança do ClickOnce

 **Zona por meio da qual seu aplicativo será instalado**

 Especifica um conjunto padrão de permissões de segurança de acesso de código. Escolha **Internet** ou **Intranet Local** para um conjunto de permissões restritas, ou escolha **(Personalizado)** para configurar um conjunto de permissões personalizadas. Se o aplicativo solicitar mais permissões do que aquelas que são concedidas em uma zona, um prompt de confiança do ClickOnce será exibido para o usuário final conceder as permissões adicionais. Para obter mais informações sobre como configurar permissões de segurança, consulte [Segurança de acesso do código para aplicativos ClickOnce](../../deployment/code-access-security-for-clickonce-applications.md).

 Por padrão, para projetos de Aplicativo de navegador da Web do WPF, essa opção fica definida como **Internet**.

 **Editar XML de Permissões**

 Abre o modelo de manifesto do aplicativo (app.manifest) para configurar as permissões para o conjunto de permissões **(Personalizado)**.

 **Avançado**

 Abre o [Caixa de diálogo Configurações de Segurança Avançadas](../../ide/reference/advanced-security-settings-dialog-box.md), que é usada para definir configurações para depurar o aplicativo com permissões restritas. Essas configurações são verificadas durante a depuração, e exceções de permissão indicam que seu aplicativo pode precisar de mais permissões do que as que foram definidas em uma zona.

## <a name="see-also"></a>Consulte também

- <xref:System.Security.Permissions.WebBrowserPermission>
- <xref:System.Security.Permissions.MediaPermission>
- [Segurança de acesso do código para aplicativos ClickOnce](../../deployment/code-access-security-for-clickonce-applications.md)
- [Como habilitar configurações de segurança do ClickOnce](../../deployment/how-to-enable-clickonce-security-settings.md)
- [Como definir uma zona de segurança para um aplicativo ClickOnce](../../deployment/how-to-set-a-security-zone-for-a-clickonce-application.md)
- [Como definir permissões personalizadas para um aplicativo ClickOnce](../../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)
- [Como depurar um aplicativo ClickOnce com permissões restritas](../../deployment/how-to-debug-a-clickonce-application-with-restricted-permissions.md)
- [Segurança e implantação do ClickOnce](../../deployment/clickonce-security-and-deployment.md)
- [Referência de Propriedades do Projeto](../../ide/reference/project-properties-reference.md)
- [Caixa de diálogo Configurações de Segurança Avançadas](../../ide/reference/advanced-security-settings-dialog-box.md)