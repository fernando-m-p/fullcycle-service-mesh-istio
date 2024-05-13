# FullCycle 3.0 - Service Mesh com Istio

## Andamento do curso

- [x] Docker
- [x] Padrões e técnicas avançadas com Git e Github
- [x] Integração contínua
- [x] Kubernetes
- [x] **Service Mesh com Istio**
- [ ] API Gateway
- [ ] API Gateway com Kong e Kubernetes
- [ ] Observabilidade
- [ ] Introdução a OpenTelemetry
- [ ] Terraform
- [ ] Ansible
- [ ] GitOps
- [ ] Deploy nas Cloud Providers
- [ ] Fundamentos da arquitetura de software
- [ ] Comunicação entre sistemas
- [ ] SOLID Express
- [ ] Domain Driven Design
- [ ] DDD: Modelagem Tática e Patterns
- [ ] Event Storming na Prática
- [ ] Arquitetura hexagonal
- [ ] Clean Architecture
- [ ] Sistemas monolíticos
- [ ] Arquitetura baseada em microsserviços
- [ ] EDA - Event Driven Architecture
- [ ] RabbitMQ
- [ ] Apache Kafka
- [ ] Autenticação e Keycloak
- [ ] Arquitetura do projeto prático - Codeflix
- [ ] Projeto prático - Java (Back-end)
- [ ] Projeto prático CodeFlix - React (Front-end)
- [ ] Projeto prático Admin CodeFlix - React (Front-end)
- [ ] Microsserviços de Encoder de Vídeo com Go Lang
- [ ] Microsserviços: API do Catálogo com Java (Back-end)
- [ ] MIcrosserviços: Assinaturas com Java (Back-end)

**Service Mesh** ou Malha de Serviços é uma camada extra adicionada junto ao seu cluster visando monitorar e modificar em tempo real o tráfego das aplicações, bem como elevar o nível de segurança e confiabilidade de todo o ecossistema.

**Istio** é um projeto open-source que implementa service mesh visando diminuir a complexidade no gerenciamento de aplicações distribuídas independente de qual linguagem ou tecnologia elas foram desenvolvidas.

O Istio pode rodar junto com:
- kubernetes [(Página Oficial)](https://kubernetes.io/)
- ApacheMesos [(Página Oficial)](https://mesos.apache.org/)
- Consul [(Página Oficial)](https://www.consul.io/)
- Nomad [(Página Oficial)](https://www.nomadproject.io/)

Principais recursos com o trabalho de Service Mesh e com o Istio:
- Gerenciamento de tráfego
    - Gateways (entrada e saída)
    - Load Balancing
    - Timeout
    - Políticas de retry
    - Circuit Breaker
    - Fault Injection
- Observabilidade
    - Métricas
    - Traces distribuídos
    - Logs
- Segurança
    - Man-in-the-middle
    - mTLS (mutual TLS)
    - AAA (authentication, authorization e audit)

## 1.0 Instalação

### 1.1 k3d [(Site Oficial)](https://k3d.io/v5.6.3/)

Seguindo o passo a passo no site oficial do k3d não obtive problema.

Lembrando que o `k3d é um wrapper leve para executar k3s (distribuição kubernetes mínima do Rancher Lab) no docker.` há outros, foi uma decisão do ministrante do curso.

#### 1.1.1 criando o cluster

```shell
    k3d cluster create -p "8000:30000@loadbalancer" --agents 2
```

### 1.2. Istio [(Site Oficial)](https://istio.io/)

Baixar o Istio

```shell    
    curl -L https://istio.io/downloadIstio | sh -
```

Mover para uma pasta eu escolhi a /opt

```shell
    sudo mv istio-X.X.X/ /opt
```

e configurar a variável de ambiente:

```shell
    export PATH=/opt/istio-X-X-X/bin:$PATH
```

Após instalar, para utilizar o Isitio no cluster


```shell
    istioctl install --set profile=default -y
    kubectl label namespace default istio-injection=enabled
```



### Configurando addons


Na página de documentação do Istio tem algumas ferramentas de integração para monitoramento do seu Service Mesh

Foi adicionado no cluster as ferramentas:

- Prometheus : `kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.21/samples/addons/prometheus.yaml`
- Kiali: `kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.21/samples/addons/kiali.yaml`
- Jaeger: `kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.21/samples/addons/jaeger.yaml`
- Grafana: `kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.21/samples/addons/grafana.yaml`



