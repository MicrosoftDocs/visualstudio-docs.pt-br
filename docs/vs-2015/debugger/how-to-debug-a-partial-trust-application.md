---
title: 'Como: depurar um aplicativo de confiança parcial | Microsoft Docs'
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
- debugging [Visual Studio], partial trust applications
- partial trust applications
- security [Visual Studio], partial trust applications
ms.assetid: 9d30ad92-28ce-4b21-91d8-698474cddf64
caps.latest.revision: 28
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 76cce8cfcf57f956b5de16b72f7a275e1d629630
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51782044"
---
# <a name="how-to-debug-a-partial-trust-application"></a>Como depurar um aplicativo parcialmente confiável
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Aplica-se a aplicativos do Windows e do console.  
  
 [Implantação e segurança do ClickOnce](../deployment/clickonce-security-and-deployment.md) torna mais fácil implantar aplicativos de confiança parcial que aproveitam [Code Access Security](http://msdn.microsoft.com/library/859af632-c80d-4736-8d6f-1e01b09ce127) para limitar o acesso a recursos em um computador.  
  
 Depurar um aplicativo de confiança parcial pode ser um desafio, porque os aplicativos de confiança parcial têm permissões de segurança diferentes (e, portanto, comportam-se diferente) dependendo de onde são instalados. Se for instalado da Internet, um aplicativo de confiança parcial terá algumas permissões. Se for instalado de uma intranet local, terá mais permissões e, se for instalado do computador local, terá permissões completas. Você também pode ter zonas personalizados, com permissões personalizadas. Você pode precisar depurar um aplicativo de confiança parcial em algumas ou todas essas condições. Felizmente, o Visual Studio facilita isso também.  
  
 Antes de iniciar uma sessão de depuração no Visual Studio, você pode escolher a zona que deseja simular a instalação de um aplicativo. Quando você iniciar a depuração, o aplicativo terá as permissões adequadas para um aplicativo de confiança parcial instalado a partir dessa zona. Isso permite ver o comportamento do aplicativo que seria exibido para um usuário que faz o download a partir dessa zona.  
  
 Se o aplicativo tentar executar uma ação para a qual não tem permissão, ocorre uma exceção. Nesse ponto, o Assistente de Exceção oferece a possibilidade adicionar uma permissão adicional, que permite reiniciar a sessão de depuração com permissões suficientes para evitar o problema.  
  
 Posteriormente, você pode voltar e ver quais permissões foram adicionadas durante a depuração. Se você tivesse que adicionar uma permissão ao depurar, ela provavelmente indicaria que você precisa adicionar uma solicitação de consentimento do usuário nesse momento em seu código.  
  
> [!NOTE]
>  Os visualizadores do depurador exigem privilégios maiores do que são permitidos por um aplicativo de confiança parcial. Os visualizadores não serão carregados quando você for interrompido no código com confiança parcial. Para depurar usando um visualizador, você deverá executar o código com confiança total.  
  
### <a name="to-choose-a-zone-for-your-partial-trust-application"></a>Para escolher uma zona para seu aplicativo de confiança parcial  
  
1.  Dos **Project** menu, escolha _Projectname_**propriedades**.  
  
2.  No *NomeDoProjeto* páginas de propriedades, clique no **segurança** página.  
  
3.  Selecione **Habilitar configurações de segurança do ClickOnce**.  
  
4.  Sob **seu aplicativo será instalado a partir de zona**, clique em caixa de listagem suspensa e escolha a zona que você deseja simular o aplicativo que está sendo instalado em.  
  
     O **as permissões exigidas pelo aplicativo** grade mostra todas as permissões disponíveis. A marca de seleção indica as permissões concedidas ao aplicativo.  
  
5.  Se a zona que você escolher foi **(personalizado)**, selecione as configurações personalizadas corretas na **configuração** coluna do **permissões** grade.  
  
6.  Clique em **OK** para fechar as páginas de propriedades.  
  
### <a name="to-add-an-extra-permission-when-a-security-exception-occurs"></a>Para adicionar uma permissão extra quando ocorrer uma exceção de segurança  
  
1.  O **Assistente de exceção** caixa de diálogo é exibida com a mensagem: **SecurityException sem tratamento.**  
  
2.  No **Assistente de exceção** caixa de diálogo **ações**, clique em **adicionar permissão ao projeto**.  
  
3.  O **reiniciar depuração** caixa de diálogo é exibida.  
  
    -   Se você deseja reiniciar a sessão de depuração com a nova permissão, clique em **Sim**.  
  
    -   Se você não quiser reiniciar ainda, clique em **não**.  
  
### <a name="to-view-extra-permissions-added-while-debugging"></a>Para exibir as permissões adicionais adicionadas durante a depuração  
  
1.  Dos **Project** menu, escolha _Projectname_**propriedades**.  
  
2.  No *NomeDoProjeto* páginas de propriedades, clique no **segurança** página.  
  
3.  Examine os **as permissões exigidas pelo aplicativo** grade. Qualquer permissão adicional que você adicionou tem dois ícones na **incluídos** coluna: a marca de seleção normal, que tem permissões, todos incluídos e um ícone adicional, que se parece com um balão que contém a letra "i".  
  
4.  Use a barra de rolagem vertical para exibir todo o **as permissões exigidas pelo aplicativo** grade.  
  
## <a name="see-also"></a>Consulte também  
 [Segurança e implantação do ClickOnce](../deployment/clickonce-security-and-deployment.md)   
 [Segurança do depurador](../debugger/debugger-security.md)



