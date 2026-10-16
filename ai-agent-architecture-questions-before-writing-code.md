# AI agent architecture: 5 questions before writing code

![Designing the connections first](https://dxggowrfyirnanabowhr.supabase.co/storage/v1/object/public/site-images/site-ai-agent-architecture-questions-before-writing-code-1792115525.jpg)

My starting point for an AI architecture is an analysis of the problem and the available data. Those inputs determine the automation platform and the tools that belong in the solution

I work through five design questions. First, assign the work: will an agent handle an action, will a Python program do it, or will the task involve both? Second, identify the execution environment, such as a remote VPS or a computer. Third, establish the data: where incoming requests originate and what knowledge is available for responses

The fourth question defines the action we want to produce. An inquiry and an appointment are different outcomes. The fifth specifies delivery: where the result arrives, how it is presented, and the frequency at which it is needed

An example from my own work is a sales assistant in Instagram Direct. Its architecture divides responsibility between Python and Claude. The conversation needs to sound natural while following an established script and collecting required information

![Planning the workflow](https://images.pexels.com/photos/1181343/pexels-photo-1181343.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

Python supervises that process. It checks completeness and keeps model responses within the defined limits. Claude chooses the content of a reply using its instructions and the knowledge base. The same conversation therefore involves two different kinds of work, each assigned to its own component

There is also a distinction between knowledge and workflow. The knowledge base supplies material for the conversation. The script defines its progression and the information that must be gathered. Connecting these parts is a design decision made before their implementation

The client message is the input. Information collected in the dialogue reaches a doctor through a Telegram card. The doctor confirms the appointment before it is created, so a human decision is part of the architecture too

![Messaging as the entry point](https://images.pexels.com/photos/6669813/pexels-photo-6669813.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)

That gives the workflow an explicit destination and a delivery format. A model response is one step along the route; the intended result depends on the connected work of the conversation, script control, and the person making the final decision

I describe the design sequence on my blog in [AI agent architecture: 5 questions before writing code](https://matintellect.com/en/posts/ai-agent-architecture-questions-before-writing-code). Once the responsibilities, data, and outcome are defined, the architecture already has a shape. No code has to exist yet for those decisions to be made
