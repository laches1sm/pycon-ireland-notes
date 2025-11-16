
AI Agent - a goal-oriented autonomous systems that plans and executes multi-step tasks, using LLMs to decide what to do next
should be able to connect securly to client environments and need a platform that can scale
multicloud and multiagent approach 
MCP adoption - open standards and open source matter when building at scale
LLMs are useless for enterprise use cases - trained on public data - public Github but not trained on your data - none of your compliance/code is in the training data of the model and if it was, something has gone horribly wrong
train your own LLM - need a few GPUs but it's horribly expensive 
by the time you train the model it's outdated
finetuning could work in theory - but it doesn't - using older models 
data moves so fast - the data is already old by the time it's done
use AI Agent - flow loop - LLM in charge of planning - searching, comes back with a bit of text - process language 
API is learning not the model itself
memory - isn't retraining itself on your data each time - it doesn't remember previous conversations - this is handled by the API
Context management - you are the one that's handling the context - not the model 
how much context they can maintain - biggest limitations of LLMs 
give it a summary of each file, or have multiple LLMs that look at the summaries and make a summary of summaries?
giving the LLM tools like google search etc. 
Agentic programming is mainly just a feedback loop - giving it a list of tools and some context 
Plan the next step - and then the model dies 
Turning thought into actions - that is all that an agent is 
Deep research - search through a lot of websites and generate some data and generate the report for you
Multi agent system - it can delegate tasks to other agents 
Can build a deep researcher for your code 
SWBench - benchmark that tests how agents perform in real world situations - 500 github issues that have been sourced from real github issues from open source python projects 
From 0.4% issues solved to 78.80% can successfully close issues without any issues 
https://www.swebench.com 
Can be sure that the agent reads the PR - no LGTM here 
get more reviews that have more value 
Where will we be in 2 years?
building agents as software - different levels of abstraction 
like using a library 
Challenges 
integrating it with other systems - challenge - building tools - which what a lot of agent devs actually build 
most fragmented 
Model Context Protocol (MCP) 
very simple to write - unfortunately everyone started to write it - not ready for enterprise - security governance/observability not here yet - adding revisions to add that in 
most of them don't handle security/retry
some of them don't support OAuth 
need to fully support the specification 
middleware between the client and the server - which solves most of the problems
ContextForge - governance/observability etc. 
(note to self - how to attack/exploit/how to make more secure MCP? might be interesting to look at)
connect to a single gateway that provides all the features it needs and it actually observes things - you have everything under control - gateway 
MCPGateway 
Security First Design - a common problem with MCP servers is XSS exploits 
SQL injection - bad for building agents if it has raw connection - user now has control over infrastructure 
Deny everything and then make an allowlist 
Pluggable security - design security upfront - need input validation etc 
Agents are dumber and they are not accountable 
Agents need to be sandboxed otherwise will have access to the machine - case of an agent deleting everything on a user's machine because it was in the home dir
filter it through a set of plugins - filter data like PII 
plugins in plugins out - written in python 
if you're a python dev learn rust 
scaling is also important - python by default is single threaded 
single threaded use cases up to 10% slower 
some of the agents can be very verbose and hammer infra 
you always need to have a security first approach - guardrails is still trying to be figured out and the same for prompt injection - filter out upfront or use another model to detect that prompt injection has taken place
regex - prompt injection doesn't always take place in English, can take place in other languages, unicode approach 
Can be dangerous - parse logs and perform things like self healing - URL you sent to the agent can contain prompt injection - doesn't know the context that the instruction has - can delete the entire cluster
Trusted Plugins Catalog - high availability, random jitter, retry-backoff, rate limiting - stops abuse or agents getting stuck in loop
plugins for scanning for viruses/malware 
SQL sanitisation - clean up output 
it's not just you that instructs the model - others will train the model to be polite etc. 
OPA Policy Engine - rego - what is allowed, what is disallowed 
connected OPA to ContextForge to add rules 
Can build templates using a template based system 
A plugin is also a MCP server 
Agent Development Lifecycle - how actual enterprises are adopting AI agents - accounts for the unpredictable nature of AI 
evals - how you know that your AI has done the right task
consensus on the evaluation 
give the AI agents the same tools that you do in a secure way - pyright etc... it's unfair to not give it the same tools that you have
takes a special kind of design to make it efficient - learn how to develop things first and learn what is going on - once you have good experience actually writing code then build your own agents 
CI-CD pipeline for context forge - different linters, static analysis tools every single PR gets reviewed and scanned 
don't think about just local dev - think about how to get it into production - think about scaling 
ArgoCD 
Open source ContextForge 
https://github.com/ibm/mcp-context-forge 
https://ibm.biz/enterprise-ai-with-mcp 