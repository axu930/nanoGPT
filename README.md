A GPT project made following the tutorial by Andrej Karpathy at https://www.youtube.com/watch?v=kCc8FmEb1nY but trained using the complete works of HP Lovecraft

The bigram notebook follows the first half of the tutorial in making the simplest possible model for a text generator; final losses end up around 2.5 after 1,000 iterations and never really get better. 

The nanoGPT notebook first implements a transformer with a single head of self attention, and then implements a second model with 4 layers of transformer blocks, each with 4 heads of self-attention + feedforward layer at the end. We also use layer norm and dropout in the latter model. Each training step is on 16 blocks of 128 characters (1024 characters total). This was trained for a total of 200,000 iterations, taking approx 90 mins on a Google colab A100. Final loss approx 1.39; validation and train losses were close enough that more training can be done. 

The LoRA notebook uses the LoRA net to fine tune the pretrained transformer from nanoGPT to learn to output tweets. The GPT model is from the pretrained model in the nanoGPT journal. The LoRA net is a basic net built following the paper https://arxiv.org/pdf/2106.09685 with middle dimension 16. The tweet data is from the Kaggle dataset: https://www.kaggle.com/datasets/kazanova/sentiment140; we only use 100,000 tweets with negative sentiment to train. This was trained for 20,000 iterations on my 2.4GHz quadcore Intel i5 over ~13 mins, with a final loss of approx 2.3; I suspect that the main bottleneck in this approach is that the original GPT model had never seen tweet text before and thus the frozen pretrained token and position embedding nets are unable to process the new text very well. 

