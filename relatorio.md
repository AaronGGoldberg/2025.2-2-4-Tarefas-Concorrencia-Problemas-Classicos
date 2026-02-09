# Relatório - Jantar dos Filósofos em Python

## Contexto inicial do trabalho (introdução)
O objetivo desta atividade é implementar o Problema do Jantar dos Filósofos utilizando threads em um único processo. O problema é um clássico de concorrência e mostra a necessidade de sincronização ao acessar recursos compartilhados (talheres) sem a presença de um coordenador central.

## Descrevendo a solução em python para o jantar dos filósofos

### Implementando o algoritmo

#### Qual o algoritmo utilizado
A solução utiliza o algoritmo de **ordenação de recursos por paridade**: filósofos com ID par pegam primeiro o talher da esquerda e depois o da direita, enquanto filósofos ímpares fazem o inverso. Essa inversão de ordem elimina a condição de espera circular, prevenindo deadlock.

#### Implementação do algoritmo em python
A implementação cria 5 threads (uma por filósofo) e 5 locks (um por talher). Cada filósofo executa o ciclo **pensar → pegar talheres → comer → devolver talheres** até atingir um número máximo de refeições.

### Tratando impasse

#### Qual a estratégia de tratamento de impasses
O tratamento de impasses é feito pela **prevenção de deadlock**, quebrando a condição de espera circular por meio da ordenação de aquisição dos recursos (talheres) baseada na paridade do filósofo.

#### Implementação do tratamento de impasse em python
No método `pegar_talheres`, a ordem de aquisição dos locks muda conforme o ID do filósofo. Isso garante que não exista um ciclo em que todos estejam esperando o recurso do vizinho ao mesmo tempo.

## Executar o código e descrever comportamento observado
Para executar o programa, use:

```bash
python src/jantar_filosofos.py
```

![1º Registro](/img/RegistroInicio.png)

![2º Registro](/img/RegistroFinal.png)

Comportamento observado: cada filósofo alterna entre pensar e comer. Os logs mostram que nenhum par de filósofos vizinhos come simultaneamente, pois ambos precisam dos talheres compartilhados. A execução termina quando todos concluem o número máximo de refeições, sem deadlock.

## Considerações finais
A solução atende aos requisitos da atividade ao usar threads, recursos compartilhados e sincronização com locks. A estratégia de ordenação por paridade é simples e eficaz para prevenir impasses, mantendo o sistema livre de deadlocks durante toda a execução.