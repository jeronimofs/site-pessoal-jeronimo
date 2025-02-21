---
layout: post
title: "Instalando Phalcon Framework no Debian 8 64 bits"
---
O Phalcon é um Framework PHP de alto desempenho, pois ele é uma extensão compilada do PHP. Assim, suas classes residem já na memória do PHP por padrão, não sendo carregadas por interpretação de arquivos PHP. Isso nos provê um altíssimo desempenho e menor consumo de memória.

Este guia nos mostra como instalar o Phalcon em 5 minutos em sua máquina Debian 8 64 bits.

- Atualize seus repositórios

```
sudo apt-get update

```

- Instale os pacotes necessários à compilação e utilização da extensão

```
sudo apt-get install php5-dev libpcre3-dev gcc make php5-mysql git

```

- Inicie a compilação do pacote

```
cd /opt sudo git clone –depth=1 git://github.com/phalcon/cphalcon.git cd cphalcon/build sudo ./install

```

- Aguarde o fim da compilação

```
Thanks for compiling Phalcon! Build succeed: Please restart your web server to complete the installation

```

- Crie os arquivos de carregamento da extensão

```
sudo printf “; configuration for phalcon module\n; priority=50\nextension=phalcon.so” > /etc/php5/cli/conf.d/50-phalcon.ini 
sudo printf “; configuration for phalcon module\n; priority=50\nextension=phalcon.so” > /etc/php5/apache2/conf.d/50-phalcon.ini

```

- Crie um arquivo phpinfo para conferir se a extensão será carregada

```
sudo printf “<?php\nphpinfo();” > /var/www/html/phpinfo.php

```

- Reinicie o apache

```
sudo service apache2 restart

```

Carregue no seu navegador o phpinfo na URL http://localhost/phpinfo.php

Se apareceu o phalcon na página do phpinfo, pronto! Sua instalação está pronta e rodando corretamente.