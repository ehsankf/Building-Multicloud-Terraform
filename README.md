#### Launch the model worker(s)
```bash
python3 -m fastchat.serve.model_worker --model-path lmsys/vicuna-7b-v1.5
```
Wait until the process finishes loading the model and you see "Uvicorn running on ...". The model worker will register itself to the controller .
