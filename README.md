# TraceMorph

![image](tracemorph/static/icon.jpg)

**TraceMorph** adalah library Python untuk melacak eksekusi fungsi, membangun visualisasi call-chain, serta menghasilkan narasi error berbasis AI (via LLM API).

### 🚀 Fitur

- Dekorator tracing fungsi otomatis
- Pelacakan exception global
- Ekspor hasil trace ke JSON
- Narasi human-readable berbasis LLM
- Bisa diintegrasikan ke middleware, testing, atau backend

### Cara install

```pip

pip install tracemorph

```

### 🧠 Contoh Penggunaan

```python
from tracemorph import trace

@trace
def bagi(a, b):
    return a / b

bagi(10, 2)
```

### contoh 2

```python

from tracemorph import trace, TraceBuilder

@trace()
def error_prone(x, y):
    return x / y  # Bisa error kalau y=0

if __name__ == "__main__":
    try:
        error_prone(10, 0)
    except Exception:
        pass

    data = TraceBuilder.build_latest_and_export()

    if data:
        print(data['colored_narrative'])  # Print narasi berwarna rapi di terminal
    else:
        print("No trace found.")

```

### contoh 3

```python

from tracemorph import trace, TraceBuilder

@trace
def test(x):
    return x * 2

test(10)

print(TraceBuilder.build_narrative_for_last()[0])

```
