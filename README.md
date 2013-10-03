#1 - Licença deste Documento

Para a utilização deste documento é necessário seguir as regras da licença Creative Commons pela mesma Licença 2.0 Brasil [](http://creativecommons.org/licenses/by-nc-sa/2.0/br/deed.pt_BR). 

Você tem a liberdade de:

![](https://raw.github.com/admin-softwarepublicobrasileiro/e-cidade/master/imagens/1.png) &nbsp; Compartilhar — copiar, distribuir e transmitir a obra.

![](https://raw.github.com/admin-softwarepublicobrasileiro/e-cidade/master/imagens/2.png) &nbsp; Remixar — criar obras derivadas.

Sob as seguintes condições:

![](https://raw.github.com/admin-softwarepublicobrasileiro/e-cidade/master/imagens/3.png) &nbsp; Atribuição — Você deve creditar a obra da forma especificada pelo autor ou licenciante (mas não de maneira que sugira que estes concedem qualquer aval a você ou ao seu uso da obra). 

![](https://raw.github.com/admin-softwarepublicobrasileiro/e-cidade/master/imagens/4.png) &nbsp; Compartilhamento pela mesma licença — Se você alterar, transformar ou criar em cima desta obra, você poderá distribuir a obra resultante apenas sob a mesma licença, ou sob uma licença similar à presente. 

Ficando claro que:
Renúncia — Qualquer das condições acima pode ser [renunciada](http://creativecommons.org/licenses/by-nc-sa/2.5/br/deed.pt_BR#) se você obtiver permissão do titular dos direitos autorais. 
Domínio Público — Onde a obra ou qualquer de seus elementos estiver em [domínio público](http://wiki.creativecommons.org/Public_domain) sob o direito aplicável, esta condição não é, de maneira alguma, afetada pela licença. 
Outros Direitos — Os seguintes direitos não são, de maneira alguma, afetados pela licença: 
Limitações e exceções aos direitos autorais ou quaisquer [usos livres](http://wiki.creativecommons.org/Frequently_Asked_Questions#Do_Creative_Commons_licenses_affect_fair_use.2C_fair_dealing_or_other_exceptions_to_copyright.3F) aplicáveis; 
Os [direitos morais](http://wiki.creativecommons.org/Frequently_Asked_Questions#I_don.E2.80.99t_like_the_way_a_person_has_used_my_work_in_a_derivative_work_or_included_it_in_a_collective_work.3B_what_can_I_do.3F) do autor; 
Direitos que outras pessoas podem ter sobre a obra ou sobre a utilização da obra, tais como [direitos de imagem](http://wiki.creativecommons.org/Frequently_Asked_Questions#When_are_publicity_rights_relevant.3F) ou privacidade. 
Aviso — Para qualquer reutilização ou distribuição, você deve deixar claro a terceiros os termos da licença a que se encontra submetida esta obra. A melhor maneira de fazer isso é com um link para esta página. 


#2 - Introdução ao Sistema e-cidade

O e-cidade destina-se a informatizar a gestão dos Municípios Brasileiros de forma integrada. Essa informatização contempla a integração entre os entes municipais: Prefeitura Municipal, Câmara Municipal, Autarquias, Fundações e outros.
A economia de recursos é somente uma das vantagens na adoção do e-cidade. Há liberdade de escolha dos fornecedores e garantia de continuidade do sistema, uma vez que é apoiado pelo Ministério do Planejamento. 

## 2.1 - Características 
O código fonte está disponível para ser baixado livremente no Portal do Software Público Brasileiro: www.softwarepublico.gov.br. 
O sistema possui a seguinte plataforma tecnológica:

LINUX
<br>APACHE – PHP</br>
<br>POSTGRESQL – PSQL</br>
<br>FPDF</br>
<br>AGATA – API</br>
<br>FIREFOX</br>
<br>HTML / CSS / JAVASCRIPT</br>
JAVA TOMCAT</br>
<br>ECLIPSE<br>

![](https://raw.github.com/admin-softwarepublicobrasileiro/e-cidade/master/imagens/5.png) &nbsp;


#3 - Instalação do Sistema

##3.1 - Informações gerais para instalação

É recomendado que este guia seja executado por um usuário com experiência em instalação de pacotes no Linux e configuração básica de Apache, PHP e PostgreSQL. 
Este roteiro está baseado no Sistema Operacional GNU/Linux Ubuntu 10.04 LTS. Cabe lembrar que em outras distribuições Linux o processo de instalação pode variar.
Este manual pressupõe que o servidor de aplicação Web e o banco de dados estarão instalados no mesmo servidor. 
Neste guia, sempre que necessário editar algum arquivo, será usado o editor de texto GEDIT. Mas cabe lembrar que é apenas uma opção, existem outros editores como o VIM.
  
#4 - Passo-a-passo da Instalação

##4.1 - Instalando e configurando o Servidor WEB Apache2

Para instalar o Apache2, execute o seguinte comando:
<br>`sudo apt-get install apache2`</br>

Agora é necessário alterar o arquivo /etc/apache2/apache2.conf. Usando o gedit, é possível editar as informações desse arquivo executando o comando:
<br>`sudo gedit /etc/apache2/apache2.conf`</br>

Altere o valor do parâmetro Timeout:
<br>`Timeout 12000`</br>

Além disso, adicione as seguintes linhas ao final desse arquivo:
<br>`# linhas adicionadas para o e-cidade`</br>
<br>`LimitRequestLine 16382`</br>
<br>`LimitRequestFieldSize 16382`</br>

Agora, altere o arquivo /etc/apache2/conf.d/charset. Usando o gedit faça assim:
<br>`sudo gedit /etc/apache2/conf.d/charset`</br>

Altere o valor do parâmetro AddDefaultCharset:
<br>`AddDefaultCharset ISO-8859-1`</br>

Caso a linha desse parâmetro esteja comentada, ou seja, iniciando com o caractere '#', remova este.

Deverá ser criada uma pasta de arquivos temporários. Crie a pasta “tmp” no DOCUMENT_ROOT do Apache (/var/www), da seguinte maneira:
<br>`sudo mkdir /var/www/tmp`</br>
<br>`sudo chown -R www-data.www-data /var/www/tmp`</br>
<br>`sudo chmod -R 777 /var/www/tmp`</br>

Adicione o usuário que irá administrar o e-cidade no grupo “www-data”. Esse usuário varia de acordo com sua instalação. No caso desse manual foi criado um usuário chamado “usuario1”. Deve-se editar o seguinte arquivo:
<br>`sudo gedit /etc/group`</br>

Adicione a seguinte linha (onde “usuario1” deve ser trocado pelo seu usuário criado na instalação do Ubuntu):
<br>`www-data:x:33:usuario1`</br>

##4.2 - Instalando o PHP 5

Execute o seguinte comando para instalar os pacotes necessários:
<br>`sudo apt-get install php5 php5-gd php5-pgsql php5-cli php5-mhash php5-mcrypt`</br>

Crie a pasta para os logs do PHP5:
<br>`sudo mkdir /var/www/log`</br>
<br>`sudo chown -R www-data.www-data /var/www/log`</br>

Agora é necessário editar o arquivo /etc/php5/apache2/php.ini:
<br>`sudo gedit /etc/php5/apache2/php.ini`</br>

Modifique os seguintes parâmetros:

`register_globals = On`
<br>`register_long_arrays = On`</br>
<br>`register_argc_argv = On`</br>
<br>`post_max_size = 64M`</br>
<br>`magic_quotes_gpc = On`</br>
<br>`upload_max_filesize = 64M`</br>
<br>`default_socket_timeout = 60000`</br>
<br>`max_execution_time = 60000`</br>
<br>`max_input_time = 60000`</br>
<br>`memory_limit = 512M`</br>
<br>`allow_call_time_pass_reference = On`</br>
<br>`error_reporting = E_ALL & ~E_NOTICE`</br>
<br>`display_errors = Off`</br>
<br>`log_errors = On`</br>
<br>`error_log = /var/www/log/php-scripts.log`(retirar o ponto e vírgula da frente da linha)</br> 
<br>`session.gc_maxlifetime = 7200`</br>

Caso a linha desses parâmetros estejam comentadas, ou seja, iniciando com o caractere '#', remova este.

## 4.3 - Instalando o PostgreSQL 8.2

Este será o banco de dados usado para armazenar as informações que serão usadas pelo software e-cidade. Para esta instalação será necessário baixar o PostgreSQL versão 8.2.
Para conseguir baixar essa versão, edite o arquivo /etc/apt/sources.list:
`sudo gedit /etc/apt/sources.list`

Acrescente a seguinte linha ao final do arquivo:

`deb http://br.archive.ubuntu.com/ubuntu hardy main universe`
  
Agora, para instalar o PostgreSQL 8.2 deve-se executar os seguintes comandos:

`sudo apt-get update`<br>
`sudo apt-get install postgresql-8.2`
  
**Configurando o Cluster.**

Cluster é o conjunto de banco de dados gerenciados por uma única instância (conjunto de datafiles, arquivos de controle e processos no servidor que formam um SGDB). Nessa instalação será usado o cluster do PostgreSQL 8.2 onde será instalado o e-cidade e encoding LATIN1(ISO-8859-1). Edite o arquivo /etc/postgresql/8.2/main/pg_hba.conf:

`sudo gedit /etc/postgresql/8.2/main/pg_hba.conf`

Altere as linhas no final do arquivo que estão sem o caractere '#', colocando “trust” no lugar da última coluna. Assim:
`local all all                trust`
<br>`host all all 127.0.0.1/32    trust`</br>
<br>`host all all ::1/128         trust`</br>
		
Recarregue as configurações do PostgreSQL:

`sudo /etc/init.d/postgresql-8.2 reload`
	
Verifique o cluster atual:

`psql -U postgres -hlocalhost -l`

Veja se o comando retorna o seguinte resultado:	

![](https://raw.github.com/admin-softwarepublicobrasileiro/e-cidade/master/imagens/6.png) &nbsp;

No caso acima precisamos recriar o cluster executando os próximos passos:

Remova o cluster atual:
<br>`sudo pg_dropcluster -stop 8.2 main`</br>
			
Crie o novo cluster como LATIN1:
<br>`sudo pg_createcluster -e LATIN1 8.2 main`</br>
	
Inicie o PostgreSQL:
<br>`sudo /etc/init.d/postgresql-8.2 start`</br>
		
Edite o arquivo /etc/postgresql/8.2/main/pg_hba.conf:
<br>`sudo gedit /etc/postgresql/8.2/main/pg_hba.conf`</br>

Altere as linhas no final do arquivo que estão sem o caractere '#', colocando “trust” no lugar da última coluna. Assim:
<br>`local all all                trust`</br>
<br>`host all all 127.0.0.1/32    trust`</br>
<br>`host all all ::1/128         trust`</br>
	
Recarregue as configurações do PostgreSQL:
<br>`sudo /etc/init.d/postgresql-8.2 reload`</br>

Novamente, verifique o encoding do cluster:
<br>`psql -U postgres -hlocalhost -l`</br>
		
![](https://raw.github.com/admin-softwarepublicobrasileiro/e-cidade/master/imagens/7.png) &nbsp;

***ATENÇÃO! Se o resultado do seu comando foi a tabela mostrada acima, pule os próximos passos, indo direto para a parte “Configurando o PostgreSQL 8.2”. Caso o resultado do comando seja algo diferente da tabela acima, então o sistema operacional instalado está sem suporte ao encoding LATIN1. Assim, será necessário realizar os passos abaixo:***

Edite o arquivo /var/lib/locales/support.d/local
<br>`sudo gedit /var/lib/locales/support.d/local`</br>

Adicione:
<br>`pt_BR.ISO-8859-1 ISO-8859-1`</br>

Edite o arquivo /etc/locale.alias:
<br>`sudo gedit /etc/locale.alias`</br>

Adicione: 
<br>`pt_BR pt_BR.ISO-8859-1`</br>

Reconfigure o locales:
<br>`</br>sudo dpkg-reconfigure locales`
<br>`export LANG=pt_BR.ISO-8859-1 `</br>
<br>`sudo pg_createcluster -e LATIN1 8.2 main`</br>

Inicie o servidor PostgreSQL:
<br>`sudo /etc/init.d/postgresql-8.2 start`</br>

Edite o arquivo /etc/postgresql/8.2/main/pg_hba.conf:
<br>`sudo gedit /etc/postgresql/8.2/main/pg_hba.conf`</br>

Altere as linhas ao final do arquivo que estão sem o caractere “#”, colocando “trust” no lugar da última coluna:
<br>`local all all                trust`</br>
<br>`host all all 127.0.0.1/32    trust`</br>
<br>`host all all ::1/128         trust`</br>
	
Recarregue as configurações do PostgreSQL:
<br>`sudo /etc/init.d/postgresql-8.2 reload`</br>

Verifique o encoding:
<br>`psql -U postgres -h localhost -l`</br>
	
O resultado deve ser o seguinte:

![](https://raw.github.com/admin-softwarepublicobrasileiro/e-cidade/master/imagens/8.png) &nbsp;

**Configurando o PostgreSQL 8.2**
É necessário modificar o arquivo postgresql.conf:
<br>`sudo gedit /etc/postgresql/8.2/main/postgresql.conf`</br>

Altere os seguintes parâmetros (o restante dos parâmetros ficam inalterados):

`max_fsm_pages = 81000 `
<br>`max_fsm_relations = 5000`</br>
<br>`checkpoint_segments = 16`</br>
<br>`redirect_stderr = on`</br> 
<br>`log_directory = 'pg_log'`</br> 
<br>`log_filename = 'postgresql-%Y-%m-%d_%H%M%S.log'`</br>
<br>`log_min_messages = warning`</br>
<br>`log_min_duration_statement = 5000 # 5 segundos`</br>
<br>`log_line_prefix = '%t [%p]: [%l-1] user=%u,db=%d'`</br>
<br>`autovacuum_naptime = 5min `</br>
<br>`autovacuum_vacuum_threshold = 50`</br>
<br>`autovacuum_analyze_threshold = 50 `</br>
<br>`autovacuum_vacuum_cost_delay = 20`</br>
<br>`add_missing_from = on `</br>
<br>`default_with_oids = on `</br>     
`escape_string_warning = off`

Caso a linha desses parâmetros estejam comentadas, ou seja, iniciando com o caractere '#', remova este.

Reinicie o PostgreSQL:
<br>`sudo /etc/init.d/postgresql-8.2 restart`</br>
	
Edite o arquivo /etc/postgresql/8.2/main/pg_hba.conf:
<br>`sudo gedit /etc/postgresql/8.2/main/pg_hba.conf`</br>

Alterar as linhas no final do arquivo que estão sem o caractere “#”, colocando “trust” no lugar da última coluna:
<br>`local all all                trust`</br>
<br>`host all all 127.0.0.1/32    trust`</br>
<br>`host all all ::1/128         trust`</br>
		
Recarregue as configurações do PostgreSQL:
<br>`sudo /etc/init.d/postgresql-8.2 reload`</br>

## 4.4 - Instalação do OpenOffice

Altere o arquivo sources.list:
<br>`sudo gedit /etc/apt/sources.list`</br>

Remova a seguinte linha que adicionamos no passo de instalação do 
PostgreSQL:
<br>`deb http://br.archive.ubuntu.com/ubuntu hardy main universe`</br>

Adicione a seguinte linha:
<br>`deb http://archive.canonical.com/ lucid partner`</br>

Atualize o repositório:
<br>`sudo apt-get update`</br>

Para instalar o OpenOffice basta executar:
<br>`sudo apt-get install openoffice.org-headless openoffice.org-java-common sun-java6-jre`</br>

Altere o arquivo /etc/rc.local/:
<br>`sudo gedit /etc/rc.local`</br>

Adicione o seguinte texto antes da linha que contém “exit 0”:
<br>`/usr/bin/soffice -accept="socket,host=localhost,port=8100;urp;" - nofirststartwizard -headless & exit 0`</br>

## 4.5 - Configuração do e-cidade
Nesse manual será instalada a versão 2.2.28 da solução, cujo pacote "e-cidade-2.2.28-linux.completo.tar.bz2" deverá ser baixado através do Portal do Software Público, comunidade e-cidade (use o pacote que está na pasta “Pacotes disponíveis” - em Armazenagem de Arquivos). Baixe o pacote e coloque na pasta /tmp.
Feito isso, acesse a pasta /tmp:

`cd /tmp` 
	
Extraia o pacote:

`sudo tar jxvf  e-cidade-2.2.28-linux.completo.tar-22075083.bz2`
	
**Criação da base de dados (chamaremos a base de "e-cidade").**

Acesse a seguinte pasta:

`cd e-cidade-2.2.28-linux.completo/sql/`

Crie o usuário dbportal do postgres:

`psql -U postgres -hlocalhost template1 -c "create role dbportal with superuser login password 'dbportal'"`

Crie o usuário dbseller do postgres: 

`psql -U postgres -h localhost template1 -c "create role dbseller with login password 'dbseller'"`

Execute o seguinte comando para criar o banco:

`createdb -U dbportal e-cidade`

Para importar os comandos. SQL de criação da estrutura de dados, execute:

`psql -U dbportal e-cidade -f e-cidade-demo-2.2.28.sql`

## 4.6 Disponibilização do e-cidade

Acesse o pacote e copie os arquivos do e-cidade para a pasta do Apache2:

`cd /tmp/e-cidade-2.2.28-linux.completo`

`sudo cp -r e-cidade /var/www`

Ajuste as permissões da pasta /var/www/e-cidade:

`sudo chown -R usuario1.www-data /var/www/e-cidade`

`sudo chmod -R 775 /var/www/e-cidade`

`sudo chmod -R 777 /var/www/e-cidade/tmp`

Lembre-se que “usuario1” varia de acordo com sua instalação e usuário utilizado.

Confira o arquivo de configuração da base de dados:

`sudo gedit /var/www/e-cidade/libs/db_conn.php` 

As variáveis devem estar da seguinte maneira:

`$DB_USUARIO = “dbportal”;`

`$DB_SENHA = “”; // Ou alguma senha, se foi definida para o usuário dbportal no postgresql` 

`$DB_SERVIDOR = “localhost”;`

`$DB_PORTA = “5432”;`

`$DB_PORTA_ALT = “5432”;` 

`$DB_BASE = “e-cidade”;`

## 4.7 - Acesso ao e-cidade

Se você optou por instalar o ambiente gráfico, então basta abrir o navegador Firefox e acessar o seguinte endereço:

`http://localhost/e-cidade`

Caso você tenha instalado o servidor sem ambiente gráfico, então apartir de um computador desktop abra o navegador Firefox e acesse o seguinte endereço:

`http://<ip_do_servidor>/e-cidade`

`Onde “ip_do_servidor” indica o entereço IP atribuído na instalação do servidor Ubuntu.`

Na tela de login do e-cidade informar o usuário “dbseller” e deixar a senha em branco.

`**ATENÇÃO! Para correto funcionamento do e-cidade, o Firefox deve estar com as janelas “pop-up” desbloqueadas para o IP do Servidor.**`

Compatibilidade das versões do Firefox:

O e-cidade é compatível com a versão 3.0 ou inferior do Mozilla Firefox.

Para tornar o e-cidade compatível com as demais versões do Firefox é necessário editar o seguinte arquivo:

`sudo gedit  /var/www/e-cidade/config/require_extensions.xml`

Onde está assim:

<browsers>
    <browser name='firefox' versao='1.5.*'></browser>
    <browser name='firefox' versao='2.0.*'></browser>
    <browser name='firefox' versao='3.0.*'></browser>
    <browser name='firefox' versao='3.1.*'></browser>
</browsers>

Deverá ficar da seguinte maneira:

<browsers>
    <browser name='firefox' versao='1.5.*'></browser>
    <browser name='firefox' versao='2.0.*'></browser>
    <browser name='firefox' versao='3.0.*'></browser>
    <browser name='firefox' versao='3.1.*'></browser>
    <browser name='firefox' versao='3.5.*'></browser>
    <browser name='firefox' versao='3.6.*'></browser>
    <browser name='msie' versao='6.0.*'></browser>
    <browser name='msie' versao='7.0.*'></browser>
    <browser name='msie' versao='8.0.*'></browser>
</browsers>

Reinicie o Apache:

`sudo /etc/init.d/apache2 restart`

##4.8 - Disponibilização do “e-cidade online”

O pacote e-cidadeonline é o serviço disponível ao cidadão.

Acesse o pacote onde estão os arquivos do e-cidade:

`cd /tmp/e-cidade-2.2.28-linux.completo`
	
Copie os arquivos do e-cidade online para a pasta do Apache2:

`sudo cp -r e-cidadeonline /var/www`
	
Ajuste as permissões da pasta:

`sudo chown -R usuario1.www-data /var/www/e-cidadeonline`

`sudo chmod -R 775 /var/www/e-cidadeonline`

`sudo chmod -R 777 /var/www/e-cidadeonline/tmp`

Confira o arquivo de configuração da base de dados:

`sudo gedit /var/www/e-cidadeonline/libs/db_conn.php`
	
As variáveis devem estar da seguinte maneira:

`$DB_INSTITUICAO = 1;`

`$DB_SENHA='; // Ou se for definida alguma senha para o usuario dbportal no postgresql`

`$DB_SERVIDOR = 'localhost';`

`$DB_PORTA= '5432';`

`$DB_BASEDADOS = 'e-cidade';`

Para acessar o e-cidade online, entre no seguinte endereço	:

`http://<ip_do_servidor>/e-cidadeonline`

#5 - Link da Licença Júridica Creative Commons
http://creativecommons.org/licenses/by-sa/2.0/br/legalcode
