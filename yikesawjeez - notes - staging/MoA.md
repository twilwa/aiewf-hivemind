# Mixture of Agents Workshop with Cerebras Hardware Overview

Tue, 03 Jun 25

### Cerebras Hardware Overview

- Cerebras builds hardware that runs AI models significantly faster than competitors
    
- Key hardware advantages vs NVIDIA H100:
    
    - 900,000 cores vs 17,000 cores on H100
        
    - One-to-one ratio of cores to memory stores
        
    - Direct memory access for each core
        
    - Only activations transfer between chips
        
    - Currently holds world records for all publicly posted models
        
    - 15.5x faster than fastest GPU provider for MAMA 3.27
        

### Mixture of Agents Architecture

- Evolution from single large models to mixture of experts (MOE) approach
    
- Core concept: Multiple specialized LLMs working together vs single large model
    
- Example benchmark: Math problem solving
    
    - GPT-4: 45 seconds, incorrect answer
        
    - GPT-3: 293 seconds, correct answer
        
    - Ninja Tech implementation: 7.4 seconds, correct answer using mixture of agents
        
- Implementation example (Ninja Tech):
    
    - Planning agent generates 8 potential solutions
        
    - Critique agents evaluate feasibility
        
    - Iterative refinement if needed
        
    - Summarization agent produces final answer
        
    - Process uses 500,000 tokens and 32 LLM calls
        

### Workshop Challenge Details

- Objective: Configure AI agents to generate optimized code
    
- Scoring system: Maximum 120 points possible
    
- Components to configure:
    
    - Model selection
        
    - Number of cycles/layers
        
    - Temperature settings
        
    - System prompts
        
    - Individual layer configurations
        
- Competition focuses on optimizing Python function using LLM agents
    
- Multiple participants achieved perfect scores early in the challenge
    
- Implementation constraints:
    
    - Must work within contact limits
        
    - Three agents and two cycles recommended
        
    - Need to maintain proper method naming in prompts
        

---

Chat with meeting transcript: [https://notes.granola.ai/d/30c37965-424b-4f71-a989-d6fd9cad1de0](https://notes.granola.ai/d/30c37965-424b-4f71-a989-d6fd9cad1de0)

hightlight:
2000-01-01T21:02:24.000Z - self
Hi, my name is Daniel. I'm the Head of Growth here at Cerebus. I,

2000-01-01T21:02:27.000Z - self
We both developer activations, developer marketing, but I also do startup sales. So, if you eat tokens and you're trying to run your startup...,

2000-01-01T21:02:37.000Z - self
you want to use Cerebras in production after the workshop, come talk to me. I am the token arbiter for Cerebras for everyone that is not enterprise. And if you have a cool,

2000-01-01T21:02:47.000Z - self
Research project you want to use Sirius for? I'm also the person to talk to, so if you want tokens for your project, talk to me. Yes, I also really like Hot Pot. I've had Hot Pot three times the last...,

2000-01-01T21:02:59.000Z - self
So, that's a little bit about me. I'm based in San Francisco, and I do a lot of these types of workshops and events and things like that, and here's my Twitter.,

2000-01-01T21:03:10.000Z - self
And this is our intern, Kevin. He's not here with us because he's taking his last high school final in high school, but I wanted to put it here.,

2000-01-01T21:03:18.000Z - self
'Cause he's so a person that built ninety-nine percent of the workshop that you're gonna be doing here today, and I want to make sure we shouted him out, but I want to get selfie. Hell yeah.,

2000-01-01T21:03:28.000Z - self
Hell yeah. He doesn't know I'm doing this. And yeah, he's going to a huge school in UCLA, coming in the fall, but he's currently in high school. So yeah.,

2000-01-01T21:03:38.000Z - self
And that's his Twitter, if you guys want to follow him. Great. Before we get started, who here has heard of Cerebrus? OK, pretty good. Last time I asked...,

2000-01-01T21:03:48.000Z - self
Question like 8 months ago, there was like 2 hands in a room full of like this, so it's so much progress that we've made in the last couple months, so I will dive a little bit deeper into what...,

2000-01-01T21:03:58.000Z - self
Cerebrus, and why our hardware is so much superior than our competitors in the later part of our presentation, but quickly, Cerebrus is a hardware company that makes custom.,

2000-01-01T21:04:22.000Z - self
And things that make our hardware architecture super dominant kind of like all boils down to the innovations we've made in the hardware itself, and...,

2000-01-01T21:04:32.000Z - self
we hold the world record in every single model we host publicly, and it's not even close, so for...,

2000-01-01T21:04:39.000Z - self
We're around 15.5 times faster than the fastest input provider on the GPU, so if you want kind of like something that doesn't compare.,

2000-01-01T21:04:48.000Z - self
for anything that's currently in the market. So this is kind of your only option for fast influence. So that's what our company does, and this is what I'm bringing to startups. So if you're a startup that wants this influence, you should come talk to me after the talk.,

2000-01-01T21:04:59.000Z - self
So, what are we doing today? So actually, spoiler alert, we're going to use to regress hardware today for our workshop, so if you guys can...,

2000-01-01T21:05:08.000Z - self
Actually try it, but before I want to explain what we're actually building, so we're going to build an application with a mixture of agents each agent.,

2000-01-01T21:05:18.000Z - self
would be a separate LLM. And kind of like right now, I want to explain why this is beneficial, why we want to build that, and why this architecture is better compared to it.,

2000-01-01T21:05:28.000Z - self
One LM that we use right now, so sort of like from a pre-training perspective, how do we make large...,

2000-01-01T21:05:38.000Z - self
Models more intelligent, better? How do we scale and faster? So, all these type of questions we ask is to regress when we have our hardware, we can scale our models pretty.,

2000-01-01T21:05:48.000Z - self
But how can we make them more efficient? What kind of architectures do we need to invest in? So I kind of wanted to give sort of like the evolution that happened in the last.,

2000-01-01T21:06:08.000Z - self
Showed is that if you continue scaling the model size, you're gonna improve the performance the models will have better skill sets that's how you better scale it.,

2000-01-01T21:06:18.000Z - self
The next thing that we saw in the LLM evolution is you actually have to spend a lot of time improving your data that you could train on, so Llama model became bigger.,

2000-01-01T21:06:28.000Z - self
But I also spend a lot of time on curating the data set and scaling the number of pockets we came for as well, and now that's when we heard about DipCP3, that was...,

2000-01-01T21:06:38.000Z - self
a few months ago, that model took some additional innovations into place. So if you want to go with a larger, you see like GBT3 is 13 billion, Lama3 is 400 billion.,

2000-01-01T21:06:48.000Z - self
So, if you want to continue getting the model size, which is what gives us better models, you need to come up with not just data set.,

2000-01-01T21:06:58.000Z - self
Improvements, so how do we actually improve the models, and that's like sort of the large models, because there's. An increased number of parameters, and...,

2000-01-01T21:07:08.000Z - self
way to scale it, scale the difference, infrastructure, and make it more efficient. The answer here is a mixture of experts.,

2000-01-01T21:07:18.000Z - self
And these type of models, to just give you an overview of how it works, imagine you have a transformer architecture, which is what we use as a backbone for large languages.,

2000-01-01T21:07:33.000Z - self
Models, it has different layers, so here I highlighted that there are more layers there, but the one important layer, some important layers are embedding attention at...,

2000-01-01T21:07:43.000Z - self
and now we're gonna see, like, how...,

2000-01-01T21:07:45.000Z - self
We changed the standard transformer transformer architecture into something called future experts. So, if you look at different layers and you do something. To work, you will...,

2000-01-01T21:07:55.000Z - self
Out that feed forward network has a specific bottom line, and. It has a challenge. Because feed forward network sort of like has to disentangle all the information that...,

2000-01-01T21:08:05.000Z - self
Previous layers, plus a potential layer, so you can think about it this way: reported network has to decide which neuron in the network to activate when it sees a goal.,

2000-01-01T21:08:16.000Z - self
So it's really hard because the task that we have, sometimes we have different. Languages, but sometimes we require different specimization.,

2000-01-01T21:08:31.000Z - self
Biology, etc. So, for networking, has the hardest job in the whole, so how does mixture of best grids go back?,

2000-01-01T21:09:33.000Z - self
because we know that for providers who are being misses, you're not increasing the instance time. So you can actually activate as a so you will have like in terms of the time.,

2000-01-01T21:09:44.000Z - self
You will be better in place, must be trainable marginal. Yeah, so sort of like to pause on this. This is the approach that other...,

2000-01-01T21:10:06.000Z - self
Companies are getting specific, and to gain excess for critical models. Throwing models over the pool, and they're kind of. Like for being able to run.,

2000-01-01T21:10:18.000Z - self
Large, large parameter models in a efficient state, so you don't have to continue to just add it to be able to run better and better models. There's other protocols work, so. Something I want to talk a little bit about this.,

2000-01-01T21:10:28.000Z - self
Inference time compute. Last year, I believe, Ilia Sitaber gave a talk at NeurIPS around how we're in the age of inference time compute, where we...,

2000-01-01T21:10:38.000Z - self
Just throwing as much data as possible, and we train these really, really large models, and eventually we're going to hit a data wall, right, where we have no more additional unique data to train our models.,

2000-01-01T21:10:48.000Z - self
So now, what we can do is do more compute after the model has been trained to be able to get better and better results and more and more employees than not.,

2000-01-01T21:10:59.000Z - self
So, an example of problems that benchmarks test for are math problems. So, I want to first take a math problem from the...,

2000-01-01T21:11:08.000Z - self
Math competition and see how certain models kind of tackle this kind of problem, and the thing with these types of math problems is that it's harder for, like, a single...,

2000-01-01T21:11:18.000Z - self
Non-reasoning model to be able to solve these, because they require multiple steps in sequential thought, where it's really hard to do things like this without reasoning, and when I ran this exact...,

2000-01-01T21:11:28.000Z - self
From GPT-4L, which is not a reasoning model, it took forty-five seconds to come to the wrong answer. This is like the frontier model, but CPT-03.,

2000-01-01T21:11:39.000Z - self
I'm sorry, GPT-03, which is a reasoning model, took 200 ninety-three seconds to come up with the right answer, so this is it on the right, doing everything.,

2000-01-01T21:11:49.000Z - self
but it just took 293 seconds. So if you want something in a reasonable within three business days kind of timeline, this is probably not the solution for you.,

2000-01-01T21:11:58.000Z - self
Like, imagine you're like going through an app and it just is loading for six minutes. Or 3 minutes or. 4 minutes and fifty-three seconds. That's just like an unreasonable amount of time from a lot of...,

2000-01-01T21:12:08.000Z - self
Tasks, so I wanted to do something called mixture of aging, which is leveraging the collective intelligence of multiple LLMs to come to the right cancer, and I think, like, because...,

2000-01-01T21:12:18.000Z - self
Cerebros is a super fascinating provider. I'm sure everyone can see where this is going. So the mixture of agents is basically the ability to take advantage of these earth-shattering speeds from,

2000-01-01T21:12:28.000Z - self
Hardware and apply them into harder problems like this, so it's not just about speed, it's about getting higher intelligence with less smart models, and...,

2000-01-01T21:12:38.000Z - self
The mixture of agents is a lot of it is inspired by a mixture of expert architecture, because essentially you're trying to do the same thing, you're trying to squeeze out as much intelligence in an efficient way.,

2000-01-01T21:12:55.000Z - self
From a lot of a lot of kind of tokens, whether it's within the model or outside of the model, so basically how it works is that you send inputs to multiple.,

2000-01-01T21:13:04.000Z - self
combines all of the answers from all the individual models into a single answer.,

2000-01-01T21:13:08.000Z - self
And this has shown that it outperforms even frontier models on certain benchmarks, as benchmarked by together.,

2000-01-01T21:13:17.000Z - self
the ones that kind of came up with this idea. So I want to show you an example of a startup that's actually building in production with,

2000-01-01T21:13:57.000Z - self
They're basically building a smarter chatbot, and this is Ninja Tech solving the same exact question in 7.4 seconds.,

2000-01-01T21:14:07.000Z - self
getting to answer correct. So people are using this type of technique and our inference together in production to solve really hard questions like this math problem.,

2000-01-01T21:14:32.000Z - self
Okay, cool. So we basically with what this startup did was take.,

2000-01-01T21:14:37.000Z - self
a bunch of models and a bunch of element calls and get the right answer that a frontier model reasoning model took 293 seconds all the way down to 7 seconds.,

2000-01-01T21:14:47.000Z - self
And here's how their whole application works. So they have a planning agent that spits out eight potential proposals for the right answer.,

2000-01-01T21:14:57.000Z - self
And then another token of critique agents comes in and be like, hey, are these any of them feasible answers to this particular problem that I'm trying to solve? In this case, all of them were bad.,

2000-01-01T21:15:07.000Z - self
So then what happens is that the planning agent goes back to the drawing board and then spits out sixteen-k contacts worth of thinking of things of eight answer proposals, and then the same virtual...,

2000-01-01T21:15:17.000Z - self
What happens where different agents like, are any of them good? In this case, in the example I showed before, two of them were potential answer candidates that could have been the correct answer.,

2000-01-01T21:15:27.000Z - self
And then another agent, a summarization agent, takes those two top answers and then turns them into the final answer. Which is essentially the right answer. So, this whole process...,

2000-01-01T21:15:37.000Z - self
It took 7 seconds, took over 500,000 tokens to be generated, and thirty-two LLM calls, some of them in parallel, some of them sequential, so this type of system...,

2000-01-01T21:15:47.000Z - self
allows you to take advantage of non-frontier models, even open source models that may not perform as well on benchmarks and turn them into performing better than frontier models.,

2000-01-01T21:15:59.000Z - self
So, like I said again, why don't people use O3 in production? It's because it's very slow, like what I...,

2000-01-01T21:16:07.000Z - self
Can't even think about use cases where you can wait 5 minutes to come up with an answer, unless it's like very asynchronous, and Cerebras solves the speed bottleneck.,

2000-01-01T21:16:17.000Z - self
And obviously, service is the leader in fast inference. So I'm going to show you why we are so fast. So this is an architecture diagram of a GPU. And how do I get it in red?,

2000-01-01T21:16:27.000Z - self
is the core, or the thing that does all the mathematical computations that allow LMs to predict the next token. In this particular GPU, which is the H100, we're around 17,

2000-01-01T21:16:37.000Z - self
1000 cores on this chip. The problem is that the memory where all the weights and all the intermediate calculations and all the other information needed to...,

2000-01-01T21:16:47.000Z - self
Produce the next second is stored largely off the chip, and these memory channels that communicate between the cores and the external.,

2000-01-01T21:16:57.000Z - self
Become bottlenecks as you run larger and larger models, because of course you have to transfer in more weights and you have to transfer in more intermediate calculations in the KB cache while you're...,

2000-01-01T21:17:07.000Z - self
To calculate the max token, Cerumbrus tackles this by having a radically different memory management system. We have 900,000 individual.,

2000-01-01T21:17:17.000Z - self
on one chip. And then with those 900,000 cores, we have 900,000 individual memory stores that are distributed all across the chip, one-to-one with our compute cores.,

2000-01-01T21:17:27.000Z - self
And each core has direct access to memory the core-specific memory holds the same set of weights, regardless of what you're putting into.,

2000-01-01T21:17:38.000Z - self
So, basically, you don't need to wait for the external weights or the intermediate calculations to load to be able to do the computation, so you can just do it in real time because there's...,

2000-01-01T21:17:47.000Z - self
No kind of memory transfer time that you need to look for everything is just on the chip, and Cerebra scales linearly across larger models, so the thing that makes...,

2000-01-01T21:17:57.000Z - self
was really fast with super large models is that the only piece of data that's being transferred from chip to chip is activations. That's the only piece of data that travels.,

2000-01-01T21:18:07.000Z - self
It can even be like transferred using a single Ethernet board, that amount of data. It's very small. With a DGX cluster with multiple GPUs, you have to transfer.,

2000-01-01T21:18:17.000Z - self
So many activations in cache computations in between layers, because single GPUs cannot be multiple layers of computations via hundreds of emulinks, connectors, switches, et cetera.,

2000-01-01T21:18:27.000Z - self
And that networking piece is the reason why we're so dominant compared to NBNGPs. So, Daria, how does this all translate? Sure.,

2000-01-01T21:18:38.000Z - self
I probably want to start with a problem that I have. And see how many people have the same problem. So when I interact with a native model with just one model, I usually...,

2000-01-01T21:18:47.000Z - self
To solve a particular problem, and then it doesn't get the right solution right away. Usually, if the problem is complex, right? So, how do you continue prompting it and refining it?,

2000-01-01T21:18:57.000Z - self
And at some point, heating the number.,

2000-01-01T21:18:59.000Z - self
For all partners that we want to open process or something like that, we'll start over with a chat from scratch. Does anyone else have the same problem? Okay, cool.,

2000-01-01T21:19:10.000Z - self
Here, what we do. With mixture of agents, we're gonna specialize each agent to solve a particular portion of the problem.,

2000-01-01T21:19:19.000Z - self
So imagine you have a very complex problem. I don't know, you need to do a surgery, let's say, right? Imagine that. So we need different types of people. To help in the surgery. And we're going to ask each expert.,

2000-01-01T21:19:29.000Z - self
To specialize in one specific part of the surgery, so they all together can work and produce better results compared to just one person.,

2000-01-01T21:19:39.000Z - self
I do it through prompt engineering, and the one nice thing about it is, instead of doing multiple rounds, multiple iterations, to find the best solution at the end.,

2000-01-01T21:19:49.000Z - self
You're gonna find a solution at your shop, at one shop. You're gonna ask one question, and because each kind of like agent is. Already specialized, and so we...,

2000-01-01T21:19:59.000Z - self
Portion of the task, they will they will combine the results together, and it's gonna be the final solution without continuing sculpting, so this is what we're gonna build today.,

2000-01-01T21:20:09.000Z - self
This is the time for the hands-on workshop. So before we move on, this is like the second time I'm showing this. Everyone needs an API key. This is like the one thing you need to do for the workshop.,

2000-01-01T21:20:19.000Z - self
Get an API key. Okay, cool. And then please go to this GitHub link and then star and fork the refresh. That's the next step.,

2000-01-01T21:20:32.000Z - self
I don't have HD shots of Kevin going like that, so that's,

2000-01-01T21:20:44.000Z - self
This is also in our Slack channel if you don't want to do our code scams. So if you are into AI engineer,

2000-01-01T21:20:50.000Z - self
We will also drop the slides there and you guys can draw here if you want to. Help each other out.,

2000-01-01T21:20:59.000Z - self
MRA workshop. Does anyone have issues finding that? Yeah, and once you guys start and work the repo, we're going to,

2000-01-01T21:21:09.000Z - self
Deploy this app via Streamlit, or you can run it locally, whatever you prefer. I just don't want to deal with Python installation issues, so that's why where I suggest...,

2000-01-01T21:21:19.000Z - self
If you have the internet bandwidth to go through Streamlit, but if not, doing it locally via Python.,

2000-01-01T21:21:29.000Z - self
If you want to come back to. Several of the steps, can we share it in a Slack channel so you can open slides YouTube to just before it?,

2000-01-01T21:21:39.000Z - self
Emily A mature agents dash workshop. Yeah, so once you start for.,

2000-01-01T21:21:49.000Z - self
So you basically are going to deploy it via Streamlit or locally. And basically how you deploy it on Streamlit is you go to Streamlit.io. I would suggest logging in.,

2000-01-01T21:21:59.000Z - self
With GitHub, that way everything is set up for you, and then deploy the streamers SAS MLA workshop that you have worked into your GitHub repo.,

2000-01-01T21:22:10.000Z - self
Changing the main file path, and then clicking Advanced Settings, and once you click Advanced Settings, you have to plug in your series, and that's how you run the app.,

2000-01-01T21:22:22.000Z - self
So I'll wait like two, let's say three minutes for everyone to go and clone and,

2000-01-01T21:22:30.000Z - self
spin up their app and then we can go from there. Raise your hand if you need help from me or Daria. Who can help you get that video.,

2000-01-01T21:23:32.000Z - self
Which repo is it? Do you know which repo it is? Okay, got it.,

2000-01-01T21:23:43.000Z - self
And if you want steps on how to set up media, you can go to the slide.,

2000-01-01T21:23:51.000Z - self
Yeah, I. Think Kevin committed the API key. Should we just...,

2000-01-01T21:24:00.000Z - self
use that one?,

2000-01-01T21:24:10.000Z - self
High schooler. It's OK. His API is rate limited. It's not like he has like the body. It's OK. He's an intern.