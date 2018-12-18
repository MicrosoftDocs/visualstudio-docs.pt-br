---
title: Propriedades de formas de imagem | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.dsltools.dsldesigner.selectimagedialog
- vs.dsltools.dsldesigner.imageshape
helpviewer_keywords:
- Domain-Specific Language, image shape
ms.assetid: 9ce00ccd-07f2-4640-ac96-2a60481d0d72
caps.latest.revision: 27
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 9ea239fcdef2c9b2e5eccc82fd162e0b940bdf44
ms.sourcegitcommit: d462dd10746624ad139f1db04edd501e7737d51e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50219959"
---
# <a name="properties-of-image-shapes"></a>Propriedades de formas de imagem
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode usar formas de imagem para especificar como as classes de domínio são exibidos em um designer gerado. Definir uma forma de imagem, definindo o `Image` propriedade da classe para um arquivo de imagem predefinidos. Há suporte para os seguintes formatos:  
  
- .gif  
  
- .jpg  
  
- . JPEG  
  
- .bmp  
  
- .wmf  
  
- . emf  
  
- .png  
  
  Por padrão, os arquivos de recurso de designer, como arquivos de imagem, estão localizados na **recursos** pasta o **Dsl** projeto.  
  
  Para obter mais informações, consulte [como definir uma linguagem específica do domínio](../modeling/how-to-define-a-domain-specific-language.md). Para obter mais informações sobre como usar essas propriedades, consulte [personalizando e estendendo uma linguagem específica do domínio](../modeling/customizing-and-extending-a-domain-specific-language.md).  
  
  Formas de imagem têm as propriedades que são listadas na tabela a seguir.  
  
|Propriedade|Descrição|Padrão|  
|--------------|-----------------|-------------|  
|Cor de preenchimento|A cor de preenchimento desta forma.|Branco|  
|Modo de gradiente de preenchimento|O modo gradiente de preenchimento desta forma.|Horizontal|  
|Tem pontos de Conexão padrão|Se `True`, a forma usará superior, inferior, esquerda e pontos de conexão certa no designer gerado.|False|  
|Cor do contorno|A cor do contorno desta forma.|Preto|  
|Estilo de contorno tracejado|O estilo de contorno tracejado desta forma (sólido, traço, Dot, Traçoponto, Traçopontoponto ou personalizado).|Sólido|  
|Espessura do contorno|A espessura do contorno desta forma.|0.03125|  
|Cor do texto|A cor que é usada para os decoradores de texto que estão associados esta forma.|Preto|  
|Modificador de acesso|O modificador de acesso da forma geométrica (público ou interno).|Público|  
|Atributos personalizados|Usado para adicionar atributos à classe de código de origem que é gerado a partir desta forma.|\<Nenhum >|  
|Gera dupla derivado|Se `True`, serão geradas uma classe base e uma classe parcial (para dar suporte à personalização por meio de substituições). Para obter mais informações, consulte [substituindo e estendendo as Classes geradas](../modeling/overriding-and-extending-the-generated-classes.md).|False|  
|Tem um construtor personalizado|Se `True`, um construtor personalizado será fornecido no código-fonte. Para obter mais informações, consulte [substituindo e estendendo as Classes geradas](../modeling/overriding-and-extending-the-generated-classes.md).|False|  
|Modificador de herança|Descreve o tipo de herança da classe de código fonte que é gerado a partir a forma de imagem (`none`, `abstract` ou `sealed`).|nenhum|  
|Forma da imagem base|A classe base dessa forma.|(nenhum)|  
|Nome|O nome desta forma.|Nome atual|  
|Namespace|O namespace que é afiliado desta forma.|Namespace atual|  
|Tipo de dica de ferramenta|O local onde a dica de ferramenta é definida (fixo, variável ou nenhum). Se fixo, em seguida, o valor da `Fixed Tooltip Text` propriedade é usada como a dica de ferramenta; se a variável, em seguida, a dica de ferramenta é definida no código personalizado.|nenhum|  
|Observações|Observações informais associadas esta forma.|\<Nenhum >|  
|Altura inicial|A altura inicial desta forma em polegadas.|1|  
|Largura inicial|A largura inicial desta forma em polegadas.|1.5|  
|Cor de preenchimento expostos como propriedade<br /><br /> Modo de gradiente de preenchimento exposto<br /><br /> Exposto a cor do contorno como propriedade<br /><br /> Exposto o estilo de contorno tracejado como propriedade<br /><br /> Exposto como propriedade de espessura do contorno<br /><br /> Expõe a cor do texto|Se `True`, o usuário pode definir a propriedade indicada de uma forma. Para configurar isso, a definição de forma com o botão direito e clique em **adicionar exposto**.|False|  
|Descrição|Usado para documentar o designer gerado.|\<Nenhum >|  
|Nome de Exibição|O nome que será exibido no designer gerado para esta forma.|\<Nenhum >|  
|Texto de dica de ferramenta fixa|O texto que é usado para uma dica de ferramenta fixa.|\<Nenhum >|  
|Palavra-chave de ajuda|A palavra-chave que é usada para indexar a Ajuda de F1 para este elemento.|\<Nenhum >|  
|Image|O caminho para o arquivo de imagem que é usado para esta forma.|\<Nenhum >|  
  
## <a name="see-also"></a>Consulte também  
 [Glossário de ferramentas de linguagem específica do domínio](http://msdn.microsoft.com/en-us/ca5e84cb-a315-465c-be24-76aa3df276aa)



