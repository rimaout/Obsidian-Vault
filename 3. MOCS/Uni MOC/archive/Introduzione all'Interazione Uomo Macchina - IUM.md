---
type: Uni Note
class:
  - "[[Interazione Uomo Macchina (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2025-12-10T09:11
updated: 2025-12-17T12:31
---
## Cos'è?

L'interazione uomo macchina è una campo multi disciplinare, che studia la progettazione, valutazione e implementazione di sistemi informatici per l'utilizzo umano.

![[Pasted image 20251210091703.png|600]]

Data la multidisciplinarietà della materia è inverosimile essere un esperti ogni campo che appartiene, per questo vengono utilizzate:
- Design methods and processes
- Models
- Heuristics
- Best practices
- Conventions
- Experiments and user studies

## Gli ingredienti

In questo ambito si parla sempre di tre soggetti:
- lo User
- il Computer
- la Task da compiere

L'obbiettivo è quello di sviluppare un sistema capace di supportare l'utente nello svolgere la task, con un focus sull'usabilità:
- Useful
- Usable
- Used

>[!note]- User
>
>Quando si parla di un utente ci si riferisce ad un essere umano composto dalle seguenti componenti:
>
>***Sensory systems***:
>- Visual
>- Auditory
>- Haptic
>- Spatial
>
>***Acting systems***:
>- Hands
>- Voice
>- Head
>- Body
>- ...
>
>***Cognitive processes***:
>- Perception
>- Memory

>[!note]- Computer
>
>***Input peripherals***:
>- Keyboard, mouse
>- Trackpad, trackball
>- Touch surfaces or screens
>- Microphone
>- Sensors
>- Card readers
>- ...
>
>***Output peripherals***:
>- Screen
>- Audio (voice, sounds)
>- Haptics
>- VR/AR headsets
>- ...

In questo ambito l'uomo è un soggetto creativo, invece la macchina è soggetto deterministico.

## Goal, Task, Domain

L'utente vuole raggiungere dei **goals**, in uno specifico dominio (**domain**).

Ogni dominio (**domain**) ha i propri termini e modi di dire, i propri obbiettivi e componenti.

Le **Task** sono operazioni effettuate dall'utente che manipolano il dominio.

Un **goal** può essere raggiunte effettuano una o più tasks.

## Human Error is bad Design

Human errors should never be considered as faults of the user rather, «they are usually a result of bad design» (Norman)

Humans tend to be imprecise, distracted, not-omniscient
- System design should anticipate this human behavior
- Minimize the chance of inappropriate actions (evaluation)
- Maximize the possibility of discovering and repairing an inappropriate action (execution)
- Enable users to understand the state of the system and build an appropriate model

## Design Processes and Frameworks

Nella progettazione di interfacce per l'interazione tra l'uomo e la macchina vengono studiati e utilizzati diversi processi e frameworks, con l'obbiettivo di semplificare e ridurre gli errori durante il processo di design.

>[!note] User-Centered Design (UCD)
>
>This approach takes the needs, wants, and limitations of the actual end users into account during each phase of the design process.
>
>User-centered design issues are discovered during the early stages, this reduce the risk of software project failure.
>
>**Benefits:** systems easier to learn, with less human errors, encourage users to discover advanced features, and avoids “building the wrong system.
>
>**Issues:** how to find users? How many? How motivated? How to speak their language? How to extract user needs, business needs, organizational implications?

>[!note] Participatory Design
>
>One step further than UCD, users are directly involved in the collaborative design of the things and applications they use.
>  
>Engage a group of users:
>- Discussions
>- ﻿﻿Creating scenarios, sketches, dramatizations
>- ﻿﻿Creating and testing lo-fi prototypes
>- ﻿﻿Continuous meetings, flexible management
>- ﻿﻿Highly reliant on the skills of the group moderators/leaders (keep involved, filter ideas, reward participation, work around resistances, ...)
>- ﻿﻿More effective with more mature and prepared user populations (less with kids, elderly, disabled, ...)

>[!note] Agile Interaction Design
>
>Borrows ideas from Agile development in software engineering:
>- System is built incrementally in rapid release cycles
>- Rapid prototyping techniques (for hardware, software and physical objects)
>
>Requires:
>- low-cost many-iterations prototype
>- fast usability inspection (extreme usability, XU)

## Human Centered Design

Lo Human Centered Design è una filosofia che da particolare importanza sull'usabilità del sistema.

>[!note] Usabilità
>
>Dove per usabilità si intende la capacità con cui un sistema può essere utilizzato dall'utente con  per eﬀectiveness, eﬃciency to achieve the specified goals.
>
>Dimensions of usability:
>- *Usefulness*: does it do something people want?
>- *Learnability*: is it easy to learn?
>- *Memorability*: one learned, is it easy to remember?
>- *Effectiveness*: does it allow reaching the goal?
>- *Efficiency*: once learned, is it fast to use?
>- *Visibility:* is the state of the system visible?
>- *Errors:* are errors few and recoverable?
>- *Satisfaction:* is it enjoyable to use?

### Process and Steps

![[Pasted image 20251210105330.png|700]]

>***Note:*** in this course we will focus on *Needfinding* - *Prototyping (Storyboarding)* - *Testing*

>[!note] Needfinding – what is wanted
>- What exactly is needed? How are people currently accomplishing the goal?
>- User observation, interviews, …
>
>>**Learn more:** [[Needfinding - IUM]]

>[!note] Analysis
>- Formalize and structure the needs
>- Create interaction scenarios, stories, tasks
>- Compare current situation with expected new situation
>
>>**Learn more:** [[Task Analysis - IUM]]

>[!note] Design
>
>- The main choices to shape the system
>- Rules, guidelines, design principles
>- Considering diﬀerent types of users
>- Modeling and describing interaction
>- Visual layout
>- Consider all inputs from cognitive models, communications theories, organization issues

>[!note] Iteration and prototyping
>- Design must be supported by intermediate verification
>- Evaluate the design in its partial forms:
>	- Prototypes
>	- Evaluation metrics
>- Involving users
>
>>**Learn more:** [[Storyboards - IUM]], [[]]

>[!note] Implementation and deployment
>- Hardware and software implementation
>- Documentation

