
Dhwani - Voice Mode 

Queries on the proposal- Feb 27, 2025

1) I see that the base model that you will be using is ai4bharat/indicconformer_stt_kn_hybrid_ctc_rnnt_large  which seems to be a 120M parameter and hence looks like its size is just 523 Mb.

In that case -  If you select one of AWS's g4 instances such as g4dn.xlarge which has 16 GB of VRAM (which we are currently using in production for inference), you can run at least 20+ instances of this model on a single GPU at a cost of 0.50$ per hour.

For inference, to achieve single GPU - multiple model instances batching / load balancing of requests - We could use either:  i) NVIDIA Triton Server or ii) Ray serve

If we can fully utilize one GPU first and then expand to multiple GPUs, I believe this would reduce the number of GPUs to scale to your target numbers(for both training and inference since the base model is just 120M parameters)

So, do you think the number of GPUs you will need will change if you consider this approach?

Please correct me if any of my assumptions are incorrect.


2) Just a curious question -  You have mentioned about 'performing initial training and performance benchmarks to make the ai4bharat/indicconformer_stt_kn_hybrid_rnnt_large' better, but you haven't provided the details about - training/testing data that will be used, its size, the licensing arrangements regarding the usage of the data.


Response to Query 1


Below are the clarifications for the queries. 

Voice Mode system is a combination of 4 distinct models
1. Automatioc Speech Recognition 
2. Translation model
3. text LLM ( we will not initially work on this)
4. Text to Speech model 


For first month, 
We want to combine all the 4 systems and run it on a single GPU.
We want to start with the lowest compute server, which can fit all the Model VRAM requirements and 5 minute audio / context VRAM requirement.

Based on this baseline, we will convert the models to Triton kernel server. This needs investigation and effort.


Once we successfully export all the models triton kernels, we will work on scaling it up with large instance and load balancing with multiple small instance. 

Multiple GPU requirement comes into play, if the model conversion fails due to lack of expertise. 
Then we will host the pytorch/transformer/uvicorn models. 

2. Evaluation harness will be done in the second months , if we observe that the accuracy is not good for daily use, then we will combine other available datasets to improve the model.
Re-training is currently out of scope for the initial exploration since it will involve additional effort of people and compute resources.

We want to first try how the existing models work ,
get it running with faster inference.