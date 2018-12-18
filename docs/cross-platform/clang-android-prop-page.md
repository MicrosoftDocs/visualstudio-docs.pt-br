---
title: Propriedades do projeto Clang (Android C++) | Microsoft Docs
ms.custom: ''
ms.date: 10/23/2017
ms.technology: vs-ide-mobile
ms.topic: conceptual
ms.assetid: 663140ea-a568-472b-a79a-dfea8818e06a
author: corob
ms.author: mblome
manager: douge
f1_keywords:
- VC.Project.VCClangCompilerTool.AdditionalIncludeDirectories
- VC.Project.VCClangCompilerTool.DebugInformationFormat
- VC.Project.VCClangCompilerTool.ObjectFile
- VC.Project.VCClangCompilerTool.WarningLevel
- VC.Project.VCClangCompilerTool.WarnAsError
- VC.Project.VCClangCompilerTool.Verbose
- VC.Project.VCClangCompilerTool.Optimization
- VC.Project.VCClangCompilerTool.StrictAliasing
- VC.Project.VCClangCompilerTool.OmitFramePointers
- VC.Project.VCClangCompilerTool.ExceptionHandling
- VC.Project.VCClangCompilerTool.EnableFunctionLevelLinking
- VC.Project.VCClangCompilerTool.DataLevelLinking
- VC.Project.VCClangCompilerTool.DataLevelLinking
- VC.Project.VCClangCompilerTool.FloatABI
- VC.Project.VCClangCompilerTool.BufferSecurityCheck
- VC.Project.VCClangCompilerTool.PIC
- VC.Project.VCClangCompilerTool.UseShortEnums
- VC.Project.VCClangCompilerTool.RuntimeTypeInfo
- VC.Project.VCClangCompilerTool.CLanguageStandard
- VC.Project.VCClangCompilerTool.CppLanguageStandard
- VC.Project.VCClangCompilerTool.PreprocessorDefinitions
- VC.Project.VCClangCompilerTool.UndefinePreprocessorDefinitions
- VC.Project.VCClangCompilerTool.UndefineAllPreprocessorDefinitions
- VC.Project.VCClangCompilerTool.ShowIncludes
- VC.Project.VCClangCompilerTool.PrecompiledHeader
- VC.Project.VCClangCompilerTool.PrecompiledHeaderFile
- VC.Project.VCClangCompilerTool.PrecompiledHeaderOutputFileDirectory
- VC.Project.VCClangCompilerTool.PrecompiledHeaderCompileAs
- VC.Project.VCClangCompilerTool.CompileAs
- VC.Project.VCClangCompilerTool.ForcedIncludeFiles
- VC.Project.VCClangCompilerTool.MultiProcessorCompilation
- vc.project.AdditionalOptionsPage
ms.workload:
- xplat-cplusplus
ms.openlocfilehash: efceeb201a7f1afcbf7cc2c6d46619301284d823
ms.sourcegitcommit: 25a62c2db771f938e3baa658df8b1ae54a960e4f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2018
ms.locfileid: "39232111"
---
# <a name="clang-project-properties-android-c"></a>Propriedades do projeto Clang (Android C++)

Propriedade | Descrição | Opções
--- | ---| ---
Diretórios de Inclusão Adicionais | Especifica um ou mais diretórios a serem adicionados ao caminho de inclusão, separados por ponto e vírgula no caso de mais de um. (-I[path]).
Formato de informações de depuração | Especifica o tipo de informações de depuração geradas pelo compilador. | **Nenhum** – não produz nenhuma informação de depuração, portanto, a compilação pode ser mais rápida.<br>**Informações de depuração completas (DWARF2)** – gerar informações de depuração DWARF2.<br>**Informações de número de linha** – gerar somente informações de número de linha.<br>
Nome do arquivo-objeto | Especifica um nome para substituir o nome do arquivo-objeto padrão. Pode ser um nome de arquivo ou de diretório. (/Fo[name]).
Nível de aviso | Selecione o rigor que você deseja que o compilador aplique aos erros de código.  Outros sinalizadores devem ser adicionados diretamente às Opções Adicionais. (/w, /Weverything). | **Desligar todos os avisos** – desabilita todos os avisos do compilador.<br>**EnableAllWarnings** – habilita todos os avisos, incluindo os que são desabilitados por padrão.<br>
Tratar avisos como erros | Trata todos os avisos do compilador como erros. Para um novo projeto, talvez seja melhor usar /WX em todas as compilações. Resolver todos os avisos assegurará o menor número possível de defeitos de código difíceis de localizar.
Habilitar modo detalhado | Mostrar os comandos a serem executados e usar a saída detalhada.
Otimização | Especifica o nível de otimização para o aplicativo. | **Personalizar** – otimização personalizada.<br>**Desabilitado** – desabilitar a otimização.<br>**Minimizar tamanho** – otimizar o tamanho.<br>**Maximizar velocidade** – otimizar a velocidade.<br>**Otimização total** – otimizações de alto custo.<br>
Alias estrito | Considere as regras de alias mais rígidas.  Um objeto de um tipo nunca será considerado como residente do mesmo endereço que um objeto de um tipo diferente.
Omitir ponteiro de quadro | Inibe a criação de ponteiros de quadros na pilha de chamadas.
Habilitar exceções C++ | Especifica o modelo de tratamento de exceções a ser utilizado pelo compilador. | **Não** – desabilitar o tratamento de exceções.<br>**Sim** – habilitar tratamento de exceções.<br>**Desenrolar tabelas** – gera todos os dados estáticos necessários, mas não afeta o código gerado.<br>
Habilitar vinculação no nível da função | Permite que o compilador empacote funções individuais no formato de funções empacotadas (COMDATs). Necessário para editar e continuar a trabalhar.     (ffunction-sections).
Habilitar vinculação no nível dos dados | Habilita as otimizações do vinculador para remover dados não utilizados ao emitir cada item de dados em uma seção separada.
Habilitar SIMD(Neon) avançado | Habilita a geração de código para hardware de ponto flutuante NEON. Somente se aplica a arquiteturas arm.
ABI de ponto flutuante | Opção de seleção para escolher o ABI de ponto flutuante. | **Suave** – 'Suave' faz com que o compilador gere saídas contendo chamadas da biblioteca para operações de ponto flutuante.<br>**SoftFP** – 'SoftFP' permite a geração de código usando instruções de ponto flutuante de hardware, mas ainda usa as convenções de chamada de flutuação suave.<br>**Rígido** – 'Rígido' permite a geração de instruções de ponto flutuante e usa convenções de chamada específicas de FPU.<br>
Verificação de segurança | A Verificação de Segurança ajuda a detectar saturações de buffer de pilha, uma tentativa de ataque comum à segurança de um programa. (fstack-protector). | **Desabilitar verificação de segurança** – Desabilitar a verificação de segurança.<br>**Habilitar verificação de segurança** – Habilitar a verificação de segurança. (fstack-protector)<br>
Código independente da posição | Gerar um PIC (código independente da posição) para ser usado em uma biblioteca compartilhada.
Usar enums curtas | O tipo enum usa somente o número de bytes exigido pelo conjunto de entrada de valores possíveis.
Habilitar informações de tipo de tempo de execução | Adiciona um código para verificar os tipos de objeto C++ no tempo de execução (informações de tipo de tempo de execução).     (frtti, fno-rtti)
Padrão de linguagem C | Determina o padrão de linguagem C. | **Padrão**<br>**C89** – padrão de linguagem C89.<br>**C99** – padrão de linguagem C99.<br>**C11** – padrão de linguagem C11.<br>**C99 (dialeto GNU)** – padrão de linguagem C99 (dialeto GNU).<br>**C11 (dialeto GNU)** – padrão de linguagem C11 (dialeto GNU).<br>
Padrão de linguagem C++ | Determina o padrão de linguagem C++. | **Padrão**<br>**C++03** – padrão de linguagem C++03.<br>**C++11** – padrão de linguagem C++11.<br>**C++14** – padrão de linguagem C++14.<br>**C++03 (dialeto GNU)** – padrão de linguagem C++03 (dialeto GNU).<br>**C++11 (dialeto GNU)** – padrão de linguagem C++11 (dialeto GNU).<br>**C++14 (dialeto GNU)** – padrão de linguagem C++14 (dialeto GNU).<br>
Definições do Pré-processador | Define símbolos de pré-processamento para o arquivo de origem. (-D)
Excluir definições do pré-processador | Especifica uma ou mais exclusões de definição do pré-processador.  (-U [macro])
Excluir todas as definições do pré-processador | Exclua as definições de todos os valores do pré-processador definidos anteriormente.  (-undef)
Mostrar inclusões | Gera uma lista de arquivos de inclusão com a saída do compilador.  (-H)
Cabeçalho pré-compilado | Criar/usar cabeçalho pré-compilado: habilita a criação ou o uso de um cabeçalho pré-compilado durante o build. | **Use** – usar um cabeçalho pré-compilado.<br>**Não usar cabeçalhos pré-compilados** – não usar um cabeçalho pré-compilado.<br>
Arquivo de cabeçalho pré-compilado | Especifica o nome do arquivo de cabeçalho a ser usado para o arquivo de cabeçalho pré-compilado. Esse arquivo também será adicionado a 'Arquivos de inclusão forçados' durante o build
Diretório de arquivo de saída de cabeçalho pré-compilado | Especifica o diretório para o cabeçalho pré-compilado gerado. Este diretório também será adicionado a 'Diretórios de inclusão adicionais' durante o build
Compilar cabeçalho pré-compilado como | Selecionar a opção de linguagem de compilação para o arquivo de cabeçalho pré-compilado (-x c-header, -x c++-header). | **Compilar como código C** – compilar como código C.<br>**Compilar como código C++** – compilar como código C++.<br>
Compilar como | Selecione a opção de linguagem de compilação para arquivos .c e .cpp.  'Padrão' detectará com base na extensão .c ou .cpp. (-x c, -x c++) | **Padrão** – padrão.<br>**Compilar como código C** – compilar como código C.<br>**Compilar como código C++** – compilar como código C++.<br>
Arquivos de inclusão forçados | um ou mais arquivos de inclusão forçados.     (-include [name])
Compilação de multiprocessador | Compilação de multiprocessador.
Opções Adicionais | Opções adicionais.
