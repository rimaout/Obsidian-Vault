---
type: Uni Note
class:
  - "[[WASA (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2025-10-24T18:14
updated: 2025-10-24T18:34
---
## Codice OpenAPI

```yaml
openapi: 3.0.0
info:
  title: API Nasoni di Roma
  description: |
    API per la gestione e la consultazione delle fontane (Nasoni) di Roma.
    Permette di registrare nuove fontane, aggiornarne lo stato e filtrare
    per posizione geografica.
  version: 1.0.0
servers:
  - url: https://api.nasoniroma.it/v1
    description: Server principale dell'API

# ===============================================
# SEZIONE 1: ANALISI E SCHEMI (components)
# ===============================================
components:
  schemas:
    # Nuovo Schema per l'ID, ora riutilizzato in Fountain e FountainID Parameter
    FountainIdSchema:
      type: integer
      format: int64
      description: ID univoco assegnato dal server.
      readOnly: true
      example: 12345

    # Schemi riutilizzabili per Latitudine e Longitudine
    Latitude:
      type: number
      format: float
      description: Latitudine in gradi decimali.
      minimum: -90
      maximum: 90
      example: 41.89025

    Longitude:
      type: number
      format: float
      description: Longitudine in gradi decimali.
      minimum: -180
      maximum: 180
      example: 12.49237

    Range:
      type: number
      format: float
      description: Raggio (in metri o km) per il filtro di vicinanza.
      minimum: 0

    # Task 1.1: Definizione dello Schema "Fountain"
    Fountain:
      title: Dettagli Fontana
      description: Rappresentazione completa di una risorsa Fontana (Nasone).
      type: object
      properties:
        # USA IL RIFERIMENTO ALLO SCHEMA ID
        id:
          $ref: '#/components/schemas/FountainIdSchema'
        state:
          type: string
          description: Stato di funzionamento della fontana.
          enum:
            - good
            - faulty
          example: good
        latitude: 
          $ref: '#/components/schemas/Latitude'
        longitude:
          $ref: '#/components/schemas/Longitude'
      required:
        - state
        - latitude
        - longitude

    Error:
      type: object
      properties:
        code:
          type: string
          example: "NOT_FOUND"
        message:
          type: string
          example: "La risorsa richiesta non è stata trovata."

  parameters:
    # Task 1.2: Definizione del Parametro "FountainID"
    FountainID:
      name: id
      in: path
      description: ID univoco della fontana (Nasone) nel percorso.
      required: true
      # USA IL RIFERIMENTO ALLO SCHEMA ID
      schema:
        $ref: '#/components/schemas/FountainIdSchema'
      # L'esempio del parametro è definito nello schema referenziato.
      
  responses:
    NotFound:
      description: Risorsa non trovata (404 Not Found)
      content:
        application/json:
          schema:
            $ref: '#/components/schemas/Error'
          examples:
            fountainNotFound:
              value:
                code: "NASONE_404"
                message: "Nessuna fontana trovata con l'ID specificato."
    BadRequest:
      description: Richiesta non valida (400 Bad Request)
      content:
        application/json:
          schema:
            $ref: '#/components/schemas/Error'
          examples:
            invalidInput:
              value:
                code: "VALIDATION_ERROR"
                message: "I dati forniti non sono validi. Controllare vincoli e campi richiesti."


# ===============================================
# SEZIONE 2: DEFINIZIONE DEI PATH
# ===============================================
paths:
  # Task 2.1: Operazioni sulla Collezione (/fountains)
  /fountains:
    post:
      operationId: createFountain
      summary: Creazione di una Nuova Fontana
      description: Registra una nuova fontana nel sistema. L'ID viene assegnato dal server.
      requestBody:
        description: Dati della nuova fontana. L'ID non deve essere incluso.
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Fountain'
      responses:
        '201':
          description: Fontana creata con successo
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Fountain'
        '400':
          $ref: '#/components/responses/BadRequest'

    get:
      operationId: listFountains
      summary: Elenco delle Fontane (con Filtri di Vicinanza)
      description: Restituisce l'elenco delle fontane. Può essere filtrato per vicinanza a un punto specifico.
      parameters:
        - name: latitude
          in: query
          description: Latitudine del punto di riferimento per il calcolo della vicinanza.
          required: false
          schema:
            $ref: '#/components/schemas/Latitude'
        - name: longitude
          in: query
          description: Longitudine del punto di riferimento per il calcolo della vicinanza.
          required: false
          schema:
            $ref: '#/components/schemas/Longitude'
        - name: range
          in: query
          description: Raggio in metri (o unità definite) entro cui cercare le fontane (richiede latitude e longitude).
          required: false
          schema:
            $ref: '#/components/schemas/Range'
      responses:
        '200':
          description: Elenco delle fontane restituito con successo
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/Fountain'
        '400':
          $ref: '#/components/responses/BadRequest'

  # Task 2.2: Operazioni sulla Risorsa Specifica (/fountains/{id})
  /fountains/{id}:
    parameters:
      - $ref: '#/components/parameters/FountainID'

    put:
      operationId: updateFountain
      summary: Aggiornamento Completo di una Fontana
      description: Sostituisce completamente la risorsa fontana con l'ID specificato con i dati forniti.
      requestBody:
        description: Dati completi della fontana per la sostituzione (l'intero oggetto).
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Fountain'
      responses:
        '200':
          description: Risorsa fontana aggiornata e restituita.
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Fountain'
        '404':
          $ref: '#/components/responses/NotFound'
        '400':
          $ref: '#/components/responses/BadRequest'

    delete:
      operationId: deleteFountain
      summary: Eliminazione di una Fontana
      description: Elimina la risorsa fontana con l'ID specificato.
      responses:
        '204':
          description: Fontana eliminata con successo (No Content)
        '404':
          $ref: '#/components/responses/NotFound'

    patch:
      operationId: partialUpdateFountain
      summary: Aggiornamento Parziale di una Fontana
      description: Applica aggiornamenti parziali ai campi forniti (es. solo lo stato).
      requestBody:
        description: Proprietà della fontana da aggiornare (solo i campi specificati vengono modificati).
        required: true
        content:
          application/json:
            schema:
              type: object
              properties:
                state:
                  $ref: '#/components/schemas/Fountain/properties/state'
                latitude:
                  $ref: '#/components/schemas/Latitude'
                longitude:
                  $ref: '#/components/schemas/Longitude'
      responses:
        '200':
          description: Aggiornamento parziale applicato con successo
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Fountain'
        '404':
          $ref: '#/components/responses/NotFound'
        '400':
          $ref: '#/components/responses/BadRequest'
```

## Esempi di Requests

>[!note]- POST /fountains
>
>Permette di registrare una nuova fontana nel sistema. L'ID viene assegnato dal server.
>
>**Request URL:** `https://api.nasoniroma.it/v1/fountains`
>
>Ma dobbiamo anche inviare il body contenente lo stato, latitudine e longitudine della fontana.
>
>Ad esempio utilizzando curl:
>
>```bash
>curl -X 'POST' \
>  'https://api.nasoniroma.it/v1/fountains' \
>  -H 'accept: application/json' \
>  -H 'Content-Type: application/json' \
>  -d '{
>  "state": "good",
>  "latitude": 41.89025,
>  "longitude": 12.49237
>}'
>```

>[!note]- GET /fountains
>
>Permette di richiedere l'elenco delle fontane. Può essere filtrato per vicinanza a un punto specifico.
>
>Una richiesta base è `https://api.nasoniroma.it/v1/fountains`, con curl:
>
>```bash
>curl -X 'GET' \
>  'https://api.nasoniroma.it/v1/fountains' \
>  -H 'accept: application/json'
>```
>
>Ma possiamo le informazioni opzionali come latitudine e longitudine, ad esempio `https://api.nasoniroma.it/v1/fountains?latitude=41.89025&longitude=12.49237`, con curl:
>```bash
>curl -X 'GET' \
>  'https://api.nasoniroma.it/v1/fountains?latitude=41.89025&longitude=12.49237' \
>  -H 'accept: application/json'
>```
>
>Se volgiamo limitare la distanza si può aggiungere il range `https://api.nasoniroma.it/v1/fountains?latitude=41.89025&longitude=12.49237&range=100`

>[!note]- PUT /fountains/{id}
>
>Permette di sostituire completamente la risorsa fontana con l'ID specificato con i dati forniti.
>
>Possiamo utilizzare l'url `https://api.nasoniroma.it/v1/fountains/{id}` ma comunque dobbiamo mandare un body contenete le informazioni delle fontana, ad esempio con curl:
>
>```bash
>curl -X 'PUT' \
>  'https://api.nasoniroma.it/v1/fountains/12345' \
>  -H 'accept: application/json' \
>  -H 'Content-Type: application/json' \
>  -d '{
>  "state": "good",
>  "latitude": 41.89025,
>  "longitude": 12.49237
>}'
>```

>[!note]- DELETE /fountain/{id}
>
>Permette di eliminare la risorsa fontana con l'ID specificato.
>
>Dobbiamo utilizzare il seguente url: `https://api.nasoniroma.it/v1/fountains/{id}`, ad esempio con curl:
>
>```bash
>curl -X 'DELETE' \
>  'https://api.nasoniroma.it/v1/fountains/12345' \
>  -H 'accept: */*'
>```

>[!note]- PATCH /fountains/{id}
>
>Permette di applicare aggiornamenti parziali ai campi forniti (es. solo lo stato).
>
>Possiamo utilizzare il seguente url: `https://api.nasoniroma.it/v1/fountains/{id}`, ad esempio con curl aggiorniamo lo stato della fontana a `good`:
>
>```bash
>curl -X 'PATCH' \
>  'https://api.nasoniroma.it/v1/fountains/12345' \
>  -H 'accept: application/json' \
>  -H 'Content-Type: application/json' \
>  -d '{
>  "state": "good",
>}'
>```
