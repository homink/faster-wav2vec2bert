# faster-wav2vec2bert
**faster-wav2vec2bert** is a reimplementation of Meta AI's Wav2Vec2Bert ASR model inference using [CTranslate2](https://github.com/OpenNMT/CTranslate2)(>v4.4.0) framework.

For the inference processing, Sigmoid activation function is added to process [the GLU activation](https://github.com/huggingface/transformers/blob/f38590dade57c1f8cf8a67e9409dae8935f8c478/src/transformers/models/wav2vec2_bert/modeling_wav2vec2_bert.py#L392) and [asymmetric relative positional embedding logic](https://github.com/huggingface/transformers/blob/f38590dade57c1f8cf8a67e9409dae8935f8c478/src/transformers/models/wav2vec2_bert/modeling_wav2vec2_bert.py#L527) is added in the Attention Class. Compared to the HuggingFace implementation, the int8 quantized model shows an 12% increase in speed and a 61% reduction in GPU memory usage with a 72% reduction in CPU memory usage when processing 300 audio files. Additionally, using an N-gram language model with pyctcdecode further can improve the speech recognition accuracy. My environment includes an NVIDIA GeForce RTX 2080 11GB with CUDA 12.4, torch==2.12+cu12.1, and transformers==4.42.0.

An [example](https://github.com/OpenNMT/CTranslate2/blob/cb16c8e670d47f060c355c52a3009e26e4861d36/python/tests/test_transformers.py#L1028) is available for your experiment.
