# Fine-Tuning word2vec Turkish models' word embeddings with Negative sampling, word extracting and dimension reduction ( autoencoders )

A Turkish word2vec model proposed by Abdullatif Koksal (https://github.com/akoksal) using the Gensim library is fine-tuned with negative sampling and word-extracting algorithm after dimension-reduction using AutoEncoders.

# Downloading the Model

Gensim model proposed by Abdulaltif Koksal can be downloaded from his repository using the link https://github.com/akoksal (trmodel).

# Generating the Dataset and Creating the JSON file for storing the Embeddings of Pre-trained Model

Embeddings size of 400 are extracted from the model and saved to a ".json" file. 
".json" file contains the each word trained in the model and their corresponding vector with a size of 400.

# Dimension Reduction from 400 vector size to 40 vector size Using AutoEncoder

Indices of each word is extracted from the .json file and fed into the autoencoder that consists of an "encoder" and "decoder" layers.
Outcome of encoder layer (words embeddings with the size of 40) is used in order to fine-tune the word embeddings of 'trmodel'.

# Fine-tuning the pre-trained model with negative sampling and word-extracting Algorithm

A new dataset is chosen from the dumps of wikipedia (https://dumps.wikimedia.org/mirrors.html).
Model architecture is created with negative sampling algorithm.
A subsampling algorithm that removes (based on frequency ratio of each word) the words that are considered as outliers is implemented as well. Due to the lack of qualified hardware and limited dataset, subsampling is NOT applied upon the text data. With a higher-level machine and a higher size of data can be chosen and a better performing Turkish word2vec model can be trained using the subsampling algorithm.

For each word in the new dataset that are already exist in the pre-trained model, corresponding word embedding is found from the .json file and used to initialize the initial value of that particular word in the model. If the word in the new dataset is not exist in the pre-trained model, then a word-extracting algorithm is proposed. If the new unique word is "arabaları", but that word is not exist in the pre-trained model; instead "araba" is exist, last character of the new word is removed and checked again until a match is found so that non-existing words could also be fine-tuned with the existing embeddings. ( E.g: "arabaları" == "araba" ---> "arabalar" == "araba" ---> "arabala" == "araba" .... "araba" == "araba" --> keep removing until match is found. A limitation until at least 3-character-word can be given to come up with meaningfull words in the end of the day.) 
