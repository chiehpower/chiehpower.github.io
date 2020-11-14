---
title: 視覺化神經網路
description: <center> 最強的神經網路視覺化工具推薦！</center>
photos:
  - 'https://lh3.googleusercontent.com/CNGadXHRhaptvYqiuLTDcIJrGPIjY2HI_ihJl8UU_qCz6aVFZ-0IM8SP4K4XC5RUh74FICkvEbZWJ6Q6HposYYbbBgIO08JV7i3YlQPO1eH3qHun2QVAaYF6IigbYyxM4ZqnUpvSN_H--0YHZGeT-xRryRSUFI3j9Fn9JJSJfc5qskvPvkoHWRjunrEis1U1dPjRq90bawY3LEUGnmE7SqhHApm8HAx0xv-kzUJqHSiEpYi2Z1CGEsr3BJEUa0hj6KqzVIV5x_WsmbuXueM07dgrgwWFbTxRzIhwGtuctFd_pIotOk340n6VbddYnorR8IFkluMSrd_z11eNGto-mGSFvh_kLIB0ZvyVVkogarbvcT82acnkv7OpLmv14or5d8TuQZk1suxZOljNNlYbTRYXLotzf5f9Qk3m06cnlUac5tgVjTBm1G3zvyAJfOAyFCxg1hv52s6niJgGkI-dDdN9gCAwxqc5xE4mKrLowy9AefiM1iBZqeyOJCXC4MDC-0e_BYDpYGeHcyw6Bm-8_EQZxrVnj-qVtXSRmWsuIofdEX3Vf_kuDVy_X8d6co427f2BfnaiNIxsoogRzyoAFumk9HnGmFk7NXkDIb4RQST9aH7RZjCqIvHcwLOLDBzzVFNq3TcIctDBAwbT8xw4EvWOyyYeI1haxZC67JkMarBU_os0jestLnplsYpC_0Wcf3z2MsqezJoRQNoVQ1OgDmpP2dzusJS8GvoRqKMbfgQUiLcTYw=w2162-h1218-no'
date: 2019-12-28 12:23:34
tags: [Share, Notes, Record, Tools, Netron, PlotNeuralNet, NN-SVG, Netscope]
categories: Share
password:
---
<br>
# Introduction
<br>
視覺化已然成為一個數據工程師或科學家必備的一項技能，我覺得算是一種軟實力，畢竟你沒有用它不會怎麼樣，但用了就可以把你的結果往上提升不只一個檔次。
學習如何化繁為簡，在最短的時間用最快最簡單的方式來呈現自己想要表達的內容。

在文獻當中，時常會看到作者們把自家的神經網路給具現化，非常清楚地呈現出神經網路裡的架構。
前陣子看到一篇post剛好在介紹這部分(請參考[這篇](https://bangqu.com/675733.html))，自己也試了之後發現非常好用，因此想來分享一下使用的心得和經驗。

一般使用TensorFlow的人可以使用內建的TensorBoard來plot神經網路圖，但個人覺得不太好用，有幾個點是：
1. 需要在code內寫入一些特定的寫法，才能讓Tensorflow在TensorBoard中顯現。
2. 他的視覺化其實頗不美觀。
3. 非常侷限，若是用其他深度學習框架則無法使用。
4. 不方便操作。

---
# [Netron](https://lutzroeder.github.io/netron/)
<br>
![netron_used](/images/netron_used.gif)
- GitHub : https://github.com/lutzroeder/netron

個人覺得這款視覺化軟體，是最強大的。
1. 他支援非常多的模型格式，同時也支援非常多的深度學習框架，可以說接受度是非常的高。
2. 操作使用上非常容易、簡單。
3. 支援多個系統平台，包含Windows、Linux、MacOS，甚至可以直接Online在Website上做視覺化操作。
4. 可以Export，包含SVG、Png格式的圖。
5. 可看見神經網路中的detail information。

> Netron supports ONNX (.onnx, .pb, .pbtxt), Keras (.h5, .keras), Core ML (.mlmodel), Caffe (.caffemodel, .prototxt), Caffe2 (predict_net.pb, predict_net.pbtxt), MXNet (.model, -symbol.json), ncnn (.param) and TensorFlow Lite (.tflite).
> Netron has experimental support for TorchScript (.pt, .pth), PyTorch (.pt, .pth), Torch (.t7), Arm NN (.armnn), BigDL (.bigdl, .model), Chainer, (.npz, .h5), CNTK (.model, .cntk), Deeplearning4j (.zip), Darknet (.cfg), ML.NET (.zip), MNN (.mnn), OpenVINO (.xml), PaddlePaddle (.zip, __model__), scikit-learn (.pkl), TensorFlow.js (model.json, .pb) and TensorFlow (.pb, .meta, .pbtxt).
> Source from : https://github.com/lutzroeder/netron

只需要直接import你的模型檔案，讓程式解析模型你的一下(解析時間取決於你的模型複雜度)，就可以直接把你的神經網路視覺化。
他的接受度非常高，例如有Tensorflow的pb檔、pytorch的onnx檔、caffe、cfg等等，一放進去就可以看見神經網路的架構細節，包含input/output name，type等等。
我這要補充一下，例如在操作TensorRT的時候，當我們在進行parser模型的時候，這些資訊就相當重要，但有時候你並不會非常清楚每一個檔案內的所有detail，理由是有些model是我們直接由github上取得現成的拿來使用，因此可以透過這個網站讓我們馬上理解模型的架構資訊。
![netron](/images/netron.png "Model Properties")

當我們視覺化完成之後，可以把他export出png或svg檔，相當方便！！
![ssd_mobile](/images/ssd_mobilenet_v1_coco_2018_01_28.png "SSD mobilenet v1")

不過當你的神經網路如果大到什麼上百MB那種，基本上下載下來的png檔已經很難細看清楚每一個神經元。
他有網頁版和離線版本，如果你的檔案是小的，可以直接使用網頁版本非常方便，但如果你的模型檔案有些大，建議可以使用離線版本，這樣在處理你的模型時比較不會造成瀏覽器的崩潰。

(使用例子是[ssd_mobilenet_v1_coco_2018_01_28](https://drive.google.com/file/d/1CJKUu5pXgzWtcw2DpfwCtv4eedBJa1dg/view?usp=sharing)，我在這邊提供一個模型僅供大家來快速練習和測試他的效果用。)


---
# [PlotNeuralNet](https://github.com/HarisIqbal88/PlotNeuralNet)
<br>
這款是屬於3D神經網路視覺化工具，他的操作就會比較複雜一點，必須要自行寫神經網路裡面的架構，不過他的效果非常的好，例如以下是github上他們展示的範例。
![example](https://user-images.githubusercontent.com/17570785/50308911-03b3c380-049d-11e9-92d9-ce15669017ad.png)

其實中有用python來產生的，也有可用tex格式的，這個應該就是可以直接用在一般latex裡面，例如在寫期刊時直接原生放入(?)
這部分還未測試，不過是一個很不錯的工具！值得推薦！

---
# [NN-SVG](http://alexlenail.me/NN-SVG/)
<br>
- GitHub : https://github.com/alexlenail/NN-SVG

這款就比較初階一點，能夠自訂的部分非常少，大概就是拿來當作很入門的介紹使用之類的。

---
# [Netscope](https://dgschwend.github.io/netscope/quickstart.html)
<br>
Netscope其實視覺化的效果不錯，也頗美觀，可惜他支持caffe的格式，所以如果你有想要呈現的結構，可能需要先轉一下他所支援的格式架構才可以。

---
# Reference
- [一圖抵千言 | 神經網絡繪圖篇！涵蓋NN-SVG、PlotNeuralNet、Netron等軟件！](https://bangqu.com/675733.html)

<br>
如果有什麼新的或覺得不錯的視覺化工具，歡迎分享給我！！
有其他問題的歡迎留言或來信。
