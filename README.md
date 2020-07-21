# Projeto Treinamento Descomplicando o Ansible

Projeto proposto como exercício do Treinamento Descomplicando o Ansible.

## Pré-Requisito

- Possuir Máquina linux com os seguintes pacotes instalados;
      
      - ansible
      - python
      - python-pip
      - boto3
      - botocore
- Possuir conta na AWS para criação das máquinas virtuais.
- Exportar as variáveis de ambiente com as suas credenciais na AWS:
```bash
  > export AWS_ACCESS_KEY_ID=****
  > export AWS_SECRET_ACCESS_KEY=*****
```

- Carregar a keypair para conexão via ssh nas máquinas da AWS. Ex.:
```bash
  > ssh-agent bash
  > ssh-add <keypair>
```

## Como usar

- 1ª Etapa: Criação das máquinas virtuais na AWS:

  Editar as variáveis *image, keypair* e *region*, contidas no arquivo *provisioning/roles/criando-instancias/vars/main.yml*, como no exemplo abaixo:

       image: ami-0b418580298265d5c
       keypair: ansible-class
       region: eu-central-1

  Entrar no diretório *provisioning* e executar o playbook lá contido:
```bash
  > ansible-playbook -i hosts main.yml
```
- 2ª Etapa: Instalar o *Kubernetes* e as ferramentas de monitoramento:

  Verificar no arquivo *hosts* do diretório *provisoning* que foram gravados diversos IPs públicos e privados das três máquinas criadas na AWS.

  Entrar no diretório *install_k8s* e editar o arquivo hosts. Escolher um par para ser de IPs (o primeiro IP público e o primeiro IP privado pertencem a mesma máquina, e assim sucessivamente) para a máquina que será o master do *Kubernetes*, colocar o IP público abaixo da marca *[k8s-master]* e o IP privado na variável *K8S_MASTER_NODE_IP*. Os outros dois IPs públicos devem ser inseridos abaixo da marca *[k8s-workers]*.

      [k8s-master]


      [k8s-workers]


      [k8s-workers:vars]
      K8S_MASTER_NODE_IP=
      K8S_API_SECURE_PORT=6443

  Executar o playbook contido no diretório *install_k8s*:
```bash
  > ansible-playbook -i hosts main.yml
```

- 3ª Etapa: Fazer o deploy da primeira versão da aplicação exemplo "giropops"

  Entrar no diretório *install_k8s* e copiar o arquivo hosts para o diretório *deploy-app-v1*.

  Executar o playbook contido no diretório *deploy-app-v1*:
```bash
  > ansible-playbook -i hosts main.yml
```

- 4ª Etapa: Fazer o deploy da segunda versão da aplicação exemplo "giropops"

  Entrar no diretório *install_k8s* e copiar o arquivo hosts para o diretório *deploy-app-v2*.

  Executar o playbook contido no diretório *deploy-app-v2*:
```bash
  > ansible-playbook -i hosts main.yml
```

## Contribuição
Exemplos dados pelo instrutor durante as vídeo aulas.
