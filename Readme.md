# Local LLM Prompt Engineering & NLP Pipeline

## Project Overview
This project explores the mechanics of Large Language Models (LLMs) by deploying Google's `flan-t5-small` locally using PyTorch and Hugging Face Transformers. The objective was to build an NLP pipeline to test model capabilities across various tasks and experiment with different prompt engineering techniques.

By executing the model locally on dedicated GPU hardware (CUDA), this project also highlights the intersection of model deployment and hardware utilization.


## Tech Stack
* **Python 3.10**
* **PyTorch:** Hardware-accelerated tensor computation (CUDA)
* **Hugging Face Transformers:** Model loading and tokenization
* **Hugging Face Datasets:** Loading the `knkarthick/dialogsum` conversational dataset

## Experiments & Tasks Performed
The model was tested on multiple NLP tasks to evaluate the effectiveness of instruction-tuned models:
1. **Machine Translation:** English to German and English to Hindi.
2. **Sentiment Analysis:** Extracting emotional context from dialogue.
3. **Zero-Shot Summarization:** Asking the model to summarize a conversation without prior examples.
4. **One-Shot Summarization:** Providing the model with an example dialogue/summary pair in the prompt to guide its output structure.

## Observations & Engineering Takeaways
* **Hardware Execution:** Successfully routed model tensors to the local GPU via PyTorch (`.to("cuda")`), significantly speeding up inference compared to CPU execution.
* **Model Limitations:** As expected with an 80M parameter model, `flan-t5-small` struggles with complex generative tasks and non-Latin translations (e.g., Hindi). However, it serves as an excellent, lightweight sandbox for testing pipeline architecture and prompt structures before scaling up to larger models like Llama 3 or Mistral.

## Inference Results & Evaluation
Below are the results from the `flan-t5-small` local inference tests. As an 80M parameter model, it performs well on basic classification (sentiment) but struggles with complex generation or low-resource translation.

| NLP Task | Prompt | Model Output | Engineering Note |
| :--- | :--- | :--- | :--- |
| **Translation (German)** | "Translate to German: I am successfully running AI on my GPU!" | *Ich habe erfolgreiches AI auf meinem GPU!* | Successfully translated technical context. |
| **Translation (Hindi)** | "Translate to Hindi: I am running large language model..." | *(Empty Output)* | Highlights the vocabulary limitations of the "small" model tier. |
| **Sentiment Analysis** | "Give me the sentiment for [Dialogue]..." | *negative* | Correctly classified the rushed, anxious tone of the dialogue. |
| **Zero-Shot Summary** | "Summarize the conversation: [Dialogue]" | *It's ten to nine by my watch.* | Extracted a sentence rather than summarizing. Needs Few-Shot prompting or a larger parameter model. |

## How to Run Locally
1. Clone the repository.
2. Install dependencies: `pip install -r requirements.txt`
3. Ensure you have a CUDA-capable GPU and the appropriate PyTorch version installed.
4. Run the Jupyter Notebook.

---
*Author: Nilesh Singh | Master's Student, Computer Engineering at SDSU*
