---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: false
created: 2025-07-26T17:19
updated: 2026-01-31T13:32
---

Senza anno:
- "\(ioStud.getEndpointAPI())/appello/ricerca?ingresso=\(token)&codiceCorso=\(exam.courseCode)&criterio=\(exam.didacticModuleCode)&tipoRicerca=4"

Con anno ma senza inserirlo:
- "\(ioStud.getEndpointAPI())/appello/ricerca?ingresso=\(token)&annoAccaAuto=&codiceCorso=\(exam.courseCode)&criterio=\(exam.didacticModuleCode)&tipoRicerca=4"

Con anno inserendolo:
- - "\(ioStud.getEndpointAPI())/appello/ricerca?ingresso=\(token)&annoAccaAuto=\(annoAcca)&codiceCorso=\(exam.courseCode)&criterio=\(exam.didacticModuleCode)&tipoRicerca=4"
- Dove annoAcca è preso dalla student bio


Risposta a richiesta prenotazione, ma opsi non era svolto:
```json
{
    "esito": {
        "flagEsito": 0,
        "id": 0,
        "nota": "URL questionario recuperata con successo.",
        "ritorno": null
    },
    "output": "e81e4f32-5ce6-47cf-ada5-1524f2e497e6",
    "url": null,
    "urlOpis": "https://www.studenti.uniroma1.it/opis/app/index.html?token_opis=L7CR40LY&env=opis_book_2025&ingresso=e81e4f32-5ce6-47cf-ada5-1524f2e497e6"
}
```

Risposta a richiesta di cancellazione di prenotazione:

```json
{
    "esito": {
        "flagEsito": 0,
        "id": 0,
        "nota": "Prenotazione eliminata con successo.",
        "ritorno": null
    },
    "output": "c0530eb2-9ec0-4d2b-befa-0ee26f0e34a5",
    "ritorno": null
}
```