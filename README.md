# 🛠 Dev Grafana | Como posso instalar o Grafana 8. 

Grafana é um aplicativo da web de análise de código aberto e visualização interativa multi-plataforma. <br>
Ele fornece tabelas, gráficos e alertas para a web quando conectado a fontes de dados compatíveis.

Grafana é um editor de gráficos e painel de métricas gratuito e de código aberto para várias fontes de dados;

#### ✅ Referências de dados

- Elasticsearch
- Graphite
- OpenTSDB
- Prometheus
- InfluxDB

### 🎲 Este guia irá guiá-lo através da instalação do Grafana no RHEL / CentOS 8.

O Grafana pode ser instalado no RHEL / CentOS 8 do repositório YUM ou baixando e instalando manualmente o pacote .rpm. </br>
O primeiro é o método preferido, pois é fácil atualizar e desinstalar o Grafana com o gerenciador de pacotes yum.

Alguns novos recursos do Grafana 8 são:

#### ✅ Painéis da biblioteca : </br>
Permitem que os usuários criem painéis que podem ser usados em vários painéis

#### ✅ Navegador de métricas Prometheus : </br>
Permite que você encontre rapidamente as métricas e selecione rótulos relevantes para construir consultas básicas.

#### ✅ Alertas do Grafana v8.0 : </br>
Centraliza as informações de alerta para alertas gerenciados pelo Grafana e alertas de fontes de dados compatíveis 
com o Prometheus em uma IU e API.

#### ✅ Streaming em tempo real : </br>
As fontes de dados agora podem enviar atualizações em tempo real para painéis por meio de uma conexão de websocket

#### ✅ Visualização do gráfico de barras : </br>
Uma nova visualização que suporta dados categóricos.

#### ✅ Visualização de histograma : </br>
Este recurso oculto do antigo painel Gráfico agora é uma visualização independente

#### ✅ Visualização da linha do tempo do estado : </br>
A visualização da linha do tempo do estado mostra mudanças discretas de estado ao longo do tempo
Visualização de séries temporais fora do Beta e agora está se transformando em um estado estável.

#### ✅ Baixar logs : </br>
Ao inspecionar um painel, agora você pode baixar os resultados do log como um arquivo de texto (.txt).

### 🛠 Etapa 1: Adicionar repositório Grafana 8 YUM
Execute os comandos abaixo como usuário com privilégios sudo ou como usuário root para adicionar conteúdo ao repositório.

cat <<EOF | sudo tee /etc/yum.repos.d/grafana.repo
[grafana]
name=grafana
baseurl=https://packages.grafana.com/oss/rpm
repo_gpgcheck=1
enabled=1
gpgcheck=1
gpgkey=https://packages.grafana.com/gpg.key
sslverify=1
sslcacert=/etc/pki/tls/certs/ca-bundle.crt
EOF

Você pode, opcionalmente, atualizar seu índice de cache para os pacotes disponíveis:

sudo dnf makecache

--

### 🛠 Etapa 2: Instale o Grafana 8 no CentOS 8 / RHEL 8
Quando o repositório do Grafana for configurado, o Grafana pode ser facilmente instalado executando os comandos abaixo:

sudo dnf -y install grafana

Informações do pacote:

rpm -qi grafana
Name        : grafana
Version     : 8.2.2
Release     : 1
Architecture: x86_64
Install Date: qui 21 out 2021 17:12:18 -03
Group       : default
Size        : 224404530
License     : "Apache 2.0"
Signature   : RSA/SHA256, qui 21 out 2021 07:10:03 -03, Key ID 8c8c34c524098cb6
Source RPM  : grafana-8.2.2-1.src.rpm
Build Date  : qui 21 out 2021 07:09:34 -03
Build Host  : 978da501e6f9
Relocations : /
Packager    : contact@grafana.com
Vendor      : Grafana
URL         : https://grafana.com
Summary     : Grafana
Description :
Grafana

--

### 🛠 Etapa 3: iniciar o serviço Grafana
O serviço Grafana é gerenciado pelo systemd. Inicie o serviço e habilite-o para iniciar na inicialização.

sudo systemctl enable --now grafana-server.service 
 
 Synchronizing state of grafana-server.service with SysV service script with /usr/lib/systemd/systemd-sysv-install.
 Executing: /usr/lib/systemd/systemd-sysv-install enable grafana-server
 Created symlink /etc/systemd/system/multi-user.target.wants/grafana-server.service → /usr/lib/systemd/system/grafana-server.service.

A porta padrão usada é 3000. 
Se você tiver outro processo usando esta porta, você precisará definir a porta personalizada no arquivo de 
configuração Grafana /etc/grafana/grafana.ini.

http_port = 3000

Seu grafana-serverserviço deve mostrar o estado de execução.

systemctl status grafana-server.service

● grafana-server.service - Grafana instance
   Loaded: loaded (/usr/lib/systemd/system/grafana-server.service; enabled; vendor preset: disabled)
   Active: active (running) since Thu 2021-10-21 17:13:10 -03; 35min ago
     Docs: http://docs.grafana.org
 Main PID: 26986 (grafana-server)
    Tasks: 12 (limit: 4518)
   Memory: 127.0M
   CGroup: /system.slice/grafana-server.service
           └─26986 /usr/sbin/grafana-server --config=/etc/grafana/grafana.ini --pidfile=/var/run/grafan>

out 21 17:13:10 grafana grafana-server[26986]: t=2021-10-21T17:13:10-0300 lvl=info msg="Registering plu>
out 21 17:13:10 grafana grafana-server[26986]: t=2021-10-21T17:13:10-0300 lvl=info msg="External plugin>
out 21 17:13:10 grafana grafana-server[26986]: t=2021-10-21T17:13:10-0300 lvl=info msg="Live Push Gatew>
out 21 17:13:10 grafana grafana-server[26986]: t=2021-10-21T17:13:10-0300 lvl=info msg="Writing PID fil>
out 21 17:13:10 grafana systemd[1]: Started Grafana instance.
out 21 17:13:10 grafana grafana-server[26986]: t=2021-10-21T17:13:10-0300 lvl=info msg="HTTP Server Lis>
out 21 17:16:09 grafana grafana-server[26986]: t=2021-10-21T17:16:09-0300 lvl=info msg="Request Complet>
out 21 17:16:19 grafana grafana-server[26986]: t=2021-10-21T17:16:19-0300 lvl=info msg="Successful Logi>
out 21 17:16:45 grafana grafana-server[26986]: t=2021-10-21T17:16:45-0300 lvl=info msg="Request Complet>
out 21 17:16:46 grafana grafana-server[26986]: t=2021-10-21T17:16:46-0300 lvl=info msg="Request Complet>
lines 1-20/20 (END)


Por padrão, o Grafana gravará logs no  diretório / var / log / 
grafana e seu banco de dados SQLite está localizado em/var/lib/grafana/grafana.db

--

### 🛠 Etapa 4: Abra a porta do firewall para Grafana
Se você tiver um serviço firewalld em execução, permita a porta  3000 de acesso ao painel da rede:

sudo firewall-cmd --add-port=3000/tcp --permanent
sudo firewall-cmd --reload

### 🛠 Etapa 5: Acesse o Grafana Dashboard
O painel da web do Grafana pode ser acessado em http://[Server IP|Hostname]:3000

Os logins padrão são:

username: admin
Password: admin

Altere a senha do administrador.

<h4 align="center"> 
	🚧 Tutorial de instalação 🚀 Em construção...  🚧
</h4>
