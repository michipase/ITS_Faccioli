Analisi per la gestione della biblioteca.

OBIETTIVO:

Gestire il prelievo e la riconsegna dei libri da parte di utenti tesserati di una biblioteca, tenendo traccia dei tempi.

IPOTESI:

La biblioteca può avere più sedi.
Gli utenti possono prelevare un libro in una sede e riconsegnarlo in un'altra.
Il prestito ha una durata massima stabilito di volta in volta.

ENTITA:

-UTENTE

	idUtente
	nome
	cognome
	CF
	dataNascita
	telefono
	email

-PRESTITO

	idPrestito
	idUtente
	idLibro
	dataInizio
	dataFine
	durataMax
	sedeInizio
	sedeFine

-LIBRO

	idLibro
	titolo
	autore
	genere
	casaEditrice
	edizione
	note
	idSede

-SEDE

	idSede
	nome
	indirizzo
	telefono
	email

QUERY:
-CREAZIONE


CREATE TABLE utente(
    idUtente text autoincrement PRIMARY KEY,
    nome text not null,
    cognome text not null,
    dataNascita date not null,
    cf text not null,
    telefono text not null,
    email text not null
);

CREATE TABLE sede(
    idSede text autoincrement PRIMARY KEY,
    nome text not null,
    indirizzo text not null,
    telefono text not null,
    email text not null
);

CREATE TABLE libro(
    idLibro text autoincrement PRIMARY KEY,
    titolo text not null,
    autore text not null,
    genere text not null,
    casaEditrice text not null,
    note text not null,
    edizione date not null,
    FOREIGN KEY (idSede) REFERENCES autori(idAutore),
);

CREATE TABLE prestito(
    idPrestito text autoincrement PRIMARY KEY,
    dataInizio date not null,
    dataFine date not null,
    durataMax text not null,
    FOREIGN KEY (idUtente) REFERENCES utente(idLibro),
    FOREIGN KEY (idLibro) REFERENCES libro(idLibro),
    FOREIGN KEY (sedeInizio) REFERENCES sede(idSede),
    FOREIGN KEY (sedeFine) REFERENCES sede(idSede)
);
