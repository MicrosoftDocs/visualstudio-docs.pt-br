---
title: Adicionando serviços móveis usando serviços conectados no Visual Studio | Microsoft Docs
description: Adicionar serviços móveis usando a caixa de diálogo do Visual Studio adicionar serviços conectados
documentationcenter: na
author: ghogen
manager: douge
ms.assetid: 75c3cb93-88e1-476d-a416-f34caa3608e3
ms.topic: conceptual
ms.workload: azure-vs
ms.prod: visual-studio-dev14
ms.technology: vs-azure
ms.custom: vs-azure
ms.date: 12/16/2015
ms.author: mlearned
ms.openlocfilehash: 1679f8e20c4516ab64c4358229b4eec6ab5029ba
ms.sourcegitcommit: e481d0055c0724d20003509000fd5f72fe9d1340
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51001305"
---
# <a name="adding-mobile-services-by-using-visual-studio-connected-services"></a>Adicionando serviços móveis usando o Visual Studio Connected Services
Com o Visual Studio 2015, você pode conectar a serviços móveis do Azure usando o **Adicionar serviço conectado** caixa de diálogo. Você pode se conectar de qualquer C# aplicativo cliente, qualquer aplicativo JavaScript ou aplicativo do Cordova entre plataformas. Depois que você se conectar, você pode criar e acessar dados, criar APIs personalizadas e trabalhos agendados ou adicionar suporte para notificações por push.  A operação de serviços conectados adiciona todas as referências apropriadas e código de conexão. Você também pode tirar proveito do suporte interno para autenticação com uma variedade de esquemas de identidade populares, como o Azure AD, Facebook, Twitter e Microsoft Accounts.

## <a name="supported-project-types"></a>Tipos de projeto com suporte
> [!NOTE]
> No Visual Studio 2015, a adição de serviços móveis do Azure para um projeto do Windows Universal (Windows 10) usando a caixa de diálogo Adicionar serviços conectados não é suportada. Você pode adicionar serviços móveis do Azure instalando os pacotes adequados usando o Gerenciador de pacotes do NuGet para seu projeto.
> 
> 

Você pode usar a caixa de diálogo Serviços conectados para se conectar a serviços móveis do Azure nos seguintes tipos de projeto.

* Projetos de aplicativo Universal, Phone e .NET Windows 8.1 Store
* Projetos do JavaScript Windows 8.1 Store, Phone e aplicativos universais
* Projetos criados usando ferramentas do Visual Studio para Apache Cordova

## <a name="connect-to-azure-mobile-services-using-the-add-connected-services-dialog"></a>Conectar-se ao Azure Mobile Services usando a caixa de diálogo Adicionar serviços conectados
1. Verifique se que você tem uma conta do Azure. Se você não tiver uma conta do Azure, você pode se inscrever para uma [avaliação gratuita](http://go.microsoft.com/fwlink/?LinkId=518146).
2. Abra o **adicionar serviços conectados** caixa de diálogo.
   
   * Para aplicativos .NET, abra o projeto no Visual Studio, abra o menu de contexto para o **referências** nó no Gerenciador de soluções e, em seguida, escolha **Adicionar serviço conectado**
     
        ![Conectar-se ao serviço móvel do Azure](./media/vs-azure-tools-connected-services-add-mobile-services/IC797635.png)
   * Para projetos de aplicativo do Apache Cordova, abra o projeto no Visual Studio, abra o menu de contexto do nó do projeto no Solution Explorer e, em seguida, escolha **Adicionar serviço conectado**.
3. No **Adicionar serviço conectado** diálogo caixa, escolha **serviços móveis do Azure**e, em seguida, escolha o **configurar** botão. Você será solicitado a fazer logon no Azure, se você ainda não fez isso.
   
    ![Adicionando um serviço móvel do Azure](./media/vs-azure-tools-connected-services-add-mobile-services/IC797636.png)
4. No **serviços móveis do Azure** caixa de diálogo, escolha um serviço móvel existente, se você tiver uma. Se você precisar criar um novo serviço móvel do Azure, siga o procedimento a seguir para fazer isso. Caso contrário, pule para a próxima etapa.
   
    Para criar uma nova conta de serviço móvel:
   
   1. Escolha o * * criar serviço * * o link na parte inferior da caixa de diálogo.
       ![Adicionar novo serviço conectado móvel](./media/vs-azure-tools-connected-services-add-mobile-services/IC797637.png)
   2. Sobre o **criar serviço móvel** caixa de diálogo, você pode escolher um serviço móvel de back-end JavaScript, ou um serviço móvel de back-end do .NET do **tempo de execução** lista suspensa. 
      
       ![Criando um serviço móvel](./media/vs-azure-tools-connected-services-add-mobile-services/IC797638.png)
      
       Um serviço de back-end do JavaScript é simples e eficiente. Se você criar um serviço móvel de back-end do JavaScript, o código de JavaScript do lado do servidor é armazenado na nuvem, mas você pode editar scripts de servidor usando o Gerenciador de servidores ou o portal de gerenciamento do Azure. 
      
       Um serviço móvel de back-end do .NET lhe dá total poder e flexibilidade da API Web e o Entity Framework. Se você criar um serviço móvel de back-end do .NET, um projeto é criado para você e adicionado à sua solução. 
   3. Escolha o **região** onde você deseja que o serviço móvel e, em seguida, insira um nome de usuário e senha para o servidor.
   4. Depois de inserir todas as informações necessárias, escolha o **criar** botão para criar o serviço móvel.
   5. O novo serviço móvel deve aparecer na lista de serviços na **serviços móveis do Azure** caixa de diálogo. Escolha o novo serviço móvel na lista e, em seguida, escolha o **adicionar** botão para adicionar o serviço ao seu projeto.
5. Examine a página de Introdução que aparece e descubra como o projeto foi modificado. Uma página de Introdução é exibida no navegador sempre que você adicionar um serviço conectado. Você pode examinar as próximas etapas sugeridas e exemplos de código ou alternar para a página o que aconteceu para ver quais referências foram adicionadas ao seu projeto e como seu código e arquivos de configuração foram modificados.
6. Usando os exemplos de código como guia, comece a escrever código para acessar seu serviço móvel!

## <a name="how-your-project-is-modified"></a>Como o projeto é modificado
Como o Visual Studio modifica seu projeto depende do tipo de projeto. Para C# aplicativos de cliente, consulte [o que aconteceu – C# projetos](http://go.microsoft.com/fwlink/p/?LinkId=513119). Para aplicativos de cliente JavaScript, consulte [o que aconteceu – projetos JavaScript](http://go.microsoft.com/fwlink/p/?LinkId=513120). Para aplicativos Cordova, consulte [o que aconteceu – projetos Cordova](http://go.microsoft.com/fwlink/p/?LinkId=513116).

## <a name="next-steps"></a>Próximas etapas
Faça perguntas e obtenha ajuda: 

* [Fórum do MSDN: Os serviços móveis do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=azuremobile)
* [Serviços móveis do Azure no blog da equipe do Microsoft Azure](https://azure.microsoft.com/blog/topics/mobile/)
* [Serviços móveis do Azure em azure.microsoft.com](https://azure.microsoft.com/services/mobile-services/)
* [Documentação de serviços móveis do Azure em azure.microsoft.com](https://azure.microsoft.com/documentation/services/mobile-services/)

