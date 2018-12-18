---
title: Implementando o código personalizado Check-in políticas de análise de código gerenciado | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.code.analysis.selecttfsrulesets
- vs.code.analysis.browsefortfsruleset
- vs.code.analysis.policyeditor
ms.assetid: fd029003-5671-4b24-8b6f-032e0a98b2e8
caps.latest.revision: 23
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 82f360bb9dc256fd78a8b06aca66d9e49c57ab22
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49268957"
---
# <a name="implementing-custom-code-analysis-check-in-policies-for-managed-code"></a>Implementando políticas de check-in de análise do código personalizadas para código gerenciado
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Uma política de check-in Especifica um conjunto de regras que os membros de um projeto de equipe devem executar no código-fonte antes que ele seja verificado no controle de versão de análise de código. A Microsoft fornece um conjunto de standard *conjuntos de regra* essa análise de código do grupo de regras em áreas funcionais. *Conjuntos de regras de política de check-in personalizado* especificar um conjunto de regras de análise de código que são específicos para um projeto de equipe. Um conjunto de regras é armazenado em um arquivo. RuleSet.  
  
 Políticas de check-in são definidas no nível de projeto de equipe e especificadas pelo local de um arquivo. RuleSet na árvore de controle de versão. Não há nenhuma restrição sobre o local do controle de versão do conjunto de regra personalizada de política de equipe.  
  
 Análise de código é configurada para os projetos de código individuais na janela Propriedades para cada projeto. Uma regra personalizada definida para um projeto de código é especificada pelo local físico do arquivo RuleSet no computador local. Quando um arquivo. RuleSet for especificado, que está localizado na mesma unidade como o projeto de código, o Visual Studio usa um caminho relativo para o arquivo de configuração do projeto.  
  
 É uma prática sugerida para a criação de um conjunto de regras personalizados de projeto de equipe armazenar o arquivo. RuleSet política de check-in em uma pasta especial que não é uma parte de qualquer projeto de código. Se você armazenar o arquivo em uma pasta dedicada, você pode aplicar permissões que restringem quem podem editar o arquivo de regra e você pode mover facilmente a estrutura de diretório que contém o projeto para outro diretório ou computador.  
  
## <a name="creating-the-team-project-custom-check-in-rule-set"></a>Criando o conjunto de regras de Check-in personalizado de projeto de equipe  
 Para criar uma regra personalizada definida para um projeto de equipe, você primeiro crie uma pasta especial para a conjunto de regras de política de check-in **Gerenciador de controle do código-fonte**. Em seguida, crie o arquivo de conjunto de regras e adicionar o arquivo ao controle de versão. Por fim, você pode especificar a conjunto de regras como a código check-in política de análise para o projeto de equipe.  
  
> [!NOTE]
>  Para criar uma pasta em um projeto de equipe, primeiro você deve mapear a raiz do projeto de equipe para um local no computador local. Para obter mais informações, consulte [criar e trabalhar com espaços de trabalho (antigo)](http://msdn.microsoft.com/en-us/db4d5692-179a-44fe-ad31-0c1c900c9cb2).  
  
#### <a name="to-create-the-version-control-folder-for-the-check-in-policy-rule-set"></a>Para criar a pasta de controle de versão para o conjunto de regras de política de check-in  
  
1.  Na [!INCLUDE[esprtfc](../includes/esprtfc-md.md)], expanda o nó do projeto de equipe e, em seguida, clique em **controle de origem**.  
  
2.  No **pastas** painel, o projeto de equipe com o botão direito e, em seguida, clique em **nova pasta**.  
  
3.  No painel de controle do código-fonte principal, clique com botão direito **nova pasta**, clique em **Renomear**e digite um nome para a regra definir pasta.  
  
#### <a name="to-create-the-check-in-policy-rule-set"></a>Para criar o conjunto de regras de política de check-in  
  
1.  Sobre o **arquivo** , aponte para **New**e, em seguida, clique em **arquivo**.  
  
2.  No **categorias** , clique em **geral**.  
  
3.  No **modelos** lista, clique duas vezes em **conjunto de regras de análise de código**.  
  
4.  Especifique as regras a serem incluídas no conjunto de regras e, em seguida, salve o arquivo de conjunto de regras para a pasta de conjunto de regras que você criou.  
  
     Para obter mais informações, consulte [criando conjuntos de regras personalizado](../code-quality/creating-custom-code-analysis-rule-sets.md)  
  
#### <a name="to-add-the-rule-set-file-to-version-control"></a>Para adicionar a regra definir o arquivo de controle de versão  
  
1.  Na **Gerenciador de controle do código-fonte**, clique com botão direito na nova pasta e, em seguida, clique em **adicionar itens à pasta**.  
  
     Para obter mais informações, consulte [usar o controle de versão](http://msdn.microsoft.com/library/33267cee-fe5f-4aa3-b2cd-6d22ceace314).  
  
2.  Clique em que a regra definir o arquivo que você criou e clique **concluir**.  
  
     O arquivo é adicionado ao controle do código-fonte e check-out para você.  
  
3.  No **Gerenciador de controle do código-fonte** janela de detalhes, clique com botão direito no nome do arquivo e, em seguida, clique em **Check-in de alterações pendentes**.  
  
4.  No **Check-in** caixa de diálogo, você tem a opção de adicionar um comentário e, em seguida, clique em **Fazer Check-In**.  
  
    > [!NOTE]
    >  Se você já tiver configurado uma política de check-in do análise código para seu projeto de equipe e você tiver selecionado a **impor check-in contenha somente os arquivos que fazem parte da solução atual**, você irá disparar um aviso de falha de política. Na caixa de diálogo Falha de política, selecione **substituir falha da política e continuar o check-in**. Adicionar um comentário necessário e, em seguida, clique em **Okey**.  
  
#### <a name="to-specify-the-rule-set-file-as-the-check-in-policy"></a>Para especificar a regra definir o arquivo como a política de check-in  
  
1.  Sobre o **Team** , aponte para **configurações de projeto de equipe**e, em seguida, clique em **controle do código-fonte**.  
  
2.  Clique em **política de Check-in**e, em seguida, clique em **Add**.  
  
3.  No **política de Check-in** lista, clique duas vezes em **análise de código**e certifique-se de que o **impor a análise de código para código gerenciado** caixa de seleção está selecionada.  
  
4.  No **executar este conjunto de regras** , clique em  **\<Selecionar conjunto de regras de controle de origem >**.  
  
5.  Digite o caminho do arquivo de conjunto de regras de política de check-in no controle de versão.  
  
     O caminho deve estar de acordo com a seguinte sintaxe:  
  
     **$/** `TeamProjectName` **/** `VersionControlPath`  
  
    > [!NOTE]
    >  Você pode copiar o caminho usando um dos procedimentos a seguir em **Gerenciador de controle do código-fonte**:  
  
    -   No **pastas** painel, clique na pasta que contém o arquivo de conjunto de regras. Copie o caminho da pasta que aparece no controle de versão do **origem** caixa e, em seguida, digite o nome do arquivo de conjunto de regras manualmente.  
  
    -   Na janela de detalhes, clique com botão direito do arquivo de conjunto de regras e, em seguida, clique em **propriedades**. Sobre o **gerais** guia, copie o valor na **nome do servidor**.  
  
## <a name="synchronizing-code-projects-to-the-check-in-policy-rule-set"></a>Sincronizando projetos de código para o conjunto de regras de política de Check-in  
 Você especificar uma regra de política de check-in do projeto de equipe definido como o conjunto de regras de análise de código de uma configuração de projeto de código na caixa de diálogo Propriedades do projeto de código. Se o conjunto de regras estiver localizado na mesma unidade como o projeto de código, um caminho relativo é usado para especificar o conjunto de regras quando o caminho é selecionado na caixa de diálogo de arquivo. Estruturas de controle de caminho relativo que proporciona as configurações de propriedades do projeto para ser portátil para outros computadores que usam a versão local semelhante.  
  
#### <a name="to-specify-a-team-project-rule-set-as-the-rule-set-of-a-code-project"></a>Para especificar uma regra de projeto de equipe definido como o conjunto de regras de um projeto de código  
  
1.  Se necessário, recupere a pasta de conjunto de regra de política de check-in e o arquivo de controle de versão.  
  
     Você pode executar essa etapa na **Gerenciador de controle do código-fonte** clicando com o conjunto de regras de pasta e, em seguida, clicando em **obter última versão**.  
  
2.  Na **Gerenciador de soluções**, clique com botão direito no projeto de código e, em seguida, clique em **propriedades**.  
  
3.  **Clique em análise de código**.  
  
4.  Se necessário, clique nas opções apropriadas na **Configuration** e **plataforma** lista.  
  
5.  Para executar a análise de código sempre que o projeto de código é compilado usando a configuração especificada, selecione a **habilitar análise de código na compilação (define a constante CODE_ANALYSIS)** caixa de seleção.  
  
6.  Para ignorar o código em componentes de outras empresas, selecione a **Suprimir resultados do código gerado** caixa de seleção.  
  
7.  No **executar este conjunto de regras** , clique em  **\<procurar... >**.  
  
8.  Especifique a versão local do arquivo de conjunto de regras de política de check-in.



