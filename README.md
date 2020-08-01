# LogicText

*LogicText* is a text generator with a logical argument. This project using OpenAI's GPT-2 text model trained on more than a hundred philosophy books. It can generate sentences or paragraphs which imitate the logic patterns; some examples are shared below.



    What then is true knowledge, good mind, whether by experience or learning; by will or by accident?

    ...

    The idea of a relative existence is in other ways at least an illusion. In other words, the notion of our being able to judge of any thing by the relations it has to every other thing is nothing more than the idea of its being an existence, which in the general sense does not exist, and is an accident.

    ...
    
    Tho’ weary woe in love, hither do I joy by the air,
        Ferry your feet upon the air,
    Warm thy heart with an unaccustomed draught
        Bring thee,
    Now this is death in the desert, 
    I sweep from the desert my heels on stone!

    '''


## "The Binary Wisdom" by *LogicText*

I have made a book format output by using a generated outputs of the *LogicText*, you can access using ```/binary_wisdom.pdf``` file. I tried to make minimal post-editing to let *LogicText* do its work, so that you can expect long sentences or few typos. :)

![](images/cover.png)

## Running the *LogicText*

### 1. Preparing Data

I firstly train GPT-2 is the OpenAI's generative machine learning (NLP) model. Training data is extracted using my other repository, [Gutenberg by Topic](https://github.com/cgokce/gutenberg_by_topic), with the *philosophy* keyword.

If you want to train the model on your corpus, you can use the above repository to generate a book corpus of another genre or topic. 

### 2. Model Training

*LogicText* uses a machine learning model, GPT-2 by Radford et al. that needs to be trained on the source data, then it can be used to generate randomized outputs similar to the source corpus. 

For the training code, [ak9250](https://github.com/ak9250/gpt-2-colab)'s Google Colab notebook is updated and used. New features are some text descriptions, dataset reading from google drive, and n-gram plagiarism checker to detect overfitting.

Colab Notebook is shared in ```scripts/GPT2_train_test.ipynb``` and run descriptions are provided in there. I have used the GPT-2 medium model and trained a total of 9436 iterations. Learning rate divided by ten at the 6000th iteration. To prevent overfitting, I manually checked the output about every 500 epoch and applied an n-gram similarity test at the final model. 

### 3. Testing

Testing requires the network checkpoint that previously saved to the google drive. It is the same as the standard procedure, where you can either do conditional sampling by feeding some initial point to the network, or random sampling, by expecting the network to randomize initial state. Depending on the output size, the network provides the results in the Google Colab cell.

I do not share the the pretrained weights by uploading to a public storage due to its size requirement. You can contact me if you need the weight data. Instead, there are about a hundred unconditional output samples provided in the ```samples/100.txt``` file that you can use to check the unfiltered model output.

## Generating the Book Contents

To compile the book, I needed to divide it into sections on different topics. To generate a section, I choose a keyword and start conditional sampling from it. To finish the rest of the section, a previously generated sentence is used as a starting point and fed it to network again. 

I also included the unconditionally generated section, which is initialized from a random point. 

*Sampling:* For each paragraph, I selected about every 1/3 of generated results and discarded the rest. The settings are set the defaults as described in the training code.

## Credits

Thanks to [Radford et al.](https://github.com/openai/gpt-2) for sharing the GPT-2 model, [@nsheppard](https://github.com/nshepperd) for providing fine-tuning code for GPT-2 and [@ak9250](https://github.com/ak9250) for sharing finetuning code of jupyter notebook. Book structure/template is gathered from [latextemplates](https://www.latextemplates.com/template/ebook). Book cover image is generated using [BigGAN TF Hub Demo](https://colab.research.google.com/github/tensorflow/hub/blob/master/examples/colab/biggan_generation_with_tf_hub.ipynb), and [placeit](https://placeit.net) is used for repo cover image.