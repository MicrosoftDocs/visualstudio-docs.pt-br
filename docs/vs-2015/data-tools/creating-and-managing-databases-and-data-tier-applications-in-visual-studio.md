---
title: Criar e gerenciar bancos de dados e aplicativos da camada de dados no Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- managing change, databases
- database features of Visual Studio, managing change
- databases, managing change
- managing change, database servers
ms.assetid: 40b51f5a-d52c-44ac-8f84-037a0917af33
caps.latest.revision: 40
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 82caaa97e4b6471e3c585fb23c49af00b2ceef0b
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49241612"
---
# <a name="creating-and-managing-databases-and-data-tier-applications-in-visual-studio"></a>Criar e gerenciar bancos de dados e aplicativos da camada de dados no Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
IMPORTANTE]
>  Os projetos de banco de dados que foram incluídos em versões anteriores do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] agora são fornecidos em [!INCLUDE[sql_Denali_long](../includes/sql-denali-long-md.md)] ferramentas. Para obter mais informações, consulte [SQL Server Developer Tools](http://go.microsoft.com/fwlink/?LinkId=228126).  
  
 Você pode usar os projetos de banco de dados para criar novos bancos de dados, novos aplicativos de camada de dados (DACs) e atualizar bancos de dados existentes e aplicativos da camada de dados. Projetos de banco de dados e projetos de DAC permitem aplicar técnicas de gerenciamento de projeto e controle de versão para seus esforços de desenvolvimento de banco de dados da mesma forma que você aplica essas técnicas para código gerenciado ou nativo. Você pode ajudar sua equipe de desenvolvimento a gerenciar as alterações de bancos de dados e servidores de banco de dados com a criação de um *projeto de DAC*, *projeto de banco de dados*, ou uma *projeto do servidor* e colocá-lo sob o controle de versão. Membros de sua equipe podem, em seguida, check-out de arquivos para fazer, compilar e testar as alterações em um *ambiente de desenvolvimento isolado*, ou de área restrita, antes de compartilhá-los com a equipe. Para ajudar a garantir a qualidade do código, sua equipe pode concluir e testar todas as alterações para uma versão específica do banco de dados em um ambiente de preparo antes de implantar as alterações em produção.  
  
 Para obter uma lista dos recursos de banco de dados que são compatíveis com aplicativos da camada de dados, consulte [recursos com suporte em aplicativos de camada de dados](http://go.microsoft.com/fwlink/?LinkId=164239) no site da Microsoft. Se você usar recursos do seu banco de dados que não são compatíveis com aplicativos da camada de dados, você deve usar um projeto de banco de dados para gerenciar as alterações ao banco de dados.  
  
## <a name="common-high-level-tasks"></a>Tarefas comuns de alto nível  
  
|Tarefas de alto nível|Conteúdo de suporte|  
|----------------------|------------------------|  
|**Iniciar o desenvolvimento de um aplicativo da camada de dados:** um DAC é um novo conceito introduzido com [!INCLUDE[sskatmai_r2](../includes/sskatmai-r2-md.md)] que contém a definição para um [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] banco de dados e o suporte a objetos que são usados por um cliente-servidor ou 3 camadas de instância aplicativo. Um DAC inclui objetos de banco de dados, como tabelas e exibições, junto com as entidades de instância, como logons. Você pode usar [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para criar um projeto de DAC, crie um arquivo de pacote DAC e enviar esse arquivo de pacote DAC para um administrador de banco de dados para a implantação em uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mecanismo de banco de dados.|-   [Criando e gerenciando aplicativos da camada de dados](http://go.microsoft.com/fwlink/?LinkId=160741) (Microsoft web site)<br />-   [SQL Server Management Studio](http://go.microsoft.com/fwlink/?LinkId=227328)|  
|**Execução de desenvolvimento iterativo do banco de dados:** se você for um desenvolvedor ou testador, você fazer check-out de partes do projeto e, em seguida, atualizá-los em um ambiente de desenvolvimento isolado. Ao usar esse tipo de ambiente, você pode testar suas alterações sem afetar outros membros da equipe. Depois que as alterações forem concluídas, você verificar os arquivos de volta para o controle de versão, onde outros membros da equipe podem obter as alterações e compilar e implantá-los em um servidor de teste.|-   [Consulta e editores de texto (SQL Server Management Studio)](http://go.microsoft.com/fwlink/?LinkId=227327) (Microsoft web site)<br />-   [Depurador Transact-SQL](http://go.microsoft.com/fwlink/?LinkId=227324) (Microsoft web site)|  
|**Criação de protótipos, verificando resultados de teste e modificar os scripts de banco de dados e objetos:** você pode usar o [!INCLUDE[tsql](../includes/tsql-md.md)] editor para realizar qualquer uma dessas tarefas comuns.|-   [Consulta e editores de texto (SQL Server Management Studio)](http://go.microsoft.com/fwlink/?LinkId=227327) (Microsoft web site)|  
  
## <a name="see-also"></a>Consulte também  
 [Ferramentas de dados do Visual Studio para .NET](../data-tools/visual-studio-data-tools-for-dotnet.md)

