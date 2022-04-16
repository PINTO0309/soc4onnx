# soc4onnx
A very simple tool that forces a change in the opset of an ONNX graph. **S**imple **O**pset **C**hanger for **ONNX**.

https://github.com/PINTO0309/simple-onnx-processing-tools

[![Downloads](https://static.pepy.tech/personalized-badge/soc4onnx?period=total&units=none&left_color=grey&right_color=brightgreen&left_text=Downloads)](https://pepy.tech/project/soc4onnx) ![GitHub](https://img.shields.io/github/license/PINTO0309/soc4onnx?color=2BAF2B) [![PyPI](https://img.shields.io/pypi/v/soc4onnx?color=2BAF2B)](https://pypi.org/project/soc4onnx/) [![CodeQL](https://github.com/PINTO0309/soc4onnx/workflows/CodeQL/badge.svg)](https://github.com/PINTO0309/soc4onnx/actions?query=workflow%3ACodeQL)

## 1. Setup
### 1-1. HostPC
```bash
### option
$ echo export PATH="~/.local/bin:$PATH" >> ~/.bashrc \
&& source ~/.bashrc

### run
$ pip install -U onnx \
&& python3 -m pip install -U onnx_graphsurgeon --index-url https://pypi.ngc.nvidia.com \
&& pip install -U soc4onnx
```
### 1-2. Docker
```bash
### docker pull
$ docker pull pinto0309/soc4onnx:latest

### docker build
$ docker build -t pinto0309/soc4onnx:latest .

### docker run
$ docker run --rm -it -v `pwd`:/workdir pinto0309/soc4onnx:latest
$ cd /workdir
```

## 2. CLI Usage
```bash
$ soc4onnx -h

usage:
    soc4onnx [-h]
    --input_onnx_file_path INPUT_ONNX_FILE_PATH
    --output_onnx_file_path OUTPUT_ONNX_FILE_PATH
    --opset OPSET
    [--non_verbose]

optional arguments:
  -h, --help
        show this help message and exit

  --input_onnx_file_path INPUT_ONNX_FILE_PATH
        Input onnx file path.

  --output_onnx_file_path OUTPUT_ONNX_FILE_PATH
        Output onnx file path.

  --opset OPSET
        opset number to be changed. e.g. --opset 11

  --non_verbose
        Do not show all information logs. Only error logs are displayed.
```

## 3. In-script Usage
```python
$ python
>>> from soc4onnx import change
>>> help(change)
Help on function change in module soc4onnx.onnx_opset_change:

change(
  opset: int,
  input_onnx_file_path: Union[str, NoneType] = '',
  output_onnx_file_path: Union[str, NoneType] = '',
  onnx_graph: Union[onnx.onnx_ml_pb2.ModelProto, NoneType] = None,
  non_verbose: Union[bool, NoneType] = False
) -> onnx.onnx_ml_pb2.ModelProto

    Parameters
    ----------
    opset: int
        opset number to be changed.
        e.g. --opset 11

    input_onnx_file_path: Optional[str]
        Input onnx file path.
        Either input_onnx_file_path or onnx_graph must be specified.

    output_onnx_file_path: Optional[str]
        Output onnx file path.
        If output_onnx_file_path is not specified, no .onnx file is output.

    onnx_graph: Optional[onnx.ModelProto]
        onnx.ModelProto.
        Either input_onnx_file_path or onnx_graph must be specified.
        onnx_graph If specified, ignore input_onnx_file_path and process onnx_graph.

    non_verbose: Optional[bool]
        Do not show all information logs. Only error logs are displayed.
        Default: False

    Returns
    -------
    changed_graph: onnx.ModelProto
        opset changed onnx ModelProto
```

## 4. CLI Execution
```bash
$ soc4onnx \
--input_onnx_file_path NonMaxSuppression.onnx \
--output_onnx_file_path NonMaxSuppression_13.onnx \
--opset 13
```

## 5. In-script Execution
```python
from soc4onnx import change

changed_graph = change(
    onnx_graph=graph,
    opset=13,
    non_verbose=True,
)
```

## 6. Sample
![image](https://user-images.githubusercontent.com/33194443/163655662-622b470c-c893-439a-82b0-85bd6a406647.png)
```bash
$ soc4onnx \
--input_onnx_file_path NonMaxSuppression.onnx \
--output_onnx_file_path NonMaxSuppression_13.onnx \
--opset 13
```
![image](https://user-images.githubusercontent.com/33194443/163655699-b456b01b-957a-40f6-9703-547c1769f8d8.png)
