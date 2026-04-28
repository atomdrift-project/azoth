# azoth

The world's first generalized open-source ML model for malware detection.

http://atomdrift.org/

azoth is the trained model (XGBoost + ONNX) that ships inside [litmus](https://codeberg.org/atomdrift/litmus). See [TRAINING.md](TRAINING.md) to rebuild it from the published corpus.

## Pipeline

```
human / LLM
    │
    ▼
cleave-traits ──► cleave / litmus ──► hopper ──► azoth-trainer ──► azoth
```

### [cleave-traits](https://codeberg.org/atomdrift/cleave-traits)
47,000+ YAML behavior rules, aligned to [MBC](https://github.com/MBCProject/mbc-markdown) and [MITRE ATT&CK](https://attack.mitre.org/). The ground truth.

### [cleave](https://codeberg.org/atomdrift/cleave)
Static analyzer. Extracts capabilities from binaries, source, and archives; scores them against cleave-traits.

### [litmus](https://codeberg.org/atomdrift/litmus)
Classifier. Wraps cleave with the azoth model and returns `hostile`, `suspicious`, or `benign` with the behaviors that drove the call.

### [hopper](https://codeberg.org/atomdrift/hopper)
Job broker and labeled sample store. Hands work to litmus workers and holds the training corpus in Postgres.

### [azoth-trainer](https://codeberg.org/atomdrift/azoth-trainer)
Streams labeled samples from hopper, trains XGBoost, calibrates a threshold, exports XGBoost and ONNX.

### azoth
The model.

## Sample store

The training corpus is published at `r2:azoth-training`. See [TRAINING.md](TRAINING.md).
