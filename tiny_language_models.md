
- generation of text data in large privacy senstive datasets
	- needs to be done on prem 
- generation of synthenics populations
- Using aggregated data from open sources to similaute populations behaviours iva agent based modelings
- agents = langauges models 
- reproduce GPT2 for $20 
- not as good as GPT3/4 but good for this kind of work 
- nanochat - covers the whole pipeline
- train a ChatGPT model from scratch
- create a bigger model by investing more money 
- what are the blocks - how do tiny language models work 
- the bigger the better?
	- by throwing infrastructure by throwing data at it the language model gets better
		- but now seeing diminishing returns 
		- lot of attention given to smaller language models
		- microsoft - phi-4 model performed on par to chatgpt3
		- one third of the computational demand of chatgpt3
		- performed good at certain tasks
	- numind - structured extraction - provided JSON and could fill out fileds
	- NuExtract - 1 billlion parameters performed better than ChatGPT4 - BUT if you ask it in the wrong way/tasks it was not build to do then it will fall
	- Tiny models - a model that can be trained on a single GPU within a few days? << 1 billion parameters
	- GPT-2-small: 124 billion parameters
	- TinyStories - how small can language models be and still speak coherent English? 
		- answer complex questions 
		- research paper
		- how children learn language
		- dataset comprised of data that children would learn from a certain age range - trained several models on these children's stories - lot of experiments on the dataset 
		- varied the size of the model
		- grammar and consistency - can it keep track of the same stories?
		- compared generation with different gpt models 
		- small models could generate new stories 
		- lead to Microsoft investigating new Phi models
		- be able to run it on your phone 
		- generate stories better than GPT2-XL 
		- the training model was very simple, very clean, created synthetically 
		- HuggingFace - SmolLM - dataset to train these models 
		- Google - Gemma - open source models that have been trained on different sizes 
			- models 27B parameters performing better than larger models 
		- Why push for more tiny and small language models?
			- environmental benefits - less energy demands 
			- LLaMA-3 paper - GPU hours to train model - 70B required by 6.4m GPU hours 
			- Nuclear power plant equivalent 
			- LLMs are becoming less and less trasnparent 
				- technical report for GPT-4 was a nothingburger and competitors followed 
				- democratising
		- Why are smaller models getting better?
			- we understand scaling loss better 
			- paper from DeepMind looking at scaling - given optimum of data used to train models
			- higher quality data to train models on 
			- proper weighted data and proper scaling laws more efficient 
		- How to train your own tiny model
			- small and large language models share very similar architectures
			- nanochat based on gpt2 
			- very similar architectures 
			- convey text into a sequnece of numbers than can be processed by a model
			- train a model to predict next token given a certain sequence 
		 -  tokenization: from sentences to sequences of numbers 
			 - present the sentence in a programatic way 
			 - represent each word as a symbol - not very flexible 
				 - lose all the language subtleties 
			- language complexities 
				- what is the max length that the model should process? 
				- What is the max sequence length? 
				- vocab size? 
					- related to tokenization - algorithm - best way of splitting  words
					- every model has a tokenizer 
						- byte pair encoding 
						-  tiktokenizer
						- shows how the model considers each word 
					- embedding
						- transforming a token into a vector representation 
						- lookup table: each token corresponds to a vector of learnable parameters
						- embedding size is one of the most important parameters in language models 
						- a model should learn representations that are meaningful - e.g. past tense of verbs or countries with their capitals, like China -> Beijing or swim -> swam 
						- embedded layers - lookup table 
						- positional embedding 
				- step 2: predicting the next word in a sequence 
					- numerical representation - meaningful - take the sequence and predicting the next word to complete the sentence 
					- not very efficient - the matrix could be very big - 100 billion of parameters
					- need to make this process more efficient 
					- mean among the columns - meaningful space - much more lightweight model 
						- destroy a lot of information 
				     * attention mechanism - 100 page LLM book, 2025 
					     * each token is transformed into a vector 
					     * models that will take a different vector 
						     * tries to contaminate it with all the other words
						     * every token is projected into a space 
						     * how each word is affecting other words within the sentence 
						     * mathematical way to weight the other words of the sentence 
						     * increase the size of the space vector used to represent information
						     * stacking more and more blocks on top of each other 
						     * models will keep getting better and better 
						     * reverse process and predict the next topic 
						     * playing with different embedding size - obtain different models with different parameter size - exactly the same arch but different parameters 
						     * bbycroft.net/llm - shows arch for each language models
					* Steps necessary to train a tiny language models
						*  Choose an architecture for the base model
						* Prepare a pre-training dataset, choose a tokenizer (vocab size), sequence length, and the model hyperparameters 
						* What to use to train a base model - data!
						* FineWeb - created by HuggingFace - extracted from CommonCrawl - crawling the web for content - done automatically so many contain junk data 
						* FineWeb key features - high quality data - discards data that is junk 
						* https://huggingface.co/datasets/HuggingFaceFW/fineweb 
						* helps improve models 
						* Simple English Wikipedia 
							* license 
							* provides a wiki that is understandable for non native speakers etc 
							* great dataset to train models to process data that is not too complex 
						* synthetic data for language models 
							* built around original data seeds to enhance model alignment and reasoning properties 
							* generated by GPT4 
							* clean examples to let the model train much better - tailored to the task at hand 
							* https://huggingface.co/spaces/HuggingFaceFW/blogpost-fineweb-v1
							* searching for keywords to see if content was generated by chatgpt - contaminated data in CommonCrawl by ChatGPT 
						* Model evaluation 
							* lot of different benchmarks - ready made benchmarks 
							* HellaSwag 
								* https://huggingface.co/datasets/Rowan/hellaswag
								* multiple choice questions - with every possible endings 
								* when the model collects the answer it gets a point 
						* Can we train our own Tiny Language Models?
							* Prepare data and feed it to our model 
							* https://github.com/gillus/tiny_corpus_prep
							* https://github.com/karpathy/nanochat
						* 