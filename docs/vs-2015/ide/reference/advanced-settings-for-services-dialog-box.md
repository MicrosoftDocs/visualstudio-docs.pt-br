---
title: Caixa de diálogo Configurações Avançadas para Serviços | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vb.ProjectPropertiesAdvancedServices
helpviewer_keywords:
- Advanced Settings for Services dialog box
ms.assetid: 6dde4a2d-85e1-4275-aa55-24b84111be91
caps.latest.revision: 18
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 217d1f6f546df94a66c5b7554a7a1710747cf83c
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49291870"
---
# <a name="advanced-settings-for-services-dialog-box"></a>Caixa de diálogo Configurações Avançadas para Serviços
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
Os serviços de aplicativo cliente fornecem acesso simplificado ao logon, às funções e aos serviços de perfil do [!INCLUDE[ajax_current_short](../../includes/ajax-current-short-md.md)] por meio dos aplicativos Windows Forms e WPF (Windows Presentation Foundation). É possível usar a página **Serviços** no **Designer de Projeto** para configurar serviços de aplicativo cliente. Para obter mais informações sobre a página **Serviços**, consulte [Página Serviços, Designer de Projeto](../../ide/reference/services-page-project-designer.md).  
  
 Use a caixa de diálogo **Configurações Avançadas para Serviços** da página **Serviços** no **Designer de Projeto** para definir configurações avançadas para serviços de aplicativo cliente. Ao usar essas configurações, é possível substituir alguns comportamentos padrão do serviço de aplicativo para habilitar cenários menos comuns. Para obter mais informações, consulte [Serviços de aplicativo cliente](http://msdn.microsoft.com/library/1487d8df-089e-4f21-abfb-a791a652b58e).  
  
 Para acessar a caixa de diálogo **Configurações Avançadas para Serviços**, selecione um nó do projeto no **Gerenciador de Soluções** e, em seguida, clique em **Propriedades** no menu **Projeto**. Quando o **Designer de Projeto** for exibido, clique na guia **Serviços** e, em seguida, no botão **Avançado**. Esse botão só será desabilitado quando você habilitar os serviços de aplicativo cliente.  
  
## <a name="task-list"></a>Lista de Tarefas  
 [Como configurar serviços de aplicativo cliente](http://msdn.microsoft.com/library/34a8688a-a32c-40d3-94be-c8e610c6a4e8)  
  
 [Como trabalhar offline com serviços de aplicativo cliente](http://msdn.microsoft.com/en-us/f792cb16-8520-4a0f-9dc9-07bfbc454e38)  
  
## <a name="uielement-list"></a>Lista UIElement  
 **Salvar o hash de senha localmente para habilitar o logon offline**  
 Especifica se um formato criptografado da senha do usuário será armazenado em cache localmente para permitir que o usuário faça logon quando o aplicativo estiver no modo offline. Para obter mais informações, consulte [Como trabalhar offline com serviços de aplicativo cliente](http://msdn.microsoft.com/en-us/f792cb16-8520-4a0f-9dc9-07bfbc454e38). Essa opção é habilitada por padrão.  
  
 **Exige que os usuários façam logon novamente sempre que o cookie de servidor expira**  
 Especifica se os usuários anteriormente autenticados são reautenticados automaticamente quando o aplicativo acessa as funções ou o serviço de perfil e o cookie de autenticação do servidor expira. Selecione essa opção para negar acesso aos serviços de aplicativo e exigir a reautenticação explícita depois que o cookie expirar. Isso é útil para aplicativos implantados em locais públicos, para garantir que os usuários que deixam o aplicativo em execução após o uso não permanecerão autenticados por tempo indefinido. Essa opção é limpa por padrão.  
  
 **Tempo limite do cache do serviço de função**  
 Especifica o tempo em que o provedor de função cliente usará os valores de função armazenados em cache em vez de acessar o serviço de funções. Defina esse intervalo de tempo como um valor pequeno quando as funções forem atualizadas com frequência ou como um valor maior quando as funções forem raramente atualizadas. O valor padrão é um dia.  
  
 O provedor de função acessa os valores de função em cache ou o serviço de funções quando você chama o método <xref:System.Web.Security.RolePrincipal.IsInRole%2A>. Para limpar o cache de forma programática e forçar esse método a acessar o serviço remoto, chame o método <xref:System.Web.ClientServices.Providers.ClientRoleProvider.ResetCache%2A>.  
  
 **Usar uma cadeia de conexão personalizada**  
 Especifica se os provedores de serviço cliente usarão um armazenamento de dados personalizado para o cache local. Por padrão, os provedores de serviço usarão o sistema de arquivos local para o cache. A seleção desta opção populará automaticamente a caixa de texto com uma cadeia de conexão padrão. É possível manter a cadeia de conexão padrão para gerar automaticamente e usar um banco de dados SQL Server Compact Edition ou é possível especificar uma cadeia de conexão para um banco de dados SQL Server existente. Para obter mais informações, consulte [Como configurar serviços de aplicativo cliente](http://msdn.microsoft.com/library/34a8688a-a32c-40d3-94be-c8e610c6a4e8). Essa opção é limpa por padrão.  
  
## <a name="see-also"></a>Consulte também  
 [Serviços de aplicativo cliente](http://msdn.microsoft.com/library/1487d8df-089e-4f21-abfb-a791a652b58e)   
 [Página Serviços, Designer de Projeto](../../ide/reference/services-page-project-designer.md)   
 [Como configurar serviços de aplicativo cliente](http://msdn.microsoft.com/library/34a8688a-a32c-40d3-94be-c8e610c6a4e8)   
 [Como trabalhar offline com serviços de aplicativo cliente](http://msdn.microsoft.com/en-us/f792cb16-8520-4a0f-9dc9-07bfbc454e38)



