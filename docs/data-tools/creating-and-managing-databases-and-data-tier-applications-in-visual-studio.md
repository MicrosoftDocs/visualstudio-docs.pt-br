---
title: Projetos de banco de dados e projetos de DAC
ms.date: 11/21/2018
ms.topic: conceptual
helpviewer_keywords:
- databases, managing change
ms.assetid: 40b51f5a-d52c-44ac-8f84-037a0917af33
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: d8671c46cf2e88ab5d5797dd7a009ff29b953c4e
ms.sourcegitcommit: c9a01c599ce19a5845605b3b28c0229fd0abb93f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2018
ms.locfileid: "52281726"
---
# <a name="database-projects-and-data-tier-applications"></a>Projetos de banco de dados e aplicativos da camada de dados

Você pode usar os projetos de banco de dados para criar novos bancos de dados, novos aplicativos de camada de dados (DACs) e atualizar bancos de dados existentes e aplicativos da camada de dados. Projetos de banco de dados e projetos de DAC permitem aplicar técnicas de gerenciamento de projeto e controle de versão para seus esforços de desenvolvimento de banco de dados da mesma forma que você aplica essas técnicas para código gerenciado ou nativo. Você pode ajudar sua equipe de desenvolvimento gerenciar alterações em bancos de dados e servidores de banco de dados criando um projeto de DAC, o projeto de banco de dados ou um projeto do servidor e colocá-lo sob controle de versão. Membros de sua equipe podem, em seguida, check-out de arquivos para fazer, compilar e testar as alterações em um ambiente de desenvolvimento isolado ou área restrita, antes de compartilhá-los com a equipe. Para ajudar a garantir a qualidade do código, sua equipe pode concluir e testar todas as alterações para uma versão específica do banco de dados em um ambiente de preparo antes de implantar as alterações em produção.

Para obter uma lista dos recursos de banco de dados que são compatíveis com aplicativos da camada de dados, consulte [suporte de DAC para objetos do SQL Server](/sql/relational-databases/data-tier-applications/dac-support-for-sql-server-objects-and-versions). Se você usar recursos do seu banco de dados que não são compatíveis com aplicativos da camada de dados, você deve usar um projeto de banco de dados para gerenciar as alterações ao banco de dados.

## <a name="common-high-level-tasks"></a>Tarefas comuns de alto nível

| Tarefas de alto nível | Conteúdo de suporte |
| - | - |
| **Iniciar o desenvolvimento de um aplicativo da camada de dados:** o conceito de um aplicativo da camada de dados (DAC) foi introduzido com o SQL Server 2008. Um DAC contém a definição de um banco de dados do SQL Server e os objetos de instância de suporte que são usados por um aplicativo de 3 camadas ou cliente-servidor. Um DAC inclui objetos de banco de dados, como tabelas e exibições, junto com as entidades de instância, como logons. Você pode usar o Visual Studio para criar um projeto de DAC, crie um arquivo de pacote DAC e envie o arquivo de pacote DAC para um administrador de banco de dados para a implantação em uma instância do mecanismo de banco de dados do SQL Server. | - [Aplicativos da camada de dados](/sql/relational-databases/data-tier-applications/data-tier-applications)<br />- [SQL Server Management Studio](/sql/ssms/sql-server-management-studio-ssms) |
| **Execução de desenvolvimento iterativo do banco de dados:** os desenvolvedores podem fazer check-out de partes do projeto e atualizá-los em um ambiente de desenvolvimento isolado. Ao usar esse tipo de ambiente, você pode testar suas alterações sem afetar outros membros da equipe. Depois que as alterações forem concluídas, você verificar os arquivos de volta para o controle de versão, onde outros membros da equipe podem obter as alterações e compilar e implantá-los em um servidor de teste. | - [Desenvolvimento de banco de dados offline orientado a projetos (SQL Server Data Tools)](/sql/ssdt/project-oriented-offline-database-development)<br />- [Depurador Transact-SQL (SQL Server Management Studio)](/sql/ssms/scripting/transact-sql-debugger) |
| **Criação de protótipos, verificando resultados de teste e modificar os scripts de banco de dados e objetos:** você pode usar o editor Transact-SQL para executar qualquer uma dessas tarefas comuns. | - [Editores de consulta e texto (SQL Server Management Studio)](/sql/ssms/scripting/query-and-text-editors-sql-server-management-studio) |

## <a name="see-also"></a>Consulte também

- [Ferramentas de dados do Visual Studio para .NET](../data-tools/visual-studio-data-tools-for-dotnet.md)