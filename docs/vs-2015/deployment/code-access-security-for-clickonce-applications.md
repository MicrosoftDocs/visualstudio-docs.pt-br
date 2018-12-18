---
title: Segurança de acesso do código para aplicativos ClickOnce | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-deployment
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vb.XBAPProjectPropertiesSecurity.HowTo
- vb.XBAProjectPropertiesSecurity.HowTo
- vb.ProjectPropertiesSecurity.HowTo
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications [ClickOnce], security
- ClickOnce applications, caspol
- security [ClickOnce], WPF browser-hosted applications
- security [ClickOnce], ClickOnce applications
- ClickOnce applications, code access security policies
- security, ClickOnce
ms.assetid: 04b104d0-0bd3-4ccb-b164-1de92d234487
caps.latest.revision: 33
author: mikejo5000
ms.author: mikejo
manager: wpickett
ms.openlocfilehash: ea1f91a50180dce6edec17afead5649ecd3e1f50
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49816053"
---
# <a name="code-access-security-for-clickonce-applications"></a>Segurança de acesso do código para aplicativos ClickOnce
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Os aplicativos ClickOnce são baseados no .NET Framework e estão sujeitos a restrições de segurança de acesso do código. Por esse motivo, é importante que você entenda as implicações do código de segurança de acesso e escrever aplicativos ClickOnce adequadamente.  
  
 Segurança de acesso do código é um mecanismo no .NET Framework que ajuda a limitar o acesso de código tem a recursos e operações protegidos. Você deve configurar as permissões de segurança de acesso do código para seu aplicativo usar a zona apropriada para o local do instalador do aplicativo ClickOnce. Na maioria dos casos, você pode escolher o **Internet** zona para um conjunto limitado de permissões ou a **Intranet Local** zona para um maior conjunto de permissões.  
  
## <a name="default-clickonce-code-access-security"></a>Segurança de acesso do código do ClickOnce padrão  
 Por padrão, um aplicativo ClickOnce recebe permissões de confiança total quando for instalado ou executado em um computador cliente.  
  
- Um aplicativo que tenha permissões de confiança total tem acesso irrestrito a recursos como o sistema de arquivos e o registro. Isso potencialmente permite que seu aplicativo (e sistema do usuário final) ser explorada por código mal-intencionado.  
  
- Quando um aplicativo requer permissões de confiança total, o usuário final será solicitado a conceder permissões para o aplicativo. Isso significa que o aplicativo não fornece realmente uma experiência de ClickOnce, e o prompt pode ser potencialmente confuso para usuários menos experientes.  
  
  > [!NOTE]
  >  Ao instalar um aplicativo de mídia removível, como um CD-ROM, o usuário não é solicitado. Além disso, um administrador de rede pode configurar a política de rede para que os usuários não são solicitados ao instalar um aplicativo de uma fonte confiável. Para obter mais informações, consulte [Trusted Application Deployment Overview](../deployment/trusted-application-deployment-overview.md).  
  
  Para restringir as permissões para um aplicativo ClickOnce, você pode modificar as permissões de segurança de acesso do código para seu aplicativo solicitar a zona que melhor se adapta as permissões que seu aplicativo requer. Na maioria dos casos, você pode selecionar a zona da qual o aplicativo está sendo implantado. Por exemplo, se seu aplicativo for um aplicativo empresarial, você pode usar o **Intranet Local** zona. Se seu aplicativo for um aplicativo da internet, você pode usar o **Internet** zona.  
  
## <a name="configuring-security-permissions"></a>Configurar permissões de segurança  
 Você sempre deve configurar seu aplicativo ClickOnce para solicitar a zona apropriada para limitar as permissões de segurança de acesso do código. Você pode configurar permissões de segurança na **segurança** página do **Designer de projeto**.  
  
 O **segurança** página na **Project Designer** contém uma **Habilitar configurações de segurança do ClickOnce** caixa de seleção. Quando essa caixa de seleção é marcada, as solicitações de permissão de segurança são adicionadas ao manifesto de implantação para seu aplicativo. No momento da instalação, o usuário deverá conceder as permissões se as permissões solicitadas excederem as permissões padrão para a zona da qual o aplicativo é implantado. Para obter mais informações, consulte [como: Habilitar configurações de segurança do ClickOnce](../deployment/how-to-enable-clickonce-security-settings.md).  
  
 Os aplicativos implantados em locais diferentes são concedidos a níveis diferentes de permissões sem avisar. Por exemplo, quando um aplicativo é implantado pela Internet, ele recebe um conjunto altamente restritivo de permissões. Quando instalado de uma Intranet local, ele recebe mais permissões e, quando instalado a partir de um CD-ROM, ele recebe permissões de confiança total.  
  
 Como um ponto de partida para configurar permissões, você pode selecionar uma zona de segurança do **zona** lista os **segurança** página. Se seu aplicativo será implantado potencialmente de mais de uma zona, selecione a zona com o mínimo de permissões. Para obter mais informações, consulte [como: definir uma zona de segurança para um aplicativo ClickOnce](../deployment/how-to-set-a-security-zone-for-a-clickonce-application.md).  
  
 Variam de acordo com as propriedades que podem ser definidas pelo conjunto de permissões; nem todos os conjuntos de permissões têm propriedades configuráveis. Para obter mais informações sobre a lista completa de permissões que seu aplicativo pode solicitar, consulte <xref:System.Security.Permissions>. Para obter mais informações sobre como definir permissões para uma zona personalizada, consulte [como: definir permissões personalizadas para um aplicativo ClickOnce](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md).  
  
## <a name="debugging-an-application-that-has-restricted-permissions"></a>Depurando um aplicativo que possui permissões restritas  
 Como desenvolvedor, você provavelmente deve executar seu computador de desenvolvimento com permissões de confiança total. Portanto, você não vir as exceções de segurança mesmo quando você depura o aplicativo que os usuários podem ver quando eles o executam com permissões restritas.  
  
 Para capturar essas exceções, você precisa depurar o aplicativo com as mesmas permissões que o usuário final. Depuração com permissões restritas pode ser habilitada no **segurança** página do **Designer de projeto**.  
  
 Quando você depura um aplicativo com permissões restritas, exceções serão geradas para qualquer demandas de segurança de código não tem sido habilitadas na **segurança** página. Um auxiliar de exceção será exibida, fornecendo sugestões sobre como modificar seu código para evitar a exceção.  
  
 Além disso, quando você escreve o código, o recurso IntelliSense no Editor de códigos desabilitará todos os membros que não estão incluídos nas permissões de segurança que você configurou.  
  
 Para obter mais informações, consulte [como: depurar um aplicativo ClickOnce com permissões restritas](../deployment/how-to-debug-a-clickonce-application-with-restricted-permissions.md).  
  
## <a name="security-permissions-for-browser-hosted-applications"></a>Permissões de segurança para aplicativos hospedados pelo navegador  
 Visual Studio fornece os seguintes tipos de projeto para aplicativos Windows Presentation Foundation (WPF):  
  
- Aplicativo do Windows WPF  
  
- Aplicativo de navegador da Web WPF  
  
- Biblioteca de Controles Personalizados do WPF  
  
- Biblioteca de serviço do WPF  
  
  Desses tipos de projeto, somente aplicativos da Web WPF navegador são hospedados em um navegador da Web e, portanto, exigem especial de implantação e configurações de segurança. As configurações de segurança padrão para esses aplicativos são da seguinte maneira:  
  
- **Habilitar configurações de segurança do ClickOnce**  
  
- **Este é um aplicativo de confiança parcial**  
  
- **Zona da Internet** (com a permissão padrão definido para aplicativos de navegador da Web WPF selecionado)  
  
  No **configurações de segurança avançadas** caixa de diálogo, o **depurar este aplicativo com o conjunto de permissões selecionado** caixa de seleção é marcada e desabilitada. Isso ocorre porque a depuração na zona não pode ser desativada para aplicativos hospedados pelo navegador.  
  
## <a name="see-also"></a>Consulte também  
 [Protegendo aplicativos ClickOnce](../deployment/securing-clickonce-applications.md)   
 [Como habilitar configurações de segurança do ClickOnce](../deployment/how-to-enable-clickonce-security-settings.md)   
 [Como definir uma zona de segurança para um aplicativo ClickOnce](../deployment/how-to-set-a-security-zone-for-a-clickonce-application.md)   
 [Como definir permissões personalizadas para um aplicativo ClickOnce](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)   
 [Como depurar um aplicativo ClickOnce com permissões restritas](../deployment/how-to-debug-a-clickonce-application-with-restricted-permissions.md)   
 [Visão geral da implantação de aplicativos confiáveis](../deployment/trusted-application-deployment-overview.md)   
 [Página Segurança, Designer de Projeto](../ide/reference/security-page-project-designer.md)



