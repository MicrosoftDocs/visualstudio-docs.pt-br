---
title: Manual de referência de IntelliTest | Ferramentas de teste do Desenvolvedor Microsoft
ms.date: 05/02/2017
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.topic: conceptual
helpviewer_keywords:
- IntelliTest Reference Manual, IntelliTest
ms.author: gewarren
manager: douge
ms.workload:
- multiple
author: gewarren
ms.openlocfilehash: 982d54bec30e164a1b2017c7aa8a221ee56e19d0
ms.sourcegitcommit: e481d0055c0724d20003509000fd5f72fe9d1340
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51000592"
---
# <a name="intellitest-reference-manual"></a>Manual de referência do IntelliTest

## <a name="contents"></a>Conteúdo

* **[Visão geral do IntelliTest](introduction.md)**
  - [O Olá, Mundo do IntelliTest](introduction.md#the-hello-world-of-intellitest)
  - [Limitações](introduction.md#limitations)
    * [Não determinismo](introduction.md#nondeterminism)
    * [Simultaneidade](introduction.md#concurrency)
    * [Código nativo](introduction.md#native-code)
    * [Plataforma](introduction.md#platform)
    * [Linguagem](introduction.md#language)
    * [Raciocínio simbólico](introduction.md#symbolic-reasoning)
    * [Rastreamentos de pilha incorretos](introduction.md#incorrect-stack-traces)
  - [Leitura adicional](introduction.md#further-reading)<p>&nbsp;</p>

* **[Introdução ao IntelliTest](getting-started.md)**
  - [Atributos importantes](getting-started.md#important-attributes)
  - [Classes auxiliares estáticas importantes](getting-started.md#helper-classes)<p>&nbsp;</p>

* **[Geração de teste](test-generation.md)**
  - [Geradores de teste](test-generation.md#test-generators)
  - [Teste de unidade parametrizado](test-generation.md#parameterized-unit-testing)
  - [Teste de unidade parametrizado genérico](test-generation.md#generic-parameterized)
  - [Permissão de exceções](test-generation.md#allowing-exceptions)
  - [Teste de tipos internos](test-generation.md#internal-types)
  - [Suposições e declarações](test-generation.md#assumptions-and-assertions)
  - [Pré-condição](test-generation.md#precondition)
  - [Pós-condição](test-generation.md#postcondition)
  - [Falhas de teste](test-generation.md#test-failures)
  - [Configuração e desmontagem](test-generation.md#setup-teardown)
  - [Leitura adicional](test-generation.md#further-reading)<p>&nbsp;</p>

* **[Geração de entrada](input-generation.md)**
  - [Solver de restrição](input-generation.md#constraint-solver)
  - [Cobertura de código dinâmico](input-generation.md#dynamic-code-coverage)
  - [Números inteiros e flutuações](input-generation.md#integers-and-floats)
  - [Objetos](input-generation.md#objects)
  - [Instanciação de classes existentes](input-generation.md#existing-classes)
  - [Visibilidade](input-generation.md#visibility)
  - [Simulações parametrizadas](input-generation.md#parameterized-mocks)
  - [Estruturas](input-generation.md#structs)
  - [Matrizes e cadeias de caracteres](input-generation.md#arrays-and-strings)
  - [Obtenção de entradas adicionais](input-generation.md#additional-inputs)
  - [Leitura adicional](input-generation.md#further-reading)<p>&nbsp;</p>

* **[Limites de exploração](exploration-bounds.md)**
  - [MaxConstraintSolverTime](exploration-bounds.md#maxconstraintsolvertime)
  - [MaxConstraintSolverMemory](exploration-bounds.md#maxconstraintsolvermemory)
  - [MaxBranches](exploration-bounds.md#maxbranches)
  - [MaxCalls](exploration-bounds.md#maxcalls)
  - [MaxStack](exploration-bounds.md#maxstack)
  - [MaxConditions](exploration-bounds.md#maxconditions)
  - [MaxRuns](exploration-bounds.md#maxruns)
  - [MaxRunsWithoutNewTests](exploration-bounds.md#maxrunswithoutnewtests)
  - [MaxRunsWithUniquePaths](exploration-bounds.md#maxrunswithuniquepaths)
  - [MaxExceptions](exploration-bounds.md#maxexceptions)
  - [TestExcludePathBoundsExceeded](exploration-bounds.md#testexcludepathboundsexceeded)
  - [TestEmissionFilter](exploration-bounds.md#testemissionfilter)
  - [TestEmissionBranchHits](exploration-bounds.md#testemissionbranchhits)<p>&nbsp;</p>

* **[Glossário do atributo](attribute-glossary.md)**
  - [PexAssumeNotNull](attribute-glossary.md#pexassumenotnull)
  - [PexClass](attribute-glossary.md#pexclass)
  - [PexGenericArguments](attribute-glossary.md#pexgenericarguments)
  - [PexMethod](attribute-glossary.md#pexmethod)
  - [PexExplorationAttributeBase](attribute-glossary.md#pexexplorationattributebase)
  - [PexAssemblySettings](attribute-glossary.md#pexassemblysettings)
  - [PexAssemblyUnderTest](attribute-glossary.md#pexassemblyundertest)
  - [PexInstrumentAssemblyAttribute](attribute-glossary.md#pexinstrumentassemblyattribute)
  - [PexUseType](attribute-glossary.md#pexusetype)
  - [PexAllowedException](attribute-glossary.md#pexallowedexception)
  - [PexAllowedExceptionFromAssembly](attribute-glossary.md#pexallowedexceptionfromassembly)
  - [PexAllowedExceptionFromType](attribute-glossary.md#pexallowedexceptionfromtype)
  - [PexAllowedExceptionFromTypeUnderTest](attribute-glossary.md#pexallowedexceptionfromtypeundertest)<p>&nbsp;</p>

* **[Cascata de configurações](settings-waterfall.md)**

* **[Classes auxiliares estáticas](static-helper-classes.md)**
  - [PexAssume](static-helper-classes.md#pexassume)
  - [PexAssert](static-helper-classes.md#pexassert)
  - [PexChoose](static-helper-classes.md#pexchoose)
  - [PexObserve](static-helper-classes.md#pexobserve)
  - [PexSymbolicValue](static-helper-classes.md#pexsymbolicvalue)<p>&nbsp;</p>

* **[Avisos e erros](warnings-and-errors.md)**
  - [MaxBranches excedido](warnings-and-errors.md#maxbranches-exceeded)
  - [MaxConstraintSolverTime excedido](warnings-and-errors.md#maxconstraintsolvertime-exceeded)
  - [MaxConditions excedido](warnings-and-errors.md#maxconditions-exceeded)
  - [MaxCalls excedido](warnings-and-errors.md#maxcalls-exceeded)
  - [MaxStack excedido](warnings-and-errors.md#maxstack-exceeded)
  - [MaxRuns excedido](warnings-and-errors.md#maxruns-exceeded)
  - [MaxRunsWithoutNewTests excedido](warnings-and-errors.md#maxrunswithoutnewtests-exceeded)
  - [Não é possível concretizar a solução](warnings-and-errors.md#cannot-concretize-solution)
  - [Precisa de ajuda para o objeto do constructo](warnings-and-errors.md#help-construct)
  - [Precisa de ajuda para encontrar tipos](warnings-and-errors.md#help-types)
  - [Tipo utilizável estimado](warnings-and-errors.md#usable-type-guessed)
  - [Falha inesperada durante a exploração](warnings-and-errors.md#unexpected-exploration)
  - [TargetInvocationException](warnings-and-errors.md#targetinvocationexception)
  - [Método não instrumentado chamado](warnings-and-errors.md#uninstrumented-method-called)
  - [Método externo chamado](warnings-and-errors.md#external-method-called)
  - [Método não instrumentável chamado](warnings-and-errors.md#uninstrumentable-method-called)
  - [Problema de capacidade de teste](warnings-and-errors.md#testability-issue)
  - [Limitação](warnings-and-errors.md#limitation)
  - [Incompatibilidade de chamada observada](warnings-and-errors.md#observed-call-mismatch)
  - [Valor armazenado no campo estático](warnings-and-errors.md#value-static-field)<p>&nbsp;</p>

## <a name="got-feedback"></a>Recebeu comentários?

Poste suas ideias e solicitações de recursos no [Developer Community](https://developercommunity.visualstudio.com/content/idea/post.html?space=8).