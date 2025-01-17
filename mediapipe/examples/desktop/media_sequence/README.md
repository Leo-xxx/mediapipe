# Preparing data sets for machine learning with MediaPipe
We include two pipelines to prepare data sets for training TensorFlow models.

Using these data sets is split into two parts. First, the data set is
constructed in with a Python script and MediaPipe C++ binary. The C++ binary
should be compiled by the end user because the preparation for different data
sets requires different MediaPipe calculator dependencies. The result of running
the script is a data set of TFRecord files on disk. The second stage is reading
the data from TensorFlow into a tf.data.Dataset. Both pipelines can be imported
and support a simple call to as_dataset() to make the data available.

### Demo data set
To generate the demo dataset you must have Tensorflow [version >= 1.19]
installed. Then the media_sequence_demo binary must be built from the top
directory in the mediapipe repo and the command to build the data set must be
run from the same directory.
```
bazel -c opt mediapipe/examples/desktop/media_sequence:media_sequence_demo \
  --define=MEDIAPIPE_DISABLE_GPU=1

python -m mediapipe.examples.desktop.media_sequence.demo_dataset \
  --alsologtostderr \
  --path_to_demo_data=/tmp/demo_data/ \
  --path_to_mediapipe_binary=bazel-bin/mediapipe/examples/desktop/\
media_sequence/media_sequence_demo  \
  --path_to_graph_directory=mediapipe/graphs/media_sequence/
```

### Charades data set

The Charades data set is ready for training and/or evaluating action recognition
models in TensorFlow. You may only use this script in ways that comply with the
Allen Institute for Artificial Intelligence's [license for the Charades data
set.](https://allenai.org/plato/charades/license.txt)

To generate the Charades dataset you must have Tensorflow [version >= 1.19]
installed. Then the media_sequence_demo binary must be built from the top
directory in the mediapipe repo and the command to build the data set must be
run from the same directory.

```
bazel -c opt mediapipe/examples/desktop/media_sequence:media_sequence_demo \
  --define=MEDIAPIPE_DISABLE_GPU=1

python -m mediapipe.examples.desktop.media_sequence.charades_dataset \
  --alsologtostderr \
  --path_to_charades_data=/tmp/charades_data/ \
  --path_to_mediapipe_binary=bazel-bin/mediapipe/examples/desktop/\
media_sequence/media_sequence_demo  \
  --path_to_graph_directory=mediapipe/graphs/media_sequence/
```
