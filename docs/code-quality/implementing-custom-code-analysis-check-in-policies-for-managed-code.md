---
title: Políticas de check-in de análise de código personalizado para código gerenciado
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.code.analysis.selecttfsrulesets
- vs.code.analysis.browsefortfsruleset
- vs.code.analysis.policyeditor
ms.assetid: fd029003-5671-4b24-8b6f-032e0a98b2e8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: b9eec66ec24c30b6e0df835d16805ea00eb08ac2
ms.sourcegitcommit: 48e93538f1e352fc1f972b642bb5fcce2f6834a2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85371762"
---
# <a name="implement-custom-code-analysis-check-in-policies-for-managed-code"></a>Implementar políticas de check-in de análise de código personalizadas para código gerenciado

Uma política de check-in de análise de código especifica um conjunto de regras que os membros de um projeto DevOps do Azure devem executar no código-fonte antes de fazer check-in no controle de versão. A Microsoft fornece um conjunto de *conjuntos de regras* padrão que agrupam regras de análise de código em áreas funcionais. Os *conjuntos de regras de política de check-in personalizados* especificam um conjunto de regras de análise de código que são específicas a um projeto. Um conjunto de regras é armazenado em um arquivo. RuleSet.

As políticas de check-in são definidas no nível do projeto DevOps do Azure e especificadas pelo local de um arquivo. RuleSet na árvore de controle de versão. Não há restrições no local de controle de versão do conjunto de regras personalizadas da política de equipe.

A análise de código é configurada para os projetos de código individuais na janela Propriedades de cada projeto. Um conjunto de regras personalizadas para um projeto de código é especificado pelo local físico do arquivo. RuleSet no computador local. Quando um arquivo. RuleSet é especificado que está localizado na mesma unidade que o projeto de código, o Visual Studio usa um caminho relativo para o arquivo na configuração do projeto.

Uma prática sugerida para criar um conjunto de regras personalizadas do projeto DevOps do Azure é armazenar o arquivo. RuleSet da diretiva de check-in em uma pasta especial que não faz parte de nenhum projeto de código. Se você armazenar o arquivo em uma pasta dedicada, poderá aplicar permissões que restringem quem pode editar o arquivo de regra, e você pode mover facilmente a estrutura do diretório que contém o projeto para outro diretório ou computador.

## <a name="create-the-project-custom-check-in-rule-set"></a>Criar o conjunto de regras de check-in personalizado do projeto

Para criar um conjunto de regras personalizado para um projeto DevOps do Azure, primeiro crie uma pasta especial para o conjunto de regras de política de check-in no **Source Control Explorer**. Em seguida, você cria o arquivo de conjunto de regras e adiciona o arquivo ao controle de versão. Por fim, você especifica o conjunto de regras como a política de check-in de análise de código para o projeto.

> [!NOTE]
> Para criar uma pasta em um projeto DevOps do Azure, primeiro você deve mapear a raiz do projeto para um local no computador local.

### <a name="to-create-the-version-control-folder-for-the-check-in-policy-rule-set"></a>Para criar a pasta de controle de versão para o conjunto de regras de política de check-in

1. Em Team Explorer, expanda o nó do projeto e clique em **controle do código-fonte**.

2. No painel **pastas** , clique com o botão direito do mouse no projeto e clique em **nova pasta**.

3. No painel principal de controle do código-fonte, clique com o botão direito do mouse em **nova pasta**, clique em **renomear**e digite um nome para a pasta do conjunto de regras.

### <a name="to-create-the-check-in-policy-rule-set"></a>Para criar o conjunto de regras de política de check-in

1. No menu **Arquivo** , aponte para **Novo**e clique em **Arquivo**.

2. Na lista **categorias** , clique em **geral**.

3. Na lista **modelos** , clique duas vezes em **conjunto de regras de análise de código**.

4. [Especifique as regras](../code-quality/how-to-create-a-custom-rule-set.md) a serem incluídas no conjunto de regras e salve o arquivo de conjunto de regras na pasta do conjunto de regras que você criou.

### <a name="to-add-the-rule-set-file-to-version-control"></a>Para adicionar o arquivo do conjunto de regras ao controle de versão

1. Em **Source Control Explorer**, clique com o botão direito do mouse na nova pasta e clique em **Adicionar itens à pasta**.

     Para obter mais informações, consulte [git e Azure Repos](/azure/devops/repos/git/overview?view=vsts).

2. Clique no arquivo de conjunto de regras que você criou e clique em **concluir**.

     O arquivo é adicionado ao controle do código-fonte e com check-out para você.

3. Na janela detalhes do **Source Control Explorer** , clique com o botão direito do mouse no nome do arquivo e clique em **fazer check-in de alterações pendentes**.

4. Na caixa de diálogo de **check-in** , você tem a opção de adicionar um comentário e, em seguida, clique em **check-in**.

    > [!NOTE]
    > Se você já tiver configurado uma política de check-in de análise de código para seu projeto DevOps do Azure e tiver selecionado o **check-in de imposição para conter apenas os arquivos que fazem parte da solução atual**, você disparará um aviso de falha de política. Na caixa de diálogo falha de política, selecione **Substituir falha da política e continuar check-in**. Adicione um comentário necessário e clique em **OK**.

### <a name="to-specify-the-rule-set-file-as-the-check-in-policy"></a>Para especificar o arquivo de conjunto de regras como a política de check-in

1. No menu **equipe** , aponte para **configurações do projeto**e clique em **controle do código-fonte**.

2. Clique em **política de check-in**e, em seguida, clique em **Adicionar**.

3. Na lista **política de check-in** , clique duas vezes em **análise de código**e verifique se a caixa de seleção **impor análise de código para código gerenciado** está marcada.

4. Na lista **executar este conjunto de regras** , clique em **\<Select Rule Set from Source Control>** .

5. Digite o caminho do arquivo de conjunto de regras de política de check-in no controle de versão.

     O caminho deve estar de acordo com a seguinte sintaxe:

     **$/** `TeamProjectName` **/** `VersionControlPath`

    > [!NOTE]
    > Você pode copiar o caminho usando um dos seguintes procedimentos no **Source Control Explorer**:

    - No painel **pastas** , clique na pasta que contém o arquivo de conjunto de regras. Copie o caminho de controle de versão da pasta que aparece na caixa **origem** e digite o nome do arquivo de conjunto de regras manualmente.

    - Na janela de detalhes, clique com o botão direito do mouse no arquivo do conjunto de regras e clique em **Propriedades**. Na guia **geral** , copie o valor em **nome do servidor**.

## <a name="synchronize-code-projects-to-the-check-in-policy-rule-set"></a>Sincronizar projetos de código com o conjunto de regras de política de check-in

Você especifica uma regra de política de check-in de projeto definida como o conjunto de regras de análise de código de uma configuração de projeto de código na caixa de diálogo Propriedades do projeto de código. Se o conjunto de regras estiver localizado na mesma unidade que o projeto de código, um caminho relativo será usado para especificar o conjunto de regras quando o caminho for selecionado na caixa de diálogo arquivo. O caminho relativo permite que as configurações de propriedades do projeto sejam portáveis para outros computadores que usam estruturas de controle de versão locais semelhantes.

### <a name="to-specify-a-project-rule-set-as-the-rule-set-of-a-code-project"></a>Para especificar um conjunto de regras de projeto como o conjunto de regras de um projeto de código

1. Se necessário, recupere a pasta e o arquivo do conjunto de regras de diretiva de check-in do controle de versão.

   Você pode executar essa etapa no **Source Control Explorer** clicando com o botão direito do mouse na pasta conjunto de regras e clicando em **obter versão mais recente**.

2. Em **Gerenciador de soluções**, clique com o botão direito do mouse no projeto de código e clique em **Propriedades**.

3. **Clique em análise de código**.

4. Se necessário, clique nas opções apropriadas nas listas de **configuração** e **plataforma** .

::: moniker range="vs-2017"

5. Para executar a análise de código toda vez que o projeto de código for criado usando a configuração especificada, selecione **Habilitar análise de código na compilação**.

::: moniker-end

::: moniker range=">=vs-2019"

5. Para executar a análise de código toda vez que o projeto de código for criado usando a configuração especificada, selecione **executar na compilação** na seção **analisadores binários** .

::: moniker-end

6. Na lista **executar este conjunto de regras** , clique em **\<Browse>** .

8. Selecione a versão local do arquivo de conjunto de regras de política de check-in.
