---
title: Analisando a cobertura de código em testes de verificação de build | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 59c07d15-511e-4fd0-b398-bde9d5ed00d9
caps.latest.revision: 10
ms.author: gewarren
manager: douge
ms.openlocfilehash: b67986e42a914c73dea99f97611967aa6ee24097
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49905448"
---
# <a name="analyzing-code-coverage-in-build-verification-tests"></a>Analisando a cobertura de código em testes de verificação de build
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A análise de cobertura de código no Microsoft Visual Studio mostra quanto de seu código está sendo utilizado por testes automatizados. Para obter mais informações, consulte [Usando cobertura de código para determinar quanto código está sendo testado](../test/using-code-coverage-to-determine-how-much-code-is-being-tested.md).  
  
 Quando você faz check-in de seu código, os testes serão executados no servidor de compilação, juntamente com os outros testes de outros membros da equipe. (Se você ainda não tiver configurado isso, consulte [Executar testes no processo de build](http://msdn.microsoft.com/library/d05743a1-c5cf-447e-bed9-bed3cb595e38).) É útil analisar a cobertura de código no serviço de build, pois isso dá o panorama mais atualizado e mais abrangente da cobertura em todo o projeto. Também incluirá os testes automatizados do sistema e outros testes codificados que você normalmente não executa nos computadores de desenvolvimento.  
  
1. No Team Explorer, abra **Compilações** e adicione ou edite uma definição de build.  
  
2. Na página **Processo**, expanda **Testes Automatizados**, **Fonte de Teste**, **Configurações de Execução**. Defina **Tipo de Arquivo de Configurações de Execução** como **Cobertura de Código Habilitada**.  
  
    Se você tiver mais de uma definição de Fonte de Teste, repita essa etapa para cada uma.  
  
   - <em>Mas não há nenhum campo nomeado **tipo de arquivo de configurações de execução</em>*. *  
  
      Em **Testes Automatizados**, selecione **Assembly de Teste** e escolha o botão de reticências **[...]** no final da linha. Na caixa de diálogo **Adicionar/Editar Execução de Teste**, em **Test Runner**, selecione **Visual Studio Test Runner**.  
  
   ![Configurar a definição de build para cobertura de código](../test/media/codecoverage-plaincc.png "CodeCoverage plainCC")  
  
   Após a execução do build, os resultados da cobertura de código aparecem no resumo do build.  
  
## <a name="see-also"></a>Consulte também  
 [Usando cobertura de código para determinar quanto código está sendo testado](../test/using-code-coverage-to-determine-how-much-code-is-being-tested.md)



