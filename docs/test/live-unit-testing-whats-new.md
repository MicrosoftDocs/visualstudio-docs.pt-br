---
title: Novidades no Live Unit Testing
ms.date: 10-11-2017
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio ALM
- Live Unit Testing
- Live Unit Testing What's New
author: rpetrusha
ms.author: ronpet
ms.workload:
- dotnet
ms.openlocfilehash: 4f3324d12d4bfc82e7980a690853b78321215205
ms.sourcegitcommit: 56ae5032d99d948aae0548ae318ca2bae97ea962
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2018
ms.locfileid: "39586457"
---
# <a name="whats-new-in-live-unit-testing"></a>Novidades no Live Unit Testing

Este tópico lista os novos recursos adicionados ao Live Unit Testing em cada versão do Visual Studio, iniciando com o Visual Studio 2017 versão 15.3. Para obter uma visão geral de como usar o Live Unit Testing, consulte [Live Unit Testing com o Visual Studio 2017](live-unit-testing.md).

## <a name="whats-new-in-live-unit-testing-for-visual-studio-2017-version-154"></a>Novidades no Live Unit Testing para Visual Studio 2017 versão 15.4

Começando com o Visual Studio 2017 versão 15.4, o Live Unit Testing inclui aprimoramentos e melhorias em várias áreas:

- **Detectabilidade aprimorada**. Para usuários que não sabem que o recurso Live Unit Testing existe, o IDE do Visual Studio mostra uma barra de ouro que menciona o Live Unit Testing sempre que o usuário abre uma solução que contém testes de unidade, mas o Live Unit Testing não está habilitado. As informações apresentadas na barra de ouro permitem que o usuário saiba mais sobre o Live Unit Testing e o habilite. A barra de ouro também exibe informações quando os pré-requisitos do Live Unit Testing não são atendidos. Elas incluem:

   - Adaptadores de teste ausentes.
   - Versões mais antigas dos adaptadores de teste presentes.
   - A necessidade de uma restauração dos pacotes NuGet referenciados pela solução. 

- **Integração com as notificações do Centro de Tarefas**. Agora, o IDE do Visual Studio mostra uma notificação de processamento em segundo plano do Live Unit Testing no Centro de Tarefas, para que os usuários possam perceber facilmente o que está acontecendo quando o Live Unit Testing está habilitado. Isso soluciona um problema importante de inicialização do Live Unit Testing em uma solução grande. Anteriormente, durante alguns minutos até que os ícones de cobertura apareciam, os usuários não podiam determinar se o Live Unit Testing estava realmente habilitado e se estava funcionando. Agora, não é mais assim!

- **Suporte para a versão 1 da estrutura do MSTest**: o Live Unit Testing já funciona com três estruturas de teste de unidade populares: xUnit, NUnit e MSTest. Anteriormente, o Live Unit Testing só funcionava quando projetos de teste de unidade do MSTest usavam MSTest versão 2. Começando com o Visual Studio 2017 versão 15.4, ele agora também é compatível com o MSTest versão 1. 

- **Confiabilidade e desempenho**: agora o Live Unit Testing garante que o sistema possa detectar melhor quando os projetos não concluíram totalmente o carregamento, evitando travamentos do Live Unit Testing. Melhorias no desempenho de build também evitam a reavaliação de projetos de MSBuild quando o sistema entende que nada foi alterado no arquivo de projeto.  

- **Diversos aprimoramentos na interface do usuário**: a opção confusa **Live Test Set – Incluir/Excluir** do gesto de clicar com o botão direito do mouse foi renomeada para **Incluir/Excluir Live Unit Testing**. A opção **Redefinir limpeza** no menu **Teste** > **Live Unit Testing** foi removida. Agora ela está acessível pela seleção de **Ferramentas** > **Opções** > **Live Unit Testing** e pela seleção de **Excluir Dados Persistidos**.

## <a name="whats-new-in-live-unit-testing-for-visual-studio-2017-version-153"></a>Novidades no Live Unit Testing para Visual Studio 2017 versão 15.3

Começando com o Visual Studio 2017 versão 15.3, o Live Unit Testing apresenta aprimoramentos e melhorias em duas áreas principais:

- Suporte para .NET Core e .NET Standard. Você pode usar o Live Unit Testing em soluções de .NET Core e .NET Standard, escritas em C# ou Visual Basic.
 
-  Melhorias de desempenho. Você notará que o desempenho está significativamente mais rápido após o primeiro build completo e a execução de testes no Live Unit Testing. Você também perceberá melhoria de desempenho significativa em inícios subsequentes do Live Unit Testing na mesma solução. Agora, nós persistimos os dados gerados pelo Live Unit Testing e os reutilizamos tanto quanto possível com verificações de estado de atualização. 
 
Além dessas importantes adições, o Live Unit Testing inclui as seguintes melhorias: 

- Um novo ícone de proveta agora é usado para distinguir um método de teste de métodos comuns. Um ícone de proveta vazio indica que o teste específico não está incluído no Live Unit Testing. 

- Ao clicar em um método de teste na janela pop-up da interface do usuário de um ícone do Live Unit Testing, agora você tem a opção de depurar o teste diretamente do contexto dentro da janela de interface do usuário e sem precisar deixar o editor de código. Isso é especialmente útil quando você se depara com um teste que falhou.  

- Várias opções adicionais configuráveis foram adicionadas a Ferramentas/Opções/Live Unit Testing/Geral. Você pode limitar a memória usada para o Live Unit Testing. Você também pode especificar o caminho do arquivo para os dados persistentes do Live Unit Testing para sua solução aberta. 

- Vários itens de menu adicionais foram incluídos na barra de menus do Teste/Live Unit Testing. **Redefinir Limpeza** exclui os dados persistentes e os gera novamente. **Opção** pula para Ferramentas/Opções/Live Unit Testing/Geral.
  
- Agora você pode usar os seguintes atributos para especificar o código-fonte que deseja excluir dos métodos de teste direcionados do Live Unit Testing:
   - Para xUnit: `[Trait("Category", "SkipWhenLiveUnitTesting")]`
   - Para NUnit: `[Category("SkipWhenLiveUnitTesting")]`
   - Para MSTest: `[TestCategory("SkipWhenLiveUnitTesting")]`

## <a name="see-also"></a>Consulte também
- [Introdução ao Live Unit Testing](live-unit-testing-intro.md)   
- [Live Unit Testing com o Visual Studio 2017](live-unit-testing.md)

