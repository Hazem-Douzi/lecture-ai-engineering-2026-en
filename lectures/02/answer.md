# Lecture 02 Answers

## Exercises

- Model and settings used (from `config` in `result.json`):
- Did you run training yourself (`executed_training_myself`): Yes / No (how far you ran the notebook: )
- Before training: `format_rate` = / `content_rate` =
- After training: `format_rate` = / `content_rate` =
- Questions that regressed:
- Failures remaining after training and their types (assertion without evidence / evasion through a confirmation request despite evidence being present / broken format):
- Results of knowledge questions (section 6; classification before → after training) and observations:
- What changed and what stayed the same with training:

## Homework

- Level attempted: Basic / Implementation / Advanced
- Settings or data changed:
- Results (comparison tables or numbers):
- Discussion of when fine-tuning is and is not suitable:

Level attempted: Basic

Settings or data changed:

I changed num_train_epochs from 20 to 10. All other settings remained the same. I restarted the session and reran the notebook.

Results:

With 20 epochs, the format rate was 100%, content rate was 90.48%, final loss was 0.0146, and training time was 208.87 seconds.

With 10 epochs, the format rate was 100%, content rate was 80.95%, final loss was 0.0747, and training time was 89.73 seconds.

Discussion of when fine-tuning is and is not suitable:

Fine-tuning is useful for improving the model's output format and performance on specific tasks. In my experiment, 20 epochs gave better accuracy, while 10 epochs was faster.

Fine-tuning is less suitable when information changes frequently or when the model needs to answer questions using external documents. In these cases, RAG may be a better choice. Fine-tuning also does not completely prevent incorrect answers.


Level attempted: Implementation

Settings or data changed:

I replaced the original FAQ with my own topic: a Python Workshop. I created 5 FAQ items about the schedule, location, registration, equipment, and certificate.

I also created new grounded and ungrounded questions. The ungrounded questions were about information not included in the FAQ, such as Wi-Fi, recordings, and age requirements.

I kept the same JSON format and needs_review design and trained the model for 10 epochs.

Results:

Before training, the format rate was 100% and the content rate was 28.57%.

After training, both rates reached 100%, with all 21 test questions answered correctly according to the evaluation.

The model also correctly requested confirmation for the unknown knowledge questions.

Discussion of when fine-tuning is and is not suitable:

Fine-tuning is useful for teaching a model to follow a specific format and answer questions about a particular topic.

In my experiment, it significantly improved content accuracy.

However, fine-tuning is less suitable for frequently changing information. In those cases, RAG may be better because it retrieves information from external documents.


Level attempted: Advanced

Settings or data changed:

I used make_sft_dataset.py to generate 116 glossary examples in JSONL format. I used 104 for training and 12 for validation.

I fine-tuned Qwen3.5-0.8B with LoRA for 10 epochs and prepared 7 evaluation questions: known terms, reworded questions, and unknown terms.

Results:

Training took 293.68 seconds, with a final logged loss of 0.0773.

After training, the model gave more accurate and concise answers for known terms such as LoRA, AI engineering, and devcontainer.

However, some reworded answers contained incorrect information. For unknown terms like Speculative Decoding and Mixture of Depths, the model gave unsupported answers instead of saying the information was not in the glossary.

Discussion: Fine-tuning vs. RAG

Fine-tuning is useful for teaching a model specific terminology and answer styles.

However, it does not guarantee factual accuracy or prevent hallucinations.

RAG is more suitable when information changes frequently or answers must be based on reliable documents, because it retrieves relevant information directly.

Conclusion:

Fine-tuning improved answers for familiar glossary terms, but RAG would be better for reliable, source-based answers.