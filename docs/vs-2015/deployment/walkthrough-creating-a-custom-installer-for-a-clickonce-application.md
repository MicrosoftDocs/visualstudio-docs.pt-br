---
title: 'Passo a passo: Criando um instalador personalizado para um aplicativo ClickOnce | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-deployment
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, custom installer
- installer [ClickOnce], custom
- deploying applications [ClickOnce], custom installer
- InPlaceHostingManager [ClickOnce], custom installer
- custom installer [ClickOnce]
ms.assetid: fb222cc5-8aeb-4b94-8c49-b93e342f5f69
caps.latest.revision: 36
author: mikejo5000
ms.author: mikejo
manager: wpickett
ms.openlocfilehash: 16686b0bf53f9e1358d96a7abcfe95f8ed6aac82
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49222762"
---
# <a name="walkthrough-creating-a-custom-installer-for-a-clickonce-application"></a>Instruções passo a passo: criando um instalador personalizado para um aplicativo ClickOnce
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Qualquer aplicativo ClickOnce com base em um arquivo .exe pode ser instalado silenciosamente e atualizado por um instalador personalizado. Um instalador personalizado pode implementar a experiência do usuário personalizada durante a instalação, incluindo caixas de diálogo personalizadas para operações de segurança e manutenção. Para executar operações de instalação, o instalador personalizado usa o <xref:System.Deployment.Application.InPlaceHostingManager> classe. Este passo a passo demonstra como criar um instalador personalizado que instala silenciosamente um aplicativo ClickOnce.  
  
## <a name="prerequisites"></a>Pré-requisitos  
  
### <a name="to-create-a-custom-clickonce-application-installer"></a>Para criar um instalador personalizado do aplicativo ClickOnce  
  
1.  Em seu aplicativo ClickOnce, adicione referências a Deployment e System.  
  
2.  Adicionar uma nova classe ao seu aplicativo e especificar qualquer nome. Este passo a passo usa o nome `MyInstaller`.  
  
3.  Adicione o seguinte `Imports` ou `using` instruções na parte superior da sua nova classe.  
  
    ```vb  
    Imports System.Deployment.Application  
    Imports System.Windows.Forms  
    ```  
  
    ```csharp  
    using System.Deployment.Application;  
    using System.Windows.Forms;  
    ```  
  
4.  Adicione os seguintes métodos à sua classe.  
  
     Esses métodos chamam <xref:System.Deployment.Application.InPlaceHostingManager> métodos para baixar o manifesto de implantação, declarar permissões apropriadas, solicitará ao usuário permissão para instalar e, em seguida, baixar e instalar o aplicativo no cache do ClickOnce. Um instalador personalizado pode especificar que um aplicativo ClickOnce é previamente confiável, ou pode adiar a decisão de confiança a <xref:System.Deployment.Application.InPlaceHostingManager.AssertApplicationRequirements%2A> chamada de método. Esse código previamente relações de confiança do aplicativo.  
  
    > [!NOTE]
    >  As permissões atribuídas confiando previamente não podem exceder as permissões do código do instalador personalizado.  
  
     [!code-csharp[System.Deployment.Application.InPlaceHostingManager#1](../snippets/csharp/VS_Snippets_Winforms/System.Deployment.Application.InPlaceHostingManager/CS/Form1.cs#1)]
     [!code-vb[System.Deployment.Application.InPlaceHostingManager#1](../snippets/visualbasic/VS_Snippets_Winforms/System.Deployment.Application.InPlaceHostingManager/VB/Form1.vb#1)]  
  
5.  Para tentar a instalação do seu código, chame o `InstallApplication` método. Por exemplo, se você nomeou sua classe `MyInstaller`, você pode chamar `InstallApplication` da seguinte maneira.  
  
    ```vb  
    Dim installer As New MyInstaller()  
    installer.InstallApplication("\\myServer\myShare\myApp.application")  
    MessageBox.Show("Installer object created.")  
    ```  
  
    ```csharp  
    MyInstaller installer = new MyInstaller();  
    installer.InstallApplication(@"\\myServer\myShare\myApp.application");  
    MessageBox.Show("Installer object created.");  
    ```  
  
## <a name="next-steps"></a>Próximas etapas  
 Um aplicativo ClickOnce também pode adicionar lógica de atualização personalizado, incluindo uma interface de usuário personalizada para mostrar durante o processo de atualização. Para obter mais informações, consulte <xref:System.Deployment.Application.UpdateCheckInfo>. Um aplicativo ClickOnce também pode suprimir a entrada de menu de início padrão, atalho e entrada de adicionar ou remover programas usando um `<customUX>` elemento. Para obter mais informações, consulte [ \<entryPoint > elemento](../deployment/entrypoint-element-clickonce-application.md) e <xref:System.Deployment.Application.DownloadApplicationCompletedEventArgs.ShortcutAppId%2A>.  
  
## <a name="see-also"></a>Consulte também  
 [Manifesto do aplicativo ClickOnce](../deployment/clickonce-application-manifest.md)   
 [\<entryPoint > elemento](../deployment/entrypoint-element-clickonce-application.md)



