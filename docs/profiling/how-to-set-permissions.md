---
title: Como definir permissões | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- profiling, setting permissions
- security [Visual Studio ALM], setting permissions
- permissions [Visual Studio ALM], profiling
- profiling tools, setting profiling permissions
- performance tools, setting profiling permissions
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 03f508bd2ff904898d77cd5ac07c30992da63b46
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85328948"
---
# <a name="how-to-set-permissions"></a>Como definir permissões

Este artigo descreve como um Administrador de um computador concede as permissões de segurança necessárias para a criação de perfil para um usuário ou grupo que não tenha permissões de Administrador no computador.

Um princípio básico de segurança declara que aplicativos devem ser executados apenas com as permissões necessárias. Esse princípio também se aplica aos usuários. Se os usuários puderem ser totalmente eficientes quando estiverem conectados como membros do grupo Usuários em vez do grupo Administradores, eles não deverão receber permissões de Administrador. O primeiro procedimento, "Para criar uma conta de usuário que tenha permissões de Usuário" descreve como criar uma conta de usuário para um membro do grupo Usuários.

Membros do grupo Usuários precisarão de acesso às pastas e arquivos no disco que está compartilhado com outros membros da equipe. O segundo procedimento, "Para conceder acesso a arquivos de projeto compartilhados" descreve como conceder esse acesso.

Membros do grupo Usuários podem executar as ferramentas de criação de perfil se um administrador conceder-lhes acesso ao driver de software das ferramentas de criação de perfil. O último procedimento, "Para conceder acesso ao driver de criação de perfil," descreve como conceder acesso a esse driver.

> [!NOTE]
> Você precisa de permissões de administrador para seguir as etapas nesses procedimentos.

## <a name="to-create-a-user-account-that-has-user-permissions"></a>Para criar uma conta de usuário que tenha permissões de Usuário

1. Clique com o botão direito do mouse em **meu computador** e clique em **gerenciar**.

     A janela **Gerenciamento do Computador** é aberta.

2. Expanda **Usuários e Grupos Locais**.

3. Clique com botão direito do mouse na pasta **Usuários** e, em seguida, clique em **Novo Usuário**.

     A caixa de diálogo **Novo Usuário** é exibida.

4. Preencha os campos nessa caixa de diálogo com as informações da conta de usuário que você está criando. Especifique uma senha. Opcionalmente, marque a caixa de seleção que exige que o usuário altere a senha no próximo logon.

5. Clique em **criar** e em **fechar**.

     O novo usuário aparecerá no grupo Usuários, um grupo de usuários que não têm permissões de Administrador.

## <a name="to-grant-access-to-shared-project-files"></a>Para conceder acesso a arquivos de projeto compartilhados

1. No Windows Explorer (ou Explorador de Arquivos), localize a raiz da árvore de pastas para os arquivos de projeto usados por este usuário e compartilhados pela equipe do projeto.

     O caminho dessa pasta pode ser parecido com o seguinte:

    ```cmd
    D:\ourProject
    ```

2. Clique com botão direito do mouse na pasta e, em seguida, clique em **Propriedades**.

     A caixa de diálogo ** \<folder name> Propriedades** é exibida.

3. Clique na guia **Segurança**.

4. Clique no nome da conta do usuário na caixa **Nomes de usuário ou grupo**.

5. Na caixa **permissões para \<user name> ** , marque a caixa de seleção para **controle total**.

6. Clique em **OK**.

     Isso concede permissões para o usuário para a árvore da pasta compartilhada que começa com a pasta selecionada na etapa 5.

## <a name="to-grant-access-to-the-profiling-driver"></a>Para conceder acesso ao driver de criação de perfil

1. Abra um prompt de comando como administrador.

2. Altere o diretório para:

    ```cmd
    <drive>:\Program Files\Microsoft Visual Studio 14\Team Tools\Performance Tools
    ```

3. Execute o comando a seguir:

    ```cmd
    vsperfcmd /admin:driver,start /admin:service,start
    ```

     Este comando instala e inicia o driver para as ferramentas de criação de perfil.

     Esse comando inicia o serviço e o driver de criação de perfil para que usuários não administradores usem os recursos de criação de perfil que estão disponíveis em seus espaços de processo de Usuário. Somente um Administrador pode executar o comando e ele falhará para usuários não administrativos.

     Observe que os efeitos desta etapa são desfeitos após o computador reiniciar, a menos que você também execute a etapa final deste procedimento.

4. Execute o comando para permitir o acesso à funcionalidade do driver de criação de perfil por um usuário ou grupo que não tem acesso de administrador no computador:

    ```cmd
    vsperfcmd /admin:security,allow,<right[,right],<user name|group name>
    ```

     Esse comando concede o \<user name> \<group name> acesso à conta do ou às ferramentas de criação de perfil. A \<right> opção determina a funcionalidade de criação de perfil que o usuário pode acessar. A \<right> opção pode ser um ou mais dos seguintes valores:

    - FullAccess – permite acesso a todos os métodos de criação de perfil, incluindo a coleta de dados de desempenho de serviços, de amostragem e de criação de perfil entre sessões.

    - SampleProfiling – permite acesso aos métodos de criação de perfil por amostragem

    - CrossSession – permite o acesso à criação de perfil entre sessões o que é necessário para serviços de criação de perfil.

5. (Opcional) Para preservar os resultados de qualquer uma das etapas anteriores depois que o computador reiniciar, execute o seguinte comando:

    ```cmd
    vsperfcmd /admin:driver,autostart,on
    ```

   Os usuários especificados, após o logon, agora poderão usar as ferramentas de criação de perfil sem permissões de Administrador.

## <a name="see-also"></a>Veja também

[Configurar sessões](../profiling/configuring-performance-sessions.md) 
 de desempenho [VSPerfCmd](../profiling/vsperfcmd.md) 
 [Criação de perfil e segurança do Windows Vista](../profiling/profiling-and-windows-vista-security.md)
