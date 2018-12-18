---
title: Validar o modelo UML | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- UML, constraints
- UML, validation
ms.assetid: deed5092-c11d-4431-a801-1e866a103075
caps.latest.revision: 12
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: fea958a20e5eee78f79f324ad19ef646f7920951
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51739966"
---
# <a name="validate-your-uml-model"></a>Validar o modelo UML
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Alguns dos modelos de UML que você pode desenhar no Visual Studio podem ser considerado inválido em seu projeto. Por exemplo, você pode exigir que um caso de uso sempre deve estar vinculado a um diagrama de sequência que tem linhas de vida que representam os atores do caso de uso. Você pode instalar ou definir *restrições* que ajudam sua equipe para atender aos requisitos como esse. As restrições podem ser aplicadas quando o usuário salva ou abre um modelo e pode ser invocado pelo comando de menu.  
  
 Não há restrições são fornecidas com [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], pois elas dependem de como sua equipe interpreta e usa modelos UML. Mas você pode definir suas próprias restrições e instalar as restrições que são definidas por outros usuários. Para saber como definir as restrições e empacotá-las para distribuição, consulte [definir restrições de validação para modelos UML](../modeling/define-validation-constraints-for-uml-models.md).  
  
## <a name="invoking-validation"></a>Invocando a validação  
 Quando você tiver instalado uma extensão de validação, as restrições que ele fornece podem ser aplicadas nos seguintes casos. Algumas restrições são definidas para aplicar em apenas alguns desses casos.  
  
- **Comando de validação.** Para invocar a validação a qualquer momento, clique em **validar modelo UML** sobre o **arquitetura** menu.  
  
  > [!NOTE]
  >  O comando será exibida apenas se as restrições de validação são instaladas.  
  
- **Sobre como salvar um modelo.** Restrições de validação podem ser aplicadas quando você salvar o modelo. A finalidade dessas restrições é certificar-se de que você não salvar um modelo que é inválido de acordo com a interpretação do seu projeto.  
  
   Se houver erros, você será solicitado se você ainda deseja salvar o modelo. Você pode escolher para corrigir os erros ou para salvar o modelo de qualquer forma.  
  
- **Como abrir um modelo.** Quando você abre um modelo, os métodos de validação podem ser aplicados para restaurar as mensagens de erro que existia quando você salva o modelo. Erros também podem ser introduzidos por inconsistências entre as alterações feitas por usuários que trabalham em diferentes partes de um modelo. Para obter mais informações, consulte [compartilhar modelos e diagramas de exportação](../modeling/share-models-and-exporting-diagrams.md).  
  
  Erros de validação são relatados no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] janela de erros.  
  
  Para selecionar os elementos que estão incorretos em um diagrama, clique duas vezes no erro. Isso só funcionará se os elementos incorretos são visíveis em um diagrama aberto.  
  
## <a name="installing-validation-constraints"></a>Instalando as restrições de validação  
 Restrições são empacotadas em [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] arquivos VSIX (extensão). Normalmente, um conjunto de restrições fará parte de uma extensão que também contém outras definições, como comandos de menu, perfis e itens de caixa de ferramentas.  
  
#### <a name="to-install-a-visual-studio-extension"></a>Para instalar uma extensão do Visual Studio  
  
1.  Clique duas vezes o **VSIX** arquivo no Windows Explorer (ou Explorador de arquivos).  
  
2.  Reiniciar qualquer instância do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] que já está em execução.  
  
## <a name="disabling-and-uninstalling-validation-constraints"></a>Desabilitar e desinstalar as restrições de validação  
 Quando você quiser trabalhar com um modelo ao qual as restrições não se aplicam, você pode desativar temporariamente a extensão de que os contém. Dessa forma, você pode trabalhar com diferentes tipos de modelo em momentos diferentes, habilitando e desabilitando extensões diferentes.  
  
#### <a name="to-disable-or-uninstall-a-visual-studio-extension"></a>Para desabilitar ou desinstalar uma extensão do Visual Studio  
  
1.  Sobre o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] **ferramentas** menu, clique em **extensões e atualizações**.  
  
2.  Junto com a extensão, clique em **desabilitar** para desabilitar temporariamente a extensão. Você pode habilitá-la novamente mais tarde, retornando para o **extensões e atualizações** janela.  
  
     \- ou -  
  
     Clique em **desinstalação** para remover a extensão.  
  
3.  Reinicie o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Definir restrições de validação para modelos UML](../modeling/define-validation-constraints-for-uml-models.md)   
 [Criar modelos para seu aplicativo](../modeling/create-models-for-your-app.md)   
 [Usar modelos no processo de desenvolvimento](../modeling/use-models-in-your-development-process.md)



