---
title: Solução (. Sln) arquivo
description: Saiba mais sobre o arquivo. sln, que é um dos arquivos que mantém informações de estado de um projeto no Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 03/15/2019
ms.topic: conceptual
helpviewer_keywords:
- sln files, VSPackages
- solutions, .sln files
- .sln files, VSPackages
ms.assetid: 7d7ef539-2e4b-4637-b853-8ec7626609df
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 27364382a7e4318fce822b148e9d3df6747bfd1e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105081991"
---
# <a name="solution-sln-file"></a>Arquivo de solução (. sln)

Uma solução é uma estrutura para organizar projetos no Visual Studio. A solução mantém as informações de estado dos projetos em dois arquivos:

- arquivo. sln (baseado em texto, compartilhado)

- arquivo. suo (opções de solução binárias específicas do usuário)

Para obter mais informações sobre arquivos. suo, consulte [Opções de usuário da solução (. Suo)](../../extensibility/internals/solution-user-options-dot-suo-file.md).

Se seu VSPackage for carregado como resultado de ser referenciado no arquivo. sln, o ambiente chamará <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.ReadSolutionProps%2A> para ler no arquivo. sln.

O arquivo. sln contém informações baseadas em texto que o ambiente usa para localizar e carregar os parâmetros de valor de nome para os dados persistentes e o projeto VSPackages que faz referência a ele. Quando um usuário abre uma solução, o ambiente percorre as `preSolution` informações, `Project` e `postSolution` no arquivo. sln para carregar a solução, os projetos dentro da solução e todas as informações persistentes anexadas à solução.

Cada arquivo do projeto contém informações adicionais lidas pelo ambiente para popular a hierarquia com os itens desse projeto. A persistência de dados de hierarquia é controlada pelo projeto. Os dados normalmente não são armazenados no arquivo. sln, embora seja possível gravar intencionalmente as informações do projeto no arquivo. sln se você optar por fazer isso. Para obter mais informações sobre persistência, consulte [persistência do projeto](../../extensibility/internals/project-persistence.md) e [abrindo e salvando itens de projeto](../../extensibility/internals/opening-and-saving-project-items.md).

## <a name="file-header"></a>Cabeçalho do arquivo

O cabeçalho de um arquivo. sln é semelhante a este:

::: moniker range="vs-2017"

```
Microsoft Visual Studio Solution File, Format Version 12.00
# Visual Studio 15
VisualStudioVersion = 15.0.26730.15
MinimumVisualStudioVersion = 10.0.40219.1
```

### <a name="definitions"></a>Definições

`Microsoft Visual Studio Solution File, Format Version 12.00`\
Cabeçalho padrão que define a versão do formato de arquivo.

`# Visual Studio 15`\
A versão principal do Visual Studio que (mais recentemente) salvou esse arquivo de solução. Essas informações controlam o número de versão no ícone da solução.

`VisualStudioVersion = 15.0.26730.15`\
A versão completa do Visual Studio que (mais recentemente) salvou o arquivo de solução. Se o arquivo da solução for salvo por uma versão mais recente do Visual Studio que tem a mesma versão principal, esse valor não será atualizado para reduzir a rotatividade em arquivos de solução.

`MinimumVisualStudioVersion = 10.0.40219.1`\
A versão mínima (mais antiga) do Visual Studio que pode abrir esse arquivo de solução.

::: moniker-end

::: moniker range=">=vs-2019"

```
Microsoft Visual Studio Solution File, Format Version 12.00
# Visual Studio Version 16
VisualStudioVersion = 16.0.28701.123
MinimumVisualStudioVersion = 10.0.40219.1
```

### <a name="definitions"></a>Definições

`Microsoft Visual Studio Solution File, Format Version 12.00`\
Cabeçalho padrão que define a versão do formato de arquivo.

`# Visual Studio Version 16`\
A versão principal do Visual Studio que (mais recentemente) salvou esse arquivo de solução. Essas informações controlam o número de versão no ícone da solução.

`VisualStudioVersion = 16.0.28701.123`\
A versão completa do Visual Studio que (mais recentemente) salvou o arquivo de solução. Se o arquivo da solução for salvo por uma versão mais recente do Visual Studio que tem a mesma versão principal, esse valor não será atualizado para reduzir a rotatividade no arquivo.

`MinimumVisualStudioVersion = 10.0.40219.1`\
A versão mínima (mais antiga) do Visual Studio que pode abrir esse arquivo de solução.

::: moniker-end

## <a name="file-body"></a>Corpo do arquivo

O corpo de um arquivo. sln consiste em várias seções rotuladas `GlobalSection` , desta forma:

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

Para carregar uma solução, o ambiente executa a seguinte sequência de tarefas:

1. O ambiente lê a seção global do arquivo. sln e processa todas as seções marcadas `preSolution` . Neste arquivo de exemplo, há uma dessas instruções:

   ```
   GlobalSection(SolutionConfiguration) = preSolution
        ConfigName.0 = Debug
        ConfigName.1 = Release
   ```

   Quando o ambiente lê a `GlobalSection('name')` marca, ele mapeia o nome para um VSPackage usando o registro. O nome da chave deve existir no registro em [HKLM \\<ID do aplicativo \SolutionPersistence\AggregateGUIDs raiz do registro \> ]. O valor padrão das chaves é o GUID do pacote (REG_SZ) do VSPackage que gravou as entradas.

2. O ambiente carrega o VSPackage, chama o `QueryInterface` VSPackage para a <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps> interface e chama o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.ReadSolutionProps%2A> método com os dados na seção para que o VSPackage possa armazenar os dados. O ambiente repete esse processo para cada `preSolution` seção.

3. O ambiente percorre os blocos de persistência do projeto. Nesse caso, há um projeto.

   ```
   Project("{F184B08F-C81C-45F6-A57F-5ABD9991F28F}") = "Project1",
   "Project1.vbproj", "{8CDD8387-B905-44A8-B5D5-07BB50E05BEA}"
   EndProject
   ```

   Essa instrução contém o GUID do projeto exclusivo e o GUID do tipo de projeto. Essas informações são usadas pelo ambiente para localizar o arquivo de projeto ou arquivos pertencentes à solução e o VSPackage necessário para cada projeto. O GUID do projeto é passado para <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory> para carregar o VSPackage específico relacionado ao projeto e, em seguida, o projeto é carregado pelo VSPackage. Nesse caso, o VSPackage que é carregado para esse projeto é Visual Basic.

   Cada projeto pode persistir uma ID de instância de projeto exclusiva para que possa ser acessado conforme necessário por outros projetos na solução. Idealmente, se a solução e os projetos estiverem sob controle do código-fonte, o caminho para o projeto deve ser relativo ao caminho para a solução. Quando a solução é carregada pela primeira vez, os arquivos de projeto não podem estar na máquina do usuário. Com o arquivo de projeto armazenado no servidor em relação ao arquivo de solução, é relativamente simples que o arquivo de projeto seja encontrado e copiado para o computador do usuário. Em seguida, ele copia e carrega o restante dos arquivos necessários para o projeto.

4. Com base nas informações contidas na seção projeto do arquivo. sln, o ambiente carrega cada arquivo de projeto. O projeto em si é, então, responsável por preencher a hierarquia do projeto e carregar quaisquer projetos aninhados.

5. Depois que todas as seções do arquivo. sln são processadas, a solução é exibida no Gerenciador de Soluções e está pronta para modificação pelo usuário.

Se qualquer VSPackage que implemente um projeto na solução falhar ao ser carregado, o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.OnProjectLoadFailure%2A> método será chamado e todos os outros projetos na solução terão a oportunidade de ignorar as alterações que podem ter sido feitas durante o carregamento. Se ocorrerem erros de análise, o máximo de informações possível é preservado com os arquivos da solução e o ambiente exibe uma caixa de diálogo avisando o usuário de que a solução está corrompida.

Quando a solução é salva ou fechada, o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.QuerySaveSolutionProps%2A> método é chamado e passado para a hierarquia para ver se foram feitas alterações na solução que precisam ser inseridas no arquivo. sln. Um valor nulo, passado para `QuerySaveSolutionProps` no <xref:Microsoft.VisualStudio.Shell.Interop.VSQUERYSAVESLNPROPS> , indica que as informações estão sendo persistidas para a solução. Se o valor não for nulo, as informações persistentes serão para um projeto específico, determinado pelo ponteiro para a <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> interface.

Se houver informações a serem salvas, a <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence> interface será chamada com um ponteiro para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.SaveSolutionProps%2A> método. O <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.WriteSolutionProps%2A> método é então chamado pelo ambiente para recuperar os pares de nome-valor da `IPropertyBag` interface e gravar as informações no arquivo. sln.

`SaveSolutionProps` e os `WriteSolutionProps` objetos são chamados recursivamente pelo ambiente para recuperar informações a serem salvas da `IPropertyBag` interface até que todas as alterações tenham sido inseridas no arquivo. sln. Dessa forma, você pode garantir que as informações serão persistidas com a solução e disponíveis na próxima vez em que a solução for aberta.

Cada VSPackage carregada é enumerada para ver se há algo a ser salvo no arquivo. sln. É apenas no momento da carga que as chaves do registro são consultadas. O ambiente conhece todos os pacotes carregados porque eles estão na memória no momento em que a solução é salva.

Somente o arquivo. sln contém entradas nas `preSolution` seções e `postSolution` . Não há seções semelhantes no arquivo. suo, pois a solução precisa que essas informações sejam carregadas corretamente. O arquivo. suo contém opções específicas do usuário, como notas particulares, que não devem ser compartilhadas ou colocadas sob controle do código-fonte.

## <a name="see-also"></a>Confira também

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps>
- [Arquivo .Suo (Solution User Options)](../../extensibility/internals/solution-user-options-dot-suo-file.md)
- [Soluções](../../extensibility/internals/solutions-overview.md)
