---
title: 'Como: verificar as configurações de propriedade do IIS | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- IIS, property settings
- debugging Web applications, troubleshooting
- IIS administration tool
- Web applications, setting properties
- properties [debugger], setting with IIS administration tool
ms.assetid: 9efc50bf-02fb-4750-9b3e-f03c38f10d8b
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 4639055fe9320c8fd1bf1b2575bca323642dd17f
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51742069"
---
# <a name="how-to-verify-iis-property-settings"></a>Como verificar as configurações de propriedade do IIS
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode definir as propriedades de um aplicativo Web usando a ferramenta de administração do IIS. Essas propriedades devem ser definidas corretamente para que o aplicativo seja executado, de modo que verificar essas configurações geralmente é uma etapa necessária na solução de problemas.  
  
> [!NOTE]
>  As caixas de diálogo e os comandos de menu que você vê podem ser diferentes dos descritos na Ajuda, dependendo da sua edição ou das configurações ativas. Para alterar as configurações, escolha **Importar e Exportar Configurações** no menu **Ferramentas**. Para obter mais informações, consulte [Personalizando configurações de desenvolvimento no Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### <a name="to-check-iis-settings-for-the-web-application"></a>Para verificar as configurações do IIS para o aplicativo Web  
  
1.  Abra o **ferramentas administrativas** janela: no **inicie** , aponte para **programas**e, em seguida, clique em **ferramentas administrativas**. Se **ferramentas administrativas** não aparecer na **programas** menu, em seguida, procure-o no **painel de controle**.  
  
    -   No Windows 2000, selecione **Gerenciador de serviços de Internet**.  
  
    -   No Windows XP, selecione **serviços de informações da Internet**.  
  
    -   No Windows Server 2003, clique duas vezes **gerenciar o servidor**.  
  
         O **gerenciar o servidor** janela é aberta. Sob **servidor de aplicativos**, clique em **gerenciar este servidor de aplicativo**.  
  
         O **servidor de aplicativos** janela é aberta. Abra o **serviços de informações da Internet (IIS) Manager** nó no painel esquerdo.  
  
2.  Na caixa de diálogo, clique no nó de controle de árvore para seu computador. Clique o **Sites da Web** nó e selecione o nó do aplicativo da Web. Ele será um nó do site da Web e, portanto, um irmão do **Site da Web padrão** nó ou um nó de diretório virtual sob um nó de site da Web existente.  
  
3.  O aplicativo Web com o botão direito e, em seguida, no menu de atalho, clique em **propriedades**.  
  
4.  Verifique as configurações de segurança para o aplicativo Web:  
  
    1.  No aplicativo Web **propriedades** janela, clique no **segurança de diretório** guia e, em seguida, clique em **editar**.  
  
    2.  No **métodos de autenticação** caixa de diálogo, selecione **habilitar o acesso anônimo** e **autenticação Windows integrada** se eles já não estiverem selecionados.  
  
    3.  Clique em **Okey** para fechar o **métodos de autenticação** caixa de diálogo.  
  
5.  Para um aplicativo do servidor ATL, verifique se o verbo DEBUG está associado à extensão ISAPI. Para obter mais informações, consulte [como: associar o verbo de depuração com a extensão](http://msdn.microsoft.com/en-us/50d261d3-4bd4-41c0-b44e-3591086f121e).  
  
6.  Para um [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] aplicativo, certifique-se a pasta virtual para o aplicativo tem um nome de aplicativo definida **serviços de informações da Internet (IIS) Manager**, **Gerenciador de serviços de Internet** ou  **Serviços de informações da Internet**.  
  
    1.  No aplicativo Web **propriedades** janela, selecione a **diretório** guia, se o aplicativo estiver em um diretório virtual, ou o **diretório base** guia, se o aplicativo está em um site da Web.  
  
    2.  Verifique o nome na **caminho Local** corresponde ao nome do diretório onde o aplicativo foi implantado de fato.  
  
    3.  Sob **configurações do aplicativo**, digite o nome do diretório raiz que contém o aplicativo.  
  
    4.  Clique em **Okey** para fechar o **propriedades** caixa de diálogo.  
  
7.  Para um [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] aplicativo, clique em de **ASP.NET** guia e verificar se a versão correta do [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] for especificado.  
  
8.  Clique em **Okey** para fechar o **propriedades** caixa de diálogo.  
  
9. Clique em **Okey** para fechar o **serviços de informações da Internet (IIS) Manager**, **Gerenciador de serviços de Internet**, ou **serviços de informações da Internet**caixa de diálogo.  
  
## <a name="see-also"></a>Consulte também  
 [Solução de problemas](../debugger/debugging-web-applications-troubleshooting.md)



