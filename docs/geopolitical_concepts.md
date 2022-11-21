# geopolitical_concepts

Each section of this document includes:
- a brief introduction to the concept
- a break down of the concept into its component parts
- a red team and a blue team implementation of the compenent part
- considerations


## control - impose your will on the adversary 
> "... supposing to ourselves two wrestlers. Each strives by physical force to compel the other to submit to his will: each endeavors to throw his adversary, and thus render him incapable of further resistance.  
> 
> War therefore is an act of violence intended to compel our opponent to fulfill our will.”  
>
>- Carl Von Clausewitz, On War

The concept we are abstracting is "imposition of your will on another entity". This is not limited to governments and violence. Enterprises and non-capitalist entities will also adopt aspects of these concepts in their pursuit of competition.


### DIME
> An acronym used in geopolitical discourse to describe how a government can impose their will on another entity

- Diplomacy
- Information
- Military
- Economy


#### Diplomacy
Almost no abstraction needed here.  Notably, diplomacy is often limited to within the respective organizations. 

For both red and blue teams:
- diplomatic relations between other friendly teams is often what leadership contributes to on the day to day


#### Information
Interpret this literally. Control over information is what we do.


A blue team could implement the following:
- do not disclose more than what is required to friendlies
- security awareness campaigns
- do not publically announce anything that is not absolutely necessary

A Red team could implement the following:
- destruction/manipulation of logs
- obfuscation of commands, payloads, methods
- emulate the TTPs of another red team


#### Military
The notion of military power can be abstracted to include any kinetic means. Kinetic means offer some of the best opportunities for creativity. Alongside these opportunities however are also opportunites to step out of professional scope. Caution is advised. 


A blue team could implement kinetic means in the following ways:
- Secure design. 
- Screens with sensitive information do not face an open room
- creating and enforcing bottlenecks, physical and logical
- denial of face to face services, i.e. choose your arena, homefield advantage

A red team could implement kinetic means in the following ways:
- use of drones to gain access to wifi
- tailgating: following closely through a checkpoint to circumvent authentication
- destructive methods for initial access or to create a situation. Note that this is extremely unlikely to ever be within scope


#### Economy
Money is just another resource. It is a way for imposing your will on the world. Most implemtations of geopolitical economic actions do not translate to our activities, they would be out of professional scope. It is important to consider that the only reason corporate security roles exist is due to their economic impact. Direct action on the adversary's economy is almost universally out of professional scope. 


A blue team could implement the following:
- buget considerations, spend all or return a residue ?
- argue based of the economic impact of failure to comply

A red team could implement the following:
- when constructing remediation reports, economic impact should be communicated effectively
- limiting your budget and producing significant results can lend a great weight to your findings


## treason - targeting the human element
Humans are the weakpoint in most modern organizations. We abstract *treason* as a representation of an insider threat. This can be further abstracted to *reasons for which an individual's interests diverge from the organization's interests*.

### MICE
> An acronym for memorizing some common motives for treason. 

- Money
- Ideology
- Coercion
- Ego

These can be applied to social engineering campaigns to leverage insiders to enable our operations. These also prove to be valuable considerations when strategizing for defensive engagements. 


#### Money
Unlikely to be within scope for the red team, except in the case of employee retention. However, as blue it must be considered. 

The following questions are good starters for strategy:
- are we paying our employees enough to stay on our team?
- are we paying our employees enough to afford a quality of life? 
- are our employees vulnerable to traditional bribes? is it likely that could happen?


#### Ideology
This concept should be the highest priority for your considerations. 

The following questions are relevant for both red and blue teams:
- do the actions of the company align with the morals and ethics of its employees?
- is "whistle blowing" a possibility for employees? do the laws of the containing country favor wistleblowers or the enterprise?

Notably for the red team, trying to social engineer someone's ideology into initial access should have at a minimum the following considerations:
- is this within scope?
- does the length of the engagement enable such an action?
- is this ethical?


#### Coercion
Unlikely to be within scope for either team. I am hesitant to outright suggest anything here. This section is left as an exercise to the reader. 

- please use your best judgement.
- before implentation, please "sanity check" any ideas you may have against an secondary source


#### Ego
Operationalizing this concept is not straight forward. The concept itself is as follows: *someone whose ego is not satisfied by their work is vulnerable to commiting treason*. 

Blue teams should care about this for the following reasons:
- employee retention
- securing employees enables a secure workpace
- insider threats are a rising trend; motives often cited are retaliation for workplace mistreatment

Red teams should consider the following:
- the length of the engagement might prevent cultivation such as this
- is this within scope?
- is this ethical?


