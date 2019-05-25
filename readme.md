# The StatNLP Semantic Parser

Code for the: Text2Math: End-to-end Parsing Text into Math Expressions

## Installation

Java 1.8

```
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java8-installer
```

ZeroMQ

```
git clone https://github.com/zeromq/libzmq
cd libzmq
./autogen.sh && ./configure && make -j 4
make check && sudo make install && sudo ldconfig
```

JZMQ

```
git clone https://github.com/zeromq/jzmq
cd jzmq/jzmq-jni
./autogen.sh && ./configure && make
sudo make install
```

Torch dependency libraries

```
luarocks install lzmq
luarocks install lua-messagepack
luarocks install luautf8
```

A jar file in provided in `bin/`. One easy way to re-compile the code is to create a new project in Eclipse and export a runnable JAR file for the main classes: `MathSolverMain` and `EquationParserMain`.

## Word embedding

Download the .pkl files from [Polyglot]( https://sites.google.com/site/rmyeid/projects/polyglot#TOC-Download-the-Embeddings). Put these files in `neural_server/polyglot`, then run the following to preprocess for Torch:

```
bash prepare_torch.sh
```

## Reproducing the experimental results

The following script will pre-train a hybrid tree model, train the neural network, and perform evaluation on the standard GeoQuery dataset.

```
bash run_parser.sh
```

Run a neural net server that listens on port 5556 and specify the `gpuid` (>= 0 for GPU, -1 for CPU)

```
th server.lua -port 5556 -gpuid -1
```

Train neural hybrid tree models for multiple languages:

```
bash run_neural.sh
```



