# -Implementando-sua-Primeira-Stack-com-AWS-CloudFormation-
Repositório organizado contendo anotações e insights adquiridos durante a prática - Implementando sua Primeira Stack com AWS CloudFormation

🚀 Resumo rápido — O que é o AWS CloudFormation

O AWS CloudFormation é um serviço que permite modelar, provisionar e gerenciar recursos AWS usando arquivos de infraestrutura como código (IaC). Com templates (JSON ou YAML) você descreve os recursos desejados e o CloudFormation cria, atualiza e remove esses recursos de forma automatizada e reprodutível.

Principais vantagens:

Reprodutibilidade e versionamento da infra (IDEAL para GitHub).

Automatização de deploys e rollbacks.

Controle de dependências entre recursos.

Boas práticas: modularizar templates, usar parâmetros e outputs.

✅ Estrutura do material neste arquivo

Passo a passo: criando Stacks via Console.

Passo a passo: criando Stacks via AWS CLI (aws cloudformation deploy).

Template exemplo: simple-vpc.yaml (iniciantes).

Template exemplo: firewall-nacl-sg.yaml (exemplo de "firewall" usando NACL + Security Group).

Template referência: network-firewall-skeleton.yaml (esqueleto para AWS Network Firewall — avançado).

1) Passo a passo — Criando uma Stack pelo Console (iniciante)

Faça login no AWS Management Console e abra o serviço CloudFormation.

Clique em Create stack → With new resources (standard).

Em Specify template, escolha Upload a template file e selecione o arquivo simple-vpc.yaml (ou cole o conteúdo em Template source).

Clique em Next.

Preencha Stack name (ex: my-simple-vpc) e os valores dos parâmetros (se houver).

Avance pelos steps (opcional: tags, permissions — verifique o IAM role se necessário).

Clique em Create stack.

Acompanhe o progresso na aba Events; quando o status virar CREATE_COMPLETE a stack estará pronta.

Dica: se ocorrer erro, leia a aba Events para identificar qual recurso falhou e por quê.

2) Passo a passo — Criando/atualizando uma Stack com AWS CLI

Requisitos: awscli configurado (aws configure) com credenciais e região corretas.

Comando recomendado (mais simples, faz create ou update) - Disponível na pasta - 

Explicação:

--template-file : caminho para o YAML/JSON.

--stack-name : nome amigável da stack.

--parameter-overrides : sobrescreve parâmetros do template.

--capabilities : necessário se o template cria recursos IAM (ex: roles, policies).

Para deletar a stack:
aws cloudformation delete-stack --stack-name my-simple-vpc

3) Template exemplo — simple-vpc.yaml

Template YAML educacional que cria uma VPC, 2 subnets públicas, Internet Gateway e rotas básicas. Disponível na pasta - 

4) Template exemplo — firewall-nacl-sg.yaml (exemplo de "firewall" com NACL + Security Group)

Observação: este exemplo demonstra controles de borda e instância usando Network ACLs (NACLs) e Security Groups. Não é o AWS managed Network Firewall — que é um serviço mais avançado (há um esqueleto abaixo). Disponível na pasta - 

5) Template referência — network-firewall-skeleton.yaml (AWS Network Firewall — avançado)

Nota: o AWS Network Firewall é um serviço gerenciado distinto. Templates prontos são maiores (policy, rule groups, logging, role). Abaixo tem um esqueleto mínimo que cria um FirewallPolicy + Firewall — é provável que você precise customizar rule groups e permissões. Disponível na pasta - 

⚠️ Atenção: o template acima é um ponto de partida. Para um deploy completo em produção será necessário:

Definir RuleGroups (stateless e/ou stateful) com regras IPS/IDS/Suricata ou regras baseadas em conjunto de endereços.

Criar LoggingConfiguration caso queira logs para S3/CloudWatch.

Garantir que as subnets usadas estejam nas rotas e arquiteturas corretas (em arquiteturas com Transit Gateway / inspection VPC etc.).

Todas as informações foram extraídas do curso Code Girls, e da internet

📅 Última atualização: 30 de Outubro de 2025
