title: java调用keras模型
author: Halfopen
tags:
  - keras
categories:
  - 机器学习
date: 2018-03-02 20:39:00
---
首先要把keras模型保存为pb格式

```python

... 模型定义，调用过model.compile

from keras import backend as K

sess = K.get_session()

def freeze_session(session, keep_var_names=None, output_names=None, clear_devices=True):
    """
    Freezes the state of a session into a prunned computation graph.

    Creates a new computation graph where variable nodes are replaced by
    constants taking their current value in the session. The new graph will be
    prunned so subgraphs that are not neccesary to compute the requested
    outputs are removed.
    @param session The TensorFlow session to be frozen.
    @param keep_var_names A list of variable names that should not be frozen,
                          or None to freeze all the variables in the graph.
    @param output_names Names of the relevant graph outputs.
    @param clear_devices Remove the device directives from the graph for better portability.
    @return The frozen graph definition.
    """
    from tensorflow.python.framework.graph_util import convert_variables_to_constants
    graph = session.graph
    with graph.as_default():
        freeze_var_names = list(set(v.op.name for v in tf.global_variables()).difference(keep_var_names or []))
        output_names = output_names or []
        output_names += [v.op.name for v in tf.global_variables()]
        input_graph_def = graph.as_graph_def()
        if clear_devices:
            for node in input_graph_def.node:
                node.device = ""
        frozen_graph = convert_variables_to_constants(session, input_graph_def,
                                                      output_names, freeze_var_names)
        return frozen_graph

frozen_graph = freeze_session(K.get_session(), output_names=[model.output.op.name])
from tensorflow.python.framework import graph_io

graph_io.write_graph(frozen_graph, "./", "model.pb", as_text=False)
```

java调用pb模型
```java
package com.cisl.text;

import org.tensorflow.*;
import org.tensorflow.types.UInt8;

import java.io.IOException;
import java.nio.FloatBuffer;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.util.Iterator;

public class PbModelTest {

    public static String modelPath = "/media/h/新加卷/TextClassification/TextModel/expert-graph.pb";

    public static void main(String[] args){


        byte[] graphDef = readAllBytesOrExit(Paths.get("/media/h/新加卷/TextClassification/TextModel/model.pb"));

        Graph g = new Graph();
        g.importGraphDef(graphDef);

        Iterator<Operation> ops = g.operations();
        // 打印可用的操作
        while (ops.hasNext()){
            Operation o = ops.next();
            System.out.println(o+" "+o.numOutputs());
        }

        Session s = new Session(g);
        int[][] shape =new int[1][200];
        Tensor inputTensor = Tensor.create(shape, Integer.class);
        Tensor keepProb = Tensor.create(0.5f);
        Tensor phase = Tensor.create(false);
        Tensor<Float> result = s.runner().feed("input", inputTensor).feed("dropout_1/keras_learning_phase", phase).fetch("output/Softmax").run().get(0).expect(Float.class);

        System.out.println(result);
        float [][] f = new float[1][3];
        result.copyTo(f);
        for (float fl:f[0]
             ) {
            System.out.print(fl+" ");
        }

    }


    private static byte[] readAllBytesOrExit(Path path) {
        try {
            return Files.readAllBytes(path);
        } catch (IOException e) {
            System.err.println("Failed to read [" + path + "]: " + e.getMessage());
            System.exit(1);
        }
        return null;
    }
}


```

调用结果

    2018-03-02 20:34:10.892312: I tensorflow/core/platform/cpu_feature_guard.cc:137] Your CPU supports instructions that this TensorFlow binary was not compiled to use: SSE4.1 SSE4.2 AVX AVX2 FMA
    <Const 'Adam/decay'> 1
    <Const 'Adam/beta_2'> 1
    <Const 'Adam/beta_1'> 1
    <Const 'Adam/lr'> 1
    <Const 'Adam/iterations'> 1
    <Const 'output/bias'> 1
    <Identity 'output/bias/read'> 1
    <Const 'output/kernel'> 1
    <Identity 'output/kernel/read'> 1
    <Placeholder 'dropout_1/keras_learning_phase'> 1
    <Identity 'dropout_1/cond/pred_id'> 1
    <Switch 'dropout_1/cond/Switch'> 2
    <Identity 'dropout_1/cond/switch_t'> 1
    <Const 'dropout_1/cond/dropout/random_uniform/max'> 1
    <Const 'dropout_1/cond/dropout/random_uniform/min'> 1
    <Sub 'dropout_1/cond/dropout/random_uniform/sub'> 1
    <Const 'dropout_1/cond/dropout/keep_prob'> 1
    <Const 'dropout_1/cond/mul/y'> 1
    <Const 'flatten_1/stack/0'> 1
    <Const 'flatten_1/Const'> 1
    <Const 'flatten_1/strided_slice/stack_2'> 1
    <Const 'flatten_1/strided_slice/stack_1'> 1
    <Const 'flatten_1/strided_slice/stack'> 1
    <Const 'merge_1/concat/axis'> 1
    <Const 'conv2d_3/bias'> 1
    <Identity 'conv2d_3/bias/read'> 1
    <Const 'conv2d_3/kernel'> 1
    <Identity 'conv2d_3/kernel/read'> 1
    <Const 'conv2d_2/bias'> 1
    <Identity 'conv2d_2/bias/read'> 1
    <Const 'conv2d_2/kernel'> 1
    <Identity 'conv2d_2/kernel/read'> 1
    <Const 'conv2d_1/bias'> 1
    <Identity 'conv2d_1/bias/read'> 1
    <Const 'conv2d_1/kernel'> 1
    <Identity 'conv2d_1/kernel/read'> 1
    <Const 'reshape_1/Reshape/shape/3'> 1
    <Const 'reshape_1/Reshape/shape/2'> 1
    <Const 'reshape_1/Reshape/shape/1'> 1
    <Const 'reshape_1/strided_slice/stack_2'> 1
    <Const 'reshape_1/strided_slice/stack_1'> 1
    <Const 'reshape_1/strided_slice/stack'> 1
    <Const 'embedding_1/embeddings'> 1
    <Identity 'embedding_1/embeddings/read'> 1
    <Placeholder 'input'> 1
    <Gather 'embedding_1/Gather'> 1
    <Shape 'reshape_1/Shape'> 1
    <StridedSlice 'reshape_1/strided_slice'> 1
    <Pack 'reshape_1/Reshape/shape'> 1
    <Reshape 'reshape_1/Reshape'> 1
    <Conv2D 'conv2d_3/convolution'> 1
    <BiasAdd 'conv2d_3/BiasAdd'> 1
    <Relu 'conv2d_3/Relu'> 1
    <MaxPool 'max_pooling2d_3/MaxPool'> 1
    <Conv2D 'conv2d_2/convolution'> 1
    <BiasAdd 'conv2d_2/BiasAdd'> 1
    <Relu 'conv2d_2/Relu'> 1
    <MaxPool 'max_pooling2d_2/MaxPool'> 1
    <Conv2D 'conv2d_1/convolution'> 1
    <BiasAdd 'conv2d_1/BiasAdd'> 1
    <Relu 'conv2d_1/Relu'> 1
    <MaxPool 'max_pooling2d_1/MaxPool'> 1
    <ConcatV2 'merge_1/concat'> 1
    <Shape 'flatten_1/Shape'> 1
    <StridedSlice 'flatten_1/strided_slice'> 1
    <Prod 'flatten_1/Prod'> 1
    <Pack 'flatten_1/stack'> 1
    <Reshape 'flatten_1/Reshape'> 1
    <Switch 'dropout_1/cond/Switch_1'> 2
    <Switch 'dropout_1/cond/mul/Switch'> 2
    <Mul 'dropout_1/cond/mul'> 1
    <RealDiv 'dropout_1/cond/dropout/div'> 1
    <Shape 'dropout_1/cond/dropout/Shape'> 1
    <RandomUniform 'dropout_1/cond/dropout/random_uniform/RandomUniform'> 1
    <Mul 'dropout_1/cond/dropout/random_uniform/mul'> 1
    <Add 'dropout_1/cond/dropout/random_uniform'> 1
    <Add 'dropout_1/cond/dropout/add'> 1
    <Floor 'dropout_1/cond/dropout/Floor'> 1
    <Mul 'dropout_1/cond/dropout/mul'> 1
    <Merge 'dropout_1/cond/Merge'> 2
    <MatMul 'output/MatMul'> 1
    <BiasAdd 'output/BiasAdd'> 1
    <Softmax 'output/Softmax'> 1
    FLOAT tensor with shape [1, 3]
    0.31037384 0.3381918 0.35143432 
    Process finished with exit code 0