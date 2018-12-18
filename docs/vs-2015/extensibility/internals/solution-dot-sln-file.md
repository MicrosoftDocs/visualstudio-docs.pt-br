---
title: Solução (. Arquivos sln) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- sln files, VSPackages
- solutions, .sln files
- .sln files, VSPackages
ms.assetid: 7d7ef539-2e4b-4637-b853-8ec7626609df
caps.latest.revision: 14
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: bc61824e7df36fa3b615d1a2c4b729cd7b7c8c1c
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51796175"
---
# <a name="solution-sln-file"></a>Arquivo de solução (.Sln)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Uma solução é uma estrutura para organizar projetos no Visual Studio. A solução mantém as informações de estado para projetos em. sln (baseado em texto, compartilhado) e arquivos. suo (opções de solução de binário, especificada pelo usuário). Para obter mais informações sobre arquivos. suo, consulte [opções de usuário da solução (. Arquivo suo)](../../extensibility/internals/solution-user-options-dot-suo-file.md).  
  
 Se o VSPackage é carregado como resultado de que está sendo referenciado no arquivo. sln, o ambiente chama <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.ReadSolutionProps%2A> para ler no arquivo. sln.  
  
 O arquivo. sln contém informações baseadas em texto, que o ambiente usa para localizar e carregar os parâmetros de nome-valor para os dados persistentes e o projeto VSPackages faz referência a ele. Quando um usuário abre uma solução, o ambiente percorre os `preSolution`, `Project`, e `postSolution` informações no arquivo. sln para carregar a solução, projetos dentro da solução, e todas as informações persistentes anexado à solução.  
  
 Arquivo de cada projeto contém informações adicionais de leitura pelo ambiente para preencher a hierarquia com itens do projeto. A persistência de dados de hierarquia é controlada pelo projeto; os dados não são normalmente armazenados no arquivo. sln, embora você possa escrever intencionalmente informações do projeto para o arquivo se você optar por fazê-lo. Para obter mais informações relacionadas à persistência, consulte [persistência do projeto](../../extensibility/internals/project-persistence.md) e [abrindo e salvando itens de projeto](../../extensibility/internals/opening-and-saving-project-items.md).  
  
## <a name="solution-file-contents"></a>Conteúdo do arquivo de solução  
 O arquivo. sln consiste em várias seções conforme ilustrado no código a seguir.  
  
```  
Project("{F184B08F-C81C-45F6-A57F-5ABD9991F28F}") = "Project1", "Project1.vbproj", "{8CDD8387-B905-44A8-B5D5-07BB50E05BEA}"  
EndProject  
Global  
  GlobalSection(SolutionNotes) = postSolution  
  EndGlobalSection  
  GlobalSection(SolutionConfiguration) = preSolution  
       ConfigName.0 = Debug  
       ConfigName.1 = Release  
  EndGlobalSection  
  GlobalSection(ProjectDependencies) = postSolution  
  EndGlobalSection  
  GlobalSection(ProjectConfiguration) = postSolution  
   {8CDD8387-B905-44A8-B5D5-07BB50E05BEA}.Debug.ActiveCfg = Debug|x86  
   {8CDD8387-B905-44A8-B5D5-07BB50E05BEA}.Debug.Build.0 = Debug|x86  
   {8CDD8387-B905-44A8-B5D5-07BB50E05BEA}.Release.ActiveCfg = Release|x86  
   {8CDD8387-B905-44A8-B5D5-07BB50E05BEA}.Release.Build.0 = Release|x86  
  EndGlobalSection  
  GlobalSection(ExtensibilityGlobals) = postSolution  
  EndGlobalSection  
  GlobalSection(ExtensibilityAddIns) = postSolution  
  EndGlobalSection  
EndGlobal  
```  
  
 Para carregar uma solução, o ambiente executa a seguinte sequência de tarefas.  
  
1. O ambiente lê a seção Global do arquivo. sln e processa todas as seções marcadas `preSolution`. Nesse caso, há um tal declaração:  
  
   ```  
   GlobalSection(SolutionConfiguration) = preSolution  
        ConfigName.0 = Debug  
        ConfigName.1 = Release  
   ```  
  
    Quando o ambiente de ler o `GlobalSection('name')` marca, ele mapeia o nome de um VSPackage usando o registro. O nome da chave deve existir no registro em [HKLM\\< raiz do registro de ID de aplicativo\>\SolutionPersistence\AggregateGUIDs]. Valor de padrão das chaves é o GUID de pacote (REG_SZ) do VSPackage que escreveu as entradas.  
  
2. O ambiente carrega o VSPackage, chamadas `QueryInterface` sobre o VSPackage para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps> interface e chama o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.ReadSolutionProps%2A> método com os dados na seção para que o VSPackage pode armazenar os dados. O ambiente repete esse processo para cada `preSolution` seção.  
  
3. O ambiente itera através dos blocos de persistência do projeto. Nesse caso, há um projeto.  
  
   ```  
   Project("{F184B08F-C81C-45F6-A57F-5ABD9991F28F}") = "Project1",  
   "Project1.vbproj", "{8CDD8387-B905-44A8-B5D5-07BB50E05BEA}"  
   EndProject  
   ```  
  
    Esta declaração contém o GUID exclusivo do projeto e o GUID do tipo de projeto. Essas informações são usadas pelo ambiente para localizar o arquivo de projeto ou arquivos que pertencem à solução e o VSPackage necessários para cada projeto. O projeto de GUID é passado para <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory> para carregar o VSPackage específico relacionado ao projeto, em seguida, o projeto é carregado pelo VSPackage. Nesse caso, o que é carregado para esse projeto VSPackage é Visual Basic.  
  
    Cada projeto pode manter uma ID de instância exclusivo do projeto para que possa ser acessado conforme a necessidade por outros projetos na solução. O ideal é que, se a solução e projetos estão sob controle do código-fonte, o caminho para o projeto deve ser relativo ao caminho para a solução. Quando a solução é carregada pela primeira vez, os arquivos de projeto não podem ser no computador do usuário. Fazendo com que o arquivo de projeto armazenado no servidor em relação ao arquivo de solução, é relativamente simple para o arquivo de projeto a ser encontrado e copiados para o computador do usuário. Em seguida, ele copia e carrega o restante dos arquivos necessários para o projeto.  
  
4. O ambiente com base nas informações contidas na seção de projeto do arquivo. sln, carrega cada arquivo de projeto. O projeto em si, em seguida, é responsável por popular da hierarquia do projeto e carregar todos os projetos aninhados.  
  
5. Após o processamento de todas as seções do arquivo. sln, a solução é exibida no Gerenciador de soluções e está pronta para modificação pelo usuário.  
  
   Se qualquer VSPackage que implementa um projeto na solução Falha ao carregar, o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.OnProjectLoadFailure%2A> método é chamado e todos os outros projetos na solução recebe uma oportunidade para ignorar as alterações que ele pode ter feito durante o carregamento. Se ocorrerem erros de análise, o máximo possível de informações são preservadas com os arquivos de solução e o ambiente exibe uma caixa de diálogo avisa ao usuário que a solução está corrompida.  
  
   Quando a solução é salvo ou fechada, o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.QuerySaveSolutionProps%2A> método é chamado e passado para a hierarquia para ver se as alterações foram feitas para a solução que precisam ser inseridos no arquivo. sln. Um valor nulo, passado para `QuerySaveSolutionProps` em <xref:Microsoft.VisualStudio.Shell.Interop.VSQUERYSAVESLNPROPS>, indica que informações estão sendo persistente para a solução. Se o valor não for nulo, as informações persistentes serão para um projeto específico, determinado pelo ponteiro para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> interface.  
  
   Se não houver informações a serem salvas, o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence> interface é chamado com um ponteiro para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.SaveSolutionProps%2A> método. O <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.WriteSolutionProps%2A> método é chamado pelo ambiente para recuperar os pares nome-valor de `IPropertyBag` de interface e gravar as informações no arquivo. sln.  
  
   `SaveSolutionProps` e `WriteSolutionProps` objetos são chamados recursivamente pelo ambiente de recuperar as informações a ser gravado do `IPropertyBag` interface até que todas as alterações tenham sido inseridas no arquivo. sln. Dessa forma, você pode garantir que as informações serão mantidas com a solução e o tempo disponível do próximo que a solução for aberta.  
  
   Cada VSPackage carregado é enumerado para ver se ela tiver algo para salvar em arquivo. sln. Ele é apenas no tempo de carregamento que as chaves do registro são consultadas. O ambiente conhece todos os pacotes carregados porque eles estão na memória no momento em que a solução é salvo.  
  
   Somente o arquivo. sln contém entradas na `preSolution` e `postSolution` seções. Não existem seções semelhantes no arquivo. suo, pois a solução precisa dessas informações para carregar corretamente. O arquivo. suo contém opções específicas do usuário, como anotações privadas, que não se destina a ser compartilhado ou colocado sob controle do código-fonte.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps>   
 [Opções de usuário da solução (. Arquivo suo)](../../extensibility/internals/solution-user-options-dot-suo-file.md)   
 [Soluções](../../extensibility/internals/solutions.md)

