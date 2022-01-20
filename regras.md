# Guia de Regras para implementação - Corações da Lila

## 1. Comprar 1 carta
O jogador compra uma carta se possuir corações suficientes para comprá-la.

   Se a carta tiver bônus o jogador rola um dado e recebe de recompensa o resultado do respectivo bônus.

---

### Algoritmo

1. O front habilita para clicar apenas as cartas que o jogador pode comprar e as destaca.
    (levar em consideração os bônus que o jogador possui)

2. O jogador vai clicar na carta que deseja comprar dentre as que estão destacadas.

3. O front vai retirar a carta da lista da mesa e adicionar na lista do jogador.

4. O front vai enviar o status da sala para o back através da rota http específica deste tipo jogada.

5. O back valida a jogada:

    - verifica qual jogador tem o status de JOGANDO.
    - verifica se o jogador possui corações suficientes para realizar a compra.
    - adiciona os pontos da carta ao jogador.
    - verifica se a carta possui bônus, se sim roda o dado (funcao de random).
    - verifica qual o resultado do dado e ja aplica esse resultado ao estado do jogo.
    - altera o status do jogador para ESPERANDO e ja atualiza o próximo jogador como JOGANDO
        
6. O back finaliza a jogada

    - verifica se o jogador possui 8 pontos. (se possuir a sala deve alterar seu status para ULTIMA_RODADA).
    - verifica se o próximo jogador é quem começou o jogo (jogador que iniciou a sala) e se a sala está na ULTIMA_RODADA para finalizar o jogo.
    - Se o jogo deve ser finalizado o status da sala deve ser alterado para FINALIZADO.
    
7. Back atualiza a sala no banco.

8. Back devolve a sala para o front através do websocket.
   
9. verifica se a carta possui bonus.
    - Se a carta comprada tiver bônus o front pede para o usuario girar o dado que terá o resultado de acordo com o enviado pelo back.

10. O front atualiza o status da sala para todos
11. O front verifica se o jogo está FINALIZADO (como descrito [aqui](#finalizar-o-jogo))
12. Se não estiver finalizado o front verifica quem é o jogador com JOGANDO e libera a jogada para ele.

## 2. Comprar 1 carta Objetivo
O jogador compra uma carta objetivo se possuir 1 coração de qualquer tipo.

- - -
### Algoritmo
1. O front habilita o baralho de cartas objetivo apenas se o jogador atual (marcado com JOGANDO) possui 1 coração (de qualquer tipo).

2. O jogador clica no baralho de cartas objetivos

3. O front remove uma carta do baralho de objetivos e adiciona na lista de cartas objetivos do jogador.

4. O front envia para o back a alteração do status da sala no endereço http referente a esta jogada.

5. O back valida a jogada:
    - Verifica qual jogador tem o status JOGANDO.
    - Verifica se o jogador possui corações suficientes para comprar a carta objetivo.
    - Altera o status do jogador para ESPERANDO e ja atualiza o próximo jogador como JOGANDO.
    


## 3. Comprar corações

### 3.1 Comprar 1 coração grande

### 3.2 Comprar 2 corações pequenos


## Finalizar o jogo