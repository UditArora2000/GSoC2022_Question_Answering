# DBpedia Question Answering System
A Question Answering pipeline to provide users with richer responses.  <br>

This repository will provide the implementation of the project proposed using the title 
"[Understanding and Optimizing DBpedia Question Answering through Explanations](https://forum.dbpedia.org/t/understanding-and-optimizing-dbpedia-question-answering-through-explanations-gsoc2022/1628)" that is funded by the [Google Summer of Code program](https://summerofcode.withgoogle.com/programs/2022/projects/xMuRURaT).

The project is carried out by [Udit Arora](https://github.com/UditArora2000). 

The project Supervision and support is done by:

* [Andreas Both](https://github.com/anbo-de)
* [Alexander Perevalov](https://github.com/Perevalov)
* [Ricardo Usbeck](https://github.com/RicardoUsbeck)
* [Ram Athreya](https://github.com/ram-g-athreya)

Use cases of the future QA system:

* Users will be able to see if their intended entities have been correctly identified by the QA system. If not the users can accordingly rephrase their questions to get the desirable results.
* Users will be made aware of alternative answers in the event of the predicted answers having a low confidence score.
* Users would have the option to improve/modify their queries in case the information user requested for is not present with in the DBpeda Knowledge Graph.

Visualization of the current QA system:
```mermaid
	graph TD
	    subgraph End-User
		    res(Default Response)
		    exp(Input Expression)
		    cres(Custom Response)
		    superres(Response) --> | | cres(Custom Response)
		    superres(Response) --> | | res(Default Response)
	    end
	    subgraph Fullfillment
		    wh(Webhook)
		    wh(Webhook) --> |contains| H(components.js);
		    wh(Webhook) --> |contains| I(app.js);
		    wh(Webhook) --> |contains| J(intent.js);
	    end
		subgraph Dialogflow
		    A(Dialogflow-Agent) -->|contains| B(Entities);
			A(Dialogflow-Agent) -->|contains| C(Intents);
		    A(Dialogflow-Agent) --> |check fulfillment| fc(Fulfillment Checker)
		    fc(Fulfillment Checker) --> |enabled| wh(Webhook)
		    fc(Fulfillment Checker) --> |disabled| res(Default Response)
	    end
	    subgraph RDF-Visualization
		    F(app.py) --> |uses| E(index.html);
			I(app.js) --> |graph request| F(app.py);
	    end
	    exp(Input Expression) --> |intent matching| A(Dialogflow-Agent)
	    I(app.js) --> |uses| H(components.js);
		I(app.js) --> |uses| J(intent.js);
	    I(app.js) --> |give response| cres(Custom Response)
```