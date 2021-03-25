---
title: Registrando um idioma herdado Service2 | Microsoft Docs
description: Este artigo lista as entradas do registro para as várias opções de serviço de linguagem disponíveis no Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- registration, language services
- language services, registry information
- registry, language services
ms.assetid: ca312aa3-f9f1-4572-8553-89bf3a724deb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: fbad469b28c0b8a6aab070d47cf12c326beb92d8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062779"
---
# <a name="registering-a-legacy-language-service-2"></a>Registrando um serviço de idioma herdado 2
As seções a seguir fornecem listas de entradas de registro para as várias opções de serviço de linguagem disponíveis no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] .

 Na lista de entradas de registro a seguir, a *raiz do vs reg* é igual a HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\\ *x. y*, em que *x. y* é o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] número de versão.

## <a name="registry-entries-for-language-service-options"></a>Entradas de registro para opções de serviço de idioma
 A chave do nome do idioma dos serviços \Languages\Languages *raiz vs reg* \\  pode conter os valores a seguir.

|Nome|Type|Intervalo|Descrição|
|----------|----------|-----------|-----------------|
|(Padrão)|REG_SZ|*\<GUID>*|GUID do serviço de idioma.|
|LangResID|REG_DWORD|0x0-0xFFFF|ResID (identificador de recurso de cadeia de caracteres) para o nome de texto localizado do idioma.|
|Pacote|REG_SZ|*\<GUID>*|GUID do VSPackage.|
|Conclusão|REG_DWORD|0-1|Especifica se as opções de **conclusão de instrução** na caixa de diálogo **Opções** estão habilitadas.|
|ShowSmartIndent|REG_DWORD|0-1|Especifica se a opção para selecionar recuo **inteligente** na caixa de diálogo **Opções** está habilitada.|
|RequestStockColors|REG_DWORD|0-1|Especifica se as cores personalizadas ou padrão são usadas para colorir palavras-chave.|
|ShowHotURLs|REG_DWORD|0-1|Especifica se o usuário pode clicar em URLs.|
|Padrão para URLs não quentes|REG_DWORD|0-1|Especifica a configuração inicial para a opção de **navegação habilitar URL de clique único** na caixa de diálogo **Opções** .|
|DefaultToInsertSpaces|REG_DWORD|0-1|Especifica se o serviço de idioma tem "Inserir espaços" como sua opção de guia padrão.|
|ShowDropdownBarOption|REG_DWORD|0-1|Habilita ou desabilita a opção **barra de navegação** na caixa de diálogo **Opções** que mostra ou oculta a barra de **navegação**.|
|Somente janela de código único|REG_DWORD|0-1|Habilita ou desabilita a nova opção de **janela** no menu **janela** de um serviço de idioma.|
|EnableAdvancedMembersOption|REG_DWORD|0-1|Habilita ou desabilita uma configuração da caixa de diálogo **Opções** para **ocultar membros avançados**.|
|Suporte CF_HTML|REG_DWORD|0-1|Especifica se o editor permite copiar e colar dados HTML.|
|EnableLineNumbersOption|REG_DWORD|0-1|Especifica se as opções de **números de linha** na caixa de diálogo **Opções** estão habilitadas para um serviço de idioma.|
|HideAdvancedMembersByDefault|REG_DWORD|0-1|Especifica se membros avançados, como campos particulares, são ocultados em listas de conclusão.|
|ShowBraceCompletion|REG_DWORD|0-1|Especifica se a opção de **preenchimento de chave** na caixa de diálogo **Opções** está habilitada.|

### <a name="example"></a>Exemplo

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\
  Languages\
    Language Services\
      C/C++\
        (Default)             = reg_sz:{B2F072B0-ABC1-11D0-9D62-00C04FD9DFD9}
        LangResID             = reg_dword:0x00000000
        Package               = reg_sz:{8C2EA640-ABC1-11D0-9D62-00C04FD9DFD9}
        ShowCompletion        = reg_dword:0x00000001
        ShowSmartIndent       = reg_dword:0x00000001
        ShowDropdownBarOption = reg_dword:0x00000001
```

## <a name="registry-entries-for-debugger-languages-options"></a>Entradas de registro para opções de idiomas do depurador
 O nome do idioma dos serviços \Languages\Languages *raiz vs reg* \\ \Debugger *Languages* \\ *GUID*\ Key pode incluir os valores a seguir.

|Nome|Type|Intervalo|Descrição|
|----------|----------|-----------|-----------------|
|(Padrão)|REG_SZ|text|O valor padrão pode ser usado para documentar o nome do idioma. O nome dessa chave é um GUID de um avaliador de expressão que tem uma entrada correspondente no *\<VS Reg Root>* avaliador \AD7Metrics\Expression.|

### <a name="example"></a>Exemplo

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\
  Languages\
    Language Services\
      C/C++\
        Debugger Languages\
          {3A12D0B7-C26C-11D0-B442-00A0244A1DD2}\
            (Default) = reg_sz:C++
```

## <a name="registry-entries-for-editor-tools-options"></a>Entradas de registro para opções de ferramentas do editor
 Você pode adicionar chaves do registro na chave EditorToolsOptions para páginas de propriedades e nós de propriedade. Essas chaves e seus valores identificam páginas de propriedades na caixa de diálogo **Opções** (no menu **ferramentas** ) que são usadas para configurar o serviço de idioma. No exemplo a seguir, *nome da página* é o nome de uma página de propriedades e *nome do nó* é o nome de um nó na árvore na caixa de diálogo **Opções** . A entrada de página e a entrada de nó devem ser especificadas separadamente.

|Nome|Type|Intervalo|Descrição|
|----------|----------|-----------|-----------------|
|(Padrão)|REG_SZ|ResID|O nome de exibição localizado desta página de opções. O nome pode ser um texto literal, ou # `nnn` , em que `nnn` é uma ID de recurso de cadeia de caracteres na DLL satélite do VSPackage especificado.|
|Pacote|REG_SZ|*GUID*|O GUID do VSPackage que implementa essa página de opções.|
|?|REG_SZ|*GUID*|O GUID da página de propriedades a ser solicitada do VSPackage chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A> método. Se essa entrada de registro não estiver presente, a chave do registro descreve um nó, e não uma página.|

### <a name="example"></a>Exemplo

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\
  Languages\
    Language Services\
      CSharp\
        EditorToolsOptions\
          Formatting\
            (Default) = reg_sz:#242
            Package   = reg_sz:{A066E284-DCAB-11D2-B551-00C04F68D4DB}
            General\
              (Default) = reg_sz:#255
              Package   = reg_sz:{A066E284-DCAB-11D2-B551-00C04F68D4DB}
              Page      = reg_sz:{3EB2CC0B-033E-4D75-B26A-B2362C25227E}
            Indentation\
              (Default) = reg_sz:#250
              Package   = reg_sz:{A066E284-DCAB-11D2-B551-00C04F68D4DB}
              Page      = reg_sz:{5E21D017-6D2A-4114-A1F1-C923F001CBBB}
            Newlines\
              (Default) = reg_sz:#253
              Package   = reg_sz:{A066E284-DCAB-11D2-B551-00C04F68D4DB}
              Page      = reg_sz:{607D8062-68D1-41E4-9A35-B5E7F14D0481}
```

## <a name="registry-entries-for-file-name-extension-options"></a>Entradas de registro para opções de extensão de nome de arquivo
 A entrada para a extensão de arquivo deve incluir o período à esquerda, por exemplo ". myext".

|Nome|Type|Intervalo|Descrição|
|----------|----------|-----------|-----------------|
|(Padrão)|REG_SZ|*GUID*|GUID de serviço para o serviço de idioma padrão para este tipo de extensão de nome de arquivo.|

### <a name="example"></a>Exemplo

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\
  Languages\
    File Extensions\
      .cpp\
        (Default) = {B2F072B0-ABC1-11D0-9D62-00C04FD9DFD9}
```

## <a name="registry-entries-for-editor-options"></a>Entradas do registro para opções do editor
 A chave \Editors do *vs reg raiz* pode conter os seguintes valores:

|Nome|Type|Intervalo|Descrição|
|----------|----------|-----------|-----------------|
|(Padrão)|REG_SZ|""|Não utilizado Você pode colocar seu nome aqui para documentação.|
|DefaultToolboxTab|REG_SZ|""|Nome da guia caixa de ferramentas para tornar o padrão quando o editor estiver ativo.|
|DisplayName|REG_SZ|ResID|Nome a ser exibido na caixa de diálogo **abrir com** . O nome é a ID de recurso de cadeia de caracteres ou um nome no formato padrão.|
|ExcludeDefTextEditor|REG_DWORD|0-1|Usado para o comando de menu **abrir com** . Se você não quiser listar o editor de texto padrão na lista de editores disponíveis para um tipo de arquivo específico, defina esse valor como 1.|
|LinkedEditorGUID|REG_SZ|*\<GUID>*|Usado para qualquer serviço de linguagem que possa abrir um arquivo com suporte de página de código. Por exemplo, quando você abre um arquivo. txt usando o comando **abrir com** , as opções são fornecidas para usar o editor de código-fonte com e sem codificação.<br /><br /> O GUID especificado no nome da subchave é para a fábrica do editor de página de código; o GUID vinculado especificado nesta entrada de Registro específica é para a fábrica de editor regular. A finalidade dessa entrada é que, se o IDE não abrir um arquivo usando o editor padrão, o IDE tentará usar o próximo editor na lista. Este próximo editor não deve ser a fábrica do editor de página de código porque essa fábrica do editor é basicamente a mesma que a fábrica do editor que falhou.|
|Pacote|REG_SZ|*\<GUID>*|VSPackage GUID para o ResID do nome de exibição.|

### <a name="example"></a>Exemplo

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\
  \Editors\
    {8281C572-2171-45AA-A642-7D8BC1662F1C}\
      (Default)            = reg_sz:Html Editor with Encoding
      DefaultToolboxTab    = reg_sz:HTML
      DisplayName          = reg_sz:#20101
      LinkedEditorGUID     = reg_sz:{C76D83F8-A489-11D0-8195-00A0C91BBEE3}
      Package              = reg_sz:{1B437D20-F8FE-11D2-A6AE-00104BCC7269}
```

## <a name="registry-entries-for-logical-view-options"></a>Entradas de registro para opções de exibição lógica
 A GUI do editor \Editors do *vs reg raiz* \\ *>* chave \LogicalViews pode conter os valores a seguir.

|Nome|Type|Intervalo|Descrição|
|----------|----------|-----------|-----------------|
|(Padrão)|REG_SZ||Não utilizado.|
|*\<GUID>*|REG_SZ|""|Chave para as exibições lógicas com suporte. Você pode ter quantas delas forem necessárias. O nome da entrada do registro é o que é importante, não o valor, que é sempre uma cadeia de caracteres vazia.|

### <a name="example"></a>Exemplo

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\
  \Editors\
    {8281C572-2171-45AA-A642-7D8BC1662F1C}\
      LogicalViews\
       (Default) = reg_sz:
       {7651a700-06e5-11d1-8ebd-00a0c90f26ea} = reg_sz:
       {7651a701-06e5-11d1-8ebd-00a0c90f26ea} = reg_sz:
       {7651a702-06e5-11d1-8ebd-00a0c90f26ea} = reg_sz:
       {7651a703-06e5-11d1-8ebd-00a0c90f26ea} = reg_sz:
```

## <a name="registry-entries-for-editor-extension-options"></a>Entradas de registro para opções de extensão do editor
 A chave \Extensions do GUID do editor \Editors do *vs reg raiz* \\ pode conter os valores a seguir. A extensão de nome de arquivo não inclui o período à esquerda.

|Nome|Type|Intervalo|Descrição|
|----------|----------|-----------|-----------------|
|(Padrão)|REG_SZ||Não utilizado.|
|*\<ext>*|REG_DWORD|0-0xFFFFFFFF|Prioridade relativa de extensões. Se dois ou mais idiomas compartilharem a mesma extensão, a linguagem de prioridade mais alta será escolhida.|

 Além disso, a seleção padrão do usuário atual para um editor é armazenada em HKEY_Current_User \Software\Microsoft\VisualStudio \\ *X. Y*\Default Editors \\ *ext*. O GUID do serviço de idioma selecionado está na entrada personalizada. Isso tem precedência para o usuário atual.

### <a name="example"></a>Exemplo

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\9.0\
  \Editors\
    {8281C572-2171-45AA-A642-7D8BC1662F1C}\
      Extensions\
       (Default) = reg_sz:
       *         = reg_dword:0x00000018
       html      = reg_dword:0x00000027
       shtm      = reg_dword:0x00000027
       shtml     = reg_dword:0x00000027
```

## <a name="registry-entries-for-managed-package-framework-language-service-options"></a>Entradas de registro para opções de serviço de linguagem da estrutura de pacote gerenciado
 As entradas de registro a seguir são específicas para as classes de serviço de linguagem MPF (estrutura de pacote gerenciada). Essas entradas de registro indicam suporte no serviço de linguagem para vários recursos do IntelliSense e para outros recursos de edição avançados.

 Essas entradas de registro são acessadas por meio da <xref:Microsoft.VisualStudio.Package.LanguagePreferences> classe.

|Nome|Type|Intervalo|Descrição|
|----------|----------|-----------|-----------------|
|CodeSense|REG_DWORD|0-1|Suporte para operações do IntelliSense.|
|MatchBraces|REG_DWORD|0-1|Suporte para pares de idiomas correspondentes, como chaves, parênteses e colchetes.|
|QuickInfo|REG_DWORD|0-1|Suporte para a operação de informações rápidas do IntelliSense.|
|ShowMatchingBrace|REG_DWORD|0-1|Suporte para exibir o par de idiomas correspondentes na barra de status.|
|MatchBracesAtCaret|REG_DWORD|0-1|Suporte para exibir pares de idiomas correspondentes, normalmente, ao realçar os dois elementos.|
|MaxErrorMessages|REG_DWORD|0-n|O número máximo de erros que podem ser exibidos na janela de **lista de erros** .|
|CodeSenseDelay|REG_DWORD|0-n|O número de milissegundos de atraso antes de iniciar qualquer análise em segundo plano para uma operação do IntelliSense.|
|EnableAsyncCompletion|REG_DWORD|0-1|Suporte para análise em segundo plano.|
|EnableCommenting|REG_DWORD|0-1|Suporte para comentários dos blocos de texto selecionados e também implica suporte para remover a marca de comentário do texto selecionado.|
|EnableFormatSelection|REG_DWORD|0-1|Suporte para formatação de texto, como Recuo automático ou ajuste da posição das chaves.|
|Estrutura de tópicos|REG_DWORD|0-1|Suporte para estrutura de tópicos (regiões que podem ser recolhidas).|
|MaxRegions|REG_DWORD|0-n|O número máximo de regiões ocultas por arquivo.|

```
ExampleHKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\
  Languages\
    Language Services\
      XML\
        (Default)             = reg_sz:{f6819a78-a205-47b5-be1c-675b3c7f0b8e}
        MatchBraces           = reg_dword:0x00000001
        QuickInfo             = reg_dword:0x00000001
        ShowMatchingBrace     = reg_dword:0x00000001
        MatchBracesAtCaret    = reg_dword:0x00000000
        MaxErrorMessages      = reg_dword:0x00000064
        CodeSenseDelay        = reg_dword:0x000001f4
        MaxRegions            = reg_dword:0x0000000a
```

## <a name="see-also"></a>Confira também
- [Desenvolvendo um serviço de linguagem herdado](../../extensibility/internals/developing-a-legacy-language-service.md)
