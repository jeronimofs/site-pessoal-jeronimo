---
layout: post
title: "Utilizando e-mail assinado e criptografado com S/MIME"
---
Para garantir a privacidade de seus e-mails, além de usar uma senha segura e um provedor de e-mail confiável, é extremamente importante a utilização de criptografia ponta-a-ponta; esse tipo de processo garante que só você e o remetente/destinatário tem acesso ao conteúdo da mensagem. Qualquer outra entidade (pessoa, empresa, governo, etc) que obtiver uma cópia da mensagem não poderá ler o conteúdo, pois ele estará “embaralhado”. Nem mesmo o provedor do e-mail terá acesso ao conteúdo. O conteúdo é criptografado em seu dispositivo (computador, smartphone, tablet, etc), e descriptografado no dispositivo do destinatário.

Adicionalmente, é conveniente assinar digitalmente os seus e-mails. Isso garante ao seu destinatário que o seu e-mail realmente partiu de você, e vice-versa.

## Tecnologias existentes

Há duas formas bastante conhecidas de criptografar e assinar e-mails: o PGP e o S/MIME.

No PGP, você cria um par de chaves pública e privada, onde a privada é protegida por uma senha, que deve ser digitada cada vez que você a utiliza. Você distribui a sua chave pública para seus contatos, assim eles podem enviar e-mails criptografados para você, bem como saber que e-mails enviados por você são realmente seus (mediante assinatura do e-mail). A garantia de que uma chave pertence realmente a uma pessoa não é regulada por nenhuma entidade, mas sim por um conceito de rede de confiança, onde as chaves públicas validadas por contatos nos quais você confia tornam-se também confiáveis por transitividade. Para utilizar o PGP, é necessário instalar um software para manipulação das chaves, bem como é necessário instalar uma extensão em seu cliente de e-mail que dê suporte ao PGP (às vezes, algumas extensões fazem os dois papéis: gerar as chaves e criptografar os e-mails). Outra coisa que é obrigatória é utilizar um cliente de e-mail instalado no seu dispositivo (Thunderbird, Outlook para Desktop, aplicativo de e-mail do seu smartphone, etc). Se você utiliza um webmail, o Mailvelope suporta alguns dos webmails mais famosos.

Já no S/MIME, a configuração e utilização é bem mais fácil que o PGP. Você cria um par de chaves pública e privada que será endossada por uma autoridade certificadora acreditada mundialmente. A geração da chave segue um processo que garante que só o dono de uma conta de e-mail pode gerar a chave; ainda, por ser endossada por uma autoridade certificadora, é automaticamente aceita em qualquer cliente com suporte ao S/MIME. É obrigatória a utilização de um cliente de e-mail instalado em seu dispositivo (como o Thunderbird, Outlook para Desktop, ou o aplicativo de e-mail do seu smartphone). Entretanto, os clientes de e-mail mais populares já tem suporte nativo ao S/MIME, o que garante uma adoção mais fácil do que o PGP. A geração das chaves é feita no site da autoridade certificadora, logo, não é necessário instalar um software adicional para isso. Ainda, mesmo que seu destinatário não utilize S/MIME, você pode enviar um e-mail assinado (mas não criptografado), e o cliente de e-mail dele saberá reconhecer a assinatura, e exibir uma notificação de acordo. Até onde conheço, não é possível utilizar S/MIME com webmails.

Neste artigo, você aprenderá gerar um certificado S/MIME gratuito e endossado por uma autoridade certificadora acreditada mundialmente, e instalar ele em seu cliente de e-mail (utilizaremos o Thunderbird como exemplo).

## Gerando o certificado S/MIME

Atualmente, a única autoridade certificadora que fornece certificados S/MIME para e-mails gratuitamente é a Actalis, da Itália. [Você pode solicitar o seu certificado no site deles](https://actalis.it/), e o certificado virá por e-mail. Siga o processo que é descrito no site (em inglês).

Assim que você receber o e-mail que contém o certificado, abra o arquivo anexo (é o certificado), e siga as instruções do seu dispositivo para instalá-lo. Guarde este arquivo para instalar sua chave em todos os dispositivos que você utiliza para enviar e-mails.

## Clientes que suportam o S/MIME

Há diversos clientes que suportam o S/MIME por padrão. Vale a pena mencionar alguns:

- Para desktop
    - Thunderbird
    - Outlook
    - Evolution
    - Apple Mail App (aplicativo padrão de e-mail do Mac)
- Para Android
    - R2Mail2
- Para iOS
    - Apple Mail App (aplicativo padrão de e-mail do iPhone/iPad)

## Conclusão

A assinatura e criptografia via S/MIME é de fácil configuração e tem ampla aceitação pelos clientes de e-mail. Ela garante a proveniência das mensagens, e quando ambas as pontas da comunicação (remetente e destinatário) usam, sua privacidade é garantida pela criptografia de ponta a ponta. Em tempos de vigilância digital em massa, é muito conveniente que todos protejam os seus dados pessoais, ainda mais com ferramentas de padrões abertos e reconhecidos.