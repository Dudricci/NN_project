<img src="https://storage.googleapis.com/music-synthesis-with-spectrogram-diffusion/architecture.png" alt="Architecture diagram">

In this work, we focus on synthesizers that can encode and decode audio from MIDI sequences with arbitrary combinations of instruments in realtime.

Our work was divided in two stages. In the first, we created the two in-parallel encoders, which have the same structure. Then, we created the decoder, with a similar architecture to the encoders.

Training on a full song was not possible in term of computational power, due to the quadratic scaling of self-attention. So we split the input into segments, and the parallelism is useful to guarantee smooth transitions in the concatenation of them. In particular, the first encoder takes a single segment in WAV format, while the second encoder takes the spectrogram of the previous segment.

The outputs of the two encoders are concatenated, to be passed to the cross-attention layer of the decoder. 

About the decoder, it is trained as a Denoising Diffusion Probabilistic Model (DDPM), taking in input both the outputs of the encoder blocks, and the real spectrogram.
