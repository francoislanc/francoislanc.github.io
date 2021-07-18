+++
title = "Audio classification on FM radio broadcasts :radio: "
description = ""
tags = [
    "classification",
    "sdr",
    "gnuradio",
    "machine learning"
]
date = "2021-07-18"
+++

The transmitted FM signal is received by using a simple RTL-SDR dongle, which provides the baseband FM modulated signal. This signal is demodulated with GNURadio and then a deep learning model classifies the audio segments into three different classes : music, speech, and ads.
{{< youtube 2eyaEt0B1Nw >}}

Developed with a RTL-SDR USB dongle, [GNURadio](https://www.gnuradio.org/), [gr-osmosdr](https://osmocom.org/projects/gr-osmosdr/wiki), and [PANNs,  Pretrained Audio Neural Networks for Audio Pattern Recognition](https://github.com/qiuqiangkong/audioset_tagging_cnn).  
