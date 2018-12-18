---
title: Como definir permissões | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- profiling, setting permissions
- security [Visual Studio ALM], setting permissions
- permissions [Visual Studio ALM], profiling
- profiling tools, setting profiling permissions
- performance tools, setting profiling permissions
ms.assetid: 69f27896-8f46-4ef3-bfb7-726d95304f3a
caps.latest.revision: 28
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 2bfbcb15d9dae16dd7d65ac00ad7c5b17600fa9d
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51792874"
---
# <a name="how-to-set-permissions"></a>Como definir permissões
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este tópico descreve como um Administrador de um computador concede as permissões de segurança necessárias para a criação de perfil para um usuário ou grupo que não tenha permissões de Administrador no computador.  
  
 Um princípio básico de segurança declara que aplicativos devem ser executados apenas com as permissões necessárias. Esse princípio também se aplica aos usuários. Se os usuários puderem ser totalmente eficientes quando estiverem conectados como membros do grupo Usuários em vez do grupo Administradores, eles não deverão receber permissões de Administrador. O primeiro procedimento, "Para criar uma conta de usuário que tenha permissões de Usuário" descreve como criar uma conta de usuário para um membro do grupo Usuários.  
  
 **Requisitos**  
  
- [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)], [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)], [!INCLUDE[vsPro](../includes/vspro-md.md)]  
  
  Membros do grupo Usuários precisarão de acesso às pastas e arquivos no disco que está compartilhado com outros membros da equipe. O segundo procedimento, "Para conceder acesso a arquivos de projeto compartilhados" descreve como conceder esse acesso.  
  
  Membros do grupo Usuários podem executar as ferramentas de criação de perfil se um administrador conceder-lhes acesso ao driver de software das ferramentas de criação de perfil. O último procedimento, "Para conceder acesso ao driver de criação de perfil," descreve como conceder acesso a esse driver.  
  
> [!NOTE]
>  Você precisa de permissões de administrador para seguir as etapas nesses procedimentos.  
  
### <a name="to-create-a-user-account-that-has-user-permissions"></a>Para criar uma conta de usuário que tenha permissões de Usuário  
  
1.  Clique com botão direito do mouse em **Meu Computador** e, em seguida, clique em **Gerenciar**.  
  
     A janela **Gerenciamento do Computador** é aberta.  
  
2.  Expanda **Usuários e Grupos Locais**.  
  
3.  Clique com botão direito do mouse na pasta **Usuários** e, em seguida, clique em **Novo Usuário**.  
  
     A caixa de diálogo **Novo Usuário** é exibida.  
  
4.  Preencha os campos nessa caixa de diálogo com as informações da conta de usuário que você está criando. Especifique uma senha. Opcionalmente, marque a caixa de seleção que exige que o usuário altere a senha no próximo logon.  
  
5.  Clique em **Criar** e, em seguida, clique em **Fechar**.  
  
     O novo usuário aparecerá no grupo Usuários, um grupo de usuários que não têm permissões de Administrador.  
  
### <a name="to-grant-access-to-shared-project-files"></a>Para conceder acesso a arquivos de projeto compartilhados  
  
1.  No Windows Explorer (ou Explorador de Arquivos), localize a raiz da árvore de pastas para os arquivos de projeto usados por este usuário e compartilhados pela equipe do projeto.  
  
     O caminho dessa pasta pode ser parecido com o seguinte:  
  
    ```  
    D:\ourProject  
    ```  
  
2.  Clique com botão direito do mouse na pasta e, em seguida, clique em **Propriedades**.  
  
     A caixa de diálogo **\<nome da pasta> Propriedades** é exibida.  
  
3.  Clique na guia **Segurança**.  
  
4.  Clique no nome da conta do usuário na caixa **Nomes de usuário ou grupo**.  
  
5.  Na caixa **Permissões para \<nome de usuário>**, marque a caixa de seleção **Controle Total**.  
  
6.  Clique em **OK**.  
  
     Isso concede permissões para o usuário para a árvore da pasta compartilhada que começa com a pasta selecionada na etapa 5.  
  
### <a name="to-grant-access-to-the-profiling-driver"></a>Para conceder acesso ao driver de criação de perfil  
  
1. Abra um prompt de comando como administrador.  
  
2. Altere o diretório para:  
  
   ```  
   <drive>:\Program Files\Microsoft Visual Studio 10\Team Tools\Performance Tools  
   ```  
  
3. Execute o seguinte comando:  
  
   ```  
   vsperfcmd /admin:driver,start /admin:service,start  
   ```  
  
    Este comando instala e inicia o driver para as ferramentas de criação de perfil.  
  
    Esse comando inicia o serviço e o driver de criação de perfil para que usuários não administradores usem os recursos de criação de perfil que estão disponíveis em seus espaços de processo de Usuário. Somente um Administrador pode executar o comando e ele falhará para usuários não administrativos.  
  
    Observe que os efeitos desta etapa são desfeitos após o computador reiniciar, a menos que você também execute a etapa final deste procedimento.  
  
4. Execute o comando para permitir o acesso à funcionalidade do driver de criação de perfil por um usuário ou grupo que não tem acesso de administrador no computador:  
  
   ```  
   vsperfcmd /admin:security,allow,<right[,right],<user name|group name>  
   ```  
  
    Este comando concede à conta \<nome de usuário> ou \<nome do grupo> o acesso às ferramentas de Criação de Perfil. A opção \<direito> determina a funcionalidade de criação de perfil que o usuário pode acessar. A opção \<direito> pode ser um ou mais dos seguintes valores:  
  
   -   FullAccess – permite acesso a todos os métodos de criação de perfil, incluindo a coleta de dados de desempenho de serviços, de amostragem e de criação de perfil entre sessões.  
  
   -   SampleProfiling – permite acesso aos métodos de criação de perfil por amostragem  
  
   -   CrossSession – permite o acesso à criação de perfil entre sessões o que é necessário para serviços de criação de perfil.  
  
5. (Opcional) Para preservar os resultados de qualquer uma das etapas anteriores depois que o computador reiniciar, execute o seguinte comando:  
  
   ```  
   vsperfcmd /admin:driver,autostart,on  
   ```  
  
   Os usuários especificados, após o logon, agora poderão usar as ferramentas de criação de perfil sem permissões de Administrador.  
  
## <a name="see-also"></a>Consulte também  
 [Configurando sessões de desempenho](../profiling/configuring-performance-sessions.md)   
 [VSPerfCmd](../profiling/vsperfcmd.md)   
 [Criação de perfil e segurança do Windows Vista](../profiling/profiling-and-windows-vista-security.md)



