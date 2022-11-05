# ShaderGenerator

This repository contains code to build a neural net trained to generate graphics shaders. This was created for the MIT 6.864 Advanced Natural Language Processing final project. 

## Dataset

We obtain data from the [Shadertoy](https://www.shadertoy.com/) site. This contains over 60k graphics shaders with associated code. These are labeled with natural language names, tags, and descriptions which we use as the input training data. Unfortunately, since this site isn't moderated, we cannot guarantee that every data point collected is of sufficient quality. However, we assume that enough shaders are appropriately annotated, so this shouldn't be an issue. The data is found [here](shader_dataset). 

## Model

The model is inspired by [[Rabinovich et al., 2017]](https://arxiv.org/pdf/1704.07535.pdf). We use the specific PyTorch implementation [torchASN](https://github.com/xiye17/torchASN). This implementation is useful because it allows adapting the NL-to-PL paradigm to new programming languages, as long as we specify certain constraints of the new language. Specifically, we update the Abstract Syntax Description Language (ASDL), the transition system, and the evaluation code. 

- The ASDL is meant to represent the tree-like structures implicit in code compilers. It defines a grammar that describes how to parse a programming language into an abstract syntax tree (AST). This is found in [torchASN/data/hearthstone](torchASN/data/hearthstone).
- The transition system allows us to convert programs from their logical forms to ASTs. It also checks if incomplete ASTs are correct, which is useful during beam search decoding in our model. This is found in [torchASN/grammar/transition_system.py](torchASN/grammar/transition_system.py). 

## Baseline

As a baseline, we replicate the results in Rabinovich et al., which creates code for each card in a Hearthstone deck. 
