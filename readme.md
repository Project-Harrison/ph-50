# PH-50

PH-50 is a lightweight benchmarking tool for evaluating large language models (LLMs) on a random sample of multiple-choice questions from a maritime-focused CSV dataset. It uses the Together AI API and supports multiple open-source instruction-tuned models via a YAML config.

---

## Features

- Randomly selects 5 questions from a dataset
- Prompts an LLM using Together API
- Compares model response to the correct answer
- Prints concise accuracy summary (e.g., `4 / 5 correct`)
- Outputs any incorrect responses for review
- Waits 1 second between API calls to avoid rate-limiting
- Model selection is driven from a YAML file (`models.yaml`)

---

## File Structure

```
PH-50/
├── main.py                # Main benchmarking script
├── questions.csv          # Input question dataset
├── models.yaml            # YAML config with list of model names
├── .env                   # Stores TOGETHER_API_KEY
```

---

## Setup

1. **Install dependencies**

```bash
pip install pandas python-dotenv tqdm together
```

2. **Create `.env`**

```
TOGETHER_API_KEY=your_api_key_here
```

3. **Add `models.yaml`**

```yaml
models:
  - name: meta-llama/Llama-3.3-70B-Instruct-Turbo-Free
  - name: meta-llama/Llama-4-Maverick-17B-128E-Instruct-FP8
  - name: deepseek-ai/DeepSeek-R1-Distill-Llama-70B-free
```

4. **Prepare `questions.csv`**

Must contain the following columns:

```
id,correct_answer,question,A,B,C,D
```

---

## Run

```bash
python main.py
```

---

## Output

Example:

```
Evaluating: 100%|████████████████████| 5/5 [00:06<00:00,  1.30s/it]

Model Accuracy: 4 / 5 correct

Incorrect Responses:

Q: What is the generally accepted method of determining whether the atmosphere within a cargo tank is explosive?
Expected: D
Model said: C
```

