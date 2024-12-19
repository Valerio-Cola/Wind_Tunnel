# MPI 

Ogni processo prende tot righe, si calcola quindi quante righe per processo segnando anche inizio e fine
Nel caso ci siano righe restanti verranno date all'ultimo processo

Ogni processo alloca la propria parte di flow flow_copy e particle_locations quindi my_rows * colonne

Inizia la simulazione:
1. la modifica della ventola viene fatta fare a un solo processo
2. Nel modulo che sposta le particelle ogni processo verifica le particelle totali ma prende in considerazione nei calcoli solo quelle che si trovano nelle proprie righe, verificabile con particles[particle].pos_row

Aggiorna particle locations di nuovo solo se la particella è nelle righe assegnate al processo

Fatto ciò ogni processo invia le proprie particelle con allgather a tutti i processi

3. Anche nella gestione del flusso ogni processo modifica solo le particelle di sua competenza 

da capire meglio

4. Negli array per l'output ogni processo si crea il proprio locale A B C e vi inserisce i propri dati
Alla fine fa una reduce MPI_SUM per tutti e 3 gli array  e la invia al rank 0, poichè fuori dal codice che non dobbiamo modificare a stampare gli output è il rank 0