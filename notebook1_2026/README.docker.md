# Docker

## Build & Run

```bash
cd notebook1_2026
docker build -t ee568-assignment .
docker run -p 8888:8888 -v $(pwd):/workspace ee568-assignment
```

Open the URL printed in the terminal (e.g. `http://127.0.0.1:8888/lab?token=...`) in your browser.

## Without Docker

```bash
pip install -r requirements.txt
jupyter lab
```
