---
title: Atualizar arquivos. mdf | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- SQL Server Express
- SQL Server LocalDB
- LocalDB
- SQLEXPRESS
- upgrading SQLExpress to SQLExpress
- upgrading to LocalDB
ms.assetid: 14ca6f76-f80e-4926-8020-3fee2d802b75
caps.latest.revision: 36
author: gewarren
ms.author: gewarren
manager: ghogen
robots: noindex,nofollow
ms.openlocfilehash: d71b38fe0d4aef412860a9dc65002c9b8d98c79c
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49812628"
---
# <a name="upgrade-mdf-files"></a>Atualizar arquivos .mdf
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Este tópico descreve as opções para atualizar seu arquivo de banco de dados (. mdf) depois de instalar uma versão mais recente do Visual Studio. Ele inclui instruções para as seguintes tarefas:  
  
- Atualizar um arquivo de banco de dados para usar uma versão mais recente do SQL Server Express LocalDB  
  
- Atualizar um arquivo de banco de dados para usar uma versão mais recente do SQL Server Express  
  
- Trabalhar com um arquivo de banco de dados no Visual Studio, mas manter a compatibilidade com uma versão mais antiga do SQL Server Express ou LocalDB  
  
- Verifique o SQL Server Express o mecanismo de banco de dados padrão  
  
  Você pode usar o Visual Studio para abrir um projeto que contém um arquivo de banco de dados (. mdf) que foi criado usando uma versão mais antiga do SQL Server Express ou LocalDB. No entanto, para continuar a desenvolver o projeto no Visual Studio, você deve ter essa versão do SQL Server Express ou LocalDB instalada no mesmo computador que o Visual Studio, ou você deve atualizar o arquivo de banco de dados. Se você atualizar o arquivo de banco de dados, você não poderá acessá-lo usando versões mais antigas do SQL Server Express ou LocalDB.  
  
  Você também será solicitado para atualizar um arquivo de banco de dados que foi criado por meio de uma versão anterior do SQL Server Express ou LocalDB se a versão do arquivo não é compatível com a instância do SQL Server Express ou LocalDB instalado no momento. Para resolver o problema, o Visual Studio solicitará que você atualize o arquivo.  
  
> [!IMPORTANT]
>  É recomendável que você faça backup do arquivo de banco de dados antes de você atualizá-lo.  
  
> [!WARNING]
>  Se você atualizar um arquivo. mdf que foi criado no LocalDB 2014 (V12) 32 bits para o LocalDB 2016 (V13), você não poderá abrir o arquivo novamente na versão de 32 bits do LocalDB.  Na atualização 2, LocalDB V13 é de 64 bits apenas.  
  
 Antes de atualizar um banco de dados, considere os seguintes critérios:  
  
-   Não atualize se você quiser trabalhar em seu projeto em uma versão mais antiga e uma versão mais recente do Visual Studio.  
  
-   Não atualize se seu aplicativo será usado em ambientes que usam o SQL Server Express em vez de LocalDB.  
  
-   Não atualize se seu aplicativo usa conexões remotas, porque o LocalDB não aceitá-los.  
  
-   Não atualize se seu aplicativo se baseia em serviços de informações da Internet (IIS).  
  
-   Considere a atualização se você quiser testar os aplicativos de banco de dados em um ambiente de área restrita, mas não quiser administrar um banco de dados.  
  
### <a name="to-upgrade-a-database-file"></a>Para atualizar um arquivo de banco de dados  
  
1. Na **Gerenciador de servidores**, selecione o **conectar-se ao banco de dados** botão.  
  
2. No **Adicionar Conexão** caixa de diálogo, especifique as seguintes informações:  
  
   -   **Fonte de dados**: `Microsoft SQL Server (SqlClient)`  
  
   -   **Nome do servidor**:  
  
       -   Para usar a versão padrão: `(localdb)\MSSQLLocalDB`.  Isso especificará ProjectV12 ou ProjectV13, dependendo de qual versão do Visual Studio está instalado e em que a primeira instância de LocalDB foi criada. O **MSSQLLocalDB** nó no **SQL Server Object Explorer** mostra qual versão ele está apontando.  
  
       -   Para usar uma versão específica: `(localdb)\ProjectsV12` ou `(localdb)\ProjectsV13`, onde V12 é LocalDB 2014, e V13 é LocalDB 2016.  
  
   -   **Anexar um arquivo de banco de dados**: O caminho físico do arquivo. mdf principal.  
  
   -   **Nome lógico**: O nome que você deseja usar com o arquivo.  
  
3. Selecione o botão **OK**.  
  
4. Quando solicitado, selecione a **Sim** botão para atualizar o arquivo.  
  
   O banco de dados é atualizado, é anexado ao mecanismo de banco de dados LocalDB e não é mais compatível com a versão mais antiga do LocalDB.  
  
   Você também pode modificar uma conexão do SQL Server Express para usar o LocalDB, abrindo o menu de atalho para a conexão e, em seguida, selecionando **Modificar Conexão**. No **Modificar Conexão** caixa de diálogo, altere o nome do servidor para `(LocalDB)\MSSQLLocalDB`. No **propriedades avançadas** diálogo caixa, certifique-se de que **instância de usuário** está definido como **False**.  
  
### <a name="to-upgrade-to-a-newer-version-of-sql-server-express"></a>Para atualizar para uma versão mais recente do SQL Server Express  
  
1. No menu de atalho para a conexão ao banco de dados, selecione **Modificar Conexão**.  
  
2. No **Modificar Conexão** caixa de diálogo, selecione o **avançado** botão.  
  
3. No **propriedades avançadas** caixa de diálogo, selecione o **Okey** botão sem alterar o nome do servidor.  
  
   O arquivo de banco de dados é atualizado para corresponder à versão atual do SQL Server Express.  
  
### <a name="to-work-with-the-database-in-visual-studio-but-retain-compatibility-with-sql-server-express"></a>Para trabalhar com o banco de dados no Visual Studio, mas manter a compatibilidade com o SQL Server Express  
  
-   No Visual Studio, abra o projeto sem atualizá-lo.  
  
    -   Para executar o projeto, selecione a tecla F5.  
  
    -   Para editar o banco de dados, abra o arquivo. mdf na **Gerenciador de soluções**e expanda o nó no **Gerenciador de servidores** para trabalhar com seu banco de dados.  
  
### <a name="to-make-sql-server-express-the-default-database-engine"></a>Para tornar o SQL Server Express o mecanismo de banco de dados padrão  
  
1. Na barra de menus, selecione **ferramentas** > **opções**.  
  
2. No **opções** diálogo caixa, expanda o **Data Tools** opções e, em seguida, selecione o **conexões de dados** nó.  
  
3. No **nome da instância do SQL Server** texto, especifique o nome da instância do SQL Server Express ou LocalDB que você deseja usar. Se a instância não for nomeada, especifique `.\SQLEXPRESS or (localdb)\MSSQLLocalDB`.  
  
4. Selecione o botão **OK**.  
  
   SQL Server Express será o mecanismo de banco de dados padrão para seus aplicativos.  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral de dados local](../data-tools/local-data-overview.md)   
 [Passo a passo: conectando a dados em um arquivo de banco de dados local (Windows Forms)](../data-tools/walkthrough-connecting-to-data-in-a-local-database-file-windows-forms.md)

