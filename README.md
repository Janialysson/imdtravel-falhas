# IMDTravel - Baseline (Parte 1.2) - Spring Boot

Projeto com 4 microserviços Spring Boot:
- imdtravel (orquestrador) - porta 8084
- airlineshub - porta 8081
- exchange - porta 8082
- fidelity - porta 8083

## Como usar

1. Buildar cada projeto com maven (ou usar uma IDE): No meu caso usei o Prompt de Comando do Windows para rodar cada MicroServiço, pois meu computador não tinha recurso suficientes para rodar no Docker. Basta seguir o passo a passo:
   ```
Passo 1
Precisa execultar o Prompt como administrador.
'''
Passo 2
Precisa indicar o caminho onde está o arquivo por exemplo:

cd "C:\Users\User\Downloads\imdtravel_baseline_multistage\imdtravel_baseline_multistage_falhas"
'''
Passo 3
Rodar cada comando dos Microserviço separadamente em um terminal:

cd C:\Users\User\Downloads\imdtravel_baseline_multistage\imdtravel_baseline_multistage_falhas\fidelity
mvn spring-boot:run

cd C:\Users\User\Downloads\imdtravel_baseline_multistage\imdtravel_baseline_multistage_falhas\exchange
mvn spring-boot:run

cd C:\Users\User\Downloads\imdtravel_baseline_multistage\imdtravel_baseline_multistage_falhas\imdtravel
mvn spring-boot:run

cd C:\Users\User\Downloads\imdtravel_baseline_multistage\imdtravel_baseline_multistage_falhas\airlineshub
mvn spring-boot:run
   ```

2. Ou usar Docker Compose (requer build dos jars ou imagem build com maven dentro do Dockerfile):
   ```
   docker compose up --build
   ```

3. Teste de compra (exemplo):
   ```
   curl -X POST "http://localhost:8080/api/buyTicket?flight=AB123&day=2025-10-25&user=1"
   ```

## Observações
- Cada serviço tem `application.properties` com a porta configurada.
- O timeout de 1s está aplicado no `RestTemplate` do `imdtravel`.
- Ajuste as versões do Spring Boot / Java no pom.xml conforme necessário.
- Lembre-se de que é necessário gerar os JARs (`mvn package`) para que o Dockerfile consiga copiar o `target/*.jar`.

## Tag para entrega
Após commitar tudo no repo, crie a tag BASELINE:
```
git tag BASELINE
git push origin BASELINE
```


### Versão com Docker Multi-Stage Build
Agora o projeto pode ser executado **sem precisar do Maven localmente**.
Para rodar tudo:

```
docker compose up --build
```
Isso compila os JARs dentro dos containers automaticamente.
