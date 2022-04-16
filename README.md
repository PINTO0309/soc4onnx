# [WIP] soc4onnx
A very simple tool that forces a change in the opset of an ONNX graph. **S**imple **O**pset **C**hanger for **ONNX**.

![image](https://user-images.githubusercontent.com/33194443/163655662-622b470c-c893-439a-82b0-85bd6a406647.png)
```bash
$ soc4onnx \
--input_onnx_file_path NonMaxSuppression.onnx \
--output_onnx_file_path NonMaxSuppression_13.onnx \
--opset 13
```
![image](https://user-images.githubusercontent.com/33194443/163655699-b456b01b-957a-40f6-9703-547c1769f8d8.png)
