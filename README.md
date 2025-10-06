# Medical-Text-Generation-Using-LLaMA-2-and-LoRA



🧠 Overview

This script fine-tunes a LLaMA-2 model using a LoRA (Low-Rank Adaptation) approach with 4-bit quantization to save GPU memory.
It uses libraries like Transformers, TRL, PEFT, and BitsAndBytes to make training faster and more efficient.

⚙️ Step-by-Step Explanation
1. Loading the Pretrained Model

The script first loads a pretrained model named aboonaji/llama2finetune-v2.

It uses 4-bit quantization, which means the model weights are stored in 4-bit precision instead of 16 or 32-bit.

This reduces GPU memory usage and makes the model lighter.

The model’s caching is turned off to allow gradient checkpointing (helps save memory).

2. Loading the Tokenizer

The tokenizer converts text into tokens (numbers the model can understand).

It’s also loaded from the same model checkpoint.

The end-of-sequence (EOS) token is used as the padding token, and padding is set to the right side of the text.

This ensures consistent input sizes during training.

3. Setting Training Arguments

These define how the model will train:

Output Directory: Where training results are stored.

Batch Size: Two samples are processed at a time.

Gradient Accumulation: Gradients are accumulated over two steps before updating weights.

Max Steps: Training will run for 100 steps (for quick testing).

Gradient Checkpointing: Saves memory during training.

Logging: Progress is shown every 10 steps.

No Saving: Model won’t save checkpoints automatically (to save time and space).

4. Formatting Function

The dataset must be in a format the model can read.

This function extracts the “text” column from the dataset, which contains the training sentences or dialogues.

5. Loading the Dataset

The dataset aboonaji/wiki_medical_terms_llam2_format is loaded from Hugging Face.

It contains medical-related text in a format suitable for instruction tuning (i.e., question-answer pairs or short paragraphs).

6. LoRA Configuration

LoRA allows fine-tuning a small number of parameters instead of the whole model, saving GPU memory and time.

Important settings:

r (rank): 64 (controls how much of the model is adapted)

alpha: 16 (scaling factor)

dropout: 0.1 (prevents overfitting)

LoRA modifies specific layers instead of all model weights, making training efficient.

7. Trainer Setup

The SFTTrainer (Supervised Fine-Tuning Trainer) from TRL is used.

It takes:

The model and tokenizer

The training arguments

The dataset

The LoRA configuration

The formatting function

This handles all fine-tuning logic automatically.

8. Training Step

The training command (train()) is commented out for now.

When enabled, it will start fine-tuning the LLaMA-2 model on the given dataset using LoRA.

9. Text Generation

After fine-tuning, a pipeline is created to generate text responses.

The user enters a prompt, for example:
“Please tell me about Ascariasis”

The model generates an informative answer based on its training.

🧾 Example Output

If the user asks about Ascariasis, the model might respond like:

“Ascariasis is a parasitic infection caused by the Ascaris lumbricoides roundworm. It spreads through contaminated soil or food and primarily affects the intestines...”



However, in some cases, the infection can cause a range of symptoms, including:

1. Abdominal pain
2. Diarrhea
3. Vomiting
4. Weight loss
5. Fatigue
6. Anemia
7. Malnutrition
8. Intestinal obstruction
9. Inflammation of the rectum and anus

The infection is caused by the ingestion of eggs, which can contaminate food or water. The eggs hatch in the small intestine, and the larvae migrate to the large intestine, where they grow and reproduce. The infection is more common in areas with poor sanitation and hygiene, and in communities where there is a lack of access to clean water and proper toilet facilities.

Ascariasis can be diagnosed through a stool sample, which is examined for the presence of eggs or larvae. Treat
