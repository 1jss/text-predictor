# Text Predictor

## Description
Text Predictor is a simple text generation application that uses a purely statistical approach to predict the next word in a sentence. There is no transformer or AI involved so the results are not very coherent. You "train" the statistical model by proviging it with a large corpus of text. The model then uses the corpus to calculate the probability of the next word in a sentence given the previous words. The model can then be used to generate random text.

## Usage
The application is a single html file that can be opened in any browser.

### Training
You train the model by pasting text in the textbox and clicking "Train Model". The text is then added to the corpus. You can train the model with as much text as you want. The more text you train the model with, the better the predictions will be. More text can be added to the model at any time.

### Generating text
You can generate random text by clicking "Generate Text". The model will then generate a random sentence based on the current corpus.

### Exporting and importing
You can export the current model for later use by clicking "Export Model". The model will be downloaded as a JSON file. You can import a previously exported model by clicking "Import Model" and selecting the JSON file. The model will then be loaded into the application. Note that nothing is saved between sessions. If you close the application, you will have to import the model again.

## How it works
On training the model the provided text is split into words (tokenized). Some special characters are split, but casing and punctuation is saved. The model then adds each token to the corpus or updates the existing token's frequency count if it already exists. This way the corpus contains the total number of times each word has appeared in the total training data.

The model also keeps track of the 10 words that have appeared after a word and their respective frequency. This is done for each word in the corpus so that the model can calculate the probability of a word appearing after another word.

When generating text the model starts with a random word that starts with a capital letter. It then selects the most probable word from the list of possible next words. The third word is selected based on the most probabilities in the two former words and so on.  This process is repeated until the model has generated a text of 100 words. The generation currently does not select next word randomly, so "temperature" for the generation is always 0. This means that the model will always select the most probable word based on the former words. There is uncommented code that makes the model select the next word randomly, but it is not used as the results were (even) worse than pure probability.