---
title: Segurança para soluções do SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- security [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, security
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: b014c3b4ada42982c41928ca17472e3f585af3ed
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49878759"
---
# <a name="security-for-sharepoint-solutions"></a>Segurança para soluções do SharePoint
  [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] incorpora os seguintes recursos para ajudar a reforçar a segurança dos aplicativos do SharePoint.

## <a name="safe-control-entries"></a>Entradas de controle seguro
 Cada item de projeto do SharePoint criado na [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] tem uma **entradas de controle seguro** coleção de controles de propriedade que representa um cofre. Sua **seguro** subpropriedade permite que você especifique os controles que você considerar seguros. Para obter mais informações, consulte [fornecer informações de implantação de pacote e em itens de projeto](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md) e [especificando seguro Web Parts](http://go.microsoft.com/fwlink/?LinkId=177521).

## <a name="allowpartiallytrustedcallers-attribute"></a>Atributo AllowPartiallyTrustedCallers
 Por padrão, somente aplicativos que são totalmente confiáveis pelo sistema de CAS (segurança) de acesso do código de tempo de execução podem acessar um assembly de código gerenciado compartilhado. Marcar um assembly totalmente confiável com o atributo AllowPartiallyTrustedCallers permite que assemblies parcialmente confiáveis para acessá-lo.

 O atributo AllowPartiallyTrustedCallers é adicionado a qualquer solução do SharePoint que não foi implantada para o cache de assembly global do sistema ( [!INCLUDE[TLA2#tla_gac](../sharepoint/includes/tla2sharptla-gac-md.md)]). Isso inclui soluções em área restrita ou soluções implantadas para o diretório de compartimento de aplicativo do SharePoint. Para obter mais informações, consulte [alterações de segurança versão 1 para o Microsoft .NET Framework](http://go.microsoft.com/fwlink/?LinkId=177515) e [implantação de Web Parts no SharePoint Foundation](http://go.microsoft.com/fwlink/?LinkId=177509).

## <a name="safe-against-script-property"></a>Seguro em relação a propriedade de script
 *Injeção de script* é a inserção de código potencialmente mal-intencionado em controles ou páginas da Web. Para ajudar a proteger os sites do SharePoint 2010 contra injeção de script, os colaboradores não podem exibir ou editar Web parts ou suas propriedades por padrão. Esse comportamento é controlado por um atributo SafeControl chamado SafeAgainstScript. Na [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)], defina esse atributo em um item de projeto **entradas de controle seguro** subpropriedade **seguro contra Script**. Para obter mais informações, consulte [fornecer informações de implantação de pacote e em itens de projeto](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md) e [como: marcar controles como controles seguros](../sharepoint/how-to-mark-controls-as-safe-controls.md).

## <a name="vista-and-windows-7-user-account-control"></a>Windows Vista e o controle de conta de usuário 7
 [!INCLUDE[windowsver](../sharepoint/includes/windowsver-md.md)] e [!INCLUDE[win7](../sharepoint/includes/win7-md.md)] incorporar um recurso de segurança, conhecido como controle de conta de usuário (UAC). Para desenvolver soluções do SharePoint no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] na [!INCLUDE[windowsver](../sharepoint/includes/windowsver-md.md)] e [!INCLUDE[win7](../sharepoint/includes/win7-md.md)] sistemas, o UAC requer que você execute [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] como um administrador do sistema. Do **inicie** menu, abra o menu de atalho [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]e, em seguida, escolha **executar como administrador**.

 Para configurar o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] atalho para sempre executar como administrador, abra o menu de atalho, escolha **propriedades**, escolha o **avançado** botão o **propriedades**caixa de diálogo e, em seguida, selecione o **executar como administrador** caixa de seleção.

 Para obter mais informações, consulte [Compreendendo e configurando o controle de conta de usuário no Windows Vista](http://go.microsoft.com/fwlink/?LinkID=156476). e [controle de conta de usuário do Windows 7](http://go.microsoft.com/fwlink/?LinkId=177523).

## <a name="sharepoint-permissions-considerations"></a>Considerações sobre permissões de SharePoint
 Para desenvolver soluções do SharePoint, você deve ter permissões suficientes para executar e depurar soluções do SharePoint. Antes de testar uma solução do SharePoint, execute as seguintes etapas para garantir que você tenha as permissões necessárias:

1.  Adicione sua conta de usuário como um administrador do sistema.

2.  Adicione sua conta de usuário como um administrador de Farm do SharePoint server.

    1.  Na Administração Central do SharePoint 2010, escolha o **gerenciar o grupo de administradores de farm** link.

    2.  No **os administradores de Farm** , escolha o **New** opção de menu

3.  Adicionar sua conta de usuário ao grupo WSS_ADMIN_WPG.

## <a name="additional-security-resources"></a>Recursos de segurança adicionais
 Para obter mais informações sobre problemas de segurança, consulte o seguinte.

### <a name="visual-studio-security"></a>Segurança do Visual Studio

-   [Segurança e permissões de usuário](http://go.microsoft.com/fwlink/?LinkId=177503)

-   [Segurança no código do .NET Framework e nativos](http://go.microsoft.com/fwlink/?LinkId=177504)

-   [Segurança no .NET Framework](http://go.microsoft.com/fwlink/?LinkId=177502)

### <a name="sharepoint-security"></a>Segurança do SharePoint

-   [Segurança e administração do SharePoint Foundation](http://go.microsoft.com/fwlink/?LinkId=177501)

-   [Central de recursos de segurança do SharePoint](http://go.microsoft.com/fwlink/?LinkId=177498)

-   [Protegendo as Web Parts no SharePoint Foundation](http://go.microsoft.com/fwlink/?LinkId=177511)

-   [Segurança melhoria do aplicativo Web: Ameaças e contramedidas](http://go.microsoft.com/fwlink/?LinkID=140080)

### <a name="general-security"></a>Segurança geral

-   [MSDN Security Development Lifecycle](http://go.microsoft.com/fwlink/?LinkID=147149)

-   [Criação de aplicativos ASP.NET seguros: Autenticação, autorização e comunicação segura](http://go.microsoft.com/fwlink/?LinkId=177494)

## <a name="see-also"></a>Consulte também

- [Desenvolver soluções do SharePoint](../sharepoint/developing-sharepoint-solutions.md)