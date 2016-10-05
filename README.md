O Barbeiro Dorminhoco

O problema consiste em simular o funcionamento de uma barbearia com as seguintes características.
A barbearia tem uma sala de espera com N cadeiras e uma cadeira de barbear. Se não tem clientes à espera,
o barbeiro senta numa cadeira e dorme. Quando chega um cliente, ele acorda o barbeiro. Se chega outro cliente
enquanto o barbeiro está trabalhando, ele ocupa uma cadeira e espera (se tiver cadeiras disponíveis).

A solução a seguir usa 3 semáforos: clientes, fila e mutex. O semáforo clientes tranca o barbeiro, sendo seus
“fantasminhas” representados pelos clientes que chegam. O valor desse semáforo indica o número de
clientes à espera.

O semáforo fila tranca os clientes e implementa a fila de espera. O semáforo mutex garante exclusão mútua.
Também é usada uma variável inteira, qtd, que conta o número de clientes à espera. O valor desta variável
é sempre  igual ao “número de fantasminhas” do semáforo clientes.

Um cliente que chega na barbearia verifica o número de clientes à espera. Se esse número é menor que o número
de cadeiras, o cliente espera, caso contrário, ele vai embora.

Inicialmente, o barbeiro fica bloqueado (dormindo) até a chegada de algum cliente.

Se tem alguma cadeira disponível, o cliente incrementa a variável count e executa a operação V no semáforo
clientes. Se o barbeiro está dormindo, ele é acordado. A seguir, o cliente libera a exclusão mútua e entra
na fila de espera. O barbeiro adquire a	exclusão mútua, pega o primeiro da fila de espera e vai fazer o corte.

Quando termina o corte de cabelo, o cliente deixa a barbearia e o barbeiro tenta pegar
um próximo cliente. Se tem cliente, o barbeiro faz outro corte. Se não tem, o barbeiro dorme.
