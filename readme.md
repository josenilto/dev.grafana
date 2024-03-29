## 🛠 Dev Grafana | Instalação e configuração o Grafana 8.2.6 

Grafana é um aplicativo da web de análise de código aberto e visualização interativa multi-plataforma. <br>
Ele fornece tabelas, gráficos e alertas para a web quando conectado a fontes de dados compatíveis.

> Grafana é um editor de gráficos e painel de métricas gratuito e de código aberto para várias fontes de dados;


Este comando é um comando shell que baixa e executa um script para instalar o Docker em seu sistema.   
O script detectará o sistema operacional e instalará a versão apropriada do Docker para esse sistema.

```bash
curl -fsSl https://get.docker.com |sh
```

```bash
sudo apt  install docker-compose
```

```bash
docker compose version
```


✅**Mantenha seu servidor atualizado ;**

```Atualização
yum update -y && yum upgrade -y
```

✅ **Referências de dados;**

- [x] Elasticsearch
- [x] Graphite
- [x] OpenTSDB
- [x] Prometheus
- [x] InfluxDB

### 🎲 **Este guia irá guiá-lo através da instalação do Grafana no RHEL / CentOS 8.**

O Grafana pode ser instalado no RHEL / CentOS 8 do repositório YUM ou baixando e instalando manualmente o pacote .rpm.  
O primeiro é o método preferido, pois é fácil atualizar e desinstalar o Grafana com o gerenciador de pacotes yum.

> Alguns novos recursos do Grafana 8 são:

✅ **Painéis da biblioteca ;**  
Permitem que os usuários criem painéis que podem ser usados em vários painéis

✅ **Navegador de métricas Prometheus ;**  
Permite que você encontre rapidamente as métricas e selecione rótulos relevantes para construir consultas básicas.

✅ **Alertas do Grafana v8.0 ;**  
Centraliza as informações de alerta para alertas gerenciados pelo Grafana e alertas de fontes de dados compatíveis 
com o Prometheus em uma IU e API.

✅ **Streaming em tempo real ;**  
As fontes de dados agora podem enviar atualizações em tempo real para painéis por meio de uma conexão de websocket

✅ **Visualização do gráfico de barras ;**  
Uma nova visualização que suporta dados categóricos.

✅ **Visualização de histograma ;**  
Este recurso oculto do antigo painel Gráfico agora é uma visualização independente

✅ **Visualização da linha do tempo do estado ;**  
A visualização da linha do tempo do estado mostra mudanças discretas de estado ao longo do tempo
Visualização de séries temporais fora do Beta e agora está se transformando em um estado estável.

✅ **Baixar logs ;**  
Ao inspecionar um painel, agora você pode baixar os resultados do log como um arquivo de texto (.txt).


🛠 **Etapa 1 :** Adicionar repositório Grafana 8 YUM  
Execute os comandos abaixo como usuário com privilégios **`sudo`** ou como usuário **`root`** para adicionar conteúdo ao repositório.

```bash
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
```

Você pode, opcionalmente, atualizar seu índice de cache para os pacotes disponíveis:

```
sudo dnf makecache
```


🛠 **Etapa 2 :** Instale o Grafana 8 no CentOS 8 / RHEL 8  
Quando o repositório do Grafana for configurado, o Grafana pode ser facilmente instalado executando os comandos abaixo:

```install
sudo dnf -y install grafana
```

Informações do pacote:

```info
rpm -qi grafana
```

🛠 **Etapa 3 :** iniciar o serviço Grafana  
O serviço Grafana é gerenciado pelo systemd.  
Inicie o serviço e habilite-o para iniciar na inicialização.

```service
sudo systemctl enable --now grafana-server.service
```

A porta padrão usada é **`3000`**. 
Se você tiver outro processo usando esta porta, você precisará definir a porta personalizada no arquivo de 
configuração Grafana **`/etc/grafana/grafana.ini`**.

**`http_port = 3000`**

Seu grafana-serverserviço deve mostrar o estado de execução.

```service
systemctl status grafana-server.service
```

Por padrão, o Grafana gravará logs no  diretório **`/var/log/`** 
grafana e seu banco de dados SQLite está localizado em **`/var/lib/grafana/grafana.db`**


🛠 **Etapa 4 :** Abra a porta do firewall para Grafana.</br>
Se você tiver um serviço firewalld em execução, permita a porta **`3000`** de acesso ao painel da rede:

```bash
sudo firewall-cmd --permanent --add-service=grafana

sudo firewall-cmd --permanent --remove-service=dhcpv6-client
sudo firewall-cmd --permanent --remove-service=cockpit

sudo firewall-cmd --reload
sudo firewall-cmd --list-all 
```
```cockipt
sudo rm -f /etc/motd.d/cockpit
```
🛠 **Etapa 5 :** Acesse o Grafana Dashboard.  
O painel da web do Grafana pode ser acessado em **`http://[Server IP|Hostname]:3000`** 

Os logins padrão são:

Username: **`admin`**  
Password: **`admin`**

Altere a senha do administrador.


#### ➡️ Links:

[<img title="Grafana" align="left" alt="josenilto | Twitter" width="28px" src="https://cdn.jsdelivr.net/npm/simple-icons@v3/icons/grafana.svg" />][grafana]
[<img title="Grafana Labs" align="left" alt="josenilto | Twitter" width="28px" src="https://raw.githubusercontent.com/iconic/open-iconic/master/svg/globe.svg" />][website]

[Grafana]: https://grafana.com
[Website]: https://grafana.com/grafana/


<h4 align="center"> 
	🚧 Tutorial de instalação 🚀 Em construção...  🚧	
</h4>
