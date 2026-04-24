# Desafio DevSecOps — Gerenciador de Tarefas

https://github.com/ueavila1/projeto-devsecops-desafio

## Sobre o Projeto
Este repositório faz parte do desafio prático do módulo de DevSecOps da ADA Tech.


## Missão
1. Implementar os steps de segurança no `pipeline.yml`
2. Fazer a pipeline **quebrar** ao detectar os problemas
3. Corrigir as vulnerabilidades encontradas
4. Fazer a pipeline **passar** com tudo verde ✅
5. Documentar o funcionamento da pipeline neste README

## O que implementar
- [ ] Secrets Scanning com **Gitleaks**
- [ ] SAST com **Semgrep**
- [ ] SCA com **Grype**
- [ ] Deploy com **GitHub Pages**

## Como a pipeline funciona

 1. Checkout do Código 

    O que faz: Cria uma cópia local do código do seu repositório dentro da máquina virtual do GitHub Actions.

    Importância para a segurança: É a base de confiança. Garante que as ferramentas de análise trabalhem exatamente sobre a versão do código que foi enviada (push), permitindo uma auditoria precisa do que está prestes a ir para produção.

2. Build (Verificação de Integridade)

    O que faz: Valida se a estrutura de pastas e arquivos necessários (neste caso, em src/) está presente e acessível.

    Importância para a segurança: Atua como um "filtro de sanidade". Garante que a pipeline não processe um código corrompido ou incompleto, o que poderia causar comportamentos inesperados ou "buracos" nas análises de segurança subsequentes.

3. Secrets Scanning (Gitleaks)

    O que faz: Varre todo o código e o histórico de commits em busca de segredos expostos, como chaves de API, senhas, tokens de banco de dados ou certificados.

   Importância para a segurança: Crítica. Evita o vazamento de credenciais que permitiriam a um invasor acessar a infraestrutura. Uma vez que um segredo é commitado, ele fica no histórico; o Gitleaks detecta isso antes que o código chegue ao servidor.

4. SAST - Static Application Security Testing (Semgrep)

    O que faz: Analisa o código-fonte sem executá-lo, procurando por padrões de programação inseguros (ex: injeção de SQL, uso de funções perigosas ou configurações de criptografia fracas).

   Importância para a segurança: Identifica vulnerabilidades de lógica criadas pelo desenvolvedor. O Semgrep ajuda a manter o padrão de "Clean Code" focado em segurança, corrigindo erros antes mesmo do software rodar.

5. SCA - Software Composition Analysis (Grype)

    O que faz: Analisa as bibliotecas e dependências de terceiros que o projeto utiliza, comparando-as com bancos de dados de vulnerabilidades conhecidas (CVEs).

   Importância para a segurança: Essencial, pois a maioria dos ataques modernos foca em falhas em bibliotecas externas e não no código original. O parâmetro --fail-on medium garante que nenhuma dependência com vulnerabilidade séria seja ignorada.

6. Configuração e Deploy

    O que faz: Prepara o ambiente e publica o conteúdo da pasta src/ na web.

    Importância para a segurança: Esta etapa só acontece se todos os passos anteriores passarem (sucesso absoluto). Isso garante que o que está "no ar" é um código limpo, testado e livre de segredos expostos, implementando o conceito de Gate de Segurança.

## URL de Produção
> https://ueavila1.github.io/projeto-devsecops-desafio/
