---
title: Como excluir projetos de um build
ms.date: 11/04/2016
ms.technology: vs-ide-compile
ms.topic: how-to
ms.assetid: 17a837ca-5db9-46cd-b5a7-b14ad1d2c47d
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c30dd912378fd933d29bff1d8828f31de58f9afa
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85284315"
---
# <a name="how-to-exclude-projects-from-a-build"></a>Como excluir projetos de um build

É possível compilar uma solução sem compilar todos os projetos que ela contém. Por exemplo, é possível excluir um projeto que interrompe o build. É possível compilar o projeto depois de investigar e resolver os problemas.

É possível excluir um projeto adotando as seguintes abordagens:

- Removê-lo temporariamente da configuração da solução ativa.

- Criando uma configuração de solução que não inclui o projeto.

Para obter mais informações, consulte [Compreender configurações de build](../ide/understanding-build-configurations.md).

## <a name="to-temporarily-remove-a-project-from-the-active-solution-configuration"></a>Para remover temporariamente um projeto da configuração da solução ativa

1. Na barra de menus, escolha **criar**  >  **Configuration Manager**.

2. Na tabela **Contextos do projeto**, localize o projeto que você deseja excluir do build.

3. Na coluna **Build** do projeto, desmarque a caixa de seleção.

4. Escolha o botão **Fechar** e, em seguida, recompile a solução.

## <a name="to-create-a-solution-configuration-that-excludes-a-project"></a>Para criar uma configuração da solução que exclui um projeto

1. Na barra de menus, escolha **criar**  >  **Configuration Manager**.

2. Na lista **configuração de solução ativa** , escolha **\<New>** .

3. Na caixa **Nome**, insira um nome para a configuração da solução.

4. Na lista **Copiar configurações de**, escolha a configuração da solução na qual você deseja basear a nova configuração (por exemplo, **Depurar**) e, em seguida, escolha o botão **OK**.

5. Na caixa de diálogo **Configuration Manager**, desmarque a caixa de seleção na coluna **Build** do projeto que você deseja excluir e, em seguida, escolha o botão **Fechar**.

6. Na barra de ferramentas **Padrão**, verifique se a nova configuração da solução é a configuração ativa na caixa **Configurações da Solução**.

7. Na barra de menus, escolha **Compilar**  >  **Recompilar solução**.

## <a name="skipped-projects"></a>Projetos ignorados

Os projetos podem ser ignorados durante a compilação porque eles não estão atualizados ou porque são excluídos da configuração. O Visual Studio usa o MSBuild para compilar seus projetos. O MSBuild cria um destino somente se a saída for mais antiga que a entrada, conforme determinado pelos carimbos de data/hora do arquivo. Para forçar uma recompilação, use a **Build**  >  **solução de recompilação**de compilação de comando.

No painel **Build** da janela de **saída** , o Visual Studio relata o número de projetos que estavam atualizados, o número que foi criado com êxito, o número que falhou e o número que foram ignorados. A contagem ignorada não inclui projetos que não foram criados porque estavam atualizados. Quando os projetos são excluídos da configuração ativa, eles são ignorados durante a compilação. Na saída da compilação, você verá uma mensagem indicando que o projeto foi ignorado:

```output
2>------ Skipped Build: Project: ConsoleApp2, Configuration: Debug x86 ------
2>Project not selected to build for this solution configuration
```

Para descobrir por que um projeto foi ignorado, observe a configuração ativa ( `Debug x86` no exemplo anterior) e escolha **criar**  >  **Configuration Manager**. Você pode exibir ou alterar quais projetos são ignorados para cada configuração, conforme discutido neste artigo.

## <a name="see-also"></a>Veja também

- [Noções sobre configurações de build](../ide/understanding-build-configurations.md)
- [Como criar e editar configurações](../ide/how-to-create-and-edit-configurations.md)
- [Como: Compilar várias configurações simultaneamente](../ide/how-to-build-multiple-configurations-simultaneously.md)
