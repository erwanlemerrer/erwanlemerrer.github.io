---
layout: archive
title: "Notes and thoughts"
permalink: /blog
author_profile: true
---

_Following opinions are solely mine. Toutes les opinions exprimées ici n'engagent que ma personne._

## Citations glanées ça et la ...

_"En examinant le statut actuel du savoir scientifique, on constate qu'alors même que ce dernier paraît plus subordonné que jamais aux puissances et qu'avec les nouvelles technologies il risque même de devenir l'un des principaux enjeux de leurs conflits, la question de la double légitimation, bien loin de s'estomper, ne peut manquer de se poser avec d'autant plus d'acuité. Car elle se pose sous la forme la plus complète, celle de la réversion, qui fait apparaître que savoir et pouvoir sont les deux faces d'une même question: qui décide ce qu’est savoir, et qui sait ce qu’il convient de décider ? La question du savoir à l’âge de l’informatique est plus que jamais une affaire de gouvernement."_ Lyotard, La condition postmoderne, 1979.

_"L'invasion de notre pensée, comme de notre sensibilité, par des
processus mécaniques est le fait décisif. Ce qui conduit d'un côté à
un art que l'on peut qualifier de mécanique, susceptible de maîtriser
la combinatoire ou d'explorer le champ des possibles défini par une
originalité de base, d'un autre côté à un art de déflagration, de
décompensation, qui exprime le malheur de l'homme hypnotisé, asservi
par la Technique même qu'il croit dominer."_ Ellul, L'Empire du non-sens. L'art et la société technicienne, 1980.

_"La logique de la recherche, c'est cet engregnage de problèmes dans lequel le chercheur est pris et qui l'entraîne, comme malgré lui. [...] Ce qu'on ne comprend pas en France, pays de l'essayisme, de l'originalité, de l'intelligence, c'est que la méthode et l'organisation collective du travail de recherche peuvent produire de l'intelligence, des engrenages de problèmes et de méthodes plus intelligents que les chercheurs. Être intelligent scientifiquement, c'est se mettre dans une situation génératrice de vrais problèmes, de vraies difficultés."_ Bourdieu, Questions de sociologie, 1980.

## Good links

#### Ph.D. thesis
##### Common advice

* for a thesis [funding @irisa](http://www.irisa.fr/en/funding-thesis)
* [Lessons from my PhD](https://web.eecs.utk.edu/~azh/blog/lessonsfrommyphd.html)
* To get acquainted with community habits [Best Paper Awards in Computer Science](https://jeffhuang.com/best_paper_awards/)

##### Where to shoot
* [Top Computer Science Conferences ](https://research.com/conference-rankings/computer-science)
* [Conference Ranks](http://www.conferenceranks.com/)

##### Data + compute
* [Public APIs](https://github.com/public-apis/public-apis)
* Getting [started with grid5000](https://www.grid5000.fr/w/Getting_Started)

#### Drafts and books
* [Learning Theory from First Principles, by F. Bach](https://www.di.ens.fr/~fbach/ltfp_book.pdf)
* [Networks, Crowds, and Markets: Reasoning about a Highly Connected World](https://www.cs.cornell.edu/home/kleinber/networks-book/networks-book.pdf)

#### Various
* [Making the Right Move to Senior Researcher: some challenges and hints](https://hal-lirmm.ccsd.cnrs.fr/lirmm-03240377/file/Valduriez-sigrec-2021.pdf)
* [Comprehensive Python Cheatsheet](https://gto76.github.io/python-cheatsheet/)

## From Dead Hand to Flash Collapse: risky machine to machine chain reactions.
##### Erwan Le Merrer (elemerrer@acm.org), June 2020

_Machine learning based algorithms are now in the wild, and read their environment to react to it. The past has already exhibited relatively benign forms of cascades or chain reactions between these. With the increasing interconnectivity of networks and complexity of algorithms, unpredictable chain reactions might lead to severe flash collapses. This possibility stays largely under the shadow of some less likely events such as a threatening strong artificial intelligence._

Due to the sensational progress of machine learning --and in particular neural networks-- for solving cognitive tasks, was resurrected a fear of technological annihilation by an "autonomous artificial intelligence". The figure of the Terminator cyborg now constitutes an equivalent to the Golwin point in some domains of science. Techno-prophets await the day where programs become self-aware, as the indication of an imminent catastrophy. Endless discussions about its near occurrence or impossibility now populate the media. As there are still no evidence that a strong AI can ever arise, one can ask whether the techno-driven apocalypse might not find another vector than killer robots1.

AUTONOMOUS. The complexity of computer systems and programs continues to increase sharply. This is made possible by the continuous growth of the available processing power, both with specialized types of processors and with the gathering of many of them in datacenter premises. Complex inference algorithms can now directly measure tens of thousands of their environmental variables, and then drive decision-making processes from their analysis. The unprecedented accuracy of their predictions finds applications in self driving cars, financial markets, and video synthesis (with eg, deep fakes).

An historical milestone for complex systems dates back to the cold war era. And this one specifically had retaliation in its code. Perimetr --or Dead Hand-- was built to send a deadly nuclear
strike to the USA, in an automated way. Fearing the decimation of the head of the Soviet after such a nuclear strike, engineers foresee this system to operate automatically, when environmental readings seem to indicate that the West has stroke first. This included monitoring for ballistic launches, ground vibrations and radioactivity (indicating that a strike had indeed happened). The system, or algorithm, was then supposed to act as a consequence of those readings to generate a counter strike, without human decisions in the loop. Yet, This fully automatic system was not deployed, and only a semi-automatic version of it2 was.

HIGH FREQUENCY. Once set-up and activated, this kind of systems lives its program life. And with its own reaction times and temporality, that are far ahead those of humans. More recently, High frequency trading (or HFT) was introduced for that very purpose of operating at super-human timings. The financial markets are now accessed by programs that are designed to read and react, that is to say that they assess their environmental metrics (stock values, number of waiting buy/sell orders, news feeds) and react to these so fast that they overcome "slow" (or human) trading operations. Algorithms are then optimized at the utmost regarding compute time (code optimization) and
action latency (using ultra low latency communication networks). This is key to their prevalence.  It turns out that this superiority w.r.t. human action scales like orders of magnitudes faster
COMPLEX INTERACTIONS AND FLASH CRASHES. Interactions of humans and algorithms, as well as from the algorithms between themselves now lead to a tremendous complexity. In fact, all the interacting pieces of software form an emergent system, that is itself out of the reach of simple institutions or groups of experts. And in consequence no one can test or bound this system. This emerging impact on the markets for instance is far too complex to predict. Salient illustrations of these uncomprehended interactions are called flash crashes. There were massive actions on the markets by those algorithms, leading to the collapse of stock prices as in May 20103. Experts say “the (market) instability can be further exacerbated by HFT algorithms herding one another and thereby transforming instability into widespread crashes”4. And with the critical impact of stocks on real life, this is far from being a good news.

ALGORITHMS PRONE TO ATTACKS. Such complex interactions, and their unpredictable effects, question potential feedback loops. A second and major concern is that algorithms reading variables from large environments are prone to attacks. Hostile high frequency trading algorithms are for instance suspected to have as objective to destabilize other algorithms, in order to get some rewards (e.g., lower stock prices after having triggered potentially unjustified sell actions). For instance a tweet from a hacked account is suspected to have triggered billions on the Standard & Poor’s 500 Index’s value5. This is highlighting the constant race in the search for good “signals” predicting future moves on markets, in order to take advantage before the competition.

Even more concerning, many of those automated algorithms are embedding neural networks, that are known to be sensitive to so called adversarial attacks. These attacks leverage the poor understanding humans have about the decision-making process of neural-networks, to trigger arguably incoherent decisions from them. This is equivalent to finding bugs in more classic algorithms, at runtime. Researchers proposed illustrative attacks in critical decision-making systems such as self-driving cars, by simply modifying their environmental inputs.

FUTURE FLASH COLLAPSE? Algorithms were up to now relatively isolated in their domain: HFT algorithms read stocks and information on the Internet, but only operate on markets. Self driving cars read environmental inputs and make decisions for maneuvering the
car. With both i) the promises of the 5G to interconnect more and more computing devices and their networks, and ii) the capability of neural network models to handle larger and larger sets of data as input, we are entering a new setup, of unprecedented complexity. And if algorithms can read from larger pools of data, on different networks and on different domains, their creators will probably not refrain to do so, following the moto "information is power".

This opens up for the creation of autonomous agents that will be inclined in reacting as fast as possible to a maximal amount of information, leading to risky interactions. Algorithms can then
indirectly influence other algorithms by writing the data some others are going to read, and so on and so forth. In that light, millions of algorithms may very soon depend on each other, in a non controlled way, to make decisions. And these dependencies will create cascade effects that are unlikely to be be interrupted by humans, due to their flash occurrence. The naïve will to create "automatic stops" is bound to encounter the problem that those might be impossible to model and, as their implementation precisely depends on the overwhelming complexity of the data and algorithms themselves.

We are then possibly already in a era where unstable clusters of algorithms are getting more and more interleaved, forming a emergent system reaching all domains of online interactions and decision making processes. The question now becomes: “how can a major chain reaction not occur in the coming years?”.
