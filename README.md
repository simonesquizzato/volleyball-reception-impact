# reception-impact-analysis
Progetto realizzato nell'ambito della Tesi Triennale in Modelli Statistici che mira ad analizzare quali fattori siano maggiormente impattanti per la conquista di un punto nel campionato di serie D campana nella stagione 2023/2024.

Il progetto è stato realizzato nell'ambito della Tesi Triennale in Modelli Statistici e mira ad analizzare quali fattori siano maggiormente impattanti per la conquista di un punto nel campionato di serie D campana nella stagione 2023/2024. In particolare, l'analisi si pone l'obiettivo di quantificare l'impatto della qualità della ricezione utilizzando un modello di regressione logistica. 

Il file Data_VS.xlsx contiene i dati su cui è stata svolta l'analisi . Ogni record del dataset si riferisce ad un punto effettuato nel corso di una partita, in particolare ogni punto si riferisce alla fase di cambio-palla (o ricezione-punto), fase del gioco della pallavolo in cui la squadra di riferimento si trova in ricezione, ossia pronta a ricevere la battuta effettuata dalla squadra avversaria.
La registrazione di un record avviene nel momento in cui la squadra avversaria effettua una battuta che supera la rete che divide la metà campo e cade nella porzione di campo della squadra oggetto di studio, quando ciò accade vengono registrati:

- La posizione da cui proviene la battuta;
- Il tipo di battuta del giocatore avversario;
- La rotazione in cui si trova la squadra oggetto di studio;
- La rotazione in cui si trova la squadra avversaria;
- La posizione occupata dal giocatore che riceve il pallone;
- L'angolo con cui il giocatore che riceve impatta la palla;
- Il valore associato alla qualità della ricezione;
- La distribuzione degli attacchi effettuati durante il punto;
- L'esito del punto.

Osserviamo, in particolare, le seguenti variabili:

-   Matchday_fac: fattore con 10 livelli contenente il nome identificativo della squadra avversaria
-   Competizione_fac: fattore con 3 livelli (Memorial, Amichevole, Campionato) contenente il tipo di competizione in cui si è giocata la partita
-   Casa_Trasferta_fac: variabile dummy indicante il luogo di svolgimento della partita (0 in trasferta/campo neutro, 1 in casa)
-   Set_fac: fattore con 5 livelli (da 1 a 5) indicante il set di riferimento in cui si è giocato il punto (unità statistica) registrato
-   Rotazione_fac: fattore con 6 livelli (da P1 a P6) indicante la rotazione di partenza della squadra in ricezione, secondo i canoni tattici del gioco della pallavolo;
-   Rotazione_Avv_fac: fattore con 6 livelli (da P1 a P6) indicante la rotazione di partenza della squadra in battuta, secondo i canoni tattici del gioco della pallavolo;
-   Pos_Battitore_fac: fattore con 3 livelli (A1, B6 e C5) indicante la zona antistante al punto da cui viene effettuata la battuta; 
-   Tipo_Battuta_fac: fattore con 3 livelli (F, JF, S) indicante il tipo di battuta che viene effettuato dal battitore avversario;
-   Pos_Ricettore_fac: fattore teoricamente con 6 livelli (da 1 a 6, formalmente da 5 perchè non registriamo nessuna ricezione in zona 4) indicante la zona occupata in campo dal ricettore seguendo la suddivisione classica del campo di pallavolo in 6 zone, osservabile dallo schema seguente:
<img width="982" height="710" alt="Image" src="https://github.com/user-attachments/assets/692396b5-f748-4781-8783-6073d17140f1" />
-   Angolo_Ricezione_fac: fattore con 10 livelli indicante la posizione del corpo che il giocatore assume durante l'esecuzione del fondamentale di ricezione (ad esempio per H si intendono tutti i tipi di palleggio o colpi sopra la testa, per MF, Middle-Forward, si intende un pallone colpito in bagher frontalmente e piegati in avanti, ecc.), precisazione importante è per il livello NA che include tutti i casi in cui la squadra subisce un ace (punto diretto) senza che ci sia un tentativo di intercettare il pallone.
<img width="1009" height="700" alt="Image" src="https://github.com/user-attachments/assets/23090123-9ec7-4426-b50e-e27cf5286af1" />
-   Score_Ricezione_fac: fattore con 4 livelli (da 0 a 3) indicante la qualità della ricezione, assegnato in base alla posizione e all'altezza in cui il palleggiatore (o chi effettua il secondo tocco) impatta il pallone, la valutazione generalmente viene valutata in primis per la posizione in cui cade l'alzata a cui viene sottratto un punto se l'alzata non viene effettuata dal palleggiatore e un punto se chi alza non può effettuare l'alzata in palleggio o in posizione comoda (ad es. necessita di abbassarsi o contorcersi per alzare).

<img width="579" height="513" alt="Image" src="https://github.com/user-attachments/assets/20cbb25c-047e-4111-9ac3-838483aa2009" />

-   Score_Ricezione: la variabile precedente ma riportata come numerica;
-   Banda: variabile di conteggio indicante il numero di volte in cui il palleggiatore alza il pallone, nel corso della stessa azione, al giocatore che ricopre il ruolo di banda;
-   Centrale: variabile di conteggio indicante il numero di volte in cui il palleggiatore alza il pallone, nel corso della stessa azione, al giocatore che ricopre il ruolo di centrale;
-   Opposto: variabile di conteggio indicante il numero di volte in cui il palleggiatore alza il pallone, nel corso della stessa azione, al giocatore che ricopre il ruolo di opposto;
-   Palleggiatore: variabile di conteggio indicante il numero di volte in cui il palleggiatore non alza il pallone, nel corso della stessa azione, provando ad attaccare;
-   Banda2: variabile di conteggio indicante il numero di volte in cui il palleggiatore alza il pallone, nel corso della stessa azione, al giocatore che ricopre il ruolo di banda di seconda linea;
-   Punto: versione numerica della variabile Punto_fac;
-   Punto_fac: variabile dummy indicante l'esito del punto giocato (dove 0 indica punto perso mentre 1 indica punto vinto);
-   Punto_M_fac: fattore con 23 livelli indicante la modalità o causa di conclusione del punto, tale variabile è risultata utile soprattutto nel corso della stagione come supporto alle decisioni dello staff tecnico della squadra. 

Il file Reception-Impact-Analysis.Rmd contiene il codice legato alle operazioni di data wrangling, all'analisi esplorativa dei dati, alla modellazione e all'analisi dei residui del modello stimato.

I file Abstract_Tesi_Simone_Squizzato.pdf e Tesi_Simone_Squizzato.pdf contengono, rispettivamente, l'Abstract e la Tesi relativi al progetto sviluppato.
