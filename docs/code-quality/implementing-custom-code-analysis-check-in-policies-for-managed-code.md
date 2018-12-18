---
title: Implementando políticas de check-in de análise do código personalizadas para código gerenciado
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- vs.code.analysis.selecttfsrulesets
- vs.code.analysis.browsefortfsruleset
- vs.code.analysis.policyeditor
ms.assetid: fd029003-5671-4b24-8b6f-032e0a98b2e8
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: 4c39ef2c70108eabb3c3d87dc7ab5af17dccd9f8
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53049852"
---
# <a name="implement-custom-code-analysis-check-in-policies-for-managed-code"></a>Implementar políticas de check-in de análise de código personalizadas para código gerenciado

Uma política de check-in do análise código especifica um conjunto de regras que os membros de um projeto de DevOps do Azure devem ser executado no código-fonte antes que ele seja verificado no controle de versão. A Microsoft fornece um conjunto de standard *conjuntos de regra* essa análise de código do grupo de regras em áreas funcionais. *Conjuntos de regras de política de check-in personalizado* especificar um conjunto de regras de análise de código que são específicas a um projeto. Um conjunto de regras é armazenado em um arquivo. RuleSet.

Políticas de check-in são definidas no nível do projeto de DevOps do Azure e são especificadas pelo local de um arquivo. RuleSet na árvore de controle de versão. Não há nenhuma restrição sobre o local do controle de versão do conjunto de regra personalizada de política de equipe.

Análise de código é configurada para os projetos de código individuais na janela Propriedades para cada projeto. Uma regra personalizada definida para um projeto de código é especificada pelo local físico do arquivo RuleSet no computador local. Quando um arquivo. RuleSet for especificado, que está localizado na mesma unidade como o projeto de código, o Visual Studio usa um caminho relativo para o arquivo de configuração do projeto.

Uma prática sugerida para a criação de um DevOps do Azure é de conjunto de regras personalizado de projeto para armazenar o arquivo. RuleSet política de check-in em uma pasta especial que não é uma parte de qualquer projeto de código. Se você armazenar o arquivo em uma pasta dedicada, você pode aplicar permissões que restringem quem podem editar o arquivo de regra e você pode mover facilmente a estrutura de diretório que contém o projeto para outro diretório ou computador.

## <a name="create-the-project-custom-check-in-rule-set"></a>Criar o conjunto de regras de Check-in personalizado de projeto

Para criar uma regra personalizada definida para um projeto de DevOps do Azure, primeiro crie uma pasta especial para a conjunto de regras de política de check-in **Gerenciador de controle do código-fonte**. Em seguida, crie o arquivo de conjunto de regras e adicionar o arquivo ao controle de versão. Por fim, você pode especificar a conjunto de regras como a código check-in política de análise para o projeto.

> [!NOTE]
> Para criar uma pasta em um projeto de DevOps do Azure, primeiro você deve mapear a raiz do projeto para um local no computador local.

### <a name="to-create-the-version-control-folder-for-the-check-in-policy-rule-set"></a>Para criar a pasta de controle de versão para o conjunto de regras de política de check-in

1. No Team Explorer, expanda o nó do projeto e, em seguida, clique em **controle de origem**.

2. No **pastas** painel, clique com botão direito no projeto e, em seguida, clique em **nova pasta**.

3. No painel de controle do código-fonte principal, clique com botão direito **nova pasta**, clique em **Renomear**e digite um nome para a regra definir pasta.

### <a name="to-create-the-check-in-policy-rule-set"></a>Para criar o conjunto de regras de política de check-in

1. Sobre o **arquivo** , aponte para **New**e, em seguida, clique em **arquivo**.

2. No **categorias** , clique em **geral**.

3. No **modelos** lista, clique duas vezes em **conjunto de regras de análise de código**.

4. [Especifique as regras](../code-quality/how-to-create-a-custom-rule-set.md) para incluir no conjunto de regras e, em seguida, salvar a regra definir o arquivo para a pasta de conjunto de regras que você criou.

### <a name="to-add-the-rule-set-file-to-version-control"></a>Para adicionar a regra definir o arquivo de controle de versão

1. Na **Gerenciador de controle do código-fonte**, clique com botão direito na nova pasta e, em seguida, clique em **adicionar itens à pasta**.

     Para obter mais informações, consulte [Git e repositórios Azure](/azure/devops/repos/git/overview?view=vsts).

2. Clique em que a regra definir o arquivo que você criou e clique **concluir**.

     O arquivo é adicionado ao controle do código-fonte e check-out para você.

3. No **Gerenciador de controle do código-fonte** janela de detalhes, clique com botão direito no nome do arquivo e, em seguida, clique em **Check-in de alterações pendentes**.

4. No **Check-in** caixa de diálogo, você tem a opção de adicionar um comentário e, em seguida, clique em **Fazer Check-In**.

    > [!NOTE]
    > Se você já tiver configurado uma política de check-in do análise código para seu projeto de DevOps do Azure e você tiver selecionado a **impor check-in contenha somente os arquivos que fazem parte da solução atual**, você irá disparar um aviso de falha de política. Na caixa de diálogo Falha de política, selecione **substituir falha da política e continuar o check-in**. Adicionar um comentário necessário e, em seguida, clique em **Okey**.

### <a name="to-specify-the-rule-set-file-as-the-check-in-policy"></a>Para especificar a regra definir o arquivo como a política de check-in

1. Sobre o **Team** , aponte para **configurações do projeto**e, em seguida, clique em **controle do código-fonte**.

2. Clique em **política de Check-in**e, em seguida, clique em **Add**.

3. No **política de Check-in** lista, clique duas vezes em **análise de código**e certifique-se de que o **impor a análise de código para código gerenciado** caixa de seleção está selecionada.

4. No **executar este conjunto de regras** , clique em  **\<Selecionar conjunto de regras de controle de origem >**.

5. Digite o caminho do arquivo de conjunto de regras de política de check-in no controle de versão.

     O caminho deve estar de acordo com a seguinte sintaxe:

     **$/** `TeamProjectName` **/** `VersionControlPath`

    > [!NOTE]
    > Você pode copiar o caminho usando um dos procedimentos a seguir em **Gerenciador de controle do código-fonte**:

    - No **pastas** painel, clique na pasta que contém o arquivo de conjunto de regras. Copie o caminho da pasta que aparece no controle de versão do **origem** caixa e, em seguida, digite o nome do arquivo de conjunto de regras manualmente.

    - Na janela de detalhes, clique com botão direito do arquivo de conjunto de regras e, em seguida, clique em **propriedades**. Sobre o **gerais** guia, copie o valor na **nome do servidor**.

## <a name="synchronize-code-projects-to-the-check-in-policy-rule-set"></a>Sincronizar os projetos de código para o conjunto de regras de política de Check-in

Você especificar uma regra de política de check-in do projeto definir como o conjunto de regras de análise de código de uma configuração de projeto de código na caixa de diálogo Propriedades do projeto de código. Se o conjunto de regras estiver localizado na mesma unidade como o projeto de código, um caminho relativo é usado para especificar o conjunto de regras quando o caminho é selecionado na caixa de diálogo de arquivo. Estruturas de controle de caminho relativo que proporciona as configurações de propriedades do projeto para ser portátil para outros computadores que usam a versão local semelhante.

### <a name="to-specify-a-project-rule-set-as-the-rule-set-of-a-code-project"></a>Para especificar uma regra de projeto definir como o conjunto de regras de um projeto de código

1. Se necessário, recupere a pasta de conjunto de regra de política de check-in e o arquivo de controle de versão.

   Você pode executar essa etapa na **Gerenciador de controle do código-fonte** clicando com o conjunto de regras de pasta e, em seguida, clicando em **obter última versão**.

2. Na **Gerenciador de soluções**, clique com botão direito no projeto de código e, em seguida, clique em **propriedades**.

3. **Clique em análise de código**.

4. Se necessário, clique nas opções apropriadas na **Configuration** e **plataforma** lista.

5. Para executar a análise de código sempre que o projeto de código é compilado usando a configuração especificada, selecione a **habilitar análise de código na compilação (define a constante CODE_ANALYSIS)** caixa de seleção.

6. Para ignorar o código em componentes de outras empresas, selecione a **Suprimir resultados do código gerado** caixa de seleção.

7. No **executar este conjunto de regras** , clique em  **\<procurar... >**.

8. Especifique a versão local do arquivo de conjunto de regras de política de check-in.