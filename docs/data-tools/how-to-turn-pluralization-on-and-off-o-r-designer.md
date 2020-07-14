---
title: Como habilitar e desabilitar a pluralização (Designer Relacional de Objetos)
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 9b693bc3-303a-40a9-97ee-9cef5ca3ae81
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 6675a136b2bbdc1ef19d90ee19ecf7497053bfe1
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85282040"
---
# <a name="how-to-turn-pluralization-on-and-off-or-designer"></a>Como habilitar e desabilitar a pluralização (Designer Relacional de Objetos)
Por padrão, quando você arrasta objetos de banco de dados que têm nomes que terminam em s ou s de **Gerenciador de servidores** ou **Gerenciador de banco de dados** nas [ferramentas de LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md), os nomes das classes de entidade geradas são alterados de plural para singular. Isso é feito a representa mais precisamente o fato que a classe instanciado de entidade mapeia para um único registro de dados. Por exemplo, a adição de uma `Customers` tabela ao o **/R Designer** resulta em uma classe de entidade chamada `Customer` , pois a classe manterá os dados para apenas um único cliente.

> [!NOTE]
> Pluralization está ativada por padrão somente na versão de língua inglesa do Visual Studio.

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

### <a name="to-turn-pluralization-on-and-off"></a>Para desativar o pluralization e sobre

1. No menu **Ferramentas** , clique em **Opções**.

2. Na caixa de diálogo **Opções**, expanda **Ferramentas de Banco de Dados**.

    > [!NOTE]
    > Selecione **Mostrar todas as configurações** se o nó de **Ferramentas de Banco de Dados** não estiver visível.

3. Clique em **Designer Relacional de Objetos**.

4. Defina **pluralização de nomes** como **habilitado**  =  **false** para definir o o **/R Designer** para que ele não altere os nomes de classe.

5. Defina **pluralização de nomes** como **habilitado**  =  **true** para aplicar as regras de pluralização aos nomes de classe dos objetos adicionados ao o **/R Designer**.

## <a name="see-also"></a>Veja também

- [Ferramentas do LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index)
- [Acessando dados no Visual Studio](../data-tools/accessing-data-in-visual-studio.md)
