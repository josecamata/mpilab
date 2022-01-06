# Uma breve descrição do problema do "Jogo da Vida"

O "Jogo da Vida" é uma simulação simples desenvolvida por John Conway. No "Jogo da Vida", o domínio é uma matriz bidimensional de células, 
e cada célula pode ter um de dois estados possíveis, geralmente chamados de "viva" ou "morta". A matriz geralmente é inicializada 
com números aleatórios e o sistema evolui no tempo. Em cada etapa de tempo,
cada célula pode ou não mudar seu estado, com base no número de células vivas adjacentes, incluindo diagonais. Existem três regras:

1. Se uma célula tiver três vizinhos vivos, a célula estará viva. Se já estava vivo, permanecerá assim, e se estava morto, ficará vivo.
2. Se uma célula tiver dois vizinhos vivos, não haverá alteração na célula. Se estava morto, permanecerá morto, e se estava vivo, permanecerá vivo.
3. Em todos os outros casos - a célula estará morta. Se estava vivo, fica morto e se estava morto permanece morto.

A ideia por trás do "Jogo da Vida" é que ele simula grosseiramente populações de organismos. Os organismos precisam do 
apoio de outros organismos para viver. Se não houver uma população significativa, ou seja, zero ou um vizinho, o organismo morrerá. 
Se houver dois vizinhos, o caso é neutro, sem alteração. Se houver três vizinhos, os organismos se multiplicarão. 
Com quatro ou mais vizinhos, há superlotação e os organismos morrerão.

Um exemplo das mudanças que ocorrem para duas células em um determinado intervalo de tempo é mostrado na Figura 1
abaixo, onde as células "vivas" são azuis e as células "mortas" são brancas.

