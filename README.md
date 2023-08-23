# Music Understanding / Music-to-data (No speech)

## Domain & Concept Knowledge
### Use Case Definition: 
Written representations of musical compositions are crucial for protecting a composer's creation as well as sharing it and reproducing it in the future. However, writing music sheets can be time consuming and not every musician has musical theory knowledge required to do it. We propose to embed and extract significant musical information from an audio file (instruments played, Notes or chords) as a first step to obtain relevant representative data from such audio.
To explore the feasibility of such a task, initially, in this project we’ll ask an LLM to classify the instrument that plays the sound. We’ll compare the results to those of the AutoModelForAudioClassification [3] (AudioSpectrogramTransformer fine tuned for AudioSet sound vocabulary dataset).

As a second step we ask the LLM to provide the chords played by a specific instrument in the audio.

## Limitations & Disclaimers 
Knowing that LLMs receive as input a sequence of text and output the most probable sequence of text that might follow the given input, and they calculate such probability based on their training corpora, it is safe to assume that providing an embedding directly into the prompt text won’t result in an accurate response. This notebook is then built with a demonstration purpose only. 
Large language models are prone to hallucination and thus might not always provide correct information. 

## Use Case
__Title__: Classify a given audio by the instrument and the notes (in a second time) played 
__Description__: 2 prompt options, one for classifying the instrument and other for determining the notes/chords in the audio. As part of the prompt, the embedding of the spectrogram image will be provided in the form of a string.

### Model Parameters:
* __Model__: text-bison-001
* __Temperature__: 0.3
* __Max Output Tokens__: 256
* __TopP__: 0.8
* __TopK__: 40

## Conclusions and Improvements
As expected, directly providing an embedding to an LLM does not seem to result in coherent or accurate outputs. Regardless of the prompt or tolerance (more tests might be necessary) the LLM seems to hallucinate most of the times it is asked to recognize the instrument played. One reason could be that the LLM was not really trained over numerical/vectorial embeddings as a direct input even if it constantly replies with an accurate explanation of a spectrogram embedding. We might improve the accuracy of the results by fine tuning the model with appropriate audio spectrogram embeddings data. 
However in certain cases when asked for the chords/notes played in the audio the amount of notes provided by the LLM was the expected number i.e. if in the audio 3 chords were played, the LLM provided 3 chords, although the chords provided were not always the correct ones, more tests are necessary before we’re able to make a conclusion over this behavior. 
